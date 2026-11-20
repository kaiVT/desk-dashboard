# Desk 看板

iPhone 主屏幕用的 desk dashboard：纽约时间、Reston, VA 天气，还有一组美股自选行情。

## 怎么当成 app 用

1. 用 iPhone 的 **Safari** 打开 GitHub Pages 链接。
2. 点底部分享按钮，选 **添加到主屏幕**。
3. 从主屏幕打开后会全屏显示，不会带 Safari 工具栏。

## 改自选股

打开 `app.js` 最上面的 `WATCHLIST` 列表，增删 ticker 即可。页面只展示代码和市场价格，不会显示持股数量或市值。

`scripts/fetch_prices.py` 里有一份同样的列表，改的时候两处一起改，备份行情才会跟上。

## 行情从哪来

- 手机端每 60 秒直接向 CNBC 的公开 quote 接口拉价格，不需要 API key，也不会消耗 AI token。
- 如果浏览器被 CORS / 广告拦截挡住，会改用仓库里的 `prices.json`。
- GitHub Action 每 15 分钟刷新一次 `prices.json`（也可在 Actions 里手动跑 `Refresh prices`）。

天气来自 [Open-Meteo](https://open-meteo.com/)，同样免费、不用 key。时钟是 `America/New_York`。

## 本地预览

在项目目录开一个静态服务器，例如：

```bash
python3 scripts/generate_icons.py
python3 scripts/fetch_prices.py
python3 -m http.server 8080
```

然后打开 `http://127.0.0.1:8080`。
