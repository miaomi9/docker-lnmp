# PHPer 常用命令容器化

* `composer` => `lnmp-composer`
* `phpunit`  => `lnmp-phpunit`
* `php CLI`  => `lnmp-php`
* `laravel`  => `lnmp-laravel`
* `php-cs-fixer` => `lnmp-php-cs-fixer`

> 为避免与原始命令冲突，这里加上了 `lnmp-` 前缀

## 使用方法

### 安装

自行将下面示例中的 `/data/lnmp` 替换为本项目实际路径。

#### Bash

```bash
$ vi ~/.bash_profile

export LNMP_PATH=/data/lnmp

export PATH=$LNMP_PATH:$LNMP_PATH/bin:$PATH
```

#### fish

```bash
$ vi ~/.config/fish/config.fish

set -gx LNMP_PATH /data/lnmp

set -gx fish_user_paths $fish_user_paths $LNMP_PATH $LNMP_PATH/bin
```

#### Windows 10

打开 `PowerShell`

```bash
$ [environment]::SetEnvironmentvariable("LNMP_PATH", "$HOME\lnmp", "User")

$ [environment]::SetEnvironmentvariable("Path", "$env:path;$env:LNMP_PATH;$env:LNMP_PATH\windows;", "User")
```

> 如果 `PoswerShell` 禁止执行脚本，请以管理员身份执行 `set-ExecutionPolicy Bypass`,之后输入 `Y` 确认。[说明](https://docs.microsoft.com/zh-cn/powershell/module/microsoft.powershell.core/about/about_execution_policies)

### 使用

```bash
$ cd my_php_project

$ lnmp-composer command

$ lnmp-phpunit command

$ lnmp-php command
```

当你遇到错误时，可以在前边加上 `$ debug=true lnmp-*`来进行调试，例如

```bash
$ debug=true lnmp-composer
```

### 最佳实践

#### 新建 `Laravel` 项目

```bash
$ cd app

$ lnmp-laravel new my_laravel_app
```

#### `Laravel` 项目预览

```bash
$ cd my_laravel_app

$ lnmp-php -S 0.0.0.0:80 -t public
```

#### `artisan` command

```bash
$ cd my_laravel_app

$ lnmp-php artisan
```

#### 安装/升级 `composer` 依赖

```bash
$ cd my_laravel_app

$ lnmp-composer [install | update]
```

#### php-cs-fixer

```bash
$ lnmp-php-cs-fixer fix
```

#### npm with git

在 `.env` 文件中新增变量，变量值为你自己的镜像（用户自行构建）。

```bash
LNMP_NODE_IMAGE=your/node:git-alpine
```
