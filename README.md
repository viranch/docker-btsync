# docker-btsync
Docker image for a secure, no-fuss BitTorrent Sync for sharing folders within a network.

### How to use?

- Install docker

- Generate a secret and remember & store it somewhere:
`secret=$(docker run --rm viranch/btsync btsync --generate-secret)`

- Run the image:

```
docker run -d --name syncer \
    -h device1 \
    -p 3369:3369/udp \
    -v /opt/btsync:/var/lib/btsync \
    -v /path/to/shared_folder:/share \
    -e SECRET=$secret \
    -e PEERS=192.168.1.2:3369,192.168.1.3:3369 \
    viranch/btsync
```

### Important notes

- The folder to be shared on host should be mounted at `/share` in the container.

- Store the generated secret somewhere (docker-compose file preferrably) so as to not lose it.

- Hostname of the container (set by `-h` switch is used as the device name by btsync)

- `PEERS` should be of the format: `<IP>:<PORT>`. Multiple values can be passed by using comma as the delimiter.

### What does it contain?

- [BitTorrent Sync](https://getsync.com/)
- [dockerize](https://github.com/jwilder/dockerize)

### Customizing

##### btsync.tmpl config template

This is the template as explained in `jwilder/dockerize` for configuring HAProxy. Customize it to your needs and if you think it will help others, send a pull request :)
