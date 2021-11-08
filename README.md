---
description: >-
  Cashier Register is a simple quota feature usage tracker for Laravel Cashier
  subscriptions.
---

# ⚡ Introduction

![](.gitbook/assets/Cashier\_Register\_25.png)

[![CI](https://github.com/renoki-co/cashier-register/workflows/CI/badge.svg?branch=master)](https://github.com/renoki-co/cashier-register/workflows/CI/badge.svg?branch=master) [![codecov](https://camo.githubusercontent.com/bfece360d9a8e308e8c65a29b75492565150de9bfdb2e519a348ea4d7dcb2713/68747470733a2f2f636f6465636f762e696f2f67682f72656e6f6b692d636f2f636173686965722d72656769737465722f6272616e63682f6d61737465722f67726170682f62616467652e737667)](https://codecov.io/gh/renoki-co/cashier-register/branch/master) [![StyleCI](https://camo.githubusercontent.com/1cb21946144ee46c0d4482f27d9e210c62b3cb864d9eda861925ae68065a7d7f/68747470733a2f2f6769746875622e7374796c6563692e696f2f7265706f732f3237373130393435362f736869656c643f6272616e63683d6d6173746572)](https://github.styleci.io/repos/277109456) [![Latest Stable Version](https://camo.githubusercontent.com/0222a920352f9d01c5233a52e0379cded2432631356ecfc054a9f0b058c283f0/68747470733a2f2f706f7365722e707567782e6f72672f72656e6f6b692d636f2f636173686965722d72656769737465722f762f737461626c65)](https://packagist.org/packages/renoki-co/cashier-register) [![Total Downloads](https://camo.githubusercontent.com/e779e17604d93fc7d78b1108979ac3bd140e9641c30881134ad9a465372d920d/68747470733a2f2f706f7365722e707567782e6f72672f72656e6f6b692d636f2f636173686965722d72656769737465722f646f776e6c6f616473)](https://packagist.org/packages/renoki-co/cashier-register) [![Monthly Downloads](https://camo.githubusercontent.com/4f200cc5bb3ce4c129f59daa1cd7d9254e31532e637977d053aa7ee5e2230cb5/68747470733a2f2f706f7365722e707567782e6f72672f72656e6f6b692d636f2f636173686965722d72656769737465722f642f6d6f6e74686c79)](https://packagist.org/packages/renoki-co/cashier-register) [![License](https://camo.githubusercontent.com/23cb2014e5899c38777abb665038ffc07a52a388012d34484985420284e8d75f/68747470733a2f2f706f7365722e707567782e6f72672f72656e6f6b692d636f2f636173686965722d72656769737465722f6c6963656e7365)](https://packagist.org/packages/renoki-co/cashier-register)

Cashier Register is a simple quota feature usage tracker for Laravel Cashier subscriptions.

It helps you define static, project-level plans, and attach features that can be tracked and limited throughout the app. For example, you might want to set a limit of `5` seats per team and make it so you can check it later. Cashier Register comes with a nice wrapper for Laravel Cashier that does that out-of-the-box.
