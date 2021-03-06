# IP

## `Shieldon\Component\Ip`

- *return* self

```php
$ip = new \Shieldon\Component\Ip();
$shieldon->setComponent($ip);
```

### inRange

- *param* string `$ip` 要檢查是否在範圍內的 IP 位址
- *param* mixed `$range` IP/CIDR netmask
- *return* boolean

```php
$result = $ip->inRange('123.22.33.44', '123.22.33.1/24');

// true
```
### setAllowedList

- *param* array `$ips` IP 陣列。
- *return* void

```php
$ip = new \Shieldon\Component\Ip();

$allowedIps = [
    '123.22.33.44',
    '88.22.33.55',
];

$ip->setAllowedList($allowedIps);
$shieldon->setComponent($ip);
```

### setAllowedItem

- *param* string `$ip` 單一 IP 位址。
- *return* void

```php
$ip = new \Shieldon\Component\Ip();
$ip->setAllowedItem('123.22.33.44');
$shieldon->setComponent($ip);
```

### getAllowedList

- *return* array

```php
$ip = new \Shieldon\Component\Ip();
$list = $ip->getAllowedList();

// ['123.22.33.44', '123.22.33.43', 'xxx.xxx.xxx.xxx']
```
### setDeniedList

- *param* array `$ips` IP 陣列。
- *return* void

```php
$ip = new \Shieldon\Component\Ip();

$deniedIps = [
    '123.22.33.44',
    '88.22.33.55',
];

$ip->setDenieddList($deniedIps);
$shieldon->setComponent($ip);
```

### setDeniedItem

- *param* string `$ip` 單一 IP 位址。
- *return* void

```php
$ip = new \Shieldon\Component\Ip();
$ip->setDeniedItem('123.22.33.44');
$shieldon->setComponent($ip);
```

### getDeniedList

- *return* array

```php
$ip = new \Shieldon\Component\Ip();
$list = $ip->getDenieddList();

// ['123.22.33.44', '123.22.33.43', 'xxx.xxx.xxx.xxx']
```

