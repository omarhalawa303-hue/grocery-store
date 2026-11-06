<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>تموينات ومخابز قلعة الأغذية</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@400;500;700;800&display=swap" rel="stylesheet">
  <style>
    :root {
      --primary: #1e7e34;
      --primary-dark: #155724;
      --accent: #f59e0b;
      --danger: #dc3545;
      --bg: #f8fafc;
      --surface: #ffffff;
      --text: #1e293b;
      --muted: #64748b;
      --border: #e2e8f0;
      --radius: 12px;
      --shadow: 0 4px 6px -1px rgba(0,0,0,0.08);
    }
    * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Tajawal', sans-serif; }
    body { background-color: var(--bg); color: var(--text); padding-bottom: 90px; }
    nav {
      background: var(--surface);
      border-bottom: 1px solid var(--border);
      padding: 12px 20px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      position: sticky;
      top: 0;
      z-index: 50;
    }
    .brand { font-size: 1.1rem; font-weight: 800; color: var(--primary); }
    .nav-actions { display: flex; gap: 8px; align-items: center; }
    .btn {
      padding: 7px 14px;
      border-radius: 8px;
      font-size: 0.85rem;
      font-weight: 600;
      cursor: pointer;
      border: 1px solid transparent;
      transition: 0.2s;
    }
    .btn-primary { background: var(--primary); color: white; }
    .btn-outline { border-color: var(--border); background: transparent; color: var(--text); }
    .btn-danger { background: var(--danger); color: white; }
    .btn-sm { padding: 4px 8px; font-size: 0.75rem; }
    header {
      background: linear-gradient(135deg, var(--primary), var(--primary-dark));
      color: white;
      padding: 24px 16px;
      text-align: center;
    }
    header h1 { font-size: 1.4rem; margin-bottom: 4px; }
    header p { font-size: 0.85rem; opacity: 0.9; }
    .container { max-width: 960px; margin: 0 auto; padding: 16px; }
    .search-bar { width: 100%; padding: 10px 14px; border: 1px solid var(--border); border-radius: var(--radius); margin-bottom: 12px; }
    .categories { display: flex; gap: 8px; overflow-x: auto; padding-bottom: 10px; scrollbar-width: none; }
    .categories::-webkit-scrollbar { display: none; }
    .cat-pill {
      background: var(--surface);
      border: 1px solid var(--border);
      padding: 6px 14px;
      border-radius: 20px;
      font-size: 0.85rem;
      white-space: nowrap;
      cursor: pointer;
    }
    .cat-pill.active { background: var(--primary); color: white; border-color: var(--primary); }
    .grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(170px, 1fr)); gap: 14px; margin-top: 10px; }
    .card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      padding: 12px;
      box-shadow: var(--shadow);
      display: flex;
      flex-direction: column;
      justify-content: space-between;
    }
    .card h3 { font-size: 0.95rem; margin-bottom: 4px; }
    .card .category-tag { font-size: 0.75rem; color: var(--muted); }
    .card .price { font-size: 1.1rem; font-weight: 700; color: var(--primary); margin: 8px 0; }
    .cart-bar {
      position: fixed;
      bottom: 0; left: 0; right: 0;
      background: var(--surface);
      border-top: 1px solid var(--border);
      padding: 12px 16px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      z-index: 40;
    }
    .admin-panel {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      padding: 20px;
      margin-bottom: 24px;
    }
    .table-responsive { width: 100%; overflow-x: auto; margin-top: 12px; }
    table { width: 100%; border-collapse: collapse; font-size: 0.85rem; }
    table th, table td { padding: 8px 10px; border-bottom: 1px solid var(--border); text-align: right; }
    .modal {
      display: none;
      position: fixed;
      inset: 0;
      background: rgba(0,0,0,0.6);
      z-index: 100;
      align-items: center;
      justify-content: center;
      padding: 16px;
    }
    .modal-box {
      background: var(--surface);
      border-radius: var(--radius);
      width: 100%;
      max-width: 440px;
      padding: 20px;
      max-height: 90vh;
      overflow-y: auto;
    }
    .modal-box h2 { font-size: 1.2rem; margin-bottom: 12px; }
    .form-group { margin-bottom: 12px; }
    .form-group label { display: block; font-size: 0.85rem; font-weight: 600; margin-bottom: 4px; }
    .form-group input, .form-group select, .form-group textarea {
      width: 100%;
      padding: 9px;
      border: 1px solid var(--border);
      border-radius: 8px;
      font-size: 0.9rem;
    }
    .hint { font-size: 0.75rem; color: var(--muted); margin-top: 4px; }
  </style>
