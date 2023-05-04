Download Link: https://assignmentchef.com/product/solved-cs5200pr1-setup-development-environment
<br>
<span style="font-size: 2.61792em; letter-spacing: -1px; font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen-Sans, Ubuntu, Cantarell, 'Helvetica Neue', sans-serif;">Introduction</span>

For this course we will be using the Java programming language to implement Spring Boot based Web applications hosted on Amazon Web Services (AWS). This assignment will walk you through setting up the local development environment and deploying a simple Hello World Web application on AWS. We will be expanding this application as the semester progresses. This document is ​ <a href="https://docs.google.com/document/d/1AE2FPPzAW5_TksvpzCtpNc8MWU2nI88HtH4M5Bju4Og/edit?usp=sharing">also available onlin</a>​ <a href="https://docs.google.com/document/d/1AE2FPPzAW5_TksvpzCtpNc8MWU2nI88HtH4M5Bju4Og/edit?usp=sharing">e</a><a href="https://docs.google.com/document/d/1AE2FPPzAW5_TksvpzCtpNc8MWU2nI88HtH4M5Bju4Og/edit?usp=sharing">.</a><u>​</u>

<h2>Learning Objectives</h2>

By the end of this assignment you should be able to

<ul>

 <li>Configure a local Java development environment</li>

 <li>Create a simple Spring Boot Web application</li>

 <li>Configure a remote Tomcat server running on AWS</li>

 <li>Deploy a Spring Boot Web application to AWS</li>

</ul>

<h1>Setup Java JDK 8</h1>

We will be using the latest version of <a href="https://www.oracle.com/java/index.html">Jav</a><u>​            </u><a href="https://www.oracle.com/java/index.html">a</a> throughout the semester. Navigate to Oracle’s Java Development Kit (JDK) 8 download website




<a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html">http://www.oracle.com/technetwork/java/javase/downloads/index.html</a>




Download and install the JDK for your particular operating system. Once the JDK has installed, verify you have the right version of Java installed. From your terminal or console, type the following




<table width="624">

 <tbody>

  <tr>

   <td width="624"><strong>&gt; java -version </strong>java version “1.8.0_77”Java(TM) SE Runtime Environment (build 1.8.0_77-b03)</td>

  </tr>

 </tbody>

</table>




On macOS you can find out where Java is installed by typing the following on the terminal:




<strong>&gt; which java </strong>

/Library/Java/JavaVirtualMachines/jdk1.8.0_77.jdk/Contents/Home//bin/java




On Windows, Java should install in Program Files/Java​




Verify environment variable JAVA_HOME​ points to the Java installation folder. From your terminal or console, type the following




<strong>&gt; echo $JAVA_HOME </strong>

/Library/Java/JavaVirtualMachines/jdk1.8.0_77.jdk/Contents/Home/




The above path might be different in your particular operating system. If JAVA_HOME​ is not set, set it for your particular operating system and add Java’s bin directory to the PATH​ environment variable. On macOS, or other Unix like OSs, add JAVA_HOME​ as an environment variable in your ~/.bash_profile​ .​ The .bash_profile​ is a hidden configuration file in your home directory (~​).​ If you have a new machine it might not yet exist, so you might need to create the file (touch​ )​ . From your terminal, type the following




<strong>&gt; cd ~ </strong>

<strong>&gt; touch .bash_profile </strong>

<strong>&gt; edit .bash_profile </strong>




This will open .bash_profile​ in your system text editor. Add the following line at the end your file​




export JAVA_HOME=/my/path/to/jdk/jdk1.8.0_77.jdk/Contents/Home/ export PATH=$JAVA_HOME/bin:$PATH




Where the path /my/path/to/jdk/​ will be different for your particular machine.​




On Windows, set up environment variables in the E​ nvironment Variables Control Panel

<ol>

 <li>Select S​ tart​, select C​ ontrol Panel​. Double click S​ ystem​, and select the A​ dvanced​ tab</li>

 <li>Click E​ nvironment Variables</li>

 <li>In the E​ dit System Variable (or N​ ew System Variable​) window, specify the value of the JAVA_HOME​ environment variable</li>

 <li>Edit the PATH​ environment variable and add ​ %JAVA_HOME%bin​</li>

</ol>

<h1>Setup Maven</h1>

