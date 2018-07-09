The minimal demo to use maven plugin to generate code by using avro

# Introduction

## Configuration

This is base on the [article](https://dzone.com/articles/using-avros-code-generation) and make some improvements for it.

There are two types of configuration for plugin: 

1. for execution, which is only applied during the lifecycle include specified phase, see [Maven official document](https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html) to understand this mechanism. Avro official document use the `generate-sources` phase which 

2. for plugin global which can be applied when execute the plugin goal separately.

## NameSpace

The name space of the avro scheme file is important which decide to package of generated code.

```json
{
  "namespace": "science.mengxin.java.avro.demo"
}
```

## Maven Lifecycle

run 

```bash
mvn package 
```

or

```bash
mvn compile
```

the code will be generate to the specific folder

## Maven run plugin goal

During development, the compile or package may not work, we can use this goal to generate code.

```bash
mvn avro:scheme
mvn avro:protocol
mvn avro:idl-protocol
```

# Steps

## Step 1: add POM plugin and dependency

Check the official document

```xml
<dependency>
  <groupId>org.apache.avro</groupId>
  <artifactId>avro</artifactId>
  <version>1.8.2</version>
</dependency>
```

plugin

```xml

<plugin>
  <groupId>org.apache.avro</groupId>
  <artifactId>avro-maven-plugin</artifactId>
  <version>1.8.2</version>
  <executions>
    <execution>
      <phase>generate-sources</phase>
      <goals>
        <goal>schema</goal>
      </goals>
      <configuration>
        <sourceDirectory>${project.basedir}/src/main/avro/</sourceDirectory>
        <outputDirectory>${project.basedir}/src/main/java/</outputDirectory>
      </configuration>
    </execution>
  </executions>
</plugin>
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-compiler-plugin</artifactId>
  <version>3.7.0</version>
  <configuration>
    <source>1.8</source>
    <target>1.8</target>
  </configuration>
</plugin>
      


```


## Step 2: add Scheme File


## Step 3: run goal and generate code