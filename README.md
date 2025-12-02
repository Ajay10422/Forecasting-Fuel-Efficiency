# Cloud-Native Fuel Efficiency Platform (Azure & Snowflake)

![Azure](https://img.shields.io/badge/Azure-ADLS%20Gen2-0078D4?logo=microsoft-azure&logoColor=white)
![Snowflake](https://img.shields.io/badge/Snowflake-Data%20Warehouse-29B5E8?logo=snowflake&logoColor=white)
![Airflow](https://img.shields.io/badge/Apache%20Airflow-Orchestration-017CEE?logo=apache-airflow&logoColor=white)
![Python](https://img.shields.io/badge/Python-FastAPI-3776AB?logo=python&logoColor=white)

## 📌 Project Overview
This repository hosts a production-grade **Cloud Data Engineering Platform** designed to process large-scale government fuel datasets. It extends the Canadian EnerGuide system by replacing static CSV analysis with a scalable **ETL Pipeline** on Azure.

The system orchestrates data movement from **Azure Data Lake Storage (ADLS Gen2)** into **Snowflake** using **Snowpipe** for near real-time ingestion, enabling downstream ML models to forecast carbon tax impacts.

### 🟢 Live Demo
**[[Launch Forecasting Dashboard](https://dashboard-5p9c.onrender.com/)](https://forecasting-fuel-efficiency-4.onrender.com/)]]**

---

## 🏗️ Enterprise Data Architecture
The pipeline follows a **Modern Data Stack** pattern, leveraging Azure for scalable storage and Snowflake for decoupled compute.

```mermaid
graph TB
    %% -- DATA SOURCES --
    subgraph Sources [Data Sources]
        CSV[Gov Canada CSVs]
        Stream[Synthetic IoT Stream]
    end

    %% -- AZURE CLOUD --
    subgraph Azure [Azure Cloud Infrastructure]
        EH(Azure Event Hubs)
        Airflow{{Apache Airflow DAGs}}
        ADLS[(Azure Data Lake\nADLS Gen2)]
    end

    %% -- SNOWFLAKE --
    subgraph Snow [Snowflake Data Cloud]
        Pipe(Snowpipe Auto-Ingest)
        Raw[(Raw Layer\nVariant Data)]
        Clean[(Curated Layer\nStructured Tables)]
    end

    %% -- SERVING --
    subgraph App [Application & ML]
        ML{Scikit-learn / XGBoost}
        API[FastAPI Backend]
        Viz[Tableau / Streamlit]
        React[React/Vue Frontend]
    end

    %% -- FLOWS --
    CSV -->|Batch Ingest| Airflow
    Stream -->|Real-Time Events| EH
    
    Airflow -->|Orchestrate Upload| ADLS
    EH -->|Capture| ADLS
    
    ADLS -->|Trigger Notification| Pipe
    Pipe -->|COPY INTO| Raw
    Raw -->|dbt / SQL| Clean
    
    Clean -->|Training Data| ML
    ML -->|Inference| API
    Clean -->|BI Analytics| Viz
    API -->|JSON Response| React

    %% -- STYLING --
    style Sources fill:#2d2d2d,stroke:#fff,color:white
    style Azure fill:#003d73,stroke:#0078D4,color:white
    style Snow fill:#29B5E8,stroke:#fff,color:white
    style App fill:#2d2d2d,stroke:#00C853,color:white
    
    %% Node Specifics
    style Airflow fill:#e67e22,color:white
    style ADLS fill:#0078D4,color:white
    style Pipe fill:#ffffff,color:black
    
    %% Arrows (White for Dark Mode)
    linkStyle default stroke:white,stroke-width:2px

```

## Key Features

* **Vehicle Search and Comparison** – Compare **fuel efficiency, emissions, and annual fuel costs** across models.
* **Interactive Dashboards** – Visualize **historical and forecasted trends** in fuel economy, emissions, and costs.
* **Predictive Analytics** – Machine learning models (e.g., **Scikit-learn, XGBoost**) estimate **fuel consumption and carbon tax impacts**.
* **Policy Insights** – Provide **projections for government agencies** to refine emissions policies.
* **Manufacturer Insights** – Identify **inefficient vehicle models** for compliance improvements.
* **Personalized Recommendations** – Suggest **cost-effective and eco-friendly vehicles** to consumers.

---

## Architecture

* **Data Ingestion** – Government datasets (CSV) + **synthetic streaming events** via **Kafka on Azure Event Hubs**.
* **Data Orchestration** – Automated ETL with **Apache Airflow DAGs** for ingestion, validation, and transformation.
* **Data Storage** – Raw and curated data stored in **Azure Data Lake Storage (ADLS Gen2)**.
* **Data Warehouse** – Processed datasets loaded into **Snowflake**, with **Snowpipe** for near real-time ingestion.
* **Visualization** – **Tableau** and **Streamlit dashboards** connected to Snowflake for interactive analytics.
* **Frontend** – User-facing dashboard built with **React/Vue.js**.

---

## Tech Stack

* **Backend**: Python, FastAPI
* **Machine Learning**: Scikit-learn, XGBoost, Random Forest, Decision Trees
* **Data Engineering**: Pandas, NumPy, **Apache Airflow**
* **Streaming**: **Kafka on Azure Event Hubs** (simulated ingestion)
* **Data Warehouse**: **Snowflake**
* **Visualization**: **Tableau, Streamlit, Matplotlib, Seaborn**
* **Frontend**: React or Vue.js
* **Deployment**: Render (demo hosting), **Azure (pipeline services)**

---

## Project Goals

* Improve **consumer awareness** of fuel costs and carbon tax.
* Enable **data-driven decision-making** for vehicle purchases.
* Provide **government agencies** with insights for emissions policies.
* Help **manufacturers** meet sustainability targets.

---

## Future Enhancements

* Integrate **real-time API/IoT data feeds**.
* Deploy predictive models as **APIs with Azure ML**.
* Expand coverage beyond Canada.
* Add **Power BI dashboards** for enterprise analytics.
