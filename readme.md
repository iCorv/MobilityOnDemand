# Mobility-On-Demand
1. Problem Scope
    -   users create an account with personal data: name, gender, and age
    -   a range of different car models is part of the fleet
    -   car details: regarding the model, the engine, the infotainment system, the interior design, and the current location
    -   user demand details: pick-up and the drop-off location, the earliest pick-up and the latest drop-off time, and the desired car features

2. Assumptions
    -   users have to add billing information for payment
    -   users have to verify as a licensed driver, in case human intervention is necessary or car is not self driving
    -   mobile and web application for users to place a demand
    -   some kind of telematic services to connect cars, users and backend
    -   cars support some kind of black-box, logging and communicating their position, state (e.g. on/off/driving), reservations
    -   users may want to specify favorite car types
    -   one or more car brands could be part of the service
 
3. Major Components
    -   Identity and access 
    -   Service 
    -   User profile 
    -   Billing 
    -   Static car 
    -   Dynamic car 
    
4. Key Issues
    -   demand will vary a lot during the day -> load balancing
    -   when not used, cars are turned off, but some functionality must persist -> battery/energy management is crucial
    
## Task 1
![alt text](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 1")

## Task 2
### Requirements
1. Cars
    -   adding and removing cars
    -   changing the car details
    -   update the current location of the car independently
2. Users
    -   adding and removing users
    -   changing the user details
3. Demand
    -   adding and removing demands
    -   changing demand details

### Idea
Data could be represented in XML. This has a few advantages:
-   It can be easily read by machines and humans
-   most languages have libraries to parse XML files
-   adding new data is easy
-   it is possible to use existing backup tools

Disadvantages may include:
-   we always send all data on one subject (e.g. Car) when distributing XML files. That might be inefficient.
-   a query on the data means always parsing the entire file

A user profiles XML-file might look like this:
```xml
<root>
    <user id="230987236"> 
        <name>"Homer Simpson"</name> 
        <gender>"male"</gender> 
        <age>45</age> 
    </user>
    <user id="082347945"> 
        <name>"Marge Simpson"</name> 
        <gender>"female"</gender> 
        <age>42</age> 
    </user>
</root>
```

## Task 3
The schedule service could use an execution queue to work through the demands from the database. 
1. Cars have to be identified that are in a certain range to the user
2. Query if these cars meet the desired features (pick-up and drop-off locations as well as the earliest pick-up and drop-off times)
3. Present query results. Advise which features have to be changed in case the schedule could not be met.

Minimization of covered distance by each car, this is a typical "traveling salesman" problem. Possible helpful algorithm could be the A*-Algorithm or the Dijkstra-Algorithm for finding a shortest path in a Graph representation of the coordinate system..

Pick-up and drop-off times are part of the total trip time, e.g. trip_time = pick_up_latency + transit_latency + drop_off_latency. Where the pick_up_latency = walking_time + wait_time and drop_off_latency = walking_time_to_destination.

## Task 4
For testing the system I first try to answer these questions: 
1. Who will use it? And why?
2. What are the use cases? Make a list.
3. What are the bounds of use?
4. What are the stress conditions or failure conditions?

Testing functions using different types of test cases:
-   Normal cases of use
-   The extremes of use (e.g. empty array)
-   Illegal input like "Null"



