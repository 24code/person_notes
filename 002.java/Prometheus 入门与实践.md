# Prometheus 入门与实践
## 原理解析
- server pull from client and gateway
- customize metric,just satisfic text regx([a-zA-Z_:][a-zA-Z0-9_:]*)
- four metric type, Counter Gauge Histogram Summary
- 通过接入grafana , 显示单位时间内的指标
## 开源项目解读
### [canal Prometheus](https://github.com/alibaba/canal/wiki/Prometheus-QuickStart)
1. 对于 sink,meta,entry,parse,store 都定义metics,label
2. embedCanalServer start stop 时,进行prometheus collectors to register or unregister
## 参考资料
[Prometheus 入门与实践](https://www.ibm.com/developerworks/cn/cloud/library/cl-lo-prometheus-getting-started-and-practice/index.html)
