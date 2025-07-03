## 什么是无头浏览器
没有图形用户界面（GUI）的浏览器。它可以在后台像正常浏览器一样加载网页、执行 JavaScript、操作 DOM，只是不显示界面。

## 对比浏览器主要用途
- 自动化任务，非常适合爬虫
```javascript
// 安装 puppeteer: npm install puppeteer
const puppeteer = require('puppeteer');

(async () => {
  const browser = await puppeteer.launch(); // 默认是无头模式
  const page = await browser.newPage();
  await page.goto('https://example.com');

  const title = await page.title();
  console.log('网页标题是：', title);

  await browser.close();
})();

```
- 相比浏览器开，多开几个tab cpu拉满，headless更轻量，性能更好