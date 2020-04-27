---
layout: post
title:  "How to Use Github As Maven Artifactory"
date:   2020-04-27 02:53:47 +0530
categories: jekyll update
---

#### How to Use Github As Maven Artifactory

Managing maven artifactory is vital in most java/scala projects as there are many common dependent jars/components built across organization. 

To manage articatory there are few managed tools available in the market like jfrog, bintray etc. But these tools come with a cost.

But what if I tell you that we have a very easy solution to manage artifactory that-to with github, let's get in depth.

To get clear understanding let's call Common-project as "vanilla" and the consuming-project as "chocolate"

**Step 1:**

1. Create repo on GitHub: https://github.com/vanilla/

2. vanilla project pom plugin should be like,

        <groupId>vanilla</groupId>
        <artifactId>vanilla</artifactId>
        <version>0.1</version>      
        <build>
            <plugins>
                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-dependency-plugin</artifactId>
                    <version>3.1.2</version>
                    <executions>
                        <execution>
                            <id>copy-installed</id>
                            <phase>install</phase>
                            <goals>
                                <goal>copy</goal>
                            </goals>
                            <configuration>
                                <artifactItems>
                                    <artifactItem>
                                        <groupId>${groupId}</groupId>
                                        <artifactId>${artifactId}</artifactId>
                                        <version>${version}</version>
                                        <type>jar</type>
                                        <outputDirectory>${project.build.directory}/../${groupId}/${artifactId}/${version}/</outputDirectory>
                                    </artifactItem>
                                </artifactItems>
                            </configuration>
                        </execution>
                    </executions>
                </plugin>
            </plugins>
        </build>

3. Once you build the project , the jar file will be in the location under ${project_directory}/vanilla/vanilla/0.1/vanilla-0.1.jar

4. Push the jar to github repo , make sure the jar is present as below,
https://github.com/vanilla/blob/master/vanilla/vanilla/0.1/vanilla-0.1.jar

**Step 2:**

1. Add Repository in chocolate pom.xml.

        <repositories>
            <repository>
                <id>vanilla-common</id>
                <name>vanilla Common</name>
                <url>https://github.com/vanilla/blob/master/vanilla/</url>
            </repository>
        </repositories>

2. Add dependency to your chocolate pom.xml file:

        <dependency>
            <groupId>vanilla</groupId>
            <artifactId>vanilla</artifactId>
            <version>0.1</version>
        </dependency>

All Set !!!!!! 


    



