# 🔧 Types of values

### Unlimited amounts

To set an infinite amount of usage, use the `unlimited()` method. You can consume as much as you want from the feature, and it will never exceed the quota:

```php
use RenokiCo\CashierRegister\Saas;

Saas::plan('Gold Plan', 'gold-plan')->features([
    Saas::feature('Seats', 'seats')->unlimited(),
]);
```

### Float amounts

The package comes with migrations that allow only unsigned small integers for `used` and `used_total`. Optionally, if you wish to have float values, you might just change the field type after publishing the migrations:

```php
Schema::create('subscription_usages', function (Blueprint $table) {
    $table->float('used', 8, 2);
    $table->float('used_total', 8, 2);
});
```
