<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="theme-color" content="#0b0d0c">
  <meta name="description" content="Kiwify Mini Dashboard — painel demonstrativo de vendas e produtos.">
  <title>Kiwify Mini Dashboard</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="style.css">
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
</head>
<body>
  <div class="app-shell">
    <aside class="sidebar" id="sidebar">
      <a class="brand" href="#" aria-label="Kiwify Mini Dashboard - início">
        <span class="brand-mark">K</span>
        <span class="brand-copy">mini<span>dashboard</span></span>
      </a>
      <div class="workspace-label">ÁREA DE TRABALHO</div>
      <nav class="nav-list" aria-label="Menu principal">
        <button class="nav-item active" data-page="dashboard"><span class="nav-icon">▦</span>Dashboard</button>
        <button class="nav-item" data-page="products"><span class="nav-icon">▣</span>Produtos</button>
        <button class="nav-item" data-page="sales"><span class="nav-icon">↗</span>Vendas</button>
        <button class="nav-item" data-page="finance"><span class="nav-icon">◈</span>Financeiro</button>
      </nav>
      <div class="sidebar-bottom">
        <div class="demo-note"><span class="status-dot"></span><div><strong>Modo demonstração</strong><small>Dados salvos neste dispositivo</small></div></div>
        <button class="nav-item" data-page="settings"><span class="nav-icon">⚙</span>Configurações</button>
        <div class="profile">
          <div class="avatar">A</div><div class="profile-copy"><strong>Área de teste</strong><small>Conta demonstrativa</small></div><span class="more">•••</span>
        </div>
      </div>
    </aside>

    <main class="main-content">
      <header class="topbar">
        <button class="mobile-menu" id="mobileMenu" aria-label="Abrir menu">☰</button>
        <div class="breadcrumb">Workspace <span>/</span> <strong id="breadcrumbCurrent">Dashboard</strong></div>
        <div class="top-actions"><span class="demo-pill"><i></i> DEMO</span><button class="icon-button" id="resetButton" title="Restaurar dados de demonstração" aria-label="Restaurar dados">↻</button></div>
      </header>

      <section class="page active-page" id="page-dashboard">
        <div class="page-heading"><div><p class="eyebrow">VISÃO GERAL</p><h1>Dashboard</h1><p class="subtitle">Acompanhe o desempenho da sua operação.</p></div><div class="date-chip" id="todayLabel">Hoje</div></div>
        <div class="stats-grid">
          <article class="stat-card"><div class="stat-top"><span>Saldo disponível</span><span class="stat-icon green">↗</span></div><div class="stat-value" id="dashBalance">R$ 0,00</div><div class="stat-foot positive">● Valor demonstrativo</div></article>
          <article class="stat-card"><div class="stat-top"><span>Vendas totais</span><span class="stat-icon">⌁</span></div><div class="stat-value" id="dashRevenue">R$ 0,00</div><div class="stat-foot muted">Soma das vendas registradas</div></article>
          <article class="stat-card"><div class="stat-top"><span>Pedidos</span><span class="stat-icon">▤</span></div><div class="stat-value" id="dashOrders">0</div><div class="stat-foot muted">Transações cadastradas</div></article>
          <article class="stat-card"><div class="stat-top"><span>Produtos ativos</span><span class="stat-icon">◇</span></div><div class="stat-value" id="dashProducts">0</div><div class="stat-foot muted">Itens no seu catálogo</div></article>
        </div>
        <div class="content-grid">
          <article class="panel chart-panel"><div class="panel-heading"><div><h2>Desempenho de vendas</h2><p>Resumo dos últimos 7 dias</p></div><span class="chart-tag">Últimos 7 dias</span></div><div class="chart-wrap"><canvas id="salesChart" aria-label="Gráfico de vendas dos últimos sete dias"></canvas></div></article>
          <article class="panel"><div class="panel-heading"><div><h2>Resumo financeiro</h2><p>Visão geral do saldo</p></div><span class="panel-more">•••</span></div><div class="finance-summary"><div class="finance-line"><span><i class="legend-dot available"></i>Disponível</span><strong id="summaryAvailable">R$ 0,00</strong></div><div class="finance-line"><span><i class="legend-dot pending"></i>Pendente</span><strong id="summaryPending">R$ 0,00</strong></div><div class="finance-divider"></div><div class="finance-total"><span>Total</span><strong id="summaryTotal">R$ 0,00</strong></div></div><button class="text-link" data-goto="finance">Ver financeiro <span>→</span></button></article>
        </div>
        <article class="panel table-panel"><div class="panel-heading"><div><h2>Vendas recentes</h2><p>As últimas movimentações da sua loja</p></div><button class="subtle-button" data-goto="sales">Ver todas</button></div><div class="table-scroll"><table><thead><tr><th>Produto</th><th>Data</th><th>Valor</th><th>Status</th></tr></thead><tbody id="recentSalesBody"></tbody></table></div></article>
      </section>

      <section class="page" id="page-products">
        <div class="page-heading"><div><p class="eyebrow">CATÁLOGO</p><h1>Produtos</h1><p class="subtitle">Gerencie os produtos da sua vitrine.</p></div><button class="primary-button" id="addProductButton">＋ Novo produto</button></div>
        <div class="toolbar"><div class="search-box"><span>⌕</span><input id="productSearch" type="search" placeholder="Buscar produto..." aria-label="Buscar produto"></div><span class="result-count" id="productCount">0 produtos</span></div>
        <div class="panel table-panel"><div class="table-scroll"><table><thead><tr><th>Produto</th><th>Preço</th><th>Vendas</th><th>Status</th><th>Ações</th></tr></thead><tbody id="productsBody"></tbody></table></div></div>
      </section>

      <section class="page" id="page-sales">
        <div class="page-heading"><div><p class="eyebrow">TRANSAÇÕES</p><h1>Vendas</h1><p class="subtitle">Consulte o histórico de pedidos.</p></div></div>
        <div class="stats-grid compact-stats"><article class="stat-card"><div class="stat-top"><span>Vendas registradas</span><span class="stat-icon">↗</span></div><div class="stat-value" id="salesCount">0</div></article><article class="stat-card"><div class="stat-top"><span>Valor total</span><span class="stat-icon green">R$</span></div><div class="stat-value" id="salesTotal">R$ 0,00</div></article></div>
        <div class="toolbar"><div class="search-box"><span>⌕</span><input id="salesSearch" type="search" placeholder="Buscar por produto..." aria-label="Buscar vendas"></div><select id="salesFilter" class="filter-select" aria-label="Filtrar por status"><option value="all">Todos os status</option><option value="approved">Aprovadas</option><option value="pending">Pendentes</option></select></div>
        <div class="panel table-panel"><div class="table-scroll"><table><thead><tr><th>Produto</th><th>Comprador</th><th>Data</th><th>Valor</th><th>Status</th></tr></thead><tbody id="salesBody"></tbody></table></div></div>
      </section>

      <section class="page" id="page-finance">
        <div class="page-heading"><div><p class="eyebrow">GESTÃO DE SALDO</p><h1>Financeiro</h1><p class="subtitle">Acompanhe os valores da conta demonstrativa.</p></div></div>
        <div class="stats-grid"><article class="stat-card"><div class="stat-top"><span>Saldo disponível</span><span class="stat-icon green">↗</span></div><div class="stat-value" id="financeAvailable">R$ 0,00</div><div class="stat-foot positive">Pronto para movimentação (simulação)</div></article><article class="stat-card"><div class="stat-top"><span>Saldo pendente</span><span class="stat-icon">◷</span></div><div class="stat-value" id="financePending">R$ 0,00</div><div class="stat-foot muted">Pagamentos aguardando confirmação</div></article><article class="stat-card"><div class="stat-top"><span>Volume total</span><span class="stat-icon">◈</span></div><div class="stat-value" id="financeGross">R$ 0,00</div><div class="stat-foot muted">Aprovadas + pendentes</div></article></div>
        <article class="panel table-panel"><div class="panel-heading"><div><h2>Movimentações</h2><p>Registro das vendas demonstrativas</p></div></div><div class="table-scroll"><table><thead><tr><th>Descrição</th><th>Data</th><th>Tipo</th><th>Valor</th><th>Status</th></tr></thead><tbody id="financeBody"></tbody></table></div></article>
        <p class="disclaimer">Este painel é uma demonstração independente. Não movimenta dinheiro e não está conectado à Kiwify.</p>
      </section>

      <section class="page" id="page-settings">
        <div class="page-heading"><div><p class="eyebrow">PREFERÊNCIAS</p><h1>Configurações</h1><p class="subtitle">Personalize sua experiência neste dispositivo.</p></div></div>
        <article class="panel settings-panel"><div class="settings-row"><div><h2>Dados de demonstração</h2><p>Os produtos e registros ficam salvos apenas neste navegador.</p></div><button class="subtle-button" id="settingsReset">Restaurar dados</button></div><div class="settings-row"><div><h2>Identidade visual</h2><p>Tema escuro com detalhes em verde.</p></div><span class="setting-value"><i class="status-dot"></i> Dark Mode</span></div><div class="settings-row"><div><h2>Sobre o projeto</h2><p>Projeto independente para estudo e demonstração.</p></div><span class="setting-value">v1.0.0</span></div></article>
      </section>
      <footer class="footer">Kiwify Mini Dashboard <span>•</span> Projeto demonstrativo independente</footer>
    </main>
  </div>

  <div class="modal-backdrop" id="productModal" aria-hidden="true">
    <div class="modal" role="dialog" aria-modal="true" aria-labelledby="modalTitle">
      <div class="modal-heading"><div><p class="eyebrow">CATÁLOGO</p><h2 id="modalTitle">Adicionar produto</h2></div><button class="close-button" id="closeModal" aria-label="Fechar">×</button></div>
      <form id="productForm">
        <input type="hidden" id="productId">
        <label for="productName">Nome do produto</label><input id="productName" maxlength="60" required placeholder="Ex.: E-book de receitas">
        <label for="productPrice">Preço (R$)</label><input id="productPrice" type="number" min="0.01" step="0.01" required placeholder="49.90">
        <div class="modal-actions"><button type="button" class="subtle-button" id="cancelModal">Cancelar</button><button type="submit" class="primary-button">Salvar produto</button></div>
      </form>
    </div>
  </div>
  <div class="toast" id="toast" role="status" aria-live="polite"></div>
  <script src="script.js"></script>
