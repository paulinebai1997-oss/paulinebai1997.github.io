<!paulinebai1997.github.io>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8">
  <title>埃及守護神占卜</title>
  <style>
    body {
      font-family: "Microsoft JhengHei", sans-serif;
      text-align: center;
      background: #111 url('https://i1.kknews.cc/d2kbbWiKHd5A_Ci-crOTcAVlK6kuziKQ8g/0.jpg') no-repeat center center fixed;
      background-size: cover;
      color: #fff;
      margin: 0;
      padding: 0;
    }
    header {
      background: rgba(0,0,0,0.6);
      padding: 20px;
      font-size: 28px;
      letter-spacing: 2px;
      text-shadow: 2px 2px 4px #000;
    }
    .box {
      background: rgba(0,0,0,0.75);
      padding: 20px;
      border-radius: 12px;
      margin: 40px auto;
      width: 80%;
      max-width: 700px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.6);
    }
    input, button {
      font-size: 18px;
      padding: 10px;
      margin: 10px;
      border-radius: 6px;
      border: none;
    }
    input {
      width: 60%;
    }
    button {
      background: #d4af37;
      color: #000;
      font-weight: bold;
      cursor: pointer;
      transition: 0.3s;
    }
    button:hover {
      background: #b8902c;
    }
    #result {
      margin-top: 20px;
      text-align: left;
      line-height: 1.6;
    }
    #result h3 {
      text-align: center;
      color: #ffd700;
    }
    .god-img {
      display: block;
      margin: 15px auto;
      max-width: 220px;
      border: 3px solid #d4af37;
      border-radius: 10px;
    }
  </style>
