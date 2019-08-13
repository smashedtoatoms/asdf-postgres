# asdf-postgres

Postgresql plugin for [asdf](https://github.com/asdf-vm/asdf) version manager

## Dependencies
_This requires [brew](http://brew.sh) if you're on a mac, or a debian flavored linux.  If you need it to work on something else, you'll likely need to modify the plugin._  

1. You will need a compiler.
  * Mac
    1. ```gcc```
    1. Hit the ok button and it will install.  If it already has it, then you are good.
  * Ubuntu  
    1. ```sudo apt-get install linux-headers-$(uname -r) build-essential```
1. On Ubuntu, you will need libreadline
  1. ```sudo apt-get install libreadline-dev```
1. On Ubuntu 19.04, you will need curl and zlib
  1. ```sudo apt-get install zlib1g-dev curl```


## Install

```
asdf plugin-add postgres https://github.com/smashedtoatoms/asdf-postgres.git
```

## ASDF options

Check [asdf](https://github.com/asdf-vm/asdf) readme for instructions on how to install & manage versions of Postgres.

When installing Postgres using `asdf install`, you can pass custom configure options with the following env vars:

* `POSTGRES_CONFIGURE_OPTIONS` - use only your configure options
* `POSTGRES_EXTRA_CONFIGURE_OPTIONS` - append these configure options along with ones that this plugin already uses

These options can be passed at runtime, or set in `~/.asdf-postgres-configure-options`. This file will be sourced at `asdf install` time if it exists.

# How to use (easier version)
## Install
1. Create your .tool-versions file in the project that needs postgres and add `postgres 9.4.7` or whatever version that you want.
2. run `asdf install`

## Run
1. Once it is done, run `pg_ctl start`
2. Once that starts, run `createdb default` _you can sub `default` with whatever you want your db name to be._
3. Then log in with `psql -d default` _if you didn't use default, make sure you use whatever you put in step 2._
4. If you need to move your data file around, move data from your install directory, which will look something like this: `~/.asdf/installs/postgres/9.4.7/data` to wherever you want it.  Once it is moved, start your db with `pg_ctl -D wherever/you/moved/it start`.  Your postgresql.conf file is in that directory if you need to change the port or anything.

## Stop
1. Just run `pg_ctl stop`  if you moved your data directory, you have to do `pg_ctl -D wherever/you/moved/it stop`
