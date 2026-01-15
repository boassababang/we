<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Universal Journal | Global Press & Arts</title>
    
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,700;0,900;1,400&family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

    <style>
        :root {
            --primary: #b11e22;
            --accent: #00f2ff;
            --glass: rgba(255, 255, 255, 0.1);
            --transition: all 0.5s cubic-bezier(0.19, 1, 0.22, 1);
        }

        /* --- BACKGROUND BODY: URBAN & NATURE --- */
        * { box-sizing: border-box; margin: 0; padding: 0; }
        body {
            font-family: 'Inter', sans-serif;
            background: linear-gradient(rgba(0,0,0,0.6), rgba(0,0,0,0.6)), 
                        url('https://images.unsplash.com/photo-1449824913935-59a10b8d2000?auto=format&fit=crop&w=1920&q=80');
            background-size: cover;
            background-attachment: fixed;
            background-position: center;
            color: #fff;
            min-height: 100vh;
            overflow-x: hidden;
            transition: var(--transition);
        }

        /* --- HEADER --- */
        header {
            position: fixed; top: 0; width: 100%; height: 85px;
            background: rgba(255, 255, 255, 0.05); backdrop-filter: blur(15px);
            display: flex; align-items: center; justify-content: space-between;
            padding: 0 6%; z-index: 2000; border-bottom: 1px solid rgba(255,255,255,0.1);
        }

        .logo-main { font-family: 'Playfair Display', serif; font-size: 1.8rem; font-weight: 900; color: #fff; text-decoration: none; }
        .logo-main span { color: var(--primary); text-shadow: 0 0 10px var(--primary); }

        .nav-desktop { display: flex; gap: 25px; }
        .nav-desktop a { text-decoration: none; color: #fff; font-weight: 700; font-size: 0.8rem; text-transform: uppercase; letter-spacing: 1px; transition: 0.3s; }
        .nav-desktop a:hover { color: var(--accent); }

        .burger-trigger { display: none; cursor: pointer; flex-direction: column; gap: 6px; z-index: 3001; }
        .burger-trigger span { width: 30px; height: 3px; background: #fff; border-radius: 5px; transition: 0.4s; }

        /* --- SIDEBAR HAMBURGER (50% WIDTH HP) --- */
        .sidebar {
            position: fixed; top: 0; right: -100%; width: 50%; height: 100vh;
            z-index: 2900; transition: var(--transition); display: flex; flex-direction: column;
            align-items: center; padding: 40px 20px;
        }

        /* 3D Anime Hologram Background */
        .sidebar-anime-bg {
            position: absolute; inset: -50%;
            background: linear-gradient(45deg, #ff0055, #0055ff, #00ff55, #ffff00);
            background-size: 400% 400%; animation: auraFlow 1.5s infinite linear;
            z-index: -2; opacity: 0.3; filter: blur(60px);
        }
        @keyframes auraFlow {
            0% { background-position: 0% 50%; transform: rotate(0deg); }
            100% { background-position: 100% 50%; transform: rotate(360deg); }
        }
        .sidebar-overlay { position: absolute; inset: 0; background: rgba(0,0,0,0.92); backdrop-filter: blur(20px); z-index: -1; }

        /* PROFILE SECTION */
        .pfp-area { text-align: center; margin-bottom: 30px; }
        .pfp-circle {
            width: 100px; height: 100px; border-radius: 50%; border: 3px solid var(--accent);
            object-fit: cover; cursor: pointer; transition: 0.5s; margin-bottom: 10px;
            box-shadow: 0 0 15px var(--accent);
        }
        .owner-name { font-family: 'Playfair Display'; font-size: 1.2rem; font-weight: 700; color: white; }
        
        /* SIDEBAR NAV LINKS */
        .sidebar-nav { width: 100%; }
        .sidebar-nav a {
            display: flex; align-items: center; gap: 15px; color: white; text-decoration: none;
            padding: 15px; margin: 10px 0; background: rgba(255,255,255,0.05); border-radius: 12px;
            font-weight: 600; font-size: 0.85rem; transition: 0.3s;
        }
        .sidebar-nav a:active { background: white; color: black; box-shadow: 0 0 20px var(--accent); }

        .social-row { display: flex; gap: 15px; margin-top: auto; padding-top: 20px; }
        .social-row a { color: #fff; font-size: 1.3rem; transition: 0.3s; }

        /* --- CONTENT FEED --- */
        .main-feed { padding: 120px 6% 60px; display: grid; grid-template-columns: repeat(auto-fill, minmax(320px, 1fr)); gap: 30px; max-width: 1400px; margin: 0 auto; }
        
        .article-card { 
            background: rgba(0,0,0,0.5); backdrop-filter: blur(10px); border-radius: 15px; 
            overflow: hidden; border: 1px solid rgba(255,255,255,0.1); transition: 0.4s;
            display: flex; flex-direction: column; height: 100%;
        }
        .article-card:hover { transform: translateY(-10px); border-color: var(--accent); }
        .card-img { width: 100%; height: 200px; object-fit: cover; }
        .card-body { padding: 25px; flex-grow: 1; display: flex; flex-direction: column; }
        .card-title { font-family: 'Playfair Display'; font-size: 1.4rem; margin-bottom: 15px; line-height: 1.2; }
        .card-text { font-size: 0.9rem; color: #ddd; line-height: 1.6; height: 70px; overflow: hidden; margin-bottom: 20px; }
        .btn-more { align-self: flex-start; padding: 10px 20px; border: 1px solid var(--accent); color: var(--accent); text-decoration: none; border-radius: 5px; font-weight: 800; font-size: 0.7rem; }

        /* --- MODAL ARTICLE VIEW --- */
        .modal-view { display: none; position: fixed; inset: 0; background: #fff; z-index: 5000; overflow-y: auto; padding: 60px 8%; color: #111; }
        .modal-content { max-width: 800px; margin: 0 auto; }
        .modal-content h1 { font-family: 'Playfair Display'; font-size: 3rem; margin-bottom: 20px; }
        .modal-body { font-size: 1.2rem; line-height: 1.8; text-align: justify; white-space: pre-wrap; margin: 30px 0; }
        .modal-img { width: 100%; border-radius: 15px; }

        /* GRAPH RATING */
        .rating-box { background: #f4f4f4; padding: 30px; border-radius: 15px; text-align: center; }
        .graph-bar { width: 100%; height: 12px; background: #ddd; border-radius: 10px; display: flex; overflow: hidden; margin: 20px 0; }
        .bar-pos { background: #27ae60; height: 100%; transition: 1s; }
        .bar-neg { background: #e74c3c; height: 100%; transition: 1s; }

        /* --- SECRET EDITOR VAULT --- */
        #adminVault { display: none; position: fixed; inset: 0; background: #f0f2f5; z-index: 6000; padding: 40px 5%; overflow-y: auto; color: #000; }
        .vault-box { background: white; padding: 40px; border-radius: 15px; max-width: 1000px; margin: 0 auto; }
        .v-input { width: 100%; padding: 15px; margin-bottom: 15px; border: 1px solid #ddd; border-radius: 8px; font-size: 1rem; }
        textarea.v-input { height: 300px; }

        /* --- RESPONSIVE ADJUSTMENTS --- */
        @media (max-width: 992px) {
            .nav-desktop { display: none; }
            .burger-trigger { display: flex; }
            .sidebar.active { right: 0; }
        }
        @media (max-width: 600px) {
            .sidebar { width: 50%; } /* Menu 50% HP */
            .modal-content h1 { font-size: 2rem; }
        }

        .click-overlay { position: fixed; inset: 0; z-index: 2800; display: none; }
        .burger-trigger.open span:nth-child(1) { transform: rotate(45deg) translate(7px, 6px); }
        .burger-trigger.open span:nth-child(2) { opacity: 0; }
        .burger-trigger.open span:nth-child(3) { transform: rotate(-45deg) translate(7px, -6px); }
    </style>
</head>
<body>

    <div class="click-overlay" id="clickOverlay"></div>

    <header id="mainHeader">
        <a href="javascript:void(0)" onclick="filterCategory('All')" class="logo-main">UNIVERSAL<span>PRESS</span></a>
        <nav class="nav-desktop">
            <a href="javascript:void(0)" onclick="filterCategory('Internasional')">Internasional</a>
            <a href="javascript:void(0)" onclick="filterCategory('Politik')">Politik</a>
            <a href="javascript:void(0)" onclick="filterCategory('Opini')">Opini</a>
            <a href="javascript:void(0)" onclick="filterCategory('Puisi')">Puisi</a>
            <a href="javascript:void(0)" onclick="filterCategory('Cerita')">Cerita</a>
        </nav>
        <div class="burger-trigger" id="burgerBtn">
            <span></span><span></span><span></span>
        </div>
    </header>

    <aside class="sidebar" id="sidebar">
        <div class="sidebar-anime-bg"></div>
        <div class="sidebar-overlay"></div>
        
        <div class="pfp-area">
            <img src="https://via.placeholder.com/150" id="ownerPfp" class="pfp-circle" onclick="document.getElementById('pfpIn').click()">
            <input type="file" id="pfpIn" style="display:none" accept="image/*">
            <div class="owner-name" id="ownerName">Nama Pemilik</div>
            <div style="font-size: 0.6rem; letter-spacing: 2px; color: var(--accent);">CHIEF PUBLISHER</div>
        </div>

        <nav class="sidebar-nav">
            <a href="javascript:void(0)" onclick="enterVault()" style="background: rgba(0,242,255,0.1);"><i class="fas fa-key"></i> Editor Vault (887321)</a>
            <a href="javascript:void(0)" onclick="filterCategory('Internasional')"><i class="fas fa-globe"></i> Internasional</a>
            <a href="javascript:void(0)" onclick="filterCategory('Politik')"><i class="fas fa-landmark"></i> Politik</a>
            <a href="javascript:void(0)" onclick="filterCategory('Opini')"><i class="fas fa-pen-nib"></i> Opini</a>
            <a href="javascript:void(0)" onclick="filterCategory('Puisi')"><i class="fas fa-feather"></i> Puisi</a>
            <a href="javascript:void(0)" onclick="filterCategory('Cerita')"><i class="fas fa-book"></i> Cerita</a>
        </nav>

        <div class="social-row">
            <a href="#"><i class="fab fa-instagram"></i></a>
            <a href="#"><i class="fab fa-facebook"></i></a>
            <a href="#"><i class="fab fa-youtube"></i></a>
            <a href="#"><i class="fas fa-envelope"></i></a>
        </div>
    </aside>

    <main class="main-feed" id="mainFeed"></main>

    <div id="articleModal" class="modal-view">
        <div class="modal-content">
            <button onclick="closeModal()" class="v-btn" style="background:#000; color:#fff; padding:10px 20px; border:none; margin-bottom:30px; cursor:pointer;">&larr; KEMBALI</button>
            <img id="mImg" class="modal-img">
            <h1 id="mTitle"></h1>
            <div id="mMeta" style="margin-bottom:20px; font-weight:700; color:#666; border-bottom:1px solid #eee; padding-bottom:10px;"></div>
            <div id="mBody" class="modal-body"></div>

            <div class="rating-box">
                <div style="display:flex; justify-content:center; gap:40px; margin-bottom:20px;">
                    <button onclick="vote('up')" style="border:none; background:none; font-size:2.5rem; cursor:pointer; color:#27ae60;"><i class="fas fa-heart"></i></button>
                    <button onclick="vote('down')" style="border:none; background:none; font-size:2.5rem; cursor:pointer; color:#e74c3c;"><i class="fas fa-thumbs-down"></i></button>
                </div>
                <div class="graph-bar"><div id="barP" class="bar-pos"></div><div id="barN" class="bar-neg"></div></div>
                <p id="statText" style="font-weight:800;"></p>
            </div>
        </div>
    </div>

    <div id="adminVault">
        <div class="vault-box">
            <button onclick="closeVault()" style="float:right; border:none; background:none; font-size:1.5rem; cursor:pointer;">&times;</button>
            <h1 style="font-family:'Playfair Display'; margin-bottom:20px;">Universal Editorial Console</h1>
            <input type="text" id="vTitle" class="v-input" placeholder="Judul Publikasi...">
            <input type="text" id="vAuthor" class="v-input" placeholder="Nama Penulis Jurnal...">
            <input type="text" id="vImg" class="v-input" placeholder="URL Gambar Artikel (Unsplash/Link)...">
            <select id="vCat" class="v-input">
                <option value="Internasional">Internasional</option>
                <option value="Politik">Politik</option>
                <option value="Opini">Opini</option>
                <option value="Puisi">Puisi</option>
                <option value="Cerita">Cerita</option>
            </select>
            <textarea id="vContent" class="v-input" placeholder="Tuliskan naskah lengkap di sini..."></textarea>
            <button onclick="publish()" class="v-input" style="background:var(--primary); color:white; font-weight:bold; cursor:pointer;">PUBLIKASIKAN SEKARANG</button>
            <div id="adminList" style="margin-top:30px;"></div>
        </div>
    </div>

    <script>
        // --- NAVIGATION JS ---
        const burgerBtn = document.getElementById('burgerBtn');
        const sidebar = document.getElementById('sidebar');
        const clickOverlay = document.getElementById('clickOverlay');
        const pfpIn = document.getElementById('pfpIn');
        const ownerPfp = document.getElementById('ownerPfp');

        function toggleMenu() {
            const isOpen = sidebar.classList.toggle('active');
            burgerBtn.classList.toggle('open');
            clickOverlay.style.display = isOpen ? 'block' : 'none';
            document.body.style.overflow = isOpen ? 'hidden' : 'auto';
        }

        burgerBtn.addEventListener('click', toggleMenu);
        clickOverlay.addEventListener('click', toggleMenu);

        // --- PFP SYSTEM ---
        pfpIn.addEventListener('change', function() {
            const reader = new FileReader();
            reader.onload = e => {
                ownerPfp.src = e.target.result;
                localStorage.setItem('univ_pfp', e.target.result);
            }
            reader.readAsDataURL(this.files[0]);
        });

        // --- CORE DATA SYSTEM ---
        let posts = JSON.parse(localStorage.getItem('univ_posts')) || [];
        let curId = null;
        let currentCat = 'All';

        function enterVault() {
            if(prompt("Kode Otoritas Admin:") === "887321") {
                document.getElementById('adminVault').style.display = 'block';
                renderAdminList();
            } else alert("Akses Ditolak!");
        }

        function closeVault() { document.getElementById('adminVault').style.display = 'none'; }

        function publish() {
            const title = document.getElementById('vTitle').value;
            const author = document.getElementById('vAuthor').value;
            const content = document.getElementById('vContent').value;
            const img = document.getElementById('vImg').value || 'https://images.unsplash.com/photo-1504711434969-e33886168f5c?w=800';
            const cat = document.getElementById('vCat').value;

            if(!title || !content) return alert("Lengkapi naskah!");

            posts.unshift({
                id: Date.now(), title, author, content, img, cat,
                date: new Date().toLocaleDateString('id-ID'),
                up: 0, down: 0
            });

            save(); renderFeed(); closeVault();
        }

        function save() { localStorage.setItem('univ_posts', JSON.stringify(posts)); }

        function filterCategory(cat) {
            currentCat = cat;
            renderFeed();
            if(sidebar.classList.contains('active')) toggleMenu();
            
            // Animasi transisi background berdasarkan kategori
            const backgrounds = {
                'Internasional': 'https://images.unsplash.com/photo-1526778548025-fa2f459cd5c1?w=1920',
                'Politik': 'https://images.unsplash.com/photo-1529107386315-e1a2ed48a620?w=1920',
                'Puisi': 'https://images.unsplash.com/photo-1471107340929-a87cd0f5b5f3?w=1920',
                'All': 'https://images.unsplash.com/photo-1449824913935-59a10b8d2000?w=1920'
            };
            if(backgrounds[cat]) document.body.style.backgroundImage = `linear-gradient(rgba(0,0,0,0.6), rgba(0,0,0,0.6)), url('${backgrounds[cat]}')`;
        }

        function renderFeed() {
            const feed = document.getElementById('mainFeed');
            const filtered = currentCat === 'All' ? posts : posts.filter(p => p.cat === currentCat);
            
            feed.innerHTML = filtered.map(p => `
                <div class="article-card">
                    <img src="${p.img}" class="card-img">
                    <div class="card-body">
                        <span style="font-size:0.6rem; color:var(--accent); font-weight:900;">${p.cat}</span>
                        <h2 class="card-title">${p.title}</h2>
                        <div class="card-text">${p.content}</div>
                        <a href="javascript:void(0)" onclick="openPost(${p.id})" class="btn-more">SELENGKAPNYA</a>
                    </div>
                </div>
            `).join('');
        }

        function renderAdminList() {
            document.getElementById('adminList').innerHTML = posts.map(p => `
                <div style="background:#f9f9f9; padding:10px; margin-bottom:5px; border-radius:8px; display:flex; justify-content:space-between;">
                    <span>${p.title}</span>
                    <button onclick="deletePost(${p.id})" style="color:red; border:none; background:none; cursor:pointer;">Hapus</button>
                </div>
            `).join('');
        }

        function deletePost(id) {
            if(confirm("Hapus artikel?")) { posts = posts.filter(x => x.id !== id); save(); renderFeed(); renderAdminList(); }
        }

        function openPost(id) {
            const p = posts.find(x => x.id === id);
            curId = id;
            document.getElementById('mImg').src = p.img;
            document.getElementById('mTitle').innerText = p.title;
            document.getElementById('mMeta').innerText = `${p.cat} | Penulis: ${p.author} | ${p.date}`;
            document.getElementById('mBody').innerText = p.content;
            updateRatingUI(p);
            document.getElementById('articleModal').style.display = 'block';
            document.body.style.overflow = 'hidden';
        }

        function closeModal() { document.getElementById('articleModal').style.display = 'none'; document.body.style.overflow = 'auto'; }

        function vote(type) {
            const p = posts.find(x => x.id === curId);
            type === 'up' ? p.up++ : p.down++;
            save(); updateRatingUI(p);
        }

        function updateRatingUI(p) {
            const total = p.up + p.down;
            const upP = total === 0 ? 50 : (p.up / total) * 100;
            document.getElementById('barP').style.width = upP + "%";
            document.getElementById('barN').style.width = (100 - upP) + "%";
            document.getElementById('statText').innerText = `Rating Jurnal: ${Math.round(upP)}% Positif`;
        }

        window.onload = () => {
            const savedPfp = localStorage.getItem('univ_pfp');
            if(savedPfp) ownerPfp.src = savedPfp;
            renderFeed();
        }
    </script>
</body>
</html>
