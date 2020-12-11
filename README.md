# transient-plugin-lifecycle
A Maven lifecycle plugin, like "jar" but with with no "package", "deploy", or "release" phase.

Create it for transients tests, and for speculative creation of transient release modules for
multi-release jars, where I don't want anything installed, thus the "transient" name.  

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
                <groupId>rwperrott</groupId>
                <artifactId>transient-plugin-lifecycle</artifactId>
                <version>1.0-SNAPSHOT</version>
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