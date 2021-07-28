[TOC]

# Part 1 Introduction to Databases
## Chapter 1 Databases and Databases Users
### 1.1 Introduction
A database is **a collection of related data**. By data, we mean known facts that can be recorded and that have implicit meaning. For example, consider the names, telephone numbers, and addresses of the people you know.
- A database represents some aspect of the real world, sometimes called the mini world or the **universe of discourse** (UoD). Changes to the mini world are reflected in the database.
- A database is a **logically coherent collection** of data with some **inherent meaning**. A **random assortment of data** cannot correctly be referred to as a database.
- A database is designed, built, and populated with data for a specific purpose. It has an intended group of users and some preconceived applications in which these users are interested.
- Common implementation:
    + database: collection of tables
    + table: collection of records
    + record: collection of fields

A **database management system** (**DBMS**) is a collection of programs that enables users to create and maintain a database. The DBMS is a *general-purpose software system* that facilitates the processes of `defining`, `constructing`, `manipulating`, and `sharing` database among various users and applications.
- **Defining** a database involves specifying the *data types*, *structures*, and *constraints* of the data to be stored in the database. The database definition or descriptive information is also stored by the DBMS in the form of a database catalog or dictionary; it is called **meta-data**.
- **Constructing** the database is the process of storing the data on some storage medium that is controlled by the DBMS.
- **Manipulating** a database includes functions such as querying the database to retrieve specific data, updating the database to reflect changes in the mini world, and generating reports from the data.
- **Sharing** a database allows multiple users and programs to access the database simultaneously.

An application program accesses the database by sending queries or requests for data to the DBMS. A **query** typically causes some data to be retrieved; a **transaction** may cause some data to be read and some data to be written into the database.

### 1.2 An Example

### 1.3 Characteristics of the Database Approach
A number of characteristics distinguish the database approach from the much older approach of programming with files.
- Self-describing nature of a database system
  + contains a complete definition or description of the database structure and constraints. (meta-data)
- Insulation between programs and data, and data abstraction
- Support of multiple views of the data
  + A database typically has many users, each of whom may require a different perspective or view of the database.
  + A view may be a subset of the database or it may contain **virtual data** that is derived from the database files but is not explicitly stored.
- Sharing of data and multiuser transaction processing
  + A transaction is an executing program or process that includes one or more database accesses, such as reading or updating of database records. Each transaction is supposed to execute *a logically correct database access if executed in its entirety without interference from other transactions*.
    * **isolation** : ensures that each transaction appears to execute in isolation from other transactions, even though hundreds of transaction may be executing concurrently.
    * **atomicity** : ensures that either all the database operations in a transaction are executed or none are.

### 1.4 Actors on the Scene
Identify the people whose jobs involve the day-to-day use of a large database;
- Database Administrators
  + In a database environment, the primary resource is the database itself, and the secondary resource is the DBMS and related software. Administering these resources is the responsibility of the database administrator (DBA).
  + The DBA is responsible for authorizing access to the database, coordinating and monitoring its user, and acquiring software and hardware resources as needed.
  + The DBA is accountable for problems such as security breaches and poor system response time.
- Database Designers
  + Database designers are responsible for **identifying the data to be stored** in the database and for **choosing appropriate structures** to represent and store this data. These tasks are mostly undertaken before the database is actually implemented and populated with data. It is the responsibility of database designers to **communicate with all prospective database users** in order to understand their requirements and to create a design that meets these requirements.
  + The final database design must be capable of supporting the requirements of all user groups.
- End Users
  + End users are the people whose jobs require access to the database for querying, updating, and generating reports;
- System Analysts and Application Programmers (Software Engineers)

### 1.5 Workers behind the Scene
These persons are typically not interested in the database content itself.
- DBMS system designers and implementers design and implement the DBMS modules and interfaces as a software package.
  + module for implementing the catalog
  + module query language processing
  + module interface processing
  + module accessing and buffering data
  + module controlling concurrency
  + module handling data recovery and security
- Tool developers - the software packages that facilitate database modeling and design, database system design, and improved performance.
- Operators and maintenance personnel - are responsible for the actual running and maintenance of the hardware and software environment for the database system.

