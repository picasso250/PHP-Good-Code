
```php
$tmpIDIndex = array();
foreach ($ret as $value) {
    $tmpIDIndex[$value['message_id']] = 1;
}
$leftIDs = array();
foreach ($tmpIDs as $id) {
    if (!isset($tmpIDIndex[$id])) {
        $leftIDs[] = $id;
    }
}
```
should be
```php
$tmpMessageIds = array_map(function($e){return $e['message_id'];}, $ret);
$leftIDs = array_diff($tmpIDs, $tmpMessageIds);
```
