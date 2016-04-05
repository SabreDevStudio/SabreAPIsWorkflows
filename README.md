## Overview
This document is a guide for using soapUI® with *Sabre APIs*. soapUI is an open source Web services tool which can be downloaded from www.soapui.org. (A supported version, soapUI Pro, is also available.) soapUI uses an editor-like interface and acts as a SOAP client, allowing you to invoke SOAP-based *Sabre APIs*. soapUI is easy to learn and use and is available at no cost. At the time of this writing soapUI 5.2.1 is the current version. 

soapUI is a product of SmartBear Software (100 Cummings Center, Suite 234N, Beverly, MA 01915, 978-236-7900, SmartBear.com) and is not endorsed or supported by Sabre Inc. For more information or for help learning soapUI or soapUI Pro please visit: www.soapui.org. 

*This document is not intended as a comprehensive tutorial on the soapUI test tool or Sabre APIs. The Sabre APIs Client Test Tool project file for soapUI is provided as-is with no warranties expressed or implied. It is offered without charge to assist customers new to Sabre APIs or who wish to create wire-frame models of business processes using Sabre APIs.*

## Download and Setup
To test *Sabre APIs* using soapUI you must first download a copy from www.soapui.org and install it on a computer attached to your production network. To execute *Sabre APIs*, soapUI must be able to access the Sabre APIs endpoints (URL) using the same network connection as your production systems. Follow the instructions on the www.soapui.org website to install the software. 

Once soapUI is installed and configured for your environment (see the help section of www.soapUI.com for instructions) you may download and import the soapUI *Sabre APIs* Workflows project file from this repository (named Sabre-APIs-Workflows-soapui-project.xml). This file includes bindings for sample *Sabre APIs* and demonstration test cases. 

Save/clone this files to a folder and make a note of the location.

## Import and Configure Sabre APIs Workflows Project
To import the project, launch soapUI and select File > Import Project. Navigate to the folder in which you stored the project file and select Sabre-APIs-Workflows-soapui-project.xml. 

soapUI will display a new project named Sabre APIs - Workflows.






