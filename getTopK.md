`ReportComponent::computeTopPerfHost()`

```php
$getTopK = function ($rows, $key, $k, $map_cb = null) {
    $topk = array();
    foreach ($rows as $row) {
        $v = $row[$key];
        if (count($topk) < $k) {
            $topk[] = $row;
        } elseif ($v > $topk[$k-1][$key]) {
            $topk[] = $row;
            usort($topk, function($a, $b){return $a[$key] > $b[$key] ? -1 : 1;});
            array_pop($topk);
        }
    }
    return $map_cb ? array_map($map_cb, $topk) : $topk;
};
$wholeTop5 = $getTopK($result, 'total_time', 5, function ($e){return intval($e['host_id']);});
$map_cb = function ($e) {
    return array(
        'id' => intval($e['host_id']),
        'speed' => round(floatval($e['total_time']) / 1000.0, 2),
    );
};
foreach (Yii::app()->params['industory'] as $key => $value) {
    $industoryHosts = array_filter($result, function ($e) use ($key, $hostArr) {
        return in_array($key, $hostArr[$e['host_id']]);
    });
    $top5[$key] = $getTopK($industoryHosts, 'total_time', 5, $map_cb);
}
```
