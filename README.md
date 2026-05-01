<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Игровая анимация | Добро пожаловать</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            min-height: 100vh;
            background: linear-gradient(135deg, #0a0f1e 0%, #0f172a 50%, #1e1b4b 100%);
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: 'Courier New', 'Press Start 2P', 'Fira Code', monospace;
            overflow: hidden;
            position: relative;
        }

        /* Игровой фон с "снегом" из пикселей */
        body::before {
            content: '';
            position: absolute;
            width: 100%;
            height: 100%;
            background-image: 
                radial-gradient(2px 2px at 20px 30px, #fff, rgba(0,0,0,0)),
                radial-gradient(2px 2px at 40px 70px, #ff6b6b, rgba(0,0,0,0)),
                radial-gradient(1px 1px at 90px 120px, #4ecdc4, rgba(0,0,0,0)),
                radial-gradient(3px 3px at 150px 50px, #ffe66d, rgba(0,0,0,0));
            background-size: 200px 200px;
            background-repeat: repeat;
            opacity: 0.4;
            animation: floatPixels 20s linear infinite;
            pointer-events: none;
        }

        @keyframes floatPixels {
            from { transform: translateY(0px) translateX(0px); }
            to { transform: translateY(-200px) translateX(50px); }
        }

        /* Главный контейнер */
        .game-container {
            text-align: center;
            z-index: 10;
            padding: 2rem;
            background: rgba(0, 0, 0, 0.6);
            backdrop-filter: blur(8px);
            border-radius: 32px;
            border: 2px solid rgba(78, 205, 196, 0.5);
            box-shadow: 0 0 50px rgba(78, 205, 196, 0.3), inset 0 0 20px rgba(78, 205, 196, 0.2);
            animation: borderPulse 2s infinite alternate;
        }

        @keyframes borderPulse {
            0% { border-color: rgba(78, 205, 196, 0.3); box-shadow: 0 0 30px rgba(78, 205, 196, 0.2); }
            100% { border-color: rgba(255, 107, 107, 0.8); box-shadow: 0 0 80px rgba(255, 107, 107, 0.5); }
        }

        /* Анимированное приветствие */
        .glitch-text {
            font-size: 4rem;
            font-weight: bold;
            color: #fff;
            text-transform: uppercase;
            position: relative;
            text-shadow: 0.05em 0 0 rgba(255,0,0,0.75), -0.05em -0.025em 0 rgba(0,255,0,0.75);
            animation: glitch 1.5s infinite;
            letter-spacing: 4px;
        }

        @keyframes glitch {
            0% { text-shadow: 0.05em 0 0 rgba(255,0,0,0.75), -0.05em -0.025em 0 rgba(0,255,0,0.75); }
            14% { text-shadow: 0.05em 0 0 rgba(255,0,0,0.75), -0.05em -0.025em 0 rgba(0,255,0,0.75); }
            15% { text-shadow: -0.05em -0.025em 0 rgba(255,0,0,0.75), 0.025em 0.05em 0 rgba(0,255,0,0.75); }
            49% { text-shadow: -0.05em -0.025em 0 rgba(255,0,0,0.75), 0.025em 0.05em 0 rgba(0,255,0,0.75); }
            50% { text-shadow: 0.025em 0.05em 0 rgba(255,0,0,0.75), 0.05em 0 0 rgba(0,255,0,0.75); }
            99% { text-shadow: 0.025em 0.05em 0 rgba(255,0,0,0.75), 0.05em 0 0 rgba(0,255,0,0.75); }
            100% { text-shadow: -0.025em 0 0 rgba(255,0,0,0.75), -0.025em -0.025em 0 rgba(0,255,0,0.75); }
        }

        /* Дополнительный текст */
        .welcome-sub {
            font-size: 1.2rem;
            color: #4ecdc4;
            margin-top: 1rem;
            font-family: monospace;
            border-right: 2px solid #4ecdc4;
            white-space: nowrap;
            overflow: hidden;
            width: 0;
            animation: typing 3s steps(30, end) forwards, blinkCursor 0.75s step-end infinite;
            display: inline-block;
        }

        @keyframes typing {
            from { width: 0; }
            to { width: 100%; }
        }

        @keyframes blinkCursor {
            from, to { border-color: transparent; }
            50% { border-color: #4ecdc4; }
        }

        /* Игровая кнопка */
        .game-btn {
            margin-top: 2rem;
            padding: 12px 32px;
            font-size: 1.2rem;
            font-family: monospace;
            font-weight: bold;
            background: transparent;
            color: #ffe66d;
            border: 2px solid #ffe66d;
            cursor: pointer;
            transition: all 0.3s ease;
            text-transform: uppercase;
            letter-spacing: 2px;
            position: relative;
            overflow: hidden;
        }

        .game-btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: #ffe66d;
            transition: left 0.3s ease;
            z-index: -1;
        }

        .game-btn:hover {
            color: #0f172a;
            border-color: #ffe66d;
            box-shadow: 0 0 20px #ffe66d;
        }

        .game-btn:hover::before {
            left: 0;
        }

        /* Пиксельные человечки (декор) */
        .pixel-man {
            position: absolute;
            bottom: 10%;
            left: 10%;
            font-size: 2rem;
            filter: drop-shadow(0 0 5px #4ecdc4);
            animation: walk 6s linear infinite;
        }

        .pixel-man2 {
            bottom: 15%;
            left: auto;
            right: 10%;
            animation-delay: -2s;
            animation-duration: 7s;
        }

        @keyframes walk {
            0% { transform: translateX(-20px); opacity: 1; }
            50% { transform: translateX(calc(100vw - 150px)); opacity: 0.8; }
            100% { transform: translateX(-20px); opacity: 1; }
        }

        /* Адаптив */
        @media (max-width: 768px) {
            .glitch-text { font-size: 2rem; }
            .welcome-sub { font-size: 0.7rem; white-space: normal; animation: none; width: auto; border-right: none; }
            .pixel-man { display: none; }
        }
    </style>
</head>
<body>
    <div class="game-container">
        <div class="glitch-text">
            🎮 WELCOME 🎮
        </div>
        <div class="welcome-sub">
            > ДОБРО ПОЖАЛОВАТЬ, ИГРОК! <
        </div>
        <div class="glitch-text" style="font-size: 2rem; margin-top: 1rem;">
            READY PLAYER ONE
        </div>
        <button class="game-btn" onclick="alert('Игра начинается! 🚀')">
            ▶ СТАРТ
        </button>
    </div>

    <!-- Пиксельные декорации -->
    <div class="pixel-man">👾</div>
    <div class="pixel-man pixel-man2">🕹️</div>
    <div class="pixel-man" style="bottom: 30%; animation-duration: 12s; left: 20%;">🎮</div>
</body>
</html>
