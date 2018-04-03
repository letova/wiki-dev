# Array flatten

*Любого уровня*

```php
function flatten($array) { 
  if (!is_array($array)) { 
    return false; 
  } 
  $result = array(); 
  foreach ($array as $key => $value) { 
    if (is_array($value)) { 
      $result = array_merge($result, flatten($value)); 
    } else { 
      $result[$key] = $value; 
    } 
  } 
  return $result; 
}
//flatten([1, 2, [3, 5], [[4, 3], 2]]) //[1, 2, 3, 5, 4, 3, 2]
//flatten([1, 2, ['three' => 3, 5], [[4, 3], 2]]) //[1, 2, 'three' => 3, 5, 4, 3, 2]
```

```php
function flatten($value)
{
    if (!is_array($value)) {
        return [$value];
    } elseif (sizeof($value) == 0) {
        return [];
    } elseif (sizeof($value) == 1) {
        return flatten(end($value));
    }
    return array_merge(flatten(array_slice($value, 0, 1)), flatten(array_slice($value, 1)));
}
//flatten([1, 2, [3, 5], [[4, 3], 2]]) //[1, 2, 3, 5, 4, 3, 2]
```