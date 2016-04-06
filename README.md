## Overview
This document is a guide for using soapUI® with *Sabre APIs*. soapUI is an open source Web services tool which can be downloaded from www.soapui.org. (A supported version, soapUI Pro, is also available.) soapUI uses an editor-like interface and acts as a SOAP client, allowing you to invoke SOAP-based *Sabre APIs*. soapUI is easy to learn and use and is available at no cost. At the time of this writing soapUI 5.2.1 is the current version. 

soapUI is a product of SmartBear Software (100 Cummings Center, Suite 234N, Beverly, MA 01915, 978-236-7900, SmartBear.com) and is not endorsed or supported by Sabre Inc. For more information or for help learning soapUI or soapUI Pro please visit: www.soapui.org. 

### Disclaimer of Warranty:
*This document is not intended as a comprehensive tutorial on the soapUI test tool or Sabre APIs. The Sabre APIs Client Test Tool project file for soapUI is provided as-is with no warranties expressed or implied. It is offered without charge to assist customers new to Sabre APIs or who wish to create wire-frame models of business processes using Sabre APIs.*

## Download and Setup
To test *Sabre APIs* using soapUI you must first download a copy from www.soapui.org and install it on a computer attached to your production network. To execute *Sabre APIs*, soapUI must be able to access the Sabre APIs endpoints (URL) using the same network connection as your production systems. Follow the instructions on the www.soapui.org website to install the software. 

Once soapUI is installed and configured for your environment (see the help section of www.soapui.com for instructions) you may download and import the soapUI *Sabre APIs* Workflows project file from this repository (named Sabre-APIs-Workflows-soapui-project.xml). This file includes bindings for sample *Sabre APIs* and demonstration test cases. 

Save/clone this files to a folder and make a note of the location.

## Import and Configure Sabre APIs Workflows Project
To import the project, launch soapUI and select File > Import Project. Navigate to the folder in which you stored the project file and select Sabre-APIs-Workflows-soapui-project.xml. 

soapUI will display a new project named Sabre APIs - Workflows.

###### img here...

