### 加密
~~~~js
/****
 * 加密函数
 * 用于文件
 * 用来加密登录和验证
 * ***/
import CryptoJS from "crypto-js";

//密钥
const _key = CryptoJS.enc.Utf8.parse("18340313259");

//加密
const _encrypt = (msgString) => {
  const iv = CryptoJS.lib.WordArray.random(16);
  const encrypted = CryptoJS.AES.encrypt(msgString, _key, { iv });
  return iv.concat(encrypted.ciphertext).toString(CryptoJS.enc.Base64);
};

//解密
const _decrypt = (cipherTextStr) => {
  const cipherText = CryptoJS.enc.Base64.parse(cipherTextStr);
  const iv = cipherText.clone();
  iv.sigBytes = 16;
  iv.clamp();
  cipherText.words.splice(0, 4);
  cipherText.sigBytes -= 16;
  const decrypted = CryptoJS.AES.decrypt({ ciphertext: cipherText }, _key, { iv, });
  return decrypted.toString(CryptoJS.enc.Utf8);
};

export {
  _encrypt,
  _decrypt
~~~~