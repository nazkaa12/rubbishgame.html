<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>🌊 Ақтау Эко-Герой | Сортируй мусор — спасай Каспий!</title>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: linear-gradient(135deg, #87CEEB 0%, #1E90FF 50%, #006994 100%);
      min-height: 100vh;
      overflow-x: hidden;
      color: #333;
    }
    
    /* Анимация волн */
    .waves {
      position: fixed;
      bottom: 0;
      width: 100%;
      height: 100px;
      background: url('image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1200 120"><path d="M0,0 L1200,0 L1200,120 L0,120 Z" fill="%23006994"/><path d="M0,60 C300,120 900,0 1200,60 L1200,120 L0,120 Z" fill="%230088cc" opacity="0.6"/></svg>') repeat-x;
      animation: wave 8s linear infinite;
      z-index: 1;
    }
    @keyframes wave {
      0% { background-position-x: 0; }
      100% { background-position-x: 1200px; }
    }

    .container {
      max-width: 1200px;
      margin: 0 auto;
      padding: 20px;
      position: relative;
      z-index: 2;
    }

    header {
      text-align: center;
      padding: 20px;
      background: rgba(255,255,255,0.9);
      border-radius: 20px;
      margin-bottom: 20px;
      box-shadow: 0 8px 32px rgba(0,0,0,0.1);
      animation: fadeInDown 0.6s ease;
    }
    
    @keyframes fadeInDown {
      from { opacity: 0; transform: translateY(-30px); }
      to { opacity: 1; transform: translateY(0); }
    }

    h1 {
      color: #006994;
      font-size: 2.2rem;
      margin-bottom: 10px;
      text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
    }
    
    .subtitle {
      color: #555;
      font-size: 1.1rem;
      margin-bottom: 15px;
    }

    .score-board {
      display: flex;
      justify-content: center;
      gap: 30px;
      flex-wrap: wrap;
      margin: 15px 0;
    }
    
    .score-item {
      background: linear-gradient(135deg, #4CAF50, #45a049);
      color: white;
      padding: 10px 25px;
      border-radius: 50px;
      font-weight: bold;
      box-shadow: 0 4px 15px rgba(0,0,0,0.2);
      animation: pulse 2s infinite;
    }
    
    @keyframes pulse {
      0%, 100% { transform: scale(1); }
      50% { transform: scale(1.05); }
    }

    .game-area {
      display: grid;
      grid-template-columns: 1fr;
      gap: 20px;
      margin: 20px 0;
    }

    .trash-zone {
      background: rgba(255,255,255,0.95);
      border-radius: 20px;
      padding: 20px;
      min-height: 180px;
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 15px;
      box-shadow: 0 8px 32px rgba(0,0,0,0.15);
      position: relative;
      overflow: hidden;
    }
    
    .trash-zone::before {
      content: "🗑️ Мусор на пляже Актау";
      position: absolute;
      top: 10px;
      left: 20px;
      font-weight: bold;
      color: #666;
      font-size: 0.9rem;
    }

    .trash-item {
      width: 70px;
      height: 70px;
      background: white;
      border-radius: 15px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 2rem;
      cursor: grab;
      box-shadow: 0 4px 12px rgba(0,0,0,0.15);
      transition: all 0.2s ease;
      user-select: none;
      animation: bounce 0.5s ease;
      position: relative;
      z-index: 10;
    }
    
    @keyframes bounce {
      0%, 100% { transform: translateY(0); }
      50% { transform: translateY(-10px); }
    }
    
    .trash-item:hover {
      transform: scale(1.1) rotate(5deg);
      box-shadow: 0 8px 25px rgba(0,0,0,0.25);
      z-index: 20;
    }
    
    .trash-item.dragging {
      opacity: 0.8;
      transform: scale(1.2);
      cursor: grabbing;
    }

    .bins-container {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
      gap: 15px;
      margin: 20px 0;
    }

    .bin {
      background: white;
      border-radius: 20px;
      padding: 15px 10px;
      text-align: center;
      box-shadow: 0 8px 32px rgba(0,0,0,0.15);
      transition: all 0.3s ease;
      cursor: pointer;
      border: 4px solid transparent;
      position: relative;
      overflow: hidden;
    }
    
    .bin:hover {
      transform: translateY(-5px);
      box-shadow: 0 12px 40px rgba(0,0,0,0.25);
    }
    
    .bin.correct {
      border-color: #4CAF50;
      animation: success 0.4s ease;
    }
    
    .bin.wrong {
      border-color: #f44336;
      animation: shake 0.4s ease;
    }
    
    @keyframes success {
      0%, 100% { transform: scale(1); }
      50% { transform: scale(1.05); }
    }
    
    @keyframes shake {
      0%, 100% { transform: translateX(0); }
      25% { transform: translateX(-8px); }
      75% { transform: translateX(8px); }
    }

    .bin.plastic { background: linear-gradient(135deg, #FF6B6B, #EE5A5A); }
    .bin.paper { background: linear-gradient(135deg, #4ECDC4, #44BDAD); }
    .bin.glass { background: linear-gradient(135deg, #95E1D3, #7FD3C3); }
    .bin.metal { background: linear-gradient(135deg, #A8E6CF, #95DDB5); }

    .bin-icon {
      font-size: 2.5rem;
      margin-bottom: 8px;
      display: block;
    }
    
    .bin-label {
      font-weight: bold;
      color: white;
      text-shadow: 1px 1px 2px rgba(0,0,0,0.3);
      font-size: 0.95rem;
      display: block;
    }
    
    .bin-hint {
      font-size: 0.75rem;
      color: rgba(255,255,255,0.9);
      margin-top: 5px;
      display: block;
    }

    .fact-box {
      background: linear-gradient(135deg, #FFF9C4, #FFECB3);
      border-left: 5px solid #FFC107;
      padding: 15px 20px;
      border-radius: 0 15px 15px 0;
      margin: 20px 0;
      animation: slideInLeft 0.5s ease;
      display: none;
    }
    
    @keyframes slideInLeft {
      from { opacity: 0; transform: translateX(-30px); }
      to { opacity: 1; transform: translateX(0); }
    }
    
    .fact-box.show { display: block; }
    
    .fact-title {
      font-weight: bold;
      color: #5D4037;
      margin-bottom: 5px;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .controls {
      text-align: center;
      margin: 25px 0;
    }
    
    .btn {
      background: linear-gradient(135deg, #2196F3, #1976D2);
      color: white;
      border: none;
      padding: 15px 40px;
      font-size: 1.1rem;
      border-radius: 50px;
      cursor: pointer;
      box-shadow: 0 6px 20px rgba(33, 150, 243, 0.4);
      transition: all 0.3s ease;
      font-weight: bold;
      margin: 5px;
    }
    
    .btn:hover {
      transform: translateY(-3px);
      box-shadow: 0 10px 30px rgba(33, 150, 243, 0.6);
    }
    
    .btn:active {
      transform: translateY(1px);
    }
    
    .btn.restart {
      background: linear-gradient(135deg, #FF9800, #F57C00);
    }

    .message {
      text-align: center;
      padding: 20px;
      background: rgba(255,255,255,0.95);
      border-radius: 20px;
      margin: 15px 0;
      font-weight: bold;
      min-height: 60px;
      display: flex;
      align-items: center;
      justify-content: center;
      box-shadow: 0 8px 32px rgba(0,0,0,0.1);
    }
    
    .message.success { color: #2E7D32; background: linear-gradient(135deg, #E8F5E9, #C8E6C9); }
    .message.error { color: #C62828; background: linear-gradient(135deg, #FFEBEE, #FFCDD2); }

    .footer {
      text-align: center;
      padding: 20px;
      color: white;
      font-size: 0.9rem;
      text-shadow: 1px 1px 2px rgba(0,0,0,0.3);
      margin-top: 20px;
    }
    
    .footer a {
      color: #FFD54F;
      text-decoration: none;
      font-weight: bold;
    }

    /* Анимация падающего мусора */
    @keyframes fall {
      from { transform: translateY(-100px) rotate(0deg); opacity: 0; }
      to { transform: translateY(0) rotate(360deg); opacity: 1; }
    }
    
    .trash-item.new {
      animation: fall 0.6s ease forwards;
    }

    /* Адаптивность */
    @media (max-width: 768px) {
      h1 { font-size: 1.8rem; }
      .subtitle { font-size: 1rem; }
      .trash-item { width: 60px; height: 60px; font-size: 1.8rem; }
      .bin-icon { font-size: 2rem; }
      .bin-label { font-size: 0.85rem; }
      .score-board { gap: 15px; }
      .score-item { padding: 8px 20px; font-size: 0.9rem; }
    }
    
    @media (max-width: 480px) {
      .container { padding: 10px; }
      header { padding: 15px; border-radius: 15px; }
      h1 { font-size: 1.5rem; }
      .trash-zone { min-height: 150px; padding: 15px; }
      .trash-item { width: 55px; height: 55px; font-size: 1.6rem; }
      .bins-container { grid-template-columns: repeat(2, 1fr); }
      .btn { padding: 12px 30px; font-size: 1rem; }
    }
  </style>
</head>
<body>
  <div class="waves"></div>
  
  <div class="container">
    <header>
      <h1>🌊 Ақтау Эко-Герой</h1>
      <p class="subtitle">Сортируй мусор — спасай Каспийское море и природу Мангистау! ♻️</p>
      
      <div class="score-board">
        <div class="score-item">⭐ Очки: <span id="score">0</span></div>
        <div class="score-item">🎯 Уровень: <span id="level">1</span></div>
        <div class="score-item">✅ Правильно: <span id="correct">0</span></div>
      </div>
    </header>

    <div class="message" id="message">👋 Перетащи мусор в правильный контейнер!</div>

    <div class="game-area">
      <!-- Зона с мусором -->
      <div class="trash-zone" id="trashZone">
        <!-- Мусор генерируется JS -->
      </div>

      <!-- Контейнеры для сортировки -->
      <div class="bins-container">
        <div class="bin plastic" data-type="plastic" draggable="true">
          <span class="bin-icon">🥤</span>
          <span class="bin-label">ПЛАСТИК</span>
          <span class="bin-hint">бутылки, пакеты</span>
        </div>
        <div class="bin paper" data-type="paper" draggable="true">
          <span class="bin-icon">📰</span>
          <span class="bin-label">БУМАГА</span>
          <span class="bin-hint">газеты, картон</span>
        </div>
        <div class="bin glass" data-type="glass" draggable="true">
          <span class="bin-icon">🫙</span>
          <span class="bin-label">СТЕКЛО</span>
          <span class="bin-hint">банки, бутылки</span>
        </div>
        <div class="bin metal" data-type="metal" draggable="true">
          <span class="bin-icon">🥫</span>
          <span class="bin-label">МЕТАЛЛ</span>
          <span class="bin-hint">консервы, фольга</span>
        </div>
      </div>
    </div>

    <!-- Образовательный факт -->
    <div class="fact-box" id="factBox">
      <div class="fact-title">💡 Знаешь ли ты?</div>
      <div id="factText"></div>
    </div>

    <div class="controls">
      <button class="btn" id="nextBtn" style="display:none">Следующий раунд ➡️</button>
      <button class="btn restart" id="restartBtn">🔄 Новая игра</button>
    </div>

    <div class="footer">
      <p>🌍 Создано для детей Актау и Мангистауской области</p>
      <p>Каждый правильный выбор помогает очистить побережье Каспия! 🐬</p>
      <p style="margin-top:10px"><small>Игра основана на принципах раздельного сбора отходов [[1]][[22]]</small></p>
    </div>
  </div>

  <script>
    // === ДАННЫЕ ИГРЫ ===
    const trashItems = [
      { id: 'bottle_plastic', emoji: '🥤', type: 'plastic', name: 'Пластиковая бутылка' },
      { id: 'bag_plastic', emoji: '🛍️', type: 'plastic', name: 'Полиэтиленовый пакет' },
      { id: 'cup_plastic', emoji: '☕', type: 'plastic', name: 'Пластиковый стаканчик' },
      { id: 'newspaper', emoji: '📰', type: 'paper', name: 'Газета' },
      { id: 'box', emoji: '📦', type: 'paper', name: 'Картонная коробка' },
      { id: 'notebook', emoji: '📓', type: 'paper', name: 'Тетрадь' },
      { id: 'jar_glass', emoji: '🫙', type: 'glass', name: 'Стеклянная банка' },
      { id: 'bottle_glass', emoji: '🍾', type: 'glass', name: 'Стеклянная бутылка' },
      { id: 'cup_glass', emoji: '🥛', type: 'glass', name: 'Стеклянный стакан' },
      { id: 'can_metal', emoji: '🥫', type: 'metal', name: 'Консервная банка' },
      { id: 'foil', emoji: '🍫', type: 'metal', name: 'Фольга' },
      { id: 'cap_metal', emoji: '🧢', type: 'metal', name: 'Крышка от бутылки' }
    ];

    const ecoFacts = [
      "🌊 Каспийское море — крупнейший замкнутый водоём на Земле. Его экосистема очень хрупкая!",
      "♻️ В Мангистау ежегодно образуется более 70 тыс. тонн отходов. Сортировка помогает уменьшить свалки [[17]].",
      "🐬 Тюлени и осётры Каспия страдают от пластикового мусора. Каждый сортированный предмет спасает жизнь!",
      "🌱 Переработка 1 тонны бумаги сохраняет 17 деревьев и экономит 20 000 литров воды.",
      "🔋 Батарейки и электронику нельзя выбрасывать с обычным мусором — они отравляют почву и воду.",
      "🏖️ Пляжи Актау становятся чище, когда жители сортируют отходы. Твой вклад важен!",
      "💧 Загрязнение воды в Каспии влияет на рыболовство — основу экономики региона [[13]].",
      "🌬️ Правильная утилизация мусора снижает вредные выбросы и улучшает воздух в Актау [[16]]."
    ];

    // === СОСТОЯНИЕ ИГРЫ ===
    let score = 0, level = 1, correctCount = 0;
    let currentItem = null;
    let gameActive = true;

    // === DOM ЭЛЕМЕНТЫ ===
    const trashZone = document.getElementById('trashZone');
    const bins = document.querySelectorAll('.bin');
    const scoreEl = document.getElementById('score');
    const levelEl = document.getElementById('level');
    const correctEl = document.getElementById('correct');
    const messageEl = document.getElementById('message');
    const factBox = document.getElementById('factBox');
    const factText = document.getElementById('factText');
    const nextBtn = document.getElementById('nextBtn');
    const restartBtn = document.getElementById('restartBtn');

    // === ИНИЦИАЛИЗАЦИЯ ===
    function initGame() {
      score = 0; level = 1; correctCount = 0;
      updateScore();
      showMessage('👋 Перетащи мусор в правильный контейнер!', '');
      factBox.classList.remove('show');
      nextBtn.style.display = 'none';
      generateTrash(3 + level); // больше предметов на уровне
      gameActive = true;
    }

    function updateScore() {
      scoreEl.textContent = score;
      levelEl.textContent = level;
      correctEl.textContent = correctCount;
    }

    function showMessage(text, type = '') {
      messageEl.textContent = text;
      messageEl.className = 'message' + (type ? ' ' + type : '');
    }

    function showFact() {
      const fact = ecoFacts[Math.floor(Math.random() * ecoFacts.length)];
      factText.textContent = fact;
      factBox.classList.add('show');
    }

    // === ГЕНЕРАЦИЯ МУСОРА ===
    function generateTrash(count) {
      trashZone.innerHTML = '';
      const shuffled = [...trashItems].sort(() => 0.5 - Math.random());
      
      for (let i = 0; i < Math.min(count, shuffled.length); i++) {
        const item = shuffled[i];
        const el = document.createElement('div');
        el.className = 'trash-item new';
        el.draggable = true;
        el.dataset.type = item.type;
        el.dataset.id = item.id;
        el.innerHTML = item.emoji;
        el.title = item.name;
        
        // События для drag-and-drop
        el.addEventListener('dragstart', dragStart);
        el.addEventListener('touchstart', touchStart, {passive: true});
        
        // Клик для мобильных
        el.addEventListener('click', () => selectItem(el));
        
        trashZone.appendChild(el);
      }
    }

    // === DRAG & DROP ЛОГИКА ===
    function dragStart(e) {
      if (!gameActive) { e.preventDefault(); return; }
      currentItem = this;
      this.classList.add('dragging');
      e.dataTransfer.setData('text/plain', this.dataset.type);
      setTimeout(() => this.style.opacity = '0.5', 0);
    }

    function touchStart(e) {
      if (!gameActive) return;
      currentItem = this;
      this.classList.add('dragging');
      // Простая имитация drag для тач-устройств
      document.addEventListener('touchmove', touchMove, {passive: false});
      document.addEventListener('touchend', touchEnd);
    }

    function touchMove(e) {
      e.preventDefault();
      const touch = e.touches[0];
      const elem = document.elementFromPoint(touch.clientX, touch.clientY);
      if (elem && elem.classList.contains('bin')) {
        highlightBin(elem, true);
      } else {
        bins.forEach(bin => highlightBin(bin, false));
      }
    }

    function touchEnd(e) {
      document.removeEventListener('touchmove', touchMove);
      document.removeEventListener('touchend', touchEnd);
      const touch = e.changedTouches[0];
      const elem = document.elementFromPoint(touch.clientX, touch.clientY);
      
      if (elem && elem.classList.contains('bin') && currentItem) {
        checkDrop(elem);
      }
      if (currentItem) {
        currentItem.classList.remove('dragging');
        currentItem = null;
      }
      bins.forEach(bin => highlightBin(bin, false));
    }

    function highlightBin(bin, highlight) {
      bin.style.transform = highlight ? 'scale(1.05) translateY(-8px)' : '';
      bin.style.boxShadow = highlight ? '0 15px 50px rgba(0,0,0,0.4)' : '';
    }

    // === ПРОВЕРКА СОРТИРОВКИ ===
    function checkDrop(bin) {
      if (!currentItem || !gameActive) return;
      
      const itemType = currentItem.dataset.type;
      const binType = bin.dataset.type;
      const isCorrect = itemType === binType;
      
      // Анимация контейнера
      bin.classList.add(isCorrect ? 'correct' : 'wrong');
      setTimeout(() => bin.classList.remove('correct', 'wrong'), 400);
      
      if (isCorrect) {
        // Правильно!
        score += 10 * level;
        correctCount++;
        showMessage(`✅ Верно! ${currentItem.title} — это ${bin.querySelector('.bin-label').textContent}`, 'success');
        currentItem.style.animation = 'success 0.3s ease forwards';
        setTimeout(() => currentItem.remove(), 300);
        
        // Уровень растёт
        if (correctCount % 5 === 0) {
          level++;
          showMessage(`🎉 Уровень ${level}! Мусора больше, очков больше!`, 'success');
          showFact();
        }
      } else {
        // Ошибка
        showMessage(`❌ Ой! ${currentItem.title} не относится к "${bin.querySelector('.bin-label').textContent}"`, 'error');
        currentItem.style.animation = 'shake 0.4s ease';
        setTimeout(() => currentItem.classList.remove('dragging'), 400);
      }
      
      updateScore();
      currentItem = null;
      
      // Проверка конца раунда
      if (trashZone.children.length === 0) {
        endRound();
      }
    }

    // === КЛИК-ВЫБОР (для мобильных) ===
    function selectItem(el) {
      if (!gameActive) return;
      // Снимаем выделение с других
      document.querySelectorAll('.trash-item').forEach(i => i.style.boxShadow = '');
      // Выделяем текущий
      el.style.boxShadow = '0 0 0 4px #2196F3, 0 8px 25px rgba(33,150,243,0.5)';
      currentItem = el;
      
      // Добавляем обработчики кликов на контейнеры
      bins.forEach(bin => {
        bin.onclick = () => {
          checkDrop(bin);
          bins.forEach(b => b.onclick = null); // убираем обработчики
        };
      });
    }

    // === НАСТРОЙКА DROP ZONE ДЛЯ БИНОВ ===
    bins.forEach(bin => {
      bin.addEventListener('dragover', e => {
        e.preventDefault();
        highlightBin(bin, true);
      });
      
      bin.addEventListener('dragleave', () => {
        highlightBin(bin, false);
      });
      
      bin.addEventListener('drop', e => {
        e.preventDefault();
        highlightBin(bin, false);
        if (currentItem) checkDrop(bin);
      });
    });

    // === КОНЕЦ РАУНДА ===
    function endRound() {
      gameActive = false;
      showMessage(`🏆 Раунд завершён! Очки: ${score}`, 'success');
      showFact();
      nextBtn.style.display = 'inline-block';
      
      // Автоматический переход через 5 сек
      se Timeout(() => {
        if (!gameActive) {
          level++;
          generateTrash(3 + level);
          gameActive = true;
          nextBtn.style.display = 'none';
          showMessage('👋 Новый раунд! Сортируй быстрее!', '');
          factBox.classList.remove('show');
        }
      }, 5000);
    }

    // === ОБРАБОТЧИКИ КНОПОК ===
    nextBtn.addEventListener('click', () => {
      level++;
      generateTrash(3 + level);
      gameActive = true;
      nextBtn.style.display = 'none';
      showMessage('👋 Новый раунд! Сортируй быстрее!', '');
      factBox.classList.remove('show');
    });

    restartBtn.addEventListener('click', () => {
      if (confirm('Начать новую игру? Текущий прогресс будет сброшен.')) {
        level = 1;
        initGame();
      }
    });

    // Запрет перетаскивания текста
    document.addEventListener('dragstart', e => {
      if (e.target.tagName === 'IMG' || e.target.classList.contains('trash-item')) {
        e.dataTransfer.effectAllowed = 'move';
      } else if (!e.target.closest('.trash-item')) {
        e.preventDefault();
      }
    });

    // === ЗАПУСК ===
    window.addEventListener('DOMContentLoaded', initGame);
    
    // Поддержка клавиатуры для доступности
    document.addEventListener('keydown', e => {
      if (e.key === 'Escape' && currentItem) {
        currentItem.classList.remove('dragging');
        currentItem = null;
        bins.forEach(bin => highlightBin(bin, false));
      }
    });
</script>
</body>
</html>
