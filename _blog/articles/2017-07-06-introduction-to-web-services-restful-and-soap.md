---
layout: post
title: Introduction to Web Services - Restful and SOAP
date: 2025-09-16 12:31:19
summary: Introduction to Web Services - Restful and SOAP, This tutorial will help you understand the basics of web services and the different kinds of web services - REST and SOAP.
categories: SwArchitecture
permalink: /introduction-to-web-services-with-soap-and-rest
image: /images/spring-boot-application.png
---

In this tutorial, you’ll learn the fundamentals of web services and explore the two primary types—REST and SOAP.

## You will learn

- What web services are
- The advantages of using web services
- The main types of web services
- An introduction to RESTful web services
- An introduction to SOAP web services

## You will require the following tools:

- **Maven 3.0+** as the build tool
- **JDK 17+** for running Java applications
- **An IDE of your choice** (e.g., Eclipse or IntelliJ IDEA)

# What is a Web Service?

> **Service delivered over the web**

Is this really a complete definition?  
Does everything delivered over the web qualify as a *web service*?

For example, consider a web application we developed in our Spring MVC course to manage to-dos.

![Image](/images/Web_Services_Web_Application_To_Manage_Todos.png)

## Is this application a web service?

> Nope. The answer is no. This is a **web application**, not a web service.

So, we are back to square one:

- What is a web service?
- How is it different from a web application?

---

## Understanding the difference

Let’s consider an example:

Mark Zuckerberg likes the **To-Do application** we developed in our Spring MVC course. He believes it’s a perfect fit to
integrate into Facebook so users can manage their tasks directly inside Facebook.

Can we use the existing application for this integration? **No.**

### Why not?

Because the current application is designed for **humans**.

- Its output is **HTML**, which is rendered by the browser.
- It is not designed for other **applications** to consume.

---

## Thinking differently

What if I wanted to design the To-Do application so that **other applications** could interact with it?

> I would need to produce the output in a format that other systems could understand. Then, Facebook could call my web
> service and integrate with it.

---

## W3C Definition of a Web Service

> **A software system designed to support interoperable machine-to-machine interaction over a network.**

---

## Key Takeaways

- Web services are designed for **machine-to-machine (or application-to-application)** interaction.
- They are **interoperable**, meaning not tied to a single platform or technology.
- They enable **communication over a network**.

---

## Web Service Data Exchange Formats

Now, let’s revisit our example:

Facebook wants to talk to the To-Do application.

- Facebook uses multiple technologies: PHP (frontend), Erlang (chat), Java and C++ (backend).
- The To-Do application is built with **Java (Spring MVC)**.

Even though these systems use **different technologies**, we still want them to communicate. That’s where **standard
data exchange formats** come in—allowing seamless interaction between diverse platforms.

![Image](/images/Web_Service_Basic_Interaction.png)

## Requests and Responses

Both applications must be able to understand the **request** and the **response**.

So, what formats should we use?

> They should be **standard formats** so that they can work across different platforms.  
> JSON and XML are the most popular data exchange formats.

---

## Types of Web Services

This is more of a **broad classification** rather than strict types:

- **SOAP**
- **REST**

These are not always mutually exclusive. Some SOAP services can also be RESTful.

So the key question is:

> When does a web service become a SOAP web service or a RESTful web service?

---

### SOAP

SOAP originally stood for **Simple Object Access Protocol**.

- SOAP requests and responses are always in **XML format**.
- But not every XML is valid SOAP. SOAP defines its own standard XML structure.
- WSDL (Web Service Definition Language) is used to describe the format of the request and response.

If Facebook wanted to call the **To-Do service**, what would we give their developers?

We would provide the **WSDL file**, which explains:

- The different operations (services) exposed by the server
- The endpoint (URL) to use for each operation
- The structure of the request XML
- The structure of the response XML

#### SOAP Message Structure

A SOAP message is wrapped inside a **SOAP-Envelope**:

