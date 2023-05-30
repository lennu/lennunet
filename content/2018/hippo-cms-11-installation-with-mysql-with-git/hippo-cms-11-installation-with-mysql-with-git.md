---
title: Hippo CMS 11 Installation with MySQL with GIT
date: 2018-03-08
redirect_from: /hippo-cms-11-installation-with-mysql-with-git/
---
In this tutorial we are going to install and run Hippo CMS version 11. This tutorial is made with Ubuntu 16.04 and requires default knowledge of the operating system.

## Initial setup

Lets start with installing the dependencies which are Java 8 and Maven.

```
sudo apt-get install openjdk-8-jdk
sudo apt-get install maven
```

Create hippo project with this command

```
mvn org.apache.maven.plugins:maven-archetype-plugin:2.4:generate \
-DarchetypeRepository=https://maven.onehippo.com/maven2 \
-DarchetypeGroupId=org.onehippo.cms7 \
-DarchetypeArtifactId=hippo-project-archetype \
-DarchetypeVersion=4.2.3
```

This will ask all kinds of questions that you’ll find the answer from https://www.onehippo.org/11/trails/getting-started/creating-a-project.html.

For this tutorial you can just click enter and the default will be applied.

## Adding GIT to project

Now it’s good time to setup git since we have the basic project files on myhippoproject -folder.

```
git init myhippofolder
cd myhippofolder
git status
git add --all
git commit -m "Initial commit"
```

## Add MySQL

To add MySQL into the project we need to create the actual database for it.

```
sudo apt-get install mysql-server
```

Remember to add a root password

```
echo "CREATE DATABASE myhippoproject;" | mysql -u root -p
echo "CREATE USER 'hippouser'@'localhost' IDENTIFIED BY 'hippouserpassword';" | mysql -u root -p
echo "GRANT ALL PRIVILEGES ON myhippoproject.* TO 'hippouser'@'localhost';" | mysql -u root -p
echo "FLUSH PRIVILEGES;" | mysql -u root -p
```

## Hippo CMS MySQL configuration

Hippo CMS configuration isn’t the best in the world and it’s quite complex and hard to follow. Finding a certain line from the configuration files can be very hard to pay attention when doing this.

First add Resource to conf/context.xml. Notice username, password and url which configure your MySQL credentials for Hippo.

```
<?xml version='1.0' encoding='utf-8'?>
<Context>
...
<Resource
    name="jdbc/repositoryDS" auth="Container" type="javax.sql.DataSource"
    maxTotal="20" maxIdle="10" minIdle="2" initialSize="2" maxWaitMillis="10000"
    testWhileIdle="true" testOnBorrow="false" validationQuery="select 1"
    timeBetweenEvictionRunsMillis="10000"
    minEvictableIdleTimeMillis="60000"
    username="hippouser" password="hippouserpassword"
    driverClassName="com.mysql.jdbc.Driver"
    url="jdbc:mysql://localhost:3306/myhippoproject?autoReconnect=true&amp;characterEncoding=utf8" />
</Context>
```

Then add conf/repository.xml, the file contains a lot of stuff and mostly unnecessary things for us to know right know, so I’ll just add the file here. Most importantly it represents the place for content to be put on to and it’s configuration.

