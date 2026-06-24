<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Yun's Glow - Korean Makeup & Skincare</title>
    <style>
        /* --- RESET & GLOBAL STYLE --- */
        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; }
        body { background-color: #f9f9f9; color: #333; }
        a { text-decoration: none; color: inherit; }
        ul { list-style: none; }

        /* --- LOGIN MODAL --- */
        .modal-overlay {
            display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.6); z-index: 1000; justify-content: center; align-items: center;
        }
        .modal-box {
            background: #fff; padding: 30px; border-radius: 10px; width: 90%; max-width: 400px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.3); position: relative;
        }
        .modal-box h2 { text-align: center; margin-bottom: 20px; color: #e8aeb7; }
        .input-group { margin-bottom: 15px; }
        .input-group label { display: block; margin-bottom: 5px; font-size: 14px; font-weight: 600; }
        .input-group input {
            width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px; outline: none;
        }
        .btn-login {
            width: 100%; padding: 10px; background: #e8aeb7; color: white; border: none; border-radius: 5px;
            font-weight: bold; cursor: pointer; transition: 0.3s;
        }
        .btn-login:hover { background: #d4939c; }
        .close-modal {
            position: absolute; top: 15px; right: 20px; font-size: 24px; cursor: pointer; color: #888;
        }
        .login-error { color: red; text-align: center; margin-top: 10px; font-size: 14px; display: none; }

        /* --- HEADER & NAV --- */
        header { background: #fff; box-shadow: 0 2px 5px rgba(0,0,0,0.05); }
        .top-bar {
            display: flex; justify-content: flex-end; padding: 10px 20px; background: #f7f7f7;
            font-size: 13px; color: #555;
        }
        .top-bar span { margin-left: 15px; cursor: pointer; }
        .top-bar .login-btn { color: #e8aeb7; font-weight: bold; }

        .header-main {
            display: flex; justify-content: space-between; align-items: center; padding: 15px 20px;
            border-bottom: 1px solid #eee;
        }
        .logo { font-family: 'Brush Script MT', cursive; font-size: 32px; font-weight: bold; color: #e8aeb7; letter-spacing: 1px; }
        .search-cart { display: flex; align-items: center; gap: 15px; }
        .search-cart input {
            padding: 8px 12px; border: 1px solid #ddd; border-radius: 20px; font-size: 12px; width: 150px;
        }
        .nav-links {
            display: flex; justify-content: center; padding: 10px 0; background: #333; color: #fff;
            font-size: 11px; font-weight: 600; letter-spacing: 0.5px; flex-wrap: wrap;
        }
        .nav-links li { padding: 0 15px; cursor: pointer; }
        .nav-links li:hover { color: #e8aeb7; }

        /* --- BANNER --- */
        .banner-container {
            position: relative; width: 100%; max-width: 1200px; margin: 20px auto; padding: 0 15px;
        }
        .banner-img {
            width: 100%; height: auto; border-radius: 10px; display: block;
            background: linear-gradient(135deg, #ffecd2 0%, #fcb69f 100%);
            min-height: 250px; display: flex; justify-content: center; align-items: center; flex-direction: column;
            color: #555; text-align: center;
        }
        .banner-text h1 { font-size: 2.5rem; color: #c44569; font-family: 'Georgia', serif; margin: 0; }
        .banner-text h2 { font-size: 3.5rem; color: #c44569; font-family: 'Georgia', serif; margin: 0; line-height: 1; }
        .banner-text p { background: #e8aeb7; color: white; padding: 5px 15px; display: inline-block; border-radius: 20px; margin-top: 10px; font-weight: bold; font-size: 0.9rem; }

        /* --- PRODUCT SECTION --- */
        .section-title {
            text-align: center; margin: 40px 0 20px; position: relative; font-weight: bold; color: #333;
        }
        .section-title::after {
            content: ''; display: block; width: 60px; height: 2px; background: #e8aeb7; margin: 8px auto 0;
        }

        .product-grid {
            display: grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
            gap: 20px; max-width: 1200px; margin: 0 auto; padding: 0 15px 40px;
        }
        .product-card {
            background: #fff; border-radius: 10px; padding: 15px; text-align: center; box-shadow: 0 4px 10px rgba(0,0,0,0.05);
            transition: transform 0.3s;
        }
        .product-card:hover { transform: translateY(-5px); }
        
        .product-img {
            width: 100%; height: 180px; border-radius: 8px; margin-bottom: 10px;
            display: flex; justify-content: center; align-items: center;
            background-color: #f9f9f9;
            overflow: hidden;
        }
        .product-img img {
            width: 100%; height: 100%; object-fit: cover;
        }
        .product-img img.error { display: none; }
        .img-placeholder { font-size: 50px; }

        .product-title { font-size: 14px; font-weight: 600; margin-bottom: 5px; }
        .product-price { color: #e8aeb7; font-weight: bold; }

        /* --- FOOTER --- */
        footer {
            background: #222; color: #ccc; padding: 40px 20px; margin-top: 30px;
            text-align: center; border-top: 5px solid #e8aeb7;
        }
        .footer-content { max-width: 1200px; margin: 0 auto; display: grid; grid-template-columns: 1fr; gap: 20px; }
        @media(min-width: 600px){ .footer-content { grid-template-columns: 1fr 1fr; } }
        .footer-col h3 { color: #fff; margin-bottom: 15px; font-size: 18px; }
        .footer-col p { margin-bottom: 8px; font-size: 14px; }
        .footer-col i { margin-right: 8px; }

        @media (max-width: 600px) {
            .header-main { flex-direction: column; gap: 10px; }
            .search-cart input { width: 120px; }
            .banner-text h1 { font-size: 1.8rem; }
            .banner-text h2 { font-size: 2.5rem; }
        }
    </style>
</head>
<body>

    <!-- 1. LOGIN MODAL -->
    <div class="modal-overlay" id="loginModal">
        <div class="modal-box">
            <span class="close-modal" onclick="closeLogin()">&times;</span>
            <h2>Login Yun's Glow</h2>
            <form id="loginForm" onsubmit="handleLogin(event)">
                <div class="input-group">
                    <label>Email</label>
                    <input type="email" id="emailInput" placeholder="contoh: email@gmail.com" required>
                </div>
                <div class="input-group">
                    <label>Password</label>
                    <input type="password" id="passInput" placeholder="Masukkan password" required>
                </div>
                <button type="submit" class="btn-login">MASUK</button>
                <div id="loginError" class="login-error">Email atau Password salah!</div>
            </form>
            <p style="text-align: center; margin-top: 15px; font-size: 12px; color: #888;">
                *Coba: yunnss77@gmail.com / 666777
            </p>
        </div>
    </div>

    <!-- 2. HEADER -->
    <header>
        <div class="top-bar">
            <span class="login-btn" onclick="openLogin()">Login</span>
            <span>Register</span>
            <span>Cart (0)</span>
        </div>
        <div class="header-main">
            <div class="logo">Yun's Glow</div>
            <div class="search-cart">
                <input type="text" placeholder="Cari produk...">
                <span>🛒</span>
            </div>
        </div>
        <ul class="nav-links">
            <li>NEW ARRIVALS</li>
            <li>EYES</li>
            <li>LIPS</li>
            <li>FACE</li>
            <li>TOOLS</li>
            <li>BEAUTY & SKINCARE</li>
            <li>SALE</li>
        </ul>
    </header>

    <!-- 3. BANNER SECTION -->
    <div class="banner-container">
        <div class="banner-img">
            <div class="banner-text">
                <h1>NEW ARRIVALS</h1>
                <h2>KOREAN</h2>
                <h2>MAKE-UP & SKINCARE</h2>
                <p>SHOP NOW &rarr;</p>
            </div>
        </div>
    </div>

    <!-- 4. PRODUCT SECTION (GAMBAR PRODUK SAJA) -->
    <h3 class="section-title">NEW ARRIVALS</h3>
    <div class="product-grid">
        
        <!-- Produk 1: Lip Tint -->
        <div class="product-card">
            <div class="product-img">
                <img src="https://images.unsplash.com/photo-1598504775868-c4ebf95c4f24?auto=format&fit=crop&w=300&q=80" alt="Watery Lip Tint" onerror="this.style.display='none'">
                <span class="img-placeholder">💄</span>
            </div>
            <div class="product-title">Watery Lip Tint</div>
            <div class="product-price">Rp 85.000</div>
        </div>

        <!-- Produk 2: Eye Palette -->
        <div class="product-card">
            <div class="product-img">
                <img src="https://images.unsplash.com/photo-1596462502278-27bfdc403348?auto=format&fit=crop&w=300&q=80" alt="Nude Eye Palette" onerror="this.style.display='none'">
                <span class="img-placeholder">🎨</span>
            </div>
            <div class="product-title">Nude Eye Palette</div>
            <div class="product-price">Rp 150.000</div>
        </div>

        <!-- Produk 3: Sunscreen -->
        <div class="product-card">
            <div class="product-img">
                <img src="https://images.unsplash.com/photo-1556228578-0d85b1a4d571?auto=format&fit=crop&w=300&q=80" alt="UV Sunscreen" onerror="this.style.display='none'">
                <span class="img-placeholder">🧴</span>
            </div>
            <div class="product-title">UV Sunscreen SPF50</div>
            <div class="product-price">Rp 120.000</div>
        </div>

        <!-- Produk 4: Brush Set -->
        <div class="product-card">
            <div class="product-img">
                <img src="https://images.unsplash.com/photo-1522338242992-e1a54906a8da?auto=format&fit=crop&w=300&q=80" alt="Professional Brush" onerror="this.style.display='none'">
                <span class="img-placeholder">🖌️</span>
            </div>
            <div class="product-title">Professional Brush Set</div>
            <div class="product-price">Rp 200.000</div>
        </div>

    </div>

    <!-- 5. FOOTER -->
    <footer>
        <div class="footer-content">
            <div class="footer-col">
                <h3>Yun's Glow</h3>
                <p>💄 Korean Beauty & Skincare Authentic</p>
                <p>📍 Jl. Nigata Suyuk, Indonesia</p>
            </div>
            <div class="footer-col">
                <h3>Kontak Kami</h3>
                <p>📞 085107060972</p>
                <p>✉️ yunnss77@gmail.com</p>
            </div>
        </div>
        <p style="margin-top: 20px; font-size: 12px; color: #777;">&copy; 2026 Yun's Glow. All Rights Reserved.</p>
    </footer>

    <!-- 6. JAVASCRIPT LOGIC (SUDAH DIPERBAIKI) -->
    <script>
        // Ambil elemen HTML
        const modal = document.getElementById('loginModal');
        const errorMsg = document.getElementById('loginError');
        const loginForm = document.getElementById('loginForm');

        // Buka Modal Login
        function openLogin() {
            modal.style.display = 'flex';
            errorMsg.style.display = 'none'; // Sembunyikan pesan error saat pertama kali buka
            loginForm.reset(); // Kosongkan form
        }

        // Tutup Modal Login
        function closeLogin() {
            modal.style.display = 'none';
        }

        // Tutup modal jika user klik di area gelap luar modal
        window.onclick = function(event) {
            if (event.target == modal) {
                closeLogin();
            }
        }

        // FUNGSI LOGIN YANG SUDAH DIPERBAIKI
        function handleLogin(event) {
            event.preventDefault(); // PENTING: Ini mencegah halaman me-refresh saat tombol ditekan!
            
            // Ambil input user
            const email = document.getElementById('emailInput').value;
            const pass = document.getElementById('passInput').value;

            // Data login yang valid
            const validEmail = "yunnss77@gmail.com";
            const validPass = "666777";

            // Cek kecocokan
            if(email === validEmail && pass === validPass) {
                // Jika BENAR
                alert("Login Berhasil! Selamat datang di Yun's Glow.");
                closeLogin(); // Tutup modal
                
                // Ubah tulisan 'Login' di atas menjadi nama user
                const loginBtn = document.querySelector('.login-btn');
                loginBtn.innerText = "Halo, Yun's";
                loginBtn.style.cursor = "default";
                loginBtn.onclick = null; // Hilangkan fungsi klik setelah login
            } else {
                // Jika SALAH
                errorMsg.style.display = 'block'; // Tampilkan pesan error merah
            }
        }
    </script>

</body>
</html>
