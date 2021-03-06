# PIXEL OT Documentation Page 



---

## Overview
<div align="justify">

This documentation explores in detail the PIXEL Operational Tools as one of the main components of the PIXEL architecture. To access the main documentation repository of PIXEL, click [here](https://pixel-ports.readthedocs.io/en/latest/). To access the PIXEL project website, click [here](https://pixel-ports.eu/).

> *PIXEL is the first smart, flexible and scalable solution for reducing environmental impacts while enabling the optimization of operations in port ecosystems through IoT.*

PIXEL enables a two-way collaboration of ports, multimodal transport agents and cities for **optimal use of internal and external resources, sustainable economic growth and environmental impact mitigation, towards the Ports of the Future**. Built on top of the state-of-the art interoperability technologies, PIXEL centralises data from the different information silos where internal and external stakeholders store their operational information. PIXEL leverages an **IoT based communication infrastructure** to voluntarily exchange data among ports and stakeholders to achieve an efficient use of resources in ports.

PIXEL has been financed by the **Horizon 2020 initiative** of the European Commission, contract 769355.  
</div>
<br/><br/>


## Main concepts and Architecture
<div align="justify">

The Operational Tools (OT) are mainly in charge of bringing closer to the user both the **models and predictive algorithms** developed within the PIXEL project. By user here we mean administrators and managers analysing port operations by means of **simulation models and predictive algorithms**. In order to reach that goal, a set of high-level tasks are defined: 

   - **Publish** models and/or predictive algorithms
   - **Edit** and **configure** the models and/or predictive algorithms
   - **Execute** models and/or predictive algorithms
   - **Schedule** models and/or predictive algorithms to be executed at a **specific time** once or **periodically**
   - **Define** different operational and environmental **Key Performance Indicators (KPIs)**, based on specific data available in the information hub for **tracking and monitoring** purposes
   - Establish some **pattern detection** mechanism. The most basic one is the use of **triggers**. 
   - Get the **trends** of a model and/or predictive algorithm (e.g. historical data)

<p align="center">
<img src="img/ot_main_concept.JPG" alt="PIXEL OT diagram" align="center" />
</p>

The functional overview of the Operational Tools is depicted in the Figure below. Several internal components can be identified:

   - **OT UI**: this is the graphical interface to access (most of) the underlying functionalities. This component provides independence and autonomy, but it can be later integrated as part of the **PIXEL dashboard** to provide a single-entry point for administrators
   - **OT API**: backend API implementing the functionalities needed. This component is aligned with **PIXEL security framework** in order to fulfil all required security policies (e.g. authentication, authorization, etc.)
   - **Publication component**: it allows publishing both models and predictive algorithms. By publishing it may be necessary to deploy the models as **Docker containers**. Besides, the models ‘and predictive algorithms’ configurations can also be edited.
   - **Engine**: this component is responsible for **executing** the different models and predictive algorithms. The execution can be invoked in **real time** or **scheduled**.
   - **Data processing**: it is responsible for managing **trends** from specific data (KPIs) and also for some **internal data adaptations** required.
   - **Event processing**: this component is responsible for **real-time monitoring of indicators** and trigger specific actions depending on previously configured rules. It includes a connector (bridge) to be integrated with an external **notification system**.
   - **Database**: the database includes description of the models and predictive algorithms that can be used, KPI description, rules as well as other configuration and output related parameters necessary for the correct behaviour of the internal building blocks.

<p align="center">
<img src="img/ot_arch.JPG" alt="PIXEL OT diagram" align="center" />
</p>

<br/><br/>

</div>


## Models
<div align="justify">
   
Models are entities in the PIXEL platform than will be used by port administrators to run and simulate models and predictive algorithms with different input parameters. As every model and predictive algorithm is different from each other and has its own internals, there is a need to homogenize a common abstract model entity to be the internal representation in the PIXEL platform. It encompasses two different types of developments that have been done within the PIXEL project:

   - **Models**: models relate to energy, traffic and environment. A specific model is the Port Environmental Index (PEI). For more information about the models, please check the **PIXEL main documentation repository** by clicking [here](https://pixel-ports.readthedocs.io/en/latest/).
   - **Predictive algorithms**: predictive algorithms relate to estimating time of arrival in ports, traffic at gates and use of AIS data. For more information about the models, please check the **PIXEL main documentation repository** by clicking [here](https://pixel-ports.readthedocs.io/en/latest/).

The Figure below shows the process experienced by any model or predictive algorithm that is going to be used inside the PIXEL platform:

- The model or predictive algorithm is first drafted as algorithm and **implemented as program**.
- The model is encapsulated into a **Docker container** to convert it into a portable component. Additionally, an OT adaptor is attached to his Docker container in order to be integrated into the PIXEL platform.
- Through the **publication process** the model or predictive algorithm becomes aware into the PIXEL platform. The **Docker image** is pulled from the (open) GitHub repository and can be used internally.
- After published, the model or predictive algorithm can be **executed** by passing the appropriate arguments (parameters) as JSON file. The description of this JSON file will be described in future sections. The execution can **run immediately** (real time) or it can be **scheduled** to be performed periodically (e.g. every day or week).
- The **results** of the model are stored into the **PIXEL Information Hub**, which can be queried by the **PIXEL dashboard** to visualize them in form of particular graphs depending on the model or predictive algorithm. 

<p align="center">
<img src="img/ot_models.jpg" alt="PIXEL model flow" align="center" />
</p>

<br/><br/>

</div>

## KPIs
<div align="justify">
   
According to [Wikipedia](https://en.wikipedia.org/wiki/Performance_indicator) a **Key Performance Indicator (KPI)** is a type of performance measurement. KPIs evaluate the success of an organization or of a particular activity in which it engages. For the PIXEL project, we envision that basic KPIs will mostly refer to:

   - **Sensors**: the PIXEL platform encompasses an IoT network and can therefore monitor any integrated sensor. Some of the sensors may represent an important impact on the decision made from port authorities (e.g. depending on the tide level or the wind speed some cargo type is not recommended to be loaded/unloaded). 
   - **Models and Predictive algorithms**: models and predictive algorithms are typically complex and provide various different outputs; however, some specific items of the output can be  considered of crucial importance and be characterized as KPIs.

More complex KPIs can be potentially defined by combining previous ones, but there is a need to define a common format for them as data entity. PIXEL has followed the **FIWARE Data Model**, which specification can be accessed [here](https://fiware-datamodels.readthedocs.io/en/latest/KeyPerformanceIndicator/doc/spec/index.html). Some extensions have been added, when needed, to particularize it to port and model needs (e.g. environmental KPIs for the PEI calculation). You can find more information on the main documentation repository of PIXEL, clicking [here](https://pixel-ports.readthedocs.io/en/latest/), as there is a section dedicated to Data Models.

<p align="center">
<img src="img/ot_kpis.jpg" alt="PIXEL KPIs" align="center" />
</p>

<br/><br/>

</div>

## Event Processing
<div align="justify">
   
According to [Wikipedia](https://en.wikipedia.org/wiki/Complex_event_processing) a **Event Processing** is a method of tracking and analysing (processing) streams of information (data) about things that happen (events), and deriving a conclusion from them. **Complex event processing**, or CEP, consists of a set of concepts and techniques developed in the early 1990s for processing real-time events and extracting information from event streams as they arrive. The goal of complex event processing is to identify meaningful events (such as opportunities or threats) in real-time situations and respond to them as quickly as possible.

Considering that the PIXEL platform uses as main database **Elasticsearch**, the selected and natural choice as CEP engine refers to **ElastAlert**. You can find detailed information about ElastAlert by clicking [here](https://elastalert.readthedocs.io/en/latest/elastalert.html#overview). Some of its main features are reliability, modularity and easiness to set up and configure.

From the perspective of the **Operational Tools**, and considering the current needs of the target ports, this will mainly be related to **monitored KPIs** where some **threshold**s are reached. For these situations, **rules and alerts** are 'templatized' to facilitate the configuration to port operators and define proper actions. More complex actions are possible and supported through ElastAlert; this will be commented in the **Developer's Guide** subsection, explaining possible extensions.
 

<p align="center">
<img src="img/ot_cep.jpg" alt="PIXEL KPIs" align="center" />
</p>

<br/><br/>

</div>



 
