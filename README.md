# Context Query Simulator for Car Park Recommendation Scenario

The rapid growth in Internet of Things (IoT) has ushered in the way for better context-awareness enabling more smarter applications. Although for the growth in the number of IoT devices, Context Management Platforms (CMPs) that integrate different domains of IoT to produce context information lacks scalability to cater to a high volume of context queries. Research in scalability and adaptation in CMPs are of significant importance due to this reason. However, there is limited methods to benchmarks and validate research in this area due to the lack of sizable sets of context queries that could simulate real-world situations, scenarios, and scenes. Commercially collected context query logs are not publicly accessible and deploying IoT devices, and context consumers in the real-world at scale is expensive and consumes a significant effort and time. Therefore, there is a need to develop a method to reliably generate and simulate context query loads that resembles real-world scenarios to test CMPs for scale. In this paper, we propose a context query simulator for the context-aware smart car parking scenario in Australia’s Melbourne Central Business District. We present the process of generating context queries using multiple real-world datasets and publicly accessible reports, followed by the context query execution process. The context query generator matches the popularity of places with the different profiles of commuters, preferences, and traffic variations to produce a dataset of context query templates containing 898,050 records. The simulator is executable over a seven-day profile which far exceeds the simulation time of any IoT system simulator. The context query generation process is also generic and context query language independent.  

![Architecture Full](https://user-images.githubusercontent.com/18043441/205787322-d10e01a7-6093-4e2d-879a-4fba4df6b109.png)

Please refer to our paper:
[1] S. Weerasinghe, A. Zaslavsky, A. Hassani, S. W. Loke, A. Medvedev, and A. Abken, ‘Context Query Simulation for Smart Carparking Scenarios in the Melbourne CDB’. arXiv, Feb. 13, 2023. Accessed: Mar. 08, 2023. [Online]. Available: http://arxiv.org/abs/2302.07190

## Despription of the dataset

| Parameter | Description | Nullable |
| --- | --- | --- |
| address | Name of the destination that the consumer intends to go to. | False |
| distance | The maximum distance from the destination that the user is willing to park the vehicle. | True |
| expected_time | The maximum time in seconds that the consumer is hoping to park (This parameter is inteded to check whether the parking facility is available for the entire time) | True |
| price | The expected price the CC intend to pay for the duration of parking. | True |
| rating | The minimum average rating expected for car parks in the response. | True | 
| vin | Vehicle identification number. | False |
| location.lat | Latitude of the context consumer at the time of query execution. | False |
| location.lng | Longitude of the context consumer at the time of query execution. | False |
| day | The specific day of the week that the context query need get executed. | False |
| hour | The specific hour of the day that the context query need get executed. | False |
| minute | The specific minute of the hour that the context query need get executed. | False |
| second | The specific second of the minute that the context query need get executed. | False |
| --- | --- | --- |

## Sample context queries from the Context Query Generator
### Sample Query 1 
`prefix schema:http//schema.org push (targetCarpark.*)
when distance(consumerCar.location, targetLocation.geo)<={“value”:500, “unit”:”m”} 
define
entity targetLocation is from schema:Place where targetLocation.name=”Melbourne Skydeck”, 
entity consumerCar is from schema:Vehicle where cosumerCar.vin=”13UNVER82367G4”,
entity targetCarpark is from schema:ParkingFacility where goodForWalking(targetWeather)>=0.6 and 
  targetCarpark.maxHeight>consumerCar.height targetCarpark.isOpen=true and targetCarpark.availableSlots>0`

### Sample Query 2
`prefix schema:http//schema.org
pull (targetCarpark.*)
define
entity targetLocation is from schema:Place where targetLocation.name=”Melbourne Skydeck”, 
entity consumerCar is from schema:Vehicle where cosumerCar.vin=”13UNVER82367G4”, 
entity taregtWeather is from schema:Thing where targetWeather.location=”Melbourne,VIC”, 
entity targetCarpark is from schema:ParkingFacility where
  ((distance(targetCarpark.location, targetLocation.geo, “walking”)<{“value”:200, “unit”:”m”} and goodForWalking(targetWeather)>=0.6) or goodForWalking(targetWeather)>0.9) and
  targetCarpark.maxHeight>consumerCar.height and targetCarpark.isOpen=true and targetCarpark.availableSlots>0 and targetCarpark.price<={“value”:20, “unit”:”aud”} and
  targetCarpark.rating>=3 and isAvailable(tagetCarpark.availableSlots, {“start_time”:now(), “end_time”:{“2020-07- 12T18:00:00”, “unit”:”datetime”}})`


