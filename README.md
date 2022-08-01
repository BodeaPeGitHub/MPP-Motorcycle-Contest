# MPP - Motorcycle Contest is a project made for the MPP Course

## The problem

The organizers of a motorcycling contest use a software system to manage the registration of participants in the contest.   
The people at the enrollment offices use a desktop application with the following functionalities:
1. Log in. After successful login, a new window opens showing the available races according to the engine capacity (125mc, 250mc, etc.) and the number of participants already registered for each race.
2. Search. After successfully logging in, the office person can search for all participants belonging to a specific team (eg Suzuki, Honda, etc.). The application displays in another list/table all participants (participant name and engine capacity).
3. Sign up. The person can register new participants. When registering a new participant, select the engine capacity, and enter the name of the participant and the team he belongs to (if any). After registering, all people from other offices see the updated list of races and the number of participants registered for each race.
4. Sign out.  

The final project is divided into 3 distinct parts, one in Java, another in C# and the last one in React.js, which are detailed below.

## The solution

### The Java part

The Java project is mainly the application server, it manages the database, creates and saves the 3 basic entities `Participant`, `Race` and `User`.
The project is managed with the help of [Gradle](https://docs.gradle.org/current/userguide/what_is_gradle.html) (a build automation tool) which deals with 
building, solving dependencies and running only the important parts of the project.
To map the entities in the database, I used [Hibernate](https://hibernate.org/) for 2 of them, and on the 3rd one, I implemented the functions.  
3 ways of communication with clients are implemented in the server:
* [gRPC](https://grpc.io/) for client communication in C#.
* [Rest protocol](https://www.techtarget.com/searchapparchitecture/definition/REST-REpresentational-State-Transfer) for communicating with the 
ReactJS client, which is used by the Spring framework to start the Rest server.
* [RPC protocol](https://duckduckgo.com/?t=ffab&q=rpc+protcol&atb=v301-1&ia=web) implemented without frameworks that communicates with the 
client in Java, where an [ActiveMQ](https://activemq.apache.org/) message broker is also used to implement the observer between client and server.

### The C# part

The client in C# is a client with a desktop interface in which, after authentication, two lists are displayed.  
A list of all the races taking place, and if a list is selected, the 2nd list displays the participants of the respective race.  
The lists are kept up to date for each client and if a new participant appears, they are updated for each client.  

### The ReactJS part

The ReactJS client is the web client of the application and uses only REST calls to communicate with the 
client and only manages the racing part.  
The client is in the beginning phase, that is, it has a very simple interface, 
it does not have a log in, but only a list of races and the possibility to delete or edit one of them.

![alt text](/screenshots/reactJS-App.png)

## Observations

* The C# project also has the server part implemented that can communicate with the C# client, 
but it is not implemented to communicate with the Java client. 

