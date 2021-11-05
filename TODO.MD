## TODO

- 监控执行sql的语句以及条件 - [laravel-query-logger](https://github.com/overtrue/laravel-query-logger)

- 模型观察，需要在 `模型` 里进行 boot 注册

- 队列

- 增加中间件，来记录请求的日志，以及返回的数据。[Link](https://learnku.com/articles/56770)

```php
// 这是中间件的代码。
$log = new RequestLog (); // 日志表
$log->url = $request->fullUrl ();
$log->ip = $request->getClientIp ();
$log->params = json_encode ($request->all (), JSON_UNESCAPED_UNICODE);
$log->save ();
$response = $next ($request);
// 这里，把返回数据，也加入到数据库 li 里。
if ($rep = $response->getContent ()) {
  $log->update ([
     'response_params' => $rep,
     'user_id' => $request->user () ? $request->user ()->id : 0,
     'duration' => get_all_duration (),
   ]);
}
return $response;
```

```php
function get_all_duration ():int
{
  $end = (int)(microtime (true)1000);
  $start = (int) ( (request()->server('REQUEST_TIME_FLOAT')) 1000 );
  return $end-$start;
}
```

- 返回数据的格式是否需要统一，[Response](https://github.com/Jiannei/laravel-response)

- 接口参数签名验证 [Link](https://learnku.com/articles/60945)
