Docker Ecosystem Survey
=======================

An incomplete survey of the Docker ecosystem. Many products are [yet to be surveyed](#to-be-surveyed). Comments and pull requests welcome!

Most products mentioned here are in Beta or even Alpha. Competition is fierce and churn is high. Dead products will be removed from the list and new ones will be added.

## Orchestration frameworks (i.e. PaaS software for Docker)

Note: Such a framework should include at least container management, cluster management, and container placement functions. Example optional functions are fault-tolerance, replication, monitoring, development workflow automation, container dependency management, data store services, container versioning, etc.

- Kubernetes: [See architecture](https://raw.githubusercontent.com/GoogleCloudPlatform/kubernetes/master/docs/architecture.png). 
- [Kubernetes on Mesos](https://github.com/mesosphere/kubernetes-mesos): "Mesos provides the fine-grained resource allocations for pods across nodes in a cluster, and can make Kubernetes play nicely with other frameworks running on the same cluster resources."
- OpenShift: uses Kubernetes
- [Mesosphere](https://mesosphere.com/) (Mesos + Marathon + Chronos)
- [Docker Machine](https://github.com/docker/machine), [Swarm](https://github.com/docker/swarm), & [Compose](https://github.com/docker/compose)
- [OpenStack Docker](https://wiki.openstack.org/wiki/Docker)
- [SmartDataCenter](https://github.com/joyent/sdc) from Joyent
- Deis from OpDemand: Uses CoreOS (fleet, etcd, etc.). Provides streamlined development/deployment workflow. [Doesn’t support container dependency](https://groups.google.com/forum/#!msg/deis-users/H50Yvh2bMyY/VKPf0DU_q1QJ)
- Flynn: Uses etcd. Similar to Deis. A general PaaS system. Not Docker specific.
- [dokku](https://github.com/progrium/dokku): a mini-Heroku for Docker (sponsored by Deis).
- Serf from maker of Vagrant: not Docker specific. http://www.centurylinklabs.com/decentralizing-docker-how-to-use-serf-with-docker/
- Tsuru: http://blog.tsuru.io/architecture/2014/04/04/running-tsuru-in-production-scaling-and-segregating-docker-containers.html
- [Decking](http://decking.io/)
- [Flocker](https://github.com/clusterhq/flocker). Mainly designed for data volume management. User specifies container-to-host mapping.
- [Rancher](www.rancher.io)
- [Clocker](https://github.com/brooklyncentral/clocker)
- [paz](https://github.com/yldio/paz)
- [galazy](https://github.com/litl/galaxy)
- [Lattice](http://lattice.cf/) from Pivotal
- [weave.works](http://weave.works/)
- [Empire](https://github.com/remind101/empire). A control layer on top of Amazon EC2 ECS.
- [gantryd](https://github.com/DevTable/gantryd)  Framework for easy management of docker-based components across machines
- [containership.io](https://github.com/containership/containership)  A simple container management platform.

## Host OSes designed for Docker

- [CoreOS](https://coreos.com). Use systemd to manage container upstarts and dependencies, etcd for service discovery, and CoreUpdate for operating system updates.
- [SmartOS](https://www.joyent.com/technology/smartos)
- [Ubuntu Core](http://www.ubuntu.com/cloud/tools/snappy)
- [Project Atomic](http://www.projectatomic.io/) from Redhat. Used by OpenShift.
- [Rancher OS](http://rancher.com/rancher-os/). All system services are implemented as containers and therefore "eliminate the need for complex init systems like systemd". Rancher OS runs two Docker daemons: system docker and user docker. It does not use systemd.
- [Project Photon](https://blogs.vmware.com/cloudnative/introducing-photon/) from VMWare. It is ["optimized for VMware vSphere and VMware vCloud Air environments."](http://www.forbes.com/sites/benkepes/2015/04/20/vmware-introduces-new-open-source-projects-to-enable-the-microservices-future/?utm_content=buffer8ee19&utm_medium=social&utm_source=twitter.com&utm_campaign=buffer)

## Host cluster management

- All Docker orchestration frameworks (see Section 1) provide cluster management one way or the other
- Docker Machine
- CoreOS Fleet: initd for containers

## Service discovery & configuration

- Consul: comparison to other software: http://www.consul.io/intro/vs
- Kubernetes: No dynamic service discovery yet. [Advocate for static port allocation](http://youtu.be/YrxnVKZeqK8?t=14m31s).
- CoreOS etcd
- ZooKeeper
- doozerd: dead. https://news.ycombinator.com/item?id=6366665
- Serf: decentralized etcd
- [SmartStack](http://nerds.airbnb.com/smartstack-service-discovery-cloud/) from airbnb

## Container placement

- Mesosphere Marathon
- CoreOS Fleet: Only for initial placement. Use systemd as underlying tool. Features: X-Fleet:Conflicts, global units, unit multi-instantiation, machine metadata match.
- Docker Swarm
- All orchestration frameworks provide container placement

## Container security

- [Project Lightwave](http://blogs.vmware.com/cloudnative/introducing-lightwave/) from VMWare

## Container high-availability & scaling

- Kubernetes ReplicationControllers. [The reconciler model](http://youtu.be/YrxnVKZeqK8?t=20m19s) is great.
- fig. The `fig scale` command
- Flynn. The `flynn scale` command
- Deis. The `deis scale` command

## Container dependency management

- CoreOS systemd: ad hoc through unit directives
- Docker Compose (formerly fig)
- Kubernetes Services concept: decouples inter-dependent containers and doesn’t allow explicit dependency declaration
- [Maestro](https://github.com/toscanini/maestro): seems dead. 
- [Maestro NG](https://github.com/signalfuse/maestro-ng)
- Panamax from CenturyLink: Application templating. Have a nice Web UI. “makes deploying complex containerized apps as easy as Drag-and-Drop."
- [Procfile](https://devcenter.heroku.com/articles/procfile): used at Heroku and by Flynn and Deis.
- [Marathon](https://mesosphere.github.io/marathon/docs/native-docker.html)

## Container inter-networking across hosts

- Kubernetes networking (https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/ovs-networking.md)
- systemd in CoreOS: %H specifiers, written to etcd, and use sidekicks to monitor downtimes
- CoreOS Flannel: can be used by Kubernetes: https://github.com/coreos/flannel#flannel
- Weave

## Custom network topologies on a single host

- [Pipework](https://github.com/jpetazzo/pipework)
- An example of using Docker to simulate complex topologies: https://github.com/brandon-rhodes/fopnp/tree/m/playground

Solomon proposed to support VXLAN from the Docker core.

## Container scheduling (i.e. cron for Docker)

- Mesosphere Chronos

## Container updates & versioning

- CoreOS CoreUpdate (paid service): mainly server-side implementations. Client side requires non-trivial integration work (We can use standard docker tag/pull mechanisms instead).
- Docker-compose's Run stage
- Deis: [See this doc](http://docs.deis.io/en/latest/using_deis/config-application/#track-changes)
- Flock?

## Container monitoring, troubleshooting & resource enforcement

- [sysdig](http://www.sysdig.org/)
- Kubernetes cAdvisor
- LMCTFY

## Container data management

- Flocker from clusterHQ. Data volumes follow container location, via ZFS.

## DevOps streamlining & tooling

- docker-compose (was fig)
    - In my own experience with OSX/boot2docker, `fig up` can be quite slow (in the matter of tens of seconds) with about 20 containers.
    - `fig up <container>` doesn't start `volumes-from` containers.
- [Crane](https://github.com/michaelsauter/crane)
- Deis
- Flynn
- [Modit](https://mod.it): for staging.
- Shippable: for testing & deployment
- docker-cmd: manage docker commands with JSON. https://github.com/iorga-group/docker-cmd. seems dead?

## Image hosting companies (i.e. private registries)

- Quay.io from CoreOS
- Docker Hub Enterprise
- Private Docker registries using the “registry" docker image.

## Container hosting companies

- AWS Container Service
- Google Container Engine
- [Rackspace](www.rackspace.com)
- Orchard
- [tutum](https://www.tutum.co/)
- [Joyent](https://www.joyent.com/)
- [StackDock](https://stackdock.com/)
- [SailAbove](https://labs.runabove.com/docker/)
- [Cloud66](http://www.cloud66.com/)
- [Giant Swarm](https://giantswarm.io/)

## Professional service providers

- [Container Solutions](http://container-solutions.com/)

## Useful resources

- [CenturyLink Labs](http://www.centurylinklabs.com/): Covers Docker related news and tutorials.
- [The 12-factor app](http://12factor.net/): Principles of building Docker apps.
- [container42.com](http://container42.com): A Docker blog.
- [The Docker Book](http://www.dockerbook.com/): A book to learn Docker.

## To be surveyed

- Products from [this mind map](http://www.mindmeister.com/389671722/docker-ecosystem).
- crane
- [Shipyard](http://shipyard-project.com/)
- Cloud Foundry (Diego)
- Helios
- Centurion
- Shipper
- Flocker
- Panamax from CenturyLink
- [Docker Engine for SmartDataCenter](https://github.com/joyent/sdc-docker)
- OpenStack Docker
- Serf
- Tsuru
- YARN?
- [Decking](http://decking.io/)
- [Geard](http://www.openshift.org/geard/) from Redhat. Core of OpenShift.
- [goclouder](https://www.goclouder.net/)
- [IndiePaaS](https://github.com/pierreozoux/indiepaas)
- [apcera](https://www.apcera.com/)

## TODOs

- Add more notes to each bullet.
- Add links.


