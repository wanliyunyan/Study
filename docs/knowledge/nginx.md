# nginx

## server

### listen 
监听的端口号

### charset
字符集 UTF-8

### access_log 访问日志
日志文件一般存放在 /var/log/nginx 下

### error_log 错误日志

### client_max_body_size
限制请求体的大小，若超过所设定的大小，返回 413 错误。

### gzip
    gzip  on;                 # 开启gzip功能
    gzip_min_length  1k;      # 响应页数据上限
    gzip_buffers     4 16k;   # 缓存空间大小
    gzip_comp_level 6;        # 设置压缩级别为6 设置gzip压缩程度，1-9级，越大，压缩程度越高，时间越久，一般折中选择
    gzip_types       text/plain application/x-javascript text/css application/xml text/javascript application/x-httpd-php application/javascript application/json; # 压缩文件类型
    gzip_disable "MSIE [1-6]\."; # IE 1-6关闭gzip压缩
    gzip_vary on;             # 启用压缩标识
    gunzip_static on;         # 检查预压缩文件

### location

```nginx configuration
    location / {
        root  /usr/src/app/; # root指令负责将匹配到的url与服务器中某个具体目录对应起来。
        index  index.html index.htm; # 会访问 /usr/src/app/ 下的 index.html / index.htm 文件
        try_files $uri $uri/ /index.html; #  当用户请求 http://localhost/example 时，这里的 $uri 就是/example。try_files 会到硬盘里尝试找这个文件。如果存在名为/$root/example（其中$root 是项目代码安装目录）的文件，就直接把这个文件的内容发送给用户。显然，目录中没有叫 example 的文件。然后就看 $uri/，增加了一个 /，也就是看有没有名为 /$root/example/的目录。又找不到，就会 fall back 到 try_files 的最后一个选项 /index.html


    location ~ ^/(images|javascript|js|css|static)/  { # ~ 正则表达式要区分大小写 
        root       /usr/src/app/;
        access_log  off;
        expires     30d; # 控制页面资源在浏览器缓存的时间
    }
    
    location /v1 {
        # add_header Access-Control-Allow-Origin '*';
        # add_header Access-Control-Allow-Methods 'GET, POST, OPTIONS';
        # add_header Access-Control-Allow-Headers 'DNT,X-Mx-ReqToken,Keep-Alive,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type,Authorization';
        proxy_pass https://****; # 用rewrite转发的话，url会发生变化的，那就用proxy_pass吧，于是添加了如下的配置：
        proxy_set_header   Host  $proxy_host; # 当Host设置为$http_host时，则不改变请求头的值，所以当要转发到bbb.example.com的时候，请求头还是aaa.example.com的Host信息，就会有问题；当Host设置为$proxy_host时，则会重新设置请求头为bbb.example.com的Host信息。
    }
    
```