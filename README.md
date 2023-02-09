# Analysis of Canada’s Energy Pipelines

#### _A Data Analysis Project using Python scikit and mlxtend, SQL SSMS, Visual Studio SSIS, and PowerBI_

_This is the Capstone project submitted as part of the degree requirements for the Southern Alberta Institute of Technology SAIT’s Diploma program in Data Analytics._

This project analyzes 13 years (2008-2021) of data on Canada Energy Regulators CER regulated pipelines incident occurrence, capacity, and throughput information, with the aim to identify safety deficiencies and risks in energy pipelines transportation systems.
The analysis is divided into **different stages**, starting with the _Business understanding, Business Modeling tools, Data Understanding, Data Preparation through ETL, SQL SSMS, SSIS, Modelling, Evaluation, and Recommendations._

## Business Understanding
Data is one of the most important resource any business or industry can have, and when collected and interpreted correctly, can provide valuable insights to the business.
However, this can only start from understanding the business industry, be it domain of Oil & Gas, Health care, Retail, Finance, Engineering, Transportation etc. Without understanding the business or industry in question, it is almost impossible to have a data understanding, and if you can not make sense of your data, then you cannot ask your data questions.
Canada Energy Regulator (CER) is Canada’s independent national energy regulator. They work to keep energy moving safely across the country. 

The CER regulates Oil & Gas Pipelines, Electricity Transmission, Imports, Exports & Energy Markets, Offshore Exploration & production, and Offshore renewables. They interface with Stakeholders including Transportation Safety Board of Canada (TSB), Natural Resources Canada, Environmental and climate change Canada, Federal and Provincial governments, Provincial Regulators, Oil & Gas Production Companies, Pipeline operating companies, and the Canadian public.
The Analysis focus on Crude Oil & Natural Gas Pipelines. There are an estimated 840,000 km of pipelines in Canada. CER regulates only inter provincial and international pipelines, and these account for about 68,000 km, and they are owned by 98 Pipeline Operating companies (POC)

A Pipeline Lifecycle goes through the Application, Construction, Operations, and finally Abandonment. Therefore, the CER collect Data on Pipeline infrastructure, Flow & Capacity utilization, Incidents, Tolls & Tariffs economics, and Financial strength (including incident and abandonment funding) of the pipeline operating companies.

The objectives of the project are:

•	Acquire a business understanding of CER and how they collect and analyse data through the lifecycle of pipelines 

•	Collate, explore, and acquire understanding of the datasets on pipelines incidents and capacities.

•	Perform Extract, Transform and Load of the datasets using Microsoft Excel, SQL Server Management Studio, and Visual Studio SSIS. 

•	Carry out exploratory data analysis on the datasets, and report on incidents, serious injuries, fatalities, utilization. How they vary by year, pipeline operating company, and/or province.

•	Perform association mining to identify frequent itemsets of the reasons (what and why) incidents happen. 

## Business Modeling
5W and 1H was used to explore the business modelling. 

**Who** are the stakeholders, who is involved, who can benefit?

**What** is the topic, and the different parts to the topic. What might get affected?

**When**does this take place?

**Where** does this occur. Is it location specific? Or affected by a location?

**Why** is the topic important, the benefits that can be derived, the problem that can be solved by the topic

**How** does the analysis work?


The business questions derived and answered by the analysis are:

Question 1: What were the top causes of pipeline incidents in 2021?

Question 1.1: Which pipeline companies contributed the most to these incidents?

Question 2: What is the average utilization of CER regulated pipelines in 2017-2021?

Question 2.2: Is there a relationship between pipeline utilization and incidents?


## Data Understanding

