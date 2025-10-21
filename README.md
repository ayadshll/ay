<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <title>عناية الطفل</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <style>
    body { font-family: 'Cairo', Arial, sans-serif; background: #fafcff; margin: 0; padding: 0; }
    header { background: #8ecae6; color: #023047; padding: 30px 0 15px 0; text-align: center; position: relative; z-index: 1001; } /* z-index added so header stays above admin panel content */
    .header-icons {
      position: absolute; right: 20px; top: 22px; display: flex; gap: 10px;
    }
    .header-icons a { display: inline-block; }
    .header-icons img { width: 32px; height: 32px; vertical-align: middle; transition: 0.2s; }
    .header-icons img:hover { opacity: 0.7; transform: scale(1.15);}
    nav { background: #219ebc; color: #fff; display: flex; justify-content: center; gap: 20px; padding: 10px 0; }
    nav a { color: #fff; text-decoration: none; font-size: 1.1em; }
    nav a:hover { text-decoration: underline; }
    section { max-width: 900px; margin: 40px auto; background: #fff; border-radius: 12px; box-shadow: 0 2px 12px #e0e0e0; padding: 25px; }
    h2 { color: #219ebc; margin-bottom: 12px; }
    ul, ol { margin-right: 30px; }
    .products { display: flex; gap: 18px; flex-wrap: wrap; margin-top: 18px; }
    .product { background: #f3f7fa; border-radius: 10px; box-shadow: 0 1px 6px #e0e0e0; width: 210px; padding: 18px; text-align: center; position: relative; }
    .product img { width: 100%; height: 120px; object-fit: cover; border-radius: 7px; }
    .product-name { font-size: 1.07em; margin: 8px 0; }
    .product-price { color: #43aa8b; font-weight: bold; }
    .product-controls { display: none; gap: 5px; justify-content: center; margin-top: 8px; }
    .product-controls.show { display: flex; }
    .btn-delete { background: #e63946; color: #fff; padding: 6px 12px; border-radius: 5px; border: none; cursor: pointer; font-size: 0.9em; }
    .btn-discount { background: #2a9d8f; color: #fff; padding: 6px 12px; border-radius: 5px; border: none; cursor: pointer; font-size: 0.9em; }
    .discount-box { margin-top: 7px; }
    .discount-box input { width: 60px; text-align: center; padding: 5px; border-radius: 5px; border: 1px solid #bbb; }
    .discount-box button { padding: 5px 13px; border-radius: 5px; border: none; background: #219ebc; color: #fff; cursor: pointer; margin-right: 5px; }
    .about-section { background: #f1f6fa; margin-bottom: 30px; }
    .about-section h2 { color: #126886; }
    footer { background: #8ecae6; color: #023047; text-align: center; padding: 18px 0; margin-top: 40px; }
    #adminBtn { position: absolute; left: 20px; top: 20px; background: #219ebc; color: #fff; border: none; padding: 8px 18px; border-radius: 6px; cursor: pointer; font-size: 1em; z-index: 1002; } /* ensure button is clickable above header elements */
    #adminBtn:hover { background: #126886; }
    #adminModal { display: none; position: fixed; top: 0; right: 0; left: 0; bottom: 0; background: rgba(0,0,0,0.35); z-index: 9999; }
    #adminModal .modal-content { background: #fff; max-width: 340px; margin: 120px auto; padding: 26px; border-radius: 10px; text-align: center; box-shadow: 0 3px 24px #bbb; }
    #adminModal input[type="password"] { padding: 8px; width: 80%; margin: 12px 0; border-radius: 5px; border: 1px solid #ccc; font-size: 1em; }
    #adminModal button { padding: 7px 18px; border-radius: 4px; border: none; background: #219ebc; color: #fff; cursor: pointer; font-size: 1em; }
    #adminPanel { display: none; background: #f7fbe7; border: 2px solid #b5d36e; border-radius: 12px; margin: 25px auto; max-width: 700px; padding: 23px; position: relative; z-index: 1; } /* keep panel below header visually */
    #adminPanel h3 { color: #628900; }
    .admin-actions { margin-top: 15px; }
    .admin-actions input, .admin-actions button { margin: 3px 6px; }
    @media (max-width: 600px) {
      section { padding: 12px; }
      .products { flex-direction: column; align-items: center; }
      .product { width: 90%; }
      #adminPanel { padding: 10px; }
      .header-icons { position: static; justify-content: center; margin-bottom: 7px; } /* keep icons in flow on small screens */
      /* Make admin button flow with header on small screens instead of absolute positioning,
         this prevents it from overlapping the icons */
      #adminBtn {
        position: static;
        left: auto;
        top: auto;
        display: inline-block;
        margin: 8px auto 0;
        transform: none;
      }
      /* Give header content natural vertical order and spacing */
      header { padding: 18px 12px; }
    }
  </style>
</head>
<body>
  <header>
    <div class="header-icons">
      <!-- Instagram Icon -->
      <a href="https://www.instagram.com/baby.careiq?igsh=ZGphNjdidXE2ZXVq" target="_blank" title="انستغرام">
        <img src="https://cdn.jsdelivr.net/npm/simple-icons@v11/icons/instagram.svg" alt="Instagram" style="background:#fff;border-radius:50%;padding:4px;">
      </a>
      <!-- WhatsApp Icon -->
      <a href="https://wa.me/9647829215612" target="_blank" title="واتساب">
        <img src="https://cdn.jsdelivr.net/npm/simple-icons@v11/icons/whatsapp.svg" alt="WhatsApp" style="background:#fff;border-radius:50%;padding:4px;">
      </a>
    </div>
    <h1>عناية الطفل</h1>
    <button id="adminBtn" onclick="openAdminModal()">لوحة الإدارة</button>
    <p>نصائح ومنتجات تساعد الآباء والأمهات في رعاية أطفالهم</p>
  </header>
  <nav>
    <a href="#tips">نصائح العناية</a>
    <a href="#products">منتجات أطفال</a>
    <a href="#about">من نحن</a>
  </nav>

  <!-- Admin Modal -->
  <div id="adminModal">
    <div class="modal-content">
      <h3>تسجيل دخول المدير</h3>
      <input type="password" id="adminPassword" placeholder="أدخل كلمة المرور">
      <div>
        <button onclick="checkAdminPassword()">دخول</button>
        <button onclick="closeAdminModal()">إلغاء</button>
      </div>
      <div id="adminError" style="color: red; margin-top: 10px;"></div>
    </div>
  </div>

  <!-- Admin Panel -->
  <div id="adminPanel">
    <h3>لوحة تحكم المدير</h3>
    <div>مرحباً بك في لوحة الإدارة! يمكنك هنا إضافة منتجات جديدة وحذف أو خصم المنتجات.</div>
    <div class="admin-actions">
      <input id="newProductName" placeholder="اسم المنتج" />
      <input id="newProductPrice" placeholder="السعر بالدينار العراقي" type="number" min="0" />
      <input id="newProductImage" placeholder="رابط صورة المنتج (مثال: https://...)" />
      <button onclick="addProduct()">إضافة المنتج</button>
    </div>
    <div id="adminSuccess" style="color: green; margin-top: 10px;"></div>
    <div style="text-align:left;">
      <button onclick="closeAdminPanel()" style="background:#e63946;color:#fff;padding:7px 18px;border-radius:5px;border:none;cursor:pointer;margin-top:6px;">خروج من لوحة الإدارة</button>
    </div>
  </div>

  <section id="tips">
    <h2>نصائح العناية بالأطفال</h2>
    <ul>
      <li>احرص على رضاعة الطفل بشكل منتظم ونظيف.</li>
      <li>تغيير الحفاضات فور اتساخها للحفاظ على صحة الجلد.</li>
      <li>تدفئة الطفل جيدًا والحرص على نظافة ملابسه.</li>
      <li>مراقبة درجة حرارة الطفل باستمرار.</li>
      <li>زيارة الطبيب بشكل دوري لمتابعة نمو الطفل.</li>
    </ul>
  </section>
  <section id="products">
    <h2>منتجات أطفال مقترحة</h2>
    <div class="products" id="productsList">
      <!-- المنتجات ستظهر هنا -->
    </div>
  </section>

  <section id="about" class="about-section">
    <h2>من نحن</h2>
    <p>
      <strong>متجر عناية الطفل</strong> وجهتك الأولى لمنتجات ونصائح رعاية الأطفال!  
      نحن متجر متخصص في توفير أفضل المنتجات الأساسية للأطفال، من حفاضات وحليب إلى مستلزمات العناية والنظافة، مع فريق يهتم بجودة ما نقدمه لضمان سلامة وراحة طفلك.
      نسعى لتوفير تجربة تسوق سهلة وآمنة لكل الأمهات والآباء، مع نصائح عملية ودعم مستمر.  
      هدفنا أن يحصل طفلك على كل ما يحتاجه لينمو بصحة وسعادة.
      <br><br>
      شكراً لاختيارك متجر عناية الطفل، لأن صحة وسلامة طفلك هي أولويتنا دائماً.
    </p>
  </section>

  <footer>
    &copy; 2025 عناية الطفل | جميع الحقوق محفوظة
  </footer>

  <script>
    const ADMIN_PASSWORD = "2000blal2006";
    let adminMode = false;

    function openAdminModal() {
      document.getElementById('adminModal').style.display = 'block';
      document.getElementById('adminPassword').focus();
      document.getElementById('adminPassword').value = '';
      document.getElementById('adminError').textContent = '';
    }
    function closeAdminModal() {
      document.getElementById('adminModal').style.display = 'none';
      document.getElementById('adminPassword').value = '';
      document.getElementById('adminError').textContent = '';
    }
    function checkAdminPassword() {
      const pwd = document.getElementById('adminPassword').value;
      if (pwd === ADMIN_PASSWORD) {
        closeAdminModal();
        showAdminPanel();
      } else {
        document.getElementById('adminError').textContent = 'كلمة المرور غير صحيحة!';
      }
    }
    function showAdminPanel() {
      document.getElementById('adminPanel').style.display = 'block';
      adminMode = true;
      showAdminControls();
      window.scrollTo({ top: 0, behavior: 'smooth' });
    }
    function closeAdminPanel() {
      document.getElementById('adminPanel').style.display = 'none';
      adminMode = false;
      hideAdminControls();
    }
    function showAdminControls() {
      const controls = document.querySelectorAll('.product-controls');
      controls.forEach(e => e.classList.add('show'));
    }
    function hideAdminControls() {
      const controls = document.querySelectorAll('.product-controls');
      controls.forEach(e => e.classList.remove('show'));
      document.querySelectorAll('.discount-box').forEach(box => box.remove());
    }
    function addProduct() {
      const name = document.getElementById('newProductName').value.trim();
      const price = document.getElementById('newProductPrice').value.trim();
      const img = document.getElementById('newProductImage').value.trim();
      const defaultImg = "https://via.placeholder.com/210x120?text=منتج+جديد";
      if (name && price) {
        const productsList = document.getElementById('productsList');
        const div = document.createElement('div');
        div.className = 'product';
        div.innerHTML = `
          <img src="${img || defaultImg}" alt="${name}" onerror="this.src='${defaultImg}'">
          <div class="product-name">${name}</div>
          <div class="product-price">${parseInt(price).toLocaleString()} دينار عراقي</div>
          <div class="product-controls${adminMode ? ' show' : ''}">
            <button class="btn-delete" onclick="deleteProduct(this)">حذف</button>
            <button class="btn-discount" onclick="discountProduct(this)">خصم</button>
          </div>
        `;
        productsList.appendChild(div);
        document.getElementById('adminSuccess').textContent = 'تمت إضافة المنتج بنجاح!';
        document.getElementById('newProductName').value = '';
        document.getElementById('newProductPrice').value = '';
        document.getElementById('newProductImage').value = '';
        setTimeout(() => { document.getElementById('adminSuccess').textContent = ''; }, 2000);
      }
    }
    function deleteProduct(btn) {
      var productDiv = btn.closest('.product');
      if (confirm('هل أنت متأكد من حذف هذا المنتج؟')) {
        productDiv.remove();
      }
    }
    function discountProduct(btn) {
      const productDiv = btn.closest('.product');
      if (productDiv.querySelector('.discount-box')) return;
      const discountBox = document.createElement('div');
      discountBox.className = 'discount-box';
      discountBox.innerHTML = `
        <input type="number" min="1" max="100" value="10" id="discountInput" placeholder="نسبة الخصم">
        <button onclick="applyDiscount(this)">تطبيق الخصم</button>
      `;
      btn.parentElement.appendChild(discountBox);
    }
    function applyDiscount(applyBtn) {
      const discountBox = applyBtn.parentElement;
      const productDiv = discountBox.closest('.product');
      const priceDiv = productDiv.querySelector('.product-price');
      let priceText = priceDiv.textContent.replace(/[^\d]/g, '');
      let price = parseInt(priceText);
      const percentInput = discountBox.querySelector('input');
      let percent = parseInt(percentInput.value);
      if (!isNaN(price) && !isNaN(percent) && percent > 0 && percent <= 100) {
        let discounted = Math.round(price * (1 - percent / 100));
        priceDiv.textContent = discounted.toLocaleString() + ' دينار عراقي (بعد الخصم ' + percent + '%)';
        productDiv.querySelector('.btn-discount').disabled = true;
        productDiv.querySelector('.btn-discount').textContent = 'تم الخصم';
        productDiv.querySelector('.btn-discount').style.background = '#aaa';
        discountBox.remove();
      }
    }
    window.onclick = function(event) {
      var modal = document.getElementById('adminModal');
      if (event.target == modal) {
        closeAdminModal();
      }
    }
    document.addEventListener('keydown', function(e){
      if(document.getElementById('adminModal').style.display === 'block') {
        if (e.key === 'Enter') checkAdminPassword();
        if (e.key === 'Escape') closeAdminModal();
      }
    });
  </script>
</body>
</html>
