---
title: How to use function from another controller in Symfony
date: 2016-08-25
redirect_from: /how-to-use-function-from-another-controller-in-symfony/
---
Sometimes there is a need to to one of the functions from another controller. The way this is done is by serving the controller as as service of Symfony.

For example we have a good solid function doing one specific thing with some entity. Lets say we have a entity that has an image associated with it and we have already done the processing and the fetching of the image somehow in one of our controller.

Now we enter into a situation where we need this same image somewhere in a slightly different situation. We wouldn’t like to build the whole process again and we’d like to use the old controller to get through this.

The solution might be to make the function static and make it so that it is not part of any instance, but that might not be a good and viable solution. If it helps you here is the way:

```
public static function nameOfTheFunction() {
    $doSomething = null;
}
```

The right way in Symfony if to serve the class as a service.

Go to your services file in app/config/services.yml and append the following there, make sure that you are appending the controller you need to serve:

```
app.your_controller_service:
    class: AppBundle\Controller\YourController
        calls:
            - [setContainer, ["@service_container"]]
```

Now in our another controller which needs the **services** of this controller we can call with this command:

```
$some = $this->get('app.your_controller_service')->getSomeAction($passSomeParameters);
```

Thats it!