<a href="https://maven.apache.org/">Maven</a> is a Java dependency package manager. It simplifies managing the lifecycle of projects such as downloading libraries, compiling, running automated tests, and packaging projects for deployment. Download maven from




<a href="https://maven.apache.org/download.cgi">http://maven.apache.org/download.cgi</a>




<ol>

 <li>Download the latest ZIP file version, e.g., <a href="http://mirrors.sonic.net/apache/maven/maven-3/3.5.2/binaries/apache-maven-3.5.2-bin.zip">apache-maven-3.5.2-bin.zi</a>​ <a href="http://mirrors.sonic.net/apache/maven/maven-3/3.5.2/binaries/apache-maven-3.5.2-bin.zip">p</a><a href="http://mirrors.sonic.net/apache/maven/maven-3/3.5.2/binaries/apache-maven-3.5.2-bin.zip">.</a><u>​</u></li>

 <li>On macOS, unzip to /urs/local/apache/maven/​ . On Windows, unzip to ​ /Program Files/apache/maven/​ .​</li>

 <li>Create environment variables M2_HOME​ and MAVEN_HOME​ to refer to the paths where you unzipped maven. Latest Maven documentation only mentions M2_HOME​ ,​ but older tools might still use the older environment variable MAVEN_HOME​ .​</li>

 <li>Add M2_HOME/bin​ and MAVEN_HOME/bin​ to your PATH​ environment variable so you can execute maven from the terminal or console.</li>

 <li>In a new terminal or console verify maven is installed by typing the following</li>

</ol>




<strong>&gt; mvn –version </strong>

Apache Maven 3.5.2 (r01de14724cdef16f02da; 2013-02-19 08:51:28-0500)

Maven home: /usr/local/apache-maven-3.0.5

Java version: 1.8.0_77, vendor: Oracle Corporation

Java home: /my/path/to/jdk/jdk1.8.0_77.jdk/Contents/Home/jre

Default locale: en_US, platform encoding: UTF-8

OS name: “mac os x”, version: “10.12.6”, family: “mac”




Your output might vary slightly

<h1>Create a Spring Boot Web Maven Project</h1>

<a href="https://projects.spring.io/spring-boot/">Spring</a> <a href="https://projects.spring.io/spring-boot/">Boot</a> is a preconfigured <a href="https://spring.io/">Sprin</a>​ <a href="https://spring.io/">g</a> <a href="https://spring.io/">framework</a> that allows creating Spring based Java applications with minimal effort. Spring Boot bootstraps a Spring application based on a heavily preconfigured set of default assumptions, hence the name Spring Boot. The assumptions Spring Boot makes address 80% of the needs of typical applications. Additional configuration would be needed when exploring the other 20%.

<h2>Setup Spring Tool Suite (STS)</h2>

<a href="https://spring.io/tools">Spring</a> <a href="https://spring.io/tools">T</a><a href="https://spring.io/tools">oo</a><a href="https://spring.io/tools">l</a> <a href="https://spring.io/tools">Suit</a><a href="https://spring.io/tools">e</a> <a href="https://spring.io/tools">(STS)</a> is an <a href="https://www.eclipse.org/">E</a><u>​ </u><a href="https://www.eclipse.org/">clipse</a> based IDE that has been optimized for working with <a href="https://projects.spring.io/spring-boot/">Sprin</a><u>​ </u><a href="https://projects.spring.io/spring-boot/">g</a> <a href="https://projects.spring.io/spring-boot/">Boot</a> <a href="https://projects.spring.io/spring-boot/">projects</a><a href="https://projects.spring.io/spring-boot/">.</a><u>​</u> Download STS for your operating system from




<a href="https://spring.io/tools/sts/all">https://spring.io/tools/sts/all</a>




unzip it, run the installer, and follow the installation instructions. On macOS, drag the S​ TS application icon to the Applications​ folder. On Windows, unzip to Program Files/spring​ . Run STS and accept the default configuration.​

<h2>Create a Spring Starter Project</h2>

Using STS, create a Spring Boot project. From the File menu, select New and then Spring Starter Project. Configure the project based on the name of the course, the semester term, and your last name. For instance, consider the following course, semester and last name




<ul>

 <li>Course: cs5200</li>

 <li>Semester: Spring 2018</li>

 <li>Last name: Annunziato</li>

</ul>




use the following configuration values:




