<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ديوان شعري</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Amiri:ital,wght@0,400;0,700;1,400&family=Cairo:wght@300;400;600;700&display=swap" rel="stylesheet">
<style>
  * { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --gold: #c9a84c;
    --gold-light: #e8d5a3;
    --gold-dark: #8b6914;
    --ink: #1a1410;
    --ink-soft: #3d3028;
    --parchment: #faf6ef;
    --parchment-dark: #f0e9d8;
  }

  body {
    font-family: 'Cairo', sans-serif;
    background: var(--ink);
    color: var(--parchment);
    line-height: 1.8;
  }

  /* ===== Header ===== */
  header {
    background: linear-gradient(135deg, #2a1f17, #1a1410);
    padding: 60px 20px 80px;
    text-align: center;
    border-bottom: 3px solid var(--gold);
  }

  header h1 {
    font-family: 'Amiri', serif;
    font-size: 3rem;
    color: var(--gold);
    margin-bottom: 10px;
  }

  header p {
    color: var(--gold-light);
    font-size: 1.1rem;
  }

  /* ===== Controls ===== */
  .controls {
    max-width: 900px;
    margin: -40px auto 0;
    padding: 20px;
    display: flex;
    flex-wrap: wrap;
    gap: 12px;
    justify-content: center;
  }

  .controls input,
  .controls select {
    font-family: 'Cairo', sans-serif;
    padding: 12px 18px;
    border-radius: 30px;
    border: 1px solid var(--gold-dark);
    background: var(--parchment);
    color: var(--ink);
    font-size: 0.95rem;
    min-width: 220px;
  }

  /* ===== Stats ===== */
  .stats {
    max-width: 900px;
    margin: 20px auto;
    padding: 20px;
    background: var(--parchment);
    border-radius: 16px;
    display: flex;
    justify-content: space-around;
    flex-wrap: wrap;
    color: var(--ink);
  }

  .stats .stat { text-align: center; padding: 10px 20px; }
  .stats .stat .num { font-size: 1.8rem; font-weight: 700; color: var(--gold-dark); }
  .stats .stat .label { font-size: 0.85rem; color: var(--ink-soft); }

  /* ===== Poems grid ===== */
  main {
    max-width: 1000px;
    margin: 0 auto;
    padding: 30px 20px 80px;
  }

  .section-title {
    font-family: 'Amiri', serif;
    font-size: 2rem;
    color: var(--gold);
    text-align: center;
    margin-bottom: 30px;
    position: relative;
  }

  .poems-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
    gap: 20px;
  }

  .poem-card {
    background: var(--parchment);
    color: var(--ink);
    border-radius: 16px;
    padding: 24px;
    cursor: pointer;
    transition: transform 0.2s ease, box-shadow 0.2s ease;
    border: 1px solid var(--parchment-dark);
    position: relative;
  }

  .poem-card:hover {
    transform: translateY(-4px);
    box-shadow: 0 10px 25px rgba(201,168,76,0.25);
  }

  .poem-card h3 {
    font-family: 'Amiri', serif;
    font-size: 1.4rem;
    color: var(--ink);
    margin-bottom: 8px;
  }

  .poem-card .meta {
    font-size: 0.8rem;
    color: var(--ink-soft);
    margin-bottom: 12px;
  }

  .poem-card .excerpt {
    font-family: 'Amiri', serif;
    font-size: 1rem;
    color: var(--ink-soft);
    white-space: pre-line;
  }

  .tag {
    display: inline-block;
    background: var(--gold-dark);
    color: var(--parchment);
    font-size: 0.75rem;
    padding: 3px 10px;
    border-radius: 20px;
    margin-top: 10px;
  }

  /* ===== Modal ===== */
  .modal-overlay {
    display: none;
    position: fixed;
    inset: 0;
    background: rgba(0,0,0,0.75);
    z-index: 100;
    align-items: center;
    justify-content: center;
    padding: 20px;
  }

  .modal-overlay.active { display: flex; }

  .modal {
    background: var(--parchment);
    color: var(--ink);
    max-width: 600px;
    width: 100%;
    max-height: 85vh;
    overflow-y: auto;
    border-radius: 20px;
    padding: 40px;
    position: relative;
  }

  .modal h2 {
    font-family: 'Amiri', serif;
    font-size: 1.8rem;
    margin-bottom: 6px;
    color: var(--ink);
  }

  .modal .meta { color: var(--ink-soft); font-size: 0.85rem; margin-bottom: 20px; }

  .modal .body {
    font-family: 'Amiri', serif;
    font-size: 1.2rem;
    white-space: pre-line;
    text-align: center;
    line-height: 2.2;
  }

  .modal-close {
    position: absolute;
    top: 16px;
    left: 16px;
    background: var(--ink);
    color: var(--parchment);
    border: none;
    width: 32px;
    height: 32px;
    border-radius: 50%;
    cursor: pointer;
    font-size: 1rem;
  }

  /* ===== Footer / copyright ===== */
  footer {
    background: #14100c;
    padding: 30px 20px;
    text-align: center;
    color: var(--gold-light);
    font-size: 0.85rem;
    border-top: 1px solid var(--gold-dark);
  }

  .watermark {
    opacity: 0.6;
    font-size: 0.8rem;
    margin-top: 6px;
  }

  @media (max-width: 600px) {
    header h1 { font-size: 2.2rem; }
    .controls input, .controls select { min-width: 100%; }
  }
