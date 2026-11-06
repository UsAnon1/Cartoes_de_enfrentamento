<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Reflexo</title>
<style>
:root{--bg:#f4f1ec;--fg:#2b2a33;--muted:#7a7785;--accent:#6c5ce7;--surface:#fff}
@media (prefers-color-scheme:dark){:root{--bg:#17161c;--fg:#f1eff7;--muted:#9a97a8;--accent:#8f82ff;--surface:#24232c}}
*{box-sizing:border-box}
body{margin:0;min-height:100vh;background:var(--bg);color:var(--fg);font-family:system-ui,-apple-system,Segoe UI,sans-serif;display:flex;justify-content:center}
.app{width:100%;max-width:440px;min-height:100vh;display:flex;flex-direction:column;padding:20px}
header{display:flex;justify-content:space-between;align-items:center}
h1{font-size:24px;margin:8px 0}
h2{margin:0 0 16px}
.stack{position:relative;flex:1;min-height:420px;margin:20px 0 12px;touch-action:pan-y}
.card{position:absolute;inset:0;border-radius:24px;display:flex;align-items:center;justify-content:center;padding:28px;text-align:center;font-size:26px;line-height:1.35;box-shadow:0 10px 30px rgba(0,0,0,.18);overflow:hidden;user-select:none;cursor:grab;transition:transform .35s ease,opacity .35s ease}
.card.drag{transition:none;cursor:grabbing}
.card img{position:absolute;inset:0;width:100%;height:100%;object-fit:cover;pointer-events:none}
.counter{color:var(--muted);font-size:13px;text-align:center;margin-bottom:80px}
.empty{text-align:center;color:var(--muted);margin-top:40%}
button{font:inherit;cursor:pointer}
.btn{width:100%;padding:14px;border:0;border-radius:12px;background:var(--accent);color:#fff;font-weight:600;font-size:16px;margin-bottom:10px}
.btn.sec{background:var(--surface);color:var(--fg);border:1px solid color-mix(in srgb,var(--fg) 20%,transparent)}
.link{background:none;border:0;color:var(--accent);padding:8px;font-size:15px}
.fab{position:fixed;bottom:24px;right:max(20px,calc(50% - 200px));width:60px;height:60px;border-radius:50%;border:0;background:var(--accent);color:#fff;font-size:32px;box-shadow:0 6px 18px rgba(0,0,0,.3)}
.modal{position:fixed;inset:0;background:rgba(0,0,0,.5);display:flex;align-items:flex-end;justify-content:center;z-index:10}
.hidden{display:none!important}
.sheet{background:var(--bg);width:100%;max-width:440px;border-radius:24px 24px 0 0;padding:24px;max-height:90vh;overflow:auto}
textarea,select{width:100%;padding:14px;border-radius:12px;border:1px solid color-mix(in srgb,var(--fg) 20%,transparent);background:var(--surface);color:var(--fg);font-size:16px;margin-bottom:12px;font-family:inherit}
.row{display:flex;gap:10px;align-items:center;margin-bottom:12px}
.row input[type=color]{width:56px;height:44px;padding:2px;border:0;background:none}
.item{display:flex;gap:10px;align-items:center;padding:10px;background:var(--surface);border-radius:12px;margin-bottom:8px}
.item .t{flex:1;font-size:14px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.item button{border:0;background:none;font-size:18px}
.sr{position:absolute;width:1px;height:1px;opacity:0;overflow:hidden;pointer-events:none}
label.btn{display:block;text-align:center;cursor:pointer}
.hint{color:var(--muted);font-size:12px;text-align:center}
</style>
</head>
<body>
<div class="app">
  <header>
    <h1>Reflexo</h1>
    <button class="link" id="lista">Minhas frases</button>
  </header>
  <div class="stack" id="stack"></div>
  <div class="counter" id="counter"></div>
  <div class="hint" style="margin-top:-60px;margin-bottom:70px">Arraste o cartão ou use as setas ← →</div>
  <input type="file" id="arq" accept="image/*" class="sr">
  <button class="fab" id="fab" aria-label="Adicionar">+</button>
  <div class="modal hidden" id="modal"><div class="sheet" id="sheet"></div></div>
</div>

<script>
var KEY='reflexo_v1';
var padrao=[
 {id:1,tipo:'texto',texto:'Eu não preciso ter todas as respostas hoje.',bg:'#6c5ce7',cor:'#ffffff',fonte:'Georgia, serif'},
 {id:2,tipo:'texto',texto:'O que eu posso fazer agora, com o que tenho?',bg:'#00b894',cor:'#ffffff',fonte:'system-ui, sans-serif'},
 {id:3,tipo:'texto',texto:'Respirar também é progresso.',bg:'#fdcb6e',cor:'#2b2a33',fonte:'Georgia, serif'},
 {id:4,tipo:'texto',texto:'Sou gentil comigo como sou com quem amo.',bg:'#e17055',cor:'#ffffff',fonte:'system-ui, sans-serif'}
];
var fila;
try{fila=JSON.parse(localStorage.getItem(KEY)||'null')}catch(e){fila=null}
if(!Array.isArray(fila))fila=padrao;
var nextId=Date.now();
var $=function(s){return document.querySelector(s)};
var stack=$('#stack'), animando=false;

function salvar(){
  try{localStorage.setItem(KEY,JSON.stringify(fila))}
  catch(e){alert('Não foi possível salvar: armazenamento do navegador cheio. Exclua algumas imagens.')}
}
function esc(t){return String(t).replace(/[&<>"]/g,function(c){return {'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;'}[c]})}

function cardEl(r,pos){
  var d=document.createElement('div');d.className='card';
  if(r.tipo==='imagem'){var i=document.createElement('img');i.src=r.url;i.alt='';d.appendChild(i);d.style.background='#000'}
  else{d.textContent=r.texto;d.style.background=r.bg;d.style.color=r.cor;d.style.fontFamily=r.fonte}
  d.style.transform='translateY('+pos*14+'px) scale('+(1-pos*0.05)+')';
  d.style.zIndex=10-pos;
  return d;
}
function render(){
  stack.innerHTML='';animando=false;
  if(!fila.length){stack.innerHTML='<p class="empty">Nenhuma frase ainda.<br>Toque em + para criar.</p>';$('#counter').textContent='';return}
  fila.slice(0,3).reverse().forEach(function(r,i,arr){stack.appendChild(cardEl(r,arr.length-1-i))});
  $('#counter').textContent=fila.length+(fila.length===1?' reflexão':' reflexões')+' em loop';
  bind(stack.lastChild);
}
function relayout(){
  [].slice.call(stack.children).reverse().forEach(function(c,pos){
    c.style.transform='translateY('+pos*14+'px) scale('+(1-pos*0.05)+')';
  });
}
function sair(el,dir){
  if(animando||fila.length<1)return;animando=true;
  el.classList.remove('drag');
  el.style.transform='translateX('+dir*600+'px) rotate('+dir*25+'deg)';el.style.opacity=0;
  fila.push(fila.shift());salvar(); // fila circular: o topo vai para o final
  setTimeout(render,300);
}
function bind(el){
  var sx=0,dx=0,on=false;
  el.addEventListener('pointerdown',function(e){if(animando)return;on=true;sx=e.clientX;el.classList.add('drag');el.setPointerCapture(e.pointerId)});
  el.addEventListener('pointermove',function(e){
    if(!on)return;dx=e.clientX-sx;
    el.style.transform='translateX('+dx+'px) rotate('+dx/18+'deg)';
    var p=Math.min(Math.abs(dx)/150,1),prev=el.previousSibling;
    if(prev)prev.style.transform='translateY('+(14-14*p)+'px) scale('+(0.95+0.05*p)+')';
  });
  function fim(){
    if(!on)return;on=false;
    if(Math.abs(dx)>90){sair(el,dx>0?1:-1)}
    else{el.classList.remove('drag');el.style.transform='translateY(0) scale(1)';relayout()}
    dx=0;
  }
  el.addEventListener('pointerup',fim);el.addEventListener('pointercancel',fim);
}
document.addEventListener('keydown',function(e){
  if(!$('#modal').classList.contains('hidden'))return;
  var t=stack.lastChild;if(!t||!t.classList.contains('card'))return;
  if(e.key==='ArrowRight')sair(t,1);
  if(e.key==='ArrowLeft')sair(t,-1);
});

function abrir(html){$('#sheet').innerHTML=html;$('#modal').classList.remove('hidden')}
function fechar(){$('#modal').classList.add('hidden')}
$('#modal').addEventListener('click',function(e){if(e.target.id==='modal')fechar()});

$('#fab').onclick=function(){
  abrir('<h2>Adicionar</h2><button class="btn" id="mTxt">✍️ Escrever nova frase</button><label class="btn sec" for="arq">🖼️ Importar imagem</label>');
  $('#mTxt').onclick=function(){editor()};
};
$('#arq').addEventListener('change',function(){
  var f=this.files&&this.files[0];this.value='';importar(f);
});
function editor(id){
  var r=id?fila.find(function(x){return x.id===id}):null;
  abrir('<h2>'+(r?'Editar frase':'Nova frase')+'</h2><textarea id="eT" rows="4" placeholder="Digite sua frase...">'+esc(r?r.texto:'')+'</textarea>'+
  '<div class="row"><label>Fundo</label><input type="color" id="eB" value="'+(r?r.bg:'#6c5ce7')+'"><label>Texto</label><input type="color" id="eC" value="'+(r?r.cor:'#ffffff')+'"></div>'+
  '<select id="eF"><option value="system-ui, sans-serif">Sans-serif</option><option value="Georgia, serif">Serifada</option><option value="\'Courier New\', monospace">Máquina de escrever</option><option value="cursive">Manuscrita</option></select>'+
  '<button class="btn" id="eS">Salvar</button>');
  if(r)$('#eF').value=r.fonte;
  $('#eS').onclick=function(){
    var t=$('#eT').value.trim();if(!t)return;
    if(r){r.texto=t;r.bg=$('#eB').value;r.cor=$('#eC').value;r.fonte=$('#eF').value}
    else fila.unshift({id:nextId++,tipo:'texto',texto:t,bg:$('#eB').value,cor:$('#eC').value,fonte:$('#eF').value});
    salvar();fechar();render();
  };
}
function importar(f){
  if(!f)return;
  var url=URL.createObjectURL(f),img=new Image();
  img.onload=function(){
    try{
      var m=1000,sc=Math.min(1,m/Math.max(img.width,img.height));
      var c=document.createElement('canvas');c.width=Math.round(img.width*sc);c.height=Math.round(img.height*sc);
      c.getContext('2d').drawImage(img,0,0,c.width,c.height);
      fila.unshift({id:nextId++,tipo:'imagem',url:c.toDataURL('image/jpeg',0.82)});
      URL.revokeObjectURL(url);salvar();fechar();render();
    }catch(e){alert('Erro ao processar a imagem: '+e.message)}
  };
  img.onerror=function(){alert('Não consegui ler essa imagem. Tente um arquivo JPG ou PNG.')};
  img.src=url;
}
$('#lista').onclick=listar;
function listar(){
  var h='<h2>Minhas frases</h2>';
  if(!fila.length)h+='<p class="hint">Vazio.</p>';
  fila.forEach(function(r){
    h+='<div class="item"><span>'+(r.tipo==='imagem'?'🖼️':'✍️')+'</span><span class="t">'+(r.tipo==='imagem'?'Imagem importada':esc(r.texto))+'</span>'+
    (r.tipo==='texto'?'<button data-e="'+r.id+'" aria-label="Editar">✏️</button>':'')+'<button data-d="'+r.id+'" aria-label="Excluir">🗑️</button></div>';
  });
  abrir(h);
  document.querySelectorAll('[data-e]').forEach(function(b){b.onclick=function(){editor(+b.dataset.e)}});
  document.querySelectorAll('[data-d]').forEach(function(b){b.onclick=function(){
    fila=fila.filter(function(x){return x.id!==+b.dataset.d});salvar();render();listar();
  }});
}
render();
</script>
</body>
</html>