<ul>

 <li>Name and Artifact: cs5200-spring2018-annunziato</li>

 <li>Group and Package: edu.northeastern.cs5200</li>

 <li>Packaging: War</li>

</ul>




Add W​ eb​, J​ PA​, and A​ pache Derby as a project dependencies and click finish. Find the path of the project folder by right clicking on the project, selecting Properties and Resources on the left, and then Location on the right. Make a note of the path since we’ll need it in a later step.

<h2>Create an HTML Index File</h2>

Once the project is created we’ll add a simple index.html​ in the webapp​ folder by right clicking the webapp​ folder, selecting N​ ew​, O​ ther​, W​ eb​, H​ TML File​, N​ ext​, and type the name of the file: index.html​ .​ Use the following content for the new index.html​ file, replacing my name with YOUR NAME:​




<table width="624">

 <tbody>

  <tr>

   <td width="624">&lt;!DOCTYPE html&gt;&lt;html&gt;&lt;head&gt;&lt;meta charset=”UTF-8″&gt;&lt;title&gt;Insert title here&lt;/title&gt;&lt;/head&gt;&lt;body&gt;<strong>&lt;h1&gt;Hello Jose Annunziato!&lt;/h1&gt; </strong>&lt;/body&gt;&lt;/html&gt;</td>

  </tr>

 </tbody>

</table>

<h2>Test Web Application Locally</h2>

Spring Boot allows to easily run a Web application locally by running a boilerplate class file that bootstraps the Spring framework and serves as the entry point of the server application. In STS, navigate to your application entry point, e.g., src/main/java/Cs5200Spring2018AnnunziatoApplication.java​        and run it as a Java Application. To run it, right click on the class, select R​ un As​, and then J​ ava Application​. This will start a local embedded Tomcat server that listens at port 8080. To test it, open a browser and point it to localhost:8080​ .​ Verify the browser displays ​Hello Jose Annunziato!, but instead of my name, YOUR NAME displays.​

<h1>Create a Spring Boot REST Controller</h1>

In later assignments we will need to access data from the server using HTTP requests. A common method of accessing data from a server is <a href="https://en.wikipedia.org/wiki/Representational_state_transfer">RES</a><u>​ </u><a href="https://en.wikipedia.org/wiki/Representational_state_transfer">T</a> <a href="https://en.wikipedia.org/wiki/Representational_state_transfer">(Representational</a> <a href="https://en.wikipedia.org/wiki/Representational_state_transfer">state</a> <a href="https://en.wikipedia.org/wiki/Representational_state_transfer">transfer)</a> which maps URL patterns and HTTP methods to server side resources. The following sections walk you through exposing different types of data by mapping HTTP request URL patterns to executable methods on the server, usually referred to as R​ EST Web service end points​.

<h2>Create a Simple REST Controller</h2>

In this section we expose a simple Java String literal as a resource available through an HTTP server request. In STS, under src/main/java​ ,​ create a new class called HelloController​   in package edu.northeastern.cs5200.controllers.hello​   .​ Use the code below as an example, but instead of my name, use YOUR NAME.




<table width="624">

 <tbody>

  <tr>

   <td width="624">package edu.northeastern.cs5200.controllers.hello; import org.springframework.web.bind.annotation.RequestMapping; import org.springframework.web.bind.annotation.RestController; @RestControllerpublic class HelloController {@RequestMapping(“}    “Hello J​            /api/hello/string​o()ose Annunziato!” {​ “)​ ;​ public String return sa​ yHell}</td>

  </tr>

 </tbody>

</table>




The code above configures the server to listen for an incoming HTTP request with the URL pattern /api/hello/string​ and maps the request to execute the sayHello()​ method. The method returns the string “Hello​ Jose Annunziato!” as an HTTP response, but instead of my name, YOUR NAME displays.

<h2>Create a Simple REST JSON Controller</h2>

A more interesting use case is to expose structured data such as Java objects of arbitrary complexity. The Java objects can implement a data model that fulfills a particular business need. As a simple example, we’ll create a HelloObject that contains just a String​ message property and expose the trivial data model as a REST HTTP request.

Create a simple POJO (Plain Old Java Object) called HelloObject​ in package edu.northeastern.cs5200​ .controllers.hello to test REST access to data on the server. Use the following code as a guide. Note the property is private and is only accessible through public setters and getters. Also note the required default constructor HelloObject().​




