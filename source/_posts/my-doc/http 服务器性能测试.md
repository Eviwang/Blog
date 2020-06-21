http 服务器性能测试


压力测试
ab

ab -c 200 -n 1600 

-c 并发数

Request per second  QPS每秒多少个请求
Time per request  每次请求时间
Time per request  across all concurrent  requests 多久得到一个并发结果
Trasfer rate 吞吐量


性能瓶颈(linux 命令)
top 查看cpu
iostat 查看硬盘

工具：

1. node --prof entry.js

同时起一个压测服务(50个请求，压15秒)
ab -c50 -t15 http://localhost:3000

2. Chrome Profile
node --inspect-brk index.js
在浏览器中输入chrome://inspect
然后点击profile进行监控，同时开启压测服务


3. Clinic.js


