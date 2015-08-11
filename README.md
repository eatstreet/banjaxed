# Banjaxed [![Build Status](https://travis-ci.org/intercom/banjaxed.svg?branch=master)](https://travis-ci.org/intercom/banjaxed) [![Code Climate](https://codeclimate.com/github/intercom/banjaxed/badges/gpa.svg)](https://codeclimate.com/github/intercom/banjaxed) [![Coverage Status](https://coveralls.io/repos/intercom/banjaxed/badge.svg?branch=master)](https://coveralls.io/r/intercom/banjaxed?branch=master) [![Dependency Status](https://gemnasium.com/intercom/banjaxed.svg)](https://gemnasium.com/intercom/banjaxed)

Banjaxed is an incident management tool.


# Configuration

GitHub OAuth is used to authenticate users. You'll need to [register an application](https://github.com/settings/applications/new) and make the details available as environment variables, as well as the organisation to use to restrict access.

| Name                 | Purpose                                                    | Required? |
| -------------------- | ---------------------------------------------------------- | --------- |
| GITHUB_CLIENT_ID     | GitHub OAuth client ID to use for authentication.          | Yes       |
| GITHUB_CLIENT_SECRET | GitHub OAuth client secret to use for authentication.      | Yes       |
| GITHUB_ORG           | Only members of this GitHub organisation will have access. | No        |

If you don't specify a GitHub organisation, any authenticated GitHub user will have access.

## Others

Use `SENTRY_DSN` to load your Sentry DSN for exception logging

## Dotenv

In development you can set these environment variables with [dotenv](https://github.com/bkeepers/dotenv), by creating a `.env` file in the root of the project:

```
export GITHUB_CLIENT_ID=myid
export GITHUB_CLIENT_SECRET=mysecret
export GITHUB_ORG=myorg
```


# Deployment

Banjaxed is a simple Rails app and should be relatively straightforward to deploy.

It is configured to use Postgres by default, but should work with any Active Record database adapter.


## On Heroku

[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy)

Here's how you could deploy Banjaxed on Heroku from the command line:

```
git clone git@github.com:intercom/banjaxed.git
cd banjaxed
heroku apps:create
heroku addons:add heroku-postgresql
heroku config:set GITHUB_CLIENT_ID=x GITHUB_CLIENT_SECRET=y GITHUB_ORG=z
git push heroku
heroku run rake db:schema:load
heroku apps:open
```

Obviously, you'll want to use actual valid GitHub application details.

The GitHub application's callback URL will need to be updated to match the Heroku app.


# Screenshots

### Listing all incidents:

![banjaxed_index](https://cloud.githubusercontent.com/assets/432189/4662923/e3adcc62-5536-11e4-8553-adcdbd6e38ad.png)

### Viewing an incident:

![banjaxed_show](https://cloud.githubusercontent.com/assets/432189/4662925/e3cf2ede-5536-11e4-85ec-ba76abc45854.png)

### Creating a new incident:

![banjaxed_new](https://cloud.githubusercontent.com/assets/432189/4662924/e3c8e204-5536-11e4-96be-b85bda235a2b.png)
