``` js
function onOpen() {
  var sheet = SpreadsheetApp.getActiveSpreadsheet();
  var myMenu=[
    {name: "①タイトル", functionName: "aaa"},
    null,
    {name: "②タイトル", functionName: "bbb"},
  ];
  sheet.addMenu("スクリプト実行", myMenu);
};
```
