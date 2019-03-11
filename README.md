# Fosdick

This Ruby gem wraps the Fosdick Fulfillment API.

[![Build Status](https://travis-ci.org/teamlaunch/fosdick-ruby.svg?branch=master)](https://travis-ci.org/teamlaunch/fosdick-ruby)

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'fosdick'
```

And then execute:

    $ bundle

## Configuration

You'll need to configure Fosdick with your settings:

```ruby
Fosdick.configure do |config|
  config.client_code = ENV['FOSDICK_CLIENT_CODE']
  config.client_name = ENV['FOSDICK_CLIENT_NAME']
  config.username = ENV['FOSDICK_USERNAME']
  config.password = ENV['FOSDICK_PASSWORD']
end
```

If you're using this gem in a Rails app, you'll probably want to put this config in an initializer.

## Usage

## Parameters

### Timestamps

Any resource can be filtered by `updated_at_min` and `updated_at_max` to only get records updated after or before a timestamp. For example, your application might keep track of the last time it fetched inventory data, and provide that timestamp for `updated_at_min` to only get records updated since then.

### Pagination

By default, all resources will be fetched by default. However, in case there's a lot of data, any resource can be fetched page by page using the `page` and `per_page` options. For example: `Fosdick::Inventory.all(per_page: 30, page: 2)`.

## Resources

### Inventory

```ruby
Fosdick::Inventory.all(params)
```

Parameter:

* `updated_at_min`
* `updated_at_max`

### Returns

```ruby
Fosdick::Return.all(params)
```

Parameters:

* `updated_at_min`
* `updated_at_max`
* `returned_at_min`
* `returned_at_max`

### Shipments

```ruby
Fosdick::Shipment.all(params)
```

Parameters:

* `updated_at_min`
* `updated_at_max`
* `shipped_on_min` - fetches shipments shipped since this timestamp
* `shipped_on_max` - fetches shipments shipped until this timestamp
* `fosdick_order_num` - fetches shipment for a specific order
* `external_order_num` - fetches shipment for a specific order

### Shipment Detail

```ruby
Fosdick::ShipmentDetail.all(params)
```

Parameters:

* `updated_at_min`
* `updated_at_max`
* `shipped_on_min` - fetches shipment detail for shipments shipped since this timestamp
* `shipped_on_max` - fetches shipment detail for shipments shipped until this timestamp
* `fosdick_order_num` - fetches shipment for a specific order
* `external_order_num` - fetches shipment for a specific order

## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `rake spec` to run the tests. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and merge to master on GitHub, then run `bundle update fosdick` in the directory for the ecommerce project.
That will update the Fosdick gem version in Gemfile.lock, which you should commit and push to the whatever branch you use for the ecommerce app's gem version bump PR.

## License

The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).

