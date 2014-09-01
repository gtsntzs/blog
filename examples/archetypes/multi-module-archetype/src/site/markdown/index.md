##Purpose 

A simple custom Maven Archetype example for java projects generation.

---

## Procedure

Generate a simple project or by using maven-archetype-archetype. Create the project structure in  the archetype-resources as wished. 

	simple-archetype
	├── pom.xml
	└── src
	    ├── main
	    │   └── resources
	    │       ├── archetype-resources
	    │       │   ├── pom.xml
	    │       │   ├── Readme.md
	    │       │   └── src
	    │       │       ├── main
	    │       │       │   ├── java
	    │       │       │   │   └── App.java
	    │       │       │   └── resources
	    │       │       ├── site
	    │       │       └── test
	    │       │           └── java
	    │       │               └── AppTest.java
	    │       └── META-INF
	    │           └── maven
	    │               └── archetype-metadata.xml
	    └── site


The simple-archetype pom requires to be packaged as maven-archetype and to include the archetype-packaging and maven-archetype-plugin plugins in the build tag.

```xml
<project 
	xmlns="http://maven.apache.org/POM/4.0.0" 
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
  
  <parent>
	 <groupId>soa.gtsntzs</groupId>
	 <artifactId>archetypes</artifactId>
	 <version>1.0.0</version>
  </parent>
  
  <modelVersion>4.0.0</modelVersion>
  <groupId>soa.gtsntzs.archetypes</groupId>
  <artifactId>simple-archetype</artifactId>
  <version>1.0-SNAPSHOT</version>
  <!-- packaging is maven-archetype! -->
  <packaging>maven-archetype</packaging>
  
  <url>http://gtsntzs.github</url>
  <name>Simple :: Archetype</name>
    
  <description>
		Simple Archetype.
  </description>

 <build>
    <extensions>
      <extension>
        <groupId>org.apache.maven.archetype</groupId>
        <artifactId>archetype-packaging</artifactId>
        <version>2.2</version>
      </extension>
    </extensions>

    <pluginManagement>
      <plugins>
	        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-archetype-plugin</artifactId>
          <version>2.2</version>
        </plugin>
      </plugins>
    </pluginManagement>
  </build>
 
</project>
```

---

##Recipe

	META-INF
	    │           └── maven
	    │               └── archetype-metadata.xml
    
in the META-INF directory create a maven folder and in the folder an archetype-metadata.xml where the metadata will be specified. As metadata tags the requiredProperties define the version of the dependency to be used and the fileSets the directory structure. In a fileSet by using the includes tag only files sutisfing the specified pattern will be created in the new project. When the includes is not being used then all folders will be included as long as the have a file of any  extension as shown in the src/site directory. 


```xml
<?xml version="1.0" encoding="UTF-8"?>
<archetype-descriptor 
    xsi:schemaLocation="http://maven.apache.org/plugins/maven-archetype-plugin/archetype-descriptor/1.0.0 http://maven.apache.org/xsd/archetype-descriptor-1.0.0.xsd" 
    name="simple-archetype-java"
    xmlns="http://maven.apache.org/plugins/maven-archetype-plugin/archetype-descriptor/1.0.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    
  <requiredProperties>
    <requiredProperty key="log4j-version">
      <defaultValue>1.2.17</defaultValue>
    </requiredProperty>
    <requiredProperty key="source-version">
      <defaultValue>1.7</defaultValue>
    </requiredProperty>
    <requiredProperty key="maven-compiler-plugin-version">
      <defaultValue>2.5.1</defaultValue>
    </requiredProperty>
    <requiredProperty key="maven-resources-plugin-version">
      <defaultValue>2.6</defaultValue>
    </requiredProperty>
    <requiredProperty key="slf4j-version">
      <defaultValue>1.7.7</defaultValue>
    </requiredProperty>
    <requiredProperty key="junit-version">
      <defaultValue>4.11</defaultValue>
    </requiredProperty>
  </requiredProperties>

  <fileSets>
    <fileSet filtered="true" packaged="true" encoding="UTF-8">
      <directory>src/main/java</directory>
      <includes>
        <include>**/*.java</include>
      </includes>
    </fileSet>
    <fileSet filtered="true" encoding="UTF-8">
      <directory>src/main/resources</directory>
      <includes>
        <include>**/*</include>
      </includes>
    </fileSet>
    <fileSet filtered="true" packaged="true" encoding="UTF-8">
      <directory>src/test/java</directory>
      <includes>
        <include>**/*.java</include>
      </includes>
    </fileSet>
    <fileSet filtered="true" encoding="UTF-8">
      <directory>src/test/resources</directory>
      <includes>
        <include>**/*</include>
      </includes>
    </fileSet>
    <fileSet encoding="UTF-8">
      <directory>src/site</directory>
    </fileSet>
    <fileSet encoding="UTF-8">
      <directory></directory>
      <includes>
        <include>ReadMe.md</include>
      </includes>
    </fileSet>
  </fileSets>
</archetype-descriptor>
```

	resources
	    ├── archetype-resources
	       ├── pom.xml

