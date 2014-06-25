Deploying to Heroku
===================

If you get stuck at any point, run `heroku logs -t` and watch the output. The application provides pretty good hints with regards to missing configuration, such as:

```
 ==========================================
 Oh no! Gittip.com needs these missing 
 environment variables:
  
   BALANCED_API_SECRET
   ...
   VENMO_CLIENT_SECRET
  
 (Sorry, we must've started looking for 
 these since you last updated Gittip!)
```

### Create a new app

* `heroku create --buildpack git://github.com/heroku/heroku-buildpack-python.git`
* `heroku addons:add heroku-postgresql`
	* Get the DATABASE_URL config var from your application
	* `DATABASE_URL=my_db_url ./recreate_schema.sh`
* Create OAuth clients
	* Github
	* Twitter
	* Bitbucket
* Set required app config
	* heroku config:set SENTRY_DSN=
	* heroku config:set SEGMENT_KEY=
	* heroku config:set MANDRILL_KEY=
	* heroku config:set TESTING=no
	* heroku config:set MIN_THREADS=10
	* heroku config:set DATABASE_MAXCONN=10
	* heroku config:set NANSWERS_THRESHOLD=2
	* heroku config:set LOG_BUSY_THREADS_EVERY=0
	* heroku config:set LOG_METRICS=0
* Set up HTTPS
	* heroku config:set CANONICAL_HOST=myappname.herokuapp.com
	* heroku config:set CANONICAL_SCHEME=https