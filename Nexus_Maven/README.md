# Integrating Maven and Nexus Repository Tool


**AIM : Hosting the jar file to nexus so that become available to other developers**

Deploying maven created jar file at nexus repository manager platform.

**Step-1:** <br>
Download nexus 3.18.1-01. Extract it you will find two file : <br>
a.	nexus-3.18.1-01		b. sonatype-work   (here Configurations are stored) <br>

go to => C:\Users\Dell\Downloads\Nexus\nexus-3.18.1-01\bin  <br>
run command :     nexus.exe   /run <br>
 
![image](https://user-images.githubusercontent.com/46487696/120102207-827db200-c167-11eb-892b-59d0708b2827.png)

You will see such screen in your command line.

**Step-2** <br>

Open browser and type localhost:8081 <br>
Nexus Repository Dashboard will be open. <br>
Sign-in in you dashboard, It will ask for the password first <br>
Configure Your password: <br>
Goto “sonatype-work > nexus3>admin.password” <br>
Open the file admin.password, Copy the unique/one time key and paste at the password option <br>
After this it will ask for the new password and submit and you will enter in your nexus Homepage. <br>
 
![image](https://user-images.githubusercontent.com/46487696/120102213-87426600-c167-11eb-8ea3-1a3999910e2f.png)


**Step-3:** <br>
To Create Repository <br>

Go to “Setting> Repository> Create Repository” and click <br>
Now select “maven (hosted)” type	 repository because we are working on a maven project. <br>

Configurations required : <br>

a.	Give name for the project <br>
b.	In Version policy: Select  “Snapshot” as our maven project version in snapshot. <br>
c.	In Hosted : Select Allow redeploy so we can re-deploy it at anytime. <br>

Now Create the repo. <br>

![image](https://user-images.githubusercontent.com/46487696/120102247-b6f16e00-c167-11eb-9e22-e4ea2952ac61.png)

**Step-4:** <br>
Goto maven folder location , open  Conf folder and then open settings xml document. <br>
Write the below command too. <br>
a.	Id can be anything according to you. <br>
b.	Username and password same as nexus repo manager web application <br>

```<server>
  <id>cicd_lab8</id>
  <username>admin</username>
  <password>*******</password>
</server> <br>
```

![image](https://user-images.githubusercontent.com/46487696/120102256-c1136c80-c167-11eb-955b-b494774a7ce3.png)

**Step-5:** <br>
Since we have to deploy so we will run mvn deploy command. <br>
For this we have to some changes in our maven project pom file to connect to the nexus repo manager. <br>

Configurations:

    <maven.compiler.source>1.6</maven.compiler.source>
    <maven.compiler.target>1.6</maven.compiler.target>
	<distributionManagement>
	<snapshotRepository>
	<id>upes</id>
	<name>upes</name>
	<url>http://localhost:8081/repository/cicd_lab8/</url>
	</snapshotRepository>
	</distributionManagement>

A.
 
![image](https://user-images.githubusercontent.com/46487696/120102262-c670b700-c167-11eb-99f7-70bcb5fd4cc6.png)

B.
 
![image](https://user-images.githubusercontent.com/46487696/120102265-ca9cd480-c167-11eb-8536-eeb16adf6885.png)

**Step-6:** <br>

Goto the maven project where pom file is stored. <br>
Run command “mvn deploy” <br>
This command will automatically run the maven goal before the deploy goal like clean and install goal of maven. <br>
 jar file will be create and will host the jar file to the nexus repo manager. <br>
A.	

![image](https://user-images.githubusercontent.com/46487696/120102267-d092b580-c167-11eb-99fe-0ce6869bedb9.png)

B.
 
![image](https://user-images.githubusercontent.com/46487696/120102276-d4bed300-c167-11eb-97fb-f195aa6fd681.png)
