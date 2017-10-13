---
title: Hibernate的配置方法及little bug
date: 2016-11-27 23:39:44
tags:
- java
- SSH
- hibernate
---

我的文件路径：
![工程路径](http://ww1.sinaimg.cn/large/005Kw4nRgw1f9zyxpd6sfj306m0dhdhw.jpg)
<!--more-->
### 基本配置：
下载hibernate-release-4.2.4.Final
在myeclipse项目右键build path->configure build path->add external jar 
导入liberary
src路径下配置hiberate.cfg.xml配置文件
```
<?xml version='1.0' encoding='utf-8'?>
<!DOCTYPE hibernate-configuration PUBLIC
        "-//Hibernate/Hibernate Configuration DTD 3.0//EN"
        "http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">

<hibernate-configuration>

    <session-factory>

        <!-- Database connection settings -->
        <property name="connection.driver_class">com.mysql.jdbc.Driver</property>
        <property name="connection.url">jdbc:mysql://localhost/hibernate</property>
        <property name="connection.username">root</property>
        <property name="connection.password">password</property>

        <!-- JDBC connection pool (use the built-in) -->
        <property name="connection.pool_size">1</property>

        <!-- SQL dialect -->
        <property name="dialect">org.hibernate.dialect.MySQLDialect</property>

        <!-- Enable Hibernate's automatic session context management -->
        <property name="current_session_context_class">thread</property>

        <!-- Disable the second-level cache  -->
        <property name="cache.provider_class">org.hibernate.cache.internal.NoCacheProvider</property>

        <!-- Echo all executed SQL to stdout -->
        <property name="show_sql">true</property>

        <!-- Drop and re-create the database schema on startup -->
        <property name="hbm2ddl.auto">update</property>

        <mapping resource="com/hdu/model/hibernate.hbm.xml"/>

    </session-factory>

</hibernate-configuration>
```
在model路径下配置hibernate.hbm.xml
```
<?xml version="1.0"?>
<!DOCTYPE hibernate-mapping PUBLIC
  "-//Hibernate/Hibernate Mapping DTD 3.0//EN"
  "http://www.hibernate.org/dtd/hibernate-mapping-3.0.dtd">
<hibernate-mapping package="com.hdu.model">
 <class name="Student" table="student">
  <id name="id" column="id">
  </id>
  <property name="name" type="string" column="name"/>
  <property name="password" type="string" column="password"/>
 </class>
</hibernate-mapping>
```
model/Student.java
```
package com.hdu.model;

public class Student {
	private int id;
	private String name;
	private String password;
	public int getId() {
		return id;
	}
	public void setId(int id) {
		this.id=id;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name=name;
	}
	public String getPassword() {
		return password;
	}
	public void setPassword(String password) {
		this.password=password;
	}
	
}
```

测试文件hibernate.java(test路径下)
```
import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.cfg.Configuration;
import com.huxing.hibernate.model.Student;
public class StudentTest {
 public static void main(String[] args) {
  Student a = new Student();
  a.setId(123);
  a.setName(32);
  a.setPassword("hello hibernate!");
  Configuration cfg = new Configuration();
  SessionFactory cf = cfg.configure().buildSessionFactory();
  Session session = cf.openSession();
  session.beginTransaction();
  session.save(a);
  session.getTransaction().commit();
  session.close();
  cf.close();
 }
}
```
### 关于struct和hibernate的antlr.jar文件版本冲突导致
**antlr.collections.AST.getLine()I错误**

解决：
删除struts中的低版本的antlr-2.7.2.jar
1、打开window->perferences->Myeclipse->project liberary->
勾选enable advanced configuration
修改struts2.1下core下anltr的勾选去掉。
重新部署struts2.1的liberary
右键项目Myeclipse->project fects->mananger进去配置一下
ps：请将tomcat路径下的低版本antlr也删除
over~


