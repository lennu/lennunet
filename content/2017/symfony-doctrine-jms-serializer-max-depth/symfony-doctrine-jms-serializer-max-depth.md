---
title: Symfony Doctrine JMS Serializer Max Depth
date: 2017-03-03
redirect_from: /symfony-doctrine-jms-serializer-max-depth/
---
There is a great **MaxDepth** exclusion policy in JMS Serializer however there is also a big  mystery how it works.

Lets think of normal case where you are from the start excluding everything in your model and then exposing the fields separately.

We have entity called Product which has properties id, category and price. **From these category and price are exposed.**

Now we know or guess that category probably has a lot of connections to many places and we’re not sure about it’s exclusion policies and **we’d like to limit the depth of our object to only one level**. Meaning **we don’t want to expose nothing from category entity which is a entity reference**.

```
&lt;?php
 
namespace AppBundle\Entity;
 
use Doctrine\ORM\Mapping as ORM;
use JMS\Serializer\Annotation as Serializer;
 
/**
&nbsp;* @ORM\Entity
&nbsp;* @ORM\Table(name="products")
&nbsp;* @Serializer\ExclusionPolicy("all")
&nbsp;*/
class Product
{
&nbsp;&nbsp;&nbsp; /**
&nbsp;&nbsp;&nbsp;&nbsp; * @ORM\Column(name="id", type="integer")
&nbsp;&nbsp;&nbsp;&nbsp; * @ORM\Id
&nbsp;&nbsp;&nbsp;&nbsp; * @ORM\GeneratedValue
&nbsp;&nbsp;&nbsp;&nbsp; */
&nbsp;&nbsp;&nbsp; private $id;
 
&nbsp;&nbsp;&nbsp; /**
&nbsp;&nbsp;&nbsp;&nbsp; * @var \ProductCategory
&nbsp;&nbsp;&nbsp;&nbsp; *
&nbsp;&nbsp;&nbsp;&nbsp; * @ORM\ManyToOne(targetEntity="Category", inversedBy="products")
&nbsp;&nbsp;&nbsp;&nbsp; * @ORM\JoinColumns({
&nbsp;&nbsp;&nbsp;&nbsp; *&nbsp;&nbsp;&nbsp;&nbsp; @ORM\JoinColumn(name="category_id", referencedColumnName="id", nullable=false)
&nbsp;&nbsp;&nbsp;&nbsp; * })
&nbsp;&nbsp;&nbsp;&nbsp; * @Serializer\Expose()
&nbsp;&nbsp;&nbsp;&nbsp; * @Serializer\MaxDepth(1)
&nbsp;&nbsp;&nbsp;&nbsp; */
&nbsp;&nbsp;&nbsp; private $category;
 
&nbsp;&nbsp;&nbsp; /**
&nbsp;&nbsp;&nbsp;&nbsp; * @var decimal
&nbsp;&nbsp;&nbsp;&nbsp; *
&nbsp;&nbsp;&nbsp;&nbsp; * @Assert\NotNull()
&nbsp;&nbsp;&nbsp;&nbsp; * @ORM\Column(name="price", type="decimal", precision=10, scale=2, nullable=false)
&nbsp;&nbsp;&nbsp;&nbsp; * @Serializer\Expose()
&nbsp;&nbsp;&nbsp;&nbsp; */
&nbsp;&nbsp;&nbsp; private $price;
}
```

So as you can see from the example we have placed

```
* @Serializer\Expose()
* @Serializer\MaxDepth(1)
```

MaxDepth(1) to our category property.

Now to make this all work, in our **controller** we have to give the serializer a custom parameter to let it know that we are using these MaxDepth annotations.

If you are using FOS\\RestBundle:

```
* @Rest\View(serializerEnableMaxDepthChecks=true)
```

If you are not then try this:

```
use JMS\Serializer\SerializationContext; $serializer->serialize($data, 'json', SerializationContext::create()->enableMaxDepthChecks());
```