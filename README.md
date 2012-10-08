# tentd-admin

tentd-admin implements a very basic administration interface for
[tentd](https://github.com/tent/tentd). It also mounts tentd as a Rack app, so
it's the easiest way to get started with a [Tent Protocol](http://tent.io)
implementation.


## Getting Started

### Cloud Foundry

```shell
vmc push --no-start
vmc env-add tentd-admin ADMIN_USERNAME=admin
vmc env-add tentd-admin ADMIN_PASSWORD=password
vmc env-add tentd-admin SERVE_ASSETS=1
vmc start tentd-admin
```

### Heroku

```shell
heroku create --addons heroku-postgresql:dev
heroku pg:promote $(heroku pg | head -1 | cut -f2 -d" ")
heroku config:add ADMIN_USERNAME=admin ADMIN_PASSWORD=password SERVE_ASSETS=1
git push heroku master
heroku open
```

### Ruby

tentd-admin requires Ruby 1.9. If you don't have Ruby 1.9 you can use your
operating system's package manager to install it.

#### OS X

The easiest way to get Ruby 1.9 on OS X is to use [Homebrew](http://mxcl.github.com/homebrew/).

```shell
brew install ruby
```

If you need to switch between ruby versions, use
[rbenv](https://github.com/sstephenson/rbenv) and
[ruby-build](https://github.com/sstephenson/ruby-build).


#### Ubuntu

```shell
sudo apt-get install build-essential ruby1.9.1-full libxml2 libxml2-dev libxslt1-dev
sudo update-alternatives --config ruby # make sure 1.9 is the default
```


### PostgreSQL

tentd-admin requires a PostgreSQL database.

#### OS X

Use [Homebrew](http://mxcl.github.com/homebrew/) or [Postgres.app](http://postgresapp.com/).

```shell
brew install postgresql
createdb tent_server
```


### Bundler

Bundler is a project dependency manager for Ruby.

```
gem install bundler
```


### Starting tentd-admin

Clone this repository, and `cd` into the directory. This should start the app:

```shell
bundle install
DATABASE_URL=postgres://localhost/tent_server ADMIN_USERNAME=admin ADMIN_PASSWORD=admin bundle exec puma -p 3000
```

If all goes well, you'll have a Tent server available at
[http://localhost:3000/](http://localhost:3000/) and you can log into the admin
interface at [http://localhost:3000/admin](http://postgresapp.com/) with the
username and password `admin`. After setting up the base profile in the admin,
this should show the profile JSON:

```shell
curl http://localhost:3000/profile
```


## Contributing

Currently tentd-admin only implements app authentication and following creation.
These are some things that could be done to improve the app:

- Add support for managing (CRUD) all of the data in Tent: profiles, followers,
  followings, apps, and posts.
- Add a log in the UI of API calls to tentd for easy debugging.
- Write tests and refactor the code.
- Make a pretty UI.
- Allow creation of the database and setting username/password from the UI.
- Show better app details in OAuth flow (icon, post/profile type details)
- Replace tentd database hooks with API calls
- Create an omnibus-style package that installs and configures everything needed
  to get started with tentd-admin.
