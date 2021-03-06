# CakePHP

CakePHP 是一套用 MVC 架構方法的開放原始碼框架，也是在 PHP 社群中最受歡迎的框架其中一支。

此篇指南已於 `3.8` 版本成功測試，我認為在較舊版本也同樣適用。

![CakePHP　框架防火牆](https://shieldon.io/images/home/cakephp-framework-firewall.png)

## 安裝

使用 PHP Composer:

```php
composer require shieldon/shieldon
```

或者下載後引入 Shieldon 自動載入器。

```php
require 'Shieldon/autoload.php';
```

## 部署

### CakePHP 3

步驟 1 及步驟 2 套用在同樣檔案位於 `/config/route.php`。

#### 1. 註冊一個 Middleware

如同其它框架，已經有一個專為 CakePHP 架構的 Middleware 可以直接使用。

```php
/**
 * Apply Shieldon Firewall tp the current route scope.
 */
$routes->registerMiddleware(
    'firewall',
    new \Shieldon\Integration\CakePhp\CakePhpMiddleware()
);

$routes->applyMiddleware('firewall');
```

#### 2. 定義一個路由給防火牆面板

```php
/**
 * Define the route for the firewall panel.
 */
$routes->connect('/firewall/panel/', [
    'controller' => 'FirewallPanel',
    'action' => 'entry'
]);
```


#### 3. 建立一個 Controller 給防火牆面板

建立一個名為 `FirewallPanelController` 的 Controller，並放進如以下的程式碼：

```php
$firewall = \Shieldon\Container::get('firewall');
$controlPanel = new \Shieldon\FirewallPanel($firewall);
$controlPanel->entry();
exit;
```

如果您有啟用 CSRF 保護機制，加此這幾行：

```php
$controlPanel->csrf(
    '_csrfToken',
    $this->request->getParam('_csrfToken')
);
```

完整的例子看起來像是這樣：

```php
<?php

namespace App\Controller;

class FirewallPanelController extends AppController
{

    /**
     * This is the entry of our Firewall Panel.
     */
    public function entry()
    {
        // Get Firewall instance from Shieldon Container.
        $firewall = \Shieldon\Container::get('firewall');

        // Get into the Firewall Panel.
        $controlPanel = new \Shieldon\FirewallPanel($firewall);
        $controlPanel->csrf(
            '_csrfToken',
            $this->request->getParam('_csrfToken')
        );

        $controlPanel->entry();
        exit;
    }
}
```

就是這樣囉。

您能夠使用網址路徑 `/firewall/panel` 能連上防火牆面板。

```
https://for.example.com/firewall/panel
```

預設的登入帳號是 `shieldon_user` 而密碼是 `shieldon_pass`。在您登入防火牆面板之後，第一件該做的事情就是更改帳號及密碼。

如果在設定區塊中的 `守護進程` 有啟用的話，Shieldon 將會開始監看您的網站，請確定您已經把設定值都設定正確。