To run the sample tests you will first need to add your credentials to the project’s Custom Properties. Your credentials are the Sabre APIs artifacts such as user name (EPR), password, and Internet Pseudo-City Code (IPCC) assigned when Sabre APIs was provisioned. If you do not have this information please contact your Sabre Sales Representative. Support can also be requested via the [contact form](https://developer.sabre.com/contact) in Sabre Dev Studio.

From the main screen select the Sabre APIs Workflows project and then click the Custom Properties tab at the bottom of the left-hand panel. Complete the fields in this table with your Sabre APIs credentials.

###### img here...

Where:

Property Name	| Value
------------- | -----
Username	| Your Sabre APIs User ID (Sabre APIs Credentials)
Password	| Your Sabre APIs Password (Sabre APIs Credentials)
Organization	| Your Internet Pseudo City Code (IPCC) for Sabre APIs 
Domain	| This designates the partition used. Leave this set to DEFAULT unless you were instructed to use a specific partition


**NOTE**: *Sabre SOAP APIs require the use of a ‘ConversationId’ for each service call, which should be set to a customer-supplied identifier used to identify the source of the transaction. For testing purposes the value is already set in the project file, to use ‘SWS-Test-[CustomerIPCC]’ as the value.*

Your *Sabre APIs* credentials are stored as Custom Properties to the Project to make them available to all Test Cases and within the *Sabre APIs Workflows* project. 

If you would like to use a different set of *Sabre APIs* credentials for an individual Test Suite or Test Case you may create Test Properties specific to the Test Suite/Case and modify the service requests to reference the new data source. See the soapUI documentation at http://www.soapui.org for instructions.

In addition, given that all workflows currently in the project require completing a booking, the city pair/route used for the booking can be set using Custom Properties at the same level the credentials are set up.

These properties are named ‘ItineraryOrigin’ and ‘ItineraryDestination’.

For convenience, sample values are provided, but depending on the point of sale associated to your ‘Internet Pseudo City Code’ (see table on previous page), flights may not be available to shop and book. 
In that case, a different pair of airport/city codes will need to be used.
If you do not have this information please contact your Sabre Sales Representative.
Support can also be requested via the [contact form](https://developer.sabre.com/contact) in Sabre Dev Studio.

###### img here...

**NOTE:** *The Project includes other Custom Properties configured at different levels that are used internally by the different Test Cases to complete and parameterize execution (e.g.: Sabre APIs endpoint). Changes can be applied, but taking the risk of leaving Test Cases under inconsistent state/unable to execute successfully, if values provided are incorrect.*

## Sabre APIs Endpoints
Running *Sabre APIs* calls via soapUI may be performed using standard *Sabre APIs* endpoints. 

These are the endpoints pre-configured in the *Sabre APIs* Workflows project: 

-	https://sws3-crt.cert.sabre.com (Sabre APIs Certification / Sabre Test Environment)
-	https://webservices3.sabre.com (Production Sabre APIs Environment) 

**NOTE:** *The Sabre APIs Workflows soapUI project is capable of generating Sabre APIs service calls against the Sabre production environment which can book live inventory.*

*For convenience, the project is pre-configured to use the Certification / Test Environment.*
*If changes are made to the endpoint of one or more Test Cases, please be aware that segments booked in the production environment when using this tool are genuine and all the standard rules apply.*

*Standard Sabre scan charges apply to all Sabre APIs transactions executed with soapUI.*

Endpoints are set at the Test Step level (each of the steps executed as part of a Test Case). 

###### img here...

## Sabre APIs Workflows

Workflows are composed of a set of steps, each of them contributing to completing a transaction in the Sabre system/s.

In the Sabre APIs Workflows project, each workflow maps to a soapUI Test Case.

The following are the workflows currently included in the project:

Workflow Name |	Objective
------------- | ---------
**Book Air Segment** | *Book flights, after the shopping process has been completed.*
**Reserve Air Seat** | *Select a seat on a given flight.*
**Issue Air Ticket <sup>[1](#fn1)</sup> | *Issue a new ticket for an existing reservation.* 
**Post Booking transaction** | *Perform a transaction after the original booking was completed (cancel the itinerary that was booked, in this case).*


In addition, other ‘Utility’ Test Cases are included in the project, for those transactions that are common to multiple workflows (e.g.: obtain and release a SOAP session token – a.k.a.: ‘ATH’ – shop for flights and fares, etc.).

This way, Test Cases can be composed of both, individual Test Steps (with calls to Sabre APIs) and other Test Cases.

Workflows can have prerequisites, which are denoted by the prefix ‘Pre’ within the list of Test Steps in a Test Case. 

Examples of prerequisites are the need for a booking completed, prior to reserving a seat from ‘Reserve Air Seat’ / issuing a ticket from ‘Issue Air Ticket’ / cancelling the itinerary from ‘Post Booking transaction’ workflows, or the need to complete ‘shopping’ (get flights and fares available) in order to create a booking from the ‘Book Air Segment’ workflow.

Finally, each of the workflows included in the project, is designed to obtain and release a session token. This means that workflow Test Cases that depend on one or more workflows (as prerequisite) don’t make optimal use of sessions (since multiple are open, for each one), from an end to end transaction/performance perspective.

For optimal use of Sabre SOAP APIs sessions, please refer to the Sabre Dev Studio best practices section: https://developer.sabre.com/resources/best_practices#sessions

<a name="fn1">1</a>: The ‘Issue Air Ticket’ workflow requires additional setup via Custom Properties.

Check the ‘Appendix’ section for additional information.

## Running a Test Case
The Sabre APIs Workflows project is ready to use. 

In order to run a Test Case, do the following:

1-	Expand the Test Suite named ‘Sabre API Workflows’ (below the list of bindings)

2-	Double click on the desired Test Case (prefixed by the word ‘Workflow’)

3-	Click on the PLAY icon (‘green triangle’) to run.

###### img here...

The Test Steps (and referenced Test Case/s) included in the selected Test Case will be executed in sequence, until completion.

Most of the Test Steps have Assertions pre-configured, in order to determine success/failure, and stop processing if not successful, avoiding unnecessary execution of subsequent steps.

**NOTE:** *The ‘Utility’ Test Cases (prefixed by the word ‘Utility’) are meant to promote reuse and avoid repetition of common steps, but not all of them can be run isolated, since they depend on contextual data previously obtained by the calling Test Case.* 

## Test Case Results
When a Test Case is run, soapUI sends each request to the Sabre APIs endpoint selected (the Certification endpoint is pre-configured) and displays the response. The editor displays the complete XML request (2) and response (3) so the contents of each are unambiguous.

For those workflows designed as ‘composite’ Test Cases (referencing other ‘Utility’ Test Cases), the traffic needs to be inspected in the Test Steps composing the corresponding ‘Utility’ Test Case.

As an example, the ‘Book Air Segment’ workflow is only composed of ‘Utility’ Test Cases, so in order to inspect the traffic for the ‘Booking’ (1) Test Case step, the ‘Utility: Booking’ Test Case needs to be expanded, and then double click on the appropriate Test Step inside it. 

###### img here...

## Reusing/Cloning Test Cases
A quick way to create a new Test Case that has all of the basic operations pre-populated is to clone an existing one. You can add new service requests or modify the existing Test Steps in the clone without modifying the original Test Case. 
Select the Test Case you wish to clone in the navigation panel. Right click and select Clone Test Case. Complete the fields for the new Test Case and click OK.

###### img here...

Once you press OK the cloned Test Case is ready and can be modified as required. 

## Help and Support
soapUI is a powerful tool with many features beyond those described in this document or used in the Sabre APIs Workflows project. It is beyond the scope of this document to fully describe all of the features or provide documentation or training in their use. For more information please consult the Getting Started section at: www.soapui.org.

Need to report an issue/suggest improvements on the workflows? 

Use the [built-in issues](https://github.com/SabreDevStudio/SabreAPIsWorkflows/issues) section




## Appendix
**Setting up printer parameters for ‘Issue Air Ticket’ workflow:**

The ‘Issue Air Ticket’ workflow requires the setup of a ticket printer type and ticket printer line address in order to be executed successfully.

These are parameters required by the Sabre system to control ticketing locations.

Values should be set under the Custom Properties tab, from the Test Case named ‘Workflow: Issue Air Ticket’ (figure below).

Sample values for ticket printer type are ‘AB’ (for ATB1 countries), ‘AT’ (for ATB2 countries). Value depends on country of the point of sale. 

Value for printer line address should also be requested to Sabre, and it is composed of 6 alpha-numeric characters.

Please contact your Sabre representative or fill the [contact form](https://developer.sabre.com/contact) in Sabre Dev Studio for help with printer parameters. 

###### img here...

**NOTE:** parameters can be different depending on the Sabre API Endpoint (Certification vs. Production) being used – and please be aware that completing bookings and issuing tickets against the Production environment have impact on live inventory and have costs associated.
