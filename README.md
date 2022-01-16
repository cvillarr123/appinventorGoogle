# appinventorGoogle
AppInventorPonerImagenenGoogleDrive
Se tomo como referencia estos links

https://www.youtube.com/watch?v=AmGqQFOCdaQ
y el script actualizado
https://groups.google.com/g/mitappinventortest/c/jW7cvVkfgCk




Script a pegar en el google extension

function doGet(e) {
return message("Error: no parameters in doGet");
   
}

function doPost(e) {
 if (!e.parameters.filename || !e.parameters.file || !e.parameters.imageformat) {
   return message("Error: Bad parameters in doPost");
 } else {
   var imgf = e.parameters.imageformat[0].toUpperCase();
   var mime =
       (imgf == 'BMP')  ? MimeType.BMP
     : (imgf == 'GIF')  ? MimeType.GIF
     : (imgf == 'JPEG') ? MimeType.JPEG
     : (imgf == 'JPG')  ? MimeType.JPEG
     : (imgf == 'PNG')  ? MimeType.PNG
     : (imgf == 'SVG')  ? MimeType.SVG
     : false;
   if (mime) {
     var data = Utilities.base64Decode(e.parameters.file, Utilities.Charset.UTF_8);
     var blob = Utilities.newBlob(data, mime, e.parameters.filename);
     DriveApp.getFolderById('1yJSFRF_CLtELaoHESsHDu2pNqYfcOdkp').createFile(blob);
     return message("Success");
   } else {
     return message("Error: Bad image format");
   }
 }
}

function message(msg) {
 return ContentService.createTextOutput(JSON.stringify({Result: msg })).setMimeType(ContentService.MimeType.JSON);
}
