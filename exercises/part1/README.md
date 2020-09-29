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
<br>
<p align="center" width="100%">
<img src="/exercises/part1/images/trial_landing_page.png" alt="Trial Landing Page" width="600"/>
</p>

2. If not already done, download the CLI for SAP Cloud Platform.
<br>
<p align="center" width="100%">
<img src="/exercises/part1/images/trial_landing_page_cli.png" width="60%"/>
</p>
3. If not already done, create your Trial account. 
<br>
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
    
<br>
<p align="center" width="100%">
<img src="/exercises/part1/images/ga_subdomain.png" width="50%"/>
</p>

6. View the details of your global account.

```
sapcp get accounts/global-account
```

<br>
<p align="center" width="100%">
<img src="/exercises/part1/images/cli_get_ga.png" width="60%"/>
</p>

7. View the available regions for your global account.

```
sapcp list accounts/available-region
```

<br>
<p align="center" width="100%">
<img src="/exercises/part1/images/cli_list_regions.png" alt="Get Global Account Info" width="60%"/>
</p>

8. View the entitlements for your global account. Note that the list will be long because your Trial global account is entitled with many services in advance, to improve the trial experience.

```
sapcp list accounts/entitlement
```
   

## Summary

Now that you have familiarized yourself with the CLI for SAP Cloud Platform, proceed to - [PART 2: GET FAMILIAR WITH THE NEW REST APIs FOR SAP CLOUD PLATFORM ](/exercises/part2/README.md)
