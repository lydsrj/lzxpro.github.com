<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <title>动态文字效果</title>
    <style>
        body {
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f0f0f0;
            transition: background-color 0.5s;
            flex-direction: column;
        }

        .btn {
            padding: 20px 40px;
            font-size: 24px;
            border: none;
            border-radius: 50px;
            background-color: #4CAF50;
            color: white;
            cursor: pointer;
            transition: transform 0.3s;
        }

        .btn:hover {
            transform: scale(1.1);
            background-color: #45a049;
        }

        .text-container {
            display: none;
            gap: 15px;
            flex-wrap: wrap;
            justify-content: center;
            align-items: center;
        }

        .text-container span {
            display: inline-block;
            color: #ff4081;
            font-family: 'Microsoft YaHei', sans-serif;
            animation-duration: 2s;
            animation-iteration-count: infinite;
            animation-direction: alternate;
        }

        .full-screen-text {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: #e0f7fa;
            justify-content: center;
            align-items: center;
            flex-wrap: wrap;
            overflow: auto;
            padding: 20px;
            box-sizing: border-box;
        }

        .full-screen-text span {
            display: inline-block;
            color: #ff4081;
            font-family: 'Microsoft YaHei', sans-serif;
            animation-duration: 2s;
            animation-iteration-count: infinite;
            animation-direction: alternate;
            margin: 10px;
        }

        @keyframes resize1 {
            from { font-size: 20px; }
            to { font-size: 50px; }
        }

        @keyframes resize2 {
            from { font-size: 30px; }
            to { font-size: 60px; }
        }

        @keyframes resize3 {
            from { font-size: 25px; }
            to { font-size: 55px; }
        }

        @keyframes resize4 {
            from { font-size: 35px; }
            to { font-size: 65px; }
        }

        @keyframes resize5 {
            from { font-size: 40px; }
            to { font-size: 70px; }
        }
    </style>
</head>
<body>
    <button class="btn" onclick="showText()">点击显示文字</button>
    <div class="text-container">
        <span style="animation-name: resize1;">林</span>
        <span style="animation-name: resize2;">子</span>
        <span style="animation-name: resize3;">萱</span>
        <span style="animation-name: resize4;">你</span>
        <span style="animation-name: resize5;">在</span>
        <span style="animation-name: resize1;">干</span>
        <span style="animation-name: resize2;">什</span>
        <span style="animation-name: resize3;">么</span>
    </div>

    <div class="full-screen-text" id="fullScreenText">
        <!-- 这里会动态生成满屏幕的“林子萱你在干什么” -->
    </div>

    <script>
        function showText() {
            const btn = document.querySelector('.btn');
            const textContainer = document.querySelector('.text-container');
            const body = document.querySelector('body');

            btn.style.display = 'none';
            textContainer.style.display = 'flex';
            body.style.backgroundColor = '#e0f7fa';

            // 添加一个新的按钮
            const newBtn = document.createElement('button');
            newBtn.className = 'btn';
            newBtn.textContent = '满屏幕显示';
            newBtn.onclick = showFullScreenText;
            body.appendChild(newBtn);
        }

        function showFullScreenText() {
            const fullScreenText = document.getElementById('fullScreenText');
            fullScreenText.style.display = 'flex';

            // 清空之前的内容
            fullScreenText.innerHTML = '';

            // 生成满屏幕的“林子萱你在干什么”
            const text = '林子萱你在干什么';
            for (let i = 0; i < 100; i++) {
                const span = document.createElement('span');
                span.textContent = text;

                // 随机分配动画效果
                const animationIndex = Math.floor(Math.random() * 5) + 1;
                span.style.animationName = `resize${animationIndex}`;

                // 点击后消失
                span.onclick = () => {
                    fullScreenText.style.display = 'none';
                };

                fullScreenText.appendChild(span);
            }
        }
    </script>
</body>
</html>
