# 👨‍🚀 Preparing the model

For billables, you should follow the installation instructions given with Cashier for Paddle or Cashier for Stripe.

This package already sets the custom `Subscription` model. In case you want to add more functionalities to the Subscription model, make sure you extend accordingly from these models:

* Paddle: `RenokiCo\CashierRegister\Models\Paddle\Subscription`
* Stripe: `RenokiCo\CashierRegister\Models\Stripe\Subscription`

Further, make sure you check the `saas.php` file and replace the subscription model from there, or you can use the `::useSubscriptionModel` call in your code.

Cashier Register already does that for you in the background, but feel free to replace them with your models if you need to.