<table width="624">

 <tbody>

  <tr>

   <td width="624">package edu.northeastern.cs5200.controllers.hello; public class HelloObject { private String message; public String getMessage() { return message;}</td>

  </tr>

  <tr>

   <td width="624">public void setMessage(String message) { this.message = message;}public HelloObject(String message) { this.message = message;}public HelloObject() {}}</td>

  </tr>

 </tbody>

</table>




To make the above data accessible through an HTTP request (to expose), add an additional @RequestMapping​ that exposes the HelloObject​ to an HTTP request mapped to /api/hello/object​ ​. Add the bolded code below, but instead of my name, use YOUR NAME.




<table width="641">

 <tbody>

  <tr>

   <td width="641">package edu.northeastern.cs5200.controllers.hello; import org.springframework.web.bind.annotation.RequestMapping; import org.springframework.web.bind.annotation.RestController; @RestControllerpublic class HelloController {@RequestMapping(“/api/hello/string”) public String sayHello() {}        return “Hello Jose Annunziato​      !​ “;<strong>public HelloObject s</strong>​ <strong>ay</strong><strong>@RequestMapping(“HelloObjec</strong><strong><sub>t ob</sub>/api/hello/object</strong>​ <strong><sub>HelloObject()j</sub> = new HelloObject(“Hello Jose Annunziato!”);</strong>​                                      <strong> {</strong><sup>​</sup> ​<strong>“)  </strong><strong>}           return ob</strong>​ <strong>j;</strong>​}</td>

  </tr>

 </tbody>

</table>




The code above configures the server to listen for an incoming HTTP request with the URL pattern /api/hello/object​ and maps the request to execute the sayHelloObject()​ method. The method returns an instance of HelloObject​ with the message​ property set to “Hello​ Jose Annunziato!”.​ Since the method returns an object instance, instead of a litteral, the object is formatted in an HTTP friendly format such as <a href="https://www.w3.org/XML/">XM</a>​ <a href="https://www.w3.org/XML/">L</a> <a href="https://www.w3.org/XML/">(Extensible</a> <a href="https://www.w3.org/XML/">Markup</a> <a href="https://www.w3.org/XML/">Language)</a> or <a href="https://www.json.org/">JSO</a>​ <a href="https://www.json.org/">N</a> <a href="https://www.json.org/">(JavaScript</a> <a href="https://www.json.org/">Object</a> <a href="https://www.json.org/">Notation)</a>.​ Spring boot request controllers format returned objects as JSON by default. Recompile, repackage, and restart the application. Point your browser to




<a href="http://localhost:8080/api/hello/string">http://localhost:8080/api/hello/string</a>




and verify the server responds with the string Hello​ Jose Annunziato!,​ but instead of my name, YOUR NAME displays. Then point your browser to




<a href="http://localhost:8080/api/hello/object">http://localhost:8080/api/hello/object</a>




and verify the server responds with the following JSON data, but instead of my name, YOUR NAME displays




{

“message”:”Hello Jose Annunziato!”

}




Note that the JSON attribute “message​ “​ is the same as the ​HelloObject ‘s​ property “message​ “,​ and the value “Hello​ Jose Annunziato!”​ is the value we used to initialize the HelloObject​ instance. In later assignments we will be exploring much more interesting and complex data models.

<h1>Deploy a Spring Boot Web Application to AWS</h1>

Now that we have tested the Web application running locally, we’ll deploy it to a remote Tomcat server running on <a href="https://aws.amazon.com/">Amazon Web Services (AWS)</a>. Navigate and login to your AWS console​




<a href="https://aws.amazon.com/console/">https://aws.amazon.com/console/</a>




Create an <a href="https://aws.amazon.com/elasticbeanstalk/">Elasti</a>​ <a href="https://aws.amazon.com/elasticbeanstalk/">c</a> <a href="https://aws.amazon.com/elasticbeanstalk/">Beanstalk</a> service instance to deploy your Web application. Elastic Beastalk can host any number of applications built on Java, .NET, PHP, Node.js, Python, Ruby, Go, and Docker. We’ll be deploying the Java Web application we built on Spring Boot in the previous sections. Follow the steps below to deploy your Java Web application on a remote Tomcat server hosted on an AWS Elastic Beanstalk service.




