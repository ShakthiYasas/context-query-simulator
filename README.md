# context-query-simulator

The rapid growth in Internet of Things (IoT) has ushered in the way for better context-awareness enabling more smarter applications. Although for the growth in the number of IoT devices, Context Management Platforms (CMPs) that integrate different domains of IoT to produce context information lacks scalability to cater to a high volume of context queries. Research in scalability and adaptation in CMPs are of significant importance due to this reason. However, there is limited methods to benchmarks and validate research in this area due to the lack of sizable sets of context queries that could simulate real-world situations, scenarios, and scenes. Commercially collected context query logs are not publicly accessible and deploying IoT devices, and context consumers in the real-world at scale is expensive and consumes a significant effort and time. Therefore, there is a need to develop a method to reliably generate and simulate context query loads that resembles real-world scenarios to test CMPs for scale. In this paper, we propose a context query simulator for the context-aware smart car parking scenario in Australia’s Melbourne Central Business District. We present the process of generating context queries using multiple real-world datasets and publicly accessible reports, followed by the context query execution process. The context query generator matches the popularity of places with the different profiles of commuters, preferences, and traffic variations to produce a dataset of context query templates containing 898,050 records. The simulator is executable over a seven-day profile which far exceeds the simulation time of any IoT system simulator. The context query generation process is also generic and context query language independent.  

![Archi](https://user-images.githubusercontent.com/18043441/205786210-a339c33e-6880-4481-a435-934fa73bb72b.png)

Please refer to "Context Query Simulation for Smart Carparking Scenarios in the Melbourne CDB" by S.Weerasinghe, A. Zaslavsky, A. Hassani, Seng W. Loke, A. Medvedev, & A. Abken for research specifications : https://www.researchgate.net/publication/364349274_Context_Query_Simulation_for_Smart_Carparking_Scenarios_in_the_Melbourne_CDB.
