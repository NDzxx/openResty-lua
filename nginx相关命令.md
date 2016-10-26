#nginx 服务器命令
```
nginx -s reload ：修改配置后重新加载生效  
nginx -s reopen ：重新打开日志文件  

测试nginx配置文件是否正确关闭nginx
nginx -t -c /path/to/nginx.conf 
nginx -s stop 快速停止nginx
quit 完整有序的停止nginx其他的停止nginx 方式：ps -ef | grep nginx  
kill -QUIT 主进程号 ：从容停止Nginx
kill -TERM 主进程号 ：快速停止Nginx
pkill -9 nginx ：强制停止Nginx
启动nginx:nginx -c /path/to/nginx.conf  
平滑重启nginx：kill -HUP 主进程号

启动：
PATH=/usr/local/openresty/nginx/sbin:$PATH 
export PATH
nginx -p `pwd`/ -c conf/nginx.conf


win下使用nginx改为对应目录的nginx.exe

调试:
http://notebook.kulchenko.com/zerobrane/debugging-openresty-nginx-lua-scripts-with-zerobrane-studio


http://www.tuicool.com/articles/u2YzA3z

```