One of the critical stages of any Data analysis project is understanding the available data, and the relationships that exists between the various business concepts. The datasets provides details on safety, performance, and economics indicators. It lists the different pipeline companies, province, incidents categories, fatality & injury, product released or spilled, what happened, why it happened, and the capacity and throughput information.
The Datasets were obtained [here](https://www.cer-rec.gc.ca/en/safety-environment/industry-performance/interactive-pipeline/incident-data.html) and [here](https://www.tsb.gc.ca/eng/stats/pipeline/data-2.html). 


A data dictionary was created to explain the attributes definition in the dataset.


## Data Preparation

This stage involved Data Extraction, Transformation and Load **(ETL)**, SSMS and SSIS tools. Steps carried here include data wrangling and manipulation, use of SQL Server Import and Export Wizard to load the dataset into SQL Server management studio **(SSMS)**, and use of Visual studio integration services **(SSIS)** to create a Dimensional model with Dimensions and Facts, and integrate into a relational database in SSMS.

![SSIS](https://user-images.githubusercontent.com/114383545/217680400-417a2398-4e93-4436-860c-fad9ae5d2e46.png)

In **SSMS**, I set the Primary key **(PK)** column for each Dimension table, telling the software which column to use as PK. Next, I defined the relationships between each Dimension table PK and corresponding Foreign Key in my Fact table. Afterwards the star schema database diagram was generated.

![star schemma](https://user-images.githubusercontent.com/114383545/217680469-25e37699-19ca-4ffd-9772-c418652d8e37.png)

## Association Mining

Python library mlxtend was used create a model to determine frequent itemsets of immediate causes of pipeline incidents. I added a categorical column for pipeline name to see if some incident causes occurring together are particular to some companies. Minimum support was calculated by first determining the minimum support of each attribute, and setting a minimum support to be less than the maximum. It is good practice to try various minimum support values, and results compared.

![am min support](https://user-images.githubusercontent.com/114383545/217680545-b5e2282b-a2a7-4e31-bbf3-1a12eab0626c.png)

With a min support of 0.05, the frequent itemset was 23 with their respective support. Support for an item is the number of transactions containing that item divided by total number of transactions. For this 0.05 minimum support, the maximum number of frequent itemset occurring together its 2 and it occurred 10 times. 

![frequent itemsets](https://user-images.githubusercontent.com/114383545/217680645-6c57cb03-fe26-4e3d-b115-69c969d528ff.png)

The association rules were sorted by confidence, and it is showing the top 10. From the model, incorrect operation as a cause of an incident usually goes hand in hand with external interference. And Enbridge mainline pipeline seem to have correlation with defects and deterioration, perhaps their maintenance strategy is not so great.

![association rules](https://user-images.githubusercontent.com/114383545/217680724-90fdf6a6-845b-4705-a93b-3b43dff4bf1a.png)

The scatter plot just shows the plot of support vs confidence of the association rule. We can see that majority have confidence between 0.2 and 0.4.

![scatter plot](https://user-images.githubusercontent.com/114383545/217680798-54344640-3743-40ff-b867-5d3351f549eb.png)

## Visualization

### Incident Numbers Dashboard

•	The incident numbers dashboard shows total number of pipeline incidents that have occurred in CER regulated pipelines in the last 13 years (1,323). 

•	The year 2010 had the highest occurrence at 175, and incidents dropped till year 2017 when there was a sharp increase to 134. However, in subsequent years after 2017, the number ramped down, although it has started increasing again in year 2021. 

•	In the 13 years data, year 2019 was a good year with the least number of incidents (16).

![dasboard](https://user-images.githubusercontent.com/114383545/217680896-b6aa965a-e8c5-4884-a5f6-38a621d0ce93.png)


### Description Dashboard

•	For the descriptive visuals, the pie chart show that about 52% of incidents occurred in a facility, 39% in a pipeline, and 8% in an infrastructure made up of a facility and pipeline. 

•	The column chart show that most of the pipeline incidents occurred at pump stations (232), with the least occurring at Receipt/Delivery facilities. Compressor stations accounted for 149 incidents, while gas processing plants contributed to 106 occurrences.

•	571 incidents occurred in transmission lines, which is not surprising because transmission lines  from one province to another predominantly make up most of CER regulated pipelines

•	The pie chart on the components of the pipeline or facility system where these incidents occurred shows only the top 5 contributor, with the pipe accounting for 369 incidents, and flange/fitting contributing to 25 incidents.


![descriptive](https://user-images.githubusercontent.com/114383545/217680942-5bc26c58-bd28-4e65-9956-71b49590cc51.png)


### Incident Type Dashboard

•	For an occurrence to be classified as an incident, it must meet certain criteria, and this include release of substance, Fire, Explosion, Serious injury, Fatality, Rupture, Operation of the pipeline beyond its design limits, and contributing to Adverse environmental conditions. The incident type dashboard gives statistics based on these categories. 

•	Substance (which can either be Crude oil or natural gas) was released in 826 of the incidents that occurred. 

•	The pie chart show percentage of true to false of each category. 


![incident type](https://user-images.githubusercontent.com/114383545/217681033-3eeb1c66-16ac-4c12-938f-3c7547e8d8d6.png)


### Incident Type Details 

•	The incident type details visual show the type and source of the incident categories discussed above. Of the 826 released substance incidents, 530 was natural gas, and 170 was crude oil spills.

•	The column chart shows the categories that served as a source of fire and explosion in the pipeline incidents. In both instance, equipment and electrical fault was the highest contributor accounting for 128 incidents out of the 387 incidents caused by fire, and 7 out of the 38 explosion incidents.


![incident type details](https://user-images.githubusercontent.com/114383545/217681108-e9d61995-57e0-4ce9-b21b-5b308ce5a7d8.png)



### Injury & Fatality Dashboard

•	The injury and fatality dashboard shows that 32 fatality has occurred since 2008, and 83 persons have been injured.

•	The column chart that details the nature of the injuries shows 21 had fracture while 16 lost consciousness.

•	Out of the 32 fatalities, 14 was as a result of pipeline construction activities.


![fatality and injury](https://user-images.githubusercontent.com/114383545/217681156-51231fd3-b46c-4399-994a-86f9e3301655.png)


### What Happened?

•	The what happened dashboard shows the immediate cause of the pipeline incident. The pie chart are percentage of false to true.  

•	35% of the all pipeline incident was due to equipment failure. It accounted for 465 cases.

![what happened](https://user-images.githubusercontent.com/114383545/217681233-de9134a8-f143-4669-a55e-b6d8b8433fa0.png)



### Why it Happened?

•	The why it happened dashboard shows the underlying cause, after an investigation was carried out.

•	Maintenance was the why behind 613 incidents that occurred, and this accounted for almost 50% of the total number of pipeline incidents between 2008 – 2021. 



![why it happened](https://user-images.githubusercontent.com/114383545/217681273-d411709a-fc3d-4ac9-a08a-506dd0e57549.png)


### Capacity & Throughput Dashboard

•	The capacity dashboard gives the pipeline throughput and capacity flow values. Key point location on the pipeline route can be selected to see the details of the throughput information at that point of interest.

•	The graph on pipeline throughput by month shows that there is a drop between April and October which corresponds to the summer months when the demand for natural gas drops, at least domestically

•	The graph of capacity vs throughput is plotted for all pipelines, although a particular pipeline can be selected. 

•	The throughput for each year is approximately less than 50%, meaning that cumulative the pipelines were not utilized up to 50% of their capacities. Energy products (Crude oil & Natural Gas) transported was less than half of what the pipeline was designed to carry. 

•	Some pipelines did better than others. For instance alliance pipeline is flowing close to its designed capacity. 

![capacity](https://user-images.githubusercontent.com/114383545/217681316-18a1d0d7-70ee-4fb0-bca4-6f64ba93df86.png)


## Business Questions Deep Dive 

•	For business question 1, there were a total of 46 pipeline incidents in 2021, and Equipment Failure was the top contributing cause, accounting for 13 out of the 46 incidents.

•	Equipment failure is A failure of the pipeline’s equipment components. It could be maybe the valves, electrical power systems or control systems

•	The next contributor to 2021 incident statistics is Corrosion and Cracking (6), External Interference (6), and Defect and Deterioration as a cause contributed to 4 incidents.


•	Trans Mountain pipeline company contributed the most to 2021 occurrences, with 18 incidents. The top 5 contributing companies for 2021 are Trans Mountain, Twin Rivers, Enbridge Mainline, NGTL, and Enbridge BC


![bq 1](https://user-images.githubusercontent.com/114383545/217681352-c6ce248a-fd4f-4146-a290-c04a8746218b.png)



•	For business question 2, the gauge visual shows that the average utilization for of the CER regulated pipelines for 2017-2021, and it is a little less than 50% cumulatively.

•	However, the bar charts show the statistics for each of the different pipelines, and the results show that some individual pipelines have better utilizations even > 70%. 

•	For instance the Alliance pipeline averaged 84% for the 5 years and Cochin and NGTL averaged 76% each 

•	There does not seem to be a relationship between pipeline utilization and incidents.

•	Considering the last 5 years, 2017 had lowest utilization with highest incidence, while 2019 had the least incidents.

•	This means that an increase in pipeline accidents cannot be linked to 'overuse' of the pipelines. 

•	Alternatively, it may be inferred that in 2017 due to the high number of incidents, some pipelines were not available for use during the year, thereby leading to an overall low utilization.

•	Both Alliance and Cochin pipelines had utilization above 70%, and yet it did not record as part of the Top 5 operating companies contributing to pipeline incidents for 2021. 

![bq 2](https://user-images.githubusercontent.com/114383545/217681431-3aa57aa2-acf7-40cc-86f1-b8975a020e3f.png)



## Observation & Insights

•	Number of incidents was high in year 2008 to 2010 (average of 161), and this dropped between 2011 to 2014 (average of 91). 

•	However, there was a large increase in incident in year 2017 (134). The values drooped to a 13-year low in year 2019 (16 incidents only).

•	There are 9 categories based on which a pipeline incident is classified. Released substance incidents had the highest occurrence in the dataset at 64%, while Rupture had the lowest occurrence at <2%.

•	Natural gas release was twice that of crude oil accounting for 530 incidents cumulatively.

•	Major sources of fire and explosion incidents was attributed to equipment and electrical malfunction.

•	In the 13 years, number of fatalities due to pipeline occurrence stands at 32, while those injured is 83. 

•	Out of this the most reported injury type was fracture, followed by loss of consciousness.

•	Equipment Failure was identified as the main cause of incidents. 

•	This accounted for >35% of occurrence and was a frequent itemset in the association mining solution.

•	 It was the top cause in the 13-year dataset, and also in year 2021.

•	The underlying reason why it happened was due to maintenance, and this happened 613 times.

•	The association mining show that the consequent External Interference, Incorrect Operations, and Equipment Failure usually go hand in hand with a fatality and/or injury.

•	Cumulatively the utilization of CER pipelines is less than 50%, however some individual pipelines have utilization percentages >70% (Alliance, Cochin, and NGTL.)

•	The utilization ratio of pipelines usually shows a drop between April and September. This is expected because gas utilization is lower in summer months.

•	No relationship exists between pipeline utilization and incidents. 

•	Considering the last 5 years, 2017 had lowest utilization with highest incidence, while 2019 had the least incidents.

•	This means that an increase in pipeline accidents cannot be linked to 'overuse' of the pipelines. 

•	Alternatively, it may be inferred that in 2017 due to the high number of incidents, some pipelines were not available for use during the year, thereby leading to an overall low utilization.

## Recommendation

•	CER can use the result of this analysis to:

	Update policies, regulations, standards, and procedures 

	Create and enforce a rewards/ penalty system for companies who adhere/default respectively.

	Deploy more CER staffs and increase frequency of inspections to problematic operators and pipelines such as those who contribute the highest to pipeline occurrences.

	Develop and implement safety trainings

	Prepare for emergency response

	Update incident funding required by pipeline operating companies. If a pipeline company is constantly known for contributing to incidents, then regulations that stipulates the amount of money to be kept aside for incident funding should be updated with the higher amount allocated to the defaulters.

•	Specifically, Companies such as Enbridge BC, Enbridge Mainline, and NGTL that occur as frequent itemsets to incident causes such as incorrect operations, and external interference, could be targeted for safety interventions to ensure that pipeline incidents at their operations are reduced or eliminated.

## Conclusion

•	Data is a high value resource that can be used as basis to develop new policies, update existing ones, and make proactive decisions that can contribute to a business bottom line.

•	However, to be able to make meaningful use of data, the integrity of data collection must be clearly governed, as well as the storage and sharing formats.

•	Therefore, the CER can collaborate with TSB (who collects data on pipeline incidents as well) to standardize the data collection process and ensure any future analysis on the subject is based on quality information.

•	In addition, CER should consider adding near misses to increase the data size.


