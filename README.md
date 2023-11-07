# Usage Report System

## Overview

This Usage Report System is designed to collect data about user interactions with a particular service or application. It captures the email address of the user and the identifier of the slide viewed, storing this information in a Google Sheet for later analysis.

## Technologies Used

- **Google Apps Script (GAS):** A cloud-based scripting language for light-weight application development in the Google Workspace platform.
- **Cloudflare Workers:** A serverless execution environment that allows you to create entirely new applications or augment existing ones without configuring or maintaining infrastructure.
- **HTML/CSS/JavaScript:** Standard web technologies used for building the front-end interface that users interact with.
- **Google Sheets:** An online spreadsheet app that lets users create and format spreadsheets and simultaneously work with other people.

## Structure

### Front-End

The front-end consists of an HTML form where users input their email and the slide they viewed. The form submission is handled by JavaScript, which validates the input and sends a POST request to the Cloudflare Worker.

#### Files:
- `index.html`: The HTML structure for the user input form.
- `script.js`: The JavaScript file handling form submission and asynchronous communication with the Cloudflare Worker.

### Cloudflare Worker

The Cloudflare Worker acts as a proxy between the front-end and the Google Apps Script. It forwards the POST requests received from the client side to the GAS and returns the GAS response back to the client.

#### Files:
- `index.js`: The main file for the Cloudflare Worker, which contains all logic for handling requests and responses.

### Google Apps Script

The GAS is used to process the data received from the Cloudflare Worker and write it to a Google Sheet named `usage_report`. It also performs validation checks to ensure no data is missing.

#### Files:
- `Code.gs`: The Google Script file that contains the `doPost` function to handle POST requests and interact with Google Sheets.

## How to Use

To use the system, users will fill out the form on the web page with their email address and the identifier of the slide they viewed. Upon submission, the data is sent to the Cloudflare Worker, which forwards it to the Google Apps Script. The script then validates the data and appends it to the `usage_report` Google Sheet. 

If any field is missing or an error occurs, the system will alert the user with a descriptive message.

## Setup Instructions

1. Deploy the Google Apps Script and note the URL provided after deployment.
2. Update the `GOOGLE_SCRIPT_URL` in the Cloudflare Worker script with the URL from step 1.
3. Deploy the Cloudflare Worker and update the `fetch` URL in the `script.js` with the Cloudflare Worker endpoint.
4. Host the `index.html` and `script.js` files on a server or local environment for user access.

## Error Handling

Both the Cloudflare Worker and Google Apps Script include error handling to ensure the system responds gracefully to issues such as missing data fields or server errors.
