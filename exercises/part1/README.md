# PART 1: SETTING UP YOUR TRIAL ACCOUNT

In this section, you will set up your subaccount in the SAP Cloud Platform Trial using the new CLI.
You will perform the following steps:
1.	View information for your global account.
2.	Create a subaccount.
3.	Assign entitlements to the subaccount you created.

So that an application can consume services, you should first make sure the relevant entitlements for these services are assigned to the subaccount. Assigning entitlements to subaccounts allows you to distribute and limit the required quota from the global account to subaccounts.

## 1.1 View your Global Account Details

In this section, you will work with the CLI for SAP Cloud Platform to get the information about your global account.

1. Open the [SAP Cloud Platform Trial landing page](https://cockpit.hanatrial.ondemand.com/cockpit#/home/trial).
    ![Trial Landing Page](/exercises/part1/images/trial_landing_page.png)

2. If not done already, download the CLI for SAP Cloud Platform.
    ![Download CLI](/exercises/part1/images/trial_landing_page_cli.png)

3. If not done already, create your Trial account.
    ![Create Trial Account](/exercises/part1/images/trial_landing_page_enter.png)
    
4. In the **Windows Command Prompt (CMD)** or **Terminal** for Mac, type the following command to explore all the available commands in the CLI for SAP Cloud Platform.
    ```
     sapcp --help
    ```
   
5. **Log in** with the server URL of the landscape (replace the **<region>** with the region of your trial account – eu10/us10).
   
   Enter your **global account subdomain** (see image), **email**, and **password** when prompted.
   
    ```
    sapcp login --url https://cpcli.cf.<region>.hana.ondemand.com
    ```
   
   ![Global Account Subdomain](/exercises/part1/images/ga_subdomain.png)
   
6. View the details for your global account.
    ```
    sapcp get accounts/global-account
    ```
   ![Get Global Account Info](/exercises/part1/images/cli_get_ga.png)

7. View the available regions for your global account.
    ```
    sapcp list accounts/available-region
    ```
   ![Get Global Account Info](/exercises/part1/images/cli_list_regions.png)
   
8. View the entitlements for your global account. Note that The list will be long because your Trial global account is entitled with many services in advance, to improve the trial experience.
    ```
    sapcp list accounts/entitlement
    ```
   

## Summary

Now that you have ... 
Continue to - [PART 2: GET FAMILIAR WITH THE NEW REST APIs FOR SAP CLOUD PLATFORM ](/exercises/part2/README.md)
