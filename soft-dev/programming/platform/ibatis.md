[TOC]

# Overview
iBATIS is a persistence framework which automates the mapping between SQL databases and objects in Java, .NET, and Ruby on Rails. The mapping are decoupled from the application logic by packaging the SQL statements in XML configuration files.

iBATIS is what is known as a data mapper and takes care of **mapping the parameters and results between the class properties and the column of the database table**.

A significant difference between iBATIS and other persistence frameworks such as Hibernate is that iBATIS empasizes use of SQL, while othe frameworks typically use a custom query language such has the *Hibernate Query Language* (HQL) or *Enterprise JavaBeans Query Language* (EJB QL).

## iBATIS Design Philosophies:
iBATIS comes with the following design philosophies:

**Simplicity**: iBATIS is widely regarded as being one of the simplest persistence frameworks available today.

**Fast Development**: iBATIS's philosophy is to do all it can to facilitate hyper-fast development.

**Portability**: iBATIS can be implemented for nearly any language or platform like Java, Ruby, and C# for Microsoft .NET.

**Independent Interfaces**: iBATIS provides database-independent interfaces and APIs that help the rest of the application remain independent of any persistence-related resources,

**Open source**: iBATIS is free and an open source software.

## Advantages of IBATIS
Here are few advantages of using IBATIS:

**Suppports Stored procedures**: iBATIS encapsulates SQL in the form of stored procedures so that business logic is kept out of the database, and the application is easier to deploy and test, and is more portable.

**Supports Inline SQL**: No precompiler is needed, and you have full access to all of the features of SQL.

**Supports [Dynamic SQL](https://ibatis.apache.org/docs/dotnet/datamapper/ch03s09.html)**: iBATIS provides features for dynamically building SQL queries based on parameters.

**Supports O/RM**: iBATIS supports many of the same features as an O/RM tool, such as lazy loading, join fetching, caching, runtime code generation, and inheritance

# Tutorial
## SqlMapConfig.xml
This is where you need to provide all configurations required for iBatis.

	<?xml version="1.0" encoding="UTF-8"?>
	<!DOCTYPE sqlMapConfig
	PUBLIC "-//ibatis.apache.org//DTD SQL Map Config 2.0//EN"
	"http://ibatis.apache.org/dtd/sql-map-config-2.dtd">

	<sqlMapConfig>
	     <settings useStatementNamespaces="true"/>

	     <transactionManager type="JDBC">
	        <dataSource type="SIMPLE">
	          <property name="JDBC.Driver"
	               value="com.mysql.jdbc.Driver"/>
	          <property name="JDBC.ConnectionURL"
	               value="jdbc:mysql://localhost:3306/testdb"/>
	          <property name="JDBC.Username" value="root"/>
	          <property name="JDBC.Password" value="root"/>
	        </dataSource>
	      </transactionManager>

	     <sqlMap resource="Employee.xml"/>
	</sqlMapConfig>

A POJO (Plain Old Java Objects) class correspond with a table in database.

File `.xml` configure for each table:

		<?xml version="1.0" encoding="UTF-8"?>
		<!DOCTYPE sqlMap
		PUBLIC "-//ibatis.apache.org//DTD SQL Map 2.0//EN"
		"http://ibatis.apache.org/dtd/sql-map-2.dtd">

		<sqlMap namespace="Employee">

		<insert id="insert" parameterClass="Employee">

		   insert into EMPLOYEE(first_name, last_name, salary)
		   values (#first_name#, #last_name#, #salary#)

		   <selectKey resultClass="int" keyProperty="id">
		      select last_insert_id() as id
		   </selectKey>

		</insert>

		<select id="abc" parameterClass="abc" resultClass="abc">
			....
		</select>

		<update id="abc" parameterClass="abc">
			UPDATE EMPLOYEE
	 		SET    first_name = #first_name#
			WHERE  id = #id#
		</update>

		<delete id="abc" parameterClass="abc">
			DELETE FROM EMPLOYEE
		  WHERE  id = #id#
		</delete>

		<!-- Using ResultMap -->
		 <resultMap id="result" class="Employee">
		    <result property="id" column="id"/>
		    <result property="first_name" column="first_name"/>
		    <result property="last_name" column="last_name"/>
		    <result property="salary" column="salary"/>
		</resultMap>
		<select id="useResultMap" resultMap="result">
		         SELECT * FROM EMPLOYEE
		         WHERE id=#id#
		</select>


		</sqlMap>





## [Dynamic SQL](http://www.tutorialspoint.com/ibatis/ibatis_dynamic_sql.htm)
[ibatis dynamic sql](https://ibatis.apache.org/docs/dotnet/datamapper/ch03s09.html)
