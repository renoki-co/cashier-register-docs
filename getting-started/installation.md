# 🚀 Installation

### Installing the package

Hop into your console and install the package via Composer:

```bash
composer require renoki-co/cashier-register
```

Publish the config file:

```bash
php artisan vendor:publish --provider="RenokiCo\CashierRegister\CashierRegisterServiceProvider" --tag="config"
```

Publish the migrations:

```bash
php artisan vendor:publish --provider="RenokiCo\CashierRegister\CashierRegisterServiceProvider" --tag="migrations"
```

The package does not come with Cashier as a dependency, so you should install it according to your needs:

#### Cashier for Stripe

```bash
composer require laravel/cashier:"^12.13"
```

#### Cashier for Paddle

```bash
composer require laravel/cashier-paddle:"^1.4.4"
```
