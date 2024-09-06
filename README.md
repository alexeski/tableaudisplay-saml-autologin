# Tableau Display Auto-Login Tableau Dashboard with SAML IdP

## Overview

This repository contains a simple web application that facilitates auto-login to a Tableau dashboard. The application is designed to work in scenarios where digital signage software has already authenticated the display using the same SAML Identity Provider (IdP) that is used for Tableau sessions. 

## Features

- Automatically retrieves workbook and view parameters from the URL.
- Constructs a dynamic URL for the Tableau dashboard.
- Opens a popup for SSO authentication.
- Redirects to the Tableau dashboard after a specified timeout.

## Prerequisites

- A valid Tableau account with access to the desired workbooks and views.
- SAML IdP configured for Tableau authentication.
- A web server to host the HTML file (optional for local testing).
- You must be already signed in to the SAML IDP before opening index.html
- Allow popups on the browser you are running this code (the saml auto-login happens in the popup, which is automatically closed after 5 seconds)

## Usage

You may hard code the parameters in the code, alternativelly pass them in the URL to customize the dashboard view:

   - `siteName`: The name of the Tableau Cloud site (default: `mySite`).
   - `workbook`: The name of the Tableau workbook (default: `CompanyAnalysis`).
   - `view`: The name of the Tableau view (default: `KPIOverview`).
   - `entityId`: The SAML entity ID for authentication (look for "Tableau Cloud entity ID" in the Tableau SAML settings page, it looks like this: `a2aecbc1-54e9-4ab0-975c-05eb6f237e8f`).

   Example URL: http://localhost:3000/index.html?siteName=mySite&workbook=SalesData&view=MonthlyOverview&entityId=your-entity-id
   
   The application will open a popup for SSO authentication and redirect to the specified Tableau dashboard after 5 seconds.

## Code Explanation

- **getParameterByName(name)**: A utility function to retrieve query parameters from the URL.
- **init()**: The main function that initializes the application:
- Retrieves the workbook, view, and entityId parameters.
- Constructs the dynamic URL for the Tableau dashboard.
- Opens a popup for SSO login.
- Sets a timer to close the popup and redirect to the dashboard.

## Customization

- You can adjust the timeout duration in the `setTimeout` function to change how long the popup remains open before redirecting.
- Modify the default values for `siteName`, `workbook`, `view`, and `entityId` as needed.
