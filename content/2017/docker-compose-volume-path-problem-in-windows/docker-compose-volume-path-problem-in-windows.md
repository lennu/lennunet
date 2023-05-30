---
title: Docker Compose Volume Path Problem in Windows
date: 2017-03-03
redirect_from: /docker-compose-volume-path-problem-in-windows/
---
If you are having some errors with composing Docker containers which have volumes in Windows there is usual and easy solution.

The problem is usually indicated by the following errors:

```
ERROR: for php&nbsp; Cannot create container for service
```

```
invalid volume specification
```

```
Encountered errors while bringing up the project.
```

There is a simple fix to make errors go away. Docker-Compose simply doesn’t follow the paths the same on Windows as it would on Unix systems.

Create **.env** file and add there:

```
COMPOSE_CONVERT_WINDOWS_PATHS=1
```