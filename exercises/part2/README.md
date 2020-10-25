# PART 2: GET FAMILIAR WITH THE REST APIs FOR SAP CLOUD PLATFORM

In this part, you will familiarize yourself with the new REST APIs that are used to automate operations involving your SAP Cloud Platform account entities.

You will perform the following steps:

1.	Obtain authentication information to use the REST APIs.
2.	Try out the API to get information for all subaccounts.
3.	Try out the API to get information about all assigned entitlements.

API documentation of the new APIs for SAP Cloud Platform is available via the popular Swagger UI interface that lets you try out the API calls directly in the browser.


## 1. Obtain Authentication Information

In this section, you will use the CLI for SAP Cloud Platform to obtain the authentication information necessary to use the SAP Cloud Platform REST APIs.

1. In your new subaccount, create an instance of the **Cloud Management (cis)** service, **central** plan.
Replace the **<new_subaccount_id>** with the ID of your new subaccount.
**Note:** *cis-central-instance* is the name for the new instance.  

```
sapcp create services/instance --name cis-central-instance --offering-name cis --plan-name central -sa <new_subaccount_id>
```

2. Create a **Binding** for the instance.  
Bindings generate credentials to use service instances.  
Replace the **<new_subaccount_id>** with the ID of your new subaccount.  
**Note:** *cis-central-binding* is the name for the binding.  

```
sapcp create services/binding --name cis-central-binding --instance-name cis-central-instance -sa <new_subaccount_id>
```  

3. Get the content of the binding you created.  
Replace the **<new_subaccount_id>** with the ID of your new subaccount.  

```
sapcp get services/binding --name cis-central-binding -sa <new_subaccount_id>
```  

4. Extract the values from the binding for the following parameters:  
* clientid
* clientsecret
* url
   
   **Save these values** as you will need them later in the exercise. These parameters will be used to obtain the **oAuth token** required to authenticate with the SAP Cloud Platform APIs.  
   
<p align="center" width="100%">
   <img src="/exercises/part2/images/cli_binding_parameters.png" width="60%"/>
</p>

5. Execute the following cURL command in the Windows command prompt (CMD), or Terminal for Mac OS.
   
   **Note:** replace **\<clientid\>**, **\<clientsecret\>** and **\<url\>** with the values you obtained in the previous step.
   Replace **\<user email\>** and **\<password\>** with your SAP CP credentials.
   
   **IMPORTANT: Make sure to remove any trailing spaces.**  

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
   <img src="/exercises/part2/images/curl_get_token.png" width="90%"/>
</p>

6. The **oAuth token** is the **value** of the **access_token** parameter in the response body.
   
   **Save this value** as you will need it later in the exercise. 
   
   **Note:** The value of the "access_token" ends right before the "token_type". 
   Make sure you copy only the value of the "access_token".  
   
<p align="center" width="100%">
   <img src="/exercises/part2/images/access_token_start.png" width="60%"/>
</p>  

<p align="center" width="100%">
   <img src="/exercises/part2/images/access_token_end.png" width="60%"/>
</p>  

## 2. Try Out the API for Viewing Information About Subaccounts

In this section, you will work with the **SAP Cloud Platform - Core Service APIs** (based on Swagger) and view information about the subaccounts in your trial global account.

1. From the [Trial Landing Page](https://cockpit.hanatrial.ondemand.com/cockpit#/home/trial), open the SAP Cloud Platform - Core Service APIs.  

<p align="center" width="100%">
   <img src="/exercises/part2/images/trial_landing_page_apis.png" width="60%"/>
</p>  

<p align="center" width="100%">
   <img src="/exercises/part2/images/apis_homepage.png" width="60%"/>
</p> 

2. Click on the “Accounts” tile to view the APIs related to the Accounts service.  

<p align="center" width="100%">
   <img src="/exercises/part2/images/apis_accounts.png" width="30%"/>
</p>  

3. In the top-right corner, click on the **Authorize** button.  

<p align="center" width="100%">
   <img src="/exercises/part2/images/apis_accounts_authorize.png" width="60%"/>
</p>  

4. Enter the following information:  
   **Bearer \<token\>**  
   where \<token\> is the oAuth access token acquired in the previous section “Obtain Authentication Information”.  
   **Note:** Make sure there is exactly **one space** between “Bearer” and the token.  
   Click on **Authorize** and **Close**.  
   
<p align="center" width="100%">
   <img src="/exercises/part2/images/apis_authorize.png" width="50%"/>
</p> 

5. In case the authorization failed, make sure you copied the correct value of the "access_token" and that you didn’t include the "token_type" value (see first section, step 6).  

6. Open the **Subaccount Operations** section and select the **GET /accounts/v1/subaccounts** API.  

<p align="center" width="100%">
   <img src="/exercises/part2/images/apis_accounts_get_subaccounts.png" width="60%"/>
</p> 

7. Click on the **Try it out** button and **Execute** to try the API and get the information for all the subaccounts.  

<p align="center" width="100%">
   <img src="/exercises/part2/images/apis_accounts_get_subaccounts_try.png" width="60%"/>
</p> 

<p align="center" width="100%">
   <img src="/exercises/part2/images/apis_execute.png" width="10%"/>
</p> 

8. The results are presented in the **response body**.  

<p align="center" width="100%">
   <img src="/exercises/part2/images/apis_responses.png" width="50%"/>
</p>  


## 3. Try Out the API for Viewing Information About All Assigned Entitlements
 
In this section, you will work with the **SAP Cloud Platform - Core Service APIs** (based on Swagger) and view information about the entitlements assigned to your global account.
 
1. Go back to the **SAP Cloud Platform - Core Service APIs** home page, click on the “Entitlements” tile to view the APIs related to the Entitlements service.  
 
 <p align="center" width="100%">
    <img src="/exercises/part2/images/apis_entitlements.png" width="30%"/>
 </p>  
 
2. Get authorized again (see steps 3 and 4 in the previous section).  
 
 <p align="center" width="100%">
    <img src="/exercises/part2/images/apis_authorize.png" width="50%"/>
 </p>  
 
3. Open the **Manage Assigned Entitlements** section and the **GET /entitlements/v1/globalAccountAssignments** API.  
 
  <p align="center" width="100%">
     <img src="/exercises/part2/images/apis_entitlements_get_entitlements.png" width="60%"/>
  </p>  
  
4. Click on the **Try it out** button and then on the **Execute** button to execute the API and to get information about all the entitlements assigned to your global account.  
    You can choose to filter the query by entering the subaccount ID of your new subaccount in the **subaccountGUID** field, and get the entitlements only for it.  
    
5. The results are presented in the **Response body**.  
   You should see the information for all the services and plans that are available and entitled to your global account.

  <p align="center" width="100%">
     <img src="/exercises/part2/images/apis_entitlements_response.png" width="50%"/>
  </p>  

## Summary

Now that you have familiarized yourself with the new REST APIs for SAP Cloud Platform, proceed to -<br/>
[PART 3: AUTOMATE SAP CLOUD PLATFORM OPERATIONS](/exercises/part3/README.md)
