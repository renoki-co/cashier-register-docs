# ✨ Features

You can attach features to the plans and you may check usage for each subscription on a specific feature:

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

        Saas::plan('Gold Plan', 'price_gold')->features([
            Saas::feature('Seats', 'seats', 5)->notResettable(),
        ]);
    }
}
```

```php
$subscription->recordFeatureUsage('seats', 3); // 3 new users joined

$subscription->getUsedQuota('seats'); // 3
$subscription->getRemainingQuota('seats') // 2
```
