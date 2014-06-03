`\webui\gxt\protected\models\SecurityVuls.php`

```php
public static function getTable(){
    $key   = 'xx';
    $value = Yii::app()->cache->get($key);
    if (empty($value)) {
        self::cacheWholeTable();
    }
    $value = Yii::app()->cache->get($key);
    return json_decode($value, true);
}
```
should be
```php
public static function getTable(){
    $key   = 'xx';
    $value = Yii::app()->cache->get($key);
    if (empty($value)) {
        self::cacheWholeTable();
        $value = Yii::app()->cache->get($key);
    }
    return json_decode($value, true);
}
```
