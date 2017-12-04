**Overview**

This document is a guide for using SoapUI with Sabre APIs. SoapUI is an
open source web services tool which can be downloaded
from [www.SoapUI.org](http://www.soapui.org/). (A supported version,
SoapUI Pro, is also available.) SoapUI uses an editor-like interface and
acts as a SOAP client, allowing you to invoke SOAP-based *Sabre APIs*.
SoapUI is easy to learn and use and is available at no cost. At the time
these test suites were produced, SoapUI 5.3.0 was the version.

SoapUI is a product of SmartBear Software and is not endorsed or
supported by Sabre. For more information or for help learning SoapUI or
SoapUI Pro visit: [www.SoapUI.org](http://www.soapui.org/).

**Disclaimer of Warranty:**

\*This document is not intended as a comprehensive tutorial on the
SoapUI test tool or Sabre APIs. The *Sabre APIs* *Test Suites project
files for SoapUI is provided as-is with no warranties expressed or
implied. It is offered without charge to assist customers new to Sabre
APIs, or those who wish to create wire-frame models of business
processes using Sabre APIs.*

**Download and Setup**

To test *Sabre APIs* using SoapUI you must first download a copy
from [www.SoapUI.org](http://www.soapui.org) and install it on a
computer attached to your production network. To execute *Sabre APIs*,
SoapUI must be able to access the Sabre APIs endpoints (URL) using the
same network connection as your production systems. Follow the
instructions on the [www.SoapUI.org](http://www.soapui.org/) website to
install the software.

Once SoapUI is installed and configured for your environment (see the
help section of [www.SoapUI.org](http://www.soapui.org/) for
instructions) you may download and import the SoapUI *Sabre APIs* files
from this repository (named SabreAPIsTestSuites). This file includes
bindings for sample *Sabre APIs* and demonstration test cases.

Save/clone this file to a folder and make a note of the location.

**Import and Configure Sabre APIs Test Suites Project**

To import each project, launch SoapUI and select File &gt; Import
Project. Navigate to the folder in which you stored the project file and
select the name of the project (.xml) (As Example:
OTA\_AirAvailLLSRQ-2.4.0-SoapUI-project.xml)

SoapUI will display a new project named OTA\_AirAvailLLSRQ-2.4.0.

! \[Import Sabre APIs Project\](/img/ImportSoapUIprojectFile.png)

### Add your credentials in the properties file

To run the sample tests, you will first need to add your credentials to
the project’s Custom Properties through Groovy Script. Your credentials
are your user name (EPR), password, and Internet Pseudo-City Code (IPCC)
assigned when Sabre APIs were provisioned. If you do not have this
information, contact your Sabre Sales Representative. Support can also
be requested via the [contact
form](https://developer.sabre.com/contact) in Sabre Dev Studio.

Your *Sabre APIs* credentials are stored as Groovy Script to the Project
to make them available to all Test Suites within the *Sabre APIs Test
Suites* project.

From the main screen, select the project and then click on the Groovy
Script step in test Suite (Test Case). Complete the fields in the Groovy
Script with your Sabre APIs credentials.

!\[Project Groovy Script - Credentials\](/ img/ChangetheCredentials.png)

Where:

| **Property Name** | **Value**                                                                                                            |
|-------------------|----------------------------------------------------------------------------------------------------------------------|
| Username          | Your Sabre APIs User ID (Sabre APIs Credentials)                                                                     |
| Password          | Your Sabre APIs Password (Sabre APIs Credentials)                                                                    |
| Organization      | Your Internet Pseudo City Code (IPCC) for Sabre APIs                                                                 |
| Domain            | This designates the partition used. Leave this set to DEFAULT unless you were instructed to use a specific partition |

**NOTE**: *Sabre SOAP APIs require the use of a ‘ConversationId’ for
each service call, which should be set to a customer-supplied identifier
used to identify the source of the transaction. For testing purposes,
the value is hard-coded with literal values.*

### API-specific qualifiers

For convenience, required and optional values, such as city pairs, are
hard-coded in the XML of each test suite, but depending on the point of
sale associated to your ‘Internet Pseudo City Code, flights may not be
available to shop and book. In that case, a different pair of
airport/city codes should be used.

Example:

!\[City/Airport code pair to be used for
bookings\](/img/CityAirportCodePairHardCoded.png)

Sabre APIs Endpoints
--------------------

Running *Sabre APIs* calls via SoapUI may be performed using
standard *Sabre APIs* endpoints.

These are the endpoints pre-configured in the *Sabre APIs* Workflows
project:

-   [](https://sws3-crt.cert.sabre.com/)
    https://sws-crt.cert.havail.sabre.com (Test)

-   https://webservices.sabre.com/websvc (Production)

**NOTE:** *This project is capable of generating Sabre APIs service
calls against the Sabre production environment which can book live
inventory.*

*For convenience, the project is pre-configured to use the*
https://sws-crt.cert.havail.sabre.com *Test environment.* *If changes
are made to the endpoint of one or more Test Suites, please be aware
that segments booked in the production environment when using this tool
are genuine and all the standard rules apply.*

*Standard Sabre scan charges apply to all Sabre APIs transactions
executed with SoapUI.*

!\[Test Step endpoint\](/img/TestStepEndPoint.png)

**Sabre APIs Test Suites**

Test Suites are composed of a set of steps, each of them contributing to
completing a transaction in the Sabre system.

The following are the test suites currently included in the project:

| **API Name**             | **Service Action Code** | **Objective**                                                                                                                 |
|--------------------------|-------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| Air Availability         | OTA\_AirAvailLLSRQ      | Searches for flights and the corresponding class availability information.                                                    |
| Create Session           | SessionCreateRQ         | Utilized to initiate a Soap API Session.                                                                                      |
| Passenger Details        | PassengerDetailsRQ      | Provides traveler information plus agency and ticketing information.                                                          |
| Get Itinerary            | TravelItineraryReadRQ   | Offers functionality to allow the Airline or Agency to search for and retrieve particular PNR data directly from AAA session. |
| Bargain Finder Max       | BargainFinderMaxRQ      | Searches for the lowest available priced itineraries based upon a specific date.                                              |
| Low Fare Search and Book | -                       | Allows you to search and book flights.                                                                                        |

Each test suite included in the project, is designed to obtain a session
token. This means that test suites that depend on one or more workflows
don’t make optimal use of sessions (since multiple are open, for each
one), from an end to end transaction/performance perspective.

**Running a Test Case**

The Sabre APIs Test Suites project is ready to use.

To run a project, do the following:

1.  Double click on the desired test suite

2.  Click on the PLAY icon (‘green triangle’) to run

!\[Running Test Cases\](/img/RunningTestCases.png)

The test suite steps will be executed in sequence, until completion.

Most of the test suites have assertions pre-configured to determine
success/failure, and stop processing if not successful, and avoiding
unnecessary execution of subsequent steps.

**Test Suite Results**

When a Test Suite is run, SoapUI sends each request to the Sabre APIs
endpoint selected (the certification endpoint is pre-configured) and
displays the response. The editor displays the complete XML request (2)
and response (3) so the contents of each are unambiguous.

!\[Test Cases results\](/img/TestCaseResults.png)

 Reusing/Cloning Test Suites
----------------------------

A quick way to create a new Test Suite that has all of the basic
operations pre-populated is to clone an existing one. You can add new
service requests or modify the existing Test Steps in the clone without
modifying the original Test Suite. Select the Test Suite you wish to
clone in the navigation panel. Right click and select Clone Test Case.
Complete the fields and click OK.

!\[Test Cases results\](/img/CloningTestCases.png)

Once you press OK, the cloned Test Suite is ready and can be modified as
required.
