# 🧓 Inherit features from other plans

You may copy the base features from a given plan and overwrite same-ID features for new plans.

In the following example, the `Paid Plan` has unlimited seats (compared with the 10 seats per Free Plan) and a new feature called `beta.access` that is exclusively for the paid plan.

```php
use RenokiCo\CashierRegister\Saas;

$freePlan = Saas::plan('Free Plan', 'free-plan')->features([
    Saas::feature('Seats', 'seats')->value(10),
]);

$paidPlan = Saas::plan('Paid Plan', 'paid-plan')->inheritFeaturesFromPlan($freePlan, [
    Saas::feature('Seats', 'seats')->unlimited(), // same-ID features are replaced
    Saas::feature('Beta Access', 'beta.access')->unlimited(), // new IDs are merged
]);
```

 **Keep in mind, avoid using further `->features()` when inheriting from another plan.**
