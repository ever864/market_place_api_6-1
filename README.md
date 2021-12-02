# Market Place API

This repository contains application example build into the [API on Rails 6](https://github.com/madeindjs/api_on_rails) book.

This final application will scratch the surface of being a market place where users will be able to place orders, upload products and more. There are plenty of options out there to set up an online store, such as [Shopify](http://shopify.com), [Spree](http://spreecommerce.com/) or [Magento](http://magento.com).

The purpose of this application is not only to teach you how to build an API with Rails but rather to teach you how to build an _evolutive_ and _maintainable_ API with Rails. That is, improve your current knowledge with Rails. On this journey, you will learn to:

- Building JSON responses
- Test your end-points with unit and functional tests
- Set up authentication with JSON Web Tokens (JWT)
- Optimize and cache the API

## Setup

```bash
git clone https://github.com/madeindjs/market_place_api_6
cd market_place_api_6
bundle install
rake db:create
rake db:migrate
```

## Usage

Create user

```sh
curl -X POST -d 'user[email]=toto@toto.fr' -d 'user[password]=toto1234' localhost:3000/api/v1/users
```

Obtain token

```sh
curl -X POST -d 'user[email]=toto@toto.fr' -d 'user[password]=toto1234' localhost:3000/api/v1/tokens
```

Manage product

```sh
export TKN="eyJhbG...WqaXAcnE" # from /api/v1/tokens
# create
curl -X POST -H "Authorization: $TKN" -d "product[title]=Bag" -d "product[price]=10" localhost:3000/api/v1/products
# update: publish and add stock
curl -X PATCH -H "Authorization: $TKN" -d "product[published]=true" -d "product[quantity]=2" localhost:3000/api/v1/products/19
# list
curl -H "Authorization: $TKN" localhost:3000/api/v1/products
# delete
curl -X DELETE -H "Authorization: $TKN" localhost:3000/api/v1/products/19
```

Manage order

```sh
export TKN="eyJhbG...WqaXAcnE" # from /api/v1/tokens
# create
curl -X POST -H "Authorization: $TKN" -d "order[product_ids_and_quantities][][product_id]=20" -d "order[product_ids_and_quantities][][quantity]=1" localhost:3000/api/v1/orders
# list
curl -H "Authorization: $TKN" localhost:3000/api/v1/orders
# show
curl -H "Authorization: $TKN" localhost:3000/api/v1/orders/7
```

## Requirments

- Ruby 2.5+
- Sqlite
