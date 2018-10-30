# assignment

## Requirement
 1. Java 1.8
 2. Gradle : https://docs.gradle.org/current/userguide/installation.html

## Ide setup
Currently it is setup for intellij idea.
However once gradle is setup. User can run `gradle eclipse`

## Steps to run

 ### One way
  Go to directory where this readme.md reside 
  1. gradle build
  2. gradle bootRun
  
  * Make sure gradle is install and in path

 ###
  Go to dist/
   java -jar swiggy-0.0.1-SNAPSHOT.jar 
 
## Health check

* Once app is up health of app can be checked http://localhost:8080/actuator/health

## DB

App has inmemory H2 db which start when application starts. Data is inserted ~/src/main/java/com/swiggy/SwiggyApplication.java everytime app starts.

## Structure

Assignment uses spring boot structure with following layer
1. com.swiggy.rest.api 
* controller -> code to service /restraunt api with parameter locationId and customerId. Only one GET API is implemented with the cases requested.
* service -> layer to read data from repository and do discounting and time slot identification

2. com.swiggy.persistance
* entity -> object to load db data into
* repository -> layer loading data into object (queries are written here)

3. com.swiggy.model
* model -> Domain/Json model used by rest api to serialize into json.


## Example

http://localhost:8080/restaurant?customerId=1&locationId=1

**  both customerId and locationId are required field. (customerId can be any value, sample data has following locationId = 1,2,3,4,5)

**  if run from 11PM to 6AM api will return "We are closed. We will open next at 6AM"

http://localhost:8080/restaurant?customerId=1&locationId=1&ad=true

** will return the retraunt in orderd list of low to high timeToPrepFood. (Further id restraunt has paid for advertisment in that slot, it will be ordered as timeToPrepFood is 5 min less than actual value)

http://localhost:8080/restaurant?customerId=1&locationId=1&super=true

** will discount the price for restaurant by 10%





