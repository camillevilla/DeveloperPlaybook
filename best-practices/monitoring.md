# Monitoring

## Honeybadger

We use [Honeybadger](https://www.honeybadger.io/) to monitor application exceptions and deployments. The [honeybadger docs](https://docs.honeybadger.io/ruby/integration-guides/rails-exception-tracking.html) contain instructions for how to set it up in a Rails application, but there is a wrinkle to consider as you do so. The instructions point out that installing will

"[g]enerate a config/honeybadger.yml file. If you don't like config files, you can place your API key in the $HONEYBADGER_API_KEY environment variable."

If you decide on the former approach, you will want to set up your honeybadger config file in [sul-dlss/shared_configs](https://github.com/sul-dlss/shared_configs). If you would like to use environment variables instead, you will need some assistance from operations to encrypt your project's API key and set up the necessary environment variables via [sul-dlss/puppet](https://github.com/sul-dlss/shared_configs).
