# 🕛 Resetting values

### Resetting tracked values

Each created feature is resettable - each time the billing cycle ends, you can call `resetQuotas` on the subscription to reset them.

You can have:

* consumable features, for example, the number of mails your client can send each month via your newsletter service
* non-resettable features, like team seats, the number of maximum projects at a time, etc.

The appropriate way is to be able to reset the quotas after each billing cycle. With Stripe, you might want to implement a Webhook controller listening to the `invoice.payment_succeeded` event:

```php
<?php

use Laravel\Cashier\Http\Controllers\WebhookController;

class StripeController extends WebhookController
{
    /**
     * Handle invoice payment succeeded.
     *
     * @param  array  $payload
     * @return \Symfony\Component\HttpFoundation\Response
     */
    public function handleInvoicePaymentSucceeded($payload)
    {
        if ($user = $this->getUserByStripeId($payload['data']['object']['customer'])) {
            $data = $payload['data']['object'];

            $subscription = $user->subscriptions()
                ->whereStripeId($data['subscription'] ?? null)
                ->first();

            if ($subscription) {
                $subscription->resetQuotas();
            }
        }

        return $this->successMethod();
    }
}
```

To avoid resetting, you may call `notResettable()` on the feature. This way, the quota reset won't occur on the `seats` feature.

```php
use RenokiCo\CashierRegister\Saas;

Saas::plan('Gold Plan', 'gold-plan')->features([
    Saas::feature('Seats', 'seats', 5)->notResettable(),
]);
```
