# ssl
nginx配置ssl

最近想给网站添加https访问，使用的是阿里云ssl免费证书

在配置之前，一定要服务器里的安全组里把443端口打开，这个是重点

HTTPS server中的conf文件配置如下

server {
    listen 443; #ssl端口号
    server_name wengr.com; #我的域名
    ssl on;
    root html;
    index index.html index.htm;
    ssl_certificate      /alidata/server/nginx/cert/1920094_wengr.pem;  #证书.pem
    ssl_certificate_key   /alidata/server/nginx/cert/1920094_wengr.key;  #证书.key
    ssl_session_timeout 5m;
    ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_prefer_server_ciphers on;
    location / {
        root /alidata/www;  #首页根目录
        index index.html index.htm;
    }
}

最近遇到的一个坑，就是忘记在服务器的安全组把443端口，特此记录下
