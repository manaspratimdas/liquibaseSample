# liquibaseSample
Demonstrate the use of liquibase maven project for database migration
Database migration with Liquibase

Liquibase can be used for database migration. It can be part of a project(like JHipster) or we can create an isolated liquibase maven project or run liquibase as command line

There are two scenario when we use Liquibase in isolation one is database migration in development environment and another is in production/customer environment. 

Database migration in development environment:

   1. Create a Maven project in eclipse.

   2. Create file liquibase.properties in resource folder

driver:com.mysql.jdbc.Driver
url:jdbc:mysql://localhost:3306/myliquibasesample
username:root
password:manas
changeLogFile:src/main/resources/liquibase/master.xml
  .  
Update the pom file to add dependency for MySQL, Liquibase and Liquibase-maven-plugin.

<dependencies>
		<dependency>
			<groupId>org.liquibase</groupId>
			<artifactId>liquibase-core</artifactId>
			<version>3.3.0</version>
		</dependency>
		<dependency>
			<groupId>mysql</groupId>
			<artifactId>mysql-connector-java</artifactId>
			<version>5.1.6</version>
		</dependency>

	</dependencies>

	<build>
		<plugins>
			<plugin>
				<groupId>org.liquibase</groupId>
				<artifactId>liquibase-maven-plugin</artifactId>
				<version>3.4.2</version>
				<configuration>
					<propertyFile>src/main/resources/liquibase/liquibase.properties</propertyFile>
				</configuration>
				<executions>
					<execution>
						<goals>
							<goal>update</goal>
						</goals>
					</execution>
				</executions>
			</plugin>
		</plugins>
	</build>

Add databaseChangeLog file in resource folder. In this case name of the databaseChangeLog file is master.xml. This file is refereed in the liquibase.properties file.

 We can have additional databaseChangeLog file which can be included in the master.xml 

　　6.  We run liquibase:update as maven goal for the project and if everything is good we will see changes in database.
  	
　　
Database migration in production/customer environment:
 
  1. Create a folder.

  2. Copy the jar file for Liquibase and MySQL connector
　　liquibase-core-3.4.2.jar
　　mysql-connector-java-5.1.6.jar 
　　
  3. Copy the master.xml or any other databaseChangeLog file in the same folder

  4. Run the command from the folder

　　java -jar liquibase-core-3.4.2.jar --driver=com.mysql.jdbc.Driver --classpath=mysql-connector-java-5.1.6.jar --changeLogFile=master.xml --url="jdbc:mysql://localhost:3306/myliquibasesample" --username=root --password=manas update    
　　
　　Note: We can also create a script file with the above command and just run the script file.
　　
 5. If everything is good you will receive the below message

　　Liquibase Update Successful
