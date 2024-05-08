**Assignment: ETL with Airflow**

**Introduction:**
In this assignment, you will demonstrate your understanding of Extract, Transform, Load (ETL) processes using Apache Airflow for workflow orchestration. You will be tasked with designing and implementing an ETL pipeline that extracts data from various sources, applies transformations, and loads the transformed data into a target database.

**Task Details:**

### 1. DAG from CSV to Database:

**Description:**
This DAG automates the process of extracting data from one or more CSV files, performing any necessary data transformations, and loading the transformed data into a target database.

**Task Details:**
- **Extract Data:** Reads the CSV file(s) and loads the data into memory.
- **Transform Data:** Applies any required transformations to the extracted data.
- **Load Data to Database:** Inserts the transformed data into the target database table.

```python
# Python script for CSV to Database DAG
# [Insert provided Python script for CSV to Database DAG here]
```

### 2. DAG from API to Database:

**Description:**
This DAG automates the process of fetching data from one or more APIs, transforming the retrieved data, and loading it into a target database.

**Task Details:**
- **Fetch Data from API:** Makes HTTP requests to one or more APIs to retrieve data. The data is typically returned in JSON format.
- **Transform Data:** Applies any necessary data transformations to the retrieved data.
- **Load Data to Database:** Inserts the transformed data into the target database table. Automatic table creation is ensured if necessary.

```python
# Python script for API to Database DAG
# [Insert provided Python script for API to Database DAG here]
```

**Assignment Requirements:**

1. **Design:** Design an Airflow Directed Acyclic Graph (DAG) to perform ETL operations. Ensure that each DAG consists of tasks for extraction, transformation, and loading.
   
2. **Implementation:** Write Python functions for each task, adhering to the provided examples. Ensure that the functions handle extraction, transformation, and loading appropriately.

3. **Error Handling:** Implement error handling mechanisms within the pipeline to handle potential failures gracefully.

4. **Logging:** Incorporate logging within the tasks to facilitate troubleshooting and monitoring of the pipeline's execution.

5. **Parameterization:** Avoid hardcoding paths, URLs, or table schemas. Parameterize these values through Airflow variables or DAG configuration.

6. **Documentation:** Provide clear documentation for each task and the overall DAG. Explain the purpose of each task and any assumptions made during the implementation.

**Submission Guidelines:**
- Compress the Airflow DAG scripts and documentation into a single folder.
- Submit the compressed folder containing the scripts and documentation.
- Ensure that the documentation is well-formatted and includes relevant explanations and assumptions.
- Slide Presentation: Create a slide presentation to accompany the stored procedure. Each slide should focus on explaining a specific step of the procedure, detailing its significance, execution process, and impact on the overall ETL workflow. Ensure the slides are clear, concise, and visually appealing to facilitate understanding.

Zip Archive Submission: Save both the stored procedure script and the slide presentation as separate files within a zip archive. This zip file should be submitted through the Learning Management System (LMS) to facilitate grading and feedback.

**Evaluation Criteria:**
- Adherence to requirements: 30%
- Implementation correctness: 30%
- Error handling and logging: 20%
- Documentation quality: 20%

**Note:** Utilize libraries and external resources as needed, and ensure that your implementation follows best practices for ETL pipelines and Airflow DAG design.

---
This assignment aims to test your ability to design and implement ETL pipelines using Apache Airflow while adhering to best practices and documentation standards. Good luck! If you have any questions, feel free to ask.
