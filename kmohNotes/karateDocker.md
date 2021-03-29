<h1>Changes that need to be made in Virtual Box - Kali machine settings<h1>

• Start Oracle-Virtual Box
• Select Kali Machine
•  Click on settings
• Click on network
• Change to Bridged Adapter
• Click advanced and change Promiscuous mode to Allow All
• Click ok
• Start Kali

**To start docker daemon on kali after restart**
systemctl start docker 
*Pasted from <https://stackoverflow.com/questions/44678725/cannot-connect-to-the-docker-daemon-at-unix-var-run-docker-sock-is-the-docker>*
	
Or try sudo dockerd

https://github.com/intuit/karate/tree/develop/examples/jobserver
  
https://github.com/intuit/karate/tree/develop/examples/jobserver .git


Step 1
Check if docker is isntalled
docker -v

Step 2 - If this is done earlier skip this step
docker pull ptrthomas/karate-chrome

Step 3
In a terminal, change to the root of the jobserver project  

docker run --name karate --rm -p 5900:5900 --cap-add=SYS_ADMIN -v "$PWD":/src ptrthomas/karate-chrome  
Leave this hanging

docker run --name karate --rm -p 9222:9222 -p 5900:5900 -e KARATE_SOCAT_START=true --cap-add=SYS_ADMIN ptrthomas/karate-chrome


**Karate-Chrome**
open vnc://localhost:5900
(password: karate)  

Step 5
In another terminal, change to the root of the jobserver project  
docker exec -it -w /src karate mvn clean test -DargLine='-Dkarate.env=docker' -Dtest=WebRunner 

*Jobserver project has 2 types of runners*
• First is a SimpleRunner which has simple tests that prints some values
• and WebRunner where tests are run on chrome
• In the above command u need to mentione which runner you wish to run agains the -Dtest command


**Chrome Remote Debug  **
• along with -p 5900:5900, add -p 9222:9222 -e KARATE_SOCAT_START=true to the first docker command that starts the container with Chrome in it
docker run --name karate --rm -p 5900:5900 --cap-add=SYS_ADMIN -v "$PWD":/src -p 9222:9222 -e KARATE_SOCAT_START=true ptrthomas/karate-chrome
• open Chrome on your host machine and navigate to http://localhost:9222
• you should see Inspectable Pages, click on the first one
• TA DA ! you will now see a mirrored view of the Chrome instance running inside Docker. The great thing is that you can use the whole set of developer tools on your host machine, instead of struggling with the limited capabilities of a VNC remote connection.
 
**reading materia**l
https://github.com/intuit/karate/tree/develop/karate-core#karate-chrome  

Karate-Gatling
In another terminal, change to the root of the Karate-Gatling project  
docker exec -it -w /src karate mvn clean test

Reprot is generated in 
target/gatling/catskaratesimulation../index.html
 