### 1.6 Advantages of Using the DBMS Approach
#### 1.6.1 Controlling Redundancy
**Redundancy** is storing the same data multiple times leads to several problems.
- Duplication of effort
- Storage space is wasted
- Inconsistent

**Data normalization** is use to ensures data store only one place in the database.

In practice, sometimes necessary to use **controlled redundancy** to improve the performance of queries.

#### 1.6.2 Restricting Unauthorized Access

#### 1.6.3 Providing Persistent Storage for Objects in OOP
The complex objects can be stored permanently in an object-oriented DBMS.

#### 1.6.4 Providing Storage Structures and Search techniques for Efficient Query Processing
- indexes
- caching
- **query processing and optimization** module

#### 1.6.5 Providing Backup and Recovery

#### 1.6.6 Providing Multiple User interfaces
- query languages for casual users
- programming language for application programmers
- forms and command codes for parametric users
- menu-driven interfaces and natural language interfaces (GUI)

#### 1.6.7 Representing Complex Relationships among Data

#### 1.6.8 Enforcing integrity Constraints
- Referential integrity constraints
- Uniqueness constraints
- Business rules
- Inherent rules

#### 1.6.9 Permitting Inferencing and Actions Using Rules
- deductive database system
- trigger
- stored procedures

### 1.7 When not to use a DBMS
- Simple
- Stringent (khat khe), real-time requirements
- Embedded system with limited storage
- Single user access to data

## Chapter 2 Databases System Concepts and Architecture
### 2.1 Data Models, Schemas, and Instances

### 2.2 Three-Schema Architecture and Data Independence

### 2.3 Database Languages and Interfaces

### 2.4 The Database System Environment

### 2.5 Centralized and Client/Server Architectures for DBMSs

### 2.6 Classification of Database Management Systems


# The Relational Data Model and SQL
## The Relational Data Model and Relational Constraints

## Basic SQL

## More SQL

## The Relational Algebra and Relational Calculus

# Conceptual Modeling and Databases Design
## Databases Modeling using the Entity-Relationship (ER) Model
### Role of high-level conceptual data model in databases design
<figure>
  <figcaption style="text-align:center;">Databases Design</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img src="dbfigures/dbdesign.png" alt="Databases Design" title="Databases Design">
</figure>

The known **functional requirements** of the application. These consist of the user defined *operations* (or *transactions*) that will be applied to the database, including both retrievals and updates. In software design, it is common to use *data flow diagrams*, *sequence diagrams*, *scenarios*, and other techniques to specify functional requirements.

The **data requirements** of the users and includes detailed descriptions of the *entity types*, *relationships*, and *constraints*.

The **conceptual schema** is transformed from the *high-level data model* into the *implementation data model*. This step is called *logical design* or *data model mapping*; its result is a database schema in the implementation data model of the DBMS. Data model mapping is often automated or semiautomated within the database design tools.

The last step is the **physical design** phase, during which the *internal storage structures*, *file organizations*, *indexes*, *access paths*, and physical design parameters for the database files are specified. In parallel with these activities, application programs are designed and implemented as database transactions corresponding to the high level transaction specifications.

### Sample Databases
Sample Databases Application name: **COMPANY**

The **COMPANY** database keeps track of a company's *employees*, *departments*, and *projects*.

**Miniworld**:

- The company is organized into departments. Each department has *a unique name*, *a unique number*, and *a particular employee who manages the department*. We keep track of *the start date when that employee began managing the department*. A department *may have several locations*.
- A department controls a number of projects, each of which has *a unique name*, *a unique number*, and *a single location*.
- We store each *employee's name*, *Social Security number*, *address*, *salary*, *sex* (gender), and *birth date*. An employee is *assigned to one department*, but *may work on several projects, which are not necessarily controlled by the same department*. We keep track of the current *number of hours per week that an employee works on each project*. We also keep track of *the direct supervisor of each employee (who is another employee)*.
- We want to keep track of *the dependents of each employee* for insurance purposes. We keep each *dependent's first name, sex, birth date, and relationship to the employee*.

<figure>
  <figcaption style="text-align:center;">Sample ERD</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img src="dbfigures/sampleerd.png" alt="Sample ERD" title="Sample ERD">
</figure>

