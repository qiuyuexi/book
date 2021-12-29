* 问题
```php
  php >  echo json_encode(['a' => (float)357.61]);
{"a":357.61000000000001}
php > echo int_get('serialize_precision');
php >
php >  echo json_encode(['a' => '357.61']);
{"a":"357.61"}
```

* 解决方法
  *  https://stackoverflow.com/questions/42981409/php7-1-json-encode-float-issue
  * serialize_precision 设置为 -1 
