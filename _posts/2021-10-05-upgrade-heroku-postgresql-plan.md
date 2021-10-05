---
layout: single
title: Upgrading Heroku Postgres Plan
description: 
header:
  overlay_image: assets/images/development/header.jpg
  caption: Photo by [Arnold Francisca](https://unsplash.com/@clark_fransa?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)
    on [Unsplash](https://unsplash.com/s/photos/staring-at-laptop?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)
  show_overlay_excerpt: false
category:
- development
tags:
- heroku
- postgres
- postgresql
- database
- devops
classes: wide
date: '2021-10-05 13:00:00 +0000'
---
# Upgrading Heroku Postgres Plan

So you built your MVP on Heroku, you have tested your idea and it has gained tracking.  Now your hobby database is reaching its limit and 30 minutes of downtime is no longer acceptable.  You've decided to upgrade your database to the standard package.  How do you go about doing that with minimum downtime? 

I'll show you how to provision a new database, create a back up of the existing database, and how to replace your hobby database with a new database. 

You'll need to have the Heroku cli installed in your local machine.
Installing and configuring the cli is straightforward, but outside of the scope of this post.  You can find more information [here](https://devcenter.heroku.com/articles/heroku-cli). 

Now that you have the CLI installed let's begin.

## Find your database information

```term
heroku pg:info
```

This should return the name of the existing database (e.g. `DATABASE_URL`)

## Put the app into maintenance mode

Setting the app in maintenance mode will prevent any writes to the existing database.

```term
heroku maintenance:on 
```

You have to do this in so that we create a clean backup.

## Create a backup of the database

```term
heroku pg:backups:capture DATABASE_URL --app awesome
```

While this is not necessary, it is better to have and not need, than need and not have.

## Provision the new database

```term
heroku addons:create heroku-postgresql:standard-0
```

Wait for the database to come online, this may take a while depending on the plan you've selected.  In this example we've selected `standard-0` but there are [others available](https://devcenter.heroku.com/articles/heroku-postgres-plans).

## Copy data into the new database

Once the database is ready, you can copy the data from the existing database into the new database.

```term
heroku pg:copy DATABASE_URL HEROKU_POSTGRESQL_GOLD_URL --app awesome
```

## Promote the new database

Promoting the new database will make it the primary database for the application.  You are almost done. 

```term
heroku pg:promote HEROKU_POSTGRESQL_GOLD_URL
```

## Turn maintenance off 

Allow new writes against the new database

```term
heroku maintenance:off
```

## Delete the old database 

You are now running your app against the new database, and you can erase your old database.  Keep in mind that its original name may have changed. 

```term
heroku addons:destroy HEROKU_POSTGRESQL_BRONZE_URL
```

## 🎉 Congratulations! 

Your app is now running on a much better database, with less downtime and you can sleep well knowing your app is ready for more users.

## Summary

I have showed you 
- how to find your database information
- turn maintenance mode on
- create a backup
- provision a new database 
- transfer data to the new database
- promote the new database

## Resources

- [Upgrading with pg:copy](https://devcenter.heroku.com/articles/upgrading-heroku-postgres-databases#upgrading-with-pg-copy)
