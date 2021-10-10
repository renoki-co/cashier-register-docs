# 🚫 Mid-Exceed Quotas in Stripe Metered Billing

When exceeding the allocated quota for a specific feature when recording, [t](https://github.com/renoki-co/cashier-register#metered-features)he Metered Billing comes in and bills for extra metered usage, but only if the feature is defined as [Metered Feature](metered-features.md).

```php
use RenokiCo\CashierRegister\Saas;

Saas::plan('Gold Plan', 'gold_price')->features([
    Saas::meteredFeature('Seats', 'seats', 5), // included: 5
        ->meteredPrice('price_metered_identifier', 3, 'seat'), // on-demand: $0.01/minute
]);
```

```php
$subscription->recordFeatureUsage('seats', 3); // 3 new users joined, 2 seats remaining

$subscription->recordFeatureUsage('seats', 4, true, function ($feature, $valueOverQuota, $subscription) {
    // From the used 3 seats, 5 are free. It remains only 2 seats.
    // The user wants another 4 seats, so Stripe Metered Billing is going to bill only 2, the remaining over quota.

    // Here you can run custom logic to handle overflow. The metered billing usage report was already done.
});
```
