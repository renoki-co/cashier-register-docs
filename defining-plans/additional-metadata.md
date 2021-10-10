# 🧵 Metadata

Items, plans, and features implement a `->data()` method that allows you to attach custom data for each item:

```php
use RenokiCo\CashierRegister\Saas;

Saas::plan('Gold Plan', 'gold-plan')
    ->data(['golden' => true])
    ->features([
        Saas::feature('Seats', 'seats')
            ->data(['digital' => true])
            ->unlimited(),
    ]);
```

```php
$plan = Saas::getPlan('gold-plan');
$feature = $plan->getFeature('seats');

$planData = $plan->getData(); // ['golden' => true]
$featureData = $feature->getData(); // ['digital' => true]
```
