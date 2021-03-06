docker-nfs-ganesha
==================

Docker image providing [NFS-Ganesha](http://nfs-ganesha.github.io/), a user space NFS v3/v4 fileserver.

Based on https://github.com/janeczku/docker-nfs-ganesha, but using fedora as base image and a newer ganesha version,
because of this unfixed bug: https://github.com/janeczku/docker-nfs-ganesha/issues/1

## Usage

```bash
$ sudo docker run -d --cap-add SYS_ADMIN --cap-add DAC_READ_SEARCH --name nfs \
 -v /path/to/export:/data/nfs slintes/nfs-ganesha:2.7.3
```

Mount the NFS export:

```bash
$ mkdir -p /mnt/nfs
$ sudo mount -t nfs4 <server-name>:/ /mnt/nfs`
```

## Environment Variables

##### `EXPORT_PATH`
Default: `/data/nfs`    
The directory to export.

##### `PSEUDO_PATH`
Default: `/`    
NFS4 pseudo path.

##### `EXPORT_ID`
Default: `0`    
An identifier for the export, between 0 and 65535.

##### `PROTOCOLS`
Default: `4`    
The NFS protocols allowed. One or multiple (comma-seperated) of 3, 4, and 9P.

##### `TRANSPORTS`
Default: `UDP, TCP`    
The transport protocols allowed. One or multiple (comma-seperated) of UDP, TCP, and RDMA.

##### `SQUASH_MODE`
Default: `No_Root_Squash`    
What kind of user id squashing is performed. No_Root_Squash, Root_Id_Squash, Root_Squash, All_Squash.

##### `GRACELESS`
Default: `true`    
Whether to disable the NFSv4 grace period.

##### `VERBOSITY`
Default: `NIV_EVENT`    
Logging verbosity. One of NIV_DEBUG, NIV_EVENT, NIV_WARN.
