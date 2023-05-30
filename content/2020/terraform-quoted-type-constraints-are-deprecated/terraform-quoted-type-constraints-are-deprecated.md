---
title: "Terraform: Quoted type constraints are deprecated"
date: 2020-01-30
redirect_from: /terraform-quoted-type-constraints-are-deprecated/
---
This warning:

```
Interpolation-only expressions are deprecated
on somewhere.tf line 165, in variable "some_variable":
  165:   type    = "list"
```


Is produced by the fact that type definitions and constraints should not be quoted (placed withing quotemarks) as it used to be.

To fix this issue you should just remove the quotemarks around the type constraint.

```
type    = list
```
