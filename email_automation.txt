
var EMAIL_SENT = 'EMAIL_SENT';

function SendM() {
 
  // get file content from template string 
  var filej = DriveApp.getFileById('file_id'); // Insert the file id
  var docContent = filej.getAs('text/plain');  
  var gBody = docContent.getDataAsString();
  var hBody = gBody;
  
  var sheet = SpreadsheetApp.getActiveSheet();
  var startRow = 2; // First row of data to process
  //var numRows = 1; // Number of rows to process
  var numRows = sheet.getLastRow()-1;
  // Fetch the range of cells A2:B3
  var dataRange = sheet.getRange(startRow, 1, numRows, 4);
  // Fetch values for each row in the Range.
  var data = dataRange.getValues();
  for (var i = 0; i < data.length; ++i) {
    var row = data[i];
    var emailAddress = row[1]; // First column
    var message = row[2]; // Second column
    gBody = gBody.replace("Placeholder",message); // Replace the placeholder to the respective message
    var emailSent = row[3]; // Third column
    if (emailSent != EMAIL_SENT) { // Prevents sending duplicates
      var subject = 'Thank you for your participation to our survey';
      
        MailApp.sendEmail(
          emailAddress,         // recipient
          subject,                  // subject 
          'test', {                        // body
            htmlBody: gBody                 // advanced options
          }
        ); 
      //MailApp.sendEmail(emailAddress, subject, {htmlBody: gBody});
      sheet.getRange(startRow + i, 4).setValue(EMAIL_SENT);
      // Make sure the cell is updated right away in case the script is interrupted
      SpreadsheetApp.flush();
      gBody = hBody; //return previous value 
    }
  }
}

function ClearStat() {
  //this function will clear status 
  
  var jThis = SpreadsheetApp.getActiveSheet();
  var jST = 2 ;
  var jEN = jThis.getLastRow();
  var jValue = '';
  //Logger.log(jEN);
  for (var jRow = jST; jRow <= jEN; jRow++)
  {
    cValue = jThis.getRange(jRow,4).getValue();
    jValue = cValue;
    jThis.getRange(jRow,4).clearContent();
  }
  
}
