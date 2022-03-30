# Transitmix [![Build Status](https://travis-ci.org/codeforamerica/transitmix.svg?branch=master)](https://travis-ci.org/codeforamerica/transitmix)

[Transitmix](http://transitmix.net/) is a sketching tool for transit planners. The tool makes it easy to draw new transit lines, understand the underlying costs, and share ideas with the public. So far, Transitmix been used to generate 30,000 new transit maps for more than 3,600 cities across the world, all powered by open data and data standards ([OpenStreetMap](http://openstreetmap.org), [Open Source Routing Machine](http://project-osrm.org), and the [Google Transit Feed Specification](http://www.gtfs-data-exchange.com/).

The project comes from a team at [Code for America](http://codeforamerica.org), a non-profit based in San Francisco focused on building better cities through technology.

Contact us at [transitmix@codeforamerica.org](mailto:transitmix@codeforamerica.org).

### Who is this made by?

- [Sam Hashemi](https://twitter.com/oksamuel)
- [Dan Getelman](https://twitter.com/dget)
- [Tiffany Chu](https://twitter.com/tchu88)
- [Danny Whalen](https://twitter.com/invisiblefunnel)
- [Lyzi Diamond](https://twitter.com/lyzidiamond)

With additional help from [Jason Denizac](https://github.com/jden), [Becky Boone](https://github.com/boonrs), [Maksim Pecherskiy](https://github.com/mrmaksimize), and [Andrew Douglass](https://github.com/ardouglass).

### How can I help?

* Check out our GitHub Issues page [here](https://github.com/codeforamerica/transitmix/issues/).

### Setup

Transitmix is a Ruby application with a PostgreSQL database.

1. [Install PostgreSQL](https://github.com/codeforamerica/howto/blob/master/PostgreSQL.md).
2. [Install Ruby](https://github.com/codeforamerica/howto/blob/master/Ruby.md).

Using the command line, clone Transmitmix from Github and prepare the database:
   
```console
git clone https://github.com/codeforamerica/transitmix.git
cd transitmix
cp .env.sample .env
bundle install
rake db:create db:migrate
rake db:create db:migrate DATABASE_URL=postgres://localhost/transitmix_test
bundle exec rackup
```

### Deploying to Heroku

```console
heroku create <app name>
heroku addons:add heroku-postgresql
git push heroku master
heroku run rake db:migrate
heroku open
```

### Deploying with Docker

```console
docker build -t transitmix .
docker run -d --name transitmix_postgres -e POSTGRES_PASSWORD=mypass -e POSTGRES_USER=transit postgres:14
docker run -it --rm -e DATABASE_URL=postgres://transit:mypass@transitmix_postgres/transit transitmix rake db:create db:migrate
docker run -d -p 9292:9292 -e DATABASE_URL=postgres://transit:mypass@transitmix_postgres/transit -e MAP_ID=MAPBOX_API_KEY transitmix
```

### Additional Setup Notes

#### Error Logging

Transitmix can be configured to log runtime errors to an external service like [Airbrake](https://airbrake.io/) or [Errbit](https://github.com/errbit/errbit). Set the `ERROR_LOG_KEY` and `ERROR_LOG_HOST` environment variables to enable the extension.

#### Testing References

* Javascript: [Jasmine](http://jasmine.github.io/)
* Ruby: [RSpec](https://www.relishapp.com/rspec)
