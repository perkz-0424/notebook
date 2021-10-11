~~~~js
import html2canvas from "html2canvas";
import {jsPDF} from "jspdf";

export default class H5Handle<T> {
  public canvasOptions: any;
  constructor() {
    this.canvasOptions = {
      useCORS: true,
      allowTaint: true,
      scale: window.devicePixelRatio
    }
  }
  downloadFile  (fileName, content)  {
    const aLink = document.createElement("a");
    const blob = this.base64ToBlob(content);
    const evt = document.createEvent("HTMLEvents");
    evt.initEvent("click", true, true);
    aLink.download = fileName;
    aLink.href = URL.createObjectURL(blob);
    aLink.dispatchEvent(new MouseEvent("click", {bubbles: true, cancelable: true, view: window}));//兼容火狐
    aLink.remove();
  }
  base64ToBlob  (code)  {
    const parts = code.split(";base64,");
    const contentType = parts[0].split(":")[1];
    const raw = window.atob(parts[1]);
    const rawLength = raw.length;
    const uInt8Array = new Uint8Array(rawLength);
    for (let i = 0; i < rawLength; ++i) {
      uInt8Array[i] = raw.charCodeAt(i);
    }
    return new Blob([uInt8Array], {type: contentType});
  }
  //直接打印pdf(小页面)
  getPdf  (target, type, cb, name = "pdf报告")  {
    html2canvas(target, this.canvasOptions)
      .then(canvas => this.compress(canvas.toDataURL("image/jpeg", 1), 1, (blob, w, h) => this.canvasToPdf(blob, w, h, type, cb, name)));
  };
  //分割打印
  getPdfByDivision  (ids: any, fileName: string, type = "download", cb?)  {
    //分割图片
    Promise.all(ids.map((item: any, index: number) => {
      return new Promise((resolve) => {
        this.getImage(document.getElementById(item), false, `page${index}.jpeg`).then(data => resolve({data, index}));
      })
    })).then(imageArray => {
      //整理图片信息
      return Promise.all(([...imageArray].sort((a: any, b: any) => (a.index - b.index))).map((item: any, index: number) => {
        return new Promise((resolve: any) => {
          const img = document.createElement("img");
          img.src = item.data;
          img.onload = () => {
            const info = {height: img.height, width: img.width, image: img}
            return resolve(info);
          }
        })
      }))
    }).then((infos: any) => {
      //重新拼接图片
      let heights = 0;
      const canvas = document.createElement("canvas");
      infos.forEach((item: any) => heights += item.height);
      canvas.width = infos[0].width;
      canvas.height = heights;
      const context = canvas.getContext("2d");
      let y = 0;
      infos.forEach((item) => {
        context.drawImage(item.image, 0, y, item.width, item.height);
        y += item.height;
      });
      const newImage = canvas.toDataURL("image/jpeg", 1);
      this.canvasToPdf(newImage, infos[0].width, heights, type, cb, fileName);
    })
  }
  //获取图片(下载图片)
  getImage (target, isDown = false, fileName?)  {
    return html2canvas(target, this.canvasOptions)
      .then(canvas => {
        isDown && this.downloadFile(fileName, canvas.toDataURL("image/jpeg", 1));
        return canvas.toDataURL("image/jpeg", 1);
      })
  }
  //压缩图片
  compress (base64, rate = 1.2, callback) {
    const img = new Image();
    img.src = base64;
    img.onload = function () {
      const canvas = document.createElement("canvas");
      const ctx = canvas["getContext"]("2d");
      const ratio = 1;
      const w = img.width;
      const h = img.height;
      canvas.setAttribute("width", `${w * ratio}`);
      canvas.setAttribute("height", `${h * ratio}`);
      ctx.scale(ratio, ratio);
      canvas.getContext("2d").drawImage(img, 0, 0, w, h);
      const base64 = canvas.toDataURL("image/jpeg");
      canvas.toBlob(function (blob) {
        // blob.size > 10005000 ? compress(base64, rate, callback) : callback(base64, w, h);//压缩
        callback(base64, w, h);
        canvas.remove();
        img.remove();
      }, "image/jpeg");
    };
  };
  //输出pdf
  canvasToPdf (base64, w, h, type, cb, name) {
    const r = h / w;
    const PDF = new jsPDF("p", "pt", "a4");
    if (r <= 841.89 / 595.28) {
      PDF.addImage(base64, "JPEG", 0, 0, 595.28, 595.28 * r);
    } else {
      const pdfPageH = 595.28 * r;
      const pages = Math.ceil(pdfPageH / 841.89);//一共多少页
      let i = 0;
      while (i < pages) {
        PDF.addImage(base64, "JPEG", 0, -i * 841.89, 595.28, 595.28 * r);
        i !== pages - 1 && PDF.addPage();
        i++;
      }
    }
    switch (type) {
      case "download"://下载pdf文档
        PDF.save(`${name}.pdf`);
        cb && cb(PDF.output("blob"));
        break;
      case "save"://保存pdf文档
        const report = PDF.output("blob");
        const reader = new FileReader();
        reader.readAsDataURL(report);
        reader.onload = () => {
          cb && cb({name: `${name}.pdf`, size: report.size, file: reader.result});
        };
        break;
      default:
        PDF.save(`${name}.pdf`);
        cb && cb(PDF.output("blob"));
        break;
    }
  };
}
~~~~