</head>
<body>

  <nav>
    <div class="brand">قلعة الأغذية 🛒</div>
    <div class="nav-actions" id="userArea"></div>
  </nav>

  <header>
    <h1>تموينات ومخابز قلعة الأغذية</h1>
    <p>توصيل سريع إلى باب منزلك في حي العريجاء والأحياء المجاورة</p>
  </header>

  <div class="container">
    <div id="adminSection" style="display: none;" class="admin-panel">
      <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 12px;">
        <h2>🛠 لوحة إدارة المنتجات (خاص بالمدير)</h2>
        <button class="btn btn-primary" onclick="openAddProductModal()">+ إضافة منتج جديد</button>
      </div>
      <div class="table-responsive">
        <table>
          <thead>
            <tr>
              <th>الاسم</th>
              <th>القسم</th>
              <th>السعر</th>
              <th>إجراءات</th>
            </tr>
          </thead>
          <tbody id="adminProductsTable"></tbody>
        </table>
      </div>
    </div>

    <div>
      <input type="text" id="searchInput" class="search-bar" placeholder="ابحث عن منتج، خبز، حليب..." oninput="filterProducts()">
      <div class="categories" id="categoryFilter">
        <button class="cat-pill active" onclick="setCategory('all', this)">الكل</button>
        <button class="cat-pill" onclick="setCategory('bakery', this)">المخبوزات</button>
        <button class="cat-pill" onclick="setCategory('dairy', this)">ألبان وأجبان</button>
        <button class="cat-pill" onclick="setCategory('drinks', this)">مشروبات ومياه</button>
        <button class="cat-pill" onclick="setCategory('pantry', this)">مواد غذائية</button>
      </div>
      <div class="grid" id="productGrid"></div>
    </div>
  </div>

  <div class="cart-bar">
    <div>
      <div style="font-size: 0.8rem; color: var(--muted);">الإجمالي:</div>
      <div style="font-weight: 800; font-size: 1.15rem; color: var(--primary);" id="totalPrice">0.00 ر.س</div>
    </div>
    <button class="btn btn-primary" style="padding: 10px 18px; font-size: 0.95rem;" onclick="openOrderModal()">
      متابعة الطلب (<span id="cartCount">0</span>)
    </button>
  </div>

  <div class="modal" id="loginModal">
    <div class="modal-box">
      <h2>تسجيل الدخول</h2>
      <p style="font-size: 0.8rem; color: var(--muted); margin-bottom: 14px;">
        حساب الأدمن: <b>0535050089</b> | كلمة المرور: <b>12345678</b>
      </p>
      <div class="form-group">
        <label>رقم الجوال:</label>
        <input type="tel" id="loginPhone" placeholder="05XXXXXXXX">
      </div>
      <div class="form-group">
        <label>كلمة المرور (8 خانات على الأقل):</label>
        <input type="password" id="loginPassword" placeholder="••••••••">
        <div class="hint">يجب أن تتكون من 8 أرقام أو حروف كحد أدنى.</div>
      </div>
      <button class="btn btn-primary" style="width: 100%; padding: 10px; margin-top: 8px;" onclick="handleLogin()">دخول</button>
      <button class="btn btn-outline" style="width: 100%; margin-top: 6px;" onclick="closeModal('loginModal')">إلغاء</button>
    </div>
  </div>

  <div class="modal" id="changePassModal">
    <div class="modal-box">
      <h2>تغيير كلمة المرور</h2>
      <div class="form-group">
        <label>كلمة المرور الحالية:</label>
        <input type="password" id="oldPassword" placeholder="••••••••">
      </div>
      <div class="form-group">
        <label>كلمة المرور الجديدة (8 خانات على الأقل):</label>
        <input type="password" id="newPassword" placeholder="••••••••">
        <div class="hint">يجب ألا تقل عن 8 خانات.</div>
      </div>
      <div class="form-group">
        <label>تأكيد كلمة المرور الجديدة:</label>
        <input type="password" id="confirmPassword" placeholder="••••••••">
      </div>
      <button class="btn btn-primary" style="width: 100%; margin-top: 8px;" onclick="handleChangePassword()">حفظ كلمة المرور</button>
      <button class="btn btn-outline" style="width: 100%; margin-top: 6px;" onclick="closeModal('changePassModal')">إلغاء</button>
    </div>
  </div>

  <div class="modal" id="productModal">
    <div class="modal-box">
      <h2>إضافة منتج جديد للمحل</h2>
      <div class="form-group">
        <label>اسم الصنف:</label>
        <input type="text" id="prodName" placeholder="مثال: حليب نادك 2 لتر">
      </div>
      <div class="form-group">
        <label>القسم:</label>
        <select id="prodCategory">
          <option value="bakery">المخبوزات</option>
          <option value="dairy">ألبان وأجبان</option>
          <option value="drinks">مشروبات ومياه</option>
          <option value="pantry">مواد غذائية</option>
        </select>
      </div>
      <div class="form-group">
        <label>السعر (ريال سعودي):</label>
        <input type="number" step="0.5" id="prodPrice" placeholder="مثال: 12.00">
      </div>
      <button class="btn btn-primary" style="width: 100%; margin-top: 10px;" onclick="saveProduct()">حفظ المنتج</button>
      <button class="btn btn-outline" style="width: 100%; margin-top: 6px;" onclick="closeModal('productModal')">إغلاق</button>
    </div>
  </div>

  <div class="modal" id="orderModal">
    <div class="modal-box">
      <h2>بيانات التوصيل</h2>
      <div id="orderItemsSummary" style="background: var(--bg); padding: 10px; border-radius: 8px; font-size: 0.85rem; margin-bottom: 12px;"></div>
      <div class="form-group">
        <label>اسم العميل:</label>
        <input type="text" id="custName" placeholder="مثال: أبو راشد">
      </div>
      <div class="form-group">
        <label>عنوان التوصيل (الحي والشارع ورقم البيت):</label>
        <input type="text" id="custAddress" placeholder="مثال: العريجاء الغربية، شارع حمزة بن عبدالمطلب">
      </div>
      <div class="form-group">
        <label>ملاحظات إضافية:</label>
        <textarea id="custNotes" rows="2" placeholder="مثال: الخبز صامولي طازج، مياه باردة"></textarea>
      </div>
      <button class="btn btn-primary" style="width: 100%; background: #25D366; border: none; padding: 10px;" onclick="sendWhatsAppOrder()">
        إرسال الطلب عبر واتساب 💬
      </button>
      <button class="btn btn-outline" style="width: 100%; margin-top: 6px;" onclick="closeModal('orderModal')">تراجع</button>
    </div>
  </div>
  <script>
    const defaultProducts = [
      { id: 1, name: "صامولي مخبز طازج (كيس)", category: "bakery", price: 1.50 },
      { id: 2, name: "خبز مفرود أبيض", category: "bakery", price: 1.00 },
      { id: 3, name: "حليب المراعي كامل الدسم 2 لتر", category: "dairy", price: 11.00 },
      { id: 4, name: "لبن نادك طازج 1.75 لتر", category: "dairy", price: 8.50 },
      { id: 5, name: "طبق بيض بلدي كبير (30 بيضة)", category: "dairy", price: 18.00 },
      { id: 6, name: "كرتون مياه صفا 40 عبوة", category: "drinks", price: 16.50 },
      { id: 7, name: "أرز الشعلان سيلا 5 كجم", category: "pantry", price: 38.00 },
      { id: 8, name: "زيت عافية ذرة 1.5 لتر", category: "pantry", price: 19.50 }
    ];

    let adminPassword = localStorage.getItem('store_admin_pass') || '12345678';
    let products = JSON.parse(localStorage.getItem('store_products')) || defaultProducts;
    let currentUser = JSON.parse(localStorage.getItem('store_user')) || null;
    let loginAttempts = JSON.parse(localStorage.getItem('login_attempts')) || [];
    let cart = {};
    let selectedCat = 'all';

    function init() {
      renderNav();
      renderProducts();
      renderAdminTable();
      updateCartUI();
    }

    function renderNav() {
      const area = document.getElementById('userArea');
      area.textContent = '';
      if (currentUser) {
        const welcome = document.createElement('span');
        welcome.style.fontSize = '0.85rem';
        welcome.style.fontWeight = '600';
        welcome.textContent = `👋 ${currentUser.name}`;

        const changePassBtn = document.createElement('button');
        changePassBtn.className = 'btn btn-outline btn-sm';
        changePassBtn.textContent = 'تغيير الرمز';
        changePassBtn.onclick = () => openModal('changePassModal');

        const logoutBtn = document.createElement('button');
        logoutBtn.className = 'btn btn-outline btn-sm';
        logoutBtn.textContent = 'خروج';
        logoutBtn.onclick = logout;

        area.append(welcome, changePassBtn, logoutBtn);
        document.getElementById('adminSection').style.display = (currentUser.role === 'admin') ? 'block' : 'none';
      } else {
        const loginBtn = document.createElement('button');
        loginBtn.className = 'btn btn-primary btn-sm';
        loginBtn.textContent = 'تسجيل الدخول';
        loginBtn.onclick = () => openModal('loginModal');
        area.appendChild(loginBtn);
        document.getElementById('adminSection').style.display = 'none';
      }
    }

    function checkRateLimit(phone) {
      const fifteenMinutesAgo = Date.now() - 15 * 60 * 1000;
      loginAttempts = loginAttempts.filter(att => att.time > fifteenMinutesAgo);
      localStorage.setItem('login_attempts', JSON.stringify(loginAttempts));
      const failed = loginAttempts.filter(att => att.phone === phone).length;
      return failed >= 5;
    }

    function recordFailedAttempt(phone) {
      loginAttempts.push({ phone, time: Date.now() });
      localStorage.setItem('login_attempts', JSON.stringify(loginAttempts));
    }

    function handleLogin() {
      const phone = document.getElementById('loginPhone').value.trim();
      const pass = document.getElementById('loginPassword').value.trim();

      if (!phone || !pass) {
        alert("يرجى إدخال رقم الجوال وكلمة المرور.");
        return;
      }

      if (checkRateLimit(phone)) {
        alert("تم حظر محاولات الدخول مؤقتاً لتكرار الخطأ. يرجى الانتظار 15 دقيقة والمحاولة مجدداً.");
        return;
      }

      if (pass.length < 8) {
        alert("تنبيه: يجب ألا تقل كلمة المرور عن 8 أرقام أو حروف.");
        return;
      }

      if (phone === "0535050089") {
        if (pass === adminPassword) {
          currentUser = { name: "إدارة قلعة الأغذية", phone: phone, role: "admin" };
          loginAttempts = loginAttempts.filter(att => att.phone !== phone);
          localStorage.setItem('login_attempts', JSON.stringify(loginAttempts));
        } else {
          recordFailedAttempt(phone);
          alert("كلمة المرور غير صحيحة لحساب المدير.");
          return;
        }
      } else {
        currentUser = { name: "عميل", phone: phone, role: "customer", password: pass };
      }

      localStorage.setItem('store_user', JSON.stringify(currentUser));
      closeModal('loginModal');
      renderNav();
      renderAdminTable();
    }

    function handleChangePassword() {
      const oldPass = document.getElementById('oldPassword').value.trim();
      const newPass = document.getElementById('newPassword').value.trim();
      const confirmPass = document.getElementById('confirmPassword').value.trim();

      if (newPass.length < 8) {
        alert("كلمة المرور الجديدة يجب أن تحتوي على 8 أرقام أو حروف على الأقل.");
        return;
      }

      if (newPass !== confirmPass) {
        alert("كلمة المرور وتأكيدها غير متطابقين.");
        return;
      }

      if (currentUser.role === 'admin') {
        if (oldPass !== adminPassword) {
          alert("كلمة المرور الحالية غير صحيحة.");
          return;
        }
        adminPassword = newPass;
        localStorage.setItem('store_admin_pass', newPass);
        alert("تم تحديث كلمة مرور المدير بنجاح!");
      } else {
        currentUser.password = newPass;
        localStorage.setItem('store_user', JSON.stringify(currentUser));
        alert("تم تحديث كلمة المرور بنجاح!");
      }

      closeModal('changePassModal');
      document.getElementById('oldPassword').value = '';
      document.getElementById('newPassword').value = '';
      document.getElementById('confirmPassword').value = '';
    }

    function logout() {
      currentUser = null;
      localStorage.removeItem('store_user');
      renderNav();
    }

    function renderProducts() {
      const grid = document.getElementById('productGrid');
      const search = document.getElementById('searchInput').value.toLowerCase();
      grid.textContent = '';

      const filtered = products.filter(p => {
        const matchesCat = (selectedCat === 'all' || p.category === selectedCat);
        const matchesSearch = p.name.toLowerCase().includes(search);
        return matchesCat && matchesSearch;
      });

      if (filtered.length === 0) {
        const empty = document.createElement('div');
        empty.style.gridColumn = '1/-1';
        empty.style.textAlign = 'center';
        empty.style.color = 'var(--muted)';
        empty.style.padding = '20px';
        empty.textContent = 'لا توجد منتجات مطابقة للبحث';
        grid.appendChild(empty);
        return;
      }

      filtered.forEach(p => {
        const card = document.createElement('div');
        card.className = 'card';

        const top = document.createElement('div');
        const tag = document.createElement('div');
        tag.className = 'category-tag';
        tag.textContent = getCatName(p.category);

        const title = document.createElement('h3');
        title.textContent = p.name;

        const price = document.createElement('div');
        price.className = 'price';
        price.textContent = `${p.price.toFixed(2)} ر.س`;

        top.append(tag, title, price);

        const addBtn = document.createElement('button');
        addBtn.className = 'btn btn-primary';
        addBtn.textContent = '+ إضافة للسلة';
        addBtn.onclick = () => addToCart(p.id);

        card.append(top, addBtn);
        grid.appendChild(card);
      });
    }

    function getCatName(cat) {
      const map = { bakery: "مخبوزات", dairy: "ألبان", drinks: "مشروبات", pantry: "غذائيات" };
      return map[cat] || cat;
    }

    function setCategory(cat, btn) {
      selectedCat = cat;
      document.querySelectorAll('.cat-pill').forEach(b => b.classList.remove('active'));
      btn.classList.add('active');
      renderProducts();
    }

    function filterProducts() {
      renderProducts();
    }

    function renderAdminTable() {
      const tbody = document.getElementById('adminProductsTable');
      tbody.textContent = '';
      products.forEach(p => {
        const tr = document.createElement('tr');

        const tdName = document.createElement('td');
        tdName.textContent = p.name;

        const tdCat = document.createElement('td');
        tdCat.textContent = getCatName(p.category);

        const tdPrice = document.createElement('td');
        tdPrice.textContent = `${p.price.toFixed(2)} ر.س`;

        const tdAction = document.createElement('td');
        const delBtn = document.createElement('button');
        delBtn.className = 'btn btn-danger btn-sm';
        delBtn.textContent = 'حذف';
        delBtn.onclick = () => deleteProduct(p.id);
        tdAction.appendChild(delBtn);

        tr.append(tdName, tdCat, tdPrice, tdAction);
        tbody.appendChild(tr);
      });
    }

    function openAddProductModal() {
      document.getElementById('prodName').value = '';
      document.getElementById('prodPrice').value = '';
      openModal('productModal');
    }

    function saveProduct() {
      const name = document.getElementById('prodName').value.trim();
      const category = document.getElementById('prodCategory').value;
      const price = parseFloat(document.getElementById('prodPrice').value);

      if (!name || isNaN(price) || price <= 0) {
        alert("يرجى إدخال اسم وسعر صحيحين");
        return;
      }

      const newProduct = { id: Date.now(), name, category, price };
      products.unshift(newProduct);
      localStorage.setItem('store_products', JSON.stringify(products));
      renderProducts();
      renderAdminTable();
      closeModal('productModal');
    }

    function deleteProduct(id) {
      if (confirm("هل أنت متأكد من حذف هذا الصنف؟")) {
        products = products.filter(p => p.id !== id);
        delete cart[id];
        localStorage.setItem('store_products', JSON.stringify(products));
        renderProducts();
        renderAdminTable();
        updateCartUI();
      }
    }

    function addToCart(id) {
      cart[id] = (cart[id] || 0) + 1;
      updateCartUI();
    }

    function updateCartUI() {
      let count = 0;
      let total = 0;
      for (const id in cart) {
        const item = products.find(p => p.id == id);
        if (item) {
          count += cart[id];
          total += item.price * cart[id];
        }
      }
      document.getElementById('cartCount').textContent = count;
      document.getElementById('totalPrice').textContent = total.toFixed(2) + ' ر.س';
    }

    function openOrderModal() {
      if (Object.keys(cart).length === 0) {
        alert("السلة فارغة، اختر بعض الأصناف أولاً.");
        return;
      }
      const summaryDiv = document.getElementById('orderItemsSummary');
      summaryDiv.textContent = '';
      
      const title = document.createElement('b');
      title.textContent = 'الأصناف المطلوبة:';
      summaryDiv.appendChild(title);
      summaryDiv.appendChild(document.createElement('br'));

      for (const id in cart) {
        const item = products.find(p => p.id == id);
        if (item) {
          const row = document.createElement('div');
          row.textContent = `• ${item.name} × ${cart[id]}`;
          summaryDiv.appendChild(row);
        }
      }
      openModal('orderModal');
    }

    function sendWhatsAppOrder() {
      const name = document.getElementById('custName').value.trim();
      const address = document.getElementById('custAddress').value.trim();
      const notes = document.getElementById('custNotes').value.trim();

      if (!name || !address) {
        alert("يرجى كتابة الاسم والعنوان");
        return;
      }

      let text = `*طلب توصيل جديد - قلعة الأغذية*\n\n`;
      text += `👤 *العميل:* ${name}\n`;
      text += `📍 *العنوان:* ${address}\n\n`;
      text += `🛒 *الأصناف:*\n`;

      let total = 0;
      for (const id in cart) {
        const item = products.find(p => p.id == id);
        if (item) {
          const subtotal = item.price * cart[id];
          text += `• ${item.name} × ${cart[id]} = ${subtotal.toFixed(2)} ر.س\n`;
          total += subtotal;
        }
      }

      text += `\n💵 *الإجمالي المتوقع:* ${total.toFixed(2)} ر.س\n`;
      if (notes) text += `📝 *ملاحظات:* ${notes}\n`;

      const storePhone = "966535050089";
      window.open(`https://wa.me/${storePhone}?text=${encodeURIComponent(text)}`, '_blank');
      closeModal('orderModal');
    }

    function openModal(id) { document.getElementById(id).style.display = 'flex'; }
    function closeModal(id) { document.getElementById(id).style.display = 'none'; }

    init();
  </script>
</body>
</html>
