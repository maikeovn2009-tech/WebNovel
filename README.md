# WebNovel
<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Góc Truyện — Wien</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,600;1,400&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/mammoth/1.6.0/mammoth.browser.min.js"></script>
<style>
:root{
  --bg:#FAF8F4;--bg-card:#FFF;--text-main:#1C1917;--text-muted:#78716C;
  --text-hint:#A8A29E;--accent:#92400E;--accent-light:#FEF3C7;--accent-mid:#D97706;
  --border:#E7E5E4;--border-strong:#D6D3D1;--tag-bg:#F5F0E8;--tag-text:#78400E;
  --red:#DC2626;--red-bg:#FEE2E2;--green:#16A34A;--green-bg:#DCFCE7;
  --blue:#1D4ED8;--blue-bg:#DBEAFE;--orange:#C2410C;--orange-bg:#FFEDD5;
}
*{margin:0;padding:0;box-sizing:border-box;}
body{font-family:'DM Sans',sans-serif;background:var(--bg);color:var(--text-main);line-height:1.7;min-height:100vh;}

header{background:var(--bg-card);border-bottom:1px solid var(--border);padding:0 2rem;position:sticky;top:0;z-index:200;display:flex;align-items:center;justify-content:space-between;height:64px;}
.logo{font-family:'Playfair Display',serif;font-size:1.4rem;color:var(--accent);cursor:pointer;user-select:none;}
nav{display:flex;gap:2rem;}
nav a{text-decoration:none;color:var(--text-muted);font-size:0.88rem;font-weight:500;cursor:pointer;transition:color 0.2s;}
nav a:hover,nav a.active{color:var(--text-main);}

.page{display:none;}
.page.active{display:block;animation:fadeIn 0.2s ease;}
@keyframes fadeIn{from{opacity:0;transform:translateY(5px)}to{opacity:1;transform:translateY(0)}}

