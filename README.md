# bili2toot

A simple script that transport dynamic from bilibili to Mastodon. Based on the Twitter RSS feed powered by [RSSHub](https://rsshub.app).

一个将bilibili动态搬运到长毛象的脚本——基于[RSSHub](https://rsshub.app)生成的B站动态RSS。

<details>
  <summary>PS. 动态中的表情处理方法</summary>
  
  B 站动态里的表情处理是一个比较麻烦的事情，RSSHub的默认处理方法是将表情转成　`<img>`，这样会导致 bili2toot 误将表情作为图片上传，为了解决这个问题，对 RSSHub 进行了一些改造（[mashirozx/RSSHub](https://github.com/mashirozx/RSSHub)，一键部署：[Dockerhub](https://hub.docker.com/r/mashirozx/rsshub)），相对原有路由 `/bilibili/user/dynamic/:uid`，新增一个路由 `/bilibili/user/dynamic_mstdn/:uid` 来对表情处理，将在 RSS 订阅中直接将表情转为 Mastodon 的短代码，mastodon短代码和bilibili原有短代码映射储存在一个外部的 json 文件中，具体原理可以看[这里](https://github.com/mashirozx/RSSHub/blob/32d9e593a646087c580a6e894e26628f2011f306/lib/routes/bilibili/dynamic_mstdn.js#L80)，而json文件及转换脚本都放这个仓库里了：[mashirozx/bilibili_emojis](https://github.com/mashirozx/bilibili_emojis)，需要用到的表情包都打包到该仓库的四个 `.tar.gz` 文件中了，可用tootctl直接导入，不过请留意表情前缀，`emoji.tar.gz` 须加上 `bili_emoji_` 前缀，剩下三个须加上 `bili_` 前缀。
</details>

```
pip3 install -r requirements.txt
cp conf.sample.ini conf.ini
nano conf.ini
python3 run.py
```

crontab job setting:
```
crontab -e
```
or (Ubuntu 18.04)
```
nano /etc/crontab
/etc/init.d/cron restart
```

Recommand do job hourly:
```
#m h dom mon dow user  command
13 *    * * *   root    cd /bili2toot && python3 run.py
```
