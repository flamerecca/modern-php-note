# TDD 環境建置

下面聊怎麼建置 TDD，一樣使用 laravel 框架做說明。

## PHPUnit

這邊建議使用 composer 安裝。

像是CentOS 7，只要下指令：

```
$ sudo yum install composer
```

就可以了。安裝完畢之後，下指令：

```
$ composer require --dev phpunit/phpunit ^6.2
```

php-invoker：可以測試時間。如果你的程式非常重視時間，可以用這個進行測試。

```
$ composer require --dev phpunit/php-invoker
```

dbunit：可以測試資料庫

```
$ composer require --dev phpunit/dbunit
```



## XDebug



