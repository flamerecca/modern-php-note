# TDD

目前我自己實際開發的思維路徑，storyBDD 或者 specBDD對我來說太難。

## 環境建置

以下假設環境建置已經建立。如果沒有的話，請參考 TDD環境建置。

## 思考架構

如果你像我一樣是使用某個MVC框架（Yii2 或者 Laravel），消化完一個工作項目之後，我們腦中應該會想到該功能的實做。  
很可能是放置在某一個 Controller 裡面，透過 Route（Laravel） 或者action\[?\]（Yii2）進行呼叫。

這個動作會對應某個函式。

接著我通常會先想，這個函式必須處理怎樣的一個例外狀況：如果送進來的網址參數不對，或者

這時候就可以將幾個草稿先寫出來了。

## 建立 Testcase

理想情況可能是將所有的測試寫完之後，才開始撰寫程式。不過通常無法這麼做。  
所以我會先將該功能先寫一個假的測試當作骨架。隨著開發中的想法，再加入對應的測試。

以下以 Laravel 的測試環境當作範例。  
首先我會寫一個假的測試函式，假設我們要測`MyController`裡面的`handle()`：

```php
<?php

namespace Tests\Unit;

use Tests\TestCase;
use Illuminate\Foundation\Testing\RefreshDatabase;

class SomeControllerTest extends TestCase
{
    /**
     * A basic test
     *
     * @return void
     */
    public function testHandle()
    {
        $this->assertTrue(true);
    }
}
```

這個函式跟我們的`handle()`沒有任何關係，無論發生什麼事情，都會回傳測試成功。

## 測試命名

寫程式一段時間就知道，命名這件事情通常很痛苦。

由於

像是這樣

```php
testBalanceIsInitiallyZero()
{
    //...
}
testBalanceCannotBecomeNegative()
{
    //...
}

testBalanceCannotBecomeNegative2()
{
    //...
}
```

那麼，該工具就會產生

```bash
$ phpunit --testdox BankAccountTest
PHPUnit 6.4.0 by Sebastian Bergmann and contributors.

BankAccount
 [x] Balance is initially zero
 [x] Balance cannot become negative
```

雖然我很少使用這個工具，但是想像這個工具的輸出，對我在函式上的命名很有幫助。

假設我想讓人從 testdox 看出「這個函式如果沒有任何輸入，應該要回傳0」這件事情，那我可能會寫

```php
public function testHandleReturnZeroWhenNoInput()
    {
        $this->assertTrue(true);
    }
```

預期能輸出

```bash
$ phpunit --testdox MyControllerTest
PHPUnit 6.4.0 by Sebastian Bergmann and contributors.

MyController
 [x] Handle return zero when no input
```



