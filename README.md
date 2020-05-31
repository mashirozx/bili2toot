# bili2toot

A simple script that transport dynamic from bilibili to Mastodon. Based on the Twitter RSS feed powered by [RSSHub](https://rsshub.app).

一个将bilibili动态搬运到长毛象的脚本——基于[RSSHub](https://rsshub.app)生成的B站动态RSS。

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