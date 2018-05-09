![NewBlueFX](img/NewBlueFX_logo.png)

To output traditional web server access logs, use `--log.format` with any value (typically 'combined', 'dev' or 'tiny'). The format value supplied is passed directly to [morgan](https://github.com/expressjs/morgan).

```js
    logFormat: "tiny",
```
<!-- ```sh
$ ws --log.format tiny
Serving at http://newbluefx.local:8010, http://127.0.0.1:8010, http://192.168.0.100:8010
``` -->
```sh
GET / 304 - - 18.937 ms
GET /index.css 304 - - 24.106 ms
GET /css/font-awesome.min.css 304 - - 17.563 ms
GET /component/boxer-profile/boxer-profile.css 304 - - 18.342 ms
GET /component/boxer-list/boxer-list.css 304 - - 15.894 ms
GET /component/boxer-list/boxer-list-item.css 304 - - 13.983 ms
GET /component/bout-list-item/bout-list-item.css 304 - - 13.808 ms
GET /component/bout-list-item/fight-list-item.css 304 - - 1.957 ms
GET /page/videos-page.css 304 - - 1.714 ms
GET /page/video-page.css 304 - - 5.436 ms
GET /page/boxers-page.css 304 - - 6.774 ms
GET /component/twitter-summary/twitter-summary.css 304 - - 7.460 ms
GET /page/article-page.css 304 - - 8.443 ms
GET /component/org-list/org-list.css 304 - - 8.677 ms
GET /component/api-view/api-view.css 304 - - 8.663 ms
GET /node_modules/moment/min/moment.min.js 304 - - 8.369 ms
GET /node_modules/moment/locale/en-gb.js 304 - - 6.527 ms
GET /index.bundle.js 304 - - 6.157 ms
GET /component/boxer-profile/boxer-profile.js 304 - - 7.456 ms
```
