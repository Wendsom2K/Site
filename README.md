<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Classico DayZ | SAMP 0.3.7</title>
<style>
:root{--verde:#00ff88;--preto:#0a0a0a;--cinza:#1a1a1a;--vermelho:#ff3333;}
*{margin:0;padding:0;box-sizing:border-box;font-family:'Segoe UI',sans-serif}
body{background:var(--preto);color:#eee;background-image:radial-gradient(#222 1px,transparent 1px);background-size:20px 20px;}
header{background:linear-gradient(180deg,#000 0%,#111 100%);border-bottom:2px solid var(--verde);padding:20px;text-align:center;position:sticky;top:0;z-index:10}
header h1{font-size:2.2rem;color:var(--verde);text-shadow:0 0 15px var(--verde)}
.status-bar{display:flex;gap:15px;justify-content:center;margin-top:10px;flex-wrap:wrap}
.badge{background:var(--cinza);padding:6px 12px;border-radius:6px;border:1px solid #333;font-size:.9rem}
.badge.online{border-color:var(--verde);color:var(--verde)}
.container{max-width:1100px;margin:30px auto;padding:0 20px;display:grid;grid-template-columns:repeat(auto-fit,minmax(320px,1fr));gap:20px}
.card{background:var(--cinza);border:1px solid #333;border-radius:10px;padding:20px;box-shadow:0 0 20px #000}
.card h2{color:var(--verde);border-bottom:2px solid var(--verde);padding-bottom:8px;margin-bottom:15px;font-size:1.2rem}
.ip-box{background:#000;border:1px dashed var(--verde);padding:12px;text-align:center;font-family:monospace;font-size:1.1rem;user-select:all}
.btn{display:inline-block;background:var(--verde);color:#000;text-decoration:none;padding:12px 20px;border-radius:6px;font-weight:700;margin-top:10px;transition:.2s}
.btn:hover{filter:brightness(1.2);box-shadow:0 0 15px var(--verde)}
.btn.discord{background:#5865F2;color:#fff}
ul{list-style:none}
ul li{padding:6px 0;border-bottom:1px dashed #333}
.horario{color:var(--vermelho);font-weight:700}
.evento{color:#ffb700;font-weight:600}
footer{text-align:center;padding:30px;color:#666;font-size:.8rem}
#playMusic{position:fixed;bottom:20px;right:20px;background:var(--verde);border:none;color:#000;padding:12px 18px;border-radius:50px;font-weight:700;cursor:pointer;z-index:99;box-shadow:0 0 15px var(--verde)}
</style>
</head>
<body>

<header>
  <h1>☣️ CLASSICO DAYZ ☣️</h1>
  <div class="status-bar">
    <div class="badge" id="serverStatus">Verificando...</div>
    <div class="badge" id="playerCount">Players: --/--</div>
    <div class="badge">IP: 181.215.45.74:7777</div>
  </div>
</header>

<div class="container">

  <div class="card">
    <h2>📡 ENTRAR NO SERVIDOR</h2>
    <p>IP Direto do Classico DayZ SAMP:</p>
    <div class="ip-box">181.215.45.74:7777</div>
    <a href="samp://181.215.45.74:7777" class="btn">▶️ CONECTAR AGORA</a>
    <a href="https://discord.gg/Ku7CMxKsrS" target="_blank" class="btn discord">💬 ENTRAR NO DISCORD</a>
  </div>

  <div class="card">
    <h2>📜 REGRAS DAYZ</h2>
    <ul>
      <li>1. RP Leve Obrigatório: Nada de Deathmatch sem motivo</li>
      <li>2. Combat Logging = BAN: Não desconecte em PvP</li>
      <li>3. Sem Hack/Aimbot/Macro: Banimento permanente</li>
      <li>4. Respeito no Chat Global e Discord</li>
      <li>5. Raid só no horário. Fora disso é KOS</li>
      <li>6. Bug Abuso = Wipe de conta + BAN</li>
    </ul>
  </div>

  <div class="card">
    <h2>💥 HORÁRIOS DE RAID</h2>
    <ul>
      <li><span class="horario">SEXTA</span> das 19:00 às 22:00</li>
      <li><span class="horario">SÁBADO</span> das 19:00 às 22:00</li>
      <li><span class="horario">DOMINGO</span> das 19:00 às 23:00</li>
    </ul>
    <p style="margin-top:10px;font-size:.9rem;color:#aaa">Fora do horário = Base protegida. Raid = Ban.</p>
  </div>

  <div class="card" style="grid-column:1/-1">
    <h2>🎯 EVENTOS SEMANAIS</h2>
    <ul>
      <li><span class="evento">QUARTA-FEIRA</span> - Rodízio de Eventos PvP/PvE:</li>
      <li>1. <b>HOMEM PERDIDO</b> - Encontre e extraia o NPC. Recompensa épica.</li>
      <li>2. <b>DROP DA CARNIFICINA</b> - Crate cai no mapa. Só 1 clã leva.</li>
      <li>3. <b>CORRIDA MORTAL</b> - Chegue primeiro. Zumbis no caminho.</li>
      <li>4. <b>FUGA DA PRISÃO MALDITA</b> - Escape do presídio lotado de horda.</li>
      <li>5. <b>INVASÃO DA MEIA NOITE</b> - 00:00 a base é invadida por bots.</li>
      <li>6. <b>ATAQUE AÉREO</b> - Heli de guerra patrulha. Derrube e looteie.</li>
      <li>7. <b>ATAQUE DA MEIA NOITE</b> - Boss zombie spawn 23:59 no centro.</li>
    </ul>
  </div>

</div>

<footer>
  Classico DayZ © 2026 | SAMP 0.3.7 R4 | Temporadas | Wipe Mensal
</footer>

<button id="playMusic">🔊 MÚSICA ON</button>
<audio id="bgMusic" loop>
  <source src="https://som.brasilplaygames.com.br/som/Dayz.mp3" type="audio/mpeg">
</audio>

<script>
// 1. Música só toca após clique - navegador bloqueia autoplay
const music = document.getElementById('bgMusic');
const btn = document.getElementById('playMusic');
let playing = false;
btn.onclick = () => {
  if(playing){music.pause(); btn.textContent='🔊 MÚSICA ON';}
  else {music.play(); btn.textContent='🔇 MÚSICA OFF';}
  playing =!playing;
};

// 2. Monitor SAMP em tempo real via API pública
async function getServerStatus(){
  try{
    const res = await fetch('https://api.open.mp/servers/host/181.215.45.74/port/7777');
    const data = await res.json();
    if(data.online){
      document.getElementById('serverStatus').textContent = '🟢 ONLINE';
      document.getElementById('serverStatus').classList.add('online');
      document.getElementById('playerCount').textContent = `Players: ${data.players}/${data.maxplayers}`;
    } else {
      document.getElementById('serverStatus').textContent = '🔴 OFFLINE';
    }
  }catch(e){
    document.getElementById('serverStatus').textContent = '🟡 VERIFICANDO...';
  }
}
getServerStatus();
setInterval(getServerStatus, 10000); // Atualiza a cada 10s
</script>
</body>
</html>
