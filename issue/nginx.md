# 适配Java服务

## dockers 启动

``` shell
docker run -d --name 服务名 -p 3100:3100   -v /data/服务名/conf:/etc/nginx/conf.d   -v /data/服务名/html:/usr/share/nginx/html   --restart always   nginx:1.26-arm64
/etc/nginx/conf.d/default.conf
server {
    listen  3100;
    server_name  _;

    location /服务名 {
        alias /usr/share/nginx/服务名; 
        index  index.html index.htm;
        try_files  $uri $uri/ /服务名/index.html;
        client_max_body_size 2048m;
    }
        location ^~ /服务名-server {
        ## http: 服务IP：端口
        proxy_pass              http:/10.1.26.243:31000/服务名-server;
        proxy_set_header        Host $host;
        proxy_set_header        X-Real-IP $remote_addr;
        proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }


}
```
