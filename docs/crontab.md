# Crontab 计划任务

* https://crontab.guru/

## 选择1：宿主机运行 crontab

```bash
$ crontab -e
```

```bash
* * * * * /usr/local/bin/docker exec -i $( docker container ls --format '{{.ID}}' -f label=com.khs1994.com -f label=com.docker.compose.service=php7 ) sh -c "php /app/path-to-your-project/artisan schedule:run >> /dev/null 2>&1"

* * * * * /usr/local/bin/docker exec -i $( docker container ls --format '{{.ID}}' -f label=com.khs1994.com -f label=com.docker.swarm.service.name=lnmp_php7 ) sh -c "php /app/path-to-your-project/artisan schedule:run >> /dev/null 2>&1"
```

通过在 **宿主机** 计划执行 `docker exec ***`，变相实现容器内计划任务，只适用于 **单机环境**。

## 选择2：容器内运行 crontab

使用 `s6` 或 [supervisord](supervisord.md)

## Alpine 非 root 用户无法运行 crontab

* https://github.com/gliderlabs/docker-alpine/issues/381
* https://github.com/inter169/systs/blob/master/alpine/crond/README.md