### Entity types, entity sets, attributes and keys
#### Entities and attributes
##### Entities and their attributes
The basic object that the ER model represents is an entity, which is a thing in the real world with an independent existence. An entity
may be an object with a physical existence (for example, a particular person, car, house, or employee) or it may be an object with a conceptual existence (for instance, a company, a job, or a university course).

Each entity has attributes - the particular properties that describe it. For example, an EMPLOYEEentity may be described by the employee's name, age, address, salary, and job. Several types of attributes occur in the ER model: *simple* versus *composite*, *single valued* versus *multivalued*, and *stored* versus *derived*.

##### Composite versus simple (atomic) attributes
**Composite attributes** can be divided into smaller subparts, which represent more basic attributes with independent meanings. For example, the *Address* attribute of the EMPLOYEE entity can be subdivided into *Street_address*, *City*, *State*, and *Zip*, with the values '2311 Kirby', 'Houston', 'Texas', and '77001'. Attributes that are not divisible are called simple or atomic attributes.

##### Single Valued versus Multivalued attributes
Most attributes have a single value for a particular entity; such attributes are called **single-valued**. For example,
Age is a single-valued attribute of a person. In some cases an attribute can have a set of values for the same entity - for instance, a Colors attribute for a car, or a College_degrees attribute for a person. Cars with one color have a single value, whereas two-tone cars have two color values. Similarly, one person may not have a college degree, another person may have one, and a third person may have two or
more degrees; therefore, different people can have different numbers of values for the College_degrees attribute. Such attributes are called **multivalued**. A multivalued attribute may have lower and upper bounds to constrain the number of values allowed for each individual entity. For example, the Colors attribute of a car may be restricted to have between one and three values, if we assume that a car can have three colors at most.

