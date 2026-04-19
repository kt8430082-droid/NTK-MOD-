<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>NTK MOD FFxLQ • AI Admin + Tạo Game</title>
  <!-- Font Awesome & Google Fonts -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
  <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body {
      background: #0B0C10;
      color: #fff;
      font-family: 'Plus Jakarta Sans', sans-serif;
      background-image: radial-gradient(circle at 20% 30%, #1A0B2E 0%, #0B0C10 90%);
      min-height: 100vh;
      line-height: 1.4;
      font-size: 0.9rem;
    }
    .container { max-width: 1440px; margin: 0 auto; padding: 20px 28px; }

    /* === Sidebar === */
    .sidebar {
      position: fixed; top: 0; left: -300px; width: 280px; height: 100%;
      background: rgba(15, 10, 25, 0.95); backdrop-filter: blur(30px);
      border-right: 2px solid #9D4EDD; z-index: 1000;
      transition: left 0.35s ease; padding: 30px 20px;
      box-shadow: 20px 0 50px rgba(157, 78, 221, 0.2);
      border-radius: 0 40px 40px 0;
    }
    .sidebar.active { left: 0; }
    .sidebar-header { display: flex; align-items: center; gap: 12px; margin-bottom: 30px; border-bottom: 1px solid #9D4EDD; padding-bottom: 20px; }
    .sidebar-header i { font-size: 28px; color: #C084FC; }
    .sidebar-header h3 { font-size: 1.6rem; font-weight: 700; background: linear-gradient(135deg, #E9D5FF, #fff); -webkit-background-clip: text; background-clip: text; color: transparent; }
    .menu-items { list-style: none; }
    .menu-item {
      display: flex; align-items: center; gap: 14px; padding: 12px 20px;
      border-radius: 40px; background: rgba(45, 35, 70, 0.4);
      border: 1px solid #6B21A8; margin-bottom: 10px;
      color: #DDD0FF; font-weight: 600; font-size: 1rem;
      cursor: pointer; transition: all 0.2s;
    }
    .menu-item i { width: 22px; color: #A78BFA; font-size: 1.1rem; }
    .menu-item:hover { background: #9D4EDD; color: white; border-color: #C084FC; transform: scale(1.02); }
    .overlay { position: fixed; inset: 0; background: rgba(0,0,0,0.6); backdrop-filter: blur(8px); z-index: 999; display: none; }
    .overlay.active { display: block; }

    /* === Header === */
    header {
      display: flex; align-items: center; justify-content: space-between; flex-wrap: wrap;
      gap: 16px; margin-bottom: 24px; padding-bottom: 18px;
      border-bottom: 1px solid rgba(157, 78, 221, 0.3);
    }
    .header-left { display: flex; align-items: center; gap: 16px; }
    .hamburger {
      background: #1E1730; border: 2px solid #9D4EDD; width: 46px; height: 46px;
      border-radius: 16px; display: flex; align-items: center; justify-content: center;
      font-size: 22px; color: #D8B4FE; cursor: pointer; transition: 0.2s;
    }
    .hamburger:hover { background: #9D4EDD; color: white; }
    .logo-area { display: flex; align-items: center; gap: 12px; }
    .logo-icon {
      background: linear-gradient(145deg, #9D4EDD, #6B21A8); width: 48px; height: 48px;
      border-radius: 18px; display: flex; align-items: center; justify-content: center;
      font-size: 26px; box-shadow: 0 8px 20px rgba(157, 78, 221, 0.5);
      animation: pulseGlow 2.5s infinite;
    }
    @keyframes pulseGlow {
      0% { box-shadow: 0 0 10px #9D4EDD; }
      50% { box-shadow: 0 0 30px #C084FC; }
      100% { box-shadow: 0 0 10px #9D4EDD; }
    }
    .logo-text h1 { font-size: 1.8rem; font-weight: 800; background: linear-gradient(135deg, #F0E6FF, #fff); -webkit-background-clip: text; background-clip: text; color: transparent; }
    .logo-text span { font-size: 0.8rem; color: #B39DDB; letter-spacing: 2px; }
    .header-right { display: flex; align-items: center; gap: 16px; }
    .search-box {
      background: #1E1730; padding: 10px 20px; border-radius: 50px;
      display: flex; align-items: center; border: 2px solid #6B21A8; min-width: 260px;
    }
    .search-box i { color: #C084FC; margin-right: 12px; font-size: 1rem; }
    .search-box input { background: transparent; border: none; color: white; outline: none; width: 100%; font-size: 0.9rem; }
    .user-area {
      display: flex; align-items: center; gap: 12px; background: #1E1730;
      padding: 4px 16px 4px 12px; border-radius: 50px; border: 2px solid #9D4EDD;
    }
    .user-avatar { width: 34px; height: 34px; background: #9D4EDD; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-weight: 700; color: white; font-size: 0.9rem; }
    .user-name { font-weight: 600; font-size: 0.9rem; }
    .balance {
      background: linear-gradient(145deg, #FFD966, #FBBF24); color: #0B0C10;
      padding: 4px 14px; border-radius: 50px; font-weight: 800; font-size: 0.8rem;
      border: 1px solid #FDE68A;
    }
    .logout-btn {
      background: transparent; border: 1.5px solid #EF4444; color: #EF4444;
      padding: 4px 12px; border-radius: 40px; font-size: 0.75rem; margin-left: 5px; cursor: pointer;
    }

    /* === Hero === */
    .hero {
      background: rgba(20, 12, 35, 0.6); backdrop-filter: blur(16px);
      border: 1.5px solid #9D4EDD; border-radius: 40px; padding: 30px 35px;
      margin-bottom: 30px; display: flex; flex-wrap: wrap; align-items: center; justify-content: space-between;
    }
    .welcome h2 { font-size: 2.2rem; font-weight: 700; background: linear-gradient(135deg, #F0E6FF, #fff); -webkit-background-clip: text; background-clip: text; color: transparent; }
    .welcome p { color: #C4B5FD; margin-top: 6px; font-size: 0.95rem; }
    .stats { display: flex; gap: 40px; }
    .stat-item { text-align: center; }
    .stat-num { font-size: 2rem; font-weight: 800; color: #FBBF24; }
    .stat-label { color: #A78BFA; font-size: 0.85rem; }
    .hero-buttons { display: flex; gap: 15px; margin-top: 20px; }
    .btn-primary {
      background: linear-gradient(145deg, #9D4EDD, #6B21A8); padding: 12px 28px;
      border-radius: 50px; color: white; font-weight: 700; text-decoration: none;
      border: 1px solid #C084FC; font-size: 0.95rem; transition: 0.2s;
    }
    .btn-primary:hover { box-shadow: 0 0 25px #9D4EDD; }
    .btn-outline {
      background: transparent; border: 2px solid #00F0FF; padding: 12px 28px;
      border-radius: 50px; color: white; text-decoration: none; font-weight: 700; font-size: 0.95rem;
    }

    /* === Sections === */
    .section-title { font-size: 1.8rem; font-weight: 700; margin: 40px 0 20px; display: flex; align-items: center; gap: 12px; }
    .key-card {
      background: rgba(20, 12, 35, 0.7); backdrop-filter: blur(12px);
      border: 2px solid #FBBF24; border-radius: 35px; padding: 28px 35px;
      display: flex; flex-wrap: wrap; align-items: center; justify-content: space-between;
    }
    .key-info h3 { color: #FCD34D; font-size: 1.5rem; }
    .key-code {
      background: #1E1730; padding: 14px 24px; border-radius: 50px;
      font-family: monospace; font-size: 1.8rem; font-weight: 700; letter-spacing: 3px;
      border: 1px solid #F59E0B; color: #FDE68A;
    }
    .key-timer { font-size: 2rem; font-weight: 800; color: #F87171; }

    /* Mods */
    .filter-bar { display: flex; gap: 12px; margin-bottom: 20px; }
    .filter-btn {
      background: #1E1730; border: 2px solid #6B21A8; padding: 10px 24px;
      border-radius: 50px; color: #CBD5E1; font-weight: 700; font-size: 0.85rem; cursor: pointer;
    }
    .filter-btn.active { background: #9D4EDD; color: white; border-color: #C084FC; }
    .mod-list { display: grid; gap: 16px; }
    .mod-item {
      background: rgba(20, 15, 35, 0.8); backdrop-filter: blur(10px);
      border: 1.5px solid #6B21A8; border-radius: 35px; padding: 18px 24px;
      display: flex; align-items: center; justify-content: space-between; flex-wrap: wrap;
    }
    .mod-item.maintenance { opacity: 0.7; border-color: #F59E0B; }
    .mod-info h4 { font-size: 1.2rem; font-weight: 700; }
    .mod-meta { color: #B39DDB; font-size: 0.85rem; }
    .status-badge { padding: 5px 16px; border-radius: 30px; font-size: 0.75rem; font-weight: 700; text-transform: uppercase; }
    .status-online { background: #14532D; color: #86EFAC; border: 1px solid #22C55E; }
    .status-maintenance { background: #78350F; color: #FDE68A; border: 1px solid #F59E0B; }
    .btn-download {
      background: linear-gradient(145deg, #7E22CE, #4C1D95); padding: 10px 24px;
      border-radius: 50px; color: white; text-decoration: none; font-weight: 700;
      border: 1px solid #A855F7; font-size: 0.85rem;
    }

    /* FAQ */
    .faq-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 20px; margin: 20px 0 40px; }
    .faq-item {
      background: #131022; border: 1.5px solid #6B21A8; border-radius: 30px;
      padding: 18px 24px; cursor: pointer;
    }
    .faq-question { font-weight: 700; font-size: 1rem; display: flex; justify-content: space-between; }
    .faq-answer { margin-top: 14px; color: #C4B5FD; display: none; font-size: 0.9rem; }
    .faq-item.active .faq-answer { display: block; }

    /* Contact */
    .contact-section {
      background: #0F0B1A; border-radius: 45px; padding: 30px; margin: 30px 0;
      border: 2px solid #9D4EDD;
    }
    .contact-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 20px; }
    .contact-item {
      display: flex; align-items: center; gap: 14px; background: #1E1730;
      padding: 16px 20px; border-radius: 40px; border: 2px solid #6B21A8; font-size: 0.9rem;
    }
    .maintenance-tag { margin-left: auto; background: #78350F; color: #FDE68A; padding: 4px 12px; border-radius: 30px; font-weight: 700; font-size: 0.75rem; }
    .copy-btn { margin-left: auto; background: #2E1A4A; border: none; color: white; padding: 8px 18px; border-radius: 30px; cursor: pointer; font-weight: 600; font-size: 0.8rem; }

    /* Modals */
    .modal-overlay { position: fixed; inset: 0; background: rgba(0,0,0,0.7); backdrop-filter: blur(15px); display: none; align-items: center; justify-content: center; z-index: 2000; }
    .modal-card {
      background: rgba(18, 12, 30, 0.95); backdrop-filter: blur(25px);
      border: 3px solid #9D4EDD; border-radius: 50px; padding: 30px;
      max-width: 600px; width: 95%; box-shadow: 0 40px 80px rgba(0,0,0,0.8);
      max-height: 85vh; overflow-y: auto;
    }
    .modal-title { font-size: 1.8rem; font-weight: 700; margin-bottom: 25px; background: linear-gradient(135deg, #F0E6FF, #fff); -webkit-background-clip: text; background-clip: text; color: transparent; }
    .modal-input, .modal-select, .modal-textarea {
      width: 100%; padding: 14px 20px; border-radius: 30px; background: #1E1730;
      border: 2px solid #9D4EDD; color: white; font-size: 0.95rem; margin-bottom: 16px; outline: none;
    }
    .modal-textarea {
      min-height: 300px;
      font-family: 'Courier New', monospace;
      resize: vertical;
    }
    .modal-btn {
      background: linear-gradient(145deg, #9D4EDD, #6B21A8); border: none; color: white;
      padding: 14px; border-radius: 50px; font-weight: 700; font-size: 1rem;
      width: 100%; cursor: pointer; border: 1px solid #C084FC; margin-bottom: 10px;
    }
    .tab-buttons { display: flex; gap: 10px; margin-bottom: 20px; }
    .tab-btn {
      flex: 1; background: #1E1730; border: 2px solid #6B21A8; padding: 10px;
      border-radius: 50px; font-weight: 700; color: #CBD5E1; cursor: pointer; text-align: center; font-size: 0.9rem;
    }
    .tab-btn.active { background: #9D4EDD; color: white; border-color: #C084FC; }
    .shop-pack {
      background: #1E1730; border-radius: 30px; padding: 20px; margin-bottom: 16px;
      display: flex; align-items: center; justify-content: space-between;
      border: 2px solid #FBBF24;
    }
    .shop-pack h4 { font-size: 1.2rem; }
    .btn-buy { background: #F59E0B; border: none; padding: 10px 24px; border-radius: 50px; font-weight: 800; cursor: pointer; font-size: 0.9rem; }

    /* Admin Panel */
    .admin-mod-item {
      background: #1A1330; padding: 16px; border-radius: 25px; margin-bottom: 16px;
      border: 1px solid #A855F7;
    }
    .admin-mod-item input, .admin-mod-item select {
      background: #2A1E40; border: 2px solid #A855F7; color: white; padding: 8px 12px;
      border-radius: 40px; margin-right: 8px; margin-bottom: 8px; font-size: 0.85rem;
    }

    /* Preview iframe */
    .game-preview {
      margin-top: 15px;
      border: 2px solid #9D4EDD;
      border-radius: 20px;
      overflow: hidden;
      background: #fff;
    }
    .game-preview iframe {
      width: 100%;
      height: 300px;
      border: none;
    }
  </style>
</head>
<body>
<div class="overlay" id="overlay"></div>
<div class="sidebar" id="sidebar">
  <div class="sidebar-header"><i class="fas fa-bars"></i><h3>NTK MOD</h3></div>
  <ul class="menu-items" id="sidebarMenu">
    <li class="menu-item" data-action="home"><i class="fas fa-home"></i> Trang chủ</li>
    <li class="menu-item" data-action="search"><i class="fas fa-search"></i> Tìm kiếm</li>
    <li class="menu-item" data-action="shop"><i class="fas fa-shopping-cart"></i> Mua Key</li>
    <li class="menu-item" data-action="recharge"><i class="fas fa-wallet"></i> Nạp Xu</li>
    <li class="menu-item" data-action="account"><i class="fas fa-user-circle"></i> Tài khoản</li>
  </ul>
</div>

<div class="container">
  <!-- HEADER -->
  <header>
    <div class="header-left">
      <div class="hamburger" id="menuToggle"><i class="fas fa-bars"></i></div>
      <div class="logo-area">
        <div class="logo-icon"><i class="fas fa-gamepad"></i></div>
        <div class="logo-text"><h1>NTK MOD FFxLQ</h1><span>AI POWERED</span></div>
      </div>
    </div>
    <div class="header-right">
      <div class="search-box"><i class="fas fa-search"></i><input type="text" placeholder="Tìm mod..." id="searchInput"></div>
      <div id="userWidget"></div>
    </div>
  </header>

  <!-- HERO -->
  <div class="hero">
    <div>
      <div class="welcome"><h2>WELCOME TO</h2><h2 style="font-size:2.8rem;">NTK Mods</h2><p>Hỗ Trợ Mod Game Cao Cấp • AI Tự Động</p></div>
      <div class="hero-buttons">
        <a href="#" class="btn-primary"><i class="fas fa-download"></i> Tải App</a>
        <a href="#" class="btn-outline"><i class="fas fa-robot"></i> AI Key</a>
      </div>
    </div>
    <div class="stats">
      <div class="stat-item"><div class="stat-num" id="totalDownloads">3.2K+</div><div class="stat-label">Lượt Tải</div></div>
      <div class="stat-item"><div class="stat-num">2.1K+</div><div class="stat-label">Thành Viên</div></div>
      <div class="stat-item"><div class="stat-num">99.9%</div><div class="stat-label">Uptime</div></div>
    </div>
  </div>

  <!-- KEY CỦA BẠN (AI) -->
  <div class="section-title"><i class="fas fa-robot" style="color:#00F0FF;"></i> AI KEY CỦA BẠN</div>
  <div class="key-card" id="userKeyArea"></div>

  <!-- DANH SÁCH MOD -->
  <div class="section-title"><i class="fas fa-gamepad"></i> KHO MOD</div>
  <div class="filter-bar">
    <button class="filter-btn active" data-filter="all">TẤT CẢ</button>
    <button class="filter-btn" data-filter="online">ONLINE <span id="onlineCount">4</span></button>
    <button class="filter-btn" data-filter="maintenance">BẢO TRÌ <span id="maintCount">0</span></button>
  </div>
  <div class="mod-list" id="modListContainer"></div>

  <!-- FAQ -->
  <div class="section-title"><i class="fas fa-question-circle"></i> HỎI ĐÁP</div>
  <div class="faq-grid">
    <div class="faq-item"><div class="faq-question"><span>Cách tải game?</span><i class="fas fa-chevron-down"></i></div><div class="faq-answer">Chọn phiên bản và nhấn Tải.</div></div>
    <div class="faq-item"><div class="faq-question"><span>Key dùng bao lâu?</span><i class="fas fa-chevron-down"></i></div><div class="faq-answer">24h hoặc 7 ngày.</div></div>
    <div class="faq-item"><div class="faq-question"><span>Làm sao mua key?</span><i class="fas fa-chevron-down"></i></div><div class="faq-answer">Vào Mua Key trong menu.</div></div>
    <div class="faq-item"><div class="faq-question"><span>Hỗ trợ?</span><i class="fas fa-chevron-down"></i></div><div class="faq-answer">Zalo: 0865729532.</div></div>
  </div>

  <!-- FOOTER -->
  <div class="contact-section">
    <div style="display:flex; justify-content:space-between; margin-bottom:25px;"><h3 style="font-size:1.8rem;"><i class="fas fa-headset"></i> Liên hệ</h3><span style="color:#4ADE80;"><i class="fas fa-circle"></i> Online 24/7</span></div>
    <div class="contact-grid">
      <div class="contact-item"><i class="fab fa-telegram"></i> Telegram <span class="maintenance-tag">Bảo trì</span></div>
      <div class="contact-item"><i class="fab fa-youtube"></i> YouTube <span class="maintenance-tag">Bảo trì</span></div>
      <div class="contact-item" style="grid-column: span 2;"><i class="fab fa-facebook-messenger"></i> Zalo: <strong>0865729532</strong> <button class="copy-btn" onclick="copyText('0865729532')">COPY</button></div>
    </div>
  </div>
</div>

<!-- MODALS -->
<div class="modal-overlay" id="shopModal"> <div class="modal-card"><div class="modal-title">🛒 Mua Key</div><div id="shopContent"></div><button class="modal-btn" style="background:#1E1730;" id="closeShopBtn">Đóng</button></div> </div>
<div class="modal-overlay" id="rechargeModal"> <div class="modal-card"><div class="modal-title">💎 Nạp Xu</div><div class="tab-buttons"><div class="tab-btn active" data-recharge-tab="qr">QR</div><div class="tab-btn" data-recharge-tab="card">Thẻ cào</div><div class="tab-btn" data-recharge-tab="bank">Ngân hàng</div></div><div id="rechargeQR"><div style="text-align:center; margin:20px 0;"><canvas id="qrCanvas"></canvas></div><input type="number" class="modal-input" placeholder="Số tiền" id="amountQR" value="100000"><button class="modal-btn" style="background:#F59E0B;" id="confirmQrBtn">Nạp QR</button></div><div id="rechargeCard" style="display:none;"><select class="modal-input" id="cardType"><option>Viettel</option><option>Mobifone</option><option>Vinaphone</option></select><input class="modal-input" placeholder="Mã thẻ" id="cardCode"><input class="modal-input" placeholder="Seri" id="cardSerial"><button class="modal-btn" style="background:#0EA5E9;" id="cardSubmitBtn">Nạp thẻ</button></div><div id="rechargeBank" style="display:none;"><select class="modal-input" id="bankName"><option>Vietcombank</option><option>BIDV</option></select><input class="modal-input" placeholder="Số TK" id="bankAccount"><input class="modal-input" placeholder="Số tiền" id="bankAmount"><button class="modal-btn" style="background:#10B981;" id="bankSubmitBtn">Chuyển khoản</button></div><button class="modal-btn" style="margin-top:20px; background:#4C1D95;" id="closeRechargeBtn">Đóng</button></div> </div>
<div class="modal-overlay" id="authModal"> <div class="modal-card"><div class="modal-title">👤 Đăng nhập</div><input class="modal-input" placeholder="Tên đăng nhập" id="loginUsername" value="ntkmod"><input class="modal-input" type="password" placeholder="Mật khẩu" id="loginPassword" value="123456"><button class="modal-btn" id="loginBtn">Đăng nhập</button><p style="color:#C084FC;">Demo: ntkmod/123456 | Admin: admin/admin123 | Phó Admin: subadmin/sub123</p><button class="modal-btn" style="background:#1E1730;" id="closeAuthBtn">Đóng</button></div> </div>
<div class="modal-overlay" id="adminModal"> <div class="modal-card" style="max-width:800px;"><div class="modal-title">⚙️ Admin Panel</div><div id="adminModsList"></div><button class="modal-btn" id="addNewModBtn"><i class="fas fa-plus"></i> Thêm Mod</button><button class="modal-btn" style="background:#F59E0B;" id="saveAdminChanges">Lưu & Cập nhật Web</button><button class="modal-btn" style="background:#1E1730;" id="closeAdminBtn">Đóng</button></div> </div>
<!-- MODAL TẠO GAME -->
<div class="modal-overlay" id="createGameModal">
  <div class="modal-card" style="max-width:900px;">
    <div class="modal-title"><i class="fas fa-code"></i> Tạo Game Riêng</div>
    <p style="margin-bottom:10px; color:#C4B5FD;">Dán code HTML/CSS/JS của bạn vào bên dưới</p>
    <textarea id="gameCode" class="modal-textarea" placeholder="<html>..."><html><head><style>body{background:#111;color:lime;font-family:monospace;padding:20px;}</style></head><body><h1>Game của bạn</h1><canvas id='gameCanvas' width='400' height='300'></canvas><script>console.log('Hello Game!');</script></body></html></textarea>
    <div style="display:flex; gap:10px;">
      <button class="modal-btn" id="previewGameBtn"><i class="fas fa-eye"></i> Xem trước</button>
      <button class="modal-btn" style="background:#0EA5E9;" id="downloadGameBtn"><i class="fas fa-download"></i> Tải game (.html)</button>
    </div>
    <div class="game-preview" id="gamePreviewContainer">
      <iframe id="gamePreviewFrame" title="Game Preview"></iframe>
    </div>
    <button class="modal-btn" style="background:#1E1730; margin-top:15px;" id="closeCreateGameBtn">Đóng</button>
  </div>
</div>

<script src="https://cdn.jsdelivr.net/npm/qrcode@1.5.1/build/qrcode.min.js"></script>
<script>
  // ==================== DỮ LIỆU & STATE ====================
  let mods = JSON.parse(localStorage.getItem('ntk_mods_data')) || [
    { id:'1', name:'[32 BIT] HACK MAP NTK V6', version:'1.62.1.4', status:'online', downloadLink:'#' },
    { id:'2', name:'[64 BIT] HACK MAP NTK V6', version:'1.62.1.4', status:'online', downloadLink:'#' },
    { id:'3', name:'[64BIT] NTK PRO MAX V2', version:'1.62.1.4', status:'online', downloadLink:'#' },
    { id:'4', name:'[TÁCH GỐC] NTK PRO MAX V2', version:'1.62.1.4', status:'online', downloadLink:'#' },
    { id:'5', name:'[VIP] ESP WALLHACK', version:'4.2.0', status:'maintenance', downloadLink:'#' },
  ];
  let currentUser = JSON.parse(localStorage.getItem('ntk_current_user')) || null;
  let userBalance = parseInt(localStorage.getItem('ntk_user_balance')) || 100000;
  let userKeys = JSON.parse(localStorage.getItem('ntk_user_keys')) || [];

  // ==================== RENDER MODS ====================
  function renderMods(filter='all'){
    const filtered = filter==='all'?mods:mods.filter(m=>m.status===filter);
    document.getElementById('onlineCount').textContent = mods.filter(m=>m.status==='online').length;
    document.getElementById('maintCount').textContent = mods.filter(m=>m.status==='maintenance').length;
    let html = '';
    filtered.forEach(m=>{
      const isMaint = m.status==='maintenance';
      html += `<div class="mod-item ${isMaint?'maintenance':''}"><div class="mod-info"><h4>${m.name}</h4><div class="mod-meta">${m.version}</div></div><div style="display:flex; gap:20px;"><span class="status-badge ${isMaint?'status-maintenance':'status-online'}">${isMaint?'BẢO TRÌ':'ONLINE'}</span><a href="${m.downloadLink}" class="btn-download ${isMaint?'disabled':''}"><i class="fas fa-download"></i> Tải</a></div></div>`;
    });
    document.getElementById('modListContainer').innerHTML = html;
  }

  // ==================== USER KEY & WIDGET ====================
  function renderUserKey(){
    const area = document.getElementById('userKeyArea');
    if(!currentUser) { area.innerHTML = `<div class="no-key">Vui lòng đăng nhập</div>`; return; }
    if(userKeys.length===0) { area.innerHTML = `<div class="no-key">Chưa có key. <a onclick="openShopModal()" style="color:#FBBF24;cursor:pointer;">Mua ngay</a></div>`; return; }
    const latest = userKeys[0];
    const expiry = new Date(latest.expiry); const now = new Date(); const valid = expiry > now;
    const diff = expiry - now; const hours = Math.floor(diff/3600000); const mins = Math.floor((diff%3600000)/60000);
    area.innerHTML = `<div class="key-info"><h3>KEY HIỆN TẠI</h3><div class="key-code">${latest.code}</div><div>Hết hạn: ${expiry.toLocaleString()}</div></div><div class="key-timer">${valid?`${hours}h ${mins}m`:'Hết hạn'}</div>`;
  }

  function updateUserWidget(){
    const widget = document.getElementById('userWidget');
    if(currentUser){
      widget.innerHTML = `<div class="user-area"><div class="user-avatar">${currentUser.username.charAt(0).toUpperCase()}</div><span class="user-name">${currentUser.username}</span><span class="balance"><i class="fas fa-coins"></i> ${userBalance.toLocaleString()} Xu</span><button class="logout-btn" id="logoutBtn">Đăng xuất</button></div>`;
      document.getElementById('logoutBtn').addEventListener('click', logout);
      // Thêm menu Admin nếu là admin
      if(currentUser.isAdmin && !document.querySelector('[data-action="admin"]')){
        const adminItem = document.createElement('li'); adminItem.className='menu-item'; adminItem.dataset.action='admin';
        adminItem.innerHTML = '<i class="fas fa-cog"></i> Admin Panel';
        document.getElementById('sidebarMenu').appendChild(adminItem);
        adminItem.addEventListener('click', ()=>{ sidebar.classList.remove('active'); overlay.classList.remove('active'); openAdminPanel(); });
      }
      // Thêm menu Tạo Game nếu là subAdmin
      if(currentUser.isSubAdmin && !document.querySelector('[data-action="createGame"]')){
        const gameItem = document.createElement('li'); gameItem.className='menu-item'; gameItem.dataset.action='createGame';
        gameItem.innerHTML = '<i class="fas fa-gamepad"></i> Tạo Game';
        document.getElementById('sidebarMenu').appendChild(gameItem);
        gameItem.addEventListener('click', ()=>{ sidebar.classList.remove('active'); overlay.classList.remove('active'); openCreateGameModal(); });
      }
    } else {
      widget.innerHTML = `<button class="btn-outline" onclick="openAuthModal()"><i class="fas fa-sign-in-alt"></i> Đăng nhập</button>`;
    }
    renderUserKey();
  }

  function logout(){ currentUser=null; localStorage.removeItem('ntk_current_user'); updateUserWidget(); renderMods('all'); }

  // ==================== AUTH ====================
  const authModal = document.getElementById('authModal');
  window.openAuthModal = ()=> authModal.style.display='flex';
  document.getElementById('closeAuthBtn').addEventListener('click', ()=> authModal.style.display='none');
  document.getElementById('loginBtn').addEventListener('click', ()=>{
    const u = document.getElementById('loginUsername').value, p = document.getElementById('loginPassword').value;
    if((u==='ntkmod' && p==='123456') || (u==='admin' && p==='admin123') || (u==='subadmin' && p==='sub123')){
      currentUser = { username: u, isAdmin: (u==='admin'), isSubAdmin: (u==='subadmin') };
      localStorage.setItem('ntk_current_user', JSON.stringify(currentUser));
      if(!localStorage.getItem('ntk_user_balance')) { userBalance = 100000; localStorage.setItem('ntk_user_balance', userBalance); }
      userKeys = JSON.parse(localStorage.getItem('ntk_user_keys')) || [];
      updateUserWidget(); authModal.style.display='none'; renderMods('all');
    } else alert('Sai thông tin!');
  });

  // ==================== SHOP ====================
  const shopModal = document.getElementById('shopModal');
  window.openShopModal = ()=>{
    if(!currentUser) { alert('Đăng nhập trước!'); openAuthModal(); return; }
    document.getElementById('shopContent').innerHTML = `
      <div class="shop-pack"><div><h4>🔑 Key 24h</h4><p>10.000 Xu</p></div><button class="btn-buy" onclick="buyKey('24h',10000)">Mua</button></div>
      <div class="shop-pack"><div><h4>🔑 Key 7 ngày</h4><p>50.000 Xu</p></div><button class="btn-buy" onclick="buyKey('7d',50000)">Mua</button></div>
      <p>Số dư: <strong>${userBalance.toLocaleString()} Xu</strong></p>
    `;
    shopModal.style.display='flex';
  };
  window.buyKey = (type, price)=>{
    if(userBalance < price) { alert('Không đủ xu!'); return; }
    userBalance -= price;
    const code = 'NTK-'+Math.random().toString(36).substring(2,8).toUpperCase();
    const expiry = new Date(); expiry.setHours(expiry.getHours() + (type==='24h'?24:168));
    userKeys.unshift({ code, expiry: expiry.toISOString() });
    localStorage.setItem('ntk_user_balance', userBalance);
    localStorage.setItem('ntk_user_keys', JSON.stringify(userKeys));
    updateUserWidget(); shopModal.style.display='none'; alert(`Mua thành công! Key: ${code}`);
  };
  document.getElementById('closeShopBtn').addEventListener('click', ()=> shopModal.style.display='none');

  // ==================== NẠP XU ====================
  const rechargeModal = document.getElementById('rechargeModal');
  window.openRechargeModal = ()=>{
    if(!currentUser) { alert('Đăng nhập để nạp'); openAuthModal(); return; }
    rechargeModal.style.display='flex';
    QRCode.toCanvas(document.getElementById('qrCanvas'), 'NGUYEN TUAN KHANH', {width:200});
  };
  document.getElementById('closeRechargeBtn').addEventListener('click', ()=> rechargeModal.style.display='none');
  document.querySelectorAll('[data-recharge-tab]').forEach(t=>{ t.addEventListener('click', ()=>{
    document.querySelectorAll('[data-recharge-tab]').forEach(x=>x.classList.remove('active')); t.classList.add('active');
    document.getElementById('rechargeQR').style.display = t.dataset.rechargeTab==='qr'?'block':'none';
    document.getElementById('rechargeCard').style.display = t.dataset.rechargeTab==='card'?'block':'none';
    document.getElementById('rechargeBank').style.display = t.dataset.rechargeTab==='bank'?'block':'none';
  }); });
  document.getElementById('confirmQrBtn').addEventListener('click', ()=>{
    let amt = parseInt(document.getElementById('amountQR').value)||0;
    userBalance += amt; localStorage.setItem('ntk_user_balance', userBalance); updateUserWidget();
    alert(`+${amt} Xu`); rechargeModal.style.display='none';
  });
  document.getElementById('cardSubmitBtn').addEventListener('click', function(){
    this.textContent='Đang xử lý...'; setTimeout(()=>{
      userBalance += 50000; localStorage.setItem('ntk_user_balance', userBalance); updateUserWidget();
      alert('+50.000 Xu'); rechargeModal.style.display='none'; this.textContent='Nạp thẻ';
    }, 1500);
  });
  document.getElementById('bankSubmitBtn').addEventListener('click', ()=>{
    let amt = parseInt(document.getElementById('bankAmount').value)||0;
    userBalance += amt; localStorage.setItem('ntk_user_balance', userBalance); updateUserWidget();
    alert(`+${amt} Xu`); rechargeModal.style.display='none';
  });

  // ==================== ADMIN PANEL ====================
  const adminModal = document.getElementById('adminModal');
  function openAdminPanel(){
    if(!currentUser?.isAdmin) { alert('Không có quyền!'); return; }
    renderAdminMods(); adminModal.style.display='flex';
  }
  function renderAdminMods(){
    const container = document.getElementById('adminModsList');
    let html = '';
    mods.forEach((mod, idx)=>{
      html += `<div class="admin-mod-item">
        <input value="${mod.name}" data-index="${idx}" data-field="name" style="width:60%;">
        <input value="${mod.version}" data-index="${idx}" data-field="version" style="width:30%;">
        <input value="${mod.downloadLink}" data-index="${idx}" data-field="downloadLink" style="width:100%;">
        <select data-index="${idx}" data-field="status">
          <option value="online" ${mod.status==='online'?'selected':''}>Online</option>
          <option value="maintenance" ${mod.status==='maintenance'?'selected':''}>Bảo trì</option>
        </select>
        <div><button onclick="deleteMod(${idx})">Xóa</button></div>
      </div>`;
    });
    container.innerHTML = html;
    container.querySelectorAll('input, select').forEach(el=>{
      el.addEventListener('change', function(){
        const idx = this.dataset.index; const field = this.dataset.field;
        mods[idx][field] = this.value;
      });
    });
  }
  window.deleteMod = (idx)=>{ mods.splice(idx,1); renderAdminMods(); };
  document.getElementById('addNewModBtn').addEventListener('click', ()=>{
    mods.push({ id: Date.now().toString(), name:'Mod mới', version:'1.0', status:'online', downloadLink:'#' });
    renderAdminMods();
  });
  document.getElementById('saveAdminChanges').addEventListener('click', ()=>{
    localStorage.setItem('ntk_mods_data', JSON.stringify(mods));
    renderMods('all'); adminModal.style.display='none'; alert('Đã cập nhật web!');
  });
  document.getElementById('closeAdminBtn').addEventListener('click', ()=> adminModal.style.display='none');

  // ==================== TẠO GAME ====================
  const createGameModal = document.getElementById('createGameModal');
  function openCreateGameModal(){
    if(!currentUser?.isSubAdmin) { alert('Bạn cần quyền Phó Admin!'); return; }
    createGameModal.style.display='flex';
  }
  document.getElementById('closeCreateGameBtn').addEventListener('click', ()=> createGameModal.style.display='none');
  document.getElementById('previewGameBtn').addEventListener('click', ()=>{
    const code = document.getElementById('gameCode').value;
    const frame = document.getElementById('gamePreviewFrame');
    frame.srcdoc = code;
  });
  document.getElementById('downloadGameBtn').addEventListener('click', ()=>{
    const code = document.getElementById('gameCode').value;
    const blob = new Blob([code], { type: 'text/html' });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = `game_${Date.now()}.html`;
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
    URL.revokeObjectURL(url);
    alert('Đã tải game!');
  });

  // ==================== SIDEBAR & OTHER ====================
  const sidebar = document.getElementById('sidebar'), overlay = document.getElementById('overlay');
  document.getElementById('menuToggle').addEventListener('click', ()=>{ sidebar.classList.add('active'); overlay.classList.add('active'); });
  overlay.addEventListener('click', ()=>{ sidebar.classList.remove('active'); overlay.classList.remove('active'); });
  document.querySelectorAll('.menu-item').forEach(i=>{ i.addEventListener('click', (e)=>{
    sidebar.classList.remove('active'); overlay.classList.remove('active');
    const action = i.dataset.action;
    if(action==='home') window.scrollTo({top:0,behavior:'smooth'});
    else if(action==='search') document.getElementById('searchInput').focus();
    else if(action==='shop') openShopModal();
    else if(action==='recharge') openRechargeModal();
    else if(action==='account') openAuthModal();
  }); });
  document.querySelectorAll('.filter-btn').forEach(btn=>{ btn.addEventListener('click', function(){
    document.querySelectorAll('.filter-btn').forEach(b=>b.classList.remove('active')); this.classList.add('active');
    renderMods(this.dataset.filter);
  }); });
  document.querySelectorAll('.faq-item').forEach(i=> i.addEventListener('click', ()=> i.classList.toggle('active')));
  window.copyText = (t) => { navigator.clipboard?.writeText(t); alert('Đã copy: '+t); };

  // Khởi tạo
  if(currentUser) { userBalance = parseInt(localStorage.getItem('ntk_user_balance'))||100000; userKeys = JSON.parse(localStorage.getItem('ntk_user_keys'))||[]; }
  updateUserWidget();
  renderMods('all');
  setInterval(()=>{ if(currentUser) renderUserKey(); }, 60000);
</script>
</body>
</html>
