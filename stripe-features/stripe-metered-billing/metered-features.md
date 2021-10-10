# 🎭 Metered Features

Metered features are opened for Stripe only and this will open up custom metering for exceeding quotas on features.

You might want to give your customers a specific amount of a feature, let's say `Build Minutes`, but for an exceeding amount of minutes, you might invoice at the end of the month a price of `$0.01` per minute:

```php
use RenokiCo\CashierRegister\Saas;

Saas::plan('Gold Plan', 'gold-plan')->features([
    Saas::meteredFeature('Build Minutes', 'build.minutes', 3000), // included: 3000
        ->meteredPrice('price_identifier', 0.01, 'minute'), // on-demand: $0.01/minute
]);
```

If you simply want just the on-demand price of the metered feature, just omit the amount:

```php
use RenokiCo\CashierRegister\Saas;

Saas::plan('Gold Plan', 'gold-plan')->features([
    Saas::meteredFeature('Build Minutes', 'build.minutes'), // included: 0
        ->meteredPrice('price_identifier', 0.01, 'minute'), // on-demand: $0.01/minute
]);
```

**The third parameter is just a conventional name for the unit. `0.01` is the price per unit (PPU). In this case, it's `minute` and `$0.01`, assuming the plan's price is in USD.**
