`ReportComponent::computeTopPerfHost()`

```php
$getTopK = function ($rows, $key, $k, $map_cb = null) {
    $ret = array();
    $r = array();
    foreach ($rows as $value) {
        $v = $value[$key];
        if (count($ret) < $k) {
            $ret[] = $value;
            $r = $v;
        } elseif ($v > min($r)) {
            $ret[] = $value;
            $r = $v;
            rsort($r);
            usort($ret, function($a, $b){return $a[$key] > $b[$key] ? -1 : 1;});
            array_pop($r);
            array_pop($ret);
        }
    }
    return $map_cb ? array_map($map_cb, $ret) : $ret;
};
$wholeTop5 = $getTopK($result, 'total_time', 5, function ($e){return intval($e['host_id']);});
$map_cb = function ($e) {
    return array(
        'id' => intval($e['host_id']),
        'speed' => round(floatval($e['total_time']) / 1000.0, 2),
    );
};
foreach (Yii::app()->params['industory'] as $key => $value) {
    $industoryHosts = array_filter($result, function($e)use($key){return in_array($key, $hostArr[$e['host_id']]);});
    $top5[$key] = $getTopK($industoryHosts, 'total_time', 5, $map_cb);
}
```
