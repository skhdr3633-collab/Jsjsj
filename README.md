<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>لوحة الإدارة - Aura_iQ</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@300;400;500;700;900&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0a0a0a;
    --bg-elev: #121012;
    --red: #e1122a;
    --red-bright: #ff2f45;
    --text: #f2efee;
    --text-muted: #a39d9c;
    --border: rgba(255,255,255,0.08);
  }
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Tajawal', sans-serif;
    padding: 20px;
  }
  .container { max-width: 1000px; margin: 0 auto; }
  
  header { text-align: center; margin-bottom: 40px; }
  h1 { font-size: 2rem; margin-bottom: 10px; }
  h1 .red { color: var(--red-bright); }
  .subtitle { color: var(--text-muted); }

  .panel {
    background: var(--bg-elev);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 20px;
    margin-bottom: 30px;
  }

  .panel h2 { font-size: 1.3rem; margin-bottom: 20px; color: var(--text); }

  .input-group {
    margin-bottom: 15px;
  }
  .input-group label {
    display: block;
    font-size: 0.9rem;
    margin-bottom: 6px;
    color: var(--text-muted);
    font-weight: 600;
  }
  input[type="text"], input[type="file"] {
    width: 100%;
    background: rgba(255,255,255,0.05);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 12px;
    color: var(--text);
    font-family: 'Tajawal', sans-serif;
    font-size: 1rem;
  }
  input:focus {
    outline: none;
    border-color: var(--red);
    background: rgba(225,18,42,0.08);
  }

  .preview-img {
    width: 100%;
    max-width: 200px;
    border-radius: 8px;
    margin-top: 10px;
    border: 1px solid var(--border);
  }

  .size-hint {
    font-size: 0.78rem;
    color: var(--text-muted);
    margin-top: 6px;
  }

  .btn-group {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
  }
  button {
    padding: 14px;
    border: none;
    border-radius: 8px;
    font-weight: 700;
    cursor: pointer;
    font-family: 'Tajawal', sans-serif;
    font-size: 1rem;
    transition: all 0.2s ease;
  }
  .btn-add {
    background: var(--red);
    color: white;
  }
  .btn-add:active { transform: scale(0.98); }
  .btn-add:disabled { opacity: 0.5; cursor: not-allowed; }
  
  .btn-clear {
    background: rgba(255,255,255,0.1);
    color: var(--text);
    grid-column: 1 / -1;
  }
  .btn-clear:active { transform: scale(0.98); }

  .btn-export {
    background: rgba(76,175,80,0.2);
    color: #4caf50;
    grid-column: 1 / -1;
    margin-top: 10px;
  }

  .shortcuts-container {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
    gap: 12px;
  }
  .shortcut-item {
    border: 1px solid var(--border);
    border-radius: 8px;
    overflow: hidden;
    background: rgba(255,255,255,0.02);
    text-align: center;
    position: relative;
  }
  .shortcut-img {
    width: 100%;
    aspect-ratio: 4/3;
    background: linear-gradient(135deg, #1a1414, #0d0a0a);
    display: flex;
    align-items: center;
    justify-content: center;
    border-bottom: 2px solid rgba(225,18,42,0.2);
  }
  .shortcut-img img { width: 100%; height: 100%; object-fit: cover; }
  .shortcut-img .placeholder {
    width: 24px;
    height: 24px;
    color: var(--text-muted);
    opacity: 0.4;
  }
  .shortcut-title {
    padding: 8px 6px;
    font-size: 0.8rem;
    font-weight: 500;
    word-break: break-word;
  }
  .btn-delete {
    position: absolute;
    top: 4px;
    left: 4px;
    width: 22px;
    height: 22px;
    background: rgba(255,59,48,0.9);
    border: none;
    border-radius: 50%;
    color: white;
    cursor: pointer;
    font-weight: bold;
    opacity: 0;
    transition: opacity 0.2s ease;
  }
  .shortcut-item:hover .btn-delete { opacity: 1; }

  .stats {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 10px;
    margin-top: 20px;
    padding-top: 20px;
    border-top: 1px solid var(--border);
  }
  .stat {
    text-align: center;
    padding: 12px;
    border-radius: 8px;
    background: rgba(225,18,42,0.1);
  }
  .stat-num { font-size: 1.5rem; font-weight: 700; color: var(--red-bright); }
  .stat-label { font-size: 0.72rem; color: var(--text-muted); margin-top: 4px; }
  .stat.warn { background: rgba(255,152,0,0.15); }
  .stat.warn .stat-num { color: #ff9800; }
  .stat.danger { background: rgba(255,59,48,0.2); }
  .stat.danger .stat-num { color: #ff3b30; }

  .empty-msg {
    text-align: center;
    padding: 30px;
    color: var(--text-muted);
  }

  @media (max-width: 600px) {
    .btn-group { grid-template-columns: 1fr; }
    .stats { grid-template-columns: 1fr; }
  }
</style>
</head>
<body>

<div class="container">
  <header>
    <h1>Aura<span class="red">_iQ</span> — لوحة الإدارة</h1>
    <p class="subtitle">أضف الاختصارات التي تشرحها كل يوم</p>
  </header>

  <!-- إضافة اختصار -->
  <div class="panel">
    <h2>➕ إضافة اختصار جديد</h2>

    <div class="input-group">
      <label>اسم الاختصار:</label>
      <input type="text" id="titleInput" placeholder="مثال: Midjourney">
    </div>

    <div class="input-group">
      <label>الصورة (اختيارية):</label>
      <input type="file" id="imageInput" accept="image/*">
      <img id="previewImg" class="preview-img" style="display:none;">
      <div class="size-hint" id="sizeHint"></div>
    </div>

    <div class="btn-group">
      <button class="btn-add" id="addBtn" onclick="addShortcut()">✓ إضافة</button>
      <button class="btn-clear" onclick="clearForm()">🗑️ مسح</button>
      <button class="btn-export" onclick="exportHTML()">📄 صدّر الموقع</button>
    </div>

    <div class="stats">
      <div class="stat">
        <div class="stat-num" id="totalCount">0</div>
        <div class="stat-label">إجمالي الاختصارات</div>
      </div>
      <div class="stat">
        <div class="stat-num" id="todayCount">0</div>
        <div class="stat-label">اليوم</div>
      </div>
      <div class="stat" id="storageStat">
        <div class="stat-num" id="storagePercent">0%</div>
        <div class="stat-label">مساحة التخزين المستخدمة</div>
      </div>
    </div>
  </div>

  <!-- عرض الاختصارات -->
  <div class="panel">
    <h2>📸 معاينة الاختصارات</h2>
    <div id="shortcutsDisplay" class="shortcuts-container"></div>
  </div>
</div>

<script>
  const TODAY = new Date().toISOString().split('T')[0];
  // الحد الأقصى التقريبي لتخزين المتصفح (نتحفظ بهامش أمان)
  const STORAGE_LIMIT_BYTES = 5 * 1024 * 1024; // ~5 ميجا
  // أقصى بعد للصورة بعد الضغط (بكسل) وجودة الضغط
  const MAX_IMAGE_DIMENSION = 900;
  const IMAGE_QUALITY = 0.72;

  let pendingImageBase64 = '';

  // تحميل البيانات
  function loadShortcuts() {
    const saved = localStorage.getItem('auriq_daily_shortcuts');
    return saved ? JSON.parse(saved) : {};
  }

  // حفظ البيانات (مع معالجة حالة امتلاء التخزين)
  function saveShortcuts(data) {
    try {
      localStorage.setItem('auriq_daily_shortcuts', JSON.stringify(data));
      updateDisplay();
      updateStats();
      return true;
    } catch (err) {
      alert('⚠️ التخزين ممتلئ! ما فيك تضيف صور جديدة حالياً.\nجرب تحذف صور قديمة ما بعد تحتاجها، أو صدّر الموقع الحالي واحفظه، وابدأ تخزين جديد.');
      return false;
    }
  }

  // ضغط وتصغير الصورة قبل الحفظ حتى تتسع أكبر عدد ممكن من الصور
  function compressImage(file, maxDim, quality) {
    return new Promise((resolve, reject) => {
      const reader = new FileReader();
      reader.onload = (e) => {
        const img = new Image();
        img.onload = () => {
          let { width, height } = img;
          if (width > height && width > maxDim) {
            height = Math.round(height * (maxDim / width));
            width = maxDim;
          } else if (height > maxDim) {
            width = Math.round(width * (maxDim / height));
            height = maxDim;
          }
          const canvas = document.createElement('canvas');
          canvas.width = width;
          canvas.height = height;
          const ctx = canvas.getContext('2d');
          ctx.drawImage(img, 0, 0, width, height);
          resolve(canvas.toDataURL('image/jpeg', quality));
        };
        img.onerror = reject;
        img.src = e.target.result;
      };
      reader.onerror = reject;
      reader.readAsDataURL(file);
    });
  }

  // معاينة الصورة + ضغطها فوراً عند الاختيار
  document.getElementById('imageInput')?.addEventListener('change', async function(e) {
    const file = e.target.files[0];
    if (!file) return;

    const hint = document.getElementById('sizeHint');
    hint.textContent = 'جارِ ضغط الصورة...';

    try {
      const compressed = await compressImage(file, MAX_IMAGE_DIMENSION, IMAGE_QUALITY);
      pendingImageBase64 = compressed;

      const img = document.getElementById('previewImg');
      img.src = compressed;
      img.style.display = 'block';

      const sizeKB = Math.round((compressed.length * 0.75) / 1024);
      hint.textContent = `📦 حجم الصورة بعد الضغط: ~${sizeKB} كيلوبايت`;
    } catch (err) {
      hint.textContent = '⚠️ تعذّر ضغط الصورة، جرب صورة أخرى';
    }
  });

  // إضافة اختصار
  function addShortcut() {
    const title = document.getElementById('titleInput').value.trim();
    if (!title) {
      alert('أدخل اسم الاختصار!');
      return;
    }

    const shortcuts = loadShortcuts();
    if (!shortcuts[TODAY]) shortcuts[TODAY] = [];

    shortcuts[TODAY].push({
      id: Date.now(),
      title: title,
      imageBase64: pendingImageBase64 || ''
    });

    const ok = saveShortcuts(shortcuts);
    if (ok) {
      clearForm();
    }
  }

  // حذف اختصار
  function deleteShortcut(id) {
    const shortcuts = loadShortcuts();
    if (shortcuts[TODAY]) {
      shortcuts[TODAY] = shortcuts[TODAY].filter(s => s.id !== id);
      saveShortcuts(shortcuts);
    }
  }

  // مسح النموذج
  function clearForm() {
    document.getElementById('titleInput').value = '';
    document.getElementById('imageInput').value = '';
    document.getElementById('previewImg').style.display = 'none';
    document.getElementById('sizeHint').textContent = '';
    pendingImageBase64 = '';
  }

  // تحديث العرض
  function updateDisplay() {
    const shortcuts = loadShortcuts();
    const todayShortcuts = shortcuts[TODAY] || [];
    const container = document.getElementById('shortcutsDisplay');

    if (todayShortcuts.length === 0) {
      container.innerHTML = '<div class="empty-msg" style="grid-column:1/-1;">لا توجد اختصارات لاليوم</div>';
      return;
    }

    container.innerHTML = todayShortcuts.map(s => `
      <div class="shortcut-item">
        <button class="btn-delete" onclick="deleteShortcut(${s.id})">✕</button>
        <div class="shortcut-img">
          ${s.imageBase64 ? `<img src="${s.imageBase64}" alt="${s.title}">` : `
          <svg class="placeholder" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
            <rect x="3" y="3" width="18" height="18" rx="3"/>
            <circle cx="8.5" cy="9" r="1.5"/>
            <path d="m21 15-5-5-9 9"/>
          </svg>`}
        </div>
        <div class="shortcut-title">${s.title}</div>
      </div>
    `).join('');
  }

  // تحديث الإحصائيات (بما فيها نسبة امتلاء التخزين)
  function updateStats() {
    const raw = localStorage.getItem('auriq_daily_shortcuts') || '';
    const shortcuts = loadShortcuts();
    const todayShortcuts = shortcuts[TODAY] || [];
    const allShortcuts = Object.values(shortcuts).flat();

    document.getElementById('todayCount').textContent = todayShortcuts.length;
    document.getElementById('totalCount').textContent = allShortcuts.length;

    const usedBytes = new Blob([raw]).size;
    const percent = Math.min(100, Math.round((usedBytes / STORAGE_LIMIT_BYTES) * 100));
    document.getElementById('storagePercent').textContent = percent + '%';

    const statEl = document.getElementById('storageStat');
    statEl.classList.remove('warn', 'danger');
    if (percent >= 90) statEl.classList.add('danger');
    else if (percent >= 65) statEl.classList.add('warn');
  }

  // تصدير الموقع
  function exportHTML() {
    const shortcuts = loadShortcuts();
    const allList = Object.values(shortcuts).flat();

    const shortcutsHTML = allList.map(s => `
      <figure class="shortcut-card">
        <div class="shortcut-media">
          ${s.imageBase64 ? `<img src="${s.imageBase64}" alt="">` : `<svg class="placeholder-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><rect x="3" y="3" width="18" height="18" rx="3"/><circle cx="8.5" cy="9" r="1.5"/><path d="m21 15-5-5-9 9"/></svg>`}
        </div>
        <figcaption>${s.title}</figcaption>
      </figure>
    `).join('');

    const html = `<!DOCTYPE html><html lang="ar" dir="rtl"><head><meta charset="UTF-8"><meta name="viewport" content="width=device-width,initial-scale=1.0"><title>Aura_iQ</title><link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@400;700&display=swap" rel="stylesheet"><style>:root{--bg:#0a0a0a;--red:#e1122a;--text:#f2efee;--border:rgba(255,255,255,0.08);}*{margin:0;padding:0;box-sizing:border-box;}body{background:var(--bg);color:var(--text);font-family:'Tajawal',sans-serif;}section{padding:60px 20px;max-width:1100px;margin:0 auto;}.section-head{text-align:center;margin-bottom:40px;}.section-head h2{font-size:2rem;font-weight:700;margin-bottom:10px;}.shortcuts-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(200px,1fr));gap:20px;}.shortcut-card{border:1px solid var(--border);border-radius:12px;overflow:hidden;background:#121012;}.shortcut-media{width:100%;aspect-ratio:4/3;background:linear-gradient(135deg,#1a1414,#0d0a0a);display:flex;align-items:center;justify-content:center;}.shortcut-media img{width:100%;height:100%;object-fit:cover;}.shortcut-card figcaption{padding:12px;text-align:center;font-weight:500;}</style></head><body><section><div class="section-head"><h2>اختصارات Aura_iQ</h2></div><div class="shortcuts-grid">${shortcutsHTML}</div></section></body></html>`;

    const blob = new Blob([html], { type: 'text/html' });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = `aura-iq-${Date.now()}.html`;
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
    
    alert('✅ تم التصدير! تحقق من مجلد التحميلات');
  }

  // تحميل البيانات عند فتح الصفحة
  updateDisplay();
  updateStats();

  // تحديث عند تغيير البيانات من نافذة أخرى
  window.addEventListener('storage', () => {
    updateDisplay();
    updateStats();
  });
</script>

</body>
</html>
