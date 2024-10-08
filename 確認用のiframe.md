``` html
<!DOCTYPE html>
<html lang="ja">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>確認用</title>
    <style>
        html,
        body {
            height: 100%;
            margin: 0;
            overflow: hidden;
        }

        .fullheight {
            height: 95%;
            width: 100%;
        }

        .selectbox {
            text-align: center;
            margin-top: 10px;
        }
    </style>
</head>

<body>
    <div class="selectbox"> <select id="selectdata">
            <option value="index1.html">1つ目のファイル</option>
            <option value="index2.html">2つ目のファイル</option>
            <option value="index3.html">3つ目のファイル</option>
        </select> </div> <iframe src="index1.html" frameborder="0" class="fullheight" id="targetframe"></iframe>
    <script>
        var select = document.getElementById('selectdata');
        select.onchange = function () {
            document.getElementById("targetframe").src = this.value;
        }
    </script>
</body>

</html>
```