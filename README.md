codexx
======
Good code talks

```php
$userTaskIDs = '';
foreach ($result as $value) {
    if (!empty($userTaskIDs)) {
        $userTaskIDs .= ',';
    }
    $userTaskIDs .= intval($value['user_task_id']);
}
```
should be 
```php
$userTaskIDsArray = array_map(function($e){return intval($e['user_task_id']);}, $result);
$userTaskIDs = implode(',', $userTaskIDsArray);
```

Feel free to discuss, issues and pull requests are welcomed.
