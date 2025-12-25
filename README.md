<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Календарь с 32-дневным декабрем</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #1a2980, #26d0ce);
            color: #333;
            min-height: 100vh;
            padding: 20px;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        
        header {
            text-align: center;
            margin-bottom: 30px;
            padding: 20px;
            background-color: rgba(255, 255, 255, 0.9);
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
        }
        
        h1 {
            color: #1a2980;
            font-size: 2.8rem;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
        }
        
        .subtitle {
            color: #26d0ce;
            font-size: 1.4rem;
            font-weight: bold;
        }
        
        .description {
            color: #666;
            font-size: 1.1rem;
            max-width: 800px;
            margin: 20px auto;
            line-height: 1.6;
        }
        
        .calendar-container {
            display: flex;
            flex-wrap: wrap;
            gap: 30px;
            justify-content: center;
            margin-bottom: 40px;
        }
        
        .calendar {
            background-color: rgba(255, 255, 255, 0.95);
            border-radius: 15px;
            padding: 25px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            width: 100%;
            max-width: 900px;
            transition: transform 0.3s;
        }
        
        .calendar:hover {
            transform: translateY(-5px);
        }
        
        .calendar-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 2px solid #26d0ce;
        }
        
        .month-year {
            font-size: 2.2rem;
            color: #1a2980;
            font-weight: bold;
        }
        
        .days-of-week {
            display: grid;
            grid-template-columns: repeat(7, 1fr);
            gap: 10px;
            margin-bottom: 15px;
        }
        
        .day-name {
            text-align: center;
            font-weight: bold;
            color: #26d0ce;
            padding: 10px;
            background-color: rgba(38, 208, 206, 0.1);
            border-radius: 8px;
        }
        
        .days-grid {
            display: grid;
            grid-template-columns: repeat(7, 1fr);
            gap: 10px;
        }
        
        .day {
            aspect-ratio: 1;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2rem;
            font-weight: 500;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.2s;
            border: 2px solid transparent;
        }
        
        .day:hover {
            transform: scale(1.05);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }
        
        .normal-day {
            background-color: #f8f9fa;
            color: #333;
        }
        
        .december-day {
            background-color: #e3f2fd;
            color: #1a2980;
            font-weight: 600;
        }
        
        .extra-day {
            background-color: #1a2980;
            color: white;
            font-weight: bold;
            position: relative;
            animation: pulse 2s infinite;
        }
        
        .extra-day::after {
            content: "✨";
            position: absolute;
            top: 5px;
            right: 5px;
            font-size: 0.8rem;
        }
        
        .today {
            border: 3px solid #26d0ce;
            background-color: #e0f7fa;
            font-weight: bold;
        }
        
        .weekend {
            color: #d32f2f;
        }
        
        .other-month {
            background-color: #f5f5f5;
            color: #aaa;
        }
        
        .legend {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 20px;
            margin-top: 30px;
            padding: 20px;
            background-color: rgba(255, 255, 255, 0.9);
            border-radius: 15px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }
        
        .legend-item {
            display: flex;
            align-items: center;
            gap: 10px;
            font-weight: 500;
        }
        
        .legend-color {
            width: 20px;
            height: 20px;
            border-radius: 5px;
        }
        
        .notes {
            background-color: rgba(255, 255, 255, 0.95);
            border-radius: 15px;
            padding: 25px;
            margin-top: 30px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
        }
        
        .notes h3 {
            color: #1a2980;
            margin-bottom: 15px;
            font-size: 1.8rem;
        }
        
        .notes ul {
            padding-left: 20px;
            line-height: 1.6;
        }
        
        .notes li {
            margin-bottom: 10px;
            font-size: 1.1rem;
        }
        
        .notes .highlight {
            color: #1a2980;
            font-weight: bold;
        }
        
        footer {
            text-align: center;
            margin-top: 40px;
            padding: 20px;
            color: white;
            font-size: 1rem;
        }
        
        @keyframes pulse {
            0% { box-shadow: 0 0 0 0 rgba(26, 41, 128, 0.7); }
            70% { box-shadow: 0 0 0 10px rgba(26, 41, 128, 0); }
            100% { box-shadow: 0 0 0 0 rgba(26, 41, 128, 0); }
        }
        
        @media (max-width: 768px) {
            .days-grid, .days-of-week {
                gap: 5px;
            }
            
            .day {
                font-size: 0.9rem;
            }
            
            .month-year {
                font-size: 1.8rem;
            }
            
            h1 {
                font-size: 2.2rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>Календарь с 32-дневным декабрем</h1>
            <div class="subtitle">Новый взгляд на завершение года</div>
            <div class="description">
                Этот календарь предлагает альтернативную версию декабря с дополнительными днями, 
                что позволяет более плавно завершить год и подготовиться к новому. 
                Дни 31 и 32 декабря выделены специально для подведения итогов и планирования будущего.
            </div>
        </header>
        
        <div class="calendar-container">
            <div class="calendar">
                <div class="calendar-header">
                    <div class="month-year">Декабрь 2023</div>
                    <div class="calendar-info">32 дня • 5 недель</div>
                </div>
                
                <div class="days-of-week">
                    <div class="day-name">Пн</div>
                    <div class="day-name">Вт</div>
                    <div class="day-name">Ср</div>
                    <div class="day-name">Чт</div>
                    <div class="day-name">Пт</div>
                    <div class="day-name weekend">Сб</div>
                    <div class="day-name weekend">Вс</div>
                </div>
                
                <div class="days-grid" id="december-days">
                    <!-- Ноябрьские дни будут заполнены JavaScript -->
                </div>
            </div>
        </div>
        
        <div class="legend">
            <div class="legend-item">
                <div class="legend-color" style="background-color: #f8f9fa;"></div>
                <span>Обычные дни</span>
            </div>
            <div class="legend-item">
                <div class="legend-color" style="background-color: #e3f2fd;"></div>
                <span>Декабрь</span>
            </div>
            <div class="legend-item">
                <div class="legend-color" style="background-color: #1a2980;"></div>
                <span>Дополнительные дни (31, 32)</span>
            </div>
            <div class="legend-item">
                <div class="legend-color" style="background-color: #e0f7fa; border: 2px solid #26d0ce;"></div>
                <span>Сегодня</span>
            </div>
        </div>
        
        <div class="notes">
            <h3>Особенности 32-дневного декабря:</h3>
            <ul>
                <li><span class="highlight">31 декабря</span> - День рефлексии и благодарности. Время подвести итоги года, поблагодарить близких и отпустить неудачи.</li>
                <li><span class="highlight">32 декабря</span> - День мечтаний и планирования. Посвятите этот день размышлениям о будущем, постановке целей и визуализации желаний.</li>
                <li>Дополнительные дни позволяют плавно перейти из старого года в новый без спешки и стресса.</li>
                <li>Такой календарь лучше соответствует естественным биоритмам человека в период зимнего солнцестояния.</li>
                <li>32-дневный декабрь дает больше времени для завершения дел, праздничных приготовлений и общения с близкими.</li>
            </ul>
        </div>
        
        <footer>
            <p>© 2023 Альтернативный календарь | Декабрь с 32 днями</p>
            <p>Этот календарь создан в творческих целях и представляет альтернативную временную систему</p>
        </footer>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const decemberDaysGrid = document.getElementById('december-days');
            
            // Получаем текущую дату
            const today = new Date();
            const currentDay = today.getDate();
            const currentMonth = today.getMonth(); // 0-январь, 11-декабрь
            
            // Определяем день недели для 1 декабря 2023 (пятница)
            // Но для нашего календаря предположим, что 1 декабря 2023 - понедельник для красивого отображения
            let firstDayOfWeek = 1; // 1 = понедельник
            
            // Создаем дни ноября (пустые клетки перед 1 декабря)
            // 1 декабря 2023 года приходится на пятницу, значит нужно 4 пустых дня до него
            // Но мы сделаем так, чтобы 1 декабря было понедельником для красивого отображения
            for (let i = 0; i < firstDayOfWeek - 1; i++) {
                const emptyDay = document.createElement('div');
                emptyDay.className = 'day other-month';
                emptyDay.textContent = '';
                decemberDaysGrid.appendChild(emptyDay);
            }
            
            // Создаем 32 дня декабря
            const totalDecemberDays = 32;
            
            for (let day = 1; day <= totalDecemberDays; day++) {
                const dayElement = document.createElement('div');
                dayElement.className = 'day december-day';
                dayElement.textContent = day;
                
                // Определяем день недели (0-воскресенье, 1-понедельник...)
                const dayOfWeek = (firstDayOfWeek - 1 + day - 1) % 7;
                
                // Добавляем класс для выходных
                if (dayOfWeek === 5 || dayOfWeek === 6) {
                    dayElement.classList.add('weekend');
                }
                
                // Особые стили для дополнительных дней
                if (day === 31 || day === 32) {
                    dayElement.classList.remove('december-day');
                    dayElement.classList.add('extra-day');
                }
                
                // Если сегодняшний день и мы в декабре
                if (currentMonth === 11 && day === currentDay) {
                    dayElement.classList.add('today');
                    dayElement.title = "Сегодня!";
                }
                
                // Добавляем всплывающие подсказки для особых дней
                if (day === 31) {
                    dayElement.title = "День рефлексии и благодарности";
                } else if (day === 32) {
                    dayElement.title = "День мечтаний и планирования";
                } else if (day === 24 || day === 25) {
                    dayElement.title = "Праздничные дни";
                }
                
                decemberDaysGrid.appendChild(dayElement);
            }
            
            // Добавляем оставшиеся пустые дни (чтобы сетка была полной)
            const totalCells = Math.ceil((firstDayOfWeek - 1 + totalDecemberDays) / 7) * 7;
            const remainingCells = totalCells - (firstDayOfWeek - 1 + totalDecemberDays);
            
            for (let i = 0; i < remainingCells; i++) {
                const emptyDay = document.createElement('div');
                emptyDay.className = 'day other-month';
                emptyDay.textContent = '';
                decemberDaysGrid.appendChild(emptyDay);
            }
            
            // Добавляем обработчик кликов на дни
            document.querySelectorAll('.day').forEach(day => {
                day.addEventListener('click', function() {
                    const dayNum = this.textContent;
                    if (dayNum) {
                        let message = `Вы выбрали ${dayNum} декабря`;
                        
                        if (dayNum == 31) {
                            message += " - День рефлексии и благодарности!";
                        } else if (dayNum == 32) {
                            message += " - День мечтаний и планирования!";
                        } else if (dayNum == 24 || dayNum == 25) {
                            message += " - Праздничный день!";
                        }
                        
                        alert(message);
                    }
                });
            });
        });
    </script>
</body>
</html>
