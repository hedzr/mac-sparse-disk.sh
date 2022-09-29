# mac-sparse-disk.sh

A bash utility to create, mount and umount a .sparsebundle file. It works
under macOS only. 

> - See also <https://hedzr.com/tech/nology/hdiutil-and-sparsebundle/>.
> - See also <https://github.com/hedzr/bash.sh>

## Install

Pull the `mac-sparse-disk.bash` directly and put it into your `/usr/local/bin`. The
command via wget can be:

```bash
wget https://github.com/hedzr/mac-sparse-disk.sh/raw/master/mac-sparse-disk.bash | sudo tee /usr/local/bin/mac-sparse-disk.bash
sudo chmod +x /usr/local/bin/mac-sparse-disk.bash
```

## Man

```bash
❯ mac-sparse-disk.bash
mac-sparse-disk.bash <commands>

Commands:
    mac-sparse-disk.bash create [namespace [size [workspace]]]
    mac-sparse-disk.bash mount [namespace]
    mac-sparse-disk.bash umount [namespace]
    mac-sparse-disk.bash attach [workspace]
    mac-sparse-disk.bash detach [namespace]
    mac-sparse-disk.bash compact [namespace [workspace]]
    mac-sparse-disk.bash info [namespace]
        mac-sparse-disk.bash to_image_path|to-image-path [namespace]

Parameters:
    workspace: in general, it's the filename of sparsebundle.
    namespace: the mount point name, the Volume name.
      By default, 'workspace' will be the value of 'namespace' when it missed.

Examples:
    $ mac-sparse-disk.bash create good-test 1g
      create a file named as good-test.sparsebundle, and its size is 1g.
    $ mac-sparse-disk.bash attach good-test
    $ mac-sparse-disk.bash detach good-test
    $ rm -rf good-test.sparsebundle good-test/
    $ mac-sparse-disk.bash info aa              # print info of 'aa', assumed /Volumes/aa has been mounted
    $ mac-sparse-disk.bash to-image-path aa     # print the image-path of volume 'aa' if it's mounted

```

### Create a .sparsebundle file

This command creates a new sparsebundle file with case-sensitive filesystem and size is 1GB:

```bash
$ mac-sparse-disk.bash create good-test 1g
```

A file (folder) named as `good-test.sparsebundle` will be created at the current directory.

### Mount it

To mount it into `/Volumes/good-test`:

```bash
$ mac-sparse-disk.bash attach good-test
```

And `./good-test/` will be created and linked to `/Volumes/good-test`.

### Umount it

```bash
$ mac-sparse-disk.bash detach good-test
```

### Retrieve the source image path

This command can find the source image path from a mount point (suchh as `/Volumes/good-test`).

```bash
$ mac-sparse-disk.bash to-image-path good-test
/Users/me/Downloads/good-test.sparsebundle
```

## LICENSE

Apache 2.0
