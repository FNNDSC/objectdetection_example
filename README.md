# objectdetection_example
```

  ___  _     _           _     ____       _            _   _             
 / _ \| |__ (_) ___  ___| |_  |  _ \  ___| |_ ___  ___| |_(_) ___  _ __  
| | | | '_ \| |/ _ \/ __| __| | | | |/ _ \ __/ _ \/ __| __| |/ _ \| '_ \ 
| |_| | |_) | |  __/ (__| |_  | |_| |  __/ ||  __/ (__| |_| | (_) | | | |
 \___/|_.__// |\___|\___|\__| |____/ \___|\__\___|\___|\__|_|\___/|_| |_|
          |__/                                                           

```
contains example input file for  pl-objectdetection_moc_ppc64 &amp;&amp; pl-objectdetection_x86

On x86_64 machine
--------

```bash
docker run --runtime=nvidia                                         \
            -e NVIDIA_VISIBLE_DEVICES=1                             \
            -v $(pwd)/in:/incoming -v $(pwd)/out:/outgoing          \
            docker.io/fnndsc/pl-objectdetection_x86                 \
            objectdetection.py                                      \
            -f animal360p.webm                                      \
            /incoming /outgoing
```

### about

* `--runtime=nvidia` tells the docker to use the [nvidia docker](https://github.com/NVIDIA/nvidia-docker).

* `-e NVIDIA_VISIBLE_DEVICES=1` specifies the visible graphic card id in the container. We can execute `nvidia-smi` on host to get information about nvidia grpahic devices.

* `-v $(pwd)/in:/incoming -v $(pwd)/out:/outgoing`  This means we bind `$(pwd)/in` and `$(pwd)/out` directory on host to `/incoming`  and `/outgoing` directory in container. Get more information about from here: [volume bind](https://docs.docker.com/storage/bind-mounts/)

* `docker.io/fnndsc/pl-objectdetection_x86` container image name. Don't forget `docker pull docker.io/fnndsc/pl-objectdetection_x86` if you try to test it after automatic build on dockerhub.

* `objectdetection.py` script file

* `-f animal360p.webm` file in the `$(pwd)/in` directory. You can also use `--file` flag.


On ppc64le machine
--------

```bash
docker run --security-opt label=type:nvidia_container_t    \
           -v $(pwd):/incoming:z -v $(pwd)/out:/outgoing:z \
           docker.io/fnndsc/pl-objectdetection_moc_ppc64   \
           objectdetection.py                              \
           -f animal360p.webm                              \
           /incoming /outgoing
```

### about

* `--security-opt label=type:nvidia_container_t` tells the docker to use the [nvidia docker](https://github.com/NVIDIA/nvidia-docker).


* `-v $(pwd):/incoming:z -v $(pwd)/out:/outgoing:z`  This means we bind `$(pwd)/in` and `$(pwd)/out` directory on host to `/incoming`  and `/outgoing` directory in container. Get more information about from here: [volume bind](https://docs.docker.com/storage/bind-mounts/)

* `docker.io/fnndsc/pl-objectdetection_moc_ppc64` container image name. Don't forget `docker pull docker.io/fnndsc/docker.io/fnndsc/pl-objectdetection_moc_ppc64` if you try to test it after pusded it from another machine.

* `objectdetection.py` script file

* `-f animal360p.webm` file in the `$(pwd)/in` directory. You can also use `--file` flag.

Troubleshoot
-----
For debuging, we can use bash inside the container.

* For x86_64
```bash
docker run --runtime=nvidia                                         \
            -v $(pwd)/in:/incoming -v $(pwd)/out:/outgoing          \
            -it --entrypoint /bin/bash                              \
            docker.io/fnndsc/pl-objectdetection_x86                 \
```
* For ppc64le
```
docker run --security-opt label=type:nvidia_container_t    \
           -v $(pwd):/incoming:z -v $(pwd)/out:/outgoing:z \
           -it --entrypoint /bin/bash                      \
           docker.io/fnndsc/pl-objectdetection_moc_ppc64   \
```
