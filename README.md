&lt;!DOCTYPE html&gt;
&lt;html lang=&quot;tr&quot;&gt;
&lt;head&gt;
  &lt;meta charset=&quot;UTF-8&quot;&gt;
  &lt;title&gt;Benimle Çıkar Mısın?&lt;/title&gt;
  &lt;style&gt;
    body {
      font-family: &#039;Segoe UI&#039;, sans-serif;
      background-color: #fff0f5;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      margin: 0;
      transition: background-color 0.5s;
    }

    h1 {
      font-size: 2em;
      color: #d63384;
      margin-bottom: 20px;
    }

    button {
      padding: 12px 24px;
      margin: 10px;
      font-size: 1.2em;
      border: none;
      border-radius: 12px;
      cursor: pointer;
      transition: 0.3s ease;
      position: relative;
    }

    #yesBtn {
      background-color: #28a745;
      color: white;
    }

    #yesBtn:hover {
      background-color: #218838;
    }

    #noBtn {
      background-color: #dc3545;
      color: white;
      position: absolute;
    }

    #response {
      margin-top: 30px;
      font-size: 1.5em;
      color: #343a40;
    }
  &lt;/style&gt;
&lt;/head&gt;
&lt;body&gt;
  &lt;h1&gt;Benimle çıkar mısın?&lt;/h1&gt;
  &lt;div style=&quot;position: relative; height: 100px; width: 300px;&quot;&gt;
    &lt;button id=&quot;yesBtn&quot;&gt;Evet&lt;/button&gt;
    &lt;button id=&quot;noBtn&quot;&gt;Hayır&lt;/button&gt;
  &lt;/div&gt;
  &lt;div id=&quot;response&quot;&gt;&lt;/div&gt;

  &lt;script&gt;
    const yesBtn = document.getElementById(&#039;yesBtn&#039;);
    const noBtn = document.getElementById(&#039;noBtn&#039;);
    const responseDiv = document.getElementById(&#039;response&#039;);
    const body = document.body;

    let hoverCount = 0;

    // &quot;Evet&quot; butonuna tıklanınca:
    yesBtn.addEventListener(&#039;click&#039;, () =&gt; {
      responseDiv.textContent = &quot; Seçimini instagramdanda iletir misin 🐇❤️&quot;;
      body.style.backgroundColor = &quot;#ffe6f0&quot;;
      saveAnswer(&quot;Evet&quot;);
    });

    // &quot;Hayır&quot; butonuna tıklanınca:
    noBtn.addEventListener(&#039;click&#039;, () =&gt; {
      responseDiv.textContent = &quot;...&quot;;
      body.style.backgroundColor = &quot;#ccc&quot;;
      saveAnswer(&quot;Hayır&quot;);
    });

    // Hayır butonuna fare yaklaşınca kaçsın
    noBtn.addEventListener(&#039;mouseenter&#039;, () =&gt; {
      const container = noBtn.parentElement;
      const maxX = container.clientWidth - noBtn.offsetWidth;
      const maxY = container.clientHeight - noBtn.offsetHeight;
      const randomX = Math.floor(Math.random() * maxX);
      const randomY = Math.floor(Math.random() * maxY);
      noBtn.style.left = `${randomX}px`;
      noBtn.style.top = `${randomY}px`;

      hoverCount++;
      if (hoverCount &gt;= 5) {
        responseDiv.textContent = &quot;😅 Hayıra basamazsın!&quot;;
      }
    });

    // Basit &quot;veritabanı&quot; simülasyonu: tarayıcıya kaydetme
    function saveAnswer(answer) {
      const logs = JSON.parse(localStorage.getItem(&quot;cevaplar&quot;) || &quot;[]&quot;);
      logs.push({ cevap: answer, zaman: new Date().toLocaleString() });
      localStorage.setItem(&quot;cevaplar&quot;, JSON.stringify(logs));
    }

    // Sayfa yüklendiğinde önceki cevapları konsola yaz
    window.onload = () =&gt; {
      const logs = JSON.parse(localStorage.getItem(&quot;cevaplar&quot;) || &quot;[]&quot;);
      console.log(&quot;Cevap geçmişi:&quot;, logs);
    };
  &lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;
