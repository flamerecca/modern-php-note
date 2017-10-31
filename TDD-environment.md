# TDD 環境建置

下面聊怎麼建置 TDD，一樣使用 laravel 框架做說明。

## PHPUnit

這邊建議使用 composer 安裝。

## Composer

像是CentOS 7，只要下指令：

```
$ sudo yum install composer
```

就可以了。

安裝 composer 完畢之後，下指令：

```
$ composer require --dev phpunit/phpunit ^6.2
```

## 其他重要套件

### php-invoker

php-invoker：可以測試時間。如果你的程式非常重視時間，可以用這個進行測試。

```
$ composer require --dev phpunit/php-invoker
```

### dbunit

dbunit：可以測試資料庫

```
$ composer require --dev phpunit/dbunit
```

## 娛樂用

### nyancat

[https://github.com/whatthejeff/nyancat-phpunit-resultprinter](https://github.com/whatthejeff/nyancat-phpunit-resultprinter)

使用以下指令安裝

```
$ composer require --dev whatthejeff/nyancat-phpunit-resultprinter
```

安裝過後， phpunit.xml 裡面要加上

```
printerFile="vendor/whatthejeff/nyancat-phpunit-resultprinter/src/NyanCat/PHPUnit/ResultPrinter.php"
printerClass="NyanCat\PHPUnit\ResultPrinter"
```

才會生效。

## XDebug



