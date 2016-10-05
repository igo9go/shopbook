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
Route::group(['middleware' => 'auth'], function () { Route::get('/', function () { // 使用 Auth 中间件 });

 Route::get('user/profile', function () { // 使用 Auth 中间件 });});

```
* 命名空间
```
Route::group(['namespace' => 'Admin'], function(){ // 控制器在 "App\Http\Controllers\Admin" 命名空间下 Route::group(['namespace' => 'User'], function(){ // 控制器在 "App\Http\Controllers\Admin\User" 命名空间下 }); });
```
* 子域名路由

```
Route::group(['domain' => '{account}.myapp.com'], function () { Route::get('user/{id}', function ($account, $id) { // }); });
```
* 路由前缀

```
Route::group(['prefix' => 'admin'], function () {           Route::get('users', function () { // 匹配 "/admin/users" URL }); });
```

5.表单方法伪造

HTML 表单不支持 PUT、PATCH 或者 DELETE 请求方法，因此，当定义 PUT、PATCH 或 DELETE 路由时，需要添加一个隐藏的 _method 字段到表单中，其值被用作该表单的 HTTP 请求方法：

```
<form action="/foo/bar" method="POST"> <input type="hidden" name="_method" value="PUT"> <input type="hidden" name="_token" value="{{ csrf_token() }}"></form>
```
还可以使用辅助函数 method_field 来实现这一目的：

{{ method_field('PUT') }}

6.访问当前路由

你可以使用 Route 门面上的 current、currentRouteName和 currentRouteAction 方法来访问处理当前输入请求的路由信息：

$route = Route::current(); 
$name = Route::currentRouteName(); 
$action = Route::currentRouteAction();










    





                                                                              

