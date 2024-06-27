# Gemini for Data Scientists and Analysts

### Task 1. Configure your environment and account <a href="#step4" id="step4"></a>

In this task, you will configure your environment, account, and user, so that you can use the Cloud AI Companion API for Gemini.

1. Sign in to the Google Cloud console with your lab credentials, and open the **Cloud Shell** terminal window.
2.  To set your project ID and region environment variables, in Cloud Shell, run the following commands:

    ```
    PROJECT_ID=$(gcloud config get-value project)
    REGION=us-central1
    echo "PROJECT_ID=${PROJECT_ID}"
    echo "REGION=${REGION}"
    ```
3.  To store the signed-in Google user account in an environment variable, run the following command:

    ```
    USER=$(gcloud config get-value account 2> /dev/null)
    echo "USER=${USER}"
    ```
4.  Enable the Cloud AI Companion API for Gemini:

    ```
    gcloud services enable cloudaicompanion.googleapis.com --project ${PROJECT_ID}
    ```
5.  To use Gemini, grant the necessary IAM roles to your Google Cloud Qwiklabs user account:

    ```
    gcloud projects add-iam-policy-binding ${PROJECT_ID} --member user:${USER} --role=roles/cloudaicompanion.user
    gcloud projects add-iam-policy-binding ${PROJECT_ID} --member user:${USER} --role=roles/serviceusage.serviceUsageViewer
    ```

    Adding these roles lets the user use Gemini assistance.

### Task 2. Create a dataset and enable Gemini features in BigQuery <a href="#step5" id="step5"></a>

In this task, you will create a dataset and enable the Gemini features in BigQuery.

#### Create a dataset

