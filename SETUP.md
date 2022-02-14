# Setup and deploy Liquid Prep Backend in IBM Cloud

Currently the backend service is deployed and hosted on IBM Cloud Liquid Prep's account.
You can also setup and deploy the Liquid Prep backend service on your own IBM Cloud account.

Instructions on how to setup, configure and deploy the backend service is as follows:

## Pre-requisites

1. IBM Cloud account:

   - [Create an IBM Cloud account](https://cloud.ibm.com/registration)
   - [Install IBM Cloud CLI](https://cloud.ibm.com/docs/cli?topic=cloud-cli-getting-started)
   - [Setup the Cloud Functions CLI plug-in](https://cloud.ibm.com/docs/openwhisk?topic=openwhisk-cli_install)
   - **Create IAM API key**;

     - Login to IBM Cloud account.
     - Click on **Manage** tab on top right of the IBM Cloud dashboard. And click on **Access (IAM)** option to open **Manage access and users** dashboard.
     - Select **API keys** option on left pane of the dashboard.
     - Select **Create an IBM Cloud API key** button on right of the **API keys** dashboard.
        <p align="middle">
            <img src="images/backend/IAM/iamKey.PNG" width ="30%" height="30%">
        </p>

     - Enter an API key name and description. Example,
        <p align="middle">
            <img src="images/backend/IAM/createIAMApikey.PNG" width ="30%" height="30%">
        </p>

     - An IAM API key will be created, copy and/or download the key and secure it safely.
       **NOTE:** This IAM API key is required later for Liquid Prep project deployment and IBM Cloud CLI login. Please copy/download and store it in a secure place. If the IAM API key is **NOT** copied/downloaded and stored in secure place, you will have to create new IAM API key.

   - **Create Resource Group**;

     - Click on **Manage** tab on top right of the IBM Cloud dashboard. And click on **Account** option to open **Account** dashboard.
     - Select **Resource groups** option on the left panel of the dashboard. Usually a **Default** resource group will be created when a cloud account is created. If not a new Resource group can be created by clicking on the **Create** button on the right of the **Resource groups** dashboard.
        <p align="middle">
            <img src="images/backend/account/resourceGrp.PNG" width ="30%" height="30%">
        </p>

   - **Create Cloud Foundry Organization**;

     - From the **Account** dashboard, select **Cloud Foundry orgs** option on the left pane to open **Cloud Foundry Orgs** dashboard.
     - Click on **Create** on the top right of the dashboard to create new Organization. If an organization already exists, you can use the same.
        <p align="middle">
            <img src="images/backend/account/organization.PNG" width ="30%" height="30%">
        </p>

   - **Create Space**;
     - From the **Cloud Foundry Orgs** dashboard, click on the Name of the organization to open the **Space** tab for the organization.
     - Click on the **Add a space** button the top right of the dashboard to create new Space. If a space already exists, you can use the same.
        <p align="middle">
            <img src="images/backend/account/space.PNG" width ="30%" height="30%">
        </p>

2. Git:

   - [Install Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git/)
   - [Configure Git](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup)
   - [Git account setup and configuration](https://git-scm.com/book/en/v2/GitHub-Account-Setup-and-Configuration)

3. Liquid Prep project:

   - [Git clone Liquid Prep project](https://github.com/Liquid-Prep/Liquid-Prep)

4. The Weather Company API Key:

   - Contact [The Weather Company](https://www.ibm.com/products/weather-company-data-packages/details) to register and subscribe the 5 day weather forecast API and obtain an API key.

5. Node and NPM:
   - [Install Node and NPM](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm)

## Setup IBM Cloud Functions

Follow the instructions to setup and configure IBM Cloud Functions.

- Create a new IBM cloud account. If you already have an account, please log in to account.
- Select **IBM Cloud Functions** icon on left the pane of the IBM Cloud account dashboard <br>
<p align="middle">
    <img src="images/backend/cloudFunctions/dashboard_cloudFunctions.PNG" width ="30%" height="30%">
</p>

&nbsp; &nbsp; &nbsp; &nbsp; Or you can search for **Functions** in search bar and select **Functions**.

<p align="middle">
    <img src="images/backend/cloudFunctions/searchCF.PNG" width ="30%" height="30%">
</p>

- Select **Actions** option on the left pane of **IBM Cloud Functions** dashboard.

<p align="middle">
    <img src="images/backend/cloudFunctions/actionsCF.PNG" width ="30%" height="30%">
</p>

- Create new Actions by clicking the **Create** on top right of the dashboard, enter Action Name as **liquid-prep-action**. Create new Package **liquidPrep**. Select **Node.js 12** as Runtime.

<p align="middle">
    <img src="images/backend/cloudFunctions/createActionCF.PNG" width ="30%" height="30%">
</p>

- Go back to **IBM Cloud Functions** dashboard and select **APIs** option on the left pane.

<p align="middle">
    <img src="images/backend/cloudFunctions/api_cloudFunctions.PNG" width ="30%" height="30%">
</p>

- Select **Create API** option on top right of the dashboard, enter API name as **liquidPrep-cf-api**. Let the **Base path for API** be default **/liquidPrep-cf-api**. Let other settings be default values, unless other specific entries are required. Scroll down the page and select **Create**.

<p align="middle">
    <img src="images/backend/cloudFunctions/createAPI_CF.PNG" width ="30%" height="30%">
</p>

- Once API is created, select the API **liquidPrep-cf-api**, select **Manage Sharing and Keys** on the left pane of the API dashboard. Enable **Include API in organization-level Shared APIs view**.

<p align="middle">
    <img src="images/backend/cloudFunctions/shareAPI_CF.PNG" width ="30%" height="30%">
</p>

## Setup IBM Cloudant

Follow the instructions to setup and configure IBM Cloudant.

- Enter **Cloudant** in the IBM Cloud search bar and select **Cloudant**.

  <p align="middle">
      <img src="images/backend/cloudant/searchCloudant.PNG" width ="30%" height="30%">
  </p>

- Next configure the Cloudant DB,

  - Under **Select an environment** section, enter Instance Name as **Cloudant-liquidPrep**.

  - Select **IAM** as Authentication method.

  - Select a suitable pricing Plan – Lite, Standard and Standard on Transaction Engine.

  <p align="middle">
      <img src="images/backend/cloudant/configureCloudant.PNG" width ="30%" height="30%">
  </p>

- Select **Create** on the bottom right pane of Cloudant dashboard. A message will be displayed to say that the instance is being provisioned, which returns you to the Resource list. From the Resource list, you see the status for your instance is, **Provision in progress.**

  <p align="middle">
      <img src="images/backend/cloudant/activeCloudant.PNG" width ="30%" height="30%">
  </p>

- When status of the instance changes to **Active**, click the **Cloudant-liquidPrep** instance and select **Service Credentials** tab on left pane of dashboard. Select **New Credential**, enter Name as **liquid-prep** and Role as **Manager**. A service credential will be created.

  <p align="middle">
      <img src="images/backend/cloudant/serviceCredsCloudant.PNG" width ="30%" height="30%">
  </p>

- Select **Manage** tab on the left pane and select **Launch Dashboard** on the top right of the page. It will launch a Cloudant dashboard to create new database.

- On the Databases page, select **Create Database** on the top right of the Cloudant dashboard.
- Enter Database name as **liquid-prep-crops**. Select the Partitioning option as **Non-partitioned**. And click on **Create** button at the bottom.

   <p align="middle">
       <img src="images/backend/cloudant/createDBCloudant.PNG" width ="15%" height="30%">
   </p>

  - The**liquid-prep-crops** database will be created and listed in Databases page.

- Select **liquid-prep-crops** and click on **Create Document** on top right of the page. A document with auto generated **\_id** key will open.

   <p align="middle">
       <img src="images/backend/cloudant/createDoc_cloudant.PNG" width ="30%" height="30%">
   </p>

- Go to Liquid Prep project directory `~/LiquidPrep-Backend/backend/resources/crops`. Open each crop document, copy the contents in the document and paste it in the **New Document** that was opened in **liquid-prep-crops** database and click **Create Document** button.

  - Example for Corn crop;
  <p align="middle">
      <img src="images/backend/cloudant/createDoc_cloudant_corn.PNG" width ="30%" height="30%">
  </p>

  - Corn document will be created and listed in **liquid-prep-crops** database.
  <p align="middle">
      <img src="images/backend/cloudant/liquidPrep_cloudant_cropsList.PNG" width ="30%" height="30%">
  </p>

- Similarly, repeat previous step for all the other crops document.

## Deploy the Backend on IBM Cloud

After seeting up and configuring IBM Cloud Functions and Cloudant DB, the Liquid Prep backend project needs to be built, bundled and deployed to IBM Cloud Functions to expose Cloud Functions API for Liquid Prep application. <br>

- Go to Liquid Prep project directory `~/LiquidPrep-Backend/backend/liquid-prep-cf` and create **.env** file.
- Add following entries to the **.env** file;

  - ```
    IAM_API_KEY=xxxxxx
    CLOUD_FUNCTIONS_URL=https://xxxxxx.appdomain.cloud/liquidprep-cf-api
    CLOUDANT_DB_URL=https://xxxxxx-bluemix.cloudant.com/
    CLOUDANT_DB_NAME=liquid-prep-crops
    WEATHER_API_KEY=xxxxxxxxxx
    ```

    - **IAM_API_KEY:** <br>
      It is the API key created at the beginning when an IBM Cloud account is created. Please refer to the **Pre-requisites** section on how to create/obtain the IAM API key.

    - **CLOUD_FUNCTIONS_URL:**

      - Go to IBM Cloud dashboard.
      - Click on the **Navigation Menu** on the top left corner of the dashboard.
      - Select **API Management** option.

      <p align="middle">
        <img src="images/backend/envEntries/apiManage.PNG" width ="30%" height="30%">
      </p>

      - Select **Shared APIs** in **API Management** dashboard.
      - The **Route** value in **Shared APIs** dashboard is the **CLOUD_FUNCTIONS_URL** value.
        <p align="middle">
            <img src="images/backend/envEntries/sharedApi.PNG" width ="30%" height="30%">
        </p>

    - **_CLOUDANT_DB_NAME: liquid-prep-crops_** <br>
      It is the Cloudant database name which was created to add the crop documents.

    - **_CLOUDANT_DB_URL:_** <br>
      The Cloudant DB URL can be obtained from its **Manage** dashboard.

      - Go to IBM CLoud dashboard.
      - Click on the **Navigation Menu** on the top left corner of the dashboard.
      - Select **Resource List** option.
      - Select **Cloudant-liquidPrep** instance under **Services** in **Resource list** dashboard.

        <p align="middle">
        <img src="images/backend/envEntries/cloudantService.PNG" width ="30%" height="30%">
        </p>

      - The **External Endpoint (preferred)** value is the **CLOUDANT_DB_URL** value.
        <p align="middle">
            <img src="images/backend/envEntries/cloudantEndpoint.PNG" width ="30%" height="30%">
        </p>

    - **_WEATHER_API_KEY:_** <br>
      The Weather API key is obtained by subscribing to The Weather Company API services. Please refer to point 4 in the [Pre-requisites](#pre-requisites) section.

- Open command terminal and execute `npm install` in project directories `~/LiquidPrep-Backend/backend/liquid-prep-cf` and `~/LiquidPrep-Backend/backend/common`.
- Log into IBM Cloud account from command terminal with **ibmcloud** CLI. Execute the login command,

  ```text
  ibmcloud login --apikey <IAM API key> -g <Resource Group> -o <organisation> -s <space> -r <region>
  ```

  - **--apikey**: <br>
    It is the **API key** created at the beginning when an IBM Cloud account is created. Please refer to the **Pre-requisites --> IBM Cloud account --> Create IAM API key** section on how to create/obtain the IAM API key.

  - **-g**: <br>
    It is the **Resource group** of the cloud account. Usually a **Default** resource group will be created. If not you can create a new resource group and enter. <br>
    Please refer to the **Pre-requisites --> IBM Cloud account --> Create Resource Group** section on how to create/obtain the Resource group.

  - **-o**: <br>
    It is the **Cloud Foundry Organization** of the cloud account. Please refer to the **Pre-requisites --> IBM Cloud account --> Create Cloud Foundry Organization** section on how to create/obtain the Cloud Foundry Organization.

  - **-s**: <br>
    It is the **Space** in the **Cloud Foundry Organization** of the cloud account. Please refer to the **Pre-requisites --> IBM Cloud account --> Create Space** section on how to create/obtain the Space.

  - **-r**: <br>
  It is the **Region** of the cloud account. Region can be obtained in the selected **Cloud Foundry Organization** dashboard beside the **Space** Name.
    <p align="middle">
    <img src="images/backend/account/space.PNG" width ="30%" height="30%">
    </p>

- Navigate to project directory `~/LiquidPrep-Backend/backend/liquid-prep-cf` from command terminal and execute `npm run deploy-dev-api`.

- Once the deployment is successful, go to IBM Cloud Functions dashboard, select **Actions** tab on the left pane and you can see **liquid-prep-action** instance in the **Actions** dashboard.

  <p align="middle">
      <img src="images/backend/cloudFunctions/liquidPrep-Actions-CF.PNG" width ="30%" height="30%">
  </p>
