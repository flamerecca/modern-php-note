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

    public function getFinance(){/*...*/}

    public function getFinance(){/*...*/}
    //......

}
```

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

其實我們一樣可以透過設定 Route ，來讓我們的controller 變小：

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

