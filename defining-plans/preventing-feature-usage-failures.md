# 🎯 Sync usage values

Usually, the most fearful thing is that at some point, your `->recordUsage()` call will throw an error and you will not bill appropriately the amount of usage a customer has.

You can prevent this from happening by defining custom callbacks that will sync the current usage before any record transaction, making sure you try to record the feature usage based on the latest fresh information:

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

        Saas::syncFeatureUsage('seats', function ($subscription, Feature $feature) {
            // Make sure to calculate the total seats each time for the given Team subscription.
            return $subscription->billable->users()->count();
        });
    }
}

$subscription->recordFeatureUsage('seats', 3);
```

This can be a good use if you add Cashier Register to a new project where your users are already registered up, making it easier for you to sync the features.

It's highly recommended to avoid letting users consume amounts from features if they don't have enough left. For example, you should not let new users be added to a team if the team has occupied all the seats.
