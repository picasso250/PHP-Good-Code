`\webui\gxt\protected\components\ReportComponent.php`
```php
$ret = array();
foreach ($induArr as $Indu => $tmpIndu) {
    $ret[$Indu] = array();
    for ($i = count($tmpIndu) - 1; $i >= 0; $i--) {
        $ret[$Indu][] = $tmpIndu[$i];
    }
}
```
should be
```php
$ret = array();
foreach ($induArr as $Indu => $tmpIndu) {
    $ret[$Indu] = array_reverse($tmpIndu);
}
```
