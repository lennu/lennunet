---
title: Doctrine Find out if Collection is Empty or Not
date: 2017-03-13
redirect_from: /doctrine-find-out-if-collection-is-empty-or-not/
---
You can do a Doctrine query based on the amount of relationship/collection size fairly easy.

Usually in these cases you want to find out if some collection that’s related to your Entity has anything or is empty.

You can use the Query Builder’s where clause to limit these results.

Let’s say we have **Category Entity** and **Product Entity**. We want to fetch all Categories that have products.

```
&lt;?php
 
namespace AppBundle\Repository;
 
class CategoryRepository extends \Doctrine\ORM\EntityRepository
{
&nbsp;&nbsp;&nbsp; public function findCategoriesWithProducts() {
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $qb = $this-&gt;createQueryBuilder('c')
        -&gt;where('SIZE(c.products) &gt; 0');
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; return $qb-&gt;getQuery()-&gt;getResult();
&nbsp;&nbsp;&nbsp; }
}
```

See we are using SIZE to create the amount of products inside the category and fetching only the categories that have more than 0 products.