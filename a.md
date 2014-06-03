`\webui\gxt\protected\models\SecurityVuls.php`

```php
    /**
     * 按漏洞英文名称查询securityVuls表
     * 输入: 无
     * 输出：json解压缩数组，key=name, value=show_name, type, ....
     **/
    public static function getTable(){
        $key   = 'SecurityVuls_whole_table';
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
        $key   = 'SecurityVuls_whole_table';
        $value = Yii::app()->cache->get($key);
        if (empty($value)) {
            self::cacheWholeTable();
            $value = Yii::app()->cache->get($key);
        }
        return json_decode($value, true);
    }
```