- **SOAP-Header** (optional): Metadata such as authentication, authorization, or encryption info
- **SOAP-Body**: The actual request/response content
- **SOAP-Fault**: Error messages returned in case of failure

---

### REST

Unlike SOAP, **REST does not define a standard message format**.

- REST services can use **XML** or **JSON** (JSON is more popular).

So, what exactly is REST?

> REST is an **architectural style** for distributed systems, based on the idea of **resources**.

#### Key Concepts

- **Resource**: Anything that can be identified—e.g., a todo item, a Facebook user
- **Resource URI**: Identifies a resource
    - `/user/Ranga/todos/1`
    - `/person/Ranga`
- **Resource Representation**: Describes the resource’s current state (XML, JSON, HTML)

When a resource is requested, its **representation** is returned.

---

#### REST and HTTP

REST is built on top of **HTTP (the language of the web)**.

**HTTP Methods (Verbs):**

- **POST** – Create a new resource
- **GET** – Read a resource
- **PUT** – Update an existing resource
- **DELETE** – Delete a resource

**HTTP Response Codes:**

- `200` – SUCCESS
- `201` – CREATED
- `400` – BAD REQUEST
- `401` – UNAUTHORIZED
- `404` – RESOURCE NOT FOUND
- `415` – UNSUPPORTED TYPE
- `500` – SERVER ERROR

---

#### REST Constraints

- **Client-Server**: Clear separation of consumer and provider
- **Uniform Interface**: Resources exposed through consistent URIs (nouns, not actions)
- **Stateless**: Each request is independent, no session data stored on the server
- **Cacheable**: Responses can be cached (e.g., HTTP cache)
- **Layered System**: Clients should not assume a direct connection to the server; intermediaries may exist

---

### Richardson Maturity Model

The **Richardson Maturity Model** defines the maturity of REST services:

- **Level 0**: Use REST endpoints but keep action-based URIs (e.g., `/getPosts`, `/deletePosts`)
- **Level 1**: Use resources with proper URIs (`/accounts`, `/accounts/10`) but ignore HTTP methods
- **Level 2**: Use proper URIs **and** HTTP methods (`PUT /accounts/1`, `POST /accounts`)
- **Level 3**: HATEOAS (Hypermedia as the Engine of Application State) – responses include links to possible next
  actions

---

### Designing RESTful APIs

When designing REST APIs, keep these points in mind:

- Focus on the **API consumer**: Does the request/response format make sense for them?
- Use **nouns (resources)** in URIs, not verbs. Prefer plurals.
- Use **hierarchical and self-descriptive URIs**.
- Always use the correct **HTTP methods**:
    - **GET** – Read (idempotent, multiple calls = same result)
    - **POST** – Create (returns `201 Created`, often with link to new resource)
    - **PUT** – Update (returns `200 OK`)
    - **DELETE** – Remove (returns `200 OK` or `204 No Content`)

---

## REST vs SOAP

- **REST** is an **architectural style**.
- **SOAP** is a **protocol/message format**.

**Typical implementations:**

- RESTful services: JSON over HTTP
- SOAP services: XML over SOAP over HTTP

**Key Comparisons:**

- REST is **simpler** to implement and consume.
- REST offers better **performance and scalability** (caching supported).
- REST supports multiple formats (JSON, XML, etc.); SOAP only uses XML.
- SOAP has **strict standards** (WSDL, WS-Security, WS-ReliableMessaging). REST documentation is evolving (
  Swagger/OpenAPI).

---

## Advantages of Web Services

- **Reuse**: Facebook doesn’t need to build its own To-Do app—just reuse ours.
- **Modularity**: Applications can be broken into smaller, independent services.
- **Language Neutrality**: Services can be consumed across different languages and platforms.

Web services are the foundation of **SOA (Service-Oriented Architecture)** and **Microservices architectures**.

## SOAP Service Examples

### Request

```xml

<Envelope xmlns="http://schemas.xmlsoap.org/soap/envelope/">
    <Body>
        <getCourseDetailsRequest xmlns="http://in28minutes.com/courses">
            <id>Course1</id>
        </getCourseDetailsRequest>
    </Body>
</Envelope>
```

