# Assignment 01: Reading/Writing objects to and from XML and JSON

## [Introduction to Service Design and Engineering](https://github.com/IntroSDE) | [University of Trento](http://www.unitn.it/) 


This repository is the solution to the [first assignment](https://sites.google.com/a/unitn.it/introsde_2015-16/lab-sessions/assignments/assignment-1) of the course IntroSDE of the University of Trento. This assignment cover the following topics:

* ANT
* XML, XPATH & XML Schemas
* Mapping XML (and JSON) to (and from) Objects

### Task of the code

The class *HealthProfileReader* reads the information about the people stored in the file *people.xml*. The file has this structure:

```xml
<people>
  <person id="0001">
    <firstname>Marlon</firstname>
    <lastname>Jakubowski</lastname>
    <birthdate>1943-03-21T00:00:00+00:00</birthdate>
    <healthprofile>
      <lastupdate>2015-10-08T15:51:28+02:00</lastupdate>
      <weight>83.52</weight>
      <height>1.85</height>
      <bmi>24.40</bmi>
    </healthprofile>
  </person>
  
  <!-- more people -->
</people>
  
```
The requirements for this assignment are:

**Based on [Lab 3](https://github.com/IntroSDE/lab03):**

1.3 two functions (getWeight and getHeight) that given the id of a person, retrieves the weight and the height of this person;  
2.3 a function that print all the details for each person stored in the file people.xml;  
3.3 a function that given the id, return the details of a person;  
4.3 a function that print all people fulfilling a condition on the weight (>90);

**Based on [Lab 4](https://github.com/IntroSDE/lab04):**
    
1.4 Create the XML schema XSD file for the example XML document of people;  
2.4 convert the list of Java object Person into XML (marshalling to XML) using classes generated with JAXB XJC;  
    convert XML into a list of Java object Person (un-marshalling from XML) using classes generated with JAXB XJC;  
3.4 convert the list of Java object Person into JSON (marshalling to JSON).

### Code

##### Folders

*[src/](src/)*: contains source code;

*[src/model](src/model)*: contains the definition of *Person* and *HealthProfile*;

*[src/peoplestore](src/peoplestore)*: contains the code for marshalling and un-marshalling from/to XML and marshalling to JSON;

##### File
*[src/HealthProfileReader.java](src/HealthProfileReader.java)*: contains the code to execute requirements 1.3, 2.3, 3.3, 4.3 of the previous list. The list of people are stored in people.xml;

*[people.xsd](people.xsd)* XML schema file for the document people.xml (requirement 1.4);

*[src/peoplestore/JAXBMarshaller.java](src/peoplestore/JAXBMarshaller.java)*: class to execute requirement 2.4. Three persons are created using Java and marshalled in XML. The Java objects are stored in the generated file *peopleMarshall.xml*;

*[src/peoplestore/JAXBUnMarshaller.java](src/peoplestore/JAXBUnMarshaller.java)*: class to execute requirement 2.4. The data are retrieved from *people.xml*;

*[src/peoplestore/JavatoJson.java](src/JavatoJson.java)*: class to execute requirement 3.4. Three persons are created using Java and marshalled in JSON. The data are stored in *people.json*; 

*[src/dao/PeopleStore.java](src/dao/PeopleStore.java)* contains the data access object.

### Installation

In order to execute this project you need the following technologies (in the brackets you see the version used to develop):

* Java (jdk1.8.0)
* ANT (version 1.9.4)

Then, clone the repository. Run in your terminal:

```
git clone https://github.com/abonte/introsde-2015-assignment-1.git && cd introsde-2015-assignment-1
```

and run the following command:
```
ant execute.evaluation
```

### Usage
This project use an [ant build script](build.xml) to automate the compilation and the execution of specific part of the Java application.
```
ant execute.evaluation
```
This command performs the following action:

* download and install ivy (dependency manager) and resolve the dependencies. *Ivy* and *lib* folders are generated;
* generate classes JAXB XJC. These classes are used for marshalling and un-marshalling to XML. You can find the classes in *src/peoplestore/generated/*;
* create a build directory and compile the code in the src folder. You can find the compiled code in *build* folder;
* call others target defined in the build file:
    * `execute.getAllPeople` perform tasks in order to fulfill requirement 2.3;
    * `execute.getPersonById` for requirements 3.3;
    * `execute.getPersonByWeight` for requirement 4.3;
    * `execute.JAXBMarshaller` for requirement 2.4;
    * `execute.JAXBUnMarshaller` for requirement 2.4;
    * `execute.JavatoJson` for requirement 3.4.

You can also execute specific task. Before, you have to execute
```
ant compile
```
and then one of the following command:

* `ant execute.getAllPeople`
* `ant execute.getPersonById`
* `ant execute.getPersonByWeight`
* `ant execute.JAXBMarshaller`
* `ant execute.JAXBUnMarshaller`
* `ant execute.JavatoJson`
* `ant clean` this command deletes the folders created during the compile phase (*build/*, *peoplestore/generated*, *lib/*, *ivy/*) and the file created during the execution of the various targets (*people.json* and *peopleMarshall.xml*). 