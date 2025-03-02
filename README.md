<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Прогресс работы</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 20px;
        }
        .progress-container {
            width: 40%;
            background: #ddd;
            border-radius: 5px;
            overflow: hidden;
            height: 30px;
            margin-top: 20px;
        }
        .progress-bar {
            height: 100%;
            background: #4caf50;
            width: 0%;
            transition: width 0.5s;
        }
        input {
            width: 80px;
            padding: 5px;
            margin: 5px;
        }
    </style>
</head>
<body>

    <h2>Визуализатор прогресса</h2>
    
    <label>Всего страниц: <input type="number" id="total" min="1"></label>
    <label>Пройдено: <input type="number" id="completed" min="0"></label>
    <button onclick="saveProgress()">Сохранить</button>

    <div class="progress-container">
        <div class="progress-bar" id="progress-bar"></div>
    </div>
    
    <p id="progress-text">Прогресс: 0%</p>

    <script>
        function saveProgress() {
            let total = parseInt(document.getElementById("total").value) || 1;
            let completed = parseInt(document.getElementById("completed").value) || 0;
            
            if (completed > total) completed = total; // Защита от неверных значений

            let progress = (completed / total) * 100;

            // Сохранение в localStorage
            localStorage.setItem("totalPages", total);
            localStorage.setItem("completedPages", completed);

            updateProgress(progress);
        }

        function updateProgress(progress) {
            document.getElementById("progress-bar").style.width = progress + "%";
            document.getElementById("progress-text").textContent = "Прогресс: " + progress.toFixed(1) + "%";
        }

        function loadProgress() {
            let total = localStorage.getItem("totalPages") || 100;
            let completed = localStorage.getItem("completedPages") || 0;

            document.getElementById("total").value = total;
            document.getElementById("completed").value = completed;

            updateProgress((completed / total) * 100);
        }

        // Загрузка данных при открытии страницы
        window.onload = loadProgress;
    </script>

</body>
</html>
