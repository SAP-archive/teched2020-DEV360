# PART 3: AUTOMATE SAP CLOUD PLATFORM OPERATIONS

In this section, you will utilize the powerful capabilities of the SAP Cloud Platform APIs to create an application that automates the process of generating and configuring the accounts on the SAP Cloud Platform.

## Scenario Overview

As the DevOps of your company, you receive many requests to create SAP Cloud Platform accounts for multiple R&D projects.

The task to create the accounts is manual, time-consuming, and error prone. Also, the accounts are similar, as they all follow the company’s guidelines in terms of the project structure, naming conventions, and other features.

In such scenarios, there is an increased need to automate the creation processes based on the predefined criteria.

SAP Cloud Platform now offers an enhanced **accounts hierarchy** based on **directories** and **custom properties**, which enables you to build an account structure that better fits your company’s business needs.
With the new **set of APIs**, you can now automate this process, enforce your guidelines, conventions, and save precious time.

In the exercise, you will use these capabilities to provide a solution that will result in the automation of the process to create accounts in SAP Cloud Platform for each R&D project, according to your company’s guidelines:

1.	Create a directory for the new project. 
2.	Create 3 subaccounts (one for each development stage – dev / test / prod).
3.	Add a custom property to each of the subaccounts.
4.	Configure the required entitlements for each subaccount.

The new **Directory** entity allows you to group several subaccounts so you can operate, manage and analyze them as a single entity.

Adding **Custom Properties** allows you to add any custom metadata relevant for you on subaccount/directory level. This allows you to identify, filter and manage multiple entities as groups based on certain criteria (regardless of the parent entity).

Once completed, the entire project structure can be created by a single click of a button (or integrated with your company’s automatic processes).

## Starter Application Overview

We prepared an existing application with both server and client components in order to save time and allow you to learn how to use the APIs.

Most of the server-side code is written in the server.js file that contains “missing pieces of code” that you will fill in as part of this exercise. The client-side (UI) of the application is already fully implemented.

## 1. Preparations

In this section, you will set up your workspace on SAP Business Application Studio and import the application.

