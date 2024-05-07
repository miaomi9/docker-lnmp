# Xdebug in Docker + PhpStorm

* https://xdebug.org/docs/all_settings

**启用 Xdebug 扩展会使 PHP 响应变慢，建议仅在需要调试时打开！**

## 启用 xdebug 扩展

> 不建议在生产环境启用 `xdebug`

编辑 `config/php/docker-php.ini` 文件，取消注释

```diff
- ; zend_extension=xdebug
+ zend_extension=xdebug
```

## 准备 PHP 项目

* PHP 项目

* NGINX 配置

* 验证浏览器能通过网址访问到你的 PHP 项目

## 设置 Xdebug

### 调试 HOST (必选项)

编辑 `.env` 文件中的 `LNMP_XDEBUG_REMOTE_HOST=192.168.199.100` 变量为你电脑的 IP，这就要求你的电脑必须固定 IP。不然电脑 IP 每次变化时，必须重新修改此变量。

#### 1. Docker Desktop

在 Docker 设置中没有配置自定义 DNS 的情况下可以使用 `LNMP_XDEBUG_REMOTE_HOST=host.docker.internal`。

#### 2. Docker for Linux

要么电脑固定 IP，要么 IP 变化时编辑 `.env` 文件中的 `LNMP_XDEBUG_REMOTE_HOST` 变量

### 调试端口（可选项）

编辑 `.env` 文件中的 `LNMP_XDEBUG_REMOTE_PORT=9003` 变量，默认 `9003`

### 警告

其他选项严禁修改，除非你明确知道某个选项将产生什么影响。

## 重启容器

```bash
$ ./lnmp-docker restart php8
```

## 在 `IDE` 设置中配置 `Xdebug`

`Preferenences` -> `Languages & ...`-> `PHP` -> `Debug`-> `xdebug`-> `Debug port 9003`(默认为 `9000`，这里改为 `9003`)

## [浏览器扩展](https://www.jetbrains.com/help/phpstorm/2022.1/browser-debugging-extensions.html)

* [火狐](https://github.com/BrianGilbert/xdebug-helper-for-firefox)
* [Chrome](https://github.com/mac-cain13/xdebug-helper-for-chrome)
* [Edge](https://microsoftedge.microsoft.com/addons/detail/xdebug-helper/ggnngifabofaddiejjeagbaebkejomen?hl=zh-CN)

**在扩展配置中 IDE key 选择 PhpStorm**

## 使用步骤

* 1.IDE 中开启调试 `Run` -> `Start Listening for PHP Debug Connections`(如果是 `Stop Listening ...` 说明已经开启了调试)

* 2.编写代码

* 3.打断点

* 4.浏览器打开对应页面，在页面点击扩展图标，选择 `debug`，之后刷新页面

* 5.自动跳转到 IDE，开始调试

* 6.首次刷新 IDE 会出现配置窗口，直接点击 `Accept` 即可。(仅需配置一次)

* 7.配置路径对应关系，由于本地代码目录结构与容器中的不一致，我们必须配置其对应关系，设置页面，`Preferenences` -> `Languages & ...`-> `PHP` -> `Servers` -> `C:\Users\username\app\laravel(本地路径)` 对应 `/app/laravel(容器路径)`(请根据实际情况配置)(仅需配置一次)

## 排错

打开 `log/php/xdebug-remote.log` 查看日志。

## More Information

* https://xdebug.org/docs/step_debug

* https://segmentfault.com/a/1190000010833434

* https://www.jetbrains.com/help/phpstorm/docker.html
