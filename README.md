# transient-plugin-lifecycle
A Maven lifecycle plugin, like "jar" but with with no "package", "deploy", or "release" phase.

It was created for transient test projects, and for speculative creation of transient release modules for
multi-release jars, where I don't want anything installed in the local repo, or a remote one, thus the "transient" name.  

Use like this:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <!-- ... -->
    <groupId>.</groupId>
    <artifactId>.</artifactId>
    <version>.</version>
    <packaging>transient</packaging> <!-- use "transient" packaging -->
    <!-- ... -->
    <build>
        <!-- ... -->
        <extensions>
            <extension> <!-- Register "transient" packaging -->
                <groupId>rwperrott.maven.plugins</groupId>
                <artifactId>transient-lifecycle-extension</artifactId>
                <version>1.1-SNAPSHOT</version>
            </extension>
            <!-- ... -->
        </extensions>
        <!-- ... -->
    </build>
</project>
```
.. to replace verbose hacks like:
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <!-- ... -->
    <groupId>.</groupId>
    <artifactId>.</artifactId>
    <version>.</version>
    <packaging>transient</packaging> <!-- use "transient" packaging -->
    <!-- ... -->
    <build>
        <pluginManagement>
            <plugins>
                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-jar-plugin</artifactId>
                    <version>.</version>
                    <executions>
                        <execution>
                            <id>default-jar</id>
                            <phase>none</phase>
                        </execution>
                        <execution>
                            <id>default-test-jar</id>
                            <phase>none</phase>
                        </execution>
                    </executions>
                </plugin>
                <!-- ... -->
            </plugins>
        </pluginManagement>
    </build>
</project>
```