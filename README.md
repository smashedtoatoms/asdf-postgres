# asdf-postgres

Postgresql plugin for [asdf](https://github.com/asdf-vm/asdf) version manager

## Install

```
asdf plugin-add postgresql https://github.com/smashedtoatoms/asdf-postgres.git
```

## Use

Check [asdf](https://github.com/asdf-vm/asdf) readme for instructions on how to install & manage versions of Postgres.

When installing Postgres using `asdf install`, you can pass custom configure options with the following env vars:

* `POSTGRES_CONFIGURE_OPTIONS` - use only your configure options
* `POSTGRES_EXTRA_CONFIGURE_OPTIONS` - append these configure options along with ones that this plugin already uses
