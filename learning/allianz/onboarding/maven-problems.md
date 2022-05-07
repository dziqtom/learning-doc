#MAVEN Problems

---
##JUnit problem
It seems that there is a problem with junit launch platform in IJ.\
Projects don't contain any artifacts in pom.xml for it and once the tests are launched in
IJ the error similar to below appears: 

```Error running 'XYZTest': Failed to resolve org.junit.vintage:junit-vintage-engine:A.B.C```  
##Explanation
IJ needs the library in local maven repo but there in no dependency in pom.xml, this however does not break the builds in CI tools (tekton) 
for some reasons as CI tools download it by themselves. 
##Solution
Add for a while appropriate entry in pom.xml and refresh the maven project:
``` 
        <dependency>
            <groupId>org.junit.vintage</groupId>
            <artifactId>junit-vintage-engine</artifactId>
            <version>5.8.2</version>
            <scope>test</scope>
        </dependency>
```
and then `$ mvn clean install`

That should download missing library and IJ should be able to launch the tests.
After tests are working it can be removed from pom.xml, not sure why it is not in the pom anyway 