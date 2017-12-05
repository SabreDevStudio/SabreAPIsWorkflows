**Download and Setup**

Use the ![README.md](/SabreAPIsTestSuites/README.md) instructions to download and
set-up SoapUI.

**Test Suite**

The following are the steps included in this test suite:

| **Step** | **Description**                                                                                             |
|----------|-------------------------------------------------------------------------------------------------------------|
| Step 1   | SessionCreateRQ API is used to get a session token.                                                         |
| Step 2   | OTA_AirAvailLLSRQ API is used to get flight availability.                                                   |
| Step 3   | TravelItineraryAddInfoLLSRQ API is used to add traveler information.                                        |
| Step 4   | OTA_AirBookLLSRQ API is used to book the flight segment.                                                    |
| Step 5   | OTA_AirPriceLLSRQ API is used to get flight prices.                                                         |
| Step 6   | EndTransactionLLSRQ API is used to complete the transaction.                                                |
| Step 7   | TravelItineraryReadRQ API is used to search for and retrieve particular PNR data directly from AAA session. |
