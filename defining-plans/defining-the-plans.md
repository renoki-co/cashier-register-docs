# 🗾 Defining the plans

 In `CashierRegisterServiceProvider`'s `boot` method you may define the plans you need:

```php
use RenokiCo\CashierRegister\CashierRegisterServiceProvider as BaseServiceProvider;
use RenokiCo\CashierRegister\Saas;

class CashierRegisterServiceProvider extends BaseServiceProvider
{
    /**
     * Boot the service provider.
     *
     * @return void
     */
    public function boot()
    {
        parent::boot();

        Saas::currency('EUR');

        Saas::plan('Gold Plan', 'price_...')
            ->monthly(30)
            ->features([
                Saas::feature('Seats', 'seats', 5)->notResettable(),
            ]);
    }
}
```

Please note that the `::plan` method accepts a display name, and the following two parameters are that **plan identifiers in either Stripe or Paddle**. This will ensure the available plans have unique IDs and they will be processed accordingly when it comes to the billing process:

```php
use RenokiCo\CashierRegister\CashierRegisterServiceProvider as BaseServiceProvider;
use RenokiCo\CashierRegister\Saas;

class CashierRegisterServiceProvider extends BaseServiceProvider
{
    /**
     * Boot the service provider.
     *
     * @return void
     */
    public function boot()
    {
        parent::boot();

        Saas::plan('Gold Plan', 'price_monthly');
    }
}
```

### Defining yearly plans

By default, yearly plans are not included but you might specify it if you have some:

```php
use RenokiCo\CashierRegister\CashierRegisterServiceProvider as BaseServiceProvider;
use RenokiCo\CashierRegister\Saas;

class CashierRegisterServiceProvider extends BaseServiceProvider
{
    /**
     * Boot the service provider.
     *
     * @return void
     */
    public function boot()
    {
        parent::boot();

        Saas::plan('Gold Plan', 'price_monthly', 'price_yearly');
    }
}
```

### Retrieving the plans

```php
use RenokiCo\CashierRegister\Saas;

$allPlans = Saas::getPlans();

foreach ($allPlans as $plan) {
    $features = $plan->getFeatures();
}
```

When retrieving a specific plan by Plan ID, you may pass the identifier:

```php
use RenokiCo\CashierRegister\Saas;

$plan = Saas::getPlan('price_monthly');
```

Please note that if the yearly plan ID is defined, you can also retrieved by it. However, the `->getId()` and `->getYearlyid()` are different:

```php
use RenokiCo\CashierRegister\Saas;

$plan = Saas::getPlan('price_yearly');

$plan->getId(); // price_monthly
$plan->getYearlyId(); // price_yearly
```

### Deprecating/Archiving plans

Deprecating plans can occur anytime. In order to do so, just call `deprecated()` when defining the plan:

```php
use RenokiCo\CashierRegister\Saas;

/**
 * Boot the service provider.
 *
 * @return void
 */
public function boot()
{
    parent::boot();

    Saas::plan('Silver Plan', 'silver-plan-id')->deprecated();
}
```

As an alternative, you can anytime retrieve the available plans only:

```php
use RenokiCo\CashierRegister\Saas;

$plans = Saas::getAvailablePlans();
```

### Setting the plan as popular

You may define a popular plan:

```php
use RenokiCo\CashierRegister\Saas;

Saas::plan('Gold Plan', 'gold-plan')
    ->popular();
```

This will add a data field called `popular` that is either `true/false`
