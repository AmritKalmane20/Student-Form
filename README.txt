
# Student Submission Form (with Sl No. and Custom Headers)

## Google Sheet Setup

1. Name the sheet: `FormResponses`
2. In the first row, enter these headers:
   Sl No. | Name | Age | Class | E-mail | Phone No.

## Google Apps Script Code

function doPost(e) {
  const sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName("FormResponses");

  const name = e.parameter.name;
  const age = e.parameter.age;
  const studentClass = e.parameter.class;
  const email = e.parameter.email;
  const phone = e.parameter.phone;

  if (!name || !age || !studentClass || !email || !phone) {
    return ContentService.createTextOutput("Incomplete submission").setMimeType(ContentService.MimeType.TEXT);
  }

  if (!email.includes("@") || !email.includes(".")) {
    return ContentService.createTextOutput("Invalid email").setMimeType(ContentService.MimeType.TEXT);
  }

  if (!/^[0-9]{10}$/.test(phone)) {
    return ContentService.createTextOutput("Invalid phone number").setMimeType(ContentService.MimeType.TEXT);
  }

  const lastRow = sheet.getLastRow();
  const slNo = lastRow >= 2 ? sheet.getRange(lastRow, 1).getValue() + 1 : 1;

  sheet.appendRow([slNo, name, age, studentClass, email, phone]);
  return ContentService.createTextOutput("Success").setMimeType(ContentService.MimeType.TEXT);
}

## Deployment Instructions

- Deploy the script as a Web App
- Access: Anyone
- Paste the Web App URL in `index.html` where indicated
- Host the form using any hosting service or local server

