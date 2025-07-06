<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Artale 頻道推薦器</title>
  <style>
    body {
      font-family: "Microsoft JhengHei", sans-serif;
      text-align: center;
      padding: 2rem;
      background-color: #f8f9fa;
    }
    input {
      padding: 0.5rem;
      font-size: 1rem;
      margin: 0.5rem;
    }
    button {
      padding: 0.5rem 1rem;
      font-size: 1rem;
      background-color: #007bff;
      color: white;
      border: none;
      border-radius: 4px;
      cursor: pointer;
    }
    button:hover {
      background-color: #0056b3;
    }
    #result {
      margin-top: 2rem;
      padding: 1rem;
      background: white;
      border: 1px solid #ccc;
      border-radius: 6px;
      width: 90%;
      max-width: 500px;
      margin-left: auto;
      margin-right: auto;
      font-size: 1.1rem;
      color: #333;
      line-height: 1.6;
    }
    .footer-note {
      margin-top: 2rem;
      font-size: 0.9rem;
      color: #888;
    }
  </style>
</head>
<body>
  <h1>🎯 Artale 頻道推薦器</h1>
  <p>輸入你的出生年月日，即可獲得今日幸運頻道與衝捲建議</p>
  <input type="date" id="birthdate" />
  <button onclick="recommendChannel()">獲得推薦</button>
  <div id="result"></div>

  <script>
    async function recommendChannel() {
      const birth = document.getElementById("birthdate").value;
      const date = new Date(birth);
      if (isNaN(date.getTime())) {
        document.getElementById("result").innerText = "❗ 請正確輸入生日 (格式: YYYY-MM-DD)";
        return;
      }

      const today = new Date();
      const year = date.getFullYear();
      const month = date.getMonth() + 1;
      const day = date.getDate();
      const zodiac = ["猴", "雞", "狗", "豬", "鼠", "牛", "虎", "兔", "龍", "蛇", "馬", "羊"][year % 12];
      const signs = [
        ["摩羯", 19], ["水瓶", 18], ["雙魚", 20], ["牡羊", 19], ["金牛", 20],
        ["雙子", 20], ["巨蟹", 22], ["獅子", 22], ["處女", 22], ["天秤", 23],
        ["天蠍", 22], ["射手", 21], ["摩羯", 31]
      ];
      const horoscope = day <= signs[month - 1][1] ? signs[month - 1][0] : signs[month][0];

      const seed = today.getFullYear() * 10000 + (today.getMonth() + 1) * 100 + today.getDate();
      const base = (seed + year + month + day) % 3000;

      const mainChannel = (base + 729 + (year % 13)) % 3000;
      const alt1 = (base + 229 + (day % 17)) % 3000;
      const alt2 = (base + 909 + (month % 9)) % 3000;

      const mainStr = mainChannel.toString().padStart(3, "0");
      const alt1Str = alt1.toString().padStart(3, "0");
      const alt2Str = al
