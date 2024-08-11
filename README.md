# Assignment: ETL with Airflow

**Introduction:**
In this assignment, you will demonstrate your understanding of Extract, Transform, Load (ETL) processes using Apache Airflow for workflow orchestration. You will be tasked with designing and implementing an ETL pipeline that extracts data from various sources, applies transformations, and loads the transformed data into a target database.

**Task Details:**

## DAG from API to Database:

**Description:**
This DAG automates the process of fetching data from one or more APIs, transforming the retrieved data, and loading it into a target database.

**Task Details:**
- **Fetch Data from API:** Makes HTTP requests to one or more APIs to retrieve data. The data is typically returned in JSON format.
    - https://github.com/wanrabbae/api-sekolah-indonesia (API Documentation)
    - https://api-sekolah-indonesia.vercel.app/sekolah?page=1&perPage=2000 (API Request)
- **Transform Data:** Apply any necessary data transformations to the retrieved data. **Ensure at least two transformations are applied.**
- **Load Data to Database:** Inserts the transformed data into the target database table. Automatic table creation is ensured if necessary.

```python
from datetime import datetime, timedelta
from airflow import DAG
from airflow.operators.python_operator import PythonOperator
from airflow.providers.postgres.hooks.postgres import PostgresHook
import pandas as pd
import requests

# Define default arguments
default_args = {
    'owner': 'airflow',
    'depends_on_past': False,
    'email_on_failure': False,
    'email_on_retry': False,
    'retries': 1,
    'retry_delay': timedelta(minutes=5),
    'start_date': datetime(2024, 5, 1),
}

# Function to fetch data from API
def fetch_data_from_api():
    response = requests.get('https://api-sekolah-indonesia.vercel.app/sekolah?page=1&perPage=2000')
    data = response.json()
    return data

# Function to transform data
def transform_data(**kwargs):
    data = kwargs['ti'].xcom_pull(task_ids='fetch_data_from_api')
    # Extract the relevant data from the nested structure
    sekolah_data = data['dataSekolah']
    # Transform JSON data to DataFrame
    df = pd.DataFrame(sekolah_data)

    #Transformation 1
    # Filter and transform data using pandas
    # transformed_df = 

    #Transformation 2
    # Filter and transform data using pandas
    # transformed_df =

    transformed_df = df 

    return transformed_df

## Define Schema before load ( Change to your schema name)
custom_schema = 'public'

# Function to load data into database
# Define the custom schema name
def load_data_to_database(**kwargs):
    transformed_data = kwargs['ti'].xcom_pull(task_ids='transform_data')
    
    # Retrieve connection from Airflow
    postgres_hook = PostgresHook(postgres_conn_id='postgres')
    
    # Analyze data types of transformed data
    data_types = {col: 'TEXT' for col, dtype in transformed_data.dtypes.items()}
    
    # Create table if it doesn't exist
    create_query = f"""
    CREATE TABLE IF NOT EXISTS {custom_schema}.target_table (
        {', '.join([f'{col} {data_types[col]}' for col in transformed_data.columns])}
    );
    """
    postgres_hook.run(create_query)
    
    # Load data into the table with custom schema
    transformed_data.to_sql('target_table', postgres_hook.get_sqlalchemy_engine(), schema=custom_schema, if_exists='append', index=False)


# Define the DAG
with DAG('api_to_database_dag', default_args=default_args, schedule_interval='@daily', catchup=False) as dag:
    
    extract_task = PythonOperator(
        task_id='fetch_data_from_api',
        python_callable=fetch_data_from_api
    )
    
    transform_task = PythonOperator(
        task_id='transform_data',
        python_callable=transform_data,
        provide_context=True
    )
    
    load_task = PythonOperator(
        task_id='load_data_to_database',
        python_callable=load_data_to_database,
        provide_context=True
    )
    
    extract_task >> transform_task >> load_task
```

**Assignment Requirements:**

1. **Design:** Design an Airflow Directed Acyclic Graph (DAG) to perform ETL operations. Ensure that each DAG consists of tasks for extraction, transformation, and loading.
   
2. **Implementation:** Write Python functions for each task, adhering to the provided examples. Ensure that the functions handle extraction, transformation, and loading appropriately.

3. **Documentation:** Provide clear documentation for each task and the overall DAG. Explain the purpose of each task and any assumptions made during the implementation.

**Submission Guidelines:**
- Ensure that the documentation is well-formatted and includes relevant explanations and assumptions.
- Slide Presentation: Create a slide presentation to accompany the stored procedure. Each slide should focus on explaining a specific step of the procedure, detailing its significance, execution process, and impact on the overall ETL workflow. Ensure the slides are clear, concise, and visually appealing to facilitate understanding.
- Compress the Airflow DAG scripts and documentation into a single folder. (Optional)
- Submit the compressed folder containing the scripts and documentation. (Optional)


Zip Archive Submission: Save both the stored procedure script and the slide presentation as separate files within a zip archive. This zip file should be submitted through the Learning Management System (LMS) to facilitate grading and feedback.


**Note:** Utilize libraries and external resources as needed, and ensure that your implementation follows best practices for ETL pipelines and Airflow DAG design.


# Slide Presentation Structure Sample: ETL Process with Airflow

## Slide 1: Introduction to ETL with Apache Airflow
- **Overview**
  - Introduction to Extract, Transform, Load (ETL) processes.
  - Explanation of Apache Airflow as a tool for orchestrating ETL workflows.


## Slide 2: ETL from API to Database
- **Objective**
  - Automating ETL process from APIs to a database table.
- **Tasks**
  - Fetching data from APIs.
  - Transformation of retrieved data.
  - Loading transformed data into a database table.

## Slide 3: ETL from API to Database: Task Overview
- **Task Overview**
  - Description of the steps involved in the ETL process from API to database.
- **Steps**
  - Fetching data from APIs.
  - Transforming the retrieved data.
  - Loading transformed data into a database table.

## Slide 4: ETL from API to Database: Implementation
- **Implementation**
  - Designing Airflow DAG for API to database ETL.
  - Writing Python functions for data retrieval, transformation, and loading.
  - Implementing error handling and logging mechanisms.

## Slide 5: ETL from API to Database: Documentation
- **Documentation**
  - Documenting each task in the DAG.
  - Providing clear explanations for assumptions and configurations.
  - Parameterizing values through Airflow variables or DAG configuration.

## Slide 6: Benefits of ETL with Apache Airflow
- **Benefits**
  - Discussing the advantages of using Apache Airflow for ETL workflows.
  - Highlighting scalability, scheduling, and monitoring capabilities.

## Slide 7: Execution and Testing
- **Execution and Testing**
  - Explanation of executing and testing the ETL pipelines in Apache Airflow.
  - Importance of testing for accuracy and reliability of data processing.

## Slide 8: Conclusion
- **Conclusion**
  - Summarizing the key points covered in ETL pipelines with Apache Airflow.
  - Reinforcing the importance of efficient ETL processes for data-driven decision making.
