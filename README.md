<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <title>عناية الطفل</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <style>
    body { font-family: 'Cairo', Arial, sans-serif; background: #fafcff; margin: 0; padding: 0; }
    header { background: #8ecae6; color: #023047; padding: 30px 0 15px 0; text-align: center; position: relative; }
    .header-icons {
      position: absolute; right: 20px; top: 22px; display: flex; gap: 10px;
    }
    .header-icons img { width: 32px; height: 32px; background: #fff; border-radius: 50%; padding: 4px; transition: 0.2s; }
    .header-icons img:hover { opacity: 0.7; transform: scale(1.15); }
    nav { background: #219ebc; color: #fff; display: flex; justify-content: center; gap: 20px; padding: 10px 0; }
    nav a { color: #fff; text-decoration: none; font-size: 1.1em; }
    section { max-width: 900px; margin: 40px auto; background: #fff; border-radius: 12px; box-shadow: 0 2px 12px #e0e0e0; padding: 25px; }
    h2 { color: #219ebc; margin-bottom: 12px; }
    .products { display: flex; gap: 18px; flex-wrap: wrap; margin-top: 18px; }
    .product { background: #f3f7fa; border-radius: 10px; box-shadow: 0 1px 6px #e0e0e0; width: 210px; padding: 18px; text-align: center; }
    .product img { width: 100%; height: 120px; object-fit: cover; border-radius: 7px; }
    .product-name { font-size: 1.07em; margin: 8px 0; }
    .product-price { color: #43aa8b; font-weight: bold; }
    footer { background: #8ecae6; color: #023047; text-align: center; padding: 18px 0; margin-top: 40px; }
    #adminBtn { position: absolute; left: 20px; top: 20px; background: #219ebc; color: #fff; border: none; padding: 8px 18px; border-radius: 6px; cursor: pointer; }
    #adminModal { display: none; position: fixed; top: 0; right: 0; left: 0; bottom: 0; background: rgba(0,0,0,0.35); }
    #adminModal .modal-content { background: #fff; max-width: 340px; margin: 120px auto; padding: 26px; border-radius: 10px; text-align: center; }
    #adminPanel { display: none; background: #f7fbe7; border: 2px solid #b5d36e; border-radius: 12px; margin: 25px auto; max-width: 700px; padding: 23px; }
    #adminPanel input { margin: 5px; padding: 7px; border-radius: 5px; border: 1px solid #ccc; }
    #adminPanel button { background: #219ebc; color: #fff; border: none; padding: 8px 14px; border-radius: 6px; cursor: pointer; }
  </style>
</head>
<body>
  <header>
    <div class="header-icons">
      <a href="https://www.instagram.com/baby.careiq" target="_blank"><img src="https://cdn.jsdelivr.net/npm/simple-icons@v11/icons/instagram.svg" alt="Instagram"></a>
      <a href="https://wa.me/9647829215612" target="_blank"><img src="https://cdn.jsdelivr.net/npm/simple-icons@v11/icons/whatsapp.svg" alt="WhatsApp"></a>
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
      <input type="password" id="adminPassword" placeholder="كلمة المرور">
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
    <input id="newProductName" placeholder="اسم المنتج" />
    <input id="newProductPrice" type="number" placeholder="السعر بالدينار" />
    <input id="newProductImage" placeholder="رابط صورة المنتج" />
    <button onclick="addProduct()">➕ إضافة المنتج</button>
  </div>

  <section id="products">
    <h2>منتجات أطفال</h2>
    <div class="products" id="productsContainer"></div>
  </section>

  <footer>© 2025 عناية الطفل</footer>

<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/12.4.0/firebase-app.js";
  import { getFirestore, collection, addDoc, getDocs, deleteDoc, doc } from "https://www.gstatic.com/firebasejs/12.4.0/firebase-firestore.js";

  const firebaseConfig = {
    apiKey: "AIzaSyAWwb775H_z2ZASvPzpaLMIbVQIFhT_I48",
    authDomain: "baby-a0fa1.firebaseapp.com",
    projectId: "baby-a0fa1",
    storageBucket: "baby-a0fa1.firebasestorage.app",
    messagingSenderId: "80891249885",
    appId: "1:80891249885:web:5bfa8038a9951ce2138734",
    measurementId: "G-7TKLR7GCFJ"
  };

  const app = initializeApp(firebaseConfig);
  const db = getFirestore(app);

  async function loadProducts() {
    const container = document.getElementById("productsContainer");
    container.innerHTML = "";
    const querySnapshot = await getDocs(collection(db, "products"));
    querySnapshot.forEach((d) => {
      const data = d.data();
      const div = document.createElement("div");
      div.className = "product";
      div.innerHTML = `
        <img src="${data.image}" alt="${data.name}">
        <div class="product-name">${data.name}</div>
        <div class="product-price">${data.price} د.ع</div>
        <button onclick="deleteProduct('${d.id}')">🗑️ حذف</button>
      `;
      container.appendChild(div);
    });
  }

  window.addProduct = async function() {
    const name = document.getElementById("newProductName").value;
    const price = document.getElementById("newProductPrice").value;
    const image = document.getElementById("newProductImage").value;
    if (!name || !price || !image) return alert("الرجاء إدخال جميع الحقول");
    await addDoc(collection(db, "products"), { name, price, image });
    alert("✅ تم إضافة المنتج بنجاح");
    loadProducts();
  }

  window.deleteProduct = async function(id) {
    if (confirm("هل أنت متأكد من حذف هذا المنتج؟")) {
      await deleteDoc(doc(db, "products", id));
      loadProducts();
    }
  }

  // لوحة الإدارة
  window.openAdminModal = function() {
    document.getElementById("adminModal").style.display = "block";
  }

  window.closeAdminModal = function() {
    document.getElementById("adminModal").style.display = "none";
  }

  window.checkAdminPassword = function() {
    const pass = document.getElementById("adminPassword").value;
    if (pass === "2000nadin2006") {
      document.getElementById("adminPanel").style.display = "block";
      closeAdminModal();
    } else {
      document.getElementById("adminError").innerText = "كلمة المرور غير صحيحة!";
    }
  }

  loadProducts();
</script>
</body>
</html>
