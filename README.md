# meta-domoticz
a yocto meta layer to enable creation of an image for my home


# Dependencies

This layer depends on:

  URI: git://git.openembedded.org/bitbake
  branch: poky

  URI: git://git.openembedded.org/openembedded-core
  layers: meta
  branch: poky

  URI: git@github.com:r2d2/meta-domoticz-custom.git

# Patches

Please submit any patches against the domoticz layer to the
the maintainer:

Maintainer: <nclsmarc@gmail.com>


# I. Adding the domoticz layer to your build

In order to use this layer, you need to make the build system aware of
it.

Assuming the domoticz layer exists at the top-level of your
yocto build tree, you can add it to the build system by adding the
location of the domoticz layer to bblayers.conf, along with any
other layers needed. e.g.:

Add this in 'bblayers.conf' :
```
  BBLAYERS ?= " \
    /path/to/yocto/meta \
    /path/to/yocto/meta-poky \
    /path/to/yocto/meta-yocto-bsp \
    /path/to/yocto/meta-domoticz \
    /path/to/yocto/meta-domoticz-custom \
    "
```

Add this in the 'local.conf' file :

```
# Enable systemd init system
DISTRO_FEATURES_append = " systemd"

```

# II. recipes description

## recipes-custom/custom-domoticz-scripts

  Adds my custom scripts :
  - get the edf tempo color for next day
  - read the values of the electrical counter (using WiFinfo - https://hallard.me/wifinfo/)

## recipes-custom/custom-iptables-rules

  Add custom iptables rules :
  - keep ssh
  - keep domoticz
  Also adds iptables-persistent startup script (systemd based)

## recipes-custom/jq

  Add the jq tool, used by the custom-domoticz-scripts recipe, to parse json (see https://stedolan.github.io/jq/)
