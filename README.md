## docker-swarm-course

This repository accompanies my experiments while attending [Docker Swarm course](https://www.safaribooksonline.com/library/view/docker-swarm/9781788398251/). 

The original author's [code and notes](https://github.com/excelsiorsoft/docker-swarm-course/blob/master/V08278_Code.zip) downloaded from Packt has been extracted into folders corresponding to course's chapters.

My own chapter notes are added to the corresponding folders as `my-notes.txt` files.

The author also has a [repo with similar contents](https://github.com/albertogviana/docker-swarm-presentation).

Docker Swarm Visualizer is described in more details [here](https://github.com/dockersamples/docker-swarm-visualizer).

Couple of services running in a cluster (from Chapter 2): 

![](https://github.com/excelsiorsoft/docker-swarm-course/blob/master/chapter-2/services-deployed-in-a-swarm.PNG)

are accessible on all cluster nodes:
```
$ docker service ls
ID                  NAME                      MODE                REPLICAS            IMAGE                                     PORTS
3x1onmfsfgk1        visualizer                replicated          1/1                 dockersamples/visualizer:latest           *:8000->8080/tcp
xum6cp7s3g69        docker-routing-mesh-svc   replicated          1/1                 albertogviana/docker-routing-mesh:1.0.0   *:8080->8080/tcp

$ curl $(docker-machine ip swarm-1):8080
The hostname is a00237d05ad4!
$ curl $(docker-machine ip swarm-2):8080
The hostname is a00237d05ad4!
$ curl $(docker-machine ip swarm-3):8080
The hostname is a00237d05ad4!
$
```
These services are also replicateable via `docker service scale docker-routing-mesh=10`:

![](https://github.com/excelsiorsoft/docker-swarm-course/blob/master/chapter-2/replicated%20services.PNG)

```
$ while true; do curl http://$(docker-machine ip swarm-1):8080; sleep 1; printf "\n"; done
The hostname is c9ab47e6e387!
The hostname is b41faa8e1926!
The hostname is 6a5f2855cd85!
The hostname is e3274e70964e!
The hostname is 2a441221ba37!
The hostname is bf39ae6958cb!
The hostname is b03250313ff8!
The hostname is c5cdeb85ba19!
The hostname is f9cbd7b427be!
The hostname is df82aef562ba!
The hostname is c9ab47e6e387!
The hostname is b41faa8e1926!
```