</head>
<body>
  <header>☥ 埃及守護神占卜 ☥</header>
  <div class="box">
    <h2>輸入生日，找出你的守護神</h2>
    <input type="date" id="birthday">
    <button onclick="findGuardian()">開始占卜</button>
    <div id="result"></div>
  </div>

  <script>
    const guardians = [
      {
        name: "尼羅河女神 哈皮 (Hapi)",
        ranges: [["01/01","01/07"],["06/19","06/28"],["09/01","09/07"],["11/18","11/26"]],
        traits: "平衡與和諧，情感豐富，充滿包容與療癒能量",
        gift: "天生帶來和平與穩定的力量，強烈的直覺力與靈性成長潛能",
        mission: "學習如何在流動中保持穩定，提供情感支持與療癒，為世界帶來和諧",
        img: "https://upload.wikimedia.org/wikipedia/commons/thumb/1/1e/Hapy_tying.svg/500px-Hapy_tying.svg.png"
      },
      {
        name: "太陽神 阿蒙 (Amon)",
        ranges: [["01/08","01/21"],["02/01","02/11"]],
        traits: "領導力、創造力、智慧，充滿自信與遠見",
        gift: "強烈的意志力，可影響並激勵他人；具有開創精神",
        mission: "學習謙遜與內在平衡，利用影響力創造更高價值",
        img: "https://upload.wikimedia.org/wikipedia/commons/thumb/5/57/Amun.svg/330px-Amun.svg.png"
      },
      {
        name: "女性之神 姆特 (Mut)",
        ranges: [["01/22","01/31"],["09/08","09/22"]],
        traits: "母性、保護、智慧與耐心",
        gift: "具備強大內在力量，可承載與轉化能量",
        mission: "學習如何在給予與自我照顧之間取得平衡",
        img: "https://upload.wikimedia.org/wikipedia/commons/thumb/9/9d/Mut.svg/375px-Mut.svg.png"
      },
      {
        name: "大地之神 蓋布 (Geb)",
        ranges: [["02/12","02/29"],["08/20","08/31"]],
        traits: "豐盛、穩定、與自然連結",
        gift: "與大自然有深厚連結，能夠帶來豐盛與穩定",
        mission: "學習如何在物質與靈性之間找到平衡",
        img: "https://upload.wikimedia.org/wikipedia/commons/thumb/5/53/Geb.svg/320px-Geb.svg.png"
      },
      {
        name: "冥王 歐西里斯 (Osiris)",
        ranges: [["03/01","03/10"],["11/27","12/18"]],
        traits: "靈魂重生、復興、轉化",
        gift: "具備強大復原能力，能帶領群眾",
        mission: "放下過去，接受新的開始，引導靈性轉化",
        img: "https://upload.wikimedia.org/wikipedia/commons/thumb/8/8b/Standing_Osiris.svg/800px-Standing_Osiris.svg.png"
      },
      {
        name: "魔法女神 伊西斯 (Isis)",
        ranges: [["03/11","03/31"],["10/18","10/29"],["12/19","12/31"]],
        traits: "神聖女性力量、療癒、愛與魔法",
        gift: "能療癒他人，帶來安慰與支持",
        mission: "學習愛自己，運用智慧幫助他人覺醒",
        img: "https://upload.wikimedia.org/wikipedia/commons/thumb/e/ec/Isis.svg/800px-Isis.svg.png"
      },
      {
        name: "智慧之神 托特 (Thoth)",
        ranges: [["04/01","04/19"],["11/08","11/17"]],
        traits: "智慧、溝通、神聖知識",
        gift: "具有高度智慧與學習能力",
        mission: "平衡理性與情感，將知識轉化為靈性工具",
        img: "https://upload.wikimedia.org/wikipedia/commons/thumb/c/c3/Thoth.svg/375px-Thoth.svg.png"
      },
      {
        name: "銳智之眼 荷魯斯 (Horus)",
        ranges: [["04/20","05/07"],["08/12","08/19"]],
        traits: "勇氣、正義、王者之力",
        gift: "具備克服困難的力量，清晰的願景",
        mission: "學習剛強與溫柔的平衡",
        img: "https://upload.wikimedia.org/wikipedia/commons/thumb/c/c2/Horus_standing.svg/330px-Horus_standing.svg.png"
      },
      {
        name: "死神 阿努比斯 (Anubis)",
        ranges: [["05/08","05/27"],["06/29","07/13"]],
        traits: "靈魂守護者、死亡與重生",
        gift: "能感知靈魂真相，適合靈性導師",
        mission: "協助他人進行深層靈魂探索",
        img: "https://upload.wikimedia.org/wikipedia/commons/thumb/6/6d/Anubis_standing.svg/375px-Anubis_standing.svg.png"
      },
      {
        name: "宇宙生命之神 賽斯 (Seth)",
        ranges: [["05/28","06/18"],["09/28","10/02"]],
        traits: "變革、混亂與創造力",
        gift: "能在動盪中找到新機會",
        mission: "調和內在黑暗與光明",
        img: "https://upload.wikimedia.org/wikipedia/commons/thumb/7/7a/Set.svg/800px-Set.svg.png"
      },
      {
        name: "貓面女神 巴斯特 (Bastet)",
        ranges: [["07/14","07/28"],["09/23","09/27"],["10/03","10/17"]],
        traits: "溫柔與力量並存，熱愛藝術與生活",
        gift: "強大的直覺力與保護力",
        mission: "學習在獨立與親密關係中取得平衡",
        img: "https://upload.wikimedia.org/wikipedia/commons/thumb/d/d9/Bastet.svg/375px-Bastet.svg.png"
      },
      {
        name: "獅子女神 賽科邁特 (Sekhmet)",
        ranges: [["07/29","08/11"],["10/30","11/07"]],
        traits: "戰士能量、力量與保護",
        gift: "極強的行動力與領導能力",
        mission: "掌控內在火焰，讓力量與慈悲共存",
        img: "https://upload.wikimedia.org/wikipedia/commons/thumb/3/31/Sekhmet.svg/375px-Sekhmet.svg.png"
      }
    ];

    function inRange(month, day, range) {
      let [sm, sd] = range[0].split("/").map(Number);
      let [em, ed] = range[1].split("/").map(Number);
      let afterStart = (month > sm) || (month === sm && day >= sd);
      let beforeEnd = (month < em) || (month === em && day <= ed);
      return afterStart && beforeEnd;
    }

    function findGuardian() {
      let dateStr = document.getElementById("birthday").value;
      if (!dateStr) {
        document.getElementById("result").innerHTML = "<p>⚠️ 請先輸入生日</p>";
        return;
      }

      let bday = new Date(dateStr);
      let m = bday.getMonth() + 1;
      let d = bday.getDate();

      for (let g of guardians) {
        for (let r of g.ranges) {
          if (inRange(m, d, r)) {
            document.getElementById("result").innerHTML = `
              <h3>☥ 守護神：${g.name}</h3>
              <img src="${g.img}" class="god-img">
              <p><b>象徵特質：</b> ${g.traits}</p>
              <p><b>靈魂天賦：</b> ${g.gift}</p>
              <p><b>靈魂使命：</b> ${g.mission}</p>
            `;
            return;
          }
        }
      }

      document.getElementById("result").innerHTML = "<p>❓ 找不到對應的守護神，請確認生日。</p>";
    }
  </script>
</body>
</html>
