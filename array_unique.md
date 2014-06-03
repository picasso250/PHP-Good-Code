`\webui\gxt\protected\models\Alerts.php`
```php
foreach ($list_alerts as $tmpKey => $tmpAlert) {
    $tmpMonth = date("Ym", CommonUtil::sstrtotime($tmpTime));
    if (!isset($messageIDs[$tmpMonth])) {
        $messageIDs[$tmpMonth] = array();
    }
    $tmpIDs   = $tmpAlert['message_ids'];
    $tmpIDs = explode(',', $tmpIDs);
    
    foreach ($tmpIDs as $tmpID) {
        if (!in_array($tmpID, $messageIDs[$tmpMonth])) {
            $messageIDs[$tmpMonth][] = trim($tmpID);
        }
    }
}
array_unique($messageIDs[$tmpMonth]);

```
should be 
```php
foreach ($list_alerts as $tmpKey => $tmpAlert) {
    $tmpMonth = date("Ym", CommonUtil::sstrtotime($tmpTime));
    if (!isset($messageIDs[$tmpMonth])) {
        $messageIDs[$tmpMonth] = array();
    }
    $tmpIDs   = $tmpAlert['message_ids'];
    $tmpIDs = explode(',', $tmpIDs);

    $messageIDs[$tmpMonth] = array_merge($messageIDs[$tmpMonth], $tmpIDs);
}
array_unique($messageIDs[$tmpMonth]);
```