</style>
</head>
<body oncontextmenu="return false;">

<header>
  <h1>ديوان شعري</h1>
  <p>أكتب بقلم حبره من دم</p>
</header>

<div class="controls">
  <input type="text" id="searchInput" placeholder="ابحث في القصائد...">
  <select id="filterTag">
    <option value="all">جميع الأغراض</option>
  </select>
</div>

<div class="stats">
  <div class="stat"><div class="num" id="statPoems">0</div><div class="label">إجمالي القصائد</div></div>
  <div class="stat"><div class="num" id="statTags">0</div><div class="label">الأغراض الشعرية</div></div>
  <div class="stat"><div class="num" id="statLines">0</div><div class="label">إجمالي الأبيات</div></div>
</div>

<main>
  <h2 class="section-title">القصائد</h2>
  <div class="poems-grid" id="poemsGrid"></div>
</main>

<footer>
  <p>© جميع الحقوق محفوظة لكاتب هذا الديوان. يمنع نسخ أو إعادة نشر أي قصيدة دون إذن.</p>
  <p class="watermark">صُمم وأُنشئ بواسطة صاحب الموقع</p>
</footer>

<div class="modal-overlay" id="modalOverlay">
  <div class="modal">
    <button class="modal-close" onclick="closeModal()">✕</button>
    <h2 id="modalTitle"></h2>
    <div class="meta" id="modalMeta"></div>
    <div class="body" id="modalBody"></div>
  </div>
</div>

<script>
/* ============================================
   ضع قصائدك هنا. كل قصيدة عنصر واحد بالمصفوفة.
   - title: عنوان القصيدة
   - date: التاريخ (اختياري)
   - tag: الغرض الشعري (غزل، رثاء، حكمة...)
   - body: نص القصيدة. استخدم \n للنزول سطر جديد بين الأبيات
   ============================================ */
const poems = [
  {
    title: "عنوان القصيدة الأولى",
    date: "2024",
    tag: "غزل",
    body: "البيت الأول من القصيدة هنا\nالبيت الثاني من القصيدة هنا\nالبيت الثالث من القصيدة هنا"
  },
  {
    title: "عنوان القصيدة الثانية",
    date: "2024",
    tag: "حكمة",
    body: "بيت أول\nبيت ثاني"
  }
];

const grid = document.getElementById('poemsGrid');
const searchInput = document.getElementById('searchInput');
const filterTag = document.getElementById('filterTag');
const modalOverlay = document.getElementById('modalOverlay');

function buildTagsFilter() {
  const tags = [...new Set(poems.map(p => p.tag))];
  tags.forEach(tag => {
    const opt = document.createElement('option');
    opt.value = tag;
    opt.textContent = tag;
    filterTag.appendChild(opt);
  });
}

function renderPoems() {
  const query = searchInput.value.trim().toLowerCase();
  const tag = filterTag.value;

  grid.innerHTML = '';
  let shown = 0;

  poems.forEach((poem, index) => {
    const matchesQuery = poem.title.toLowerCase().includes(query) || poem.body.toLowerCase().includes(query);
    const matchesTag = tag === 'all' || poem.tag === tag;
    if (!matchesQuery || !matchesTag) return;

    shown++;
    const excerpt = poem.body.split('\n').slice(0, 2).join('\n');

    const card = document.createElement('div');
    card.className = 'poem-card';
    card.innerHTML = `
      <h3>${poem.title}</h3>
      <div class="meta">${poem.date}</div>
      <div class="excerpt">${excerpt}</div>
      <span class="tag">${poem.tag}</span>
    `;
    card.addEventListener('click', () => openModal(index));
    grid.appendChild(card);
  });

  updateStats();
}

function updateStats() {
  document.getElementById('statPoems').textContent = poems.length;
  document.getElementById('statTags').textContent = new Set(poems.map(p => p.tag)).size;
  const totalLines = poems.reduce((sum, p) => sum + p.body.split('\n').length, 0);
  document.getElementById('statLines').textContent = totalLines;
}

function openModal(index) {
  const poem = poems[index];
  document.getElementById('modalTitle').textContent = poem.title;
  document.getElementById('modalMeta').textContent = `${poem.date} • ${poem.tag}`;
  document.getElementById('modalBody').textContent = poem.body;
  modalOverlay.classList.add('active');
}

function closeModal() {
  modalOverlay.classList.remove('active');
}

modalOverlay.addEventListener('click', (e) => {
  if (e.target === modalOverlay) closeModal();
});

searchInput.addEventListener('input', renderPoems);
filterTag.addEventListener('change', renderPoems);

/* حماية بسيطة: تعطيل النسخ بالكيبورد ونقل التحديد */
document.addEventListener('keydown', (e) => {
  if ((e.ctrlKey || e.metaKey) && (e.key === 'c' || e.key === 'u' || e.key === 's')) {
    e.preventDefault();
  }
});

buildTagsFilter();
renderPoems();
</script>

</body>
</html>

