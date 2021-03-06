# bspsync
Automated pipeline for iterative public map testing.

### Usage
```
> node bspsync.js --watch "d:/cstrike/maps" fy_aixxe.bsp
versioning map 'fy_aixxe' to 'fy_aixxe_v1'..
compressing 'fy_aixxe_v1.bsp' for fastdl..
uploading 'fy_aixxe_v1.bsp.bz2' to remote server..
remotely extracting 'fy_aixxe_v1.bsp.bz2' to game server..
changing level on remote game server..
```

### Requirements

You will need to place the following files in the 'bin' directory.
* [bzip2.exe](http://gnuwin32.sourceforge.net/downlinks/bzip2-bin-zip.php)
* [plink.exe](https://the.earth.li/~sgtatham/putty/latest/w32/plink.exe)
* [pscp.exe](https://the.earth.li/~sgtatham/putty/latest/w32/pscp.exe)

### Problem

I want to test my maps on a remote SRCDS server with the following setup:

- [ ] Watch BSP file(s) for changes recursively
- [ ] Packed map resources
- [ ] Unique map name (serverside only)
- [ ] bz2 compression for FastDL
- [ ] Notification of success/failure

### Solution

A utility will be created that addresses above problems, with some
configuration options for making it work for lots of different workflows.

I could do this pretty easily with a Linux shell script, but as this is
supposed to run on the same machine as Hammer Editor, I want to make
something more cross platform.

This tool will watch over a map source directory, waiting for a BSP to be
created or updated. The tool will then pack any materials or sounds into the
BSP, give the map a unique name, compress it into bz2 format for server Fast
Download, and finally upload it to the server.

I would like options for automatically switching the server to the map and
extracting the BSP to the server maps directory, but this would be outside the
scope of this tool, as the problem resides on the remote server. Perhaps a
simple bash script via a CRON job can be supplied as an example.

### Configuration

I suppose that the following will be configurable:

- [ ] Map source directory for watching BSP updates
- [ ] BSP Pack scan game directory (e.g. /path/to/cstrike/)
- [ ] Remote server address / directory for uploading compressed map
- [ ] Toggle notification(s)