##### Stored versus Derived Attributes
In some cases, two (or more) attribute values are related - for example, the Age and Birth_date attributes of a person. For a
particular person entity, the value ofAgecan be determined from the current (today's) date and the value of that person's Birth_date. The Age attribute is hence called a derived attribute and is said to be derivable from the Birth\_date attribute, which is called a stored attribute. Some attribute values can be derived from related entities; for example, an attribute Number\_of\_employees of a DEPARTMENT
entity can be derived by counting the number of employees related to (working for) that department.

##### NULL values

##### Complex values
Mix composite and multivalued.

#### Entity types, entity sets, keys, and value sets
##### Entity types and entity sets
An **Entity type** defines a collection (or set) of entities that have the same attributes. The collection of all entities of a particular entity type in the database at any point in time is called an **entity set**.

An entity type is represented in ER diagrams as a rectangular box enclosing the entity type name. Attribute names are enclosed in ovals and are attached to their entity type by straight lines. Composite attributes are attached to their component attributes by straight lines. Multivalued attributes are displayed in double ovals.

##### Key attributes of an Entity Type
An entity usually has one or more attributes whose values are distinct for each individual entity in the entity set. They is called a **key attribute**.

##### Value sets (domain) of attributes
Each simple attribute of an entity type is associated with a **value set** (or **domain** of value), which specifies the set of value may be assigned to that attribute for each individual entity.

##### Initial Conceptual Design of the COMPANY database
We can identify four entity type:

<figure>
  <figcaption style="text-align:center;">Department entity type</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img src="dbfigures/department.png" alt="Department entity type" title="Department entity type">
</figure>

<figure>
  <figcaption style="text-align:center;">Project entity type</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img src="dbfigures/project.png" alt="Project entity type" title="Project entity type">
</figure>

<figure>
  <figcaption style="text-align:center;">Employee entity type</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img src="dbfigures/employee.png" alt="Employee entity type" title="Employee entity type">
</figure>

<figure>
  <figcaption style="text-align:center;">Employee entity type</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img src="dbfigures/dependent.png" alt="Employee entity type" title="Employee entity type">
</figure>

### Relationship types, relationship sets, Roles, and structure constraints
#### Relation ship types, sets, instances

#### Relationship degree, role names, and recursive relationships
**The degree of a relationship type** is the number of participating entity types. Hence, the WORKS_FOR relationship is of degree two. A relationship type of degree two is called *binary*, and one of degree three is called *ternary*.

**Relationships as attributes**: foreign key in relational databases

#### Constraints on binary relationship types
**The Cardinality ratios for binary relationships** specifies the *maximum number* of relationship instances that an entity can participate in.

For example, in the WORKS_FOR binary relationship type, DEPARTMENT:EMPLOYEE is of cardinality ratio 1:N, meaning that each department can be related to (that is, employs) any number of employees, but an employee can be related to (work for) only one department. This means that for this particular relationship WORKS\_FOR, a particular department entity can be related to any number of employees (N indicates there is no maximum number). On the other hand, an employee can be related to a maximum of one department. The possible cardinality ratios for binary relationship types are 1:1, 1:N, N:1, and M:N.

**Participation Constraints and Existence Dependencies**. The participation constraint specifies whether the existence of an entity depends on its being related to another entity via the relationship type. This constraint specifies the *minimum number* of relationship instances that each entity can participate in, and is sometimes called the *minimum cardinality constraint*. There are two types of participation constraints - total and partial - that we illustrate by example. If a company policy states that every employee must work for a department, then an employee entity can exist only if it participates in at least one WORKS_FOR relationship instance. Thus, the participation of EMPLOYEE in WORKS\_FOR is called *total participation*, meaning that **every entity in the total set of employee entities must be related to a department entity via WORKS\_FOR**. Total participation is also called *existence dependency*. We do not expect every employee to manage a department, so the participation of EMPLOYEE in the MANAGES relationship type is partial, meaning that some or part of the set of employee entities are related to some department entity via MANAGES, but not necessarily all.

In ER diagrams, total participation (or existence dependency) is displayed as a *double line* connecting the participating entity type to the relationship, whereas partial participation is represented by a *single line*.

#### Attributes of relationship types
Default is have key attributes of entities participate in relationship, if need other attributes then add them in. With relationship 1:1, attributes of relationship can be transformed to the entity type on the any-side of relationship. With relationship 1:N, attributes can be migrated to the entity type on the N-side of the relationship.

### Weak entity types
Entity types that do not have key attributes of their own are called weak entity types. Entities belonging to a weak entity type are identified by being related to specific entities from another entity type in combination with one of their attribute values.

A weak entity type normally has a **partial key**, which is the attribute that can uniquely identify weak entities that are related to the same owner entity type.

In ER diagrams, both a weak entity type and its identifying relationship are distinguished by surrounding their boxes and diamonds with double lines. The partial key attribute is underlined with a dashed or dotted line.

### ER Diagrams, Naming conventions, and Design issues
#### Summary of notation for ERD
<figure>
  <figcaption style="text-align:center;">Notation of ERD</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img src="dbfigures/notation.png" alt="Notation of ERD" title="Notation of ERD">
</figure>
#### Naming conventions
We choose to use *singular names for entity types*, rather than plural ones, because the entity type name applies to each individual entity belonging to that entity type. In our ER diagrams, we will use the convention that *entity type and relationship type names are uppercase letters*, *attribute names have their initial letter capitalized*, and role names are lowercase letters. The *nouns* appearing in the narrative tend to give rise to entity type names, and the *verbs* tend to indicate names of relationship types.

#### Alternative notations for ERD
<figure>
  <figcaption style="text-align:center;">Alternative Notation of ERD</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img src="dbfigures/AlternativeNotation.png" alt="Alternative Notation of ERD" title="Alternative Notation of ERD">
</figure>

### UML Class Diagram
<figure>
  <figcaption style="text-align:center;">UML Class Diagram</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img src="dbfigures/uml.png" alt="UML Class Diagram" title="UML Class Diagram">
</figure>

- Object = entity
- Class = entity type
	+ Class name = entity type name
	+ Attributes: The designer can optionally specify the domain of an attribute if desired, by placing a colon (:) followed by the domain name or description.
		A multivalued attribute will generally be modeled as a separate class.
	+ Operations
- Associations = relationship type
- Links = relationship instance
- ... (research continue)

### Relationship types of degree higher than two
#### Choosing between binary and Ternary relationships
Meaning is different between three binary relationship and ternary relationship.

#### Constraints on ternary relationships
- First notation: the cardinality ratio
- Second notation: the (min, max) notation

## The Enhanced Entity Relationship (EER) model
Add the concepts of **class/subclass relationships**, **type inheritance**, **generalization**, **specialization** and **category** or **union type** into the ER model.
### Subclasses, Superclasses, and Inheritance


## Relational databases design by ER-EER to relational mapping

## Practical Design methodology and use of UML Diagrams

# Object, Object-Relational, and XML: Concepts, Models, Languages, and Standards
## Object and Object-Relational Databases

## XML: Extensible Markup Language

# Databases Programming Technique
## Introduction to SQL Programming

## Web database programming using PHP

# Databases Design Theory and Normalization
## Basics of Functional Dependencies and Normalization for Relational Databases

## Relational Databases design algorithms and further dependencies

# File Structures, Indexing and Hashing
## Disk Storage, Basic file structure, and Hashing

## Indexing structure for files

# Query Processing and Optimization, and Databases Tuning
## Algorithms for Query Processing and Optimization

## Physical Databases Design and Tuning

# Transaction Processing, Concurrency control, and Recovery
## Transaction Processing Concept and Theory

## Concurrency control

## Databases Recovery

# Security and Distribution
## Databases Security

## Databases Distributed

# Advanced Databases Models, Systems, and Applications
## Enhanced Data Models for Advanced Applications

## Introduction to Information Retrieval and Web Search

## Data Mining Concepts

## Overview of Data Warehousing and OLAP


# Real Knowledge
## Stored Procedure
- http://www.techrepublic.com/article/determine-when-to-use-stored-procedures-vs-sql-in-the-code/
- http://www.seguetech.com/blog/06/04/Advantage-drawbacks-stored-procedures-processing-data
- http://programmers.stackexchange.com/questions/65742/stored-procedures-a-bad-practice-at-one-of-worlds-largest-it-software-consulting

## DAtabase URI
sqlite:////tmp/test.db
mysql://username:password@server/db

## [MyISAM vs InnoDB](http://stackoverflow.com/questions/20148/myisam-versus-innodb)
- [rackspace article](http://www.rackspace.com/knowledge_center/article/mysql-engines-myisam-vs-innodb)
- http://en.wikipedia.org/wiki/Comparison_of_MySQL_database_engines
- http://tag1consulting.com/MySQL_Engines_MyISAM_vs_InnoDB
- http://en.wikipedia.org/wiki/MyISAM

Here is a small overview of which type you should use in which situation:

|                                                | My ISAM | InnoDB |
| -                                              | -       | -      |
| Required full text Search                      | Yes     | 5.6+   |
| Require Transactions                           |         | Yes    |
| frequent select queries                        | Yes     |        |
| frequent insert,update,delete                  |         | Yes    |
| Row Locking (multi processing on single table) |         | Yes    |
| Relational base design                         |         | Yes    |

To summarize:

Frequent reading, almost no writing   => MyISAM
Full text search in MySQL <= 5.5      => MyISAM


InnoDB offers:

    ACID transactions
    row-level locking
    foreign key constraints
    automatic crash recovery
    table compression (read/write)
    spatial data types (no spatial indexes)

In InnoDB all data in a row except for TEXT and BLOB can occupy 8,000 bytes at most. No full text indexing is available for InnoDB. In InnoDB the COUNT(*)s (when WHERE, GROUP BY, or JOIN is not used) execute slower than in MyISAM because the row count is not stored internally. InnoDB stores both data and indexes in one file. InnoDB uses a buffer pool to cache both data and indexes.

MyISAM offers:

    fast COUNT(*)s (when WHERE, GROUP BY, or JOIN is not used)
    full text indexing
    smaller disk footprint
    very high table compression (read only)
    spatial data types and indexes (R-tree)

MyISAM has table-level locking, but no row-level locking. No transactions. No automatic crash recovery, but it does offer repair table functionality. No foreign key constraints. MyISAM tables are generally more compact in size on disk when compared to InnoDB tables. MyISAM tables could be further highly reduced in size by compressing with myisampack if needed, but become read-only. MyISAM stores indexes in one file and data in another. MyISAM uses key buffers for caching indexes and leaves the data caching management to the operating system.

Overall I would recommend InnoDB for most purposes and MyISAM for specialized uses only. InnoDB is now the default engine in new MySQL versions.
