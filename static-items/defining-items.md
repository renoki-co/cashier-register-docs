# 🧶 Defining Items

In case you are not using plans, you can describe items once in Cashier Register's service provider and then leverage it for some neat usage:

```php
use RenokiCo\CashierRegister\Saas;

Saas::item('Elephant Sticker', 'elephant-sticker')
    ->price(5, 'EUR');
```

Then later be able to retrieve it:

```php
use RenokiCo\CashierRegister\Saas;

$item = Saas::getItem('elephant-sticker');

$item->getPrice(); // 5
$item->getCurrency(); // 'EUR'
```

Each item can have sub-items too:

```php
use RenokiCo\CashierRegister\Saas;

Saas::item('Sticker Pack', 'sticker-pack')
    ->price(20, 'EUR')
    ->subitems([
        Saas::item('Elephant Sticker', 'elephant-sticker')->price(5, 'EUR'),
        Saas::item('Zebra Sticker', 'zebra-sticker')->price(10, 'EUR'),
    ]);
```

```php
$item = Saas::getItem('sticker-pack');

foreach ($item->getSubitems() as $item) {
    $item->getName(); // Elephant Sticker, Zebra Sticker, etc...
}
```
