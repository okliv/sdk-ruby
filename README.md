# Ruby gem for LiqPay.com API

Ruby gem wrapper for official Liqpay SDK https://github.com/liqpay/sdk-ruby

## Installation

Add the gem to your Gemfile:

```ruby
gem 'liqpay', github: 'okliv/sdk-ruby'
```

And don't forget to run Bundler:

```shell
$ bundle install
```

## Configuration

Get API keys on https://www.liqpay.com/ and save them in config:
 
```ruby
# config/initializers/liqpay.rb

::Liqpay.configure do |config|
  config.public_key = 'public_key'
  config.private_key = 'private_key'
end
```

You can also store API keys in `ENV['LIQPAY_PUBLIC_KEY']` and `ENV['LIQPAY_PRIVATE_KEY']`

## Usage

```ruby
require 'liqpay'
liqpay = Liqpay.new
liqpay.api 'invoice/send', { email: 'test@example.com', amount: 100, currency: 'UAH',
  order_id: 1,
  goods: [{
              amount: 100,
              count: 1,
              unit: 'pcs',
              name: 'Order' }]}

```
subscriptions:

```ruby

liqpay = Liqpay::Liqpay.new
liqpay.cnb_form({
                               :action         => 'subscribe',
                               :amount         => 100500,
                               :currency       => 'USD',
                               :description    => 'description',
                               :order_id       => 'un1q_0rd3r_1d', #some order_id
                               :version        => '3',
                               server_url: url_helpers.liqpay_payment_url,
                               result_url: url_helpers.root_url,
                               subscribe: 1,
                               subscribe_periodicity: 'month',
                               subscribe_date_start: Time.zone.now.strftime('%F %T'),
                               sandbox: 1, #if you want to test before actual transactions
                               customer: current_user.id, #in case you can pass the user id it is helpful to hook after payment actions to user
                               language: 'en'
                               # paytypes: %w(card masterpass)
                           })
  end

```


Full Liqpay API documentation is available on https://www.liqpay.com/en/doc

## Tests

To pass the API tests, specify API keys in `ENV['LIQPAY_PUBLIC_KEY']` and `ENV['LIQPAY_PRIVATE_KEY']`
or in `spec/dummy/config.rb`:

```ruby
# spec/dummy/config.rb
::Liqpay.configure do |config|
  config.public_key = 'public_key'
  config.private_key = 'private_key'
end
```





