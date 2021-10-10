# 🛑 Checking for exceeded quotas

Checking exceeded quotas can be useful when users fall back from a bigger plan to a smaller one. In this case, you may end up with an exceeded quota case where the users will have feature tracking values greater than the smaller plan values.

Before swapping, you might check the features from the lower plan and get the list of features that need to be handled:

```php
use RenokiCo\CashierRegister\Saas;

$freePlan = Saas::plan('Free Plan', 'price_free'); // already subscribed to this plan
$paidPlan = Saas::plan('Paid Plan', 'price_paid');

$overQuotaFeatures = $subscription->featuresOverQuotaWhenSwapping($paidPlan);

// If no features are over quotas before swapping, apply the plan swap.
if ($overQuotaFeatures->count() === 0) {
    $subscription->swap($freePlan->getId());
}

foreach ($overQuotaFeatures as $feature) {
    // $feature->getName();
}
```

### Catching Mid-Exceed Quotas

Naturally, `recordFeatureUsage()` has a callback parameter that gets called whenever the amount of consumption gets over the allocated total quota right when recording the usage.

For example, customers can have 5 seats in total, but when all of 5 seats are full, you might want to re-check the amount of exceeded quota and billing separately:

```php
$subscription->recordFeatureUsage('seats', 5); // 5 new users joined, 0 seats remaining

$subscription->recordFeatureUsage('seats', 3, true, function ($feature, $valueOverQuota, $subscription) {
    // $this->billUserForExtraSeats($subscription->model, $valueOverQuota);
    // or whatever...
});
```
