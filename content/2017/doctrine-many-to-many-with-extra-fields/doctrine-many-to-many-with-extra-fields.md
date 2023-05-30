---
title: Doctrine Many To Many with Extra Fields
date: 2017-03-09
redirect_from: /doctrine-many-to-many-with-extra-fields/
---
Extra fields for Many to Many relationship is usually well supported. However in Doctrine this is actually something that you can’t do with just normal ManyToMany entity.

In Doctrine you have to define three Entities where you kind of manually create the Many To Many relationship. This is done like this.

Lets say we have Products and Categories. Products can have many Categories and Categories can have many Products. So we need a many to many relationship.

Now for the sake of example we also need quantity of how many products are in a category. It would be convenient to store the information into the middle table of our many to many relationship.

Lets first define the Product class

```
namespace Entity;
 
use Doctrine\ORM\Mapping as ORM;
 
/**
 * @ORM\Entity()
 * @ORM\Table(name="product")
 */
class Product
{
&nbsp;&nbsp;&nbsp; /**
     * @ORM\Id()
     * @ORM\Column(type="integer")
     */
&nbsp;&nbsp;&nbsp; private $id;
 
&nbsp;&nbsp;&nbsp; /**
     * ORM\Column(name="name", type="string", length=50, nullable=false)
     */
&nbsp;&nbsp;&nbsp; private $name;
 
&nbsp;&nbsp;&nbsp; /**
     * @ORM\OneToMany(targetEntity="Entity\CategoryProduct", mappedBy="product")
     */
&nbsp;&nbsp;&nbsp; private $categoryProducts;
}
```

So you see that we are using **OneToMany** relationship in here and it is targeting Entity CategoryProducts which eventually will be our middle table.

Now lets define Category class:

```
namespace Entity;
 
use Doctrine\ORM\Mapping as ORM;
 
/**
&nbsp;* @ORM\Entity()
&nbsp;* @ORM\Table(name="store")
&nbsp;*/
class Store
{
&nbsp;&nbsp;&nbsp; /**
&nbsp;&nbsp;&nbsp;&nbsp; * @ORM\Id()
&nbsp;&nbsp;&nbsp;&nbsp; * @ORM\Column(type="integer")
&nbsp;&nbsp;&nbsp;&nbsp; */
&nbsp;&nbsp;&nbsp; private $id;
 
&nbsp;&nbsp;&nbsp; /**
&nbsp;&nbsp;&nbsp;&nbsp; * ORM\Column(name="name", type="string", length=50, nullable=false)
&nbsp;&nbsp;&nbsp;&nbsp; */
&nbsp;&nbsp;&nbsp; private $name;
 
&nbsp;&nbsp;&nbsp; /**
&nbsp;&nbsp;&nbsp;&nbsp; * @ORM\OneToMany(targetEntity="Entity\CategoryProduct", mappedBy="category")
&nbsp;&nbsp;&nbsp;&nbsp; */
&nbsp;&nbsp;&nbsp; private $categoryProducts;
}
```

Now we have defined both of our main entities. Now it’s time for the middle table.

```
namespace Entity;
 
use Doctrine\ORM\Mapping as ORM;
 
/**
&nbsp;* @ORM\Entity()
&nbsp;* @ORM\Table(name="category_product")
&nbsp;*/
class CategoryProduct
{
&nbsp;&nbsp;&nbsp; /**
&nbsp;&nbsp;&nbsp;&nbsp; * ORM\Column(type="integer")
&nbsp;&nbsp;&nbsp;&nbsp; */
&nbsp;&nbsp;&nbsp; private $quantity;
 
&nbsp;&nbsp;&nbsp; /**
&nbsp;&nbsp;&nbsp;&nbsp; * @ORM\Id()
&nbsp;&nbsp;&nbsp;&nbsp; * @ORM\ManyToOne(targetEntity="Entity\Product", inversedBy="categoryProducts") 
&nbsp;&nbsp;&nbsp;&nbsp; * @ORM\JoinColumn(name="product_id", referencedColumnName="id", nullable=false) 
&nbsp;&nbsp;&nbsp;&nbsp; */
&nbsp;&nbsp;&nbsp; private $product;
 
&nbsp;&nbsp;&nbsp; /**
&nbsp;&nbsp;&nbsp;&nbsp; * @ORM\Id()
&nbsp;&nbsp;&nbsp;&nbsp; * @ORM\ManyToOne(targetEntity="Entity\Category", inversedBy="categoryProducts") 
&nbsp;&nbsp;&nbsp;&nbsp; * @ORM\JoinColumn(name="category_id", referencedColumnName="id", nullable=false) 
&nbsp;&nbsp;&nbsp;&nbsp; */
&nbsp;&nbsp;&nbsp; private $category;
}
```

Here in the middle table we just define ManyToOne side relationships to their corresponding OneToMany relations on the main entities. We can also add here as many extra fields as we like. Currently this entity contains the **Quantity** which will store the information of how many products are in this category.