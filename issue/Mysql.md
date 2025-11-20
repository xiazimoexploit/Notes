# docker 常见服务
dockers 启动MySQL命令

``` shell
# 如果 /data/sl 以前没用过，先赋权，避免 MySQL 启动报错
sudo mkdir -p /data/sl
sudo chown -R 999:999 /data/sl      # 999 是 mysql 镜像里 mysql 用户的 UID/GID

docker run -d --name sgbsqzl-mysql \
  -p 3307:3306 \
  -e MYSQL_ROOT_PASSWORD=123456 \
  -v /data/服务名/mysql/data:/var/lib/mysql \
  mysql:5.7.42-arm64 --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci
```