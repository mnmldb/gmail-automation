# Gmail Automation 
## Overview
This script aims to send emails respectively to recipients with different contents with one-click.  
In order not to send the email more than twice to the recipient, we would like to add the flag "Sent" for the completion.  
For the reuse purpose, we created the function to reset all "Sent" status.

## Requirements
- Google App Script
- Gmail
- Google Docs
    - for the message body
- Google Sheets
    - for the email addresses and respective messages

## Usage
### Preparation
1. Create a google docs that contains the message body with a placeholder(s) to be replaced afterwards
1. Create a google sheets that contains the email addresses and respective messages

### Customize the Script
1. Replace the `file_id` in `var filej = DriveApp.getFileById('file_id')` with the file id of the google docs

### Execute the Script
1. Execute `SendM()` for sending emails
1. Execute `ClearStat()` for resetting the "Sent" status
