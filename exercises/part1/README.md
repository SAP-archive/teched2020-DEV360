# PART 1: SETTING UP YOUR TRIAL ACCOUNT

In this section, you will set up your subaccount in the SAP Cloud Platform Trial using the new CLI.
You will perform the following steps:
1.	View information of your global account.
2.	Create a subaccount.
3.	Assign entitlements to the subaccount you created.

So that an application can consume services, you should first make sure the relevant entitlements for these services are assigned to the subaccount. Assigning entitlements to subaccounts allows you to distribute and limit the required quota from the global account to subaccounts.

## 1. View your Global Account Details

In this section, you will work with the CLI for SAP Cloud Platform to get the information about your global account.

1. Open the [SAP Cloud Platform Trial landing page](https://cockpit.hanatrial.ondemand.com/cockpit#/home/trial).  
<p align="center" width="100%">
   <img src="/exercises/part1/images/trial_landing_page.png" alt="Trial Landing Page" width="600"/>
</p>

2. If not already done, download the CLI for SAP Cloud Platform (latest version for your operating system).  
Unpack the archive and copy the client file (for example, sapcp.exe) to your local system.  
Open the directory with the client file in the **Windows Command Prompt (CMD)** or **Terminal** for Mac.  

<p align="center" width="100%">
   <img src="/exercises/part1/images/trial_landing_page_cli.png" width="60%"/>
</p>

3. If not already done, create your Trial account.  

<p align="center" width="100%">
   <img src="/exercises/part1/images/trial_landing_page_enter.png" width="60%"/>
</p>

4. In the **Windows Command Prompt (CMD)** or **Terminal** for Mac, type the following command to explore all the available commands in the CLI for SAP Cloud Platform.

```
sapcp --help
```  

5. **Log in** with the server URL of the landscape (replace the **\<region\>** with the region of your trial account – eu10/us10).  
Enter your **global account subdomain** (see image below), **email**, and **password** when prompted.  

```
sapcp login --url https://cpcli.cf.<region>.hana.ondemand.com
```  

<p align="center" width="100%">
<img src="/exercises/part1/images/ga_subdomain.png" width="50%"/>
</p>

6. View the details of your global account.

```
sapcp get accounts/global-account
```

<p align="center" width="100%">
   <img src="/exercises/part1/images/cli_get_ga.png" width="60%"/>
</p>

7. View the available regions for your global account.

```
sapcp list accounts/available-region
```

<p align="center" width="100%">
   <img src="/exercises/part1/images/cli_list_regions.png" alt="Get Global Account Info" width="60%"/>
</p>

8. View the entitlements for your global account. Note that the list will be long because your Trial global account is entitled with many services in advance, to improve the trial experience.

```
sapcp list accounts/entitlement
```  

## 2. Create a New Subaccount

In this section, you will work with the CLI for SAP Cloud Platform to create a subaccount.

1. Create a new subaccount named Dev.  
   Replace the **<new_subdomain>** with a value of your choice.  
   **Note:** A subdomain can contain letters (a-z), digits (0-9), and hyphens only.  
   Replace the **\<region\>** with the region of your global account (eu10 / us10).  
   
```
sapcp create accounts/subaccount --region <region> --display-name Dev --subdomain <new_subdomain>
```
   
<p align="center" width="100%">
   <img src="/exercises/part1/images/cli_create_subaccount.png" width="60%"/>
</p> 
2. Verify the subaccount has been created successfully.  

```
sapcp list accounts/subaccount
```

<p align="center" width="100%">
   <img src="/exercises/part1/images/cli_get_subaccounts.png" width="85%"/>
</p>
3. Copy the ID of your new subaccount and save it.  

<p align="center" width="100%">
   <img src="/exercises/part1/images/cli_get_subaccounts_id.png" width="85%"/>
</p>
4. Refresh the cockpit to see the new subaccount.  

## 3. Assign Entitlements to the New Subaccount

In this section, you will work with the CLI for SAP Cloud Platform to assign service entitlements to your new subaccount.  
  
You will assign these services to the subaccount:
* **Application Runtime (APPLICATION_RUNTIME)**: Enables the deployment of applications in the SAP Cloud Platform, Cloud Foundry environment, such as the application you will develop as part of this exercise.
* **Cloud Management (cis)**: Manages SAP CP core entities such as accounts and entitlements. Assigning entitlements to CIS allows access to the SAP CP APIs.
* **Usage Data Management (uas)**: Gathers, stores, and exposes usage information for services and applications in all regions in a cloud deployment, for the purpose of central analysis, reporting, and license auditing.  
  
**Note:** Usage Data Management will be used later in PART 5: RETRIEVE USAGE INFORMATION.

1. In the cockpit, enter **Entitlements > Entity Assignments**, select **All Subaccounts** and click **Go**.
<p align="center" width="100%">
   <img src="/exercises/part1/images/cockpit_entitlements_subaccounts.png" width="70%"/>
</p>

2. You can see that your new subaccount currently has no entitlements assigned to it. Let’s assign it using the CLI.

3. Assign an entitlement to the **Cloud Management (cis)** service, **central** plan.  
   Replace the **<new_subaccount_id>** with the ID of your new subaccount.  
   
```
sapcp assign accounts/entitlement --for-service cis --plan central --to-subaccount <new_subaccount_id>
```
   
<p align="center" width="100%">
   <img src="/exercises/part1/images/cli_assign_cis.png" width="70%"/>
</p>

4. Assign an entitlement to **Usage Data Management (uas)** service, **reporting-ga-admin** plan.  
Replace the **<new_subaccount_id>** with the ID of your new subaccount.  

```
sapcp assign accounts/entitlement --for-service uas --plan reporting-ga-admin --to-subaccount <new_subaccount_id>
```

<p align="center" width="100%">
   <img src="/exercises/part1/images/cli_assign_uas.png" width="70%"/>
</p>

5. Next is to assign an entitlement to the **Application Runtime** service.  
For this, you first need to free the quota assigned to the *“trial”* subaccount, which gets all the quota assigned to it by default (4 units).  
Locate the subaccount ID of the *“trial”* subaccount which can be derived in multiple ways, one of them is via the “info” button in the cockpit.

<p align="center" width="100%">
   <img src="/exercises/part1/images/cockpit_get_subaccount_id.png" width="60%"/>
</p>

6. Replace the **<trial_subaccount_id>** with the ID of your *“trial”* subaccount, and assign 0 units to it.  

```
sapcp assign accounts/entitlement --for-service APPLICATION_RUNTIME --plan MEMORY --amount 0 --to-subaccount <trial_subaccount_id>
```

7. Assign an entitlement to the **Application Runtime (APPLICATION_RUNTIME)** service, **MEMORY** plan.  
Replace the **<new_subaccount_id>** with the ID of your new subaccount.  

```
sapcp assign accounts/entitlement --for-service APPLICATION_RUNTIME --plan MEMORY --amount 1 --to-subaccount <new_subaccount_id>
```

8. Execute the following command to verify the entitlements were successfully assigned.  
Replace the **<new_subaccount_id>** with the ID of your new subaccount.  

```
sapcp list accounts/entitlement -sa <new_subaccount_id>
```

9. Refresh the **Entity Assignments** screen in the cockpit to view the new assigned entitlements.


## Summary

Now that you have familiarized yourself with the CLI for SAP Cloud Platform, proceed to -<br/>
[PART 2: GET FAMILIAR WITH THE NEW REST APIs FOR SAP CLOUD PLATFORM](/exercises/part2/README.md)
