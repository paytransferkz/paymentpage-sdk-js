# PaytransferKZ Javascript package

[![Build Status](https://travis-ci.com/paytransferkz/paymentpage-sdk-js.svg?branch=main)](https://travis-ci.com/paytransferkz/paymentpage-sdk-js)

### What is it?

It is package that will help you with generating payment URL according to 
[PaytransferKZ documentation](https://developers.paytransfer.kz/en/en_PP_Integration.html).

### How to use?

#### Get payment page URL

1. Install the package (with your package manager):
```shell
npm install paytransferkz
yarn add paytransferkz
```

2. Require somewhere in your code, set parameters and get the URL:
```javascript
const { Payment } = require('paytransferkz');

// create Payment object with your account ID and secret salt
const e = new Payment('112', 'my_secret');

// set payment details 
e.paymentAmount = 1000;
e.paymentId = 'FFCD12-30';
e.paymentCurrency = 'USD';

// set another parameters, like success or fail callback URL, customer details, etc.

// get payment URL
const url = e.getUrl();
```

Now your can render payment `url` somewhere on your checkout page.

#### Receive callback from PaytransferKZ

Example with [Express](http://expressjs.com):
```javascript
const { Callback } = require('paytransferkz');

app.post('/payment/callback', function(req, res) {
  const callback = new Callback('secret', req.body);
  if (callback.isPaymentSuccess()) {
    const paymentId = callback.getPaymentId();
    // here is your code for success payment
  }
});
```
Note that `Callback` constructor throws Error if signature isn't valid.