<ol>

 <li>Once you’ve logged in to your AWS console, expand A​ ll services and select E​ lastic Beanstalk​. Click C​ reate New Application on the top right and name the application the same way you named it for the project, e.g., cs5200-spring2018-annunziato, and click create.​</li>

 <li>On the left, click on E​ nvironments and then C​ reate one now on the right to create a runtime environment to host the Tomcat server. In the C​ hoose an environment tier dialog choose W​ eb server environment and then Select​.</li>

 <li>In the C​ reate a new environment screen choose a public domain for your Web application. Try the same name as the name of the application. Click on C​ heck availability to see if the domain is not already taken. In the unlikely event that the domain is already taken, add a counter to the domain name to distinguish it, e.g, cs5200 -spring2018-annunziato<strong>-1</strong>​ . Scroll down and choose ​ T​ omcat​ for the P​ latform​.</li>

 <li>Down further select U​ pload your code and click on U​ pload​. Browse to the location of the WAR file in the target folder in the location of your project. You made a note of the location of your project in an earlier step. It can be retrieved by right clicking the project, selecting P​ roperties​, then R​ esources​, then L​ ocation on the right. Upload the WAR file, click create environment, and wait for the application to deploy. After a few minutes your application should have deployed.</li>

</ol>

<h2>Test Your Deployed Application</h2>




Navigate to your Website, e.g.,




<a href="http://cs5200-spring2018-annunziato.us-west-2.elasticbeanstalk.com/">http://cs5200-spring2018-annunziato.us-west-2.elasticbeanstalk.com/</a>




and verify that Hello Jose Annunziato! displays from the root index.html​ file as shown below, but instead of my name,

YOUR NAME displays.

<strong>Hello Jose Annunziato! </strong>

Then navigate to the REST controllers that returned a string and an object. Add /api/hello​ /string to the URL used in the previous step, e.g., navigate to




<a href="http://cs5200-spring2018-annunziato.us-west-2.elasticbeanstalk.com/api/hello/string">http://cs5200-spring2018-annunziato.us-west-2.elasticbeanstalk.com/api/hello/string</a>




and verify the server responds with the string Hello​ Jose Annunziato!,​ but instead of my name, YOUR NAME displays. Finally, replace string with object in the previous URL, e.g, point your browser to




<a href="http://cs5200-spring2018-annunziato.us-west-2.elasticbeanstalk.com/api/hello/object">http://cs5200-spring2018-annunziato.us-west-2.elasticbeanstalk.com/api/hello/object</a>




and verify the server responds with the following JSON data, but instead of my name, YOUR NAME displays.




{

“message”:”Hello Jose Annunziato!”

}




Submit all AWS URLs above as deliverables for this assignment, e.g.,




<a href="http://cs5200-spring2018-annunziato.us-west-2.elasticbeanstalk.com/">http://cs5200-spring2018-annunziato.us-west-2.elasticbeanstalk.com/</a>

<a href="http://cs5200-spring2018-annunziato.us-west-2.elasticbeanstalk.com/api/hello/string">http://cs5200-spring2018-annunziato.us-west-2.elasticbeanstalk.com/api/hello/string</a> <a href="http://cs5200-spring2018-annunziato.us-west-2.elasticbeanstalk.com/api/hello/object">http://cs5200-spring2018-annunziato.us-west-2.elasticbeanstalk.com/api/hello/object</a>

<h1>Commit and Push Your Code to GitHub.com</h1>

Create an account at github.com and push your code to a repository named the same as your project, e.g., cs5200-spring2018-annunziato.




<ol>

 <li>Navigate and login at github.com</li>

 <li>Click on Repositories and click on New to create a new repository</li>

 <li>Type the name of the repository in the R​ epository name​ field, e.g., cs5200-spring2018-annunziato, and click on C​ reate repository​. Several commands are shown to initialize, add, commit, and push your code.</li>

 <li>On your machine, use the terminal to navigate to your project folder and type the commands github suggests, e.g.,</li>

</ol>




<table width="674">

 <tbody>

  <tr>

   <td width="674">git init git add .git commit -m “first commit”git remote add origin https://github.com/jannunzi/cs5200-spring2018-annunziato.git git push -u origin master</td>

  </tr>

 </tbody>

</table>




<ol start="5">

 <li>Where my jannunzi above is my github username and cs5200-spring2018-annunziato is my repository. Use YOUR usename and your repository instead</li>

 <li>Submit the URL to your repository as a deliverable for this assignment, e.g.,</li>

</ol>


