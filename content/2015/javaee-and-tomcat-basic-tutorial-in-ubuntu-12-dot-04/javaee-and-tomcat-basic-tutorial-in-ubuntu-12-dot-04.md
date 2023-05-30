---
title: JavaEE and Tomcat Basic Tutorial in Ubuntu 12.04
date: 2015-01-15
redirect_from: /javaee-and-tomcat-basic-tutorial-in-ubuntu-12-dot-04/
---

If you are interested in developing JavaEE with Linux and don’t want to use any IDE, or you are just looking around how JavaEE and Tomcat works with Ubuntu 12.04, well here is a fast and simple tutorial for you. Our object is to create a weight index calculator!  

### JavaEE and Tomcat Environment

First we will create the JavaEE development environment by installing JDK and Tomcat.

```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install openjdk-7-jdk
sudo apt-get install tomcat7
```

Next we will edit Tomcat configurations.

```
sudoedit /etc/tomcat7/server.xml
```

Add the following lines inside and edit your own USERNAME to the lines.

```
<Context docBase="/home/USERNAME/jsp" path="/jsp">
</Context>
```

### JavaEE File Structure in Tomcat

Create the `jsp/` folder into your home folder.

```
cd
mkdir jsp
```

Move inside the folder and create the basic file structure.

```
cd jsp/
mkdir WEB-INF
mkdir WEB-INF/classes
mkdir META-INF
touch WEB-INF/web.xml
```

### Minimal web.xml

Move to WEB-INF folder and edit configuration file for our JavaEE web application.

```
cd WEB-INF
nano web.xml
```

Here is the minimal web.xml file you can have, except I have included one servlet in here which we are going to use later. Paste this into the opened file.

```
<?xml version="1.0" encoding="ISO-8859-1"?>
<web-app xmlns="http://java.sun.com/xml/ns/j2ee"
     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
     xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd"
     version="2.5">
	<servlet>
		<servlet-name>index</servlet-name>
		<servlet-class>index.index</servlet-class>
	</servlet>
 
</web-app>
```

### JavaEE classes in Tomcat

We are going to create one class to help our application, these classes are also called beans.

```
cd classes
mkdir index
cd index
nano index.java
```

We will create simple Java class.

```
package index;
 
public class index {
	float height;
	float weight;
	float index;
 
	public void setWeight(float weight) {
		this.weight=weight;
	}
	public float getWeight() {
		return weight;
	}
	public void setHeight(float height) {
		this.height=height;
	}
	public float getHeight() {
		return height;
	}
	public float getIndex() {
		index=weight/(height*height);
		return index;
	}
}
```

Now we need to compile this file with `javac`.

```
javac index.java
```

Important note here! This is not a good style to compile the classes, you should have the `.java` files somewhere else and then just import the `.class` files here, because it is not secure to have original files here on the web interface. But since this is only a tutorial and we are learning here, this will do.

### JSP files

Now we will create the `.jsp` files which will be shown to user as they browse our web application.

```
cd
cd jsp/
nano weight.jsp
```

Add this code into the file.

```
<%@ page info="Weight index with JSP" %>
<jsp:useBean id="indexbean" scope="page" class="index.index"/>
<jsp:setProperty name="indexbean" property="*"/>
 
<html>
<head>
<title>Weight Index with JSP</title>
</head>
<body>
<h2>Please give your weight in kg and height in meters.</h2>
<form action="calculator.jsp" method="GET">
<table>
	<tr>
		<td>Your weight</td>
		<td><input type="text" name="weight"/></td>
		<br/>
	</tr>
	<tr>
		<td>Your height</td>
		<td><input type="text" name="height"/></td>
		<br/>
	</tr>
</table>
<input type="submit" value="Calculate"/>
</form>
</body>
</html>
```

And add another file

```
nano calculator.jsp
```

```
<%@ page info="Showing the result" %>
 
<jsp:useBean id="indexbean" scope="page" class="index.index" />
<jsp:setProperty name="indexbean" property="*" />
 
<html>
<head>
<title>Weight Index with JSP</title>
</head>
<body>
<h2>Your weight index is <jsp:getProperty name="indexbean" property="index" /></h2>
</body>
</html>
```

### Starting Tomcat and testing the application

Now we have created all of our files and want to start our server and see the webpages. Type in the following command and restart the Tomcat server.

```
sudo service tomcat7 restart
```

Open up web browser and go to `http://localhost:8080/jsp/weight.jsp` and you will see our application.  

{% image "./tomcat-form.png", "Tomcat Form" %}

Give it your info and continue to the next page which will make use of our java class.

{% image "./tomcat-result.png", "Tomcat Result" %}

There are alot more in the world of JavaEE but this is was just a simple crash course into the subject using Ubuntu 12.04.