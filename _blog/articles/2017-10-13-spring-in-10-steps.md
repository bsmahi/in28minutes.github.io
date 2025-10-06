---
layout:     post
title:      Spring Framework Tutorial for Beginners - Your First 10 Steps
date:       2025-09-24 12:31:19
summary:    Learn the basics of Spring Framework setting up a very simple example.
categories: SpringFramework
permalink:  /spring-tutorial-for-beginners
image: /images/spring-framework-category.png
---

The Spring Framework is just as popular today as it was 12 years ago when I first used it.  
How has it managed to stay relevant in an ever-changing world where software architecture has evolved so dramatically?

### What you will learn

- Spring Framework Fundamentals
    - Dependency Injection
    - Constructor and Setter Injection
    - Autowiring
- Key Annotations: `@Component`, `@Autowired`, `@Primary`
- Overview of Core Spring Modules
- Overview of Major Spring Projects

### Section Introduction

Welcome to this section on the Spring Framework.  
Here, we will guide you through setting up a simple Spring project and introduce key concepts such as tight coupling, loose coupling, dependency injection, inversion of control, and autowiring. You will also get a high-level overview of the Spring ecosystem:

- What are Spring Modules?
- What are Spring Projects?

Finally, we’ll explore why the Spring Framework continues to be so popular.

### The First 10 Steps in Spring

#### Step 1: Create a Spring Project with Spring Initializr

One of the most important features of the Spring Framework is **dependency injection**, which enables the creation of loosely coupled applications. To fully appreciate dependency injection, it’s essential to first understand **tight coupling** and how Spring helps us move toward **loose coupling**.

We’ll begin by setting up a simple example that highlights these concepts.

Creating a Spring project with **Spring Initializr** is straightforward:

> Spring Initializr [http://start.spring.io/](http://start.spring.io/) is a powerful tool to quickly bootstrap your Spring Boot projects.


![Image](/images/spring-initializr-spring-in-10-steps.png "Spring Initializr")   

As shown in the image above, follow these steps:

- Launch **Spring Initializr** and configure it as follows:
    - Group: `com.in28minutes.spring.basics`
    - Artifact: `spring-in-5-steps`
    - Do not select any additional dependencies.
        - By default, the Basic Starter is included, which provides the core Spring Framework and the Spring Test Starter.
- Click the **Generate** button to create a new project.
- Import the project into **Eclipse**.
- To understand all the files that are part of this project, refer to the provided resource.

#### Step 2: Understanding Tight Coupling with the Binary Search Algorithm Example

Next, set up an example of **tight coupling** using the Binary Search and Bubble Sort algorithms, as illustrated in the diagram below.


![Image](/images/SpringIn10Steps-BinarySearchTightlyCoupleWithBubbleSort.png "Spring In 10 Steps - Tight Coupling") 

However, we have a problem with the above implementation. If we want to use binary search with a different sort algorithm, I would need to change the code.

We want to make the binary search algorithm loosely coupled so that it can work with any sorting algorithm. 

> Think about the solution before moving to the next step!

#### Step 3 : Making the Binary Search Algorithm Example Loosely Coupled

Introduce an interface to make the Binary Search loosely coupled to the sort algorithm.

```java
package com.in28minutes.spring.basics.springin5steps;

public interface SortAlgorithm {
	public int[] sort(int[] numbers);
}
```

```java
public class BinarySearchImpl {

    private SortAlgorithm sortAlgorithm;

}    
```	


#### Step 4 : Using Spring to Manage Dependencies-@Component, @Autowired

> In the previous steps, we wrote code to create objects using the bubble sort algorithm and binary search. We also managed the dependencies. It would be great if some framework could take control of the creation of the beans and autowire the dependencies.

That's where the Spring Framework comes in!

Let's start using Spring to do autowiring.

Notes

- The sort algorithm is a dependency of the binary search.


```java
@Component
public class BinarySearchImpl {

	@Autowired
	private SortAlgorithm sortAlgorithm;
```	


```java
@Component
public class BubbleSortAlgorithm implements SortAlgorithm {
	public int[] sort(int[] numbers) {
		// Logic for Bubble Sort
		return numbers;
	}
}
```

#### Step 5 : What is happening in the background?

Enable debug logging to observe what’s happening behind the scenes.

**/src/main/resources/application.properties**
```properties
logging.level.org.springframework = debug
```

- Spring performs a component scan on the parent package com.in28minutes.spring.basics.springin5steps to discover classes annotated with @Component.
- It identifies available components and their dependencies.
- It determines that BinarySearchImpl depends on SortAlgorithm.
- Since SortAlgorithm itself has no dependencies, Spring creates an instance of it and automatically wires it into an instance of BinarySearchImpl.

#### Step 6 : Dynamic auto wiring and troubleshooting-@Primary

What if we add one more SortAlgorithm?

```java
package com.in28minutes.spring.basics.springin5steps;

import org.springframework.stereotype.Component;

@Component
public class QuickSortAlgorithm implements SortAlgorithm {
	public int[] sort(int[] numbers) {
		// Logic for Quick Sort
		return numbers;
	}
}
```

There are now two matching SortAlgorithm instances. Spring throws an exception because it doesn’t know which one to use.

We can use the @Primary annotation to mark one of the SortAlgorithm implementations as the default or preferred choice.

```java
package com.in28minutes.spring.basics.springin5steps;

import org.springframework.context.annotation.Primary;
import org.springframework.stereotype.Component;

@Component
@Primary
public class BubbleSortAlgorithm implements SortAlgorithm {
	public int[] sort(int[] numbers) {
		// Logic for Bubble Sort
		return numbers;
	}
}
```
#### Step 7: Inject Constructor and Setter

Constructor Injection
![Image](/images/SpringIn10Steps-ConstructorInjection.png "Spring In 10 Step - Constructor Injection ") 

Setter Injection
![Image](/images/SpringIn10Steps-SetterInjection.png "Spring In 10 Step - Setter Injection") 
 
#### Step 8 : Spring Modules

Spring is designed in a highly modular way, allowing us to use specific modules independently without needing the others.

![Image](/images/SpringIn10Steps-SpringModules.png "Spring In 10 Steps - Spring Modules") 

Notes
- **Spring Beans, Core, and Context** form the foundation of the Spring Framework — they are responsible for creating the application context, managing bean lifecycles, and handling dependency injection (autowiring).
- Spring provides excellent integration with both data access and integration layers. 
- One of the key data access modules is Spring JDBC, which simplifies working with JDBC. Code that typically requires around twenty-five lines in plain JDBC can often be written in just five to ten lines using Spring JDBC. Spring also integrates seamlessly with JPA and ORM frameworks such as **Hibernate**.
- **Spring JMS** enables communication between applications using JMS. You can send and receive messages through queues, and perform object-to-XML transformations when required.
- **Spring** has strong integration with web frameworks like **Struts**, and it also offers its own web framework called **Spring MVC**.
- **Cross-Cutting Concerns** refer to functionalities that affect multiple layers of an application, such as security and logging. Through **aspect-oriented programming (AOP)**, Spring makes it easy to handle these concerns. The **Spring AOP** module provides basic AOP capabilities, and Spring also offers excellent integration with **AspectJ**.
- **Spring** provides robust support for unit testing through the **Spring Test** framework.

#### Step 9 : Spring Projects

Spring projects offer solutions to various challenges commonly faced by enterprise applications.

![Image](/images/SpringIn10Steps-SpringProjects.png "Spring In 10 Steps - Spring Projects")

### Notes

- **Spring Boot** is one of the most popular frameworks for developing microservices today. It makes application development fast and easy. With features like starter projects, auto-configuration, and actuators, Spring Boot simplifies building production-ready applications.
- The world is moving towards the **cloud**, and everyone wants to deploy their applications there. Therefore, it’s not enough to just develop good applications — we need to build **cloud-native applications**. These applications should support dynamic configuration and connectivity. Cloud-native applications require many additional features, and **Spring Cloud** helps in enabling microservices for the cloud.
- **Spring Data** provides a consistent and simplified way to access data. In the past, most applications connected only to relational SQL databases. Today, we have a mix of data sources — relational, NoSQL, and others. Spring Data ensures that accessing data from different sources remains consistent and easy to manage.
- **Spring Integration** addresses the challenges of application integration. It implements the patterns described in the book *Enterprise Integration Patterns*.
- **Spring Batch** focuses on batch processing applications, which have specific requirements — such as restarting failed jobs, tracking execution details, and monitoring progress. Spring Batch provides these capabilities, making it easy to develop robust batch applications.
- **Spring Security** is an essential module for protecting applications. Whether you are developing a web application or a RESTful service, Spring Security provides comprehensive solutions to secure them.
- **Spring HATEOAS** enables you to create HATEOAS-compliant REST services. In REST, it’s not enough to just return data — it’s also important to include related links that guide the consumer on possible next actions. Spring HATEOAS makes implementing this pattern simple and effective.


So far, we’ve explored seven Spring projects, which just scratch the surface. There are many more, including **Spring Web Services**, **Spring Sessions**, **Spring Social**, **Spring Mobile**, and **Spring Android**, each designed to solve problems in specific areas.

> Spring has not limited itself to just the core framework; it has expanded into a wide range of projects.


#### Step 10 : Why Is Spring Popular?
![Image](/images/SpringIn10Steps-SpringPopularity.png "Spring In 10 Steps - Spring Popularity")
Spring is one of the very few frameworks that remains as popular today as it was 15 years ago.

**How has Spring maintained its popularity over the past 15 years?**

- **Unit Testing** – One of the main reasons for Spring’s popularity is that it enables writing highly testable code. The core feature of Spring is **dependency injection (DI)**. When used properly, DI makes writing unit tests for your code straightforward. Spring also integrates well with testing frameworks like `JUnit` and `Mockito`, allowing developers to write effective unit tests quickly.
- **Zero Plumbing Code** – Spring reduces boilerplate code. For example, exception handling is simplified because Spring makes most exceptions unchecked, minimizing unnecessary plumbing code.
- **Architectural Flexibility** – Spring is highly modular. It offers modules and projects for specific purposes, allowing you to use only the parts you need. For instance, even though Spring has a robust MVC framework (**Spring MVC**), it still provides excellent support for other MVC frameworks like Struts. Similarly, while Spring MVC provides REST support, Spring also integrates well with **JAX-RS** and **Jersey**. Using Spring does not restrict your architectural choices.
- **Staying Current with Trends** – Spring remains relevant by evolving with industry trends. For example, with the rise of microservices and cloud computing, Spring has introduced projects like **Spring Cloud** and **Spring Boot** to help developers build modern, cloud-native applications efficiently.

## Example of Complete Code

### /pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.in28minutes.spring.basics</groupId>
	<artifactId>spring-in-5-steps</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>

	<name>spring-in-5-steps</name>
	<description>Demo project for Spring Boot</description>

	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>4.0.0-M2</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>

	<properties>
		<java.version>21</java.version>
	</properties>

	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
	</dependencies>

	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>

	<repositories>
		<repository>
			<id>spring-milestones</id>
			<name>Spring Milestones</name>
			<url>https://repo.spring.io/milestone</url>
			<snapshots>
				<enabled>false</enabled>
			</snapshots>
		</repository>
   </repositories>

   <pluginRepositories>
		<pluginRepository>
			<id>spring-milestones</id>
			<name>Spring Milestones</name>
			<url>https://repo.spring.io/milestone</url>
			<snapshots>
				<enabled>false</enabled>
			</snapshots>
		</pluginRepository>
	</pluginRepositories>


</project>
```
---

### /src/main/java/com/in28minutes/spring/basics/springin5steps/BinarySearchImpl.java

```java
package com.in28minutes.spring.basics.springin5steps;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

@Component
public class BinarySearchImpl {

	@Autowired
	private SortAlgorithm sortAlgorithm;
	
	public int binarySearch(int[] numbers, int numberToSearchFor) {

		int[] sortedNumbers = sortAlgorithm.sort(numbers);
		System.out.println(sortAlgorithm);
		// Search the array
		return 3;
	}

}
```
---

### /src/main/java/com/in28minutes/spring/basics/springin5steps/BubbleSortAlgorithm.java

```java
package com.in28minutes.spring.basics.springin5steps;

import org.springframework.context.annotation.Primary;
import org.springframework.stereotype.Component;

@Component
@Primary
public class BubbleSortAlgorithm implements SortAlgorithm {
	public int[] sort(int[] numbers) {
		// Logic for Bubble Sort
		return numbers;
	}
}
```
---

### /src/main/java/com/in28minutes/spring/basics/springin5steps/QuickSortAlgorithm.java

```java
package com.in28minutes.spring.basics.springin5steps;

import org.springframework.stereotype.Component;

@Component
public class QuickSortAlgorithm implements SortAlgorithm {
	public int[] sort(int[] numbers) {
		// Logic for Quick Sort
		return numbers;
	}
}
```
---

### /src/main/java/com/in28minutes/spring/basics/springin5steps/SortAlgorithm.java

```java
package com.in28minutes.spring.basics.springin5steps;

public interface SortAlgorithm {
	public int[] sort(int[] numbers);
}
```
---

### /src/main/java/com/in28minutes/spring/basics/springin5steps/SpringIn5StepsApplication.java

```java
package com.in28minutes.spring.basics.springin5steps;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ApplicationContext;

@SpringBootApplication
public class SpringIn5StepsApplication {

	// What are the beans?
	// What are the dependencies of a bean?
	// Where to search for beans? => No need

	public static void main(String[] args) {

		// BinarySearchImpl binarySearch =
		// new BinarySearchImpl(new QuickSortAlgorithm());
		// Application Context
		ApplicationContext applicationContext = SpringApplication.run(SpringIn5StepsApplication.class, args);
		
		BinarySearchImpl binarySearch = applicationContext.getBean(BinarySearchImpl.class);
		
		int result = binarySearch.binarySearch(new int[] { 12, 4, 6 }, 3);

		System.out.println(result);
	}
}
```
---

### /src/main/resources/application.properties

```properties
logging.level.org.springframework = debug
```
---

### /src/main/resources/log.txt

```
Searching directory [/in28Minutes/git/getting-started-in-5-steps/spring-in-5-steps/target/classes/com/in28minutes/spring/basics/springin5steps] for files matching pattern [/in28Minutes/git/getting-started-in-5-steps/spring-in-5-steps/target/classes/com/in28minutes/spring/basics/springin5steps/**/*.class]
Identified candidate component class: file [/in28Minutes/git/getting-started-in-5-steps/spring-in-5-steps/target/classes/com/in28minutes/spring/basics/springin5steps/BinarySearchImpl.class]
Identified candidate component class: file [/in28Minutes/git/getting-started-in-5-steps/spring-in-5-steps/target/classes/com/in28minutes/spring/basics/springin5steps/BubbleSortAlgorithm.class]

Creating instance of bean 'binarySearchImpl'
Creating instance of bean 'bubbleSortAlgorithm'
Finished creating instance of bean 'bubbleSortAlgorithm'

Constuctor-Autowiring by type from bean name 'binarySearchImpl' via constructor to bean named 'bubbleSortAlgorithm'
Setter-Autowiring by type from bean name 'binarySearchImpl' to bean name 'bubbleSortAlgorithm'
No Setter or Constructor-Autowiring by type from bean name 'binarySearchImpl' to bean name 'bubbleSortAlgorithm'

Finished creating instance of bean 'binarySearchImpl'
```
---

### /src/test/java/com/in28minutes/spring/basics/springin5steps/SpringIn5StepsApplicationTests.java

```java
package com.in28minutes.spring.basics.springin5steps;

import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit.jupiter.SpringExtension;

@ExtendWith(SpringExtension.class)
@SpringBootTest
public class SpringIn5StepsApplicationTests {

	@Test
	public void contextLoads() {
	}

}
```
---