</body>
</html>
@import url('https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700;800&display=swap');
:root{--bg:#0b0d0c;--panel:#151a17;--panel2:#191f1c;--line:#252d28;--green:#00d084;--green-soft:rgba(0,208,132,.12);--text:#f3f6f4;--muted:#87918b;--red:#ff7272;--yellow:#e8bb62;--radius:16px}
*{box-sizing:border-box}body{margin:0;background:var(--bg);color:var(--text);font-family:'DM Sans',sans-serif;font-size:14px}button,input,select{font:inherit}button{cursor:pointer}.app-shell{min-height:100vh}.sidebar{width:248px;position:fixed;inset:0 auto 0 0;background:#101411;border-right:1px solid var(--line);padding:27px 17px 18px;display:flex;flex-direction:column;z-index:20}.brand{display:flex;align-items:center;gap:11px;text-decoration:none;color:var(--text);padding:0 8px 39px}.brand-mark{width:34px;height:34px;border-radius:11px;background:var(--green);color:#062719;display:grid;place-items:center;font-size:21px;font-weight:800}.brand-copy{font-size:16px;font-weight:800;letter-spacing:-.6px}.brand-copy span{display:block;font-size:10px;color:var(--muted);font-weight:500;letter-spacing:1.5px;text-transform:uppercase;margin-top:1px}.workspace-label,.eyebrow{font-size:10px;letter-spacing:1.5px;color:#6f7c74;font-weight:700}.workspace-label{padding:0 10px 12px}.nav-list{display:grid;gap:5px}.nav-item{width:100%;border:0;background:transparent;color:#9ba69f;padding:12px 13px;border-radius:10px;display:flex;align-items:center;gap:13px;text-align:left;font-weight:600;transition:.2s}.nav-item:hover{background:#1a211d;color:white}.nav-item.active{background:var(--green-soft);color:var(--green)}.nav-icon{width:18px;text-align:center;font-size:18px}.sidebar-bottom{margin-top:auto}.demo-note{display:flex;gap:10px;align-items:center;padding:13px 10px;margin:0 0 12px;background:#171e19;border:1px solid #26332b;border-radius:12px}.status-dot{width:7px;height:7px;display:inline-block;border-radius:50%;background:var(--green);box-shadow:0 0 10px #00d08477}.demo-note strong,.profile-copy strong{display:block;font-size:11px}.demo-note small,.profile-copy small{display:block;color:var(--muted);font-size:10px;margin-top:3px}.profile{border-top:1px solid var(--line);margin-top:15px;padding:17px 5px 0;display:flex;align-items:center;gap:10px}.avatar{width:34px;height:34px;border-radius:50%;background:#294a3a;color:#8ef0c4;display:grid;place-items:center;font-weight:700}.profile-copy{flex:1}.more{color:var(--muted);letter-spacing:2px}.main-content{margin-left:248px;min-height:100vh;padding:0 38px;max-width:1800px}.topbar{height:72px;border-bottom:1px solid var(--line);display:flex;align-items:center;justify-content:space-between}.breadcrumb{color:var(--muted);font-size:12px}.breadcrumb span{padding:0 9px;color:#465149}.breadcrumb strong{color:#e5ebe7;font-weight:600}.top-actions{display:flex;align-items:center;gap:12px}.demo-pill{font-size:9px;letter-spacing:1px;color:var(--green);background:var(--green-soft);border:1px solid #164b35;padding:6px 9px;border-radius:20px;font-weight:800}.demo-pill i{display:inline-block;width:5px;height:5px;border-radius:50%;background:var(--green);vertical-align:middle;margin-right:5px}.icon-button,.mobile-menu,.close-button{border:1px solid var(--line);background:var(--panel);color:#aab4ad;border-radius:9px;width:34px;height:34px}.mobile-menu{display:none}.page{display:none;padding:34px 0 20px;animation:fade .25s ease}.page.active-page{display:block}@keyframes fade{from{opacity:.3;transform:translateY(4px)}to{opacity:1;transform:none}}.page-heading{display:flex;align-items:flex-end;justify-content:space-between;margin-bottom:25px}.eyebrow{margin:0 0 8px;color:var(--green)}h1{font-size:29px;letter-spacing:-1.1px;margin:0;font-weight:700}.subtitle{color:var(--muted);margin:7px 0 0;font-size:13px}.date-chip,.chart-tag{border:1px solid var(--line);border-radius:8px;color:#aeb8b1;padding:8px 11px;font-size:11px}.stats-grid{display:grid;grid-template-columns:repeat(4,minmax(0,1fr));gap:15px;margin-bottom:17px}.stat-card,.panel{background:var(--panel);border:1px solid var(--line);border-radius:var(--radius)}.stat-card{padding:17px 18px;min-height:128px}.stat-top{display:flex;align-items:center;justify-content:space-between;color:#a2ada5;font-size:11px;font-weight:500}.stat-icon{width:29px;height:29px;display:grid;place-items:center;border-radius:9px;background:#202823;color:#b7c3bb;font-size:15px}.stat-icon.green{color:var(--green);background:var(--green-soft)}.stat-value{font-size:25px;font-weight:700;letter-spacing:-.8px;margin:14px 0 7px}.stat-foot{font-size:10px}.positive{color:var(--green)}.muted{color:var(--muted)}.content-grid{display:grid;grid-template-columns:minmax(0,1.7fr) minmax(250px,1fr);gap:15px;margin-bottom:17px}.panel{padding:19px}.panel-heading{display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:19px}.panel-heading h2,.settings-row h2{font-size:13px;margin:0;font-weight:700}.panel-heading p,.settings-row p{font-size:11px;color:var(--muted);margin:5px 0 0}.panel-more{color:var(--muted);letter-spacing:2px}.chart-wrap{height:218px;position:relative}.finance-summary{padding:8px 0 13px}.finance-line,.finance-total{display:flex;align-items:center;justify-content:space-between;margin:15px 0;font-size:11px;color:#aab4ad}.finance-line strong,.finance-total strong{color:#eef3ef;font-size:12px}.legend-dot{display:inline-block;width:7px;height:7px;border-radius:50%;margin-right:8px}.available{background:var(--green)}.pending{background:var(--yellow)}.finance-divider{border-top:1px solid var(--line);margin-top:20px}.finance-total{margin-bottom:4px}.finance-total strong{font-size:17px}.text-link{border:0;background:none;color:var(--green);padding:9px 0 0;font-size:11px;font-weight:700}.text-link span{margin-left:5px}.table-panel{padding:19px 0 0;overflow:hidden}.table-panel>.panel-heading{padding:0 19px}.subtle-button{background:#202722;border:1px solid #303b34;color:#c3ccc6;border-radius:8px;padding:8px 12px;font-size:10px;font-weight:600}.subtle-button:hover{border-color:#4b6555;color:white}.table-scroll{overflow-x:auto}table{width:100%;border-collapse:collapse;white-space:nowrap;text-align:left}th{font-size:9px;text-transform:uppercase;letter-spacing:1px;color:#77837b;font-weight:700;background:#171d19;padding:12px 19px}td{padding:14px 19px;border-top:1px solid #222a25;color:#b7c1ba;font-size:11px}td:first-child{color:#e4eae6;font-weight:600}.empty-state{text-align:center;padding:28px;color:var(--muted)}.status{display:inline-flex;align-items:center;gap:6px;padding:5px 8px;border-radius:20px;font-size:9px;font-weight:700}.status:before{content:'';width:5px;height:5px;border-radius:50%;background:currentColor}.status.approved{background:var(--green-soft);color:var(--green)}.status.pending{background:#3a3020;color:var(--yellow)}.row-actions{display:flex;gap:6px}.row-action{border:1px solid var(--line);background:#1b221e;color:#aeb9b1;border-radius:6px;padding:5px 8px;font-size:10px}.row-action.delete{color:#f28c8c}.toolbar{display:flex;align-items:center;gap:12px;margin:0 0 15px}.search-box{display:flex;align-items:center;gap:9px;background:var(--panel);border:1px solid var(--line);border-radius:9px;padding:0 12px;width:min(330px,100%);height:38px;color:var(--muted)}.search-box input{background:none;border:0;outline:0;color:var(--text);width:100%;font-size:11px}.search-box input::placeholder{color:#68746c}.result-count{margin-left:auto;color:var(--muted);font-size:10px}.filter-select{height:38px;background:var(--panel);border:1px solid var(--line);border-radius:9px;color:#c4cec7;padding:0 10px;font-size:11px}.compact-stats{grid-template-columns:repeat(2,minmax(0,1fr));max-width:550px}.compact-stats .stat-card{min-height:105px}.compact-stats .stat-value{margin:10px 0 0}.primary-button{background:var(--green);color:#062719;border:0;border-radius:9px;padding:11px 15px;font-size:11px;font-weight:800;transition:.2s}.primary-button:hover{background:#20e49b;transform:translateY(-1px)}.disclaimer{color:#77837b;font-size:10px;margin:14px 2px}.settings-panel{padding:0 20px}.settings-row{display:flex;align-items:center;justify-content:space-between;gap:20px;padding:20px 0;border-bottom:1px solid var(--line)}.settings-row:last-child{border:0}.setting-value{color:#b8c2bb;font-size:11px}.setting-value .status-dot{margin-right:7px}.footer{padding:25px 0 20px;color:#59645d;font-size:10px}.footer span{padding:0 5px;color:var(--green)}.modal-backdrop{position:fixed;inset:0;background:#000b;display:none;align-items:center;justify-content:center;padding:18px;z-index:50}.modal-backdrop.open{display:flex}.modal{width:min(430px,100%);background:#151b17;border:1px solid #303b34;border-radius:17px;padding:22px;box-shadow:0 25px 90px #0009;animation:fade .2s ease}.modal-heading{display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:22px}.modal-heading h2{margin:0;font-size:19px}.close-button{font-size:21px}.modal form{display:grid;gap:9px}.modal label{font-size:11px;color:#aab5ad;margin-top:5px}.modal input{width:100%;background:#0d120f;border:1px solid #303a33;border-radius:8px;padding:12px;color:white;outline:0}.modal input:focus{border-color:var(--green)}.modal-actions{display:flex;justify-content:flex-end;gap:9px;margin-top:17px}.toast{position:fixed;bottom:22px;left:50%;transform:translate(-50%,20px);opacity:0;pointer-events:none;background:#1c2921;border:1px solid #28533b;color:#c8f8df;padding:11px 16px;border-radius:9px;font-size:11px;z-index:80;transition:.25s}.toast.show{opacity:1;transform:translate(-50%,0)}
@media(max-width:1100px){.main-content{padding:0 25px}.stats-grid{grid-template-columns:repeat(2,minmax(0,1fr))}.content-grid{grid-template-columns:1fr}.chart-wrap{height:205px}}
@media(max-width:700px){.sidebar{transform:translateX(-100%);transition:transform .25s ease;box-shadow:15px 0 40px #0008}.sidebar.open{transform:translateX(0)}.main-content{margin-left:0;padding:0 16px}.topbar{height:61px;gap:12px}.mobile-menu{display:block;flex-shrink:0}.breadcrumb{margin-right:auto;font-size:11px}.page{padding-top:25px}.page-heading{align-items:flex-start;gap:12px}h1{font-size:25px}.subtitle{font-size:11px;line-height:1.5}.date-chip{display:none}.stats-grid{gap:9px}.stat-card{padding:14px;min-height:116px}.stat-value{font-size:21px}.stat-top{font-size:10px}.stat-icon{width:25px;height:25px}.panel{padding:15px}.table-panel{padding:15px 0 0}.panel-heading{padding:0 15px}.table-panel>.panel-heading{padding:0 15px}.table-panel th,.table-panel td{padding-left:13px;padding-right:13px}.chart-wrap{height:190px}.toolbar{flex-wrap:wrap}.search-box{width:100%}.result-count{margin-left:0}.filter-select{flex:1}.primary-button{padding:10px 11px;font-size:10px}.page-heading .primary-button{white-space:nowrap}.compact-stats{grid-template-columns:repeat(2,minmax(0,1fr))}.settings-row{align-items:flex-start;flex-direction:column;gap:12px}.footer{padding-bottom:28px}}
@media(max-width:380px){.main-content{padding:0 11px}.stats-grid{gap:7px}.stat-card{padding:11px}.stat-value{font-size:18px}.page-heading .primary-button{font-size:9px;padding:9px}.demo-pill{display:none}}
const STORAGE_KEY = "kiwifyMiniDashboard_v1";
const brl = value => Number(value || 0).toLocaleString("pt-BR",{style:"currency",currency:"BRL"});
const dateBR = value => new Date(value + "T12:00:00").toLocaleDateString("pt-BR");
const isoDaysAgo = days => { const d=new Date(); d.setDate(d.getDate()-days); return d.toISOString().slice(0,10); };

function seedData(){
  return {
    products:[
      {id:1,name:"E-book: Comece do Zero",price:49.90,active:true},
      {id:2,name:"Planner Digital 2026",price:29.90,active:true},
      {id:3,name:"Curso Criatividade na Prática",price:197.00,active:true},
      {id:4,name:"Pack de Templates",price:39.90,active:true}
    ],
    sales:[
      {id:101,product:"E-book: Comece do Zero",buyer:"Marina S.",date:isoDaysAgo(0),amount:49.90,status:"approved"},
      {id:102,product:"Planner Digital 2026",buyer:"Lucas R.",date:isoDaysAgo(0),amount:29.90,status:"pending"},
      {id:103,product:"Curso Criatividade na Prática",buyer:"Ana C.",date:isoDaysAgo(1),amount:197,status:"approved"},
      {id:104,product:"Pack de Templates",buyer:"João P.",date:isoDaysAgo(2),amount:39.90,status:"approved"},
      {id:105,product:"E-book: Comece do Zero",buyer:"Bia M.",date:isoDaysAgo(3),amount:49.90,status:"pending"},
      {id:106,product:"Planner Digital 2026",buyer:"Rafa T.",date:isoDaysAgo(4),amount:29.90,status:"approved"},
      {id:107,product:"Curso Criatividade na Prática",buyer:"Duda F.",date:isoDaysAgo(5),amount:197,status:"approved"},
      {id:108,product:"Pack de Templates",buyer:"Caio L.",date:isoDaysAgo(6),amount:39.90,status:"approved"}
    ]
  };
}
function loadData(){try{const saved=localStorage.getItem(STORAGE_KEY);return saved?JSON.parse(saved):seedData()}catch(e){return seedData()}}
let data=loadData();
function saveData(){localStorage.setItem(STORAGE_KEY,JSON.stringify(data))}
function totals(){
  const approved=data.sales.filter(s=>s.status==="approved").reduce((a,s)=>a+s.amount,0);
  const pending=data.sales.filter(s=>s.status==="pending").reduce((a,s)=>a+s.amount,0);
  return {approved,pending,gross:approved+pending};
}
function statusHTML(status){return `<span class="status ${status}">${status==="approved"?"Aprovada":"Pendente"}</span>`}
function emptyRow(cols,message){return `<tr><td colspan="${cols}" class="empty-state">${message}</td></tr>`}
function renderDashboard(){
  const t=totals();
  document.getElementById("dashBalance").textContent=brl(t.approved);
  document.getElementById("dashRevenue").textContent=brl(t.gross);
  document.getElementById("dashOrders").textContent=data.sales.length;
  document.getElementById("dashProducts").textContent=data.products.length;
  document.getElementById("summaryAvailable").textContent=brl(t.approved);
  document.getElementById("summaryPending").textContent=brl(t.pending);
  document.getElementById("summaryTotal").textContent=brl(t.gross);
  const recent=[...data.sales].sort((a,b)=>b.date.localeCompare(a.date)).slice(0,5);
  document.getElementById("recentSalesBody").innerHTML=recent.length?recent.map(s=>`<tr><td>${escapeHTML(s.product)}</td><td>${dateBR(s.date)}</td><td>${brl(s.amount)}</td><td>${statusHTML(s.status)}</td></tr>`).join(""):emptyRow(4,"Nenhuma venda cadastrada ainda.");
  renderChart();
}
function renderChart(){
  const canvas=document.getElementById("salesChart"); if(!canvas||!window.Chart)return;
  const labels=[],values=[];
  for(let i=6;i>=0;i--){const day=isoDaysAgo(i);labels.push(new Date(day+"T12:00:00").toLocaleDateString("pt-BR",{day:"2-digit",month:"2-digit"}));values.push(data.sales.filter(s=>s.date===day&&s.status==="approved").reduce((sum,s)=>sum+s.amount,0))}
  if(window.salesChartInstance)window.salesChartInstance.destroy();
  window.salesChartInstance=new Chart(canvas,{type:"line",data:{labels,datasets:[{data:values,borderColor:"#00d084",backgroundColor:"rgba(0,208,132,.12)",fill:true,tension:.38,borderWidth:2,pointRadius:3,pointBackgroundColor:"#00d084",pointBorderColor:"#151a17",pointBorderWidth:2}]},options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false},tooltip:{backgroundColor:"#202923",titleColor:"#fff",bodyColor:"#dce6df",displayColors:false,callbacks:{label:c=>brl(c.raw)}}},scales:{x:{grid:{display:false},ticks:{color:"#78847c",font:{family:"DM Sans",size:10}}},y:{beginAtZero:true,grid:{color:"rgba(130,150,137,.12)"},ticks:{color:"#78847c",font:{family:"DM Sans",size:9},callback:v=>v>=1000?"R$"+(v/1000).toFixed(1)+"k":"R$"+v}}}}});
}
function renderProducts(){
  const query=(document.getElementById("productSearch")?.value||"").toLowerCase();
  const rows=data.products.filter(p=>p.name.toLowerCase().includes(query));
  document.getElementById("productCount").textContent=`${data.products.length} produto${data.products.length===1?"":"s"}`;
  document.getElementById("productsBody").innerHTML=rows.length?rows.map(p=>{
    const count=data.sales.filter(s=>s.product===p.name).length;
    return `<tr><td>${escapeHTML(p.name)}</td><td>${brl(p.price)}</td><td>${count}</td><td><span class="status approved">Ativo</span></td><td><div class="row-actions"><button class="row-action" data-edit="${p.id}">Editar</button><button class="row-action delete" data-delete="${p.id}">Excluir</button></div></td></tr>`
  }).join(""):emptyRow(5,"Nenhum produto encontrado.");
}
function renderSales(){
  const query=(document.getElementById("salesSearch")?.value||"").toLowerCase();
  const filter=document.getElementById("salesFilter")?.value||"all";
  const rows=[...data.sales].sort((a,b)=>b.date.localeCompare(a.date)).filter(s=>s.product.toLowerCase().includes(query)&&(filter==="all"||s.status===filter));
  document.getElementById("salesCount").textContent=data.sales.length;
  document.getElementById("salesTotal").textContent=brl(totals().gross);
  document.getElementById("salesBody").innerHTML=rows.length?rows.map(s=>`<tr><td>${escapeHTML(s.product)}</td><td>${escapeHTML(s.buyer)}</td><td>${dateBR(s.date)}</td><td>${brl(s.amount)}</td><td>${statusHTML(s.status)}</td></tr>`).join(""):emptyRow(5,"Nenhuma venda encontrada.");
}
function renderFinance(){
  const t=totals();
  document.getElementById("financeAvailable").textContent=brl(t.approved);
  document.getElementById("financePending").textContent=brl(t.pending);
  document.getElementById("financeGross").textContent=brl(t.gross);
  const rows=[...data.sales].sort((a,b)=>b.date.localeCompare(a.date));
  document.getElementById("financeBody").innerHTML=rows.length?rows.map(s=>`<tr><td>Venda — ${escapeHTML(s.product)}</td><td>${dateBR(s.date)}</td><td>Entrada</td><td>${brl(s.amount)}</td><td>${statusHTML(s.status)}</td></tr>`).join(""):emptyRow(5,"Nenhuma movimentação registrada.");
}
function renderAll(){renderDashboard();renderProducts();renderSales();renderFinance()}
function escapeHTML(str){return String(str).replace(/[&<>"']/g,c=>({"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;"}[c]))}
function showToast(message){const toast=document.getElementById("toast");toast.textContent=message;toast.classList.add("show");clearTimeout(showToast.timer);showToast.timer=setTimeout(()=>toast.classList.remove("show"),2400)}
function navigate(page){
  document.querySelectorAll(".page").forEach(p=>p.classList.toggle("active-page",p.id===`page-${page}`));
  document.querySelectorAll(".nav-item[data-page]").forEach(b=>b.classList.toggle("active",b.dataset.page===page));
  const labels={dashboard:"Dashboard",products:"Produtos",sales:"Vendas",finance:"Financeiro",settings:"Configurações"};
  document.getElementById("breadcrumbCurrent").textContent=labels[page]||"Dashboard";
  document.getElementById("sidebar").classList.remove("open");
  if(page==="dashboard")renderChart();
}
function openModal(product=null){
  document.getElementById("productForm").reset();
  document.getElementById("productId").value=product?product.id:"";
  document.getElementById("modalTitle").textContent=product?"Editar produto":"Adicionar produto";
  if(product){document.getElementById("productName").value=product.name;document.getElementById("productPrice").value=product.price}
  const modal=document.getElementById("productModal");modal.classList.add("open");modal.setAttribute("aria-hidden","false");document.getElementById("productName").focus();
}
function closeModal(){const modal=document.getElementById("productModal");modal.classList.remove("open");modal.setAttribute("aria-hidden","true")}
function resetData(){if(confirm("Restaurar os dados fictícios originais? Suas alterações locais serão perdidas.")){data=seedData();saveData();renderAll();showToast("Dados de demonstração restaurados.")}}

document.querySelectorAll(".nav-item[data-page]").forEach(btn=>btn.addEventListener("click",()=>navigate(btn.dataset.page)));
document.querySelectorAll("[data-goto]").forEach(btn=>btn.addEventListener("click",()=>navigate(btn.dataset.goto)));
document.getElementById("mobileMenu").addEventListener("click",()=>document.getElementById("sidebar").classList.toggle("open"));
document.getElementById("addProductButton").addEventListener("click",()=>openModal());
document.getElementById("closeModal").addEventListener("click",closeModal);
document.getElementById("cancelModal").addEventListener("click",closeModal);
document.getElementById("productModal").addEventListener("click",e=>{if(e.target.id==="productModal")closeModal()});
document.addEventListener("keydown",e=>{if(e.key==="Escape")closeModal()});
document.getElementById("productForm").addEventListener("submit",e=>{
  e.preventDefault();
  const id=document.getElementById("productId").value;
  const name=document.getElementById("productName").value.trim();
  const price=Number(document.getElementById("productPrice").value);
  if(!name||!Number.isFinite(price)||price<=0){showToast("Confira o nome e o preço do produto.");return}
  if(id){const product=data.products.find(p=>p.id===Number(id));if(product){const oldName=product.name;product.name=name;product.price=price;data.sales.forEach(s=>{if(s.product===oldName)s.product=name})}showToast("Produto atualizado!")}
  else{data.products.push({id:Date.now(),name,price,active:true});showToast("Produto adicionado!")}
  saveData();renderAll();closeModal();
});
document.getElementById("productsBody").addEventListener("click",e=>{
  const edit=e.target.closest("[data-edit]"),del=e.target.closest("[data-delete]");
  if(edit){const p=data.products.find(x=>x.id===Number(edit.dataset.edit));if(p)openModal(p)}
  if(del){const p=data.products.find(x=>x.id===Number(del.dataset.delete));if(!p)return;if(confirm(`Excluir "${p.name}" do catálogo? O histórico de vendas será mantido.`)){data.products=data.products.filter(x=>x.id!==p.id);saveData();renderAll();showToast("Produto excluído.")}}
});
document.getElementById("productSearch").addEventListener("input",renderProducts);
document.getElementById("salesSearch").addEventListener("input",renderSales);
document.getElementById("salesFilter").addEventListener("change",renderSales);
document.getElementById("resetButton").addEventListener("click",resetData);
document.getElementById("settingsReset").addEventListener("click",resetData);
document.getElementById("todayLabel").textContent=new Date().toLocaleDateString("pt-BR",{day:"2-digit",month:"short",year:"numeric"});
renderAll();