```
<?xml version="1.0" encoding="UTF-8"?>
 
<!DOCTYPE Repository
          PUBLIC "-//The Apache Software Foundation//DTD Jackrabbit 2.6//EN"
          "http://jackrabbit.apache.org/dtd/repository-2.6.dtd">
 
<Repository>
 
  <DataSources>
    <DataSource name="repositoryDS">
      <param name="driver" value="javax.naming.InitialContext"/>
      <param name="url" value="java:comp/env/jdbc/repositoryDS"/>
      <param name="databaseType" value="mysql"/>
    </DataSource>
  </DataSources>
 
  <FileSystem class="org.apache.jackrabbit.core.fs.db.DbFileSystem">
    <param name="dataSourceName" value="repositoryDS"/>
    <param name="schemaObjectPrefix" value="repository_"/>
  </FileSystem>
 
  <Security appName="Jackrabbit">
    <SecurityManager class="org.hippoecm.repository.security.SecurityManager"/>
    <AccessManager class="org.hippoecm.repository.security.HippoAccessManager"/>
    <LoginModule class="org.hippoecm.repository.security.HippoLoginModule"/>
  </Security>
 
  <Workspaces rootPath="${rep.home}/workspaces" defaultWorkspace="default"/>
 
  <Workspace name="${wsp.name}">
    <FileSystem class="org.apache.jackrabbit.core.fs.db.DbFileSystem">
      <param name="dataSourceName" value="repositoryDS"/>
      <param name="schemaObjectPrefix" value="${wsp.name}_"/>
    </FileSystem>
 
    <PersistenceManager class="org.apache.jackrabbit.core.persistence.pool.MySqlPersistenceManager">
      <param name="dataSourceName" value="repositoryDS"/>
      <param name="schemaObjectPrefix" value="${wsp.name}_"/>
      <param name="externalBLOBs" value="true"/>
      <param name="consistencyCheck" value="false"/>
      <param name="consistencyFix" value="false"/>
      <param name="bundleCacheSize" value="64"/>
    </PersistenceManager>
 
    <SearchIndex class="org.hippoecm.repository.FacetedNavigationEngineImpl">
      <param name="indexingConfiguration" value="indexing_configuration.xml"/>
      <param name="indexingConfigurationClass" value="org.hippoecm.repository.query.lucene.ServicingIndexingConfigurationImpl"/>
      <param name="path" value="${wsp.home}/index"/>
      <param name="useSimpleFSDirectory" value="true"/>
      <param name="useCompoundFile" value="true"/>
      <param name="minMergeDocs" value="100"/>
      <param name="volatileIdleTime" value="10"/>
      <param name="maxMergeDocs" value="100000"/>
      <param name="mergeFactor" value="5"/>
      <param name="maxFieldLength" value="10000"/>
      <param name="bufferSize" value="1000"/>
      <param name="cacheSize" value="1000"/>
      <param name="onWorkspaceInconsistency" value="log"/>
      <param name="forceConsistencyCheck" value="false"/>
      <param name="enableConsistencyCheck" value="false"/>
      <param name="autoRepair" value="true"/>
      <param name="analyzer" value="org.hippoecm.repository.query.lucene.StandardHippoAnalyzer"/>
      <param name="queryClass" value="org.apache.jackrabbit.core.query.QueryImpl"/>
      <param name="respectDocumentOrder" value="false"/>
      <param name="resultFetchSize" value="1000"/>
      <param name="extractorTimeout" value="100"/>
      <param name="extractorBackLogSize" value="100"/>
      <param name="excerptProviderClass" value="org.apache.jackrabbit.core.query.lucene.DefaultHTMLExcerpt"/>
      <param name="supportSimilarityOnStrings" value="true"/>
      <param name="supportSimilarityOnBinaries" value="false"/>
    </SearchIndex>
 
    <ISMLocking class="org.apache.jackrabbit.core.state.FineGrainedISMLocking"/>
  </Workspace>
 
  <Versioning rootPath="${rep.home}/version">
    <FileSystem class="org.apache.jackrabbit.core.fs.db.DbFileSystem">
      <param name="dataSourceName" value="repositoryDS"/>
      <param name="schemaObjectPrefix" value="version_"/>
    </FileSystem>
 
    <PersistenceManager class="org.apache.jackrabbit.core.persistence.pool.MySqlPersistenceManager">
      <param name="dataSourceName" value="repositoryDS"/>
      <param name="schemaObjectPrefix" value="version_"/>
      <param name="externalBLOBs" value="true"/>
      <param name="consistencyCheck" value="false"/>
      <param name="consistencyFix" value="false"/>
    </PersistenceManager>
 
    <ISMLocking class="org.apache.jackrabbit.core.state.FineGrainedISMLocking"/>
  </Versioning>
 
  <Cluster>
    <Journal class="org.apache.jackrabbit.core.journal.DatabaseJournal">
      <param name="dataSourceName" value="repositoryDS"/>
      <param name="databaseType" value="mysql"/>
      <param name="schemaObjectPrefix" value="repository_"/>
      <param name="revision" value="${rep.home}/revision.log"/>
    </Journal>
  </Cluster>
 
  <DataStore class="org.apache.jackrabbit.core.data.db.DbDataStore">
    <param name="dataSourceName" value="repositoryDS"/>
    <param name="minRecordLength" value="1024"/>
    <param name="maxConnections" value="5"/>
    <param name="copyWhenReading" value="true"/>
  </DataStore>
 
</Repository>
```

Finally we need to modify our pom.xml file to know about our just created repository.xml and MySQL scheme. So do the following changes in pom.xml:

```
From pom.xml find this:
<container>
  <systemProperties>
  ...
  </systemProperties>
</container>
 
Inside <systemProperties> add:
<repo.config>file:${project.basedir}/conf/repository.xml</repo.config>
 
And right after the </systemProperties> and just before </container> add this:
<dependencies>
  <dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <classpath>extra</classpath>
  </dependency>
</dependencies>
```

```
and at the end of the file before </project> add this:
<dependencies>
  <dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.34</version>
    <scope>provided</scope>
  </dependency>
</dependencies>
```

Before rushing to the next step you should commit your changes:

```
git add --all
git commit -m "Add MySQL configuration"
```

## Build & Run

Now lets build our project.

```
mvn clean verify
```

This downloads some assets and creates the runnable java files. Now we need to create .gitignore file because the created files shouldn’t go to version control. So create .gitignore and add the following in there. Also commit the file in git.

```
**/target/**
```

```
git add .gitignore
git commit -m "Add .gitignore"
```

Now we are ready to run the project with this command:

```
mvn -Pcargo.run -Drepo.bootstrap=true
```

The -Drepo.bootsrap=true is there to ensure that we are creating the system from scratch. If you don’t want to do this after the initial setup, you can just omit it.

Try it out
You should now be able to go and see hippo working.

```
http://localhost:8080/cms or http://localhost:8080/site
```

Happy Hippo CMS:ing!