.hero{max-width:860px;margin:4rem auto 2.5rem;padding:0 2rem;text-align:center;}
.hero h1{font-family:'Playfair Display',serif;font-size:clamp(2rem,5vw,3.2rem);line-height:1.15;margin-bottom:0.8rem;}
.hero h1 em{font-style:italic;color:var(--accent-mid);}
.hero p{color:var(--text-muted);font-size:1rem;max-width:480px;margin:0 auto;}
.controls{max-width:900px;margin:0 auto 1.5rem;padding:0 2rem;display:flex;flex-direction:column;gap:0.85rem;}
.search-sort-row{display:flex;gap:0.7rem;align-items:center;}
.search-box{position:relative;flex:1;}
.search-box input{width:100%;padding:0.65rem 1rem 0.65rem 2.6rem;border:1px solid var(--border-strong);border-radius:8px;font-family:'DM Sans',sans-serif;font-size:0.9rem;background:var(--bg-card);color:var(--text-main);outline:none;transition:border-color 0.2s;}
.search-box input:focus{border-color:var(--accent-mid);}
.search-icon{position:absolute;left:0.85rem;top:50%;transform:translateY(-50%);color:var(--text-hint);font-size:0.85rem;pointer-events:none;}
.sort-select{padding:0.6rem 0.85rem;border:1px solid var(--border-strong);border-radius:8px;font-family:'DM Sans',sans-serif;font-size:0.82rem;color:var(--text-muted);background:var(--bg-card);outline:none;cursor:pointer;white-space:nowrap;}
.filter-row{display:flex;gap:0.4rem;flex-wrap:wrap;align-items:center;}
.filter-label{font-size:0.7rem;color:var(--text-hint);font-weight:500;text-transform:uppercase;letter-spacing:0.05em;padding:0 0.15rem;}
.filter-btn{padding:0.33rem 0.82rem;border:1px solid var(--border-strong);border-radius:99px;background:var(--bg-card);color:var(--text-muted);font-family:'DM Sans',sans-serif;font-size:0.77rem;font-weight:500;cursor:pointer;transition:all 0.18s;white-space:nowrap;}
.filter-btn:hover{border-color:var(--accent-mid);color:var(--accent);}
.filter-btn.active{background:var(--accent);border-color:var(--accent);color:#FFF;}
.filter-btn.hplus-btn{border-color:#F87171;color:var(--red);}
.filter-btn.hplus-btn.active{background:var(--red);border-color:var(--red);color:#FFF;}
.divider-v{width:1px;height:16px;background:var(--border-strong);margin:0 0.1rem;flex-shrink:0;}

.tag-status-ongoing{background:#DBEAFE;color:#1D4ED8;}
.tag-status-hiatus{background:#FFEDD5;color:#C2410C;}
.tag-status-done{background:var(--green-bg);color:var(--green);}

.story-grid{max-width:900px;margin:0 auto;padding:0 2rem 5rem;display:grid;grid-template-columns:repeat(auto-fill,minmax(255px,1fr));gap:1.4rem;}
.story-card{background:var(--bg-card);border:1px solid var(--border);border-radius:12px;overflow:hidden;transition:transform 0.2s,box-shadow 0.2s;cursor:pointer;display:flex;flex-direction:column;}
.story-card:hover{transform:translateY(-3px);box-shadow:0 10px 28px rgba(0,0,0,0.09);}
.story-card-cover{height:128px;display:flex;align-items:center;justify-content:center;font-family:'Playfair Display',serif;font-size:2.2rem;font-style:italic;color:rgba(255,255,255,0.92);position:relative;}
.story-card-body{padding:1rem 1.2rem 1.15rem;flex:1;display:flex;flex-direction:column;}
.tag-row{display:flex;gap:0.35rem;flex-wrap:wrap;margin-bottom:0.5rem;}
.tag{display:inline-block;font-size:0.67rem;font-weight:500;padding:2px 8px;border-radius:99px;text-transform:uppercase;letter-spacing:0.04em;}
.tag-genre{background:#EDE9FE;color:#5B21B6;}
.tag-type{background:var(--tag-bg);color:var(--tag-text);}
.tag-hplus{background:var(--red-bg);color:var(--red);}
.story-title{font-family:'Playfair Display',serif;font-size:1.03rem;font-weight:600;line-height:1.3;margin-bottom:0.3rem;}
.story-desc{font-size:0.81rem;color:var(--text-muted);line-height:1.6;flex:1;display:-webkit-box;-webkit-line-clamp:3;-webkit-box-orient:vertical;overflow:hidden;}
.story-meta{display:flex;align-items:center;justify-content:space-between;margin-top:0.85rem;padding-top:0.65rem;border-top:1px solid var(--border);font-size:0.75rem;color:var(--text-hint);}
.read-btn{color:var(--accent-mid);font-weight:500;}
.empty-state{grid-column:1/-1;text-align:center;padding:4rem 0;color:var(--text-hint);}
.empty-state .empty-icon{font-size:2.5rem;margin-bottom:0.75rem;}
.empty-state p{font-size:0.88rem;}

.story-header{max-width:720px;margin:3rem auto 1.5rem;padding:0 2rem;}
.back-btn{display:inline-flex;align-items:center;gap:0.4rem;color:var(--text-muted);font-size:0.83rem;cursor:pointer;margin-bottom:1.2rem;transition:color 0.2s;border:none;background:none;font-family:'DM Sans',sans-serif;padding:0;}
.back-btn:hover{color:var(--text-main);}
.cover-banner{height:110px;border-radius:12px;margin-bottom:1.2rem;display:flex;align-items:center;padding:0 2rem;font-family:'Playfair Display',serif;font-size:2.4rem;font-style:italic;color:rgba(255,255,255,0.92);}
.chapter-list{max-width:720px;margin:0 auto;padding:0 2rem 5rem;}
.section-label{font-size:0.7rem;text-transform:uppercase;letter-spacing:0.09em;color:var(--text-hint);font-weight:500;margin-bottom:0.65rem;}
.chapter-item{display:flex;align-items:center;padding:0.75rem 1rem;border:1px solid var(--border);border-radius:8px;margin-bottom:0.4rem;background:var(--bg-card);cursor:pointer;transition:all 0.18s;}
.chapter-item:hover{border-color:var(--accent-mid);background:var(--accent-light);}
.chapter-num{font-size:0.7rem;color:var(--text-hint);font-weight:500;min-width:72px;}
.chapter-name{flex:1;font-size:0.88rem;}
.chapter-arrow{color:var(--text-hint);}

.reading-header{max-width:660px;margin:3rem auto 0;padding:0 2rem;}
.breadcrumb{display:flex;align-items:center;gap:0.45rem;margin-bottom:1.75rem;font-size:0.8rem;color:var(--text-muted);flex-wrap:wrap;}
.breadcrumb span{cursor:pointer;transition:color 0.2s;}
.breadcrumb span:hover{color:var(--text-main);}
.breadcrumb .sep,.breadcrumb .current{cursor:default;}
.breadcrumb .current{color:var(--text-main);}
.reading-title{font-family:'Playfair Display',serif;font-size:clamp(1.5rem,3.5vw,2rem);margin-bottom:0.3rem;line-height:1.25;}
.reading-info{color:var(--text-hint);font-size:0.8rem;margin-bottom:1rem;}

.font-controls{display:flex;align-items:center;gap:0.5rem;margin-bottom:2rem;padding:0.5rem 0.75rem;background:var(--bg-card);border:1px solid var(--border);border-radius:8px;width:fit-content;}
.font-controls span{font-size:0.75rem;color:var(--text-hint);margin-right:0.25rem;}
.font-btn{width:28px;height:28px;border:1px solid var(--border-strong);border-radius:6px;background:var(--bg);color:var(--text-muted);cursor:pointer;font-family:'DM Sans',sans-serif;font-size:0.82rem;font-weight:500;display:flex;align-items:center;justify-content:center;transition:all 0.18s;}
.font-btn:hover{border-color:var(--accent-mid);color:var(--accent);}
.font-size-label{font-size:0.8rem;color:var(--text-muted);min-width:32px;text-align:center;}

.reading-body{max-width:660px;margin:0 auto;padding:0 2rem 4rem;line-height:2;color:#2C2A28;}
.reading-body p{margin-bottom:1.4em;}
.reading-body h2{font-family:'Playfair Display',serif;font-size:1.2rem;margin:2em 0 0.75em;color:var(--text-main);}
.chapter-footer{max-width:660px;margin:0 auto 5rem;padding:1rem 2rem 0;display:flex;justify-content:space-between;gap:1rem;border-top:1px solid var(--border);}
.nav-btn{padding:0.58rem 1.3rem;border:1px solid var(--border-strong);border-radius:8px;background:var(--bg-card);font-family:'DM Sans',sans-serif;font-size:0.83rem;color:var(--text-muted);cursor:pointer;transition:all 0.2s;font-weight:500;}
.nav-btn:hover:not(:disabled){border-color:var(--accent-mid);color:var(--accent);}
.nav-btn:disabled{opacity:0.28;cursor:not-allowed;}

.about-wrap{max-width:660px;margin:5rem auto;padding:0 2rem 5rem;}
.about-wrap h1{font-family:'Playfair Display',serif;font-size:2rem;margin-bottom:1.5rem;}
.about-wrap p{color:var(--text-muted);margin-bottom:1.1rem;font-size:0.97rem;line-height:1.85;}

.admin-wrap{max-width:760px;margin:3rem auto;padding:0 2rem 5rem;}
.admin-wrap h1{font-family:'Playfair Display',serif;font-size:1.8rem;margin-bottom:0.35rem;}
.admin-subtitle{color:var(--text-muted);font-size:0.86rem;margin-bottom:1.5rem;}

.admin-tabs{display:flex;gap:0;border:1px solid var(--border);border-radius:10px;overflow:hidden;margin-bottom:1.5rem;}
.admin-tab{flex:1;padding:0.65rem 1rem;border:none;background:var(--bg-card);color:var(--text-muted);font-family:'DM Sans',sans-serif;font-size:0.83rem;font-weight:500;cursor:pointer;transition:all 0.18s;border-right:1px solid var(--border);text-align:center;}
.admin-tab:last-child{border-right:none;}
.admin-tab:hover{background:var(--accent-light);color:var(--accent);}
.admin-tab.active{background:var(--accent);color:#FFF;}
.admin-panel{display:none;}
.admin-panel.active{display:block;}

.admin-section{background:var(--bg-card);border:1px solid var(--border);border-radius:12px;padding:1.5rem;margin-bottom:1.2rem;}
.admin-section h2{font-size:0.92rem;font-weight:500;margin-bottom:1.15rem;color:var(--text-main);}
.form-row{margin-bottom:0.9rem;}
.form-row label{display:block;font-size:0.72rem;font-weight:500;color:var(--text-muted);margin-bottom:0.28rem;text-transform:uppercase;letter-spacing:0.04em;}
.form-row input,.form-row select,.form-row textarea{width:100%;padding:0.56rem 0.85rem;border:1px solid var(--border-strong);border-radius:8px;font-family:'DM Sans',sans-serif;font-size:0.88rem;color:var(--text-main);background:var(--bg);outline:none;transition:border-color 0.2s;}
.form-row input:focus,.form-row select:focus,.form-row textarea:focus{border-color:var(--accent-mid);background:var(--bg-card);}
.form-row textarea{min-height:76px;resize:vertical;}
.form-row-2{display:grid;grid-template-columns:1fr 1fr;gap:0.75rem;}
.form-row-3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:0.75rem;}
.checkbox-label{display:flex;align-items:center;gap:0.55rem;padding:0.55rem 0.85rem;border:1px solid var(--border-strong);border-radius:8px;background:var(--bg);cursor:pointer;}
.checkbox-label input[type=checkbox]{accent-color:var(--red);cursor:pointer;width:15px;height:15px;flex-shrink:0;}
.checkbox-label span{font-size:0.85rem;color:var(--text-muted);}

.story-manage-item{border:1px solid var(--border);border-radius:10px;margin-bottom:0.6rem;background:var(--bg-card);overflow:hidden;}
.story-manage-header{display:flex;align-items:center;padding:0.75rem 1rem;gap:0.75rem;cursor:pointer;transition:background 0.18s;}
.story-manage-header:hover{background:var(--bg);}
.story-manage-cover{width:36px;height:36px;border-radius:6px;display:flex;align-items:center;justify-content:center;font-family:'Playfair Display',serif;font-size:1rem;font-style:italic;color:rgba(255,255,255,0.9);flex-shrink:0;}
.story-manage-info{flex:1;min-width:0;}
.story-manage-name{font-size:0.88rem;font-weight:500;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
.story-manage-meta{font-size:0.72rem;color:var(--text-hint);margin-top:1px;}
.story-manage-actions{display:flex;gap:0.35rem;flex-shrink:0;}
.story-manage-body{display:none;border-top:1px solid var(--border);padding:1rem;}
.story-manage-body.open{display:block;}
.chapter-manage-item{display:flex;align-items:center;padding:0.55rem 0.75rem;border:1px solid var(--border);border-radius:7px;margin-bottom:0.35rem;background:var(--bg);gap:0.6rem;}
.chapter-manage-num{font-size:0.7rem;color:var(--text-hint);min-width:60px;}
.chapter-manage-name{flex:1;font-size:0.85rem;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;}
.chapter-manage-actions{display:flex;gap:0.3rem;flex-shrink:0;}

.btn-primary{background:var(--accent);color:#FFF;border:none;padding:0.6rem 1.35rem;border-radius:8px;font-family:'DM Sans',sans-serif;font-size:0.86rem;font-weight:500;cursor:pointer;transition:background 0.2s;}
.btn-primary:hover{background:#78350F;}
.btn-secondary{background:var(--bg-card);color:var(--text-main);border:1px solid var(--border-strong);padding:0.56rem 1.1rem;border-radius:8px;font-family:'DM Sans',sans-serif;font-size:0.86rem;cursor:pointer;transition:all 0.2s;}
.btn-secondary:hover{border-color:var(--accent-mid);}
.btn-danger{background:var(--bg-card);color:var(--red);border:1px solid #FECACA;padding:0.56rem 1.1rem;border-radius:8px;font-family:'DM Sans',sans-serif;font-size:0.86rem;cursor:pointer;transition:all 0.2s;}
.btn-danger:hover{background:var(--red-bg);}
.btn-sm{padding:0.25rem 0.65rem;font-size:0.72rem;border-radius:6px;border:1px solid var(--border-strong);background:var(--bg-card);color:var(--text-muted);cursor:pointer;font-family:'DM Sans',sans-serif;transition:all 0.18s;white-space:nowrap;}
.btn-sm:hover{border-color:var(--accent-mid);color:var(--accent);}
.btn-sm.del:hover{border-color:var(--red);color:var(--red);}
.btn-sm.edit-sm:hover{border-color:var(--blue);color:var(--blue);}

.upload-zone{border:2px dashed var(--border-strong);border-radius:10px;padding:1.4rem;text-align:center;cursor:pointer;transition:all 0.2s;background:var(--bg);}
.upload-zone:hover,.upload-zone.drag-over{border-color:var(--accent-mid);background:var(--accent-light);}
.upload-zone .icon{font-size:1.5rem;display:block;margin-bottom:0.3rem;}
.upload-zone strong{font-size:0.84rem;}
.upload-zone p{color:var(--text-muted);font-size:0.78rem;margin-top:0.15rem;}
#word-file-input,#edit-word-input{display:none;}
.file-preview-box{border:1px solid var(--border);border-radius:8px;padding:0.65rem 1rem;margin-top:0.5rem;background:var(--bg);display:flex;align-items:center;justify-content:space-between;}
.file-preview-box span{font-size:0.82rem;}
.file-preview-box button{background:none;border:none;color:var(--text-hint);cursor:pointer;font-size:1rem;padding:0;line-height:1;transition:color 0.2s;}
.file-preview-box button:hover{color:var(--red);}

.color-picker-row{display:flex;gap:0.4rem;flex-wrap:wrap;}
.color-opt{width:26px;height:26px;border-radius:5px;cursor:pointer;border:2px solid transparent;transition:border-color 0.15s,transform 0.15s;}
.color-opt:hover{transform:scale(1.12);}
.color-opt.selected{border-color:var(--text-main);}

.login-wrap{min-height:80vh;display:flex;align-items:center;justify-content:center;padding:2rem;}
.login-box{background:var(--bg-card);border:1px solid var(--border);border-radius:16px;padding:2.5rem 2rem;width:100%;max-width:380px;}
.login-error{display:none;background:#FEF2F2;border:1px solid #FECACA;border-radius:8px;padding:0.58rem 0.85rem;font-size:0.81rem;color:var(--red);margin-bottom:0.9rem;}

.modal-backdrop{display:none;position:fixed;inset:0;background:rgba(0,0,0,0.4);z-index:500;align-items:center;justify-content:center;padding:1rem;}
.modal-backdrop.open{display:flex;}
.modal-box{background:var(--bg-card);border-radius:14px;padding:2rem;max-width:420px;width:100%;}
.modal-box h3{font-family:'Playfair Display',serif;font-size:1.2rem;margin-bottom:0.5rem;}
.modal-box p{font-size:0.88rem;color:var(--text-muted);margin-bottom:1.25rem;line-height:1.6;}
.modal-actions{display:flex;gap:0.6rem;justify-content:flex-end;}

.read-progress{position:fixed;top:64px;left:0;right:0;height:2px;background:var(--border);z-index:190;}
.read-progress-bar{height:100%;background:var(--accent-mid);width:0%;transition:width 0.1s;}

.toast{position:fixed;bottom:1.75rem;right:1.75rem;background:#1C1917;color:#FFF;padding:0.65rem 1.1rem;border-radius:8px;font-size:0.82rem;z-index:999;opacity:0;transform:translateY(6px);transition:opacity 0.25s,transform 0.25s;pointer-events:none;max-width:320px;line-height:1.4;}
.toast.show{opacity:1;transform:translateY(0);}

/* Storage info banner */
.storage-banner{background:var(--accent-light);border:1px solid #FDE68A;border-radius:10px;padding:0.85rem 1.1rem;margin-bottom:1.2rem;font-size:0.82rem;color:#92400E;display:flex;align-items:flex-start;gap:0.6rem;line-height:1.5;}
.storage-banner strong{display:block;margin-bottom:0.15rem;}

@media(max-width:640px){
  header{padding:0 1rem;}nav{gap:1.2rem;}
  .story-grid{grid-template-columns:1fr;padding:0 1rem 4rem;}
  .controls,.story-header,.chapter-list,.reading-header,.reading-body,.chapter-footer,.about-wrap,.admin-wrap{padding-left:1rem;padding-right:1rem;}
  .form-row-2,.form-row-3{grid-template-columns:1fr;}
}
</style>
</head>
<body>

<div class="read-progress"><div class="read-progress-bar" id="prog-bar"></div></div>

<header>
  <div class="logo" onclick="goHome()">✦ Góc Truyện</div>
  <nav>
    <a onclick="goHome()" id="nav-home" class="active">Trang chủ</a>
    <a onclick="goAbout()" id="nav-about">Tác giả</a>
    <a onclick="goAdmin()" id="nav-admin">Quản lý</a>
  </nav>
</header>

<!-- HOME -->
<div class="page active" id="page-home">
  <div class="hero">
    <h1><span id="hero-line1">Song tu là đạo</span><br><em id="hero-line2">Song hành là duyên</em></h1>
    <p id="hero-sub">Đạo vô vi ấy là yên — truyện đây kể trọn, duyên duyên ắt tìm.</p>
  </div>
  <div class="controls">
    <div class="search-sort-row">
      <div class="search-box">
        <span class="search-icon">🔍</span>
        <input type="text" id="search-input" placeholder="Tìm tên truyện..." oninput="applyFilters()">
      </div>
      <select class="sort-select" id="sort-select" onchange="applyFilters()">
        <option value="newest">Mới nhất</option>
        <option value="oldest">Cũ nhất</option>
        <option value="az">Tên A → Z</option>
        <option value="za">Tên Z → A</option>
        <option value="chapters">Nhiều chương nhất</option>
      </select>
    </div>
    <div class="filter-row">
      <span class="filter-label">Thể loại</span>
      <button class="filter-btn active" data-fkey="genre" data-fval="all" onclick="setFilter('genre','all',this)">Tất cả</button>
      <button class="filter-btn" data-fkey="genre" data-fval="Tu Tiên" onclick="setFilter('genre','Tu Tiên',this)">Tu Tiên</button>
      <button class="filter-btn" data-fkey="genre" data-fval="Boy Love" onclick="setFilter('genre','Boy Love',this)">Boy Love</button>
      <button class="filter-btn" data-fkey="genre" data-fval="Xuyên Không/Trùng Sinh" onclick="setFilter('genre','Xuyên Không/Trùng Sinh',this)">Xuyên Không / Trùng Sinh</button>
      <div class="divider-v"></div>
      <span class="filter-label">Dạng</span>
      <button class="filter-btn active" data-fkey="type" data-fval="all" onclick="setFilter('type','all',this)">Tất cả</button>
      <button class="filter-btn" data-fkey="type" data-fval="Oneshot" onclick="setFilter('type','Oneshot',this)">Oneshot</button>
      <button class="filter-btn" data-fkey="type" data-fval="Truyện Dài" onclick="setFilter('type','Truyện Dài',this)">Truyện Dài</button>
      <div class="divider-v"></div>
      <span class="filter-label">Trạng thái</span>
      <button class="filter-btn active" data-fkey="status" data-fval="all" onclick="setFilter('status','all',this)">Tất cả</button>
      <button class="filter-btn" data-fkey="status" data-fval="ongoing" onclick="setFilter('status','ongoing',this)">Đang ra</button>
      <button class="filter-btn" data-fkey="status" data-fval="hiatus" onclick="setFilter('status','hiatus',this)">Tạm dừng</button>
      <button class="filter-btn" data-fkey="status" data-fval="done" onclick="setFilter('status','done',this)">Hoàn thành</button>
      <div class="divider-v"></div>
      <button class="filter-btn hplus-btn" id="hplus-filter-btn" onclick="toggleHplus(this)">🔞 H+</button>
    </div>
  </div>
  <div class="story-grid" id="story-grid"></div>
</div>

<!-- STORY DETAIL -->
<div class="page" id="page-story">
  <div class="story-header">
    <button class="back-btn" onclick="goHome()">← Quay lại</button>
    <div class="cover-banner" id="detail-banner"></div>
    <h1 id="detail-title" style="font-family:'Playfair Display',serif;font-size:clamp(1.6rem,4vw,2.3rem);margin-bottom:0.4rem;line-height:1.2;"></h1>
    <div id="detail-tags" style="display:flex;gap:0.35rem;flex-wrap:wrap;margin-bottom:0.85rem;"></div>
    <p id="detail-desc" style="color:var(--text-muted);font-size:0.92rem;line-height:1.75;"></p>
  </div>
  <div class="chapter-list">
    <div class="section-label">Danh sách chương</div>
    <div id="chapter-items"></div>
  </div>
</div>

<!-- READING -->
<div class="page" id="page-reading">
  <div class="reading-header">
    <div class="breadcrumb">
      <span onclick="goHome()">Trang chủ</span>
      <span class="sep">›</span>
      <span id="nav-story-name" onclick="goBackToStory()"></span>
      <span class="sep">›</span>
      <span class="current" id="nav-chapter-name"></span>
    </div>
    <div class="reading-title" id="read-title"></div>
    <div class="reading-info" id="read-info"></div>
    <div class="font-controls">
      <span>Cỡ chữ</span>
      <button class="font-btn" onclick="changeFontSize(-1)">A−</button>
      <span class="font-size-label" id="font-size-label">16</span>
      <button class="font-btn" onclick="changeFontSize(1)">A+</button>
    </div>
  </div>
  <div class="reading-body" id="read-body"></div>
  <div class="chapter-footer">
    <button class="nav-btn" id="btn-prev" onclick="navChapter(-1)">← Chương trước</button>
    <button class="nav-btn" id="btn-next" onclick="navChapter(1)">Chương tiếp →</button>
  </div>
</div>

<!-- ABOUT -->
<div class="page" id="page-about">
  <div class="about-wrap">
    <h1 id="about-title">Về tác giả</h1>
    <p id="about-p1"></p><p id="about-p2"></p><p id="about-p3"></p>
  </div>
</div>

<!-- LOGIN -->
<div class="page" id="page-login">
  <div class="login-wrap">
    <div class="login-box">
      <div style="text-align:center;margin-bottom:1.75rem;">
        <div style="font-size:2rem;margin-bottom:0.4rem;">🔐</div>
        <div style="font-family:'Playfair Display',serif;font-size:1.4rem;margin-bottom:0.2rem;">Khu vực tác giả</div>
        <div style="font-size:0.8rem;color:var(--text-hint);">Chỉ dành cho chủ trang</div>
      </div>
      <div class="form-row"><label>Tên đăng nhập</label>
        <input type="text" id="login-user" placeholder="Nhập tên đăng nhập" autocomplete="username" onkeydown="if(event.key==='Enter')doLogin()">
      </div>
      <div class="form-row"><label>Mật khẩu</label>
        <input type="password" id="login-pass" placeholder="Nhập mật khẩu" autocomplete="current-password" onkeydown="if(event.key==='Enter')doLogin()">
      </div>
      <div class="login-error" id="login-error">Tên đăng nhập hoặc mật khẩu không đúng.</div>
      <button class="btn-primary" style="width:100%;padding:0.65rem;" onclick="doLogin()">Đăng nhập</button>
      <div style="text-align:center;margin-top:1.2rem;">
        <span onclick="goHome()" style="font-size:0.8rem;color:var(--text-hint);cursor:pointer;" onmouseover="this.style.color='var(--text-main)'" onmouseout="this.style.color='var(--text-hint)'">← Quay về trang chủ</span>
      </div>
    </div>
  </div>
</div>

<!-- ADMIN -->
<div class="page" id="page-admin">
  <div class="admin-wrap">
    <h1>Quản lý truyện</h1>
    <p class="admin-subtitle">Thêm truyện và chương — dữ liệu tự lưu ngay vào trình duyệt, hiện trên trang chủ luôn.</p>

    <!-- Storage info banner -->
    <div class="storage-banner">
      <span style="font-size:1.1rem;flex-shrink:0;">💾</span>
      <div>
        <strong>Dữ liệu lưu tự động trong trình duyệt này</strong>
        Thêm truyện/chương xong là hiện trên trang chủ ngay — không cần xuất file. Nếu muốn backup hoặc chia sẻ sang máy khác, dùng tab <strong>Xuất file</strong> để tải HTML về rồi upload lên GitHub.
      </div>
    </div>

    <div class="admin-tabs">
      <button class="admin-tab active" onclick="switchTab('tab-stories',this)">📚 Truyện của tôi</button>
      <button class="admin-tab" onclick="switchTab('tab-add-story',this)">➕ Thêm truyện</button>
      <button class="admin-tab" onclick="switchTab('tab-add-chapter',this)">📖 Thêm chương</button>
      <button class="admin-tab" onclick="switchTab('tab-export',this)">💾 Xuất file</button>
    </div>

    <!-- TAB: DANH SÁCH TRUYỆN -->
    <div class="admin-panel active" id="tab-stories">
      <div class="admin-section">
        <h2>📚 Tất cả truyện <span id="story-count-badge" style="font-size:0.78rem;color:var(--text-hint);font-weight:400;"></span></h2>
        <div id="story-manage-list"><p style="color:var(--text-hint);font-size:0.85rem;">Chưa có truyện nào.</p></div>
      </div>
    </div>

    <!-- TAB: THÊM TRUYỆN -->
    <div class="admin-panel" id="tab-add-story">
      <div class="admin-section">
        <h2>➕ Thêm truyện mới</h2>
        <div class="form-row"><label>Tên truyện *</label>
          <input type="text" id="new-title" placeholder="VD: Tiên Đạo Vô Danh">
        </div>
        <div class="form-row"><label>Mô tả ngắn</label>
          <textarea id="new-desc" placeholder="Viết vài dòng giới thiệu về truyện..."></textarea>
        </div>
        <div class="form-row-3">
          <div class="form-row" style="margin:0"><label>Thể loại</label>
            <select id="new-genre">
              <option value="Tu Tiên">Tu Tiên</option>
              <option value="Boy Love">Boy Love</option>
              <option value="Xuyên Không/Trùng Sinh">Xuyên Không / Trùng Sinh</option>
            </select>
          </div>
          <div class="form-row" style="margin:0"><label>Dạng</label>
            <select id="new-type">
              <option value="Oneshot">Oneshot</option>
              <option value="Truyện Dài">Truyện Dài</option>
            </select>
          </div>
          <div class="form-row" style="margin:0"><label>Trạng thái</label>
            <select id="new-status">
              <option value="ongoing">Đang ra</option>
              <option value="hiatus">Tạm dừng</option>
              <option value="done">Hoàn thành</option>
            </select>
          </div>
        </div>
        <div class="form-row">
          <label>Nội dung người lớn</label>
          <label class="checkbox-label">
            <input type="checkbox" id="new-hplus">
            <span>Đánh dấu truyện này có nội dung H+ (18+)</span>
          </label>
        </div>
        <div class="form-row"><label>Màu bìa</label>
          <div class="color-picker-row" id="color-picker">
            <div class="color-opt selected" data-color="linear-gradient(135deg,#F59E0B,#D97706)" style="background:linear-gradient(135deg,#F59E0B,#D97706)" title="Vàng cam"></div>
            <div class="color-opt" data-color="linear-gradient(135deg,#6366F1,#4338CA)" style="background:linear-gradient(135deg,#6366F1,#4338CA)" title="Indigo"></div>
            <div class="color-opt" data-color="linear-gradient(135deg,#10B981,#059669)" style="background:linear-gradient(135deg,#10B981,#059669)" title="Xanh lá"></div>
            <div class="color-opt" data-color="linear-gradient(135deg,#EC4899,#BE185D)" style="background:linear-gradient(135deg,#EC4899,#BE185D)" title="Hồng đậm"></div>
            <div class="color-opt" data-color="linear-gradient(135deg,#EF4444,#DC2626)" style="background:linear-gradient(135deg,#EF4444,#DC2626)" title="Đỏ"></div>
            <div class="color-opt" data-color="linear-gradient(135deg,#14B8A6,#0F766E)" style="background:linear-gradient(135deg,#14B8A6,#0F766E)" title="Ngọc lam"></div>
            <div class="color-opt" data-color="linear-gradient(135deg,#8B5CF6,#6D28D9)" style="background:linear-gradient(135deg,#8B5CF6,#6D28D9)" title="Tím"></div>
            <div class="color-opt" data-color="linear-gradient(135deg,#F97316,#EA580C)" style="background:linear-gradient(135deg,#F97316,#EA580C)" title="Cam"></div>
            <div class="color-opt" data-color="linear-gradient(135deg,#0EA5E9,#0284C7)" style="background:linear-gradient(135deg,#0EA5E9,#0284C7)" title="Xanh dương"></div>
            <div class="color-opt" data-color="linear-gradient(135deg,#64748B,#334155)" style="background:linear-gradient(135deg,#64748B,#334155)" title="Xám tối"></div>
          </div>
        </div>
        <div class="form-row"><label>Chữ hiển thị trên bìa</label>
          <input type="text" id="new-emoji" maxlength="2" placeholder="VD: T" style="max-width:70px;">
        </div>
        <button class="btn-primary" onclick="addStory()">Tạo truyện</button>
      </div>
    </div>

    <!-- TAB: THÊM CHƯƠNG -->
    <div class="admin-panel" id="tab-add-chapter">
      <div class="admin-section">
        <h2>📖 Thêm chương mới từ file Word</h2>
        <div class="form-row"><label>Chọn truyện *</label>
          <select id="chapter-story-select"><option value="">-- Chọn truyện --</option></select>
        </div>
        <div class="form-row"><label>Tên chương *</label>
          <input type="text" id="new-chapter-title" placeholder="VD: Chương 1 – Khởi đầu">
        </div>
        <div class="form-row">
          <label>File Word (.docx) *</label>
          <div class="upload-zone" id="upload-zone" onclick="document.getElementById('word-file-input').click()">
            <span class="icon">📄</span>
            <strong>Bấm để chọn file .docx</strong>
            <p>hoặc kéo thả file vào đây</p>
          </div>
          <input type="file" id="word-file-input" accept=".docx" onchange="handleWordFile(this.files[0])">
          <div id="file-preview"></div>
        </div>
        <button class="btn-primary" onclick="addChapter()">Thêm chương</button>
      </div>
    </div>

    <!-- TAB: XUẤT FILE -->
    <div class="admin-panel" id="tab-export">
      <div class="admin-section">
        <h2>💾 Xuất & backup lên GitHub</h2>
        <p style="font-size:0.83rem;color:var(--text-muted);margin-bottom:0.6rem;line-height:1.7;">
          Dữ liệu truyện đã được <strong>tự động lưu trong trình duyệt</strong> này rồi — bạn không cần xuất file để đọc truyện.<br><br>
          Nút <strong>Xuất file HTML</strong> dùng khi bạn muốn:
        </p>
        <ul style="font-size:0.83rem;color:var(--text-muted);margin-bottom:1.2rem;padding-left:1.3rem;line-height:2;">
          <li>🌐 Chia sẻ trang web lên <strong>GitHub Pages</strong> để người khác đọc được</li>
          <li>💼 Backup toàn bộ dữ liệu ra file an toàn</li>
          <li>💻 Mở trên máy tính khác / trình duyệt khác</li>
        </ul>
        <div style="background:var(--bg);border:1px solid var(--border);border-radius:10px;padding:1rem 1.2rem;margin-bottom:1.2rem;font-size:0.82rem;color:var(--text-muted);line-height:1.8;">
          <strong style="color:var(--text-main);display:block;margin-bottom:0.3rem;">📋 Hướng dẫn upload GitHub:</strong>
          1. Bấm <strong>Xuất file HTML</strong> → tải về file <code style="background:#e5e7eb;padding:1px 5px;border-radius:3px;">index.html</code><br>
          2. Vào <a href="https://github.com" target="_blank" style="color:var(--accent-mid);">github.com</a> → mở repository của bạn<br>
          3. Bấm vào file <code style="background:#e5e7eb;padding:1px 5px;border-radius:3px;">index.html</code> → bấm biểu tượng ✏️ (Edit)<br>
          4. Xóa hết nội dung cũ → dán nội dung file mới vào → bấm <strong>Commit changes</strong><br>
          <em style="font-size:0.78rem;">Hoặc: kéo thả file index.html mới vào thẳng repository → chọn "Replace"</em>
        </div>
        <div style="display:flex;gap:0.6rem;flex-wrap:wrap;align-items:center;">
          <button class="btn-primary" onclick="exportHTML()">⬇ Xuất file HTML</button>
          <button class="btn-secondary" onclick="goHome()">← Xem trang chủ</button>
          <button class="btn-danger" onclick="doLogout()" style="margin-left:auto;">Đăng xuất</button>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- Modal xác nhận xóa -->
<div class="modal-backdrop" id="confirm-modal">
  <div class="modal-box">
    <h3 id="modal-title">Xác nhận</h3>
    <p id="modal-msg"></p>
    <div class="modal-actions">
      <button class="btn-secondary" onclick="closeModal()">Hủy</button>
      <button class="btn-danger" id="modal-confirm-btn">Xóa</button>
    </div>
  </div>
</div>

<!-- Modal sửa tên chương -->
<div class="modal-backdrop" id="edit-chapter-modal">
  <div class="modal-box">
    <h3>Sửa chương</h3>
    <div class="form-row" style="margin-bottom:0.75rem;"><label>Tên chương</label>
      <input type="text" id="edit-chapter-name-input" placeholder="Tên chương">
    </div>
    <div class="form-row" style="margin-bottom:0.75rem;"><label>Thay nội dung bằng file Word mới (tuỳ chọn)</label>
      <div class="upload-zone" style="padding:1rem;" onclick="document.getElementById('edit-word-input').click()">
        <span class="icon" style="font-size:1.2rem;">📄</span>
        <strong style="font-size:0.8rem;">Chọn file .docx để thay nội dung</strong>
        <p style="font-size:0.75rem;">Để trống nếu chỉ đổi tên</p>
      </div>
      <input type="file" id="edit-word-input" accept=".docx" onchange="handleWordFile(this.files[0], true)">
      <div id="edit-file-preview"></div>
    </div>
    <div class="modal-actions">
      <button class="btn-secondary" onclick="closeEditChapterModal()">Hủy</button>
      <button class="btn-primary" onclick="saveEditChapter()">Lưu</button>
    </div>
  </div>
</div>

<!-- Modal sửa truyện -->
<div class="modal-backdrop" id="edit-story-modal">
  <div class="modal-box" style="max-width:500px;">
    <h3>Sửa thông tin truyện</h3>
    <input type="hidden" id="edit-story-id">
    <div class="form-row"><label>Tên truyện</label><input type="text" id="edit-story-title"></div>
    <div class="form-row"><label>Mô tả ngắn</label><textarea id="edit-story-desc" style="min-height:65px;"></textarea></div>
    <div class="form-row-3">
      <div class="form-row" style="margin:0"><label>Thể loại</label>
        <select id="edit-story-genre">
          <option value="Tu Tiên">Tu Tiên</option>
          <option value="Boy Love">Boy Love</option>
          <option value="Xuyên Không/Trùng Sinh">Xuyên Không / Trùng Sinh</option>
        </select>
      </div>
      <div class="form-row" style="margin:0"><label>Dạng</label>
        <select id="edit-story-type">
          <option value="Oneshot">Oneshot</option>
          <option value="Truyện Dài">Truyện Dài</option>
        </select>
      </div>
      <div class="form-row" style="margin:0"><label>Trạng thái</label>
        <select id="edit-story-status">
          <option value="ongoing">Đang ra</option>
          <option value="hiatus">Tạm dừng</option>
          <option value="done">Hoàn thành</option>
        </select>
      </div>
    </div>
    <div class="form-row">
      <label class="checkbox-label" style="margin-top:0.2rem;">
        <input type="checkbox" id="edit-story-hplus">
        <span>Có nội dung H+ (18+)</span>
      </label>
    </div>
    <div class="modal-actions">
      <button class="btn-secondary" onclick="closeEditStoryModal()">Hủy</button>
      <button class="btn-primary" onclick="saveEditStory()">Lưu thay đổi</button>
    </div>
  </div>
</div>

<div class="toast" id="toast"></div>

<script>
// ================================================================
//  CÀI ĐẶT NỘI DUNG
// ================================================================
const TEXT = {
  logo        : "✦ Góc Truyện",
  hero_line1  : "Song tu là đạo",
  hero_line2  : "Song hành là duyên",
  hero_sub    : "Đạo vô vi ấy là yên — truyện đây kể trọn, duyên duyên ắt tìm.",
  about_title : "Về tác giả",
  about_p1    : "Xin chào! Mình là Wien aka Hỏa Ngư, thích viết ra những chuyện mình vu vơ nghĩ đến.",
  about_p2    : "Trang web này là nơi mình lưu giữ và chia sẻ những câu chuyện mình tự viết — từ những mẩu oneshot viết trong đêm khuya đến những bộ truyện dài hơi ấp ủ từ lâu.",
  about_p3    : "Cảm ơn bạn đã ghé thăm và đọc truyện của mình!",
};
const ADMIN_USER = "tam hon thu thai hon dai am duong";
const ADMIN_PASS = "1900100biet";
const STORAGE_KEY = "goctruyen_stories_v1";

// ================================================================
//  DỮ LIỆU MẪU (chỉ dùng lần đầu nếu localStorage trống)
// ================================================================
const DEFAULT_STORIES = [
  {id:1,title:"Mùa Hè Không Tên",genre:"Xuyên Không/Trùng Sinh",type:"Oneshot",status:"done",hplus:false,
   desc:"Câu chuyện về hai người trẻ gặp nhau trong một mùa hè ngắn ngủi, và những kỷ niệm họ để lại cho nhau mãi mãi không phai.",
   cover:{bg:"linear-gradient(135deg,#F59E0B,#D97706)",emoji:"M"},
   chapters:[{title:"Buổi chiều đầu tiên",content:"<p>Hà gặp Minh vào một buổi chiều tháng Sáu, khi cơn mưa đầu mùa còn chưa kịp tan.</p><p>Quán cà phê nhỏ hôm ấy đông hơn thường lệ. Hà chọn chiếc ghế cạnh cửa sổ — để những hạt nước li ti bắn vào tay mà không cảm thấy khó chịu.</p><p>\"Xin lỗi, chỗ này còn trống không?\"</p><p>Cô ngẩng lên. Một anh chàng đứng trước mặt, tóc ướt một nửa, nụ cười hơi ngại ngùng.</p>"}]},
  {id:2,title:"Thiên Đạo Ngược Chiều",genre:"Tu Tiên",type:"Truyện Dài",status:"ongoing",hplus:false,
   desc:"Lâm Phong — một tu sĩ phế vật — vô tình nhận được ký ức của tiền bối mạnh nhất thế giới tu tiên.",
   cover:{bg:"linear-gradient(135deg,#6366F1,#4338CA)",emoji:"T"},
   chapters:[{title:"Phế vật thức tỉnh",content:"<p>Không ai ngờ Lâm Phong sẽ sống qua đêm đó.</p><p>Hắn nằm giữa vũng máu, thân thể kinh mạch tấc tấc đứt gãy.</p>"}]},
  {id:3,title:"Mưa Rơi Ở Thành Phố Người",genre:"Boy Love",type:"Truyện Dài",status:"ongoing",hplus:false,
   desc:"Kiên và Hữu — hai người đàn ông, hai tính cách trái ngược — tình cờ trở thành hàng xóm.",
   cover:{bg:"linear-gradient(135deg,#EC4899,#BE185D)",emoji:"M"},
   chapters:[{title:"Tầng ba, căn 301",content:"<p>Kiên dọn đến căn 301 vào một sáng thứ Tư, khi trời Sài Gòn đang chuẩn bị đổ mưa.</p>"}]}
];

// ================================================================
//  LƯU / TẢI DỮ LIỆU (localStorage)
// ================================================================
function loadStories() {
  try {
    const raw = localStorage.getItem(STORAGE_KEY);
    if (raw) return JSON.parse(raw);
  } catch(e) {}
  return null;
}

function saveStories() {
  try {
    localStorage.setItem(STORAGE_KEY, JSON.stringify(STORIES));
  } catch(e) {
    showToast('⚠️ Không lưu được — bộ nhớ trình duyệt đầy!');
  }
}

// Khởi tạo STORIES
let STORIES = loadStories() || JSON.parse(JSON.stringify(DEFAULT_STORIES));

// ================================================================
//  STATE
// ================================================================
const STATUS_LABELS  = {ongoing:'Đang ra', hiatus:'Tạm dừng', done:'Hoàn thành'};
const STATUS_CLASSES = {ongoing:'tag-status-ongoing', hiatus:'tag-status-hiatus', done:'tag-status-done'};
let activeFilters = {genre:'all', type:'all', status:'all', hplus:false};
let currentStoryId = null, currentChapterIdx = null;
let pendingContent = null, editPendingContent = null;
let editTargetStoryId = null, editTargetChapterIdx = null;
let selectedColor = "linear-gradient(135deg,#F59E0B,#D97706)";
let isLoggedIn = false;
let confirmCallback = null;
let fontSize = 16;

// ================================================================
//  FONT SIZE
// ================================================================
function changeFontSize(delta) {
  fontSize = Math.min(22, Math.max(13, fontSize + delta));
  document.getElementById('read-body').style.fontSize = fontSize + 'px';
  document.getElementById('font-size-label').textContent = fontSize;
}

// ================================================================
//  FILTER & SORT
// ================================================================
function setFilter(key, val, btn) {
  activeFilters[key] = val;
  document.querySelectorAll('[data-fkey="'+key+'"]').forEach(b => b.classList.remove('active'));
  btn.classList.add('active');
  applyFilters();
}
function toggleHplus(btn) {
  activeFilters.hplus = !activeFilters.hplus;
  btn.classList.toggle('active', activeFilters.hplus);
  applyFilters();
}
function applyFilters() {
  const q    = (document.getElementById('search-input').value || '').toLowerCase().trim();
  const sort = document.getElementById('sort-select').value;
  let result = STORIES.filter(s => {
    const okGenre  = activeFilters.genre  === 'all' || s.genre  === activeFilters.genre;
    const okType   = activeFilters.type   === 'all' || s.type   === activeFilters.type;
    const okStatus = activeFilters.status === 'all' || (s.status||'ongoing') === activeFilters.status;
    const okHplus  = !activeFilters.hplus || s.hplus === true;
    const okQuery  = !q || s.title.toLowerCase().includes(q) || (s.desc||'').toLowerCase().includes(q);
    return okGenre && okType && okStatus && okHplus && okQuery;
  });
  result = [...result].sort((a,b) => {
    if (sort === 'newest')   return b.id - a.id;
    if (sort === 'oldest')   return a.id - b.id;
    if (sort === 'az')       return a.title.localeCompare(b.title, 'vi');
    if (sort === 'za')       return b.title.localeCompare(a.title, 'vi');
    if (sort === 'chapters') return b.chapters.length - a.chapters.length;
    return 0;
  });
  renderStories(result);
}

// ================================================================
//  RENDER GRID
// ================================================================
function renderStories(list) {
  const grid = document.getElementById('story-grid');
  grid.innerHTML = '';
  if (!list.length) {
    grid.innerHTML = '<div class="empty-state"><div class="empty-icon">📖</div><p>Không tìm thấy truyện nào phù hợp.</p></div>';
    return;
  }
  list.forEach(s => {
    const el  = document.createElement('div');
    el.className = 'story-card';
    el.onclick   = () => openStory(s.id);
    const st = s.status || 'ongoing';
    const hp = s.hplus ? '<span class="tag tag-hplus">🔞 H+</span>' : '';
    el.innerHTML =
      '<div class="story-card-cover" style="background:'+s.cover.bg+'">'+s.cover.emoji+'</div>'+
      '<div class="story-card-body">'+
        '<div class="tag-row">'+
          '<span class="tag tag-genre">'+s.genre+'</span>'+
          '<span class="tag tag-type">'+s.type+'</span>'+
          '<span class="tag '+STATUS_CLASSES[st]+'">'+STATUS_LABELS[st]+'</span>'+hp+
        '</div>'+
        '<div class="story-title">'+s.title+'</div>'+
        '<div class="story-desc">'+(s.desc||'')+'</div>'+
        '<div class="story-meta"><span>'+s.chapters.length+' chương</span><span class="read-btn">Đọc ngay →</span></div>'+
      '</div>';
    grid.appendChild(el);
  });
}

// ================================================================
//  STORY DETAIL
// ================================================================
function openStory(id) {
  const s = STORIES.find(x => x.id === id);
  if (!s) return;
  currentStoryId = id;
  const st = s.status || 'ongoing';
  const hp = s.hplus ? '<span class="tag tag-hplus">🔞 H+</span>' : '';
  document.getElementById('detail-banner').style.background = s.cover.bg;
  document.getElementById('detail-banner').textContent      = s.cover.emoji;
  document.getElementById('detail-title').textContent       = s.title;
  document.getElementById('detail-desc').textContent        = s.desc || '';
  document.getElementById('detail-tags').innerHTML =
    '<span class="tag tag-genre">'+s.genre+'</span>'+
    '<span class="tag tag-type">'+s.type+'</span>'+
    '<span class="tag '+STATUS_CLASSES[st]+'">'+STATUS_LABELS[st]+'</span>'+hp;
  const items = document.getElementById('chapter-items');
  items.innerHTML = '';
  if (!s.chapters.length) {
    items.innerHTML = '<p style="color:var(--text-hint);font-size:0.85rem;padding:0.5rem 0;">Truyện chưa có chương nào.</p>';
  } else {
    s.chapters.forEach((ch, i) => {
      const el = document.createElement('div');
      el.className = 'chapter-item';
      el.onclick   = () => openChapter(id, i);
      el.innerHTML = '<span class="chapter-num">Chương '+(i+1)+'</span><span class="chapter-name">'+ch.title+'</span><span class="chapter-arrow">›</span>';
      items.appendChild(el);
    });
  }
  showPage('page-story');
}

// ================================================================
//  READING
// ================================================================
function openChapter(sid, idx) {
  const s = STORIES.find(x => x.id === sid);
  if (!s || !s.chapters[idx]) return;
  currentStoryId = sid; currentChapterIdx = idx;
  const ch = s.chapters[idx];
  document.getElementById('nav-story-name').textContent  = s.title;
  document.getElementById('nav-chapter-name').textContent = 'Chương '+(idx+1);
  document.getElementById('read-title').textContent      = ch.title;
  document.getElementById('read-info').textContent       = s.title+' · Chương '+(idx+1)+' / '+s.chapters.length;
  const body = document.getElementById('read-body');
  body.innerHTML  = ch.content || '<p style="color:var(--text-hint)">Chương này chưa có nội dung.</p>';
  body.style.fontSize = fontSize + 'px';
  document.getElementById('font-size-label').textContent = fontSize;
  document.getElementById('btn-prev').disabled = idx === 0;
  document.getElementById('btn-next').disabled = idx === s.chapters.length-1;
  document.getElementById('prog-bar').style.width = '0%';
  showPage('page-reading');
  window.scrollTo(0,0);
}
function navChapter(d) {
  const s = STORIES.find(x => x.id === currentStoryId);
  if (!s) return;
  const ni = currentChapterIdx + d;
  if (ni >= 0 && ni < s.chapters.length) openChapter(currentStoryId, ni);
}
function goBackToStory() { openStory(currentStoryId); }

window.addEventListener('scroll', () => {
  if (!document.getElementById('page-reading').classList.contains('active')) return;
  const body  = document.getElementById('read-body');
  if (!body) return;
  const total   = body.offsetHeight;
  const scrolled = Math.max(0, window.scrollY - body.offsetTop + 120);
  document.getElementById('prog-bar').style.width = Math.min(100, Math.round((scrolled/total)*100)) + '%';
});

// ================================================================
//  ADMIN TABS
// ================================================================
function switchTab(tabId, btn) {
  document.querySelectorAll('.admin-panel').forEach(p => p.classList.remove('active'));
  document.querySelectorAll('.admin-tab').forEach(t => t.classList.remove('active'));
  document.getElementById(tabId).classList.add('active');
  if (btn) btn.classList.add('active');
  if (tabId === 'tab-stories')     refreshManageList();
  if (tabId === 'tab-add-chapter') refreshStorySelect();
}

// ================================================================
//  MANAGE LIST
// ================================================================
function refreshStorySelect() {
  const sel  = document.getElementById('chapter-story-select');
  const prev = sel.value;
  sel.innerHTML = '<option value="">-- Chọn truyện --</option>';
  STORIES.forEach(s => {
    const o = document.createElement('option');
    o.value = s.id; o.textContent = s.title;
    sel.appendChild(o);
  });
  if (prev) sel.value = prev;
}

function refreshManageList() {
  const el    = document.getElementById('story-manage-list');
  const badge = document.getElementById('story-count-badge');
  badge.textContent = '('+STORIES.length+' truyện)';
  if (!STORIES.length) {
    el.innerHTML = '<p style="color:var(--text-hint);font-size:0.85rem;">Chưa có truyện nào. Vào tab "Thêm truyện" để bắt đầu!</p>';
    return;
  }
  el.innerHTML = '';
  STORIES.forEach(s => {
    const st   = s.status || 'ongoing';
    const wrap = document.createElement('div');
    wrap.className = 'story-manage-item';
    wrap.innerHTML =
      '<div class="story-manage-header" onclick="toggleManageBody('+s.id+')">'+
        '<div class="story-manage-cover" style="background:'+s.cover.bg+'">'+s.cover.emoji+'</div>'+
        '<div class="story-manage-info">'+
          '<div class="story-manage-name">'+s.title+
            (s.hplus?' <span style="font-size:0.67rem;background:var(--red-bg);color:var(--red);padding:1px 6px;border-radius:99px;">H+</span>':'')+
          '</div>'+
          '<div class="story-manage-meta">'+s.genre+' · '+s.type+' · '+STATUS_LABELS[st]+' · '+s.chapters.length+' chương</div>'+
        '</div>'+
        '<div class="story-manage-actions" onclick="event.stopPropagation()">'+
          '<button class="btn-sm edit-sm" onclick="openEditStoryModal('+s.id+')">Sửa</button>'+
          '<button class="btn-sm del" onclick="confirmAction(\'Xóa truyện &quot;'+s.title+'&quot;? Tất cả '+s.chapters.length+' chương sẽ bị xóa.\', ()=>doDeleteStory('+s.id+'))">Xóa</button>'+
        '</div>'+
        '<span style="color:var(--text-hint);font-size:0.75rem;margin-left:0.25rem;">▾</span>'+
      '</div>'+
      '<div class="story-manage-body" id="manage-body-'+s.id+'">'+
        renderChapterManageList(s)+
        '<div style="margin-top:0.75rem;padding-top:0.75rem;border-top:1px solid var(--border);">'+
          '<button class="btn-sm" onclick="quickAddChapter('+s.id+')" style="font-size:0.78rem;">+ Thêm chương vào truyện này</button>'+
        '</div>'+
      '</div>';
    el.appendChild(wrap);
  });
}

function renderChapterManageList(s) {
  if (!s.chapters.length) return '<p style="color:var(--text-hint);font-size:0.82rem;padding:0.25rem 0;">Chưa có chương nào.</p>';
  return s.chapters.map((ch, i) =>
    '<div class="chapter-manage-item">'+
      '<span class="chapter-manage-num">Chương '+(i+1)+'</span>'+
      '<span class="chapter-manage-name">'+ch.title+'</span>'+
      '<div class="chapter-manage-actions">'+
        '<button class="btn-sm edit-sm" onclick="openEditChapterModal('+s.id+','+i+')">Sửa</button>'+
        '<button class="btn-sm" onclick="moveChapter('+s.id+','+i+',-1)" '+(i===0?'disabled':'')+' title="Lên">↑</button>'+
        '<button class="btn-sm" onclick="moveChapter('+s.id+','+i+',1)" '+(i===s.chapters.length-1?'disabled':'')+' title="Xuống">↓</button>'+
        '<button class="btn-sm del" onclick="confirmAction(\'Xóa chương &quot;'+ch.title+'&quot;?\', ()=>doDeleteChapter('+s.id+','+i+'))">Xóa</button>'+
      '</div>'+
    '</div>'
  ).join('');
}

function toggleManageBody(id) {
  document.getElementById('manage-body-'+id).classList.toggle('open');
}

function quickAddChapter(storyId) {
  document.querySelectorAll('.admin-tab').forEach((t,i) => t.classList.toggle('active', i===2));
  document.querySelectorAll('.admin-panel').forEach(p => p.classList.remove('active'));
  document.getElementById('tab-add-chapter').classList.add('active');
  refreshStorySelect();
  document.getElementById('chapter-story-select').value = storyId;
}

function moveChapter(storyId, idx, dir) {
  const s  = STORIES.find(x => x.id === storyId);
  if (!s) return;
  const ni = idx + dir;
  if (ni < 0 || ni >= s.chapters.length) return;
  [s.chapters[idx], s.chapters[ni]] = [s.chapters[ni], s.chapters[idx]];
  saveStories();
  refreshManageList();
  document.getElementById('manage-body-'+storyId).classList.add('open');
  showToast('Đã đổi thứ tự chương.');
}

// ================================================================
//  THÊM TRUYỆN
// ================================================================
document.querySelectorAll('.color-opt').forEach(el => {
  el.onclick = () => {
    document.querySelectorAll('.color-opt').forEach(e => e.classList.remove('selected'));
    el.classList.add('selected');
    selectedColor = el.dataset.color;
  };
});

function addStory() {
  const title  = document.getElementById('new-title').value.trim();
  const desc   = document.getElementById('new-desc').value.trim();
  const genre  = document.getElementById('new-genre').value;
  const type   = document.getElementById('new-type').value;
  const status = document.getElementById('new-status').value;
  const hplus  = document.getElementById('new-hplus').checked;
  const emoji  = document.getElementById('new-emoji').value.trim() || (title[0]||'✦');
  if (!title) { showToast('⚠️ Vui lòng nhập tên truyện!'); return; }
  const newId = STORIES.length ? Math.max(...STORIES.map(s=>s.id))+1 : 1;
  STORIES.push({id:newId, title, genre, type, status, hplus, desc, cover:{bg:selectedColor, emoji}, chapters:[]});
  saveStories(); // ← LƯU NGAY
  ['new-title','new-desc','new-emoji'].forEach(id => document.getElementById(id).value='');
  document.getElementById('new-hplus').checked = false;
  applyFilters();
  showToast('✅ Đã thêm truyện "'+title+'" — hiện trên trang chủ rồi!');
}

// ================================================================
//  XÓA TRUYỆN
// ================================================================
function doDeleteStory(id) {
  STORIES = STORIES.filter(s => s.id !== id);
  saveStories(); // ← LƯU NGAY
  refreshManageList(); applyFilters();
  showToast('Đã xóa truyện.');
}

// ================================================================
//  SỬA TRUYỆN
// ================================================================
function openEditStoryModal(id) {
  const s = STORIES.find(x => x.id === id);
  if (!s) return;
  document.getElementById('edit-story-id').value        = id;
  document.getElementById('edit-story-title').value     = s.title;
  document.getElementById('edit-story-desc').value      = s.desc || '';
  document.getElementById('edit-story-genre').value     = s.genre;
  document.getElementById('edit-story-type').value      = s.type;
  document.getElementById('edit-story-status').value    = s.status || 'ongoing';
  document.getElementById('edit-story-hplus').checked   = s.hplus || false;
  document.getElementById('edit-story-modal').classList.add('open');
}
function closeEditStoryModal() { document.getElementById('edit-story-modal').classList.remove('open'); }
function saveEditStory() {
  const id    = parseInt(document.getElementById('edit-story-id').value);
  const s     = STORIES.find(x => x.id === id);
  if (!s) return;
  const title = document.getElementById('edit-story-title').value.trim();
  if (!title) { showToast('⚠️ Nhập tên truyện!'); return; }
  s.title  = title;
  s.desc   = document.getElementById('edit-story-desc').value.trim();
  s.genre  = document.getElementById('edit-story-genre').value;
  s.type   = document.getElementById('edit-story-type').value;
  s.status = document.getElementById('edit-story-status').value;
  s.hplus  = document.getElementById('edit-story-hplus').checked;
  saveStories(); // ← LƯU NGAY
  closeEditStoryModal();
  refreshManageList(); applyFilters();
  document.getElementById('manage-body-'+id).classList.add('open');
  showToast('✅ Đã lưu thay đổi cho "'+title+'"');
}

// ================================================================
//  THÊM CHƯƠNG
// ================================================================
const uploadZone = document.getElementById('upload-zone');
uploadZone.addEventListener('dragover', e => { e.preventDefault(); uploadZone.classList.add('drag-over'); });
uploadZone.addEventListener('dragleave', () => uploadZone.classList.remove('drag-over'));
uploadZone.addEventListener('drop', e => {
  e.preventDefault(); uploadZone.classList.remove('drag-over');
  const f = e.dataTransfer.files[0];
  if (f && f.name.toLowerCase().endsWith('.docx')) handleWordFile(f);
  else showToast('⚠️ Chỉ hỗ trợ file .docx');
});

function handleWordFile(file, isEdit) {
  if (!file || !file.name.toLowerCase().endsWith('.docx')) { showToast('⚠️ Chỉ hỗ trợ file .docx'); return; }
  showToast('⏳ Đang đọc file...');
  const reader = new FileReader();
  reader.onload = e => {
    if (typeof mammoth === 'undefined') { showToast('❌ Thư viện chưa tải xong, thử lại.'); return; }
    mammoth.convertToHtml({arrayBuffer: e.target.result})
      .then(r => {
        if (isEdit) {
          editPendingContent = r.value;
          document.getElementById('edit-file-preview').innerHTML =
            '<div class="file-preview-box"><span>📄 '+file.name+'</span><button onclick="editPendingContent=null;this.parentElement.parentElement.innerHTML=\'\'">✕</button></div>';
        } else {
          pendingContent = r.value;
          document.getElementById('file-preview').innerHTML =
            '<div class="file-preview-box"><span>📄 '+file.name+'</span><button onclick="clearWord()">✕</button></div>';
        }
        showToast('✅ Đọc file Word thành công!');
      })
      .catch(() => showToast('❌ Không đọc được file.'));
  };
  reader.onerror = () => showToast('❌ Lỗi đọc file.');
  reader.readAsArrayBuffer(file);
}

function clearWord() {
  pendingContent = null;
  document.getElementById('file-preview').innerHTML = '';
  document.getElementById('word-file-input').value  = '';
}

function addChapter() {
  const sid   = parseInt(document.getElementById('chapter-story-select').value);
  const title = document.getElementById('new-chapter-title').value.trim();
  if (!sid)            { showToast('⚠️ Chọn truyện trước!'); return; }
  if (!title)          { showToast('⚠️ Nhập tên chương!'); return; }
  if (!pendingContent) { showToast('⚠️ Upload file Word trước!'); return; }
  const story = STORIES.find(s => s.id === sid);
  if (!story) return;
  story.chapters.push({title, content: pendingContent});
  saveStories(); // ← LƯU NGAY
  document.getElementById('new-chapter-title').value = '';
  clearWord();
  applyFilters();
  showToast('✅ Đã thêm "'+title+'" — hiện trên trang chủ rồi!');
}

// ================================================================
//  SỬA / XÓA CHƯƠNG
// ================================================================
function openEditChapterModal(storyId, chIdx) {
  editTargetStoryId  = storyId;
  editTargetChapterIdx = chIdx;
  editPendingContent = null;
  const s = STORIES.find(x => x.id === storyId);
  document.getElementById('edit-chapter-name-input').value = s.chapters[chIdx].title;
  document.getElementById('edit-file-preview').innerHTML   = '';
  document.getElementById('edit-word-input').value         = '';
  document.getElementById('edit-chapter-modal').classList.add('open');
}
function closeEditChapterModal() {
  document.getElementById('edit-chapter-modal').classList.remove('open');
  editTargetStoryId = null; editTargetChapterIdx = null; editPendingContent = null;
}
function saveEditChapter() {
  const s    = STORIES.find(x => x.id === editTargetStoryId);
  if (!s) return;
  const name = document.getElementById('edit-chapter-name-input').value.trim();
  if (!name) { showToast('⚠️ Nhập tên chương!'); return; }
  s.chapters[editTargetChapterIdx].title = name;
  if (editPendingContent) s.chapters[editTargetChapterIdx].content = editPendingContent;
  saveStories(); // ← LƯU NGAY
  closeEditChapterModal();
  refreshManageList();
  document.getElementById('manage-body-'+editTargetStoryId).classList.add('open');
  showToast('✅ Đã lưu chương "'+name+'"');
}

function doDeleteChapter(storyId, chIdx) {
  const s = STORIES.find(x => x.id === storyId);
  if (!s) return;
  s.chapters.splice(chIdx, 1);
  saveStories(); // ← LƯU NGAY
  refreshManageList();
  document.getElementById('manage-body-'+storyId).classList.add('open');
  applyFilters();
  showToast('Đã xóa chương.');
}

// ================================================================
//  CONFIRM MODAL
// ================================================================
function confirmAction(msg, cb) {
  confirmCallback = cb;
  document.getElementById('modal-msg').innerHTML = msg;
  document.getElementById('modal-confirm-btn').onclick = () => { closeModal(); cb(); };
  document.getElementById('confirm-modal').classList.add('open');
}
function closeModal() { document.getElementById('confirm-modal').classList.remove('open'); confirmCallback = null; }
document.getElementById('confirm-modal').addEventListener('click',     function(e){ if(e.target===this) closeModal(); });
document.getElementById('edit-story-modal').addEventListener('click',  function(e){ if(e.target===this) closeEditStoryModal(); });
document.getElementById('edit-chapter-modal').addEventListener('click',function(e){ if(e.target===this) closeEditChapterModal(); });

// ================================================================
//  XUẤT HTML (backup / GitHub)
// ================================================================
function exportHTML() {
  const storiesJSON = JSON.stringify(STORIES, null, 2);
  fetch(window.location.href)
    .then(r => r.text())
    .then(src => {
      let out = src.replace(/const DEFAULT_STORIES = \[[\s\S]*?\];\n/, 'const DEFAULT_STORIES = '+storiesJSON+';\n');
      if (!out.includes(storiesJSON.slice(0,40))) {
        out = src.replace(/const DEFAULT_STORIES = \[[\s\S]*?\];/, 'const DEFAULT_STORIES = '+storiesJSON+';');
      }
      downloadHTML(out);
    })
    .catch(() => {
      let src = document.documentElement.outerHTML;
      src = src.replace(/const DEFAULT_STORIES = \[[\s\S]*?\];/, 'const DEFAULT_STORIES = '+storiesJSON+';');
      downloadHTML(src);
    });
}
function downloadHTML(content) {
  const blob = new Blob([content], {type:'text/html;charset=utf-8'});
  const a    = document.createElement('a');
  a.href     = URL.createObjectURL(blob);
  a.download = 'index.html';
  document.body.appendChild(a); a.click();
  setTimeout(() => { URL.revokeObjectURL(a.href); a.remove(); }, 1000);
  showToast('✅ Đã tải file HTML! Xem hướng dẫn GitHub trong tab Xuất file.');
}

// ================================================================
//  ĐĂNG NHẬP / ĐĂNG XUẤT
// ================================================================
function goAdmin() {
  if (isLoggedIn) {
    showPage('page-admin'); refreshManageList();
  } else {
    document.getElementById('login-user').value = '';
    document.getElementById('login-pass').value = '';
    document.getElementById('login-error').style.display = 'none';
    showPage('page-login');
    setTimeout(() => document.getElementById('login-user').focus(), 150);
  }
}
function doLogin() {
  const u = document.getElementById('login-user').value.trim();
  const p = document.getElementById('login-pass').value;
  if (u === ADMIN_USER && p === ADMIN_PASS) {
    isLoggedIn = true;
    document.getElementById('login-error').style.display = 'none';
    showPage('page-admin'); refreshManageList();
  } else {
    document.getElementById('login-error').style.display = 'block';
    document.getElementById('login-pass').value = '';
    document.getElementById('login-pass').focus();
  }
}
function doLogout() { isLoggedIn = false; goHome(); showToast('Đã đăng xuất.'); }

// ================================================================
//  NAVIGATION
// ================================================================
function showPage(id) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.getElementById(id).classList.add('active');
  window.scrollTo(0,0);
  document.querySelectorAll('nav a').forEach(a => a.classList.remove('active'));
  const map = {'page-home':'nav-home','page-about':'nav-about','page-admin':'nav-admin','page-login':'nav-admin'};
  if (map[id]) document.getElementById(map[id]).classList.add('active');
}
function goHome()  { showPage('page-home'); applyFilters(); }
function goAbout() { showPage('page-about'); }

// ================================================================
//  TOAST
// ================================================================
let toastTimer = null;
function showToast(msg) {
  const t = document.getElementById('toast');
  t.textContent = msg; t.classList.add('show');
  clearTimeout(toastTimer);
  toastTimer = setTimeout(() => t.classList.remove('show'), 3200);
}

// ================================================================
//  APPLY TEXT CONFIG
// ================================================================
function applyTextConfig() {
  document.querySelector('.logo').textContent        = TEXT.logo;
  document.getElementById('hero-line1').textContent  = TEXT.hero_line1;
  document.getElementById('hero-line2').textContent  = TEXT.hero_line2;
  document.getElementById('hero-sub').textContent    = TEXT.hero_sub;
  document.getElementById('about-title').textContent = TEXT.about_title;
  document.getElementById('about-p1').textContent    = TEXT.about_p1;
  document.getElementById('about-p2').textContent    = TEXT.about_p2;
  document.getElementById('about-p3').textContent    = TEXT.about_p3;
  document.title = 'Góc Truyện — Wien';
}

// ================================================================
//  INIT
// ================================================================
applyTextConfig();
applyFilters();
</script>
</body>
</html>
