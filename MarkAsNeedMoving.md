# 註解函式為需要移動

肥大的物件通常是被賦予了太多功能。裡面包含了太多的函式，所以無法被移動。

可是要拆解物件，要想新的物件名稱，總是讓人感到棘手：萬一命名得不好或者函式功能太少，是不是並沒有讓程式的設計變得更好，而是做白工呢？

## 註解函式

```php
class ApiController extends Controller
{

    public function getWorkHour(){/*...*/}

    public function getSalary(){/*...*/}

    public function markWorkerIsOverwork(){/*...*/}

    public function bookName(){/*...*/}

    public function bookPrice(){/*...*/}

    public function setBookName(){/*...*/}

    public function getFinance1(){/*...*/}

    public function getFinance2(){/*...*/}
    //......

}
```

這個類別不僅函式功能很雜亂，而且有的函式命名還很不清楚，比方說 `getFinance1()` 和 `getFinance2()`

### 註解

首先，我們先把這些函式裡面的內容看懂，並下註解

```php
class ApiController extends Controller
{
    
    //TODO 輸入員工號碼取得工作時間 跟員工相關
    public function getWorkHour(){/*...*/}
    
    //TODO 輸入員工號碼取得薪資 跟員工相關
    public function getSalary(){/*...*/}
    
    //TODO 輸入員工號碼取得該員工是否超時工作 跟員工相關
    public function markWorkerIsOverwork(){/*...*/}
    
    //TODO 輸入書本號碼取得書本名稱 跟書本相關
    public function bookName(){/*...*/}
    
    //TODO 輸入書本號碼取得書本價格 跟書本相關
    public function bookPrice(){/*...*/}
    
    //TODO 修改書本名稱
    public function setBookName(){/*...*/}

    //TODO 輸入部門號碼取得該部門最近收入 應該改名為getSectionIncome()之類的？
    public function getFinance1(){/*...*/}

    //TODO 看不太懂，可能和部門支出有關
    public function getFinance2(){/*...*/}
    //......

}
```

然後我們又可以擺著了。

等到有一天，我們需要清理 TODO 註解時，我們又回頭來看看這一段再做什麼。發現大量不同功能的函式被放在一起。這時候就可以新開類別來放相近的函式了。

最棒的地方是，我們不需要給自己壓力，一次把所有函式移動並測試完成。我們可以一點一點移動。

### 改變註解

隨著時間過去，我們可能發現之前的判斷是錯誤的。比方說，突然發現`getFinance2()` 其實是用來計算單一員工所提報的支出。這個函式與其跟 getFinance1\(\) 放在一起，可能更適合跟其他員工相關的函式放在一起。

如果我們沒空馬上修改，起碼可以先註解起來該做的事情，之後來處理這個行為。

### 為什麼是用註解？

## 網址問題

在 laravel 裡面，網址是隨著Route設定而改變的，所以不用擔心多拆成幾個物件會對網址有什麼改變。

```php
Route::get('/api/StoringAlpha', 'StorageAlphaController@store');
Route::get('/api/StoringBeta', 'StorageBetaController@store');
Route::get('/api/StoringGamma', 'StorageGammaController@store');
Route::get('/api/StoringDelta', 'StorageDeltaController@store');
Route::get('/api/StoringEpsilon', 'StorageEpsilonController@store');
```

Yii2 裡面，預設網址是`Controller/actionFunction` 的形式。這也是很容易就把上面所說的`forStoring[???]` 全部寫進 `ApiController` 的原因。

其實我們一樣可以透過設定 Route ，來讓我們的controller 變小，像是這樣：

```php
'urlManager' => [
    //...
    'rules' => [
        'api/StoringAlpha' => 'StorageAlphaController/store',
        'api/StoringBeta' => 'StorageBetaController/store',
        'api/StoringGamma' => 'StorageGammaController/store',
        'api/StoringDelta' => 'StorageDeltaController/store',
        'api/StoringEpsilon' => 'StorageEpsilonController/store',
    ],
]
```

## 物件太小？

拆解過程中，有時候會讓人擔心，一個物件如果只有一個函式，那豈不是過度重構了？

所以我自己使用先註解起來的方式，顯露出明顯的壞味道。  
當壞味道累積夠多，我們可以很簡單的從註解裡，找出夠多類似的函式，並放在同一個物件底下。