1. From the [Trial Landing Page](https://cockpit.hanatrial.ondemand.com/cockpit#/home/trial), open **SAP Business Application Studio**.  

<p align="center" width="100%">
   <img src="/exercises/part3/images/trial_landing_page_bas.png" width="60%"/>
</p>  

If prompted with this screen, click **OK**.  

<p align="center" width="100%">
   <img src="/exercises/part3/images/bas_consent.png" width="80%"/>
</p>  

2. Create a new Dev Space of type **Basic**.  
Enter a name for your space. There's no need to select any extension.

<p align="center" width="100%">
   <img src="/exercises/part3/images/create_space.png" width="30%"/>
</p>  

3. Wait for the status to be RUNNING and then click on the name of the space to open it.  

<p align="center" width="100%">
   <img src="/exercises/part3/images/space_running.png" width="50%"/>
</p>  

4. Click on **Open Workspace**.  

<p align="center" width="100%">
   <img src="/exercises/part3/images/open_workspace.png" width="40%"/>
</p>  

5. Click **Open**.  

<p align="center" width="100%">
   <img src="/exercises/part3/images/open.png" width="40%"/>
</p>  

6. To use the starter application, you need to add it to your workspace.  
Download the “cei-demo-master” folder from [here](https://sap-my.sharepoint.com/:f:/p/michal_keidar/EpmsN58JG-5KlfCMf0ql7XsBxpgJEYq9YGGIhIVPVOJa2A?e=HuO3Fl).  
Extract the ZIP file, and then **Drag and drop** the "cei-demo-master" folder to your SAP Business Application Studio workspace.  
If for any reason, dragging and dropping the folder doesn't work for you, import them manually to your workspace.  
  
<p align="center" width="100%">
  <img src="/exercises/part3/images/cei_demo_master.png" width="40%"/>
</p>  

7. Open the **server.js** file, located in the cei-demo-master folder.  

<p align="center" width="100%">
  <img src="/exercises/part3/images/server_file.png" width="40%"/>
</p>  

8. Locate the set of the configuration constants.  
Fill in the values for the **CLIENT_ID**, **CLIENT_SECRET**, and **AUTH_URL** using the values obtained from the Binding (Part 2, Section 1, Step 4).  
Fill in the values for the **USER_EMAIL** and **PASSWORD** with your SAP Cloud Platform credentials.  
Fill in the values for the **REGION** with the region of your Trial account (eu10 / us10). Make sure you fill it in **all 3 locations**.  
**Save your changes**.  

<p align="center" width="100%">
  <img src="/exercises/part3/images/constants_empty.png" width="60%"/>
</p>  
  
Example:  
<p align="center" width="100%">
  <img src="/exercises/part3/images/constants_filled.png" width="60%"/>
</p>  
  

## 2. Automate Directory Creation

In this section, you will implement the “createDirectory()” function which will create a directory.  

1. In the server.js file, copy the following code snippet to the "/submit" endpoint handler, instead of the entire comment "PLACE YOUR CODE HERE".  
This code retrieves the **oAuth token** that is used to authenticate to SAP Cloud Platform.  

```javascript
token = await getAccessToken();
```  

2. Copy and paste the following function call **after** the call to getAccessToken().  
The directory name is given as an input from the UI, and the description is provided in the second parameter.  

```javascript
let directory = await createDirectory(name, "TechEd Directory");
```  

3. The "/submit" endpoint handler format should be as in this example:  

<p align="center" width="100%">
  <img src="/exercises/part3/images/create_directory_call.png" width="60%"/>
</p>  

4. Now we need to implement the **createDirectory()** function.  
Locate it in the file, copy the following snippet, and paste it to the location: “PLACE CODE FOR DIRECTORY CREATION HERE”.  

```javascript
let response = await request('POST',
    `${ACCOUNTS_SERVICE_URL}<CREATE-DIRECTORY URL>`, {},
    {
       displayName: name,
       description: description
    });
let directory = response.body;
return directory;
```  

**Save your changes**.  

5. Back in the [SAP Cloud Platform - Core Service APIs](https://accounts-service.cfapps.eu10.hana.ondemand.com/swagger-index.html), in the **Accounts** service tile, open the **Directory Operations** group and locate the URL endpoint used to create a directory.  

<p align="center" width="100%">
  <img src="/exercises/part3/images/create_directory_url.png" width="60%"/>
</p>  

6. Copy the URL and paste it instead of the following placeholder: **\<CREATE-DIRECTORY URL\>** in the createDirectory() function.  

7. To get detailed explanations about the required body parameters, click on the **Model** tab in the **Parameters** section.  

<p align="center" width="100%">
  <img src="/exercises/part3/images/payload_model_tab.png" width="60%"/>
</p>  

8. The required parameters are marked with red asterisk.  

<p align="center" width="100%">
  <img src="/exercises/part3/images/payload_model_tab_open.png" width="60%"/>
</p>  

9. **Your createDirectory() function is now ready!**  

<p align="center" width="100%">
  <img src="/exercises/part3/images/create_directory_function.png" width="60%"/>
</p>  

## 3. Automate Subaccount Creation

In this section, you will create 3 subaccounts in the directory, by implementing the “createSubaccountInDirectory()” function.  

1. Copy and paste these 3 function calls into the "/submit" endpoint handler, after the call to createDirectory().  
These calls will eventually create 3 subaccounts in the directory, each subaccount with its own name, description and a custom property marking the development stage (development / test / production).  

```javascript
let subaccount1 = await createSubaccountInDirectory(directory, {
    region: REGION_KEY,
    subdomain: "devsa",
    name: "Dev Subaccount",
    description: "Subaccount for development",
    devStage: "development"
});

let subaccount2 = await createSubaccountInDirectory(directory, {
    region: REGION_KEY,
    subdomain: "testsa",
    name: "Test Subaccount",
    description: "Subaccount for testing",
    devStage: "test"
});

let subaccount3 = await createSubaccountInDirectory(directory, {
    region: REGION_KEY,
    subdomain: "prodsa",
    name: "Prod Subaccount",
    description: "Subaccount for production",
    devStage: "production"
});
```  

**Save your changes**.  

2. The "/submit" endpoint handler should be in the following format:  

<p align="center" width="100%">
  <img src="/exercises/part3/images/create_subaccounts_calls.png" width="60%"/>
</p>  

3. In this step we will implement the **createSubaccountInDirectory()** function.  
Locate it in the code, copy the code snippet below, and paste it instead of the comment: “PLACE CODE FOR SUBACCOUNT CREATION HERE”.  
This function executes a POST request to SAP Cloud Platform to start an async job for creating a new subaccount in a directory.  
The directory’s GUID is being provided as value for the “parentGUID” parameter.  
The "region" parameter defines in which region the subaccount is created.  
The “customProperties” contains a key called “devStage”, indicating in which development stage the subaccount is in. The possible dev stages are:  
* development
* test
* production  

Creating a subaccount may take several seconds.  
During the creation process, the status of the async operation will be "In Progress".  
Upon completion, the status will be either "COMPLETED" or "FAILED".  

Copy the following code snippet, and paste it instead of the comment: “PLACE CODE FOR SUBACCOUNT CREATION HERE”.

```javascript
let response = await request('POST',
    `${ACCOUNTS_SERVICE_URL}<CREATE-SUBACCOUNT URL>`, {},
    {
        parentGUID: directory.guid,
        region: inputParameters.region,
        subdomain: `${inputParameters.subdomain}-${uuid.v4().substring(0, 5)}`,
        displayName: inputParameters.name,
        description: inputParameters.description,
        customProperties: [{
            key: "devStage",
            value: inputParameters.devStage
        }]
    });

let subaccount = response.body;

log(`Subaccount created asynchronously: ${subaccount.displayName}, 
${subaccount.guid}. Waiting for completion...`);

await pollForCompletion(`${ACCOUNTS_SERVICE_URL}${response.headers['location']}`);
log(`Subaccount creation operation COMPLETED`);

return subaccount;
```  

**Save your changes**.  

4. Back in the [SAP Cloud Platform - Core Service APIs](https://accounts-service.cfapps.eu10.hana.ondemand.com/swagger-index.html), in the **Accounts** service tile, open the **Subaccount Operations** group and locate the API’s URL endpoint to create a subaccount.  

<p align="center" width="100%">
  <img src="/exercises/part3/images/create_subaccount_url.png" width="60%"/>
</p>  

5. Copy the URL and paste it instead of the following place holder: **\<CREATE-SUBACCOUNT URL\>** in the **createSubaccountInDirectory()** function code.  

6. The "createSubaccountInDirectory()" function should be in the following format:  

<p align="center" width="100%">
  <img src="/exercises/part3/images/create_subaccount_function.png" width="70%"/>
</p>  

## 4. Automate Entitlements Assignment

Subaccounts can be entitled to the services that are visible in the global account.  
Each service can have one or more plans, and these plans need to be assigned to the subaccounts.  
  
In this section, you will implement the “entitleSubaccount()” function to assign entitlements to each subaccount that you’ve created.  
As an example, we will assign the **Application Runtime**, and **Document Translation** services.  

1. Copy and paste these 3 function calls into the "/submit" endpoint handler, after the call to create the third subaccount in a directory.  
These calls will entitle the 3 subaccounts to the **Application Runtime**, and **Document Translation** services.  
**Remember:** Initially our trial subaccount was entitled with **4 units** of Application Runtime, MEMORY plan. Then we assigned *trial* with 0 units. This leaves us with 4 units to assign to our dev, test and prod subaccounts.  

```javascript
await entitleSubaccount(subaccount1, {
    appRuntime: 1,
    documentTranslation: true
});

await entitleSubaccount(subaccount2, {
    appRuntime: 1,
    documentTranslation: true
});

await entitleSubaccount(subaccount3, {
    appRuntime: 2,
    documentTranslation: true
});
```  

**Save your changes**.  

2. Implement the **entitleSubaccount()** function.  
Locate the function in the server.js file, copy the below code snippet, and paste it instead of the comment: “PLACE CODE FOR SUBACCOUNT ENTITLEMENT HERE”.  
This function executes a PUT request to SAP Cloud Platform to start an async operation that assigns the two following service plans to every subaccount:  
* Application Runtime's "MEMORY" plan.
* Document Translation’s "trial" plan.  

The requested service plans and their respective amounts are specified in the request body.  
Since this operation is asynchronous, we use the pollForCompletion() function to periodically check its status.  

Copy the following code snippet, and paste it instead of the comment: “PLACE CODE FOR SUBACCOUNT ENTITLEMENT HERE”.  

```javascript
response = await request('PUT',
        `${ENTITLEMENTS_SERVICE_URL}/entitlements/v1/subaccountServicePlans`, {}, {
    subaccountServicePlans: [{
        serviceName: 'APPLICATION_RUNTIME',
        servicePlanName: 'MEMORY',
        assignmentInfo: [{
            amount: entitlements.appRuntime,
            subaccountGUID: subaccount.guid
        }]
    }, {
        serviceName: 'document-translation',
        servicePlanName: 'trial',
        assignmentInfo: [{
            enable: entitlements.documentTranslation,
            subaccountGUID: subaccount.guid
        }]
    }]
});

log(`Entitled subaccount. Waiting for completion...`);

await pollForCompletion(`${ENTITLEMENTS_SERVICE_URL}${response.headers['location']}`);
log(`Entitlement job COMPLETED`);
```  

**Save your changes**.  

3. **Your entitleSubaccount() function is ready!**  

<p align="center" width="100%">
  <img src="/exercises/part3/images/entitle_subaccount_function.png" width="60%"/>
</p>  

4. The relevant code in the "/submit" endpoint handler should be in the following format:  

<p align="center" width="100%">
  <img src="/exercises/part3/images/create_subaccounts_calls.png" width="50%"/>
</p>  

<p align="center" width="100%">
  <img src="/exercises/part3/images/entitle_subaccount_calls.png" width="40%"/>
</p>  

## 5. Run the Application

In this section, you will run the application with the SAP Business Application Studio.  

1. In SAP Business Application Studio, open the Terminal.  
Right-click on the **"cei-demo-master"** folder and choose **Open in Terminal**.  

<p align="center" width="100%">
  <img src="/exercises/part3/images/open_in_terminal.png" width="40%"/>
</p>  

2. In the Terminal, execute the following command:  

```
npm install
```  

<p align="center" width="100%">
  <img src="/exercises/part3/images/npm_install.png" width="40%"/>
</p>  

3. You will see the following screen once the command has been successfully executed.  

<p align="center" width="100%">
  <img src="/exercises/part3/images/npm_install_done.png" width="40%"/>
</p>  

4. Execute this command to run the application.  

```
npm start
```  

<p align="center" width="100%">
  <img src="/exercises/part3/images/npm_start.png" width="40%"/>
</p>  

5. Click on the **Expose and Open** button to open the application in a new browser tab.  

<p align="center" width="100%">
  <img src="/exercises/part3/images/expose_and_open.png" width="60%"/>
</p>  

6. If required, press ‘Enter’ in the popup dialog.  

<p align="center" width="100%">
  <img src="/exercises/part3/images/press_enter.png" width="60%"/>
</p>  

7. **Your application is running!**  
Proceed to Part 4 to use it in a productive scenario.  

<p align="center" width="100%">
  <img src="/exercises/part3/images/runtime_empty.png" width="60%"/>
</p>  


## Summary

Now that you have successfully created an application that automates the process of generating and configuring accounts on the SAP Cloud Platform, proceed to - [PART 4: USE THE NEW APPLICATION IN A PRODUCTION SCENARIO](/exercises/part4/README.md)

