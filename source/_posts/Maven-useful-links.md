title: "Maven useful links"
date: 2015-02-16 22:57:06
categories:
- Java
tags:
- Java
---
![Maven](/thumbnails/maven.jpg)

Sometimes it is so hard to start a project without any reference. When I start to study something, I always create a document with every useful website to use it later.

You may see below some links that I took note related to Maven:

**About pom.xml**
[http://www.javaworld.com/javaworld/jw-05-2006/jw-0529-maven.html](http://www.javaworld.com/javaworld/jw-05-2006/jw-0529-maven.html)

**How to create a web application with Maven**
[http://www.mkyong.com/maven/how-to-create-a-web-application-project-with-maven/](http://www.mkyong.com/maven/how-to-create-a-web-application-project-with-maven/)

```sh
mvn archetype:generate -DgroupId=br.com.ericmaicon -DartifactId=ProjectName -DarchetypeArtifactId=maven-archetype-webapp -DinteractiveMode=false
mvn eclipse:eclipse -Dwtpversion=2.0
mvn dependency:resolve
mvn install
```

**Spring MVC with Maven**
[http://www.mkyong.com/spring-mvc/spring-3-mvc-and-json-example/](http://www.mkyong.com/spring-mvc/spring-3-mvc-and-json-example/)

**How to create a Java application with Maven**
[http://www.mkyong.com/maven/how-to-create-a-java-project-with-maven/](http://www.mkyong.com/maven/how-to-create-a-java-project-with-maven/)

```sh
mvn archetype:generate -DgroupId=br.com.ericmaicon -DartifactId=ProjectName -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
mvn dependency:resolve
```

**Using Maven with Netbeans**
[http://mrhaki.blogspot.com.br/2008/11/mvn-netbeansnetbeans.html](http://mrhaki.blogspot.com.br/2008/11/mvn-netbeansnetbeans.html)

[http://blog.gilbertoca.com/?p=679](http://blog.gilbertoca.com/?p=679)

**Using Maven with Eclipse**
[http://clinging-to-reality.blogspot.com.br/2012/09/eclipse-and-maven-breaking-adding.html](http://clinging-to-reality.blogspot.com.br/2012/09/eclipse-and-maven-breaking-adding.html)

*Some useful commands:*
```sh
mvn eclipse:eclipse
mvn eclipse:clean
```

**Maven with Tomcat**
[http://t7mp.github.io/](http://t7mp.github.io/)

[http://build-force.googlecode.com/svn/site/tomcat-plugin/index.html](http://build-force.googlecode.com/svn/site/tomcat-plugin/index.html)

**Maven with Jetty**
[http://docs.codehaus.org/display/JETTY/Maven+Jetty+Plugin](http://docs.codehaus.org/display/JETTY/Maven+Jetty+Plugin)

[http://blog.gilbertoca.com/?p=679](http://blog.gilbertoca.com/?p=679)

*How to run:*
```sh
mvn jetty:run
```

**Maven with Oracle driver**
[http://www.mkyong.com/maven/how-to-add-oracle-jdbc-driver-in-your-maven-local-repository/](http://www.mkyong.com/maven/how-to-add-oracle-jdbc-driver-in-your-maven-local-repository/)

```sh
mvn install:install-file -Dfile=/Users/eric/ojdbc6.jar -DgroupId=com.oracle -DartifactId=ojdbc6 -Dversion=11.2.0 -Dpackaging=jar
```

**Unmanaged dependency**

```sh
mvn install:install-file -Dfile=/Users/eric/Sites/my_jar_dependecy.jar -DgroupId=br.com. -DartifactId=my_jar_artifact -Dversion=1.0.0 -Dpackaging=jar
```

**Maven with SQL Server**
[http://claude.betancourt.us/add-microsoft-sql-jdbc-driver-to-maven/](http://claude.betancourt.us/add-microsoft-sql-jdbc-driver-to-maven/)

```sh
mvn install:install-file -Dfile=sqljdbc4.jar -Dpackaging=jar -DgroupId=com.microsoft.sqlserver -DartifactId=sqljdbc4 -Dversion=4.0
```

**C3P0**
[https://github.com/danielme-com/Maven---JPA-2---Hibernate-4---Log4j](https://github.com/danielme-com/Maven---JPA-2---Hibernate-4---Log4j)