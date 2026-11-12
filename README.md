<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>🚗 Мой Гараж</title>
<style>
  :root {
    --bg: #0f1115;
    --card: #181b22;
    --card-hover: #1f232c;
    --border: #2a2f3a;
    --text: #e8eaed;
    --text-dim: #9aa0aa;
    --accent: #4f8cff;
    --accent-2: #7c5cff;
    --green: #2ecc71;
    --yellow: #f1c40f;
    --red: #e74c3c;
    --orange: #e67e22;
  }
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body {
    font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
    background: radial-gradient(1200px 600px at 10% -10%, #1a1f2e 0%, var(--bg) 50%);
    color: var(--text);
    min-height: 100vh;
    padding: 24px;
  }
  .container { max-width: 1200px; margin: 0 auto; }

  /* Header */
  header {
    display: flex; justify-content: space-between; align-items: center;
    margin-bottom: 24px; flex-wrap: wrap; gap: 16px;
  }
  h1 {
    font-size: 28px; font-weight: 700;
    background: linear-gradient(90deg, var(--accent), var(--accent-2));
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
  }
  .subtitle { color: var(--text-dim); font-size: 14px; margin-top: 4px; }

  /* Stats */
  .stats { display: grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr)); gap: 14px; margin-bottom: 24px; }
  .stat-card {
    background: var(--card); border: 1px solid var(--border);
    border-radius: 16px; padding: 18px;
    display: flex; flex-direction: column; gap: 6px;
    transition: transform .2s, border-color .2s;
  }
  .stat-card:hover { transform: translateY(-2px); border-color: var(--accent); }
  .stat-label { font-size: 13px; color: var(--text-dim); text-transform: uppercase; letter-spacing: .5px; }
  .stat-value { font-size: 26px; font-weight: 700; }
  .stat-value.green { color: var(--green); }
  .stat-value.red { color: var(--red); }
  .stat-value.yellow { color: var(--yellow); }

  /* Toolbar */
  .toolbar {
    display: flex; gap: 12px; margin-bottom: 20px; flex-wrap: wrap;
  }
  .search {
    flex: 1; min-width: 200px;
    background: var(--card); border: 1px solid var(--border);
    border-radius: 12px; padding: 12px 16px; color: var(--text);
    font-size: 15px; outline: none; transition: border-color .2s;
  }
  .search:focus { border-color: var(--accent); }
  .filter {
    background: var(--card); border: 1px solid var(--border);
    border-radius: 12px; padding: 12px 16px; color: var(--text);
    font-size: 15px; outline: none; cursor: pointer;
  }
  .btn {
    background: linear-gradient(90deg, var(--accent), var(--accent-2));
    color: white; border: none; border-radius: 12px;
    padding: 12px 22px; font-size: 15px; font-weight: 600;
    cursor: pointer; transition: opacity .2s, transform .1s;
    white-space: nowrap;
  }
  .btn:hover { opacity: .9; }
  .btn:active { transform: scale(.97); }
  .btn-ghost {
    background: transparent; border: 1px solid var(--border); color: var(--text);
  }

  /* Cards */
  .grid {
    display: grid; grid-template-columns: repeat(auto-fill, minmax(320px, 1fr)); gap: 16px;
  }
  .item {
    background: var(--card); border: 1px solid var(--border);
    border-radius: 16px; padding: 18px;
    transition: transform .2s, border-color .2s, background .2s;
    position: relative;
  }
  .item:hover { transform: translateY(-3px); background: var(--card-hover); border-color: var(--accent); }
  .item-header { display: flex; justify-content: space-between; align-items: flex-start; gap: 10px; margin-bottom: 10px; }
  .item-title { font-size: 17px; font-weight: 600; line-height: 1.3; }
  .item-actions { display: flex; gap: 6px; }
  .icon-btn {
    background: transparent; border: 1px solid var(--border); color: var(--text-dim);
    width: 30px; height: 30px; border-radius: 8px; cursor: pointer;
    font-size: 14px; transition: all .2s;
  }
  .icon-btn:hover { color: var(--text); border-color: var(--accent); }
  .icon-btn.danger:hover { color: var(--red); border-color: var(--red); }

  .badges { display: flex; flex-wrap: wrap; gap: 6px; margin: 10px 0; }
  .badge {
    font-size: 11px; padding: 4px 10px; border-radius: 20px;
    font-weight: 600; letter-spacing: .3px;
  }
  .badge.planned { background: rgba(79,140,255,.15); color: #7aa7ff; }
  .badge.inprogress { background: rgba(241,196,15,.15); color: var(--yellow); }
  .badge.done { background: rgba(46,204,113,.15); color: var(--green); }
  .badge.optional { background: rgba(154,160,170,.15); color: var(--text-dim); }
  .badge.required { background: rgba(230,126,34,.15); color: var(--orange); }
  .badge.paid { background: rgba(46,204,113,.15); color: var(--green); }
  .badge.unpaid { background: rgba(231,76,60,.15); color: var(--red); }
  .badge.delivered { background: rgba(46,204,113,.15); color: var(--green); }
  .badge.ordered { background: rgba(79,140,255,.15); color: #7aa7ff); }

  .item-meta { font-size: 13px; color: var(--text-dim); display: flex; flex-direction: column; gap: 4px; margin-top: 10px; }
  .item-meta strong { color: var(--text); font-weight: 500; }
  .item-comment {
    margin-top: 10px; font-size: 13px; color: var(--text-dim);
    padding: 8px 12px; background: rgba(255,255,255,.02); border-radius: 10px;
    border-left: 2px solid var(--accent);
  }
  .item-link {
    display: inline-block; margin-top: 10px; font-size: 13px;
    color: var(--accent); text-decoration: none;
  }
  .item-link:hover { text-decoration: underline; }

  /* Empty state */
  .empty {
    text-align: center; padding: 60px 20px; color: var(--text-dim);
  }
  .empty-icon { font-size: 64px; margin-bottom: 16px; }

  /* Modal */
  .modal-overlay {
    position: fixed; inset: 0; background: rgba(0,0,0,.7);
    backdrop-filter: blur(4px); display: none; align-items: center; justify-content: center;
    padding: 20px; z-index: 100;
  }
  .modal-overlay.active { display: flex; }
  .modal {
    background: var(--card); border: 1px solid var(--border);
    border-radius: 20px; padding: 28px; width: 100%; max-width: 560px;
    max-height: 90vh; overflow-y: auto;
    animation: slideUp .3s ease;
  }
  @keyframes slideUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
  .modal h2 { margin-bottom: 20px; font-size: 22px; }
  .form-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 14px; }
  .form-field { display: flex; flex-direction: column; gap: 6px; }
  .form-field.full { grid-column: 1 / -1; }
  label { font-size: 13px; color: var(--text-dim); font-weight: 500; }
  input, select, textarea {
    background: var(--bg); border: 1px solid var(--border);
    border-radius: 10px; padding: 10px 14px; color: var(--text);
    font-size: 14px; outline: none; font-family: inherit;
    transition: border-color .2s;
  }
  input:focus, select:focus, textarea:focus { border-color: var(--accent); }
  textarea { resize: vertical; min-height: 70px; }
  .modal-footer { display: flex; gap: 10px; justify-content: flex-end; margin-top: 24px; }

  @media (max-width: 600px) {
    body { padding: 16px; }
    .form-grid { grid-template-columns: 1fr; }
    h1 { font-size: 22px; }
  }
</style>
</head>
<body>
<div class="container">
  <header>
    <div>
      <h1>🚗 Мой Гараж</h1>
      <div class="subtitle">Отслеживание работ и планов по машине</div>
    </div>
    <button class="btn" onclick="openModal()">+ Добавить запись</button>
  </header>

  <div class="stats">
    <div class="stat-card">
      <div class="stat-label">Всего записей</div>
      <div class="stat-value" id="statTotal">0</div>
    </div>
    <div class="stat-card">
      <div class="stat-label">✅ Сделано</div>
      <div class="stat-value green" id="statDone">0</div>
    </div>
    <div class="stat-card">
      <div class="stat-label">🔧 В процессе</div>
      <div class="stat-value yellow" id="statInProgress">0</div>
    </div>
    <div class="stat-card">
      <div class="stat-label">💰 Общая стоимость</div>
      <div class="stat-value" id="statCost">0 ₽</div>
    </div>
  </div>

  <div class="toolbar">
    <input type="text" class="search" id="search" placeholder="🔍 Поиск по названию, комментарию..." oninput="render()">
    <select class="filter" id="filterStatus" onchange="render()">
      <option value="">Все статусы</option>
      <option value="Планируется">Планируется</option>
      <option value="В процессе">В процессе</option>
      <option value="Сделано">Сделано</option>
    </select>
    <select class="filter" id="filterPayment" onchange="render()">
      <option value="">Все оплаты</option>
      <option value="Оплачено">Оплачено</option>
      <option value="Не оплачено">Не оплачено</option>
    </select>
    <button class="btn btn-ghost" onclick="exportData()">⬇ Экспорт</button>
  </div>

  <div class="grid" id="grid"></div>
  <div class="empty" id="empty" style="display:none">
    <div class="empty-icon">🔧</div>
    <h3>Пока пусто</h3>
    <p>Добавьте первую запись о работе или плане по машине</p>
  </div>
</div>

<!-- Модальное окно -->
<div class="modal-overlay" id="modalOverlay" onclick="if(event.target===this)closeModal()">
  <div class="modal">
    <h2 id="modalTitle">Новая запись</h2>
    <form id="form" onsubmit="saveItem(event)">
      <input type="hidden" id="itemId">
      <div class="form-grid">
        <div class="form-field full">
          <label>Наименование *</label>
          <input type="text" id="name" required placeholder="Например: Замена масла">
        </div>
        <div class="form-field">
          <label>Дата</label>
          <input type="date" id="date">
        </div>
        <div class="form-field">
          <label>Категория</label>
          <select id="category">
            <option>ТО</option>
            <option>Ремонт</option>
            <option>Тюнинг</option>
            <option>Расходники</option>
            <option>Другое</option>
          </select>
        </div>
        <div class="form-field">
          <label>Необходимость</label>
          <select id="necessity">
            <option>Обязательно</option>
            <option>Желательно</option>
            <option>Опционально</option>
          </select>
        </div>
        <div class="form-field">
          <label>Состояние</label>
          <select id="status">
            <option>Планируется</option>
            <option>В процессе</option>
            <option>Сделано</option>
          </select>
        </div>
        <div class="form-field">
          <label>Стоимость (₽)</label>
          <input type="number" id="cost" min="0" step="1" placeholder="0">
        </div>
        <div class="form-field">
          <label>Статус оплаты</label>
          <select id="payment">
            <option>Не оплачено</option>
            <option>Оплачено</option>
          </select>
        </div>
        <div class="form-field">
          <label>Статус доставки</label>
          <select id="delivery">
            <option>Не требуется</option>
            <option>Заказано</option>
            <option>Доставлено</option>
          </select>
        </div>
        <div class="form-field">
          <label>Дата доставки</label>
          <input type="date" id="deliveryDate">
        </div>
        <div class="form-field full">
          <label>Комментарии</label>
          <textarea id="comment" placeholder="Детали, артикулы, адреса..."></textarea>
        </div>
        <div class="form-field full">
          <label>Ссылка</label>
          <input type="url" id="link" placeholder="https://...">
        </div>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-ghost" onclick="closeModal()">Отмена</button>
        <button type="submit" class="btn">Сохранить</button>
      </div>
    </form>
  </div>
</div>

<script>
// ====== Хранилище ======
const STORAGE_KEY = 'car_tracker_items_v1';
let items = JSON.parse(localStorage.getItem(STORAGE_KEY) || '[]');

function persist() { localStorage.setItem(STORAGE_KEY, JSON.stringify(items)); }

// ====== Модалка ======
function openModal(id) {
  const overlay = document.getElementById('modalOverlay');
  const form = document.getElementById('form');
  form.reset();
  document.getElementById('itemId').value = '';

  if (id) {
    const it = items.find(x => x.id === id);
    if (it) {
      document.getElementById('modalTitle').textContent = 'Редактировать запись';
      document.getElementById('itemId').value = it.id;
      ['name','date','category','necessity','status','cost','payment','delivery','deliveryDate','comment','link']
        .forEach(k => { const el = document.getElementById(k); if (el) el.value = it[k] || ''; });
    }
  } else {
    document.getElementById('modalTitle').textContent = 'Новая запись';
    document.getElementById('date').value = new Date().toISOString().slice(0,10);
  }
  overlay.classList.add('active');
}
function closeModal() { document.getElementById('modalOverlay').classList.remove('active'); }

// ====== Сохранение ======
function saveItem(e) {
  e.preventDefault();
  const id = document.getElementById('itemId').value || (Date.now() + Math.random().toString(36).slice(2));
  const item = {
    id,
    name: document.getElementById('name').value.trim(),
    date: document.getElementById('date').value,
    category: document.getElementById('category').value,
    necessity: document.getElementById('necessity').value,
    status: document.getElementById('status').value,
    cost: Number(document.getElementById('cost').value) || 0,
    payment: document.getElementById('payment').value,
    delivery: document.getElementById('delivery').value,
    deliveryDate: document.getElementById('deliveryDate').value,
    comment: document.getElementById('comment').value.trim(),
    link: document.getElementById('link').value.trim(),
  };
  const idx = items.findIndex(x => x.id === id);
  if (idx >= 0) items[idx] = item; else items.unshift(item);
  persist(); closeModal(); render();
}

function deleteItem(id) {
  if (!confirm('Удалить эту запись?')) return;
  items = items.filter(x => x.id !== id);
  persist(); render();
}

function toggleDone(id) {
  const it = items.find(x => x.id === id);
  if (it) { it.status = it.status === 'Сделано' ? 'Планируется' : 'Сделано'; persist(); render(); }
}

// ====== Отрисовка ======
function badgeClass(text) {
  const map = {
    'Сделано':'done', 'В процессе':'inprogress', 'Планируется':'planned',
    'Обязательно':'required', 'Опционально':'optional',
    'Оплачено':'paid', 'Не оплачено':'unpaid',
    'Доставлено':'delivered', 'Заказано':'ordered'
  };
  return map[text] || '';
}
function esc(s){ return (s||'').replace(/[&<>"']/g, c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c])); }
function fmtDate(d){ if(!d) return ''; const [y,m,day]=d.split('-'); return `${day}.${m}.${y}`; }

function render() {
  const q = document.getElementById('search').value.toLowerCase().trim();
  const fs = document.getElementById('filterStatus').value;
  const fp = document.getElementById('filterPayment').value;

  let list = items.filter(it => {
    if (fs && it.status !== fs) return false;
    if (fp && it.payment !== fp) return false;
    if (q && !(it.name.toLowerCase().includes(q) || (it.comment||'').toLowerCase().includes(q))) return false;
    return true;
  });

  // Статистика по всем (не отфильтрованным)
  document.getElementById('statTotal').textContent = items.length;
  document.getElementById('statDone').textContent = items.filter(x=>x.status==='Сделано').length;
  document.getElementById('statInProgress').textContent = items.filter(x=>x.status==='В процессе').length;
  const totalCost = items.reduce((s,x)=>s+(x.cost||0),0);
  document.getElementById('statCost').textContent = totalCost.toLocaleString('ru-RU') + ' ₽';

  const grid = document.getElementById('grid');
  const empty = document.getElementById('empty');
  grid.innerHTML = '';
  empty.style.display = list.length === 0 ? 'block' : 'none';

  list.forEach(it => {
    const el = document.createElement('div');
    el.className = 'item';
    el.innerHTML = `
      <div class="item-header">
        <div class="item-title">${esc(it.name)}</div>
        <div class="item-actions">
          <button class="icon-btn" title="Отметить сделано" onclick="toggleDone('${it.id}')">${it.status==='Сделано'?'↺':'✓'}</button>
          <button class="icon-btn" title="Редактировать" onclick="openModal('${it.id}')">✎</button>
          <button class="icon-btn danger" title="Удалить" onclick="deleteItem('${it.id}')">✕</button>
        </div>
      </div>
      <div class="badges">
        <span class="badge ${badgeClass(it.status)}">${esc(it.status)}</span>
        <span class="badge ${badgeClass(it.necessity)}">${esc(it.necessity)}</span>
        <span class="badge ${badgeClass(it.payment)}">${esc(it.payment)}</span>
        ${it.delivery && it.delivery!=='Не требуется' ? `<span class="badge ${badgeClass(it.delivery)}">${esc(it.delivery)}</span>` : ''}
        <span class="badge" style="background:rgba(124,92,255,.15);color:#a48bff">${esc(it.category)}</span>
      </div>
      <div class="item-meta">
        ${it.date ? `<div>📅 Дата: <strong>${fmtDate(it.date)}</strong></div>` : ''}
        ${it.cost ? `<div>💰 Стоимость: <strong>${it.cost.toLocaleString('ru-RU')} ₽</strong></div>` : ''}
        ${it.deliveryDate ? `<div>🚚 Доставка: <strong>${fmtDate(it.deliveryDate)}</strong></div>` : ''}
      </div>
      ${it.comment ? `<div class="item-comment">${esc(it.comment)}</div>` : ''}
      ${it.link ? `<a class="item-link" href="${esc(it.link)}" target="_blank" rel="noopener">🔗 Открыть ссылку</a>` : ''}
    `;
    grid.appendChild(el);
  });
}

// ====== Экспорт ======
function exportData() {
  const blob = new Blob([JSON.stringify(items, null, 2)], {type:'application/json'});
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url; a.download = 'car-tracker-' + new Date().toISOString().slice(0,10) + '.json';
  a.click(); URL.revokeObjectURL(url);
}

// ====== Инициализация ======
render();
</script>
</body>
</html>