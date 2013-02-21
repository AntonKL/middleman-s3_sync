# Middleman::S3Sync

This gem determines which files need to be added, updated and optionally deleted
and only transfer these files up. This reduces the impact of an update
on a web site hosted on S3.

## Why not Middleman Sync?

[Middleman Sync](https://github.com/karlfreeman/middleman-sync) does a
great job to push [Middleman](http://middlemanapp.com)  generated
websites to S3. The only issue I have with it is that it pushes
every files under build to S3 and doesn't seem to properly delete files
that are no longer needed.

## Installation

Add this line to your application's Gemfile:

    gem 'middleman-s3_sync'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install middleman-s3_sync

## Usage

You need to add the following code to your ```config.rb``` file:

```ruby
activate :s3_sync do |s3_sync|
  s3_sync.bucket                = 'my.bucket.com' # The name of the S3 bucket you are targetting. This is globally unique.
  s3_sync.region                = 'us-west-1'     # The AWS region for your bucket.
  s3_sync.aws_access_key_id     = 'AWS KEY ID'
  s3_sync.aws_secret_access_key = 'AWS SECRET KEY'
  s3_sync.delete                = false # We delete stray files by default.
  s3_sync.after_build           = false # We chain after the build step by default. This may not be your desired behavior...
end
```

You can then start synchronizing files with S3 through ```middleman s3_sync```. 

## A Debt of Gratitude

I used Middleman Sync as a template for building a Middleman extension.
The code is well structured and easy to understand and it was easy to
extend it to add my synchronization code. My gratitude goes to @karlfreeman
and is work on Middleman sync.

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request