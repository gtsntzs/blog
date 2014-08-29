
# Under Construction

## In Brief

This is a collection of examples using modern frameworks mainly in Java language.

a list of frameworks being used is: 

* Apache Camel
* Apache Lucene
* Spring IO
* Maven 
	
containers like:

* Fabric8.io
* Apache Karaf

and persistence providers :

* Apache Cassandra
* Apache Sorl
* RedisIO

--- 


## Usage

In order to use the examples you need to have maven 3.2.1 and above, git and java 1.7 or greater.

### Documentation

Every project has its own documentation site. 

### Maven Project Structure

The project structure is organised in a way to make life easier, but first lets put some terminology through. When a project ends with "Aggregator" implies that it 's none of the other sub-projects are dependent on it. If it contains "Parent" it manages all dependencies and plugins of the sub-projects. When contain none of the above terms its a project Example

In order to use an example it has to be packaged by packaging its Parent project.

---

## Configuration

The skin is configurable using the `<custom>` element in your `site.xml` file. The available
options are [described in the documentation][doc]. A sample configuration file is below:

[doc]: config.html

```xml
<project>
  ...
  <custom>
    <reflowSkin>
      <theme>bootswatch-spacelab</theme>
      <highlightJs>true</highlightJs>
      <brand>
        <name>My Project</name>
        <href>http://github.com/andriusvelykis/reflow-maven-skin</href>
      </brand>
      <slogan>Super interesting project doing good things.</slogan>
      <titleTemplate>%2$s | %1$s</titleTemplate>
      <toc>top</toc>
      <topNav>Download|reports</topNav>
      <bottomNav>
        <column>Main|Download</column>
        <column>Documentation</column>
        <column>reports|modules</column>
      </bottomNav>
      <bottomDescription>
        This is a very good project doing interesting and valuable things.
      </bottomDescription>
      <pages>
        <index project="project-id">
          <shortTitle>Welcome</shortTitle>
          <breadcrumbs>false</breadcrumbs>
          <toc>false</toc>
          <sections>
            <carousel />
            <body />
            <sidebar />
            <thumbs>2</thumbs>
            <columns>3</columns>
          </sections>
        </index>
        <developer-info>
          <toc>sidebar</toc>
        </developer-info>
      </pages>
    </reflowSkin>
  </custom>
  ...
</project>
```
--- 


## Learn by example

This website itself is generated using Reflow Maven skin and is written in Markdown.
The source code is [available on GitHub][reflow-src].

Look for the site configuration and web page sources in `/src/site` of each module;
and for plug-in configuration in respective POM files.

[reflow-src]: http://github.com/andriusvelykis/reflow-maven-skin "Reflow Maven skin source code"
