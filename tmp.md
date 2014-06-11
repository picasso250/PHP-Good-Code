
```php
$normalData   = array();
$abnormalData = array();
foreach ($result as $key => $value) {
    if ($value['status'] == 'NORMAL') {
        $tmpHour = intval($value['hour']);
        $normalData[$tmpHour]['latency']     = intval($value['latency']);
        $normalData[$tmpHour]['noava_time']  = intval($value['noava_time']);
        $normalData[$tmpHour]['count']       = intval($value['count']);
        $normalData[$tmpHour]['total_count'] = intval($value['total_count']);
    }
    else if ($value['status'] == 'ABNORMAL') {
        $tmpHour = intval($value['hour']);
        $abnormalData[$tmpHour]['latency']     = intval($value['latency']);
        $abnormalData[$tmpHour]['noava_time']  = intval($value['noava_time']);
        $abnormalData[$tmpHour]['count']       = intval($value['count']);
        $abnormalData[$tmpHour]['total_count'] = intval($value['total_count']);
    }
}
```
should be

```php
$normalData   = array();
$abnormalData = array();
foreach ($result as $key => $value) {
    $tmpHour = intval($value['hour']);
    $tmpArr = array(
        'latency'     => intval($value['latency']),
        'noava_time'  => intval($value['noava_time']),
        'count'       => intval($value['count']),
        'total_count' => intval($value['total_count']),
    );
    if ($value['status'] == 'NORMAL') {
        $normalData[$tmpHour] = $tmpArr;
    }
    else if ($value['status'] == 'ABNORMAL') {
        $abnormalData[$tmpHour] = $tmpArr;
    }
}
```
