###路由
1.基本路由

最基本的 Laravel 路由只接收一个 URI 和一个闭包，并以此提供一个非常简单且优雅的定义路由方法：

```
Route::get('foo',
     function () { 
        return 'Hello World';
     }
);
```
* 默认路由文件
    
    所有Laravel路由都定义位于routes目录下的路由文件中，这些文件通过框架自动加载。routes/web.php文件定义了web界面的路由，这些路由被分配给web中间件组，从而可以提供session和csrf防护等功能。routes/api.php中的路由是无状态的，被分配到api中间件组。

* 有效的路由方法
    * Route::get($uri, $callback);
    * Route::post($uri, $callback);
    * Route::put($uri, $callback); 
    * Route::patch($uri, $callback);
    * Route::delete($uri, $callback);
    * Route::options($uri, $callback);
    * Route::match(['get', 'post'], '/', function () { // });  
    * Route::any('foo', function(){});

2.路由参数
* 必选参数



 Route::get('posts/{post}/comments/{comment}', function ($postId, $commentId) { // });

* 可选参数

 Route::get('user/{name?}', function ($name = null) { return $name; });

 Route::get('user/{name?}', function ($name = 'John') { return $name; });

3.命名路由

Route::get('user/profile', 'UserController@showProfile')->name('profile');

4.路由群组

路由群组允许我们在多个路由中共享路由属性，比如中间件和命名空间等，这样的话我们就不必为每一个路由单独定义属性。共享属性以数组的形式作为第一个参数被传递给 Route::group 方法。
* 中间件

```
Route::group(['middleware' => 'auth'], function () {      Route::get('/', function () { // 使用 Auth 中间件 }); Route::get('user/profile', function () { // 使用 Auth 中间件 }); });
```

    





                                                                              

