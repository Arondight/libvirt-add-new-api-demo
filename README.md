# libvirt-add-new-api-demo

## ABOUT

This patch is an example to add new APIs in [LibVirt][LIBVIRT-WEBSITE], also add entries in virsh. I implement qemu driver only but others is the same.

## USAGE

```bash
git clone https://github.com/Arondight/libvirt-add-new-api-demo.git
git clone https://github.com/libvirt/libvirt.git
git clone https://github.com/coreutils/gnulib.git
export LIBVIRT_PATCH=$(readlink -f ./libvirt-add-new-api-demo/LibVirt-add-new-API-demo.patch)
export GNULIB_SRCDIR=$(readlink -f ./gnulib)
cd libvirt
git checkout v2.5.0
git am $LIBVIRT_PATCH
./autogen.sh
make -j8
```

## SYNOPSIS

There are 3 new commands in `virsh`:

1. `get-magic`: Get magic file's content
+ `set-magic`: Set magic file's content
+ `magic-status`: Show if magic file can be read

You can run `virsh` via `run` to try these.

First start `libvirtd` in a new console with root privilege.

```bash
sudo ./run ./daemon/libvirtd
```

Then set or get magic file's content.

```bash
sudo ./run ./tools/virsh set-magic 'Hello World!'
sudo ./run ./tools/virsh get-magic
```

If you set magic file's content to `0xabadcafe`, QEMU driver will refused to boot any VM.

```bash
sudo ./run ./tools/virsh -c qemu:///system set-magic '0xabadcafe'
sudo ./run ./tools/virsh -c qemu:///system start <domain>
```

## COPYRIGHT

Copyright (c) 2016 秦凡东 (Qin Fandong)

## LICENSE

Read [LICENSE][LICENSE-URL].

[LICENSE-URL]: LICENSE "Read LICENSE"
