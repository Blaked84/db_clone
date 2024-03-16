# DbClone

DbClone is a simple rake task to download your heroku db to replace your current local database.

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'db_clone'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install db_clone

## Usage

This gem provide 2 rake tasks to clone your heroku database to your local database.

### `db:clone_prod`

Create a new backup of your production database and download it to your local database.
The backup will be saved in `tmp/latest.dump`.
The backup is then automatically restored to your local database using `rake db:import_last_backup`.

### `db:import_last_backup`
Recreate your local database (development per default) and import the latest backup from `tmp/latest.dump`.
It then run missing migrations

### Options

You can use the `PG_RESTORE_ARGS` environment variable to pass additional arguments to `pg_restore` when importing the backup.
For example, you may want to use multiple threads to speed up the import:

```bash
PG_RESTORE_ARGS="-j4" rake db:import_last_backup
```

You can also make the output verbose :
```bash
PG_RESTORE_ARGS="--verbose" rake db:import_last_backup
```


## Development

After checking out the repo, run `bin/setup` to install dependencies. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/[USERNAME]/db_clone. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [Contributor Covenant](http://contributor-covenant.org) code of conduct.


## License

The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).

