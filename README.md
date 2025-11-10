<!DOCTYPE html>
<html lang="az">
<head>
<meta charset="UTF-8">
<title>Başlaya toxun</title>
<style>
    body {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        height: 100vh;
        background-color: #111;
        color: white;
        font-family: Arial, sans-serif;
    }

    /* Başla düyməsi yanıb-sönmə */
    #start {
        font-size: 48px;
        color: #ff4081;
        text-decoration: none;
        cursor: pointer;
        animation: blink 1s infinite;
        margin-bottom: 20px;
    }

    @keyframes blink {
        0%,50%,100% {opacity:1;}
        25%,75% {opacity:0;}
    }

    .hidden { display: none; }

    .button-like {
        font-size: 28px;
        padding: 10px 20px;
        margin: 10px;
        border: 2px solid #ff4081;
        border-radius: 8px;
        cursor: pointer;
        background-color: transparent;
        color: #ff4081;
        transition: 0.2s;
        text-align: center;
    }

    .button-like:hover { 
        background-color: #ff4081; 
        color: black; 
    }

    #heartCanvas {
        display: none;
        margin-top: 20px;
        background-color: black;
    }

    #finalText {
        font-size: 32px;
        color: #7CFC00; /* tünd yaşıl */
        text-align: center;
        margin-top: 10px;
        font-weight: bold;
    }
</style>
</head>
<body>

    <!-- Başla düyməsi -->
    <a href="#" id="start">Başla</a>

    <!-- Sual ekranı -->
    <div id="questionScreen" class="hidden">
        <div id="questionText" style="font-size:28px; margin-bottom:20px;">Pişikləri sevirsən?</div>
        <div id="yesBtn" class="button-like">Hə</div>
        <div id="noBtn" class="button-like">Yox</div>
    </div>

    <!-- Yox cavabı ekranı -->
    <div id="noScreen" class="hidden">
        <div style="font-size:28px; margin-bottom:20px;">Hə de gör nə deyirəm</div>
        <div id="backBtn" class="button-like">Geri dön</div>
    </div>

    <!-- Ürək və final yazısı -->
    <canvas id="heartCanvas" width="500" height="500"></canvas>
    <div id="finalText" class="hidden">Afərin Gözəllik✨</div>

    <script>
        // Elementləri götür
        const start = document.getElementById("start");
        const questionScreen = document.getElementById("questionScreen");
        const yesBtn = document.getElementById("yesBtn");
        const noBtn = document.getElementById("noBtn");
        const noScreen = document.getElementById("noScreen");
        const backBtn = document.getElementById("backBtn");
        const heartCanvas = document.getElementById("heartCanvas");
        const finalText = document.getElementById("finalText");
        const ctx = heartCanvas.getContext("2d");

        // Başla düyməsi
        start.addEventListener("click", function(e){
            e.preventDefault();
            start.classList.add("hidden");
            questionScreen.classList.remove("hidden");
        });

        // Yox düyməsi
        noBtn.addEventListener("click", function(){
            questionScreen.classList.add("hidden");
            noScreen.classList.remove("hidden");
        });

        // Geri dön
        backBtn.addEventListener("click", function(){
            noScreen.classList.add("hidden");
            questionScreen.classList.remove("hidden");
        });

        // Hə düyməsi
        yesBtn.addEventListener("click", function(){
            questionScreen.classList.add("hidden");
            heartCanvas.style.display = "block";
            finalText.classList.remove("hidden");
            drawHeart();
        });

        // Lazer ürək funksiyası
        function drawHeart() {
            ctx.clearRect(0,0,heartCanvas.width,heartCanvas.height);

            let t = 0;
            const heartX = 250, heartY = 250;
            const scale = 250; // böyük ölçü

            function animateHeart() {
                t += 0.03;
                if(t > 2*Math.PI) return;

                let x = heartX + scale * 16 * Math.pow(Math.sin(t),3) /16;
                let y = heartY - scale * (13*Math.cos(t) - 5*Math.cos(2*t) - 2*Math.cos(3*t) - Math.cos(4*t))/16;

                ctx.beginPath();
                ctx.arc(x, y, 3, 0, Math.PI*2);
                ctx.fillStyle = "#006400"; // tünd yaşıl
                ctx.fill();

                requestAnimationFrame(animateHeart);
            }

            animateHeart();
        }
    </script>
</body>
</html>
