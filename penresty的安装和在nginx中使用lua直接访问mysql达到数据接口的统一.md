# nginx中使用lua直接访问mysql达到数据接口的统一

OpenResty的安装：

安装nginx 中 rewrite模块等需要的插件：

apt-get install libreadline-dev libpcre3-dev libssl-dev perl build-essential下载最新版的OpenRestyhttp://openresty.org/wget http://openresty.org/download/ngx_openresty-1.2.7.1.tar.gztar -xvf nngx_openresty-1.2.7.1.tar.gzmv nngx_openresty-1.2.7.1 /usr/local/openresty-1.2.7.1cd openresty-1.2.7.1./configure --with-luajit --prefix=/usr/local/openrestymake & make install

这样基本就可以把nginx基本的第三方库安装进去

在/to/nginx/conf 下修改配置文件nginx.config

location /hello {  default_type 'text/plain';  content_by_lua 'ngx.say("hello, lua")'; }

/to/nginx/sbin/nginx #启动nginx

或者/to/nginx/sbin/nginx –s reload #重启nginx访问localhost/hello会出现“hello,lua”

让nginx 中的nginx_lua_module支持mysql 和memcache下载https://github.com/agentzh/lua-resty-memcachedhttps://github.com/agentzh/lua-resty-mysql

对于访问接口的统一有很多的处理方式，这里介绍使用nginx lua 访问mysql并用memcache缓存起来。

```
location /getXxxInfo { default_type 'text/plain'; content_by_lua '  --先从memcache提取数据 local args = ngx.req.get_uri_args()  if args["appleid"] == nil then return end  local memcached = require "resty.memcached" local memc, err = memcached:new() if not memc then ngx.say("failed to instantiate memc: ", err) return end memc:set_timeout(1000) -- 1 sec  local ok, err = memc:connect("192.168.40.xxx", 11211) if not ok then ngx.say("failed to connect: ", err) return end local res, flags, err = memc:get(args["appleid"] ) if err then ngx.say("failed to get dog: ", err) return end  --数据不在memcache中 从数据库提取并放到memcache if not res then local mysql = require "resty.mysql" local db, err = mysql:new() if not db then ngx.say("failed to instantiate mysql: ", err) return end db:set_timeout(1000) -- 1 sec local ok, err, errno, sqlstate = db:connect{ host = "xxx.xxx.xx.xxx", port = 3306, database = "xxxx", user = "root", password = "xxxx", max_packet_size = 1024 * 1024  }  if not ok then ngx.say("failed to connect: ", err, ": ", errno, " ", sqlstate) return end --ngx.say("connected to mysql.")  sql = "select * from xxx where xxx = "..args["xxx"] res, err, errno, sqlstate = db:query(sql) if not res then ngx.say("bad result: ", err, ": ", errno, ": ", sqlstate, ".") return end local cjson = require "cjson" ngx.say(cjson.encode(res))  local ok, err = memc:set(args["xxxx"], cjson.encode(res)) if not ok then ngx.say("failed to set dog: ", err) return end local ok, err = db:set_keepalive(0, 100) if not ok then ngx.say("failed to set keepalive: ", err) return end return end ngx.say(res) memc:set_keepalive(0, 100)  '; } 


```