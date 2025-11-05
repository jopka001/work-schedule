
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>📅 Расписание бригад</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: 'Segoe UI', sans-serif; min-height: 100vh; padding: 20px; transition: all 0.3s ease; }
        .theme-blue { background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); color: #333; }
        .theme-ocean { background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%); color: #333; }
        .theme-sunset { background: linear-gradient(135deg, #fa709a 0%, #fee140 100%); color: #333; }
        .theme-purple { background: linear-gradient(135deg, #a18cd1 0%, #fbc2eb 100%); color: #333; }
        .theme-forest { background: linear-gradient(135deg, #11998e 0%, #38ef7d 100%); color: #333; }
        .theme-fire { background: linear-gradient(135deg, #ff6b6b 0%, #ffa726 100%); color: #333; }
        .theme-space { background: linear-gradient(135deg, #0c0c0c 0%, #2c3e50 100%); color: #ecf0f1; }
        .theme-lavender { background: linear-gradient(135deg, #e0c3fc 0%, #8ec5fc 100%); color: #333; }
        .container { max-width: 500px; margin: 0 auto; background: rgba(255,255,255,0.95); border-radius: 20px; padding: 25px; box-shadow: 0 15px 35px rgba(0,0,0,0.2); }
        .theme-space .container { background: rgba(44,62,80,0.95); color: #ecf0f1; }
        header { text-align: center; margin-bottom: 25px; }
        h1 { font-size: 1.8em; margin-bottom: 8px; background: linear-gradient(135deg, #667eea, #764ba2); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
        .controls { display: flex; flex-direction: column; gap: 10px; margin-bottom: 20px; }
        .btn { padding: 14px 16px; border: none; border-radius: 12px; font-size: 15px; font-weight: 600; cursor: pointer; transition: all 0.3s ease; text-align: center; }
        .btn:hover { transform: translateY(-3px); box-shadow: 0 8px 20px rgba(0,0,0,0.3); }
        .btn-primary { background: linear-gradient(135deg, #667eea, #764ba2); color: white; }
        .btn-secondary { background: linear-gradient(135deg, #fd746c, #ff9068); color: white; }
        .btn-success { background: linear-gradient(135deg, #11998e, #38ef7d); color: white; }
        .btn-support { background: linear-gradient(135deg, #e65c00, #F9D423); color: white; }
        .section { margin: 12px 0; padding: 18px; border-radius: 15px; background: rgba(255,255,255,0.9); border: 2px solid rgba(255,255,255,0.5); }
        .theme-space .section { background: rgba(44,62,80,0.9); border-color: rgba(255,255,255,0.1); }
        .hidden { display: none; }
        input, textarea, select { width: 100%; padding: 12px; margin: 10px 0; border: 2px solid #e1e8ed; border-radius: 10px; font-size: 14px; background: rgba(255,255,255,0.8); }
        .schedule-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-top: 15px; }
        .schedule-card { padding: 15px; border-radius: 12px; text-align: center; background: rgba(255,255,255,0.7); border: 1px solid rgba(255,255,255,0.5); }
        .brigade-name { font-weight: bold; font-size: 0.9em; margin-bottom: 8px; }
        .shift { font-weight: bold; padding: 6px 12px; border-radius: 20px; font-size: 0.85em; display: inline-block; min-width: 80px; }
        .shift.день { background: linear-gradient(135deg, #e8f5e8, #c8e6c9); color: #27ae60; }
        .shift.ночь { background: linear-gradient(135deg, #e8eaf6, #c5cae9); color: #5c6bc0; }
        .shift.выходной { background: linear-gradient(135deg, #fff3e0, #ffe0b2); color: #f57c00; }
        .shift.отсыпной { background: linear-gradient(135deg, #e0f2f1, #b2dfdb); color: #00897b; }
        .message { padding: 12px 15px; border-radius: 10px; margin: 10px 0; text-align: center; font-weight: 600; font-size: 0.9em; }
        .message.success { background: linear-gradient(135deg, #d4edda, #c3e6cb); color: #155724; }
        .message.error { background: linear-gradient(135deg, #f8d7da, #f5c6cb); color: #721c24; }
        .close-btn { background: linear-gradient(135deg, #95a5a6, #7f8c8d); color: white; padding: 8px 16px; border: none; border-radius: 8px; cursor: pointer; margin-top: 12px; }
        .theme-selector { display: grid; grid-template-columns: repeat(4, 1fr); gap: 8px; margin: 12px 0; }
        .theme-option { padding: 10px 5px; border: 2px solid rgba(255,255,255,0.3); border-radius: 10px; cursor: pointer; text-align: center; font-size: 0.75em; font-weight: 600; color: white; }
        .theme-option.active { border-color: white; box-shadow: 0 0 0 2px rgba(255,255,255,0.8); }
        .footer { text-align: center; margin-top: 20px; padding-top: 15px; border-top: 1px solid rgba(255,255,255,0.3); color: rgba(255,255,255,0.8); font-size: 0.8em; }
    </style>


    <div class="container">
        <header>
            <h1>&nbsp;Расписание бригад</h1>
            <p class="subtitle">Простой и удобный планировщик</p>
        </header>

        <div class="section">
            <h3>🎨 Выберите тему</h3>
            <div class="theme-selector">
                <div class="theme-option active" onclick="changeTheme('theme-blue')" style="background-image: linear-gradient(135deg, rgb(102, 126, 234), rgb(118, 75, 162)); background-position: initial; background-size: initial; background-repeat: initial; background-attachment: initial; background-origin: initial; background-clip: initial;">Синяя</div>
                <div class="theme-option" onclick="changeTheme('theme-ocean')" style="background-image: linear-gradient(135deg, rgb(79, 172, 254), rgb(0, 242, 254)); background-position: initial; background-size: initial; background-repeat: initial; background-attachment: initial; background-origin: initial; background-clip: initial;">Океан</div>
                <div class="theme-option" onclick="changeTheme('theme-sunset')" style="background-image: linear-gradient(135deg, rgb(250, 112, 154), rgb(254, 225, 64)); background-position: initial; background-size: initial; background-repeat: initial; background-attachment: initial; background-origin: initial; background-clip: initial;">Закат</div>
                <div class="theme-option" onclick="changeTheme('theme-purple')" style="background-image: linear-gradient(135deg, rgb(161, 140, 209), rgb(251, 194, 235)); background-position: initial; background-size: initial; background-repeat: initial; background-attachment: initial; background-origin: initial; background-clip: initial;">Лаванда</div>
                <div class="theme-option" onclick="changeTheme('theme-forest')" style="background-image: linear-gradient(135deg, rgb(17, 153, 142), rgb(56, 239, 125)); background-position: initial; background-size: initial; background-repeat: initial; background-attachment: initial; background-origin: initial; background-clip: initial;">Лес</div>
                <div class="theme-option" onclick="changeTheme('theme-fire')" style="background-image: linear-gradient(135deg, rgb(255, 107, 107), rgb(255, 167, 38)); background-position: initial; background-size: initial; background-repeat: initial; background-attachment: initial; background-origin: initial; background-clip: initial;">Огонь</div>
                <div class="theme-option" onclick="changeTheme('theme-space')" style="background-image: linear-gradient(135deg, rgb(12, 12, 12), rgb(44, 62, 80)); background-position: initial; background-size: initial; background-repeat: initial; background-attachment: initial; background-origin: initial; background-clip: initial;">Космос</div>
                <div class="theme-option" onclick="changeTheme('theme-lavender')" style="background-image: linear-gradient(135deg, rgb(224, 195, 252), rgb(142, 197, 252)); background-position: initial; background-size: initial; background-repeat: initial; background-attachment: initial; background-origin: initial; background-clip: initial; color: rgb(51, 51, 51);">Нежность</div>
            </div>
        </div>

        <div class="controls">
            <button class="btn btn-primary" onclick="toggleSection('todaySchedule')">📅 Сегодня</button>
            <button class="btn btn-secondary" onclick="toggleSection('datePicker')">📆 Выбрать дату</button>
            <button class="btn btn-success" onclick="toggleSection('messageForm')">✉️ Сообщение</button>
            <button class="btn btn-support" onclick="toggleSection('supportPanel')">💝 Поддержка</button>
        </div>

        <div id="todaySchedule" class="section hidden">
            <h3>📅 Расписание на сегодня</h3>
            <div id="todayResult" class="schedule-grid"></div>
            <button class="close-btn" onclick="toggleSection('todaySchedule')">❌ Закрыть</button>
        </div>

        <div id="datePicker" class="section hidden">
            <h3>📆 Выберите дату</h3>
            <input type="date" id="dateInput">
            <button class="btn btn-primary" onclick="showDateSchedule()">Показать расписание</button>
            <div id="dateResult" class="schedule-grid" style="margin-top: 15px;"></div>
            <button class="close-btn" onclick="toggleSection('datePicker')">❌ Закрыть</button>
        </div>

        <div id="messageForm" class="section">
            <h3>✉️ Сообщение администратору</h3>
            <input type="text" id="usernameInput" placeholder="Ваше имя (необязательно)">
            <textarea id="messageText" placeholder="Ваше сообщение..." rows="3"></textarea>
            <button class="btn btn-success" onclick="sendMessage()">📤 Отправить</button><div id="messageStatus"></div>
            <button class="close-btn" onclick="toggleSection('messageForm')">❌ Закрыть</button>
        </div>

        <div id="supportPanel" class="section hidden">
            <h3>💝 Поддержать проект</h3>
            <div class="support-content">
Здорово, что вы решили поддержать проект!

1. Перешли другу ссылку на сайт
2. Сообщи об ошибках, если найдёшь
3. Пользуйся регулярно

Спасибо за использование! ❤️
            </div>
            <button class="close-btn" onclick="toggleSection('supportPanel')">❌ Закрыть</button>
        </div>

        <div class="footer">
            <p>Простое расписание • Красивые темы • v2.0</p>
        </div>
    </div>

    <script>
        const START_DATE = new Date('2025-04-21');
        const SCHEDULES = [
            {"Бригада 1": "Выходной", "Бригада 2": "День", "Бригада 3": "Ночь", "Бригада 4": "Отсыпной"},
            {"Бригада 1": "День", "Бригада 2": "Ночь", "Бригада 3": "Отсыпной", "Бригада 4": "Выходной"},
            {"Бригада 1": "Ночь", "Бригада 2": "Отсыпной", "Бригада 3": "Выходной", "Бригада 4": "День"},
            {"Бригада 1": "Отсыпной", "Бригада 2": "Выходной", "Бригада 3": "День", "Бригада 4": "Ночь"}
        ];

        function changeTheme(themeName) {
            document.body.className = themeName;
            document.querySelectorAll('.theme-option').forEach(option => option.classList.remove('active'));
            event.target.classList.add('active');
            localStorage.setItem('selectedTheme', themeName);
        }

        function toggleSection(sectionId) {
            document.querySelectorAll('.section').forEach(section => {
                if (section.id) section.classList.add('hidden');
            });
            const section = document.getElementById(sectionId);
            if (section) {
                section.classList.remove('hidden');
                if (sectionId === 'todaySchedule') showTodaySchedule();
            }
        }

        function showTodaySchedule() {
            const today = new Date();
            const schedule = getShiftSchedule(today);
            displaySchedule(schedule, 'todayResult');
        }

        function showDateSchedule() {
            const dateInput = document.getElementById('dateInput');
            if (!dateInput.value) return showMessage('Выберите дату', 'error');
            const schedule = getShiftSchedule(new Date(dateInput.value));
            displaySchedule(schedule, 'dateResult');
        }

        function displaySchedule(schedule, containerId) {
            let html = '';
            for (const [brigade, shift] of Object.entries(schedule)) {
                html += `<div class="schedule-card"><div class="brigade-name">${brigade}</div><div class="shift ${shift.toLowerCase()}">${shift}</div></div>`;
            }
            document.getElementById(containerId).innerHTML = html;
        }

        function getShiftSchedule(targetDate) {
            const diffDays = Math.floor((targetDate - START_DATE) / (1000 * 60 * 60 * 24));
            return SCHEDULES[diffDays % 4];
        }

        function sendMessage() {
            const messageText = document.getElementById('messageText').value;
            if (!messageText.trim()) return showMessage('Введите сообщение', 'error');
            showMessage('✅ Сообщение отправлено!', 'success');
            document.getElementById('messageText').value = '';
        }

        function showMessage(text, type) {
            const statusDiv = document.getElementById('messageStatus');
            statusDiv.innerHTML = `<div class="message ${type}">${text}</div>`;
            setTimeout(() => statusDiv.innerHTML = '', 3000);
        }

        window.onload = function() {
            const savedTheme = localStorage.getItem('selectedTheme') || 'theme-blue';
            document.body.className = savedTheme;
            document.getElementById('dateInput').value = new Date().toISOString().split('T')[0];
        };
    </script>

# work-schedule