The desired pom will import the groupId, artifactId, version will be given manualy by adding the tags in the mvn command or through the interactive mode. The *-version properties will be inserted from the archetype-metadata.xml specified above. 


```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" 
		 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
		 xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
							 http://maven.apache.org/maven-v4_0_0.xsd">

  <modelVersion>4.0.0</modelVersion>

  <groupId>${groupId}</groupId>
  <artifactId>${artifactId}</artifactId>
  <packaging>jar</packaging>
  <version>${version}</version>

  <name>Simple Archetype :: Project</name>
  <url>http://www.domain.org</url>

  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>

	<!-- dependencies properties -->
    <slf4j.version>${slf4j-version}</slf4j.version>
    <log4j.version>${log4j-version}</log4j.version>
    <junit.version>${junit-version}</junit.version>
    <!-- plugins properties -->
	<source.version>${source-version}</source.version>
    <maven.compiler.plugin.version>${maven-compiler-plugin-version}</maven.compiler.plugin.version>
    <maven.resources.plugin.version>${maven-resources-plugin-version}</maven.resources.plugin.version>
  </properties>

  <dependencies>
    <!-- logging -->
    <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>slf4j-api</artifactId>
      <version>${slf4j.version}</version>
    </dependency>
    <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>slf4j-log4j12</artifactId>
      <version>${slf4j.version}</version>
    </dependency>
    <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>jcl-over-slf4j</artifactId>
      <version>${slf4j.version}</version>
    </dependency>
    <dependency>
      <groupId>log4j</groupId>
      <artifactId>log4j</artifactId>
      <version>${log4j.version}</version>
    </dependency>

    <!-- testing -->
    <dependency>
	  <groupId>junit</groupId>
	  <artifactId>junit</artifactId>
 	  <version>${junit.version}</version>
      <scope>test</scope>
    </dependency>
  </dependencies>

  <build>
    <defaultGoal>install</defaultGoal>

    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>${maven.compiler.plugin.version}</version>
        <configuration>
          <source>${source.version}</source>
          <target>${source.version}</target>
        </configuration>
      </plugin>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-resources-plugin</artifactId>
        <version>${maven.resources.plugin.version}</version>
        <configuration>
          <encoding>${project.build.sourceEncoding}</encoding>
        </configuration>
      </plugin>
    </plugins>
  </build>

</project>
```

Once everything is specified as needed, install the archetype to the local repository with the command:
```sh
    mvn clean install
```
The archetype is ready for use:
```sh
mvn archetype:generate 
        -DarchetypeGroupId=soa.gtsntzs.archetypes 
        -DarchetypeArtifactId=simple-archetype 
        -DarchetypeVersion=1.0-SNAPSHOT
        -DgroupId=test.group 
        -DartifactId=test```
```

##Output 
 
The produced project structure is:
 
	test/
	├── pom.xml
	└── src
	    ├── main
	    │   ├── java
	    │   │   └── soa
	    │   │       └── gtsntzs
	    │   │           └── App.java
	    │   └── resources
	    ├── site
	    │   └── markdown
	    │       └── index.md
	    └── test
	        ├── java
	        │   └── soa
	        │       └── gtsntzs
	        │           └── AppTest.java
	        └── resources


##tips & tricks
 
* in App.java define package as : package ${groupId};
* remove from fileSet the includes tyg if all subfolder containing a file is required.    
* generate an archetype using an archetype! Replace archetype.xml with a archetype-metadata.xml as shown 

```sh 
        mvn archetype:generate 
	        -DgroupId=[your project's group id] 
	        -DartifactId=[your project's artifact id] 
	        -DarchetypeArtifactId=maven-archetype-archetype
```


> Written with [StackEdit](https://stackedit.io/).