1. In the Google Cloud console, select the **Navigation menu** (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), and then select **BigQuery**.
2.  In the **Explorer** panel, for **`qwiklabs-gcp-01-22f156fc7bb6`**, select **View actions** (![More menu icon](https://cdn.qwiklabs.com/2ufrDePg5inKfodUoT2Kib4oE7II7emYn%2BypCC85FjQ%3D)), and then select **Create dataset**.

    You [create a dataset](https://cloud.google.com/bigquery/docs/datasets) to store database objects, including tables and models.
3.  In the **Create dataset** pane, enter the following information:

    | Field         | Value                   |
    | ------------- | ----------------------- |
    | Dataset ID    | bqml\_tutorial          |
    | Location type | select **Multi-region** |

    Leave the other fields at their defaults.
4. Click **Create Dataset**.

#### Enable the Gemini features in BigQuery

1. To view Gemini features in BigQuery, in the toolbar, click **Gemini** (![Gemini](https://cdn.qwiklabs.com/bVHWh2RPFFD%2F7Y9aAK7vqg7F8%2BWVa%2BL7o1Grv4IaZUQ%3D)). If it's not visible then, refresh the page.
2. In the **Gemini in BigQuery SQL editor** list, select all of the following options:
   * **Auto completion**
   * **Auto generation**
   * **Explanation**

**Note:** To disable Gemini features in BigQuery, deselect the Gemini features that you want to disable.

### Task 3. Use Gemini to analyze your data <a href="#step6" id="step6"></a>

Gemini can help you discover and analyze your available data.

Before you can query data, you need to know what data you can access. Every data product organizes and stores data differently. To get help, you can send Gemini a natural language statement (or prompt) like, "How do I view which datasets and tables are available to me in BigQuery?"

If you want to understand the characteristics of different data query systems, you might prompt Gemini for specific product information like the following:

* "How do I get started with BigQuery?"
* "What are the benefits of using BigQuery for data analysis?"
* "How does BigQuery handle auto-scaling for queries?"

In this task, you will prompt Gemini to answer questions about your data.

#### Prompt Gemini to answer questions about your data

1. In the Google Cloud console, select the **Navigation menu** (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), and then select **BigQuery**.
2. In the Google Cloud console toolbar, click **Open Gemini** (![console Gemini menu](https://cdn.qwiklabs.com/8enFLY%2FtuyohEbT5f1NbBaC%2Fa%2Be7cuSzbbq1l19r%2B3Q%3D)).
3.  The _Welcome to Gemini in Cloud Console_ message is displayed in the Gemini pane. Click **Start Chatting**.

    **Note:** If the **Start Chatting** button is not enabled, refresh the page and open Gemini again.
4.  In the Gemini pane, enter the prompt:

    ```
    How do I learn which datasets and tables are available to me in BigQuery?
    ```
5.  Click send **Send prompt** (![Gemini send menu](https://cdn.qwiklabs.com/%2FmzrTT7U8dkGsp7pSuOUCbVh%2B9qgdh64vfB7FtF8io4%3D)).

    Gemini doesn't use your prompts or its responses as data to train its model. For more information, see [How Gemini for Google Cloud uses your data](https://cloud.google.com/gemini/docs/discover/data-governance).

    Gemini returns a response similar to the following:

    ```
    There are a few ways to learn which datasets and tables are available to you in BigQuery.

    You can use the Google Cloud console to browse the public datasets that are available.

    You can use the bq command-line tool to list the datasets and tables in your project.

    You can make calls to the BigQuery REST API to get a list of the datasets and tables in your project.
    ```
6. To optionally reset your chat history, in the Gemini pane, click **Reset Chat** (![Gemini reset chat](https://cdn.qwiklabs.com/gWJznEVRldNzJD0Ih7NsmC6h%2BqVWLix3a59Kxq%2FAeag%3D)).

**Note:** The chat history state is kept in memory only and doesn't persist when you switch to another workspace or when you close the Google Cloud console.

### Task 4. Prompt Gemini to explain SQL queries in a sales dataset <a href="#step7" id="step7"></a>

Gemini can help you work with SQL. For instance, if you work with SQL queries that other people wrote, Gemini in BigQuery can explain a complex query in plain language. Such explanations can help you understand the query syntax, underlying schema, and business context.

To prompt Gemini to explain an example SQL query, follow these steps:

1. In the Google Cloud console, select the **Navigation menu** (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), and then select **BigQuery**.
2. Click **Compose SQL QUERY**. The Explorer pane automatically loads the selected database.
3.  In the query editor, open or paste the query that you want explained.

    For example, you might want to understand how data tables and queries are related in a sales dataset, and you might want help writing queries that use the dataset. In the following example query, you might understand which tables are being used, but other sections of the query might take you time to parse and understand.

    ```
    SELECT u.id as user_id, u.first_name, u.last_name, avg(oi.sale_price) as avg_sale_price   
    FROM `bigquery-public-data.thelook_ecommerce.users` as u   
    JOIN `bigquery-public-data.thelook_ecommerce.order_items` as oi   
    ON u.id = oi.user_id   
    GROUP BY 1,2,3   
    ORDER BY avg_sale_price DESC   
    LIMIT 10
    ```

    Copied!content\_copy
4.  Highlight the query that you want Gemini to explain, and right-click on the highlighted query. In the menu, click **Explain current selection**.

    The SQL explanation appears in the **Gemini** pane.

    Using the example query from the previous step, Gemini returns an explanation similar to the following:

    ```
    The intent of this query is to find the top 10 users by average sale price. The query first joins the users and order_items tables on the user_id column. It then groups the results by user_id , first_name , and last_name, and calculates the average sale price for each group. The results are then ordered by average sale price in descending order, and the top 10 results are returned.
    ```

### Task 5. Generate a SQL query that groups sales by day and product <a href="#step8" id="step8"></a>

You can provide Gemini with a prompt to generate a SQL query based on your data's schema. Even if you're starting with no code, a limited knowledge of the data schema, or only a basic knowledge of SQL syntax, Gemini can suggest one or more SQL statements.

In this task, you generate a query that lists your top products for each day. This type of query is often complex, but you can automatically create a statement using Gemini. You then use tables in the **thelook\_ecommerce** dataset and prompt Gemini to generate a query to calculate sales by order item and by product name.

1. In the Google Cloud console, select the **Navigation menu** (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), and then select **BigQuery**.
2. In the navigation menu, click **BigQuery Studio**.
3. Click **Compose a new query**. The **Explorer** pane automatically loads the selected database.
4.  In the query editor, enter the following prompt, and then press ENTER. The pound character (#) prompts Gemini to generate SQL.

    ```
    # select the sum of sale_price by Date(created_at) and product_id casted to day from bigquery-public-data.thelook_ecommerce.order_id as t1 joined this with products table in the same dataset as t2
    ```

    Gemini suggests a SQL query similar to the following:

    ```
    # select the sum of sale_price by Date(created_at) and product_id casted to day from bigquery-public-data.thelook_ecommerce.order_id as t1 joined this with products table in the same dataset as t2
    SELECT
      SUM(sale_price),
      DATE(created_at) AS created_at_day,
      CAST(product_id as INT64)
    FROM
      `bigquery-public-data.thelook_ecommerce.order_items` AS t1
    JOIN
      `bigquery-public-data.thelook_ecommerce.products` AS t2 ON t1.product_id = t2.id
    GROUP BY
      created_at_day,
      product_id
    ```

    **Note:** Gemini might suggest multiple SQL statements for your prompt.
5. To accept the suggested code, click **Tab**, and then click **Run** to execute the SQL statement. You can also scroll through the suggested SQL and accept specific words suggested in the statement.
6. In the **Query results** pane, view the query results.

### Task 6. Build a forecasting model and view results <a href="#step9" id="step9"></a>

In this task, you use BigQuery ML to use a trend query to build a forecasting model, and use Gemini to explain and help you write a query to view results of the forecasting model.

You use the following example query with actual sales, which are used as an input to the model. The query is used as a part of creating the ML model.

1.  To create a forecasting ML model, in the **BigQuery SQL editor**, run the following SQL:

    ```
    CREATE MODEL bqml_tutorial.sales_forecasting_model
    OPTIONS(MODEL_TYPE='ARIMA_PLUS',
    time_series_timestamp_col='date_col',
    time_series_data_col='total_sales',
    time_series_id_col='product_id') AS
    SELECT sum(sale_price) as total_sales,
    DATE(created_at) as date_col,
    product_id
    FROM `bigquery-public-data.thelook_ecommerce.order_items`
    AS t1
    INNER JOIN `bigquery-public-data.thelook_ecommerce.products`
    AS t2
    ON t1.product_id = t2.id
    GROUP BY 2, 3;
    ```

You can use Gemini to help you [understand this query](https://cloud.google.com/gemini/docs/use-cases/analyze-data-gemini#prompt-gemini-explain-sql-queries).

**Note:**The query takes approximately 10 minutes to complete. While the model is running, you can also prompt Gemini with questions like **What is an ARIMA\_PLUS model type?**

When the model is created, the Results pane displays a message similar to the following:

```
Successfully created model named sales_forecasting_model.
```

2. Select the **sales\_forecast\_model** in the Explorer tab and copy the **Model ID** from the DETAILS tab to a text file. You will use this model ID in a future step.
3. In the **Gemini** pane, enter a prompt for Gemini to help you write a query to get a forecast from the model when it's completed. For example, enter **How can I get a forecast in SQL from the model?**

Based on the context of the prompt, Gemini returns an example of an ML model that forecasts sales:

```
To get a forecast in SQL from the model, you can use the following query:

SELECT
*
FROM
  ML.FORECAST(MODEL `PROJECT_ID.DATASET_ID.MODEL_NAME`,
STRUCT(
      7 AS horizon,
      0.95 AS confidence_level
)
)
```

**Note:** Gemini uses the context of the chat session to help answer questions in the same session.

4. In the **Gemini** pane, copy the SQL query.
5. In the **BigQuery SQL editor**, paste the SQL query.
6. On line 4, replace the MODEL sample string **PROJECT\_ID.DATASET\_ID.MODEL\_NAME** with the model ID you copied in a previous step.
7. Run the query and review the results.
