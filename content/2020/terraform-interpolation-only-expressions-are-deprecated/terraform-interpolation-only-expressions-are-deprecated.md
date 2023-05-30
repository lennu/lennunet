---
title: "Terraform: Interpolation-only expressions are deprecated"
date: 2020-01-30
redirect_from: /terraform-interpolation-only-expressions-are-deprecated/
---
Terraform is updating constantly and code styles are getting reworked all the time. This update was a very good one and you should definitely start using it as it makes your code more readable.

You may get warning like this:

```
Interpolation-only expressions are deprecated
on some_terraform_file.tf line 13, in resource "in_some_resouce" "some_name":
   13:   something = "${variable}"
```


This means that variables can now be given without interpolation (without quotation marks and the dollar sign). To fix this just remove the interpolation. This is actually very good deprecation since the old style is very bad and misleading code style.

```
something = variable
```


The interpolation syntax should still be used if you want to create actual strings with variables in them.