### Response

```xml

<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/">
    <SOAP-ENV:Header/>
    <SOAP-ENV:Body>
        <ns2:getCourseDetailsResponse xmlns:ns2="http://in28minutes.com/courses">
            <ns2:course>
                <ns2:id>Course1</ns2:id>
                <ns2:name>Spring</ns2:name>
                <ns2:description>10 Steps</ns2:description>
            </ns2:course>
        </ns2:getCourseDetailsResponse>
    </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

### Fault

```xml

<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/">
    <SOAP-ENV:Header/>
    <SOAP-ENV:Body>
        <SOAP-ENV:Fault>
            <faultcode>SOAP-ENV:Server</faultcode>
            <faultstring xml:lang="en">java.lang.NullPointerException</faultstring>
        </SOAP-ENV:Fault>
    </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

### WSDL

- view-source:http://localhost:8080/ws/courses.wsdl

```xml
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<wsdl:definitions xmlns:wsdl="http://schemas.xmlsoap.org/wsdl/" xmlns:sch="http://in28minutes.com/courses"
                  xmlns:soap="http://schemas.xmlsoap.org/wsdl/soap/" xmlns:tns="http://in28minutes.com/courses"
                  targetNamespace="http://in28minutes.com/courses">
    <wsdl:types>
        <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" elementFormDefault="qualified"
                   targetNamespace="http://in28minutes.com/courses">

            <xs:element name="getCourseDetailsRequest">
                <xs:complexType>
                    <xs:sequence>
                        <xs:element name="id" type="xs:string"/>
                    </xs:sequence>
                </xs:complexType>
            </xs:element>

            <xs:element name="getCourseDetailsResponse">
                <xs:complexType>
                    <xs:sequence>
                        <xs:element name="course" type="tns:course"/>
                    </xs:sequence>
                </xs:complexType>
            </xs:element>

            <xs:complexType name="course">
                <xs:sequence>
                    <xs:element name="id" type="xs:string"/>
                    <xs:element name="name" type="xs:string"/>
                    <xs:element name="description" type="xs:string"/>
                </xs:sequence>
            </xs:complexType>
        </xs:schema>
    </wsdl:types>
    <wsdl:message name="getCourseDetailsRequest">
        <wsdl:part element="tns:getCourseDetailsRequest" name="getCourseDetailsRequest">
        </wsdl:part>
    </wsdl:message>
    <wsdl:message name="getCourseDetailsResponse">
        <wsdl:part element="tns:getCourseDetailsResponse" name="getCourseDetailsResponse">
        </wsdl:part>
    </wsdl:message>
    <wsdl:portType name="CoursesPort">
        <wsdl:operation name="getCourseDetails">
            <wsdl:input message="tns:getCourseDetailsRequest" name="getCourseDetailsRequest">
            </wsdl:input>
            <wsdl:output message="tns:getCourseDetailsResponse" name="getCourseDetailsResponse">
            </wsdl:output>
        </wsdl:operation>
    </wsdl:portType>
    <wsdl:binding name="CoursesPortSoap11" type="tns:CoursesPort">
        <soap:binding style="document" transport="http://schemas.xmlsoap.org/soap/http"/>
        <wsdl:operation name="getCourseDetails">
            <soap:operation soapAction=""/>
            <wsdl:input name="getCourseDetailsRequest">
                <soap:body use="literal"/>
            </wsdl:input>
            <wsdl:output name="getCourseDetailsResponse">
                <soap:body use="literal"/>
            </wsdl:output>
        </wsdl:operation>
    </wsdl:binding>
    <wsdl:service name="CoursesPortService">
        <wsdl:port binding="tns:CoursesPortSoap11" name="CoursesPortSoap11">
            <soap:address location="http://localhost:8080/ws"/>
        </wsdl:port>
    </wsdl:service>
</wsdl:definitions>
```
