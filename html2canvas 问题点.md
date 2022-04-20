### html2canvas 问题点

1. 图片模糊问题

> https://juejin.cn/post/6844903826265210888

- 解决：不要把背景图做为 background 的元素添加，要插入 dom 里面。也就是 img 标签定位替代 div 设置 background

2. 跨域图片不显示

> https://blog.csdn.net/qq_39045645/article/details/115690019

- 解决：跨域图片资源都转 base64，因为 base64 资源在本地。

```js
// 获取图片 base64 地址
export const getImageBase64 = (url) => {
  return new Promise((resolve, reject) => {
    const image = new Image();

    image.crossOrigin = "anonymous"; // 支持跨域图片
    image.src = url;

    image.onload = () => {
      const canvas = document.createElement("canvas");
      canvas.width = image.width;
      canvas.height = image.height;
      const ctx = canvas.getContext("2d");
      ctx.drawImage(image, 0, 0, image.width, image.height);
      const base64DataURL = canvas.toDataURL("image/png");

      resolve(base64DataURL);
    };

    image.onerror = reject;
  });
};

// 使用
getAvatarImgBase64 = async () => {
  const imgUrl =
    "https://hysd-web-static-develop.shengdiudiu.com/image/mp/about.png";
  const imgBase64 = await getImageBase64(imgUrl);
  console.log({ imgBase64 });
};
```

3. ios 出现 The operation is insecure toDataUrl

> https://stackoverflow.com/questions/25753754/canvas-todataurl-security-error-the-operation-is-insecure

- 解决：设置图片允许跨域，并且写在设置 src 之前。

```js
image.crossOrigin = "anonymous"; // This enables CORS
image.src = url;
```
