# DEV360 - Explore the new capabilities of SAP Cloud Platform - Open API and CLI

## Description

This repository contains the material for the SAP TechEd 2020 session DEV360 - Explore the new capabilities of SAP Cloud Platform - Open API and CLI. 

## Overview

In 2020, SAP released a new version of SAP Cloud Platform (SAP CP).
This enhanced version represents a major milestone, as it introduces a new best-practice for supporting cloud resource management and automation through a set of new features that are currently being developed based on the feedback collected from major customer and partner stakeholders. 

The main new features of SAP CP are:

1. **Improved Account Structure**: a new grouping concept for subaccounts, called “directories”. Directories support the aggregation of subaccounts according to a customer’s own business and technical needs, allowing account administrators to better allocate SAP CP resources to different lines of business, departments, and teams under their domains.

![Improved Account Structure](/assets/images/Overview.png)

2. **Automation Support**: a new programmatic interface for all major SAP CP cockpit operations, available both as a new CLI tool for command-line scripting and as a REST API platform. The main operational categories are:
    * Account management
    * Entitlement management
    * Service provisioning
    * Multitenant service management
    * Resource consumption
    * Member management
    * Role assignment
    
    During this exercise we will present these interfaces to you, and you will be able to try them out yourselves.
    
3. **Custom Properties**: a new concept to label or tag directories and subaccounts with custom properties and values, based on your own business and technical needs, to make organizing and filtering your directories and subaccounts easier within your global account.

4. **Improved Cost and Billing Control**: detailed and exportable breakdown of service consumption and associated costs.

### Stakeholder Roles: Best Practices For SAP Cloud Platform

SAP CP increasingly distinguishes between various SAP CP stakeholders, their roles, and their respective business requirements. 
The stakeholders are divided into three main groups:

1. **Business administrator and commercial contact**
    * Signs contracts with SAP
    * Orders services and apps from SAP
    * Receives and reviews monthly balance statements
    * Reviews usage and costs
    * Rarely uses SAP CP cockpit
    
2. **Technical account administrator and technical contact**
    * Manages a global account, regions, security, and so on
    * Sets up directories, subaccounts, and roles for additional stakeholders in the company
    * Maps service entitlements and quotas to each of these stakeholders
    * Tracks usage dashboard
    * Uses the CLI tools to automate procedures
    * Subscribes business users to applications
    * Frequently uses SAP CP cockpit
    
3. **Subaccount administrator and developer**
    * Responsible for a directory or subaccount administration 
    * Assigns user rights to other developers
    * Uses development tools and CLI to develop and debug various applications (Git, SAP Application Studio, S/4 Cloud SDK, SAP Rapid Application Studio, MTA builder and deployer, etc.)
    * Integrates SAP CP business services and technical resources (e.g., databases)
    * May programmatically interact with SAP CP using the SAP CP REST APIs
    * Uses dev, test, staging and productive subaccounts to test and to deploy applications
    * Rarely uses SAP CP cockpit


## Exercise Overview

The purpose of this exercise is to illustrate some of the new CLI and API automation capabilities introduced in the enhanced version of SAP CP. 
In the first part of the exercise, you will act as a technical account administrator of a new SAP CP global account. Your task is to use the CLI tools to set up the account for your development team.
In the second, third and fourth parts of the exercise, you will ask your friend, the development guru, to explore the SAP CP REST APIs, and then to write an application to automate one of your most frequent tasks. Finally, in the fifth part of the exercise, you will retrieve the latest usage and cost information of the created accounts.
You will use your Trial account.


## Exercises

- [PART 1: SETTING UP YOUR TRIAL ACCOUNT](exercises/part1/README.md)
- [PART 2: GET FAMILIAR WITH THE NEW REST APIs FOR SAP CLOUD PLATFORM ](exercises/part2/README.md)
- [PART 3: AUTOMATE SAP CLOUD PLATFORM OPERATIONS](exercises/part3/README.md)
- [PART 4: USE THE NEW APPLICATION IN A PRODUCTION SCENARIO](exercises/part4/README.md)
- [PART 5: RETRIEVE USAGE INFORMATION](exercises/part5/README.md)


## How to obtain support

Support for the content in this repository is available during the actual time of the online session for which this content has been designed. Otherwise, you may request support via the [Issues](../../issues) tab.

## License
Copyright (c) 2020 SAP SE or an SAP affiliate company. All rights reserved. This file is licensed under the Apache Software License, version 2.0 except as noted otherwise in the [LICENSE](LICENSES/Apache-2.0.txt) file.
