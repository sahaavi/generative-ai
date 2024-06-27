# Gemini for Data Scientists

### Task 1. Configure your environment and account <a href="#step4" id="step4"></a>

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
    gcloud projects add-iam-policy-binding ${PROJECT_ID} --member user:${USER} --role=roles/aiplatform.notebookRuntimeUser
    gcloud projects add-iam-policy-binding ${PROJECT_ID} --member user:${USER} --role=roles/dataform.codeEditor
    ```

    Adding these roles lets the user use Gemini assistance and Python notebooks with Colab Enterprise.
6.  Add the Notebook Runtime User, Dataform Code Editor and Compute Admin roles to the Qwiklabs user service account.

    ```
    CLOUD_BUILD_SERVICE_ACCOUNT="${PROJECT_ID}@${PROJECT_ID}.iam.gserviceaccount.com"
    gcloud projects add-iam-policy-binding $PROJECT_ID \
      --member serviceAccount:$CLOUD_BUILD_SERVICE_ACCOUNT \
      --role roles/aiplatform.notebookRuntimeUser
    gcloud projects add-iam-policy-binding $PROJECT_ID \
      --member serviceAccount:$CLOUD_BUILD_SERVICE_ACCOUNT \
      --role roles/dataform.codeEditor
    gcloud projects add-iam-policy-binding $PROJECT_ID \
      --member serviceAccount:$CLOUD_BUILD_SERVICE_ACCOUNT \
      --role roles/compute.admin
    ```

### Task 2. Create a BigQuery dataset for your project <a href="#step5" id="step5"></a>

In this task, you will create the ecommerce dataset in BigQuery. The dataset will be used to store the ecommerce data you will categorize in this lab.

1.  In the Google Cloud console, select the **Navigation menu** (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), and then select **BigQuery**.

    The Welcome to BigQuery in the Cloud Console pop-up is displayed.
2. Click **Done**.
3.  In the **Explorer** panel, for **`qwiklabs-gcp-01-ea65c06478f7`**, select **View actions** (![More menu icon](https://cdn.qwiklabs.com/2ufrDePg5inKfodUoT2Kib4oE7II7emYn%2BypCC85FjQ%3D)), and then select **Create dataset**.

    You [create a dataset](https://cloud.google.com/bigquery/docs/datasets) to store database objects, including tables and models.
4.  In the **Create dataset** pane, enter the following information:

    | Field         | Value                   |
    | ------------- | ----------------------- |
    | Dataset ID    | ecommerce               |
    | Location type | select **Multi-Region** |

    Leave the other fields at their defaults.
5. Click **Create Dataset**.

### Task 3. Create a new Python notebook and Enable the required APIs <a href="#step6" id="step6"></a>

In this task, you create a new Python notebook in BigQuery and you will enable the required APIs, so that you may use Gemini in BigQuery. The Python notebook is needed in BigQuery so that you may use Python machine learning libraries to identify customers and categorize them into groups, based upon shopping data in the ecommerce dataset.

1. In the Google Cloud console, select the **Navigation menu** (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), and then select **BigQuery**.
2. To enable Gemini for BigQuery Studio, At the top of the page, click the **down arrow** next to the plus sign.
3. Select **Python Notebook**.
4. Select the region **`us-central1`** to store your code assets from the dropdown and click **Select**.
5. You will see the a pop-up stating **Introducing BigQuery Studio notebooks** click **ENABLE APIS**.
6.  You will see the Enable Features pop-up appear on the right-hand side of the browser window and there are three section:

    * Core feature APIs
    * Permissions
    * Additional APIs

    **Note:** When performing the following steps, you may need help from your Google Cloud administrator or whomever the project owner is if you do not have the right permissions to enable these APIs.
7. Under Version history and sharing, check Dataform API is enabled if not click **ENABLE** to enable the API.
8. Under Python notebooks, click **ENABLE ALL** to enable the Vertex AI API and the Compute Engine API.
9. Click **NEXT**.
10. Under Permissions, click **NEXT**.
11. Under Additional APIs click **ENABLE ALL**. All required and optional APIs are now enabled.
12. Close the Enable Features pop-up.

    A new sample notebook is created with some example cells. Review these if you want, but you will not use them in this lab.
13. Delete all of the cells that are in the notebook by clicking the **Garbage Can** icon that appears when you hover over each cell.

    Once complete, the notebook should be blank and you are ready to move on to the next step.

### Task 4. Connect to the Colab Enterprise runtime in BigQuery <a href="#step7" id="step7"></a>

The next step is to connect to the Colab Enterprise runtime in BigQuery. Think of this runtime as a managed environment in BigQuery that allows you to access machine learning libraries that can help you identify your customers and categorize them into groups.

1. While remaining in the BigQuery Studio console, in the upper right corner of the notebook click on the **down arrow** next to Connect.
2. In the drop down select **Connect to a runtime**.
3. Select **Create a new runtime**.
4.  Select **Create default runtime**.

    Wait a few minutes while the runtime is allocated.

    You see the Open OAuth popup displayed.
5.  Click **OPEN**.

    You will see another pop-up window, with the Qwiklabs student ID displayed.
6.  Click on the **Qwiklabs student ID**.

    A new pop-up is displayed, with an option to Allow.
7.  Click **Allow** on this pop-up.

    You will then see the connection status update to Connected at the bottom of your browser window.

    You will also notice that the Python notebook is added in the notebooks section of the explorer under your project.

### Task 5. Build the Python Notebook <a href="#step8" id="step8"></a>

In this task, you begin to build the Python notebook, by performing the following steps:

* Import Python libraries
* Define variables
* Create and import a base table as a BigQuery DataFrame from a public dataset
* Generate the K-means clustering model and visualization

#### Refreshing the current page using your browser

**Important:** Before proceeding with the steps in this task, we recommend you manually refresh the current page using your browser. This will ensure that the Generate button is available to you within notebooks.

To refresh your browser and return to the notebook, use the steps below:

1.  In the Google Chrome Browser, use the **Reload this page**. Use a similar process if you are using Safari or Firefox.

    **Note:** Refreshing the browser page returns you to the Welcome to BigQuery Studio! page (BigQuery home page)
2.  On the Welcome to BigQuery Studio! page, click **OPEN** for the Untitled notebook you created earlier.

    You will see that the example cells are still removed, and that the notebook will reconnect to the default runtime.
3. Confirm the runtime has a status of Connected.

#### Import Python libraries and define variables

The first step to build the Python notebook is to import python libraries and define variables.

To import the libraries into your notebook, use the steps below:

1. Add a code cell into the notebook, click the **+Code** button at the top of the notebook window.
2.  Paste the following code snippet into the cell:

    ```
    from google.cloud import bigquery
    from google.cloud import aiplatform
    import bigframes.pandas as bpd
    import pandas as pd
    from vertexai.language_models._language_models import TextGenerationModel
    from bigframes.ml.cluster import KMeans
    from bigframes.ml.model_selection import train_test_split
    ```
3.  Run ![Run](https://cdn.qwiklabs.com/vQVR9T%2FhiD%2FqJV39SQycI6EymyOmwn8wcJPayFhFyLE%3D) the cell.

    The runtime will load the Python libraries, which will take approximately 1 minute. You can follow the progress by checking the status of the runtime at the bottom of the browser window.

    When complete you will see a green checkmark ![checkmark](https://cdn.qwiklabs.com/KUe9YKOMJZpJ9jFw6P8qnTnglDiNt2raJZH0FAIWHMs%3D) next to the Run button on the cell.

The table below provides more information about the Python libraries that you just imported to your notebook, including a brief description about each one.

| Library                                                                                                                               | Description                                                                                                         |
| ------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| [BigQuery](https://cloud.google.com/python/docs/reference/bigquery/latest)                                                            | Python Client for Google BigQuery                                                                                   |
| [AI Platform](https://cloud.google.com/python/docs/reference/aiplatform/latest)                                                       | Vertex AI SDK for Python                                                                                            |
| [bigframes.pandas](https://cloud.google.com/python/docs/reference/bigframes/latest)                                                   | BigQuery DataFrames                                                                                                 |
| [pandas](https://pandas.pydata.org/)                                                                                                  | Open source data analysis and manipulation tool, built on top of the Python programming language.                   |
| [TextGenerationModel](https://cloud.google.com/python/docs/reference/aiplatform/latest/vertexai.language\_models.TextGenerationModel) | Creates a LanguageModel within VertexAI.                                                                            |
| [Kmeans](https://cloud.google.com/python/docs/reference/bigframes/latest/bigframes.ml.cluster.KMeans)                                 | Used to create K-means clustering models within BigQuery DataFrames                                                 |
| [train\_test\_split](https://cloud.google.com/python/docs/reference/bigframes/latest/bigframes.ml.model\_selection)                   | Used to split source dataset into test and training subsets, and used with model tuning within BigQuery DataFrames. |

**Note:** If you want to learn more about each library, use the link provided.

#### Define variables and initiate the BigQuery and Vertex AI connection

Next you will define variables and initiate the BigQuery and Vertex AI connection.

1. Add another code cell at the end of the notebook.
2.  Paste the following code snippet into the cell.

    ```
    project_id = '<project_id>'
    dataset_name = "ecommerce"
    model_name = "customer_segmentation_model"
    table_name = "customer_stats"
    location = "<location>"
    client = bigquery.Client(project=project_id)
    aiplatform.init(project=project_id, location=location)
    ```
3. Replace **\<project\_id>** with **`qwiklabs-gcp-01-ea65c06478f7`**.
4. Replace **\<location>** with **`us-central1`**.
5. Run ![Run](https://cdn.qwiklabs.com/vQVR9T%2FhiD%2FqJV39SQycI6EymyOmwn8wcJPayFhFyLE%3D) the cell.

#### Create and import the ecommerce.customer\_stats table

Next you will store data from thelook\_ecommerce BigQuery public dataset into a new table entitled customer\_status in your ecommerce dataset.

1. Add another code cell at the end of the notebook.
2.  Paste the following code snippet into the cell.

    ```
    %%bigquery
    CREATE OR REPLACE TABLE ecommerce.customer_stats AS
    SELECT
      user_id,
      DATE_DIFF(CURRENT_DATE(), CAST(MAX(order_created_date) AS DATE), day) AS days_since_last_order, ---RECENCY
      COUNT(order_id) AS count_orders, --FREQUENCY
      AVG(sale_price) AS average_spend --MONETARY
      FROM (
          SELECT
            user_id,
            order_id,
            sale_price,
            created_at AS order_created_date
            FROM `bigquery-public-data.thelook_ecommerce.order_items`
            WHERE
            created_at
                BETWEEN '2022-01-01' AND '2023-01-01'
      )
    GROUP BY user_id;
    ```
3. Run ![Run](https://cdn.qwiklabs.com/vQVR9T%2FhiD%2FqJV39SQycI6EymyOmwn8wcJPayFhFyLE%3D) the cell.

#### Create a BigQuery DataFrame and load the data using a Gemini prompt

In this step, you create a BigQuery DataFrame using a Gemini prompt and load the customer stats data into it, so that you may process the data later with the K-means clustering model.

1. Add another code cell at the end of the notebook.
2. Within the cell, click **generate**. This allows you to generate code with Gemini, and you will see a prompt where you can add text.
3.  Paste the following text into the prompt.

    ```
    Convert the table ecommerce.customer_stats to a BigQuery DataFrames dataframe and show the top 10 records
    ```
4.  Press **\<Enter>** or click **generate**. Gemini will generate the code below.

    ```
    df = bpd.read_gbq(f"bq://{project_id}.{dataset_name}.{table_name}")
    df.head(10)
    ```

    Copied!content\_copy**Note:** Remember that in a previous step, you added code to cell number 2 in the notebook that saved the project ID, the dataset name, and the table name as variables. If you completed this step, when you run the cell in the next step you will not have any issues and the DataFrame will be created with the first 10 rows displayed.
5.  Remove **bq://** from the first line in the cell Gemini just created for you. Once that text is removed, the cell should contain the following:

    ```
    df = bpd.read_gbq(f"{project_id}.{dataset_name}.{table_name}")
    df.head(10)
    ```
6.  Run ![Run](https://cdn.qwiklabs.com/vQVR9T%2FhiD%2FqJV39SQycI6EymyOmwn8wcJPayFhFyLE%3D) the cell.

    You will see the BigQuery DataFrame output with the first 10 rows of the dataset displayed.

#### Generate the K-means clustering model

Now that you have your customer data in a BigQuery DataFrame, you will create a K-means clustering model to split the customer data into clusters based on fields like order recency, order count, and spend, and you will then visualize these as groups within a chart directly within the notebook.

1. Add another code cell at the end of the notebook.
2. Click **generate** in the cell. This will allow you to generate code with Gemini using a prompt.
3.  Add the following prompt to the cell:

    ```
    1. Split df into test and training data for a K-means clustering algorithm store these as df_test_ and df_train. 2. Create a K-means cluster model using bigframes.ml.cluster KMeans with 5 clusters. 3. Save the model to BigQuery in a model called ecommerce.model_name using the to_gbq method.
    ```
4.  Press **\<Enter>**. You will see output similar to the following:

    ```
    #prompt: 1. Split df into test and training data for a K-means clustering algorithm store these as df_test_ and df_train. 2. Create a K-means cluster model using bigframes.ml.cluster KMeans with 5 clusters. 3. Save the model to BigQuery in a model called ecommerce.model_name using the to_gbq method.

    df_train, df_test = train_test_split(df, test_size=0.2,  random_state=42)
    model = KMeans(n_clusters=5)
    model.fit(df_train)
    model.to_gbq(f"{project_id}.{dataset_name}.{model_name}")
    ```

    **Important:** Check the code that is created from Gemini in this step. If the kmeans model is kmeans for the variable name in line 2, it needs to be changed (manually) to model, and subsequently so do lines 3 and 4. Keep in mind, "As an early-stage technology, Gemini can generate output that seems plausible but is factually incorrect. We recommend that you validate all output from Gemini before you use it. For more information, see Gemini in Google Cloud and responsible AI."
5.  Run ![Run](https://cdn.qwiklabs.com/vQVR9T%2FhiD%2FqJV39SQycI6EymyOmwn8wcJPayFhFyLE%3D) the cell.

    **Note:** This step will take approximately 2 minutes to complete.

    Your model is now created!
6.  Refresh the contents of your Explorer panel by clicking the **three dots** next to your project name and selecting **Refresh contents**. It should pop up under your ecommerce dataset.

    Next, you define a new BigQuery DataFrame that joins the segment/cluster produced by the K-means model back to the original data.
7. Add another code cell at the end of the notebook.
8.  Click **generate** in the cell.

    This will allow you to generate code with Gemini using a prompt.
9.  Add the following prompt to the cell:

    ```
    1. Call the K-means prediction model on the df dataframe, and store the results as predictions_df and show the first 10 records.
    ```
10. Press **\<Enter>**. You will see output similar to the following:

    ```
    # prompt: 1. Call the K-means prediction model on the df dataframe, and store the results as predictions_df and show the first 10 records.

    predictions_df = model.predict(df)
    predictions_df.head(10)
    ```
11. Run ![Run](https://cdn.qwiklabs.com/vQVR9T%2FhiD%2FqJV39SQycI6EymyOmwn8wcJPayFhFyLE%3D) the cell.

    You see that the first 10 records are shown with the CENTROID\_ID. CENTROID\_ID is the cluster that the customer will be categorized as later in the lab. You also see the user\_id, days\_since\_last\_order, count\_orders and average\_spend fields.

#### Create a visualization of the K-means clustering model results

In this next step, you will create a visualization of the K-means clustering model results. Specifically, you will generate a scatterplot using predictions\_df to look at the relationship between the days since last order by average spend, colored by segment\_id (which was generated using our K-means model!)

1. Add another code cell at the end of the notebook.
2. Click **generate** in the cell. This will allow you to generate code with Gemini using a prompt.
3.  Add the following prompt to the cell:

    ```
    1. Using predictions_df, and matplotlib, generate a scatterplot. 2. On the x-axis of the scatterplot, display days_since_last_order and on the y-axis, display average_spend from predictions_df. 3. Color by cluster. The chart should be titled "Attribute grouped by K-means cluster."
    ```
4.  Press **\<Enter>**. You will see output similar to the following:

    ```
    #prompt: 1. Using predictions_df, and matplotlib, generate a scatterplot. 2. On the x-axis of the scatterplot, display days_since_last_order and on the y-axis, display average_spend from predictions_df. 3. Color by cluster. The chart should be titled "Attribute grouped by K-means cluster."


    import matplotlib.pyplot as plt

    plt.scatter(predictions_df['days_since_last_order'], predictions_df['average_spend'], c=predictions_df['cluster'])
    plt.xlabel("days_since_last_order")
    plt.ylabel("average_spend")
    plt.title("Attribute grouped by K-means Cluster")
    plt.show()
    ```
5. Replace 'cluster' with **'CENTROID\_ID'**.
6.  Run ![Run](https://cdn.qwiklabs.com/vQVR9T%2FhiD%2FqJV39SQycI6EymyOmwn8wcJPayFhFyLE%3D) the cell.

    You will see the visualization displayed.

**Note:** If you get a **TypeError** replace the code with the example output and then run the cell.

### Task 6. Generate insights from the results of the model <a href="#step9" id="step9"></a>

In this task, you generate insights from the results of the model by performing the following steps:

* Summarize each cluster generated from the K-means model
* Define a prompt for the marketing campaign
* Generate the marketing campaign using the text-bison model

#### Summarize each cluster generated from the K-means model

In this step, you will summarize each cluster generated from the K-means model.

1. Add another code cell at the end of the notebook.
2.  Paste the following code snippet into the cell:

    ```
    query = """
    SELECT
     CONCAT('cluster ', CAST(centroid_id as STRING)) as centroid,
     average_spend,
     count_orders,
     days_since_last_order
    FROM (
     SELECT centroid_id, feature, ROUND(numerical_value, 2) as value
     FROM ML.CENTROIDS(MODEL `{0}.{1}`)
    )
    PIVOT (
     SUM(value)
     FOR feature IN ('average_spend',  'count_orders', 'days_since_last_order')
    )
    ORDER BY centroid_id
    """.format(dataset_name, model_name)

    df_centroid = client.query(query).to_dataframe()
    df_centroid.head()
    ```
3.  Run ![Run](https://cdn.qwiklabs.com/vQVR9T%2FhiD%2FqJV39SQycI6EymyOmwn8wcJPayFhFyLE%3D) the cell.

    You should see the clusters summarized in a table. Some insights you can get from this table are that some clusters have a higher average spend, and others have a higher count of orders.

    Next, you will convert the data frame into a string, so you can pass it to your large language model call.
4. Add another code cell at the end of the notebook.
5.  Paste the following code snippet into the cell:

    ```
    df_query = client.query(query).to_dataframe()
    df_query.to_string(header=False, index=False)

    cluster_info = []
    for i, row in df_query.iterrows():
     cluster_info.append("{0}, average spend ${2}, count of orders per person {1}, days since last order {3}"
      .format(row["centroid"], row["count_orders"], row["average_spend"], row["days_since_last_order"]) )

    cluster_info = (str.join("\n", cluster_info))
    print(cluster_info)
    ```
6.  Run ![Run](https://cdn.qwiklabs.com/vQVR9T%2FhiD%2FqJV39SQycI6EymyOmwn8wcJPayFhFyLE%3D) the cell.

    The output should be similar to:

    ```
    cluster 1, average spend $48.32, count of orders per person 1.36, days since last order 384.37
    cluster 2, average spend $202.34, count of orders per person 1.3, days since last order 482.62
    cluster 3, average spend $45.68, count of orders per person 1.36, days since last order 585.4
    cluster 4, average spend $44.71, count of orders per person 1.36, days since last order 466.26
    cluster 5, average spend $58.08, count of orders per person 3.92, days since last order 427.36
    ```

#### Define a prompt for the marketing campaign

In this step, you define a prompt, so that your large language model (based on text-bison) understands what you are asking for.

1. Add another code cell at the end of the notebook.
2.  Paste the following code snippet into the cell:

    ```
    prompt = f"""
    You're a creative brand strategist, given the following clusters, come up with \
    creative brand persona, a catchy title, and next marketing action, \
    explained step by step.

    Clusters:
    {cluster_info}

    For each Cluster:
    * Title:
    * Persona:
    * Next marketing step:
    """
    ```
3. Run ![Run](https://cdn.qwiklabs.com/vQVR9T%2FhiD%2FqJV39SQycI6EymyOmwn8wcJPayFhFyLE%3D) the cell.

**Note:** You will not see output from running this cell because you are just defining the variable ‘prompt’, which will be used in the next step.

#### Generate the marketing campaign using the text-bison model

You have created a K-means model, assigned each customer to a cluster from the model, generated summary statistics for each cluster, and defined a prompt. Next you can call the text-bison model to generate customer insights and next steps for our marketing team.

For each cluster/segment defined by the K-means model, we'll generate three items that can be used by our marketing team:

* Title
* Persona
* Next marketing step

1. Add another code cell at the end of the notebook.
2.  Click **generate** in the cell.

    This will allow you to generate code with Gemini using a prompt.
3.  Add the following prompt to the cell:

    ```
    Use the Vertex AI language_models API to call the PaLM2 text-bison model and generate a marketing campaign using the variable prompt. Use the following model settings: max_output_tokens=1024, temperature=0.4
    ```
4.  Press **\<Enter>**. You will see output similar to the following:

    ```
    #prompt:  Use the Vertex AI language_models API to call the PaLM2 text-bison model and generate a marketing campaign using the variable prompt. Use the following model settings: max_output_tokens=1024, temperature=0.4

    model = TextGenerationModel.from_pretrained("text-bison")
    response = model.predict(prompt, max_output_tokens=1024, temperature=0.4)
    print(response.text)
    ```
5.  Run ![Run](https://cdn.qwiklabs.com/vQVR9T%2FhiD%2FqJV39SQycI6EymyOmwn8wcJPayFhFyLE%3D) the cell.

    You should see results similar to:

    ```
    Cluster 1:
    Title: "The Occasional Shoppers"
    Persona: These customers are likely to be sporadic shoppers who make infrequent purchases. They may be attracted to discounts or promotions, and they may be more likely to purchase items that are on sale.
    Next marketing step: Offer discounts or promotions to entice these customers to make more frequent purchases.


    Cluster 2:
    Title: "The Loyal Customers"
    Persona: These customers are likely to be loyal to your brand and make repeat purchases. They may be more likely to spend more money on each purchase and be less likely to be swayed by competitors' offerings.
    Next marketing step: Reward these customers for their loyalty with a loyalty program or exclusive discounts.


    Cluster 3:
    Title: "The Lapsed Customers"
    Persona: These customers have not made a purchase in a long time. They may have been lost to a competitor or simply lost interest in your brand.
    Next marketing step: Reach out to these customers with a special offer or promotion to win them back.


    Cluster 4:
    Title: "The Bargain Hunters"
    Persona: These customers are likely to be motivated by price and are more likely to purchase items that are on sale. They may be less loyal to your brand and more likely to switch to a competitor if they find a better deal.
    Next marketing step: Offer discounts or promotions to entice these customers to make more frequent purchases.


    Cluster 5:
    Title: "The Power Buyers"
    Persona: These customers are likely to be your most valuable customers. They spend the most money and make the most frequent purchases. They may be more likely to be brand advocates and refer your brand to others.
    Next marketing step: Reward these customers for their loyalty with a loyalty program or exclusive discounts. Additionally, ask them to refer your brand to their friends and family.
    ```

Information about each cluster and next marketing steps for them is now easily shareable with the marketing team.

Typically, gathering customized information to account for taste, spend, and buy frequency would take teams considerable time for manual work. Now a data scientist is able to do it in minutes by combining generative AI with the data in BigQuery.

### Task 7. Clean up project resources (Optional) <a href="#step10" id="step10"></a>

In this lab, you created resources within the Google Cloud console. In a production environment you will need to remove these resources from your account, as they would be no longer needed once the insights from the model are collected. To remove the resources from your account and avoid further charges for their use, you have two options:

* Remove the project (see cautions below)
* Remove the individual resources

#### Clean up resources by removing the project

To avoid incurring charges to your Google Cloud account for the resources used in this tutorial, you can delete the Google Cloud project that you created for this tutorial.

**Caution:** Deleting a project has the following effects:

* Everything in the project is deleted. If you used an existing project for the tasks in this document, when you delete it, you also delete any other work you've done in the project.
* Custom project IDs are lost. When you created this project, you might have created a custom project ID that you want to use in the future. To preserve the URLs that use the project ID, such as an appspot.com URL, delete selected resources inside the project instead of deleting the whole project.

If you plan to explore multiple architectures, tutorials, or quickstarts, reusing projects can help you avoid exceeding project quota limits.

1. In the Google Cloud console, go to the **Manage resources** page.
2. In the project list, select the project that you want to delete, and then click **Delete**.
3. In the dialog, type the _project ID_, and then click **Shut Down Anyway** to delete the project.

#### Clean up resources by deleting individual resources

To avoid incurring charges, you can delete the table and model used in this lab by running the following code in a new code cell within the notebook:

```
# Delete customer_stats table

client.delete_table(f"{project_id}.{dataset_name}.{table_name}", not_found_ok=True)
print(f"Deleted table: {project_id}.{dataset_name}.{table_name}")


# Delete K-means model
client.delete_model(f"{project_id}.{dataset_name}.{model_name}", not_found_ok=True)
print(f"Deleted model: {project_id}.{dataset_name}.{model_name}")
```

After you run the cell, you can refresh the contents of your project in BigQuery studio to observe the deletion of the table and the model.
