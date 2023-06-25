---
title: "YAML for Everyone: The Simple Guide to YAML"
seoTitle: "YAML Guide: Syntax, Properties, DataTypes & Tools | Simplified"
seoDescription: "Master YAML with our comprehensive guide! Learn YAML syntax, properties, datatypes, and tools. Enhance your configuration skills and boost productivity. YAM"
datePublished: Sun Jun 25 2023 06:34:38 GMT+0000 (Coordinated Universal Time)
cuid: cljb21q3z00000al08efm7fhc
slug: yaml-for-everyone-the-simple-guide-to-yaml
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1687674621695/6a2fc4e5-3ea0-4516-89b2-5d0ca3597659.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1687674813878/19a705f9-65fc-4c87-97f9-d8d9ea35f1ed.png
tags: javascript, devops, yaml, devops-tools, devops-articles

---

In today's world of software development, configuration files are an integral part of any project. They serve as a blueprint for setting up and customizing applications, ensuring consistency and ease of maintenance. One such configuration file format that has gained significant popularity is **YAML (YAML Ain't Markup Language)**. YAML is a human-readable data serialization format, widely used for configuration files, data exchange, and even as a markup language for structured documents. Its simplicity and flexibility make it a favorite choice among developers, system administrators, and DevOps professionals.

This blog post aims to provide a comprehensive guide to YAML, catering to everyone from beginners to experienced developers. Whether you're new to YAML or looking to enhance your knowledge, this guide will walk you through the essentials of YAML, including its syntax, properties/datatypes, and useful tools that can boost your productivity.

# What is YAML ?

***YAML was previously known as "Yet Another Markup Language". But now it is called "YAML ain't Markup Language".***

It is not a programming language. It is a data format used to exchange data. It is similar to XML and JSON datatypes.

It is a simple human-readable language that can be used to represent data. It is used to store some information about configurations.

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">In YAML you can store only data, not commands.</div>
</div>

## What is DATA SERIALIZATION?

Serialization is a process of converting the data objects that is present in some complex data structure into a stream of byte (or storage) that can be used to transfer this data on your physical devices.

