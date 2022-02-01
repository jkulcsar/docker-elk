
## [How to copy data from docker volume to host?](https://stackoverflow.com/questions/35406213/how-to-copy-data-from-docker-volume-to-host)

To copy data from the volume to the host, use a temporary container that has the volume mounted.
Using `busybox`, for example:

```
CID=$(docker run -d -v hello:/hello busybox true)
docker cp $CID:/hello ./
```

To copy a directory from the host to volume:

```
cd local_dir
docker cp . $CID:/hello/
```

Then clean up the temporary container.

```
docker rm $CID
```


For this Docker ELK instance, get the name of the named volume with `docker volume ls`.
In this case, it should be `docker-elk_elasticsearch`.
The commands are:

```
CID=$(docker run -d -v docker-elk_elasticsearch:/elasticsearch busybox true)
docker cp $CID:/elasticsearch .
docker rm $CID
```