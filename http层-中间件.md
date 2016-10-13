1.简介

HTTP 中间件为过滤进入应用的 HTTP 请求提供了一套便利的机制。例如，Laravel 内置了一个中间件来验证用户是否经过授权，如果用户没有经过授权，中间件会将用户重定向到登录页面，否则如果用户经过授权，中间件就会允许请求继续往前进入下一步操作。

当然，除了认证之外，中间件还可以被用来处理更多其它任务。比如：CORS 中间件可以用于为离开站点的响应添加合适的头（跨域）；日志中间件可以记录所有进入站点的请求。

2.定义中间件

php artisan make:middleware CheckAge

3.注册中间件

如果你想要中间件在每一个 HTTP 请求期间被执行，只需要将相应的中间件类设置到 app/Http/Kernel.php 的数组属性 $middleware 中即可

4.中间件参数

5.可终止的中间件
有时候中间件可能需要在 HTTP 响应发送到浏览器之后做一些工作。比如，Laravel 内置的“session”中间件会在响应发送到浏览器之后将 Session 数据写到存储器中，为了实现这个功能，需要定义一个可终止的中间件并添加 terminate 方法到这个中间件
```
<?php

namespace Illuminate\Session\Middleware;

use Closure;

class StartSession{ public function handle($request, Closure $next) { return $next($request); }

 public function terminate($request, $response) { // 存储session数据... }}
```

terminate 方法将会接收请求和响应作为参数。定义了一个可终止的中间件之后，还需要将其加入到 HTTP kernel 的全局中间件列表中。

当调用中间件上的 terminate 方法时，Laravel 将会从服务容器中取出该中间件的新的实例，如果你想要在调用handle 和 terminate 方法时使用同一个中间件实例，则需要使用容器的 singleton 方法将该中间件注册到容器中。


