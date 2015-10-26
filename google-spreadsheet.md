[TOC]

# Overview

# Functions
## IMPORTXML

# Examples

```javascript
function getSpreadsheetId() {
  Logger.log('Spreadsheet key: ' + SpreadsheetApp.getActiveSpreadsheet().getId());
};

function onOpen() {
  //  Get active SpreadSheet
  var sheet = SpreadsheetApp.getActiveSpreadsheet();

  //  Add menu with entries
  var entries = [{name:"Generate RewriteRule",functionName:"GenerateRewriteRule"}];
  sheet.addMenu("Functions", entries);
};

function rewriteRuleMoto301() {
  //  Get active SpreadSheet
  var ss = SpreadsheetApp.getActiveSpreadsheet();

  //  Get sheet by name
  var s = ss.getSheetByName("rewrite_rule_moto_301");

  //  Get range of model search key
  //  Maybe need modify Range to get
  //  Because sheet is modified before
  var searchKeyV2 = s.getRange("A103:A323").getValues();
  var searchKeyV3 = s.getRange("B103:B323").getValues();
  var modelMaker = s.getRange("F103:F323").getValues();

  generatePatternV2(s, searchKeyV2);
  generateSubstitutionV3(s, searchKeyV3);
  generateRewriteRule(s);
  generateLocalTestLink(s, searchKeyV2, modelMaker);
  generateExpectedLocalTestLink(s, searchKeyV3, modelMaker);
  generateAWSTestLink(s, searchKeyV2, modelMaker);
  generateExpectedAWSTestLink(s, searchKeyV3, modelMaker);

};

function generatePatternV2(s, searchKeyV2) {
  for (var row=0; row<searchKeyV2.length; row++) {
    for (var col=0; col<searchKeyV2[row].length; col++) {
//      Logger.log(s.getRange(row+103, col+1).getValue());
      s.getRange(row+103, col+3).setValue('^(.*)/' + searchKeyV2[row][col] + '/(.*)$');
    }
  }
};

function generateSubstitutionV3(s, searchKeyV3) {
  for (var row=0; row<searchKeyV3.length; row++) {
    for (var col=0; col<searchKeyV3[row].length; col++) {
//      Logger.log(s.getRange(row+103, col+1).getValue());
      s.getRange(row+103, col+4).setValue('$1/' + searchKeyV3[row][col] + '/$2');
    }
  }
};

function generateRewriteRule(s) {
  var linkModelV2 = s.getRange("C103:C323").getValues();
  var linkModelV3 = s.getRange("D103:D323").getValues();
  for (var row=0; row<linkModelV2.length; row++) {
    for (var col=0; col<linkModelV2[row].length; col++) {
      s.getRange(row+103, col+5).setValue('RewriteRule ' + linkModelV2[row][col] + ' ' + linkModelV3[row][col] + '');
    }
  }
};

function generateLocalTestLink(s, searchKeyV2, modelMaker) {
  for (var row=0; row<searchKeyV2.length; row++) {
    for (var col=0; col<searchKeyV2[row].length; col++) {
      s.getRange(row+103, col+7).setValue('http://192.168.33.15/' + modelMaker[row][col] + '/' + searchKeyV2[row][col] + '/list/');
    }
  }
};

function generateExpectedLocalTestLink(s, searchKeyV3, modelMaker) {
  for (var row=0; row<searchKeyV3.length; row++) {
    for (var col=0; col<searchKeyV3[row].length; col++) {
      s.getRange(row+103, col+8).setValue('http://192.168.33.15/' + modelMaker[row][col] + '/' + searchKeyV3[row][col] + '/list/');
    }
  }
};

function generateAWSTestLink(s, searchKeyV2, modelMaker) {
  for (var row=0; row<searchKeyV2.length; row++) {
    for (var col=0; col<searchKeyV2[row].length; col++) {
      s.getRange(row+103, col+9).setValue('http://54.248.223.71/' + modelMaker[row][col] + '/' + searchKeyV2[row][col] + '/list/');
    }
  }
};

function generateExpectedAWSTestLink(s, searchKeyV3, modelMaker) {
  for (var row=0; row<searchKeyV3.length; row++) {
    for (var col=0; col<searchKeyV3[row].length; col++) {
      s.getRange(row+103, col+10).setValue('http://54.248.223.71/' + modelMaker[row][col] + '/' + searchKeyV3[row][col] + '/list/');
    }
  }
};

function _301ModelNew() {
  //  Get active SpreadSheet
  var ss = SpreadsheetApp.getActiveSpreadsheet();

  //  Get sheet by name
  var s = ss.getSheetByName("301_model_new");

  //  Get range of model search key
  //  Maybe need modify Range to get
  //  Because sheet is modified before
  var v2Range = s.getRange("C39:C259").getValues();
  var v3Range = s.getRange("E39:E259").getValues();

  checkModelV3SameV2(s, v2Range, v3Range);
};

function checkModelV3SameV2(s, v2Range, v3Range) {
  for (var rowV3=0; rowV3<v3Range.length; rowV3++) {
    for (var colV3=0; colV3<v3Range[rowV3].length; colV3++) {
      for (var rowV2=0; rowV2<v2Range.length; rowV2++) {
        for (var colV2=0; colV2<v2Range[rowV2].length; colV2++) {
          if (v3Range[rowV3][colV3] == v2Range[rowV2][colV2]) {
//            s.getRange(rowV3+1,colV3+5).setValue(v2Range[rowV2][colV2]);
//            s.getRange(rowV3+1,colV3+6).setValue(v3Range[rowV3][colV3]);
            Logger.log(v2Range[rowV2][colV2]);
          }
        }
      }
    }
  }
};
```
