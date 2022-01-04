###### window.location.reload刷新页面
###### process.nexttick()ES6定时器
###### string.includes(searchvalue, start)查找是否含有子字符串
###### $(selector).serialize()创建以标准 URL 编码表示的文本字符串(jQuery)
###### e.stopPropagation()阻止冒泡捕获
###### e.preventDefault();阻止默认事件
###### window.screen.availWidth获取屏幕宽度
###### document.documentElement.clientWidth页面dom宽度
###### react在新页面跳转用window.open
###### 排序arr.sort((a,b)=>{return a.s-b.s})
###### 用scroll({ top: elOffsetTop, behavior: "smooth" });代替el.scrollIntoView({ behavior: "smooth" });滚动条滚动到可视区域
###### 监听esc键盘事件用不用onkeydown，onkeyup，onkeypress，用onresize去监听
###### 标题在固定宽里两端对齐  text-align-last: justify;
###### 加载同一模块的不同版本  npm install echarts4@npm:echarts@^4.7.0

###### webWorker:
~~~~ts
/**
 * 新开线程处理倒计时任务
 * 定义新线程：const worker = newWorkerForTime(60);
 * 通信传值：worker.onmessage = ({ data }) => {};
 * 杀死线程：worker.terminate();
 **/
const newWorkerForTimes = (time: number): Worker => {
  const webWorkerFile: string = `
     let time = ${time};
     const interval = setInterval(() => {
        postMessage(--time);
        time === 0 && clearInterval(interval);
     }, 1000);`;
  const file = new Blob([webWorkerFile]); //将代码转化成文件
  return new Worker(window.URL.createObjectURL(file)); //将文件放入到新的线程中
};

export default newWorkerForTimes;
~~~~
###### 睡眠
~~~~js
function sleep(time) {
  return new Promise((resolve) => setTimeout(resolve, time))
}
~~~~
##### cookie设置
~~~~ts
import config from '../../config';

export function getCookie(cookieName: string) {
  const name = cookieName + '=';
  const cookies = document.cookie.split(';');
  for (let i = 0; i < cookies.length; i++) {
    const c = cookies[i].trim();
    if (c.indexOf(name) == 0) {
      return c.substring(name.length, c.length);
    }
  }
  return '';
}

export function setCookie(cookieName: string, cookieValue: string) {
  document.cookie = `${cookieName}=${cookieValue}; expires=Thu, 18 Dec 2043 12:00:00 GMT;domain=${config.COOKIE_DOMAIN};path=/`;
}
~~~~
##### 去重
~~~~js
export function duplicateRemoval(data = []) {
  const set = new Set();
  data.forEach((item) => set.add(item));
  return [...set];
}
~~~~
##### copy
~~~~js
export function copyText(value) {
  const oInput = document.createElement('input');
  oInput.value = value;
  document.body.appendChild(oInput);
  oInput.select();
  document.execCommand('Copy');
  oInput.className = 'oInput';
  oInput.style.display = 'none';
  message.success('复制成功', 1);
}
~~~~
