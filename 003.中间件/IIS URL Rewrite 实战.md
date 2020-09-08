# IIS URL Rewrite 实战
## 代理 server 80 到 3000,解决前端mock调试时,跨域访问问题
## 问题
1. rewrite 配置规则复杂,不清晰
2. iis rewrite 代理层级 -- server层,website层
3. 安装 Application Request Routing (ARR) 和 url rewrite 组件

## 参考
- [How to Enable URL Rewrite in IIS 8.5/8/7](https://tecadmin.net/enable-url-rewrite-iis/)
- [Reverse Proxy with URL Rewrite v2 and Application Request Routing](https://docs.microsoft.com/en-us/iis/extensions/url-rewrite-module/reverse-proxy-with-url-rewrite-v2-and-application-request-routing?source=post_page-----a2ab7e4fee59----------------------)
- [The Very Common Mistakes When Using IIS URL Rewrite Module](https://blog.lextudio.com/the-very-common-mistakes-when-using-iis-url-rewrite-module-a2ab7e4fee59)
- [Creating Rewrite Rules for the URL Rewrite Module](https://docs.microsoft.com/en-us/iis/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module)
