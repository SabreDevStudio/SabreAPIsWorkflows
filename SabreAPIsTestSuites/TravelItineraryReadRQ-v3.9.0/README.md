**Download and Setup**

Use the ![README.md](/SabreAPIsTestSuites/README.md) instructions to download and
set-up SoapUI.

**Test Suite**

The following are the steps included in this test suite:

| **Step** | **Description**                                                                                               |
|----------|---------------------------------------------------------------------------------------------------------------|
| Step 1   | Calls the SessionCreateRQ API to get a session token.                                                         |
| Step 2   | Calls the OTA_AirAvailLLSRQ API to get flight availability.                                                   |
| Step 3   | Calls the TravelItineraryAddInfoLLSRQ API to add traveler information.                                        |
| Step 4   | Calls the OTA_AirBookLLSRQ API to book the flight segment.                                                    |
| Step 5   | Calls the OTA_AirPriceLLSRQ API to get flight prices.                                                         |
| Step 6   | Calls the EndTransactionLLSRQ API to complete the transaction.                                                |
| Step 7   | Calls the TravelItineraryReadRQ API to search for and retrieve particular PNR data directly from AAA session. |


