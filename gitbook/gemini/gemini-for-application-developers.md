# Gemini for Application Developers

### Task 1. Configure your environment and account <a href="#step4" id="step4"></a>

1. Sign in to the Google Cloud console with your lab credentials, and open the **Cloud Shell** terminal window.
2.  To set your project ID and region environment variables, in Cloud Shell, run the following commands:

    ```
    PROJECT_ID=$(gcloud config get-value project)
    REGION=us-west1
    echo "PROJECT_ID=${PROJECT_ID}"
    echo "REGION=${REGION}"
    ```
3.  To store the signed-in Google user account in an environment variable, run the following command:

    ```
    USER=$(gcloud config get-value account 2> /dev/null)
    echo "USER=${USER}
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

### Task 2. Create a Cloud Workstation <a href="#step5" id="step5"></a>

This lab uses Gemini assistance to develop an app with the Cloud Code plugin for Cloud Workstations IDE. Cloud Workstations is a fully managed integrated development environment that includes native integration with Gemini.

In this task, you configure and provision your Cloud Workstation environment, and you enable the Cloud Code plugin for Gemini.

#### View the workstation cluster

A workstation cluster named `my-cluster` has been pre-created for this lab. This cluster is used to configure and create a workstation.

1. In the Google Cloud console, select the **Navigation menu** (![Navigation menu icon](https://cdn.qwiklabs.com/tkgw1TDgj4Q%2BYKQUW4jUFd0O5OEKlUMBRYbhlCrF0WY%3D)), and then select **More Products > Tools > Cloud Workstations**.
2. In the **Navigation pane**, click **Cluster management**.
3. Check the **Status** of the cluster. If the status of the cluster is `Reconciling` or `Updating`, periodically refresh and wait until it becomes `Ready` before moving to the next step.

#### Create a workstation configuration

Before creating a workstation, you must create a workstation configuration in Cloud Workstations.

1. In the **Navigation pane**, click **Workstation configurations**, and then click **Create Workstation Configuration**.
2.  Specify the following values:

    | Property            | Value                   |
    | ------------------- | ----------------------- |
    | Name                | **my-config**           |
    | Workstation cluster | _select_ **my-cluster** |
3. Click **Create**.
4. Click **Refresh**.
5. Check the **Status** of the configuration being created. If the status of the configuration is `Reconciling` or `Updating`, periodically refresh and wait until the status becomes `Ready` before moving to the next step.

#### Create a workstation

1. In the **Navigation pane**, click **Workstations**, and then click **Create Workstation**.
2.  Specify the following values:

    | Property      | Value                  |
    | ------------- | ---------------------- |
    | Name          | **my-workstation**     |
    | Configuration | _select_ **my-config** |
3.  Click **Create**.

    After the workstation is created, it is listed under **My workstations** with a status of `Stopped`.
4.  To start the workstation, click **Start**.

    As the workstation starts up, the status changes to `Starting`. Wait for the status to change to `Running` which indicates that it is ready to be used. It might take several minutes for the workstation to fully start up.

#### Launch the IDE

To function properly, some extensions need third-party cookies to be enabled in your browser.

1. To enable third-party cookies in Chrome, in the **Chrome** menu, click **Settings**.
2. In the search bar, type **Third-party cookies**.
3.  Click the **Third-party cookies** setting, and select **Allow third-party cookies**.

    **Note:** If you want to restore your browser to its current settings after the lab, note the original setting for third-party cookies.

*   To launch the Code OSS IDE on the workstation, from the **Workstations** page in the Google Cloud console, click **Launch**.

    The IDE opens in a separate browser tab.

    ![OSS IDE with highlighted activity and status bars](https://cdn.qwiklabs.com/VW%2BlTAfhGJ1a%2BK3h0yAGNWQs3cPiLJkc%2BCBIxCtPdK4%3D)

### Task 3. Update the Cloud Code extension to enable Gemini <a href="#step6" id="step6"></a>

In this task, you enable Gemini in Cloud Code for your Workstation IDE.

#### Connect to Google Cloud

To connect to Google Cloud in your workstation, perform these steps:

1. At the bottom of the window, on the status bar, click **Cloud Code - Sign In**.
2.  When you're prompted to sign in, click **Proceed to sign in**.

    A link is displayed in the terminal.
3. To launch the Cloud Cloud sign-in flow, press Control (for Windows and Linux) or Command (for MacOS) and click the link in the terminal.
4. If you are asked to confirm the opening of the external website, click **Open**.
5. Click the student email address.
6. When you're prompted to continue, click **Continue**.
7.  To let the Google Cloud SDK access your Google Account and agree to the terms, click **Allow**.

    Your verification code is displayed in the browser tab.

    **Note:** You may see a warning that you ran a gcloud auth login command. This process is normal. The IDE ran this command on your behalf.
8. Click **Copy**.
9. Back in the IDE, in the terminal, where it says **Enter authorization code**, paste the code.
10. If asked to approve copying from the clipboard, click **Allow**.
11. Click Enter, and then wait for the status bar to show **Cloud Code - No Project**.

    You're now connected to Google Cloud.

#### Enable Gemini in Cloud Code

To enable Gemini in Cloud Code for your workstation IDE, perform these steps:

1. In your workstation IDE, click the menu (![Code OSS main menu](https://cdn.qwiklabs.com/H8AIg8zPKj8LfgE5rJjMSqNVieIjiopITlMQfBWkz0I%3D)), and then navigate to **File > Preferences > Settings**.
2. On the **User** tab of the Settings dialog, select **Extensions > Google Cloud Code**.
3. In **Search settings**, enter `Gemini`.
4.  On the Qwiklabs lab credentials panel, to copy the Project ID, click **Copy**.

    ![Copy button for Project ID is higlighted](https://cdn.qwiklabs.com/HQNEsxIwv%2B1NfXUePwPSg2QifSApfXMoa4Nz6yE2xNI%3D)
5.  On the Cloud Code settings page, for **Cloudcode > Gemini: Project**, paste the Google Cloud project ID.

    **Note:** This setting may be specified as **Cloudcode > Duet AI: Project**.
6.  Confirm that **Cloud Code > Gemini: Enable** is enabled.

    **Note:** This setting may be specified as **Cloudcode > Duet AI: Enable**.
7. In the IDE status bar, click **Cloud Code - No Project**.
8.  Click **Select a Google Cloud Project**, and then click your project ID.

    The project ID is now shown in the status bar. Gemini is now ready to use.

### Task 4. Chat with Gemini <a href="#step7" id="step7"></a>

Gemini can help you choose the Google Cloud services that meet the requirements of your application architecture. If you want to develop and test your app in your local IDE, and then deploy it to Google Cloud, you can chat with Gemini to get help.

In this task, you use the **Gemini pane** to enter prompts and view the responses from Gemini.

Prompts are questions or statements that describe the help that you need. Prompts can include context from existing code that Google Cloud analyzes to provide more useful or complete responses. For more information on writing prompts to generate good responses, see [Write better prompts for Gemini in Google Cloud](https://cloud.google.com/gemini/docs/discover/write-prompts).

#### Prompt Gemini

To prompt Gemini about Google Cloud services, perform these steps:

1. To open the Gemini chat pane, in the IDE activity bar, click **Gemini** (![Code OSS Gemini menu](https://cdn.qwiklabs.com/8enFLY%2FtuyohEbT5f1NbBaC%2Fa%2Be7cuSzbbq1l19r%2B3Q%3D)).
2. If an error occurs when trying to open the Gemini chat pane, refresh the browser window.
3.  In the **Gemini** pane, type the following prompt, and then click **Send** (![Gemini send](https://cdn.qwiklabs.com/%2FmzrTT7U8dkGsp7pSuOUCbVh%2B9qgdh64vfB7FtF8io4%3D)):

    ```
    I am new to Google Cloud and I want to use the Cloud Code extension. Give me some examples of Google services that I can use to build and deploy a sample app.
    ```

    Copied!content\_copy

    Gemini responds with a list of Google Cloud services and descriptions.

    In this example, assume that Gemini suggests both Cloud Run and Cloud Functions as two Google Cloud services that can help you build and deploy a sample app. You can ask for more information about those services.
4.  To provide a follow-up question or prompt, in the **Gemini** pane, type the text below, and then click **Send**:

    ```
    What is the difference between Cloud Run and Cloud Functions?
    ```

    Copied!content\_copy

    Gemini responds with key differences between the two Google Cloud services.
5.  To reset your chat history, in the **Gemini** pane, click **Reset Chat** (![Gemini reset chat](https://cdn.qwiklabs.com/gWJznEVRldNzJD0Ih7NsmC6h%2BqVWLix3a59Kxq%2FAeag%3D)).

    **Note:** Chat history state is kept in memory only, and doesn't persist when you switch to another workspace or when you close your IDE. Gemini doesn't use your prompts or its responses as data to train its model. For more information, see [How Gemini for Google Cloud uses your data](https://cloud.google.com/gemini/docs/discover/data-governance).

### Task 5. Develop a Python app <a href="#step8" id="step8"></a>

Let's now use Cloud Run to create and deploy a basic Python app. Because you're new to Cloud Run and Cloud Code, you need help with the steps for creating the app.

In this task, you prompt Gemini for help to build a Hello World Python app in Cloud Run.

#### Get help from Gemini

1.  In the **Gemini** pane, to learn how to create a Cloud Run app with Cloud Code, type the following prompt, and then click **Send** (![Gemini send](https://cdn.qwiklabs.com/%2FmzrTT7U8dkGsp7pSuOUCbVh%2B9qgdh64vfB7FtF8io4%3D)):

    ```
    How do I create a new Cloud Run app in Cloud Code using the command palette? What languages are supported?
    ```

    Copied!content\_copy
2.  In the response from Gemini, view the set of steps to create an app. Gemini also displays the supported languages for the Cloud Run app.

    **Note:** The command palette in VS Code provides a list of all the commands, including the commands for Cloud Code.

#### Create a Python app by using the steps from Gemini

1. Click the menu (![Code OSS main menu](https://cdn.qwiklabs.com/H8AIg8zPKj8LfgE5rJjMSqNVieIjiopITlMQfBWkz0I%3D)), and then navigate to **View > Command Palette**.
2. Type `Cloud Code New`, and then select **Cloud Code: New Application**.
3. Select **Cloud Run application**.
4. Select **Python (Flask): Cloud Run**.
5.  Update the name of the app and top-level folder to `/home/user/hello-world`, and then click **Ok**.

    Cloud Code downloads the template and creates the application files in the folder in your IDE.

#### Explore the app with Gemini

Now that you've created your `Hello World` app in Cloud Run, you can use Gemini to explain the files and code snippets that are deployed in your IDE.

1. If the files are not visible, in the IDE activity bar, click **Explorer** (![Code OSS Explorer menu](https://cdn.qwiklabs.com/O0MFBj4lYUnKniPTeF5CRvcp8WYEfriQ1TKU2JDw%2FgQ%3D)).
2. In the Explorer pane, select **Dockerfile**.
3.  Select the entire contents of the Dockerfile, click the bulb (![Code OSS Gemini bulb](https://cdn.qwiklabs.com/tLYH7qWU%2BLK5Z3aeYQf6nH7omJ0LQhao5WaGbYeXKLk%3D)), and from the **More Actions** menu, click **Explain this**.

    Gemini generates a natural-language explanation about the contents and function of the `Dockerfile`. You can also select portions of the file contents, click the bulb (![Code OSS Gemini bulb](https://cdn.qwiklabs.com/tLYH7qWU%2BLK5Z3aeYQf6nH7omJ0LQhao5WaGbYeXKLk%3D)), and then click **Explain this**.
4.  Select the line that begins with **ENTRYPOINT**, click the bulb (![Code OSS Gemini bulb](https://cdn.qwiklabs.com/tLYH7qWU%2BLK5Z3aeYQf6nH7omJ0LQhao5WaGbYeXKLk%3D)), and then click **Explain this**.

    Gemini responds with details about the ENTRYPOINT instruction. You learn that, with this instruction, Docker will run the app.py file when the container launches.
5. To view the contents of the `app.py` file, in the activity bar, click **Explorer** (![Code OSS Explorer menu](https://cdn.qwiklabs.com/O0MFBj4lYUnKniPTeF5CRvcp8WYEfriQ1TKU2JDw%2FgQ%3D)), and then click `app.py`.
6.  In the `hello()` function definition, select the lines that contain the `K_SERVICE`, and `K_REVISION` environment variables. Click the bulb (![Code OSS Gemini bulb](https://cdn.qwiklabs.com/tLYH7qWU%2BLK5Z3aeYQf6nH7omJ0LQhao5WaGbYeXKLk%3D)), then click **Explain this**.

    Gemini responds with a detailed explanation of these two Cloud Run environment variables and how they are used in the application code.

#### Run the app locally

You can run your app locally from your IDE by using the Cloud Run emulator. In this case, _locally_ means on the workstation machine.

1.  In the activity bar of your IDE, click **Cloud Code** (![Code OSS Cloud Code menu](https://cdn.qwiklabs.com/h7a1cGNlfuYGKBrCndl%2Fn9cDcLtr2yacmETamGQFgAs%3D)), and then click **Cloud Run**.

    **Note:** You will first run the app using the Cloud Run Emulator, so you won't need to enable the Cloud Run API yet.
2.  In the Cloud Run activity bar, click **Run App on Local Cloud Run Emulator** (![Cloud Run - run on local emulator](https://cdn.qwiklabs.com/z1o4I2oLA6FB2DV9wgz8KLptStQuC0l4PxaS%2Bq%2F3PVs%3D)), and then click **Run**.

    The **Output** tab in the IDE displays the progress of the build.
3.  When prompted at the top of the screen to **Enable minikube gcp-auth addon to access Google APIs**, select **Yes**.

    ![Enable minikube gcp-auth addon prompt](https://cdn.qwiklabs.com/jWdDb2enSYYc1cAEhixP71%2BXd8mUMqr7Anhh92d%2BTwg%3D)

    Wait for the build and deploy to complete.
4.  Hold the pointer over the link to the hello-world service at the localhost URL, and click **Follow link**.

    ![highlighted localhost URL and follow links](https://cdn.qwiklabs.com/CvNSc6ObDkrf%2BtAB10kEwv7zF%2F1dm6jy12zj8iEhA00%3D)

    A new tab is opened in the browser that displays a page indicating that the service is running.

### Task 6. Enhance the Python app <a href="#step9" id="step9"></a>

Let's now add data and functionality to the app so that it can be used for management of inventory data.

In this task, you first add inventory data for the app.

#### Generate sample data using Gemini

1. In the activity bar of your IDE, click **Explorer** (![Code OSS Explorer menu](https://cdn.qwiklabs.com/O0MFBj4lYUnKniPTeF5CRvcp8WYEfriQ1TKU2JDw%2FgQ%3D)).
2. Click **New file** (![Explorer - new file](https://cdn.qwiklabs.com/FeWHYTzVb8DXHcyWlssgCQ5rwEMk%2FOlcYYeDZC2Lnak%3D)), and create a file named `inventory.py`.
3.  To let Gemini generate the sample data, open the **Gemini** pane, type the following prompt, and then click **Send**:

    ```
    Create a variable called inventory which is a list of 3 JSON objects. Each JSON object has 2 attributes: productid and onhandqty. Both attributes are strings.
    ```

    Copied!content\_copy

    Gemini generates the `inventory` JSON array that contains 3 JSON objects.
4.  To insert the sample JSON data in the inventory.py file, in the Gemini response, click **Insert in current file** (![Gemini - insert in current file](https://cdn.qwiklabs.com/rqqAHJzWVn36fpBDgUmKEKBIsWqFpgHDHES0QFKLFX4%3D)). The contents of the file is similar to:

    ```
    inventory = [
        {
            "productid": "P001",
            "onhandqty": "10"
        },
        {
            "productid": "P002",
            "onhandqty": "20"
        },
        {
            "productid": "P003",
            "onhandqty": "30"
        }
    ]
    ```

    Copied!content\_copy
5.  To save the `inventory.py` file in the `home/user/hello-world` folder, in the IDE menu (![Code OSS main menu](https://cdn.qwiklabs.com/H8AIg8zPKj8LfgE5rJjMSqNVieIjiopITlMQfBWkz0I%3D)), click **File > Save**.

    You use this sample inventory data in the next subtask.

#### Add the GET /inventory list API method to the app

You now introduce API methods in the `app.py` file that can operate on the inventory data. To complete this subtask, you use the code generation feature in Gemini.

1. In the folder and file list in **Explorer**, open the `app.py` file by selecting it.
2.  Modify the flask import statement to add the `inventory.py` file and the `jsonify` library:

    ```
    from flask import Flask, render_template, jsonify
    from inventory import inventory
    ```

    Copied!content\_copy
3.  In the `app.py` file, position your cursor below the _app_ assignment statement:

    ```
    app = Flask(__name__)
    ```
4.  To let **Gemini** generate the code for the first API method, in the `app.py` file, enter the following comment:

    ```
    # Generate an app route to display a list of inventory items in the JSON format from the inventory.py file.
    # Use the GET method.
    ```

    Copied!content\_copy
5. Select the comment lines, including the blank line below the comment.
6.  Click the bulb (![Code OSS Gemini bulb](https://cdn.qwiklabs.com/tLYH7qWU%2BLK5Z3aeYQf6nH7omJ0LQhao5WaGbYeXKLk%3D)), and then in the **More Actions** menu, select **Generate code**.

    Gemini generates a function for the GET operation that returns a list of items from the `inventory.py` file. The function generally looks similar to this:

    ```
    @app.route('/inventory', methods=['GET'])
    def inventory_list():
        """Return a list of inventory items in JSON format."""
        return jsonify(inventory)
    ```

    Copied!content\_copy**Note:** To learn more about the `jsonify(inventory)` function, highlight the term and prompt Gemini to explain the code to you.
7.  To accept the generated code, hold the pointer over any part of the generate code response, then click **Accept**.

    **Important:** Gemini can generate more than one code snippet, and these snippets might differ from the snippet that is displayed above.
8. If the **app.route** and **return** statements in your generated code is different from the code shown above, replace the generated code snippet with the snippet displayed above. This should ensure that the lab works as intended.

#### Add the GET /inventory/ method to the app

Let's add another API method to return data about a specific inventory item, given its productID. If the productID is not found, the API returns the standard HTTP status code of 404.

1. Add a few blank lines.
2.  To let Gemini generate the code for this second API method, in the `app.py` file, enter the following comment:

    ```
    # Generate an App route to get a product from the list of inventory items given the productID.
    # Use the GET method.
    # If there is an invalid productID, return a 404 error with an error message in the JSON.
    ```

    Copied!content\_copy
3.  Select the 3 comment lines and the blank line that follows the comment, click the bulb (![Code OSS Gemini bulb](https://cdn.qwiklabs.com/tLYH7qWU%2BLK5Z3aeYQf6nH7omJ0LQhao5WaGbYeXKLk%3D)), and then in the **More Actions** menu, select **Generate code**.

    Gemini generates a function for the GET operation that returns the item from the inventory file whose productID is provided in the request, or the 404 status code if the product does not exist.

    ```
    @app.route('/inventory/<productid>', methods=['GET'])
    def inventory_item(productid):
        """Return a single inventory item in JSON format."""
        for item in inventory:
            if item['productid'] == productid:
                return jsonify(item)
        return jsonify({'error': 'Product not found'}), 404
    ```

    Copied!content\_copy
4. Hold the pointer over any part of the generate code response. To accept the generated code, in the toolbar, click **Accept**.
5. If the generated code is different from the code shown above, replace the generated code snippet with the snippet displayed above.

#### Rebuild and redeploy the app locally

You can run your app locally from your IDE using the Cloud Run emulator. In this case, _locally_ means on the workstation machine.

1. In the activity bar of your IDE, click **Cloud Code** (![Code OSS Cloud Code menu](https://cdn.qwiklabs.com/h7a1cGNlfuYGKBrCndl%2Fn9cDcLtr2yacmETamGQFgAs%3D)).
2. In the Cloud Run activity bar, click **Run App on Local Cloud Run Emulator** (![Cloud Run - run on local emulator](https://cdn.qwiklabs.com/z1o4I2oLA6FB2DV9wgz8KLptStQuC0l4PxaS%2Bq%2F3PVs%3D)).
3.  When prompted at the top of the screen to **Enable minikube gcp-auth addon to access Google APIs**, select **Yes**.

    Wait for the build and deploy to complete.
4.  Hold the pointer over the link to the hello-world service at the localhost URL, and click **Follow link**.

    A new tab is opened in the browser that displays a page indicating that the service is running.

#### Test the API methods

1. Follow the steps in the earlier task to run the app locally.
2.  After following the link to view the running app in a separate browser tab, append `/inventory` to the URL in this tab, and type Enter.

    The API returns a JSON response that contains the list of products from the `inventory.py` file.
3. Append `/{PRODUCTID}` to the URL that ends with `/inventory`, where `{PRODUCTID}` is a product ID in your inventory.
4.  Type Enter.

    The API returns a JSON response that contains data about the specific product.
5.  Replace the product ID with `XXXXX` and type Enter.

    XXXXX is not a valid product ID, so the API returns a JSON error response indicating that the product is not found.

### Task 7. Deploy the app to Cloud Run <a href="#step10" id="step10"></a>

You can now deploy the app to Cloud Run on Google Cloud.

1. In the activity bar main menu (![Code OSS main menu](https://cdn.qwiklabs.com/H8AIg8zPKj8LfgE5rJjMSqNVieIjiopITlMQfBWkz0I%3D)), click **View > Command Palette**.
2. In the command palette field, type **Cloud Code Deploy**, and then select **Cloud Code: Deploy to Cloud Run** from the list.
3. To enable the Cloud Run API for your project, click **Enable API**.
4. On the **Service Settings** page, for **Region**, select **`us-west1`**.
5.  Leave the remaining settings as their defaults, and then click **Deploy**.

    Cloud Code builds your image, pushes it to the registry, and deploys your service to Cloud Run. This may take a few minutes.

    **Note:** To see the detailed logs for the deployment, click **Show Detailed Logs**.
6. To view your running service, open the URL that is displayed in the Deploy to Cloud Run dialog.
7.  Test your service by appending the `/inventory`, and `/inventory/{PRODUCTID}` paths to the URL, and verify the response.

    To get the URL for the Cloud Run service inventory page, in Cloud Shell, run the following command:

    ```
    export SVC_URL=$(gcloud run services describe hello-world \
      --region us-west1 \
      --platform managed \
      --format='value(status.url)')
    echo ${SVC_URL}/inventory
    ```
