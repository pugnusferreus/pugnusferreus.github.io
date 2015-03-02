---
layout: post
title: "Creating a REST application with Spring 4"
date: 2015-03-02 19:00
comments: true
categories: 
---

1 . Install <a href="http://www.oracle.com/technetwork/java/javase/downloads/index-jsp-138363.html#javasejdk">JDK 7 or higher</a>, <a href="http://maven.apache.org">Maven</a> and <a href="http://git-scm.com">GIT</a>

2 . On your terminal, run `git clone https://github.com/pugnusferreus/spring-rest.git`

3 . In the spring-rest folder, run `mvn -e  jetty:run -Djetty.port=8080`

4 . On your browser, go to `http://localhost:8080/rest/someEndPoint` and you'll get the following response `{"key":"Hello from a manager!"}`.

I'll not explain step by step on how to wire up all these since there are a dozen of articles on how to wire up a REST application with Spring 4. I'll be highlighting on the things that we should be looking at.

Configuration
-------------

1 . `src/main/webapp/WEB-INF/web.xml` basically tells your Java Web App on which spring context it should use and the URL pattern mapping. In this example, we want to configure all our REST calls with /rest/*.

2 . `src/main/webapp/WEB-INF/applicationContext.xml` and `src/main/webapp/WEB-INF/manager-context.xml` is where we declare our spring beans. I deliberately separate them up so that manager classes will be declared in the manager-context.xml.

3 . `src/main/java/log4j2.xml` is where we configure our logging. We're using <a href="http://logging.apache.org/log4j/2.x/">Log4J2</a> in this example. This XML tells LOG4J to log spring-rest.log and to the terminal console.

4 . `pom.xml` is our Maven build file. <dependencies /> tells Maven what this application's dependencies are so that Maven can fetch them from the Maven repository. <plugins />  is where we configure our Java compilation, WAR file build and Jetty configurations.

Source
------

1 . `com.progriff.managers.TestManager` is our manager class. We should always put our business logic in a manager class.

2 . `com.progriff.controllers.TestController` is our controller. Note that there is an `@Autowired` on top of the TestManager class. Spring will automatically wire up TestManager with TestController. Do note that your variable name must be the same as the bean id in the manager-context.xml file.

3 . In TestController, for each methods that are to be mapped to a URL, we'll need `@RequestMapping` and `@ResponseBody`. You can set the REST URL path, Request Method and the Media Type that this REST will produce in the @RequestMapping annotation. Do note that when we return the java.util.Map in that method, Jackson will automatically convert the object into JSON.