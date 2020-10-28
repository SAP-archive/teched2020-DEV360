# PART 5: RETRIEVE USAGE INFORMATION

In this section, you will use the new REST APIs to retrieve the latest usage information for your global account.  
You will perform the following steps:  
* Obtain authentication information to use the REST APIs.
* Generate usage for a service in your global account.
* Try out the API to view the usage for your global account.  

## 1. Obtain Authentication Information for using the Usage Data Management REST APIs

In this section, you will use the CLI for SAP Cloud Platform to obtain the required information to authenticate to the **Usage Data Management (uas)** service so that you can use the Usage Data Management REST APIs. You will use the subaccount created in [PART 1](/exercises/part1/README.md).  

1. In your subaccount, create an instance of the **Usage Data Management (uas)** service, **reporting-ga-admin** plan.  
Replace the **\<new_subaccount_id\>** with the ID of your new subaccount.  
**Note:** uas-instance is the name for the new instance.  

**TBD**
```
sapcp create services/instance -sa <new_subaccount_id>
```  

2. Create a **Binding**.  
Bindings generate credentials to use service instances.  
Replace the **\<new_subaccount_id\>** with the ID of your subaccount.  
**Note:** uas-binding is the name for the binding.  

**TBD**  
```
sapcp create services/binding -sa <new_subaccount_id>
```  

3. Get the content of the binding you created.    
Replace the **\<new_subaccount_id\>** with the ID of your new subaccount.
   
**TBD**  
```
sapcp get services/binding -sa <new_subaccount_id>
```  

4. Extract the values from the binding for the following parameters:  
* clientid
* clientsecret
* url
      
**Save these values** as you will need them later in the exercise. These parameters will be used to obtain the **oAuth token** required to authenticate with the API.  

<p align="center" width="100%">
   <img src="/exercises/part5/images/cli_binding_parameters.png" width="60%"/>
</p>  


## 2. Create Usage for Document Translation Service

The **Document Translation** service, **trial** plan, provides an API that allows you to translate documents of various formats into multiple languages.  
In this section, you will use the SAP Cloud Platform cockpit to create usage for this service, that will later be retrieved using the API.  
**Note:** the **Document Translation** service, **trial** plan, is offered on **EU10 region only**, so you must use a subaccount on EU10. If you don't have one, create it.

1. Back in the cockpit, choose any subaccount on the EU10 region, and verify it is assigned with quota of the **Document Translation** service, **trial** plan.  
Enter the subaccount, and the **Services > Service Marketplace**.    

<p align="center" width="100%">
   <img src="/exercises/part5/images/cockpit_marketplace.png" width="60%"/>
</p>  

2. Locate the **Document Translation** service and click on the 3 dots menu button to create an instance.  

<p align="center" width="100%">
   <img src="/exercises/part5/images/document_translation_create_instance.png" width="40%"/>
</p>  

3. In the **New Instance** dialog, choose **Other** as **Runtime Environment**, enter a name for the instance, and click **Create Instance**.  

<p align="center" width="100%">
   <img src="/exercises/part5/images/document_translation_new_instance_dialog.png" width="60%"/>
</p>  

4. In the **Success** popup dialog, choose **View Instance**.  

<p align="center" width="100%">
   <img src="/exercises/part5/images/view_instance.png" width="40%"/>
</p>  

5. On the right-hand side, click on the 3 dots menu button and choose **Create Binding**.  

<p align="center" width="100%">
   <img src="/exercises/part5/images/document_translation_create_binding.png" width="50%"/>
</p>  

6. In the **New Binding** dialog, enter a name for the binding and click **Create**.  

<p align="center" width="100%">
   <img src="/exercises/part5/images/document_translation_new_binding_dialog.png" width="40%"/>
</p>  

7. Click on the new binding’s 3 dots menu button and choose **View**.  

<p align="center" width="100%">
   <img src="/exercises/part5/images/view_binding.png" width="40%"/>
</p>  

8. From the opened dialog, save the following properties:  
* clientid
* clientsecret
* identityzone  

