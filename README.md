# Lita development environment

This repository provides Lita users with a complete development environment for trying out Lita and developing Lita plugins.

## Quick start

1. Install [Vagrant](https://www.vagrantup.com/)
1. Install [VirtualBox](https://www.virtualbox.org/)
1. `git clone https://github.com/litaio/development-environment.git lita-dev`
1. `cd lita-dev`
1. `vagrant up` - This will take a few minutes the first time.
1. `vagrant ssh`
1. `lita-dev`

After the last step, you will be dropped into a shell in a Debian system inside the `/home/lita/workspace` directory. This directory is shared with the "workspace" directory on your host computer inside the repository you cloned. The system has Redis, Ruby, and Lita already installed.

## Next steps

If you want to run Lita, first generate a new project with:

``` bash
lita new .
```

This will generate a new Lita project in the workspace directory. Then start Lita with:

``` bash
lita
```

If you want to develop a plugin, run one of the following commands:

``` bash
lita adapter NEW_ADAPTER_NAME
lita handler NEW_HANDLER_NAME
lita extension NEW_EXTENSION_NAME
```

The capitalized phrase should be replaced with the name you want to give your plugin.

## Documentation

For complete documentation on installing and using the development environment, please visit [Installation](http://docs.lita.io/getting-started/installation/) on the Lita documentation site.

## License

[MIT](http://opensource.org/licenses/MIT)
