---
title: Docker Compose & Machine Cheatsheet
date: 2017-03-03
redirect_from: /docker-compose-machine-cheatsheet/
---
Docker Machine
--------------

Create a default docker machine with Virtualbox as its driver:

```
docker-machine create -d virtualbox default
```

Configure Docker Client to act against **default** Docker Machine:

```
docker-machine env default
```

Unset Docker Client to normal state:

```
docker-machine env -u
```

Run with these commands:

```
docker-machine start
docker-machine stop
docker-machine restart
```

Docker Compose
--------------

Run Docker Compose

```
docker-compose up
```

To run Compose in **headless state** use this:

```
docker-compose up -d
```

Stop Docker Compose’s containers

```
docker-compose down
```

To remove all volumes while taking containers down, use:

```
docker-compose down -v
```