<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>أذكار الموصل</title>
    <style>
        :root { --primary: #2c3e50; --accent: #27ae60; --bg: #f8f9fa; }
        body { font-family: 'Segoe UI', Tahoma, sans-serif; background: var(--bg); color: var(--primary); margin: 0; padding: 20px; }
        .header { background: var(--primary); color: white; padding: 20px; border-radius: 15px; margin-bottom: 20px; box-shadow: 0 4px 6px rgba(0,0,0,0.1); }
        .card { background: white; border-radius: 12px; padding: 20px; margin-bottom: 15px; box-shadow: 0 2px 4px rgba(0,0,0,0.05); transition: 0.3s; border-right: 5px solid var(--accent); }
        .count-btn { background: var(--accent); color: white; border: none; padding: 12px 25px; border-radius: 8px; font-size: 1.1rem; cursor: pointer; width: 100%; margin-top: 10px; }
        .count-btn:disabled { background: #bdc3c7; cursor: default; }
        .time-info { font-size: 0.9rem; opacity: 0.8; }
    </style>
</head>
<body>

<div class="header">
    <h1>أذكار المسلم</h1>
    <p id="city-time">توقيت الموصل الآن: <span id="clock">--:--</span></p>
    <p id="suggested-dhikr">استعن بالله وابدأ ذكرك</p>
</div>

<div id="dhikr-list"></div>

<script>
    const azkar = [
        { text: "أصبحنا وأصبح الملك لله، والحمد لله ولا إله إلا الله وحده لا شريك له", count: 1, type: "صباح" },
        { text: "اللهم بك أصبحنا وبك أمسينا وبك نحيا وبك نموت وإليك النشور", count: 1, type: "صباح" },
        { text: "سبحان الله وبحمده", count: 100, type: "كلاهما" },
        { text: "أستغفر الله وأتوب إليه", count: 100, type: "كلاهما" }
    ];

    function updateClock() {
        const now = new Date();
        const timeStr = now.toLocaleTimeString('ar-EG', { hour: '2-digit', minute: '2-digit', hour12: true });
        document.getElementById('clock').innerText = timeStr;
        
        const hour = now.getHours();
        const status = document.getElementById('suggested-dhikr');
        if (hour >= 4 && hour < 11) status.innerText = "وقت أذكار الصباح";
        else if (hour >= 15 && hour < 19) status.innerText = "وقت أذكار المساء";
        else status.innerText = "وقت الذكر المطلق";
    }

    function renderAzkar() {
        const list = document.getElementById('dhikr-list');
        azkar.forEach((item, index) => {
            const card = document.createElement('div');
            card.className = 'card';
            card.innerHTML = 
                <p style="font-size: 1.2rem; line-height: 1.6;">${item.text}</p>
                <button class="count-btn" id="btn-${index}" onclick="decrease(${index})">العدد المتبقي: ${item.count}</button>
            ;
            list.appendChild(card);
        });
    }

    let counters = azkar.map(a => a.count);

    function decrease(idx) {
        if (counters[idx] > 0) {
            counters[idx]--;
            const btn = document.getElementById(btn-${idx});
            btn.innerText = counters[idx] === 0 ? "تم بحمد الله" : العدد المتبقي: ${counters[idx]};
            if (counters[idx] === 0) btn.disabled = true;
            if (navigator.vibrate) navigator.vibrate(50);
        }
    }

    setInterval(updateClock, 1000);
    renderAzkar();
    updateClock();
</script>
</body>
</html>
