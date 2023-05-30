---
title: Symfony route optional parameter
date: 2016-04-06
redirect_from: /symfony-route-optional-parameter/
---
Symfony routes can have optional parameters, so that your path works with or without a parameter. This is something that usually a good service should do so that the user won’t get lost and no error pages occur.

This feature can be achieved by setting a default value for the parameter.

Here are the examples of setting routes in Symfony with default parameter.  
Annotation:

```
/**
 * @Route("/task/{task}", defaults={"task" = 1})
 */
public function taskAction($task)
{
    
}
```

YAML:

```
task:
    path:      /task/{task}
    defaults:  { _controller: AppBundle:Task:index, task: 1 }
```

XML:

```
<!-- app/config/routing.xml -->
<?xml version="1.0" encoding="UTF-8" ?>
<routes xmlns="http://symfony.com/schema/routing"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://symfony.com/schema/routing
        http://symfony.com/schema/routing/routing-1.0.xsd">
 
    <route id="task" path="/task/{task}">
        <default key="_controller">AppBundle:Task:index</default>
        <default key="task">1</default>
    </route>
</routes>
```

PHP:

```
use Symfony\Component\Routing\RouteCollection;
use Symfony\Component\Routing\Route;
 
$collection = new RouteCollection();
$collection->add('task', new Route('/task/{task}', array(
    '_controller' => 'AppBundle:Task:index',
    'task'        => 1,
)));
 
return $collection;
```

By using this, you can access pages /task and /task/2 by using the same controller and route. Remember that trailing slash /task/ does not work by default on Symfony (you need to redirect trailing slashes).