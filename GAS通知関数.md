GAS（Google Apps Script）で通知したい時用の簡易メモ。

``` js
function myFunction() {
  var msg = "test";

  mail(msg);
  slack(msg);
  line(msg);
  chatwork(msg);
  hangout(msg);
}
```

## Mail

``` js
function mail(message) {
  var to = "***@gmail.com";
  var subject = "test";
  MailApp.sendEmail({
    to: to,
    subject: subject,
    body: message,
  });
}
```

## Slack
- Incoming WebHooksを設定。
  - https://slack.com/apps/A0F7XDUAZ--web-
  - 設定を追加　＞　「Webhook URL」をメモ。

``` js
function slack(message) {
  var postUrl = 'https://hooks.slack.com/services/******************'; // Incoming WebHooksで発行したURL
  var jsonData =
  {
     "text" : message
  };
  var payload = JSON.stringify(jsonData);
  var options =
  {
    "method" : "post",
    "contentType" : "application/json",
    "payload" : payload
  };
  UrlFetchApp.fetch(postUrl, options);
}
```

## LINE
- LINE Notify
  - https://notify-bot.line.me/ja/
- マイページ　＞　トークンを発行する
  - トークン名
    - LINEで通知を受け取る際に一番上に表示される名前。「自動通知」などに。
  - 通知を送信するトークルーム
    - 送信したいLINEグループを選ぶ。但し、最初は「1:1でLINE Notifyから通知を受け取る」でテストを。
- トークンをメモする
  - 一度しか表示されないので必ずメモを。
  - 忘れてしまったら再度トークン発行で対応。


``` js
function line(message){
  var token = "******************"; // LINENotifyで発行したトークン
  var api = "https://notify-api.line.me/api/notify";
  var options =
   {
     "method"  : "post",
     "payload" : {"message": message, }, 
     "headers" : {"Authorization" : "Bearer "+ token}
   };
   UrlFetchApp.fetch(api,options);
}
```

## Chatwork
- Chatwork　＞　「API設定」　＞　API Tokenを取得　＞　API Tokenをメモ
- Chatworkのライブラリを追加
  - GAS　＞　「リソース」 ＞　「ライブラリ」　＞　M6TcEyniCs1xb3sdXFF_FhI-MNonZQ_sT　＞　一番新しい番号のバージョンを選択
- ChatworkのルームID
  - $!ridXXXXX の数字がルームID

``` js
function chatwork(message){
  var client = ChatWorkClient.factory({token: "****************"}); // Chatwork API トークンを記載
  client.sendMessage({
    room_id: **********, // チャットを通知したいグループチャットのIDを記載。#!ridはいらない。
    body: message
  }); 
}
```

## Hangout
- チャットルーム名　＞　Webhookを設定

``` js
function hangout(message) {
  var url = 'https://chat.googleapis.com/**********************'; //　WebhookのURLを記載
  var msg = { 'text' : message }
  var options = {
    'method': 'POST',
    'headers' : {
      'Content-Type': 'application/json; charset=UTF-8'
    },
    'payload':JSON.stringify(msg)
  };
  UrlFetchApp.fetch(url, options);
}
```
