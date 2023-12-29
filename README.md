# asdf-postgres [![Build](https://github.com/smashedtoatoms/asdf-postgres/actions/workflows/build.yml/badge.svg)](https://github.com/smashedtoatoms/asdf-postgres/actions/workflows/build.yml)

Postgresql plugin for [asdf](https://github.com/asdf-vm/asdf) version manager

## Dependencies

- openssl
- libreadline
- zlib
- curl
- uuid
- icu-devtools (linux)

_This assumes macOS, a Debian-flavored linux, or a SUSE-flavored linux.  If you
need it to work on something else, you may need to modify the plugin. You'll
need the dependencies referenced in the list above installed via whatever method
you prefer. There are some suggestions below._

### Mac

```sh
brew install gcc readline zlib curl ossp-uuid
```

If you are on Apple silicon, you may need to set the HOMEBREW_PREFIX environment
variable to `/opt/homebrew`. You can do this by putting `export
HOMEBREW_PREFIX=/opt/homebrew` in your `~/.zshrc` file. It isn't always
required, but I don't know why this is required for some people.  The same goes
for intel machines only the prefix is `/usr/local`, which can also be dropped
into your `~/.zshrc` file `export HOMEBREW_PREFIX=/usr/local`.

### Ubuntu

```sh
sudo apt-get install linux-headers-$(uname -r) build-essential libssl-dev
libreadline-dev zlib1g-dev libcurl4-openssl-dev uuid-dev icu-devtools libicu-dev
```

### Ubuntu (WSL)

```sh
sudo apt-get install build-essential libssl-dev libreadline-dev zlib1g-dev
libcurl4-openssl-dev uuid-dev icu-devtools libicu-dev
```

### Fedora

```sh
sudo dnf install openssl-devel readline-devel zlib-devel libcurl-devel uuid-devel libuuid-devel
```

### (open)SUSE

```
sudo zypper install -t pattern devel_basis
sudo zypper in openssl-devel readline-devel zlib-devel libcurl-devel uuid-devel libuuid-devel
```

## Install

```
asdf plugin-add postgres
```

## ASDF options

Check [asdf](https://github.com/asdf-vm/asdf) readme for instructions on how to
install & manage versions of Postgres.

When installing Postgres using `asdf install`, you can pass custom configure
options with the following env vars:

- `POSTGRES_CONFIGURE_OPTIONS` - use only your configure options
- `POSTGRES_EXTRA_CONFIGURE_OPTIONS` - append these configure options along with
  ones that this plugin already uses (curl, openssl, readline, zlib, uuid)

These options can be passed at runtime, or set in
`~/.asdf-postgres-configure-options`. This file will be sourced at `asdf
install` time if it exists.

For example, if you want to compile with a specific set of openssl libraries,
you might do something like `POSTGRES_EXTRA_CONFIGURE_OPTIONS="--with-uuid=e2fs
--with-openssl --with-libraries=/usr/local/lib:/usr/local/opt/openssl@1.1/lib
--with-includes=/usr/local/include:/usr/local/opt/openssl@1.1/include" asdf
install postgres`

The option `POSTGRES_SKIP_INITDB` can be used to skip `initdb` command which is
not allowed to run from `root` account.

# How to use (easier version)

## Install

1. Create your .tool-versions file in the project that needs postgres and add
   `postgres 9.4.7` or whatever version that you want.
2. run `asdf install`

## Run

1. Once it is done, run `pg_ctl start`
2. Once that starts, run `createdb default` _you can sub `default` with whatever
   you want your db name to be._
3. Then log in with `psql -d default` _if you didn't use default, make sure you
   use whatever you put in step 2._
4. If you need to move your data file around, move data from your install
   directory, which will look something like this:
   `~/.asdf/installs/postgres/9.4.7/data` to wherever you want it. Once it is
   moved, start your db with `pg_ctl -D wherever/you/moved/it start`. Your
   postgresql.conf file is in that directory if you need to change the port or
   anything.

## Stop

1. Just run `pg_ctl stop` if you moved your data directory, you have to do
   `pg_ctl -D wherever/you/moved/it stop`
