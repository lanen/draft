Java persistence API
====================

JPA 是 J2EE 持久化对象的规范，JPA 做了如下定义：

1. the Java persistence API
2. the query language
3. Object/relational mapping metadata


 
##the Java persistence API

API 中定义了`实体`和`实体管理`
### Entites 实体

#### 实体（Entities）的定义

An entity is a lightweight persistence domain object. Typically an entity represents a table in a relational database, and each entity instance corresponds to a row in that table. The primary programming artifact of an entity is the entity class（一个实体的主要编程工作在于定义实体类）。
`The persistent state` of an entity is represented either through `persistent fields or persistent properties`. These fields or properties use `object/relational mapping annotations` to map the entities and entity relationships to the relational data in the underlying data store


#### 实体类（Entity Classes）

实体类的定义必须满足如下需求：

- The class must be annotated with the `javax.persistence.Entity` annotation.

- The class must *have a public or protected, no-argument constructor*. The class may have other constructors.

- The class must *not be declared final*. No methods or persistent instance variables must be declared final.

- If an entity instance be passed by value as a detached object, such as through a session bean’s remote business interface, the class *must implement the Serializable interface*.

- Entities may extend both entity and non-entity classes, and non-entity classes may extend entity classes.

- Persistent instance variables must be declared private, protected, or package-private, and can only be accessed directly by the entity class’s methods. Clients must access the entity’s state through accessor or business methods.

实体类中会出现 persistent fields 和 persistent properties


- 什么是 Persistent Fields


	If the entity class uses persistent fields, the Persistence runtime accesses entity class instance variables directly. All fields not annotated javax.persistence.Transient or not marked as Java transient will be persisted to the data store. The object/relational mapping annotations must be applied to the instance variables.


- 什么是 Persistent Properties


	If the entity uses persistent properties, the entity must follow the method conventions of JavaBeans components. JavaBeans-style properties use getter and setter methods that are typically named after the entity class’s instance variable names. For every persistent property property of type Type of the entity, there is a getter method getProperty and setter method setProperty. If the property is a boolean, you may use isProperty instead of getProperty. For example, if a Customer entity uses persistent properties, and has a private instance variable called firstName, the class defines a getFirstName and setFirstName method for retrieving and setting the state of the firstName instance variable.



Entities may either use persistent fields or persistent properties. If the mapping annotations are applied to the entity’s instance variables, the entity uses persistent fields. If the mapping annotations are applied to the entity’s getter methods for JavaBeans-style properties, the entity uses persistent properties. You cannot apply mapping annotations to both fields and properties in a single entity.

实体类可以通过注解需要持久化的字段或者通过gettor/settor 待持久化属性（persistent properties，可能在xml配置）


- Primary Keys in Entities

Each entity has a unique object identifier，Simple primary keys use the `javax.persistence.Id` annotation to denote the primary key property or field.

Composite primary keys must correspond to either a single persistent property or field, or to a set of single persistent properties or fields. Composite primary keys must be defined in a primary key class. Composite primary keys are denoted using the javax.persistence.EmbeddedId and javax.persistence.IdClass annotations.

- 实体类之间的关系

one-to-one, one-to-many, many-to-one, and many-to-many，有了这些关联，常见用于级联删除记录

*One-to-one*: Each entity instance is related to a single instance of another entity. For example, to model a physical warehouse in which each storage bin contains a single widget, StorageBin and Widget would have a one-to-one relationship. One-to-one relationships use the javax.persistence.OneToOne annotation on the corresponding persistent property or field.

*One-to-many*: An entity instance can be related to multiple instances of the other entities. A sales order, for example, can have multiple line items. In the order application, Order would have a one-to-many relationship with LineItem. One-to-many relationships use the javax.persistence.OneToMany annotation on the corresponding persistent property or field.

*Many-to-one*: Multiple instances of an entity can be related to a single instance of the other entity. This multiplicity is the opposite of a one-to-many relationship. In the example just mentioned, from the perspective of LineItem the relationship to Order is many-to-one. Many-to-one relationships use the javax.persistence.ManyToOne annotation on the corresponding persistent property or field.

*Many-to-many*: The entity instances can be related to multiple instances of each other. For example, in college each course has many students, and every student may take several courses. Therefore, in an enrollment application, Course and Student would have a many-to-many relationship. Many-to-many relationships use the javax.persistence.ManyToMany annotation on the corresponding persistent property or field.


- 实体类继承 



- Abstract Entities 抽象实体

实际的查询会在子类进行

- Mapped Superclasses 映射父类

Entities may inherit from superclasses that contain persistent state and mapping information, but are not entities. That is, the superclass is not decorated with the @Entity annotation, and is not mapped as an entity by the Java Persistence provider. These superclasses are most often used when you have state and mapping information common to multiple entity classes. (被多个实体继承，该类供子类通用的持久化状态和映射信息)，该类无法进行持久化操作和查询操作


- Non-Entity Superclasses 非实体父类

没有可映射的数据表

- 继承的映射策略

	- A single table per class hierarchy （单表-对应一个实体继承层次）

	- A table per concrete entity class （表与子类一一对应）

	- A “join” strategy, where fields or properties that are specific to a subclass are mapped to a different table than the fields or properties that are common to the parent class






### Managing Entites 管理实体

Entities are managed by the entity manager。The entity manager is represented by `javax.persistence.EntityManager` instances. Each `EntityManager` instance is associated with *a persistence context*. A persistence context defines the scope under which particular entity instances are created, persisted, and removed



待续：http://docs.oracle.com/javaee/5/tutorial/doc/bnbqw.html



### Requirements for Entity Classes
### Persistent Fields and Properties in Entity Classes
### Multiplicity in Entity Relationships
### Direction in Entity Relationships
### Entity Inheritance

##the query language

##Object/relational mapping metadata