9. Open the [Document Translation service’s page](https://api.sap.com/api/documenttranslation/resource) on **SAP API Business Hub** and **Log On**.  
Click on **Configure Environments**.  

<p align="center" width="100%">
   <img src="/exercises/part5/images/api_hub_configure_environments.png" width="60%"/>
</p>  

10. Enter a **Display Name** for the Environment.  
Then enter the **Client Id** and **Secret** retrieved from the binding.  
In the **subaccount** field enter the **identityzone**, and also enter the **region** (eu10/us10).  
Click **Save**.  

<p align="center" width="100%">
   <img src="/exercises/part5/images/save_environment.png" width="60%"/>
</p>  

11. In the **POST /translation** request, click on the **Try out** button.  

<p align="center" width="100%">
   <img src="/exercises/part5/images/Try_out.png" width="60%"/>
</p>  

12. Now you will try out the API that translates a file.  
Enter the desired **sourceLanguage** and **targetLanguage** and browse for a file to be translated (for example a .docx file).  
Choose **Execute**.  
From the result choose **Download file** to see the translated file.  
**Note:** the **Document Translation** service measures the usage of their service based on the **number of translated characters**.    
  
## 3. Try Out the API to View the Usage of your Global Account

In this section, you will work with the **SAP Cloud Platform - Core Service APIs** (based on Swagger) and view the usage of your global account.  
**NOTE: It usually takes 1-2 days until the usage is returned in the API and shown in the cockpit.**  

1. Execute the following cURL command in the Windows command prompt (CMD), or Terminal for Mac OS.  
**Note:** replace **\<clientid\>**, **\<clientsecret\>** and **\<url\>** with the values you obtained in this part, section 1, step 4.  
Replace **\<user email\>** and **\<password\>** with your SAP Cloud Platform credentials.  
**IMPORTANT: Make sure to remove any trailing spaces**.  

```
For Windows OS:
curl -L -X POST "<url>/oauth/token" ^
-H "Content-Type: application/x-www-form-urlencoded" ^
-u "<clientid>:<clientsecret>" ^
-d "grant_type=password" ^
-d "username=<user email>" ^
-d "password=<password>"

For Mac OS:
curl -L -X POST '<url>/oauth/token' \
-H 'Content-Type: application/x-www-form-urlencoded' \
-u '<client_id>:<client_secret>' \
-d 'grant_type=password' \
-d 'username=<user email>' \
-d 'password=<password>'
```  

<p align="center" width="100%">
   <img src="/exercises/part5/images/curl_get_token.png" width="80%"/>
</p>  

2. The **oAuth token** is the **value** of the **access_token** parameter in the response body.  
**Save this value** as you will need it later in the exercise.   
**Note:** The value of the "access_token" ends right before the "token_type". Make sure you copy only the value of the "access_token".   
      
<p align="center" width="100%">
  <img src="/exercises/part5/images/access_token_start.png" width="60%"/>
</p>  

<p align="center" width="100%">
  <img src="/exercises/part5/images/access_token_end.png" width="60%"/>
</p>  

3. Back in the [SAP Cloud Platform - Core Service APIs](https://accounts-service.cfapps.eu10.hana.ondemand.com/swagger-index.html), click on the **Resource Consumption** tile to view the APIs related to the Resource Consumption service.  

<p align="center" width="100%">
  <img src="/exercises/part5/images/resource_consumption.png" width="30%"/>
</p>  

4. In the top-right corner, click on the **Authorize** button.  

<p align="center" width="100%">
  <img src="/exercises/part5/images/resource_consumption_autorize.png" width="50%"/>
</p>  

5. Enter the following information:    
**Bearer \<token\>**    
where \<token\> is the oAuth access token acquired in the previous section “Obtain Authentication Information”.    
**Note:** Make sure there is exactly **one space** between “Bearer” and the token.    
Click on **Authorize** and **Close**.    
      
<p align="center" width="100%">
  <img src="/exercises/part5/images/apis_authorize.png" width="50%"/>
</p> 
   
6. In case you failed to get authorization, make sure you copied the correct value of the "access_token" and that you didn’t include the "token_type" value (see step 2).  

7. Open the **Usage and Cost Management** section and the **GET /reports/v1/monthlyUsage** API.  

<p align="center" width="100%">
  <img src="/exercises/part5/images/get_monthly_usage_api.png" width="60%"/>
</p>  

8. Click on the **Try it out** button to execute the API and to get the **monthly usage of your global account**.  

<p align="center" width="100%">
  <img src="/exercises/part5/images/resource_consumption_try_it_out.png" width="30%"/>
</p>  

9. Fill in the **fromDate** and **toDate** parameters in the following format: YYYYMM, e.g., 202012 for December (12) 2020.  
Click **Execute**.  

<p align="center" width="100%">
  <img src="/exercises/part5/images/execute.png" width="60%"/>
</p>  

10. The results are presented in the **Response body**.  

**TBD screenshot**  

11. You should see a section per service, and the usage is presented in the “usage” field.  

**TBD screenshot**  

12. The usage information is also presented in the cockpit.  
Enter your global account’s **Usage Analytics** view.  

**TBD screenshot**  


## Congratulations! You have completed the exercise.










