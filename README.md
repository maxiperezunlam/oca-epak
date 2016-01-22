# oca-epak
Ruby Wrapper for OCA e-Pak API

[![Gem Version](https://badge.fury.io/rb/oca-epak.svg)](http://badge.fury.io/rb/oca-epak)
[![Build Status](https://travis-ci.org/ombulabs/oca-epak.svg?branch=master)](https://travis-ci.org/ombulabs/oca-epak)

## Getting Started

For command line usage:

```bash
$ gem install oca-epak
```

If you intend to use it within an application, add `gem "oca-epak"` to your
`Gemfile`.

## Usage

First, initialize an Oca client:

```ruby
oca = Oca.new("your-email@example.com", "your-password")
```

To check whether your credentials are valid or not, run `#check_credentials`

```ruby
oca.check_credentials
=> true
```

NOTE: Keep in mind that you cannot register/create an operation code via Oca's
API, you have to get in touch with someone from Oca and they take care of the
registration.

After you have your operation code active for a given delivery type, you can
begin calculating shipping rates and delivery estimates:

```ruby
opts = { total_weight: "50", total_volume: "0.027", origin_zip_code: "1646",
         destination_zip_code: "2000", declared_value: "100",
         package_quantity: "1", cuit: "30-99999999-7", operation_code: "77790" }

oca.get_shipping_rate(opts)
=> [{:tarifador=>"15",
    :precio=>"328.9000",
    :id_tiposervicio=>"2",
    :ambito=>"Regional",
    :plazo_entrega=>"3",
    :adicional=>"0.0000",
    :total=>"328.9000",
    :xml=>"<row Tarifador=\"15\" Precio=\"328.9000\"/>",
    :"@diffgr:id"=>"Table1",
    :"@msdata:row_order"=>"0"}]
```

## Contributing & Development

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Write your feature (and tests)
4. Run tests (`bundle exec rake`)
5. Commit your changes (`git commit -am 'Added some feature'`)
6. Push to the branch (`git push origin my-new-feature`)
7. Create new Pull Request

## Release the Gem

```bash
$ bundle exec rake release
```