![](https://documents.lucid.app/documents/879e0a1c-c893-494e-8995-93c34e7dfeed/pages/0_0?a=298&x=46&y=107&w=1188&h=286&store=1&accept=image%2F*&auth=LCA%201250ad644104e0804147a4aca45e0652463f5c3ed937e6291c891e49c51dde64-ts%3D1687672007 align="left")

> Object -&gt; File = Serialization
> 
> File -&gt; Object = Deserialization

![](https://documents.lucid.app/documents/879e0a1c-c893-494e-8995-93c34e7dfeed/pages/Tvq-aSC.4rYD?a=561&x=-147&y=14&w=1034&h=374&store=1&accept=image%2F*&auth=LCA%207b617399330fb74394f9dbe76876709893c685ade3461b83112598a657ef4a1a-ts%3D1687672007 align="left")

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">The object is the combination of code + data. It is a data storage unit.</div>
</div>

### Another Definition of Serialization :

Serialization is a process of converting this data object which is a combination of code and data into a series of bytes that saves the state of this object in a form that is easily transmittable.

## Deserialization :

The reverse of data serialization is called deserialization.

**Data serialization Languages :**

* YAML
    
* JSON
    
* XML
    

### Why YAML is not known as the Markup Language? Why did the full form change?

Markup languages are used to store only documents. But ***in YAML you can store object data along with documents***. That is why it is known as YAML ain't Markup Language.

### Uses of YAML File :

* Configuration files - Docker, Kubernetes etc.
    
* Logs, Caches etc.
    

### Benefits of YAML :

1. It is simple and easy to read.
    
2. It has a strict syntax - Indentation is Important.
    
3. Easily convertible to JSON & XML Files.
    
4. Most languages use YAML.
    
5. It is more powerful when representing complex data.
    
6. You can use it with various tools like parsers etc.
    
7. Parsing is easy. (Parsing means reading the data)
    

### Some Important Points:

* YAML is case-sensitive. **{ Apple != apple }**
    
* In YAML we use spaces for indentation and not TABS.
    
* In YAML, there are no multi-line comments. (Only single-line comments are available).\\
    
* To separate blocks of code and treat them as documents in a YAML file use **<mark>---</mark>**
    
* To mark as the end of documents use **<mark>...</mark>**
    
* Some of the keys of the sequence will be empty and is known as **sparse-sequence.**
    

## XML

* XML stands for eXtensible Markup Language.
    
* XML is a markup language much like HTML.
    
* XML was designed to store and transport data.
    
* XML was designed to be self-descriptive.
    

```xml
Example :

<?xml version="1.0" encoding="UTF-8"?> 
<note>
  <to>Abhishek</to>
  <from>Bhattacharjee</from>
  <heading>Reminder</heading>
  <body>Don't forget to subscribe to newsletter for awesome blogs</body>
</note>
```

## JSON :

* JSON stands for **J**ava**S**cript **O**bject **N**otation
    
* JSON is a lightweight format for storing and transporting data
    
* JSON is often used when data is sent from a server to a web page
    
* JSON is "self-describing" and easy to understand
    

### JSON Syntax Rules

* Data is in name/value pairs
    
* Data is separated by commas
    
* Curly braces hold objects
    
* Square brackets hold arrays
    

```json
Example :
{
"employees":[
    {"firstName":"John", "lastName":"Doe"},
    {"firstName":"Anna", "lastName":"Smith"},
    {"firstName":"Peter", "lastName":"Jones"}
]
}
```

## Major Concepts of YAML :

### Lists:

* Lists in YAML are represented using (-) followed by a space.
    

```yaml
Fruits:
 - apple
 - banana
 - orange
 - Apple  // case sensitive , so { Apple != apple }
```

### Comments:

* Comments in YAML start with the pound (#) symbol and continue until the end of the line.
    

```yaml
# This is comment in YAML
```

### Inline Notation:

* The inline notation allows you to represent data on a single line.
    

```yaml
person: {name: John, age: 25, City: Newyork}
cities: [Mumbai, Delhi, Raipur]
```

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">Always give one space after <strong><mark>:</mark></strong> when writing the value</div>
</div>

### Flow Notation:

* Flow notation allows you to represent complex data structures using square brackets (**\[\]**) and curly braces (**{}**).
    

```yaml
employees: [{name: John, age: 30}, {name: Jane, age: 28}]

# which is same as writing 

employees:
  - name: John
    age: 30
  - name: Jane
    age: 28
```

### String Data types and ways of writing :

* Strings in YAML can be written using single quotes (**<mark>''</mark>**), double quotes (**<mark>""</mark>**), or without quotes.
    

```yaml
name: 'Abhishek'
address : "123, XYZ"
message: Hello world!
```

### Multi-line Strings:

* Multi-line strings in YAML can be written using the pipe symbol (**<mark>|</mark>**) followed by a new line and proper indentation.
    

```yaml
description: | 
  This is a multi-line 
  String Example
```

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">In any case, the lines should be aligned with the indentation of the <strong><em>description</em></strong></div>
</div>

### Writing a single line in multiple lines using '&gt;' :

* The greater than symbol (&gt;) followed by space allows you to write a single line in multiple lines while preserving line breaks.
    

```yaml
message: >
  This is a single line
  written in multiple lines
```

### Scalar values:

* Scalar values are simple atomic values like numbers, booleans and Strings in YAML.
    

```yaml
number: 43
marks: 98.5
booleanValue: false
```

> The boolean value can also be represented as :
> 
> **<mark>n, N, False, false, FALSE </mark>** \-&gt; for false
> 
> **<mark>y, Y, true, True, TRUE</mark>** -&gt; for true

### Flow Style :

* Flow style allows representing data in a compact form using commas and braces.
    

```yaml
person: {name: John,age: 25, city: India}
```

### Specifying the data types:

* YAML allows specifying the data type of a value using the '**<mark>!!</mark>**'.
    
* Syntax : **variableName: !!Datatype value**
    

```yaml
price: !!float 9.99
zero: !!int 0
cost: !!int 99
positiveno: !!int 55
negativeno: !!int -55
booleanValue: !!bool true 
comma Value: !!int 1,00,000
expo Value: 6.23E56
binaryValue: !!binary ob11010
octalValue: !!int 0o777
hexValue: !!int 0xFF

# What does 6.23E56 mean?
# 6.23 * 10^560
```

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">The key can be written with spaces &amp; special characters.</div>
</div>

### Floating point numbers and Other types :

```yaml
floatNumber: !!float 55.5
infinity: !!float .inf
negativeInfinity: !!float -.inf
not a num: .nan
booleanValue: !!bool true
stringmessage: !!str This is a string

#What does .inf mean 
# It means infinity

#What does .nan mean 
# It means not a number
```

> .inf -&gt; infinity
> 
> .nan -&gt; not a number

### Null values & Null keys:

* Null values can be represented using the **<mark>null, Null, NULL,~(tilde).</mark>**
    

```yaml
surname: !!null null
```

### Dates and times:

* Dates and times can be represented in YAML using ISO 8601 format.
    

```yaml
date: 2017-01-01
time: 12:00:00
datetime: 2017-01-01T12:00:00 # No timezone specified
datetime: 2017-01-01T12:00:00Z # Assuming UTC timezone
datetime: 2017-01-01T12:00:00+05:30 # Assuming IST timezone
```

### Sequence

* The **<mark>!!seq</mark>** tag can be used to specify that a value should be treated as a sequence(list).
    

```yaml
student: !!seq
 - marks
 - name
 - roll_no

 #like this also
 cities: !!seq [Mumbai, Delhi, Bangalore] #OR
 cities: [Mumbai, Delhi, Bangalore] # Inline notation
```

### Sparse Sequence:

* YAML allows representing sparse sequences where some elements are null or missing.
    
    **OR**
    
* When we wish that some of the keys of the sequence should be empty.
    

```yaml
sparse seq: !!seq
 - marks
 - 
 - roll_no
 - null
```

### Nested sequence:

```yaml
-
 - Apple
 - Banana
 - Orange
-
 - Red
 - Yellow
 - Blue
```

### !!Map:

* Which contains key-value pairs.
    

```yaml
# nested mappings (Map within a Map)

 name: Abhishek Bhattacharjee
role: 
  age: 55
  job: Software Engineer
  company: Red Hat
  location: Bangalore
  hobbies: 
    - reading
    - writing
    - travelling
    - playing

#same as
name: Abhishek Bhattacharjee
role: {age: 55, job: Software Engineer, company: Red Hat, 
location: Bangalore, hobbies: [reading, writing, travelling, playing]}    
```

### !!pairs:

* YAML allows representing multiple values for the same key using pairs which are represented using **<mark>!!pairs</mark>**.
    

```yaml
pairs example: !!pairs
 - job: 
    - Software Engineer
    - Teacher
  # OR
  - job: [Software Engineer, Teacher] # This will be an array of hashtables  
  # OR  
  - job : Software Engineer
  - job : Teacher
  # OR
  pair example: !!pairs [job:Software Engineer, job: Teacher]
```

### !!Set

* The **<mark>!!set</mark>** tag can be used to specify that a value should be treated as a set (Collection of unique elements).
    

```yaml
 # !!set will allow only unique values
  names : !!set
    ? Abhishek
    ? Dipika
    ? Anuradha
  # It cannot have same values  

  # what does ? means above !
  # It mean it has null values as of now
```

### Dictionary (!!omap):

* The **<mark>!!omap</mark>** tag can be used to specify that a value should be treated as an ordered map (dictionary with preserved order).
    

```yaml
# dictionary !!omap
people: !!omap
  - Abhishek:
    - age: 55
    - job: Software Engineer
  - Dipika:
    - age: 50
    - job: Teacher
  - Anuradha:
    - age: 25
    - job: Student
```

### Anchors (&) and Aliases (\*):

* YAML allows the use of Anchors (**&**) and Aliases (**\***) to refer to the same value multiple times within the document.
    

```yaml
#reusing some properties using anchors
likings: &likes
  fav fruit: mango
  dislikes : grapes

person1:
   name: Abhishek
    <<: *likes
    dislikes: banana # Overriding the dislikes value here from likings 

#this will be same as
person1:
   name: Abhishek
    fav fruit: mango
    dislikes : banana  #overwrites the dislikes from the anchor    

person2:   
   name: Dipika
    <<: *likes

person3:   
   name: Anuradha
    <<: *likes
```

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">&lt;&lt;: is used to use Anchors using Aliases.</div>
</div>

### DevOps Tools for YAML:

These are the tools that can make your life easier when you are playing around with YAML Files:

* Monokle: [https://monokle.io/](https://monokle.io/)
    
* Datree: [https://www.datree.io/](https://www.datree.io/)
    
* Lens IDE: [https://k8slens.dev/](https://k8slens.dev/)
    

### Resources to Learn and Practice YAML :

* Blog :  
    [https://itnext.io/how-to-validate-kubernetes-yaml-files-9a17b9a30f08](https://itnext.io/how-to-validate-kubernetes-yaml-files-9a17b9a30f08)
    
* To check the syntax of the yaml file:
    
    [https://www.yamllint.com/](https://www.yamllint.com/)
    
* To convert YAML to JSON:
    
    [https://onlineyamltools.com/convert-yaml-to-json](https://onlineyamltools.com/convert-yaml-to-json)
    
* Notes:
    
    [https://github.com/AbhiiVops/YAML](https://github.com/AbhiiVops/YAML)
    

This blog covers the entire YAML required for you to work in Cloud Native landscape. If you want a detailed blog on the use case of the mentioned DevOps Tools then please let me know in the comments.

***Also if you like the blog don't forget to ❤️ and follow me for such awesome blogs. Your support encourage me to write more such blogs. Happy reading!✨***