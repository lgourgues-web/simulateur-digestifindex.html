<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="utf-8">
<title>Simulateur du système digestif</title>
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Bricolage+Grotesque:wght@400;600;800&display=swap">
<style>
:root{--bg:#EEF3F1;--ink:#17302B;--mut:#5A716B;--card:#fff;--line:#CFDCD8;--acc:#2B3A67;--accfg:#fff;--organ:#F3A7A0;--organ2:#D9776E;--gland:#F2C14E;--mec:#1F7A63;--chi:#8A4FBF;--ok:#1F7A63;--ko:#B33A3A;
box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}
@media (prefers-color-scheme:dark){:root:not([data-theme="light"]){--bg:#0F1B18;--ink:#E4EFEB;--mut:#96ADA6;--card:#182824;--line:#2C433D;--acc:#9FB2F0;--accfg:#0F1B18;--organ:#C9807A;--organ2:#F3A7A0;--mec:#5CCBA9;--chi:#C39BEF;--ok:#5CCBA9;--ko:#F08080}}
:root[data-theme="dark"]{--bg:#0F1B18;--ink:#E4EFEB;--mut:#96ADA6;--card:#182824;--line:#2C433D;--acc:#9FB2F0;--accfg:#0F1B18;--organ:#C9807A;--organ2:#F3A7A0;--mec:#5CCBA9;--chi:#C39BEF;--ok:#5CCBA9;--ko:#F08080}
html{scroll-padding-top:env(safe-area-inset-top,0px)}
*{box-sizing:border-box}
button,[role=button],[data-mol],.chip,.cards button,.opts button,nav button,input[type=range]{-webkit-tap-highlight-color:transparent;touch-action:manipulation}
[data-id],.o,.g,.oline,.mol,svg text,nav{-webkit-touch-callout:none;-webkit-user-select:none;user-select:none}
body{margin:0;background:var(--bg);color:var(--ink);font-family:'Bricolage Grotesque',system-ui,-apple-system,Segoe UI,sans-serif;line-height:1.5;-webkit-text-size-adjust:100%}
main{max-width:1000px;margin:0 auto;padding:20px 16px 40px}
h1{font-size:clamp(1.7rem,4vw,2.4rem);font-weight:800;margin:0 0 4px;letter-spacing:-.02em}
h2{font-size:1.3rem;margin:0 0 6px}
.sub{color:var(--mut);margin:0 0 16px;max-width:60ch}
nav{display:flex;gap:6px;flex-wrap:wrap;margin-bottom:16px}
button{font:inherit;color:inherit;cursor:pointer}
nav button{border:1.5px solid var(--line);background:var(--card);padding:11px 16px;border-radius:999px;font-weight:600;min-height:44px}
nav button[aria-selected=true]{background:var(--acc);color:var(--accfg);border-color:var(--acc)}
button:focus-visible,[tabindex]:focus-visible{outline:3px solid var(--acc);outline-offset:2px}
section{display:none}section.on{display:block}
.grid{display:grid;grid-template-columns:minmax(260px,340px) 1fr;gap:18px;align-items:start}
@media(max-width:760px){.grid{grid-template-columns:1fr}}
.card{background:var(--card);border:1px solid var(--line);border-radius:14px;padding:16px}
.bar{display:flex;gap:8px;flex-wrap:wrap;margin-bottom:12px}
.btn{border:1.5px solid var(--acc);background:transparent;color:var(--acc);padding:10px 14px;border-radius:10px;font-weight:600;min-height:44px}
.btn[aria-pressed=true],.btn.solid{background:var(--acc);color:var(--accfg)}
svg{width:100%;height:auto;display:block;max-height:78vh}
.o{fill:var(--organ);stroke:var(--organ2);stroke-width:2;cursor:pointer;transition:opacity .2s}
.oline{cursor:pointer;transition:opacity .2s}
.oline path{fill:none;stroke-linecap:round;stroke-linejoin:round}
.oline .u{stroke:var(--organ2)}.oline .t{stroke:var(--organ)}.oline .h{stroke:var(--organ2);stroke-dasharray:1.5 7;opacity:.55}
.g{fill:var(--gland);stroke:#B98A10;stroke-width:1.5;cursor:pointer;transition:opacity .2s}
svg[data-mode=tube] .g{opacity:.35}svg[data-mode=glandes] .o,svg[data-mode=glandes] .oline{opacity:.3}
.sel{filter:drop-shadow(0 0 4px var(--acc));stroke:var(--acc)!important;stroke-width:3}
.lbl{font-size:11px;fill:var(--mut);pointer-events:none}
.lbl2{font-size:9px;font-style:italic;fill:var(--acc);pointer-events:none}
#dot{fill:#7A4A1E;stroke:#fff;stroke-width:2;transition:transform 1.8s ease-in-out;pointer-events:none}
.badge{display:inline-block;padding:2px 10px;border-radius:999px;font-size:.8rem;font-weight:600;border:1.5px solid;margin:0 6px 6px 0}
.b-m{color:var(--mec);border-color:var(--mec)}.b-c{color:var(--chi);border-color:var(--chi)}.b-k{color:var(--mut);border-color:var(--line)}
ul{padding-left:20px;margin:6px 0}
.chips{display:flex;gap:6px;flex-wrap:wrap;margin:8px 0}
.chip{border:1.5px solid var(--line);background:var(--card);padding:9px 13px;border-radius:999px;font-size:.92rem;min-height:40px}
.cards{display:grid;grid-template-columns:repeat(auto-fill,minmax(150px,1fr));gap:10px;margin-bottom:14px}
.cards button{text-align:left;background:var(--card);border:1.5px solid var(--line);border-radius:12px;padding:12px}
.cards button[aria-pressed=true]{border-color:var(--acc);box-shadow:inset 0 0 0 1px var(--acc)}
.cards b{display:block}.cards small{color:var(--mut)}
.opts{display:flex;gap:8px;flex-wrap:wrap;margin:10px 0}
.opts button{border:1.5px solid var(--line);background:var(--card);padding:11px 14px;border-radius:10px;min-height:44px}
.opts button.ok{border-color:var(--ok);background:color-mix(in srgb,var(--ok) 18%,transparent)}
.opts button.ko{border-color:var(--ko);background:color-mix(in srgb,var(--ko) 18%,transparent)}
.fb{min-height:1.5em;font-weight:600}
.row{display:grid;grid-template-columns:1fr 130px 70px 44px;gap:8px;align-items:center;padding:8px 0;border-bottom:1px solid var(--line)}
.row small{display:block;color:var(--mut)}
.row input{width:100%}
.x{border:0;background:none;font-size:1.2rem;color:var(--mut);min-width:44px;min-height:44px}
.stack{display:flex;height:26px;border-radius:8px;overflow:hidden;background:var(--line);margin:8px 0}
.stack i{display:block;height:100%;transition:width .3s}
.lg{display:flex;gap:14px;flex-wrap:wrap;font-size:.9rem}
.lg span::before{content:"";display:inline-block;width:11px;height:11px;border-radius:3px;margin-right:5px;background:var(--c)}
.big{font-size:2rem;font-weight:800;letter-spacing:-.02em}
.tr{display:flex;flex-direction:column;gap:10px}
.tr .it{display:flex;gap:10px;flex-wrap:wrap;align-items:center;justify-content:space-between;border:1px solid var(--line);border-radius:12px;padding:10px 12px;background:var(--card)}
.tr .it .a{flex:1 1 230px}
.tr .it .fbk{flex:1 1 100%;font-size:.9rem;color:var(--mut)}
#svg2 *{cursor:default}
#svg2 .o,#svg2 .oline,#svg2 .g{opacity:.4}
#svg2 .act{opacity:1;animation:glow var(--d,1.6s) ease-in-out infinite}
#svg2 .g.act,#svg2 .o.act{transform-box:fill-box;transform-origin:center;animation:pl var(--d,1.6s) ease-in-out infinite}
@keyframes pl{50%{transform:scale(var(--s,1.2));filter:drop-shadow(0 0 5px var(--acc))}}
@keyframes glow{50%{filter:drop-shadow(0 0 6px var(--acc))}}
.rw{display:grid;grid-template-columns:130px 54px 1fr;gap:8px;align-items:center;padding:7px 0;border-bottom:1px solid var(--line)}
.rw small{color:var(--mut);font-size:.88rem}
.mt{display:flex;gap:3px}.mt i{width:14px;height:10px;border-radius:3px;background:var(--line)}.mt i.on{background:var(--acc)}
@media(max-width:520px){.rw{grid-template-columns:1fr 54px}.rw small{grid-column:1/-1}}
@media(prefers-reduced-motion:reduce){#dot{transition:none}#svg2 .act,#svg2 .g.act,#svg2 .o.act{animation:none;filter:drop-shadow(0 0 5px var(--acc))}}
.mol{display:none;width:100%;height:auto;max-height:60vh}
.mol.on{display:block}
.mol .piece{transform-box:fill-box;transform-origin:center;transition:transform 1.3s cubic-bezier(.3,.7,.3,1)}
.mol.split .piece{transform:translate(var(--tx,0),var(--ty,0)) rotate(var(--rz,0deg))}
.mol.absorbed .piece{transform:translate(calc(var(--tx,0) + var(--bx,0)),calc(var(--ty,0) + var(--by,0))) rotate(var(--rz,0deg))}
.mol .bond{transition:opacity .5s ease .1s;stroke-linecap:round}
.mol.split .bond{opacity:0}
.wall{stroke:var(--mut);stroke-width:3;stroke-dasharray:6 5;opacity:.6}
.blood{fill:color-mix(in srgb,var(--ko) 14%,transparent);stroke:var(--ko);stroke-width:1.5;stroke-dasharray:3 4;opacity:.8}
.wlbl{font-size:11px;fill:var(--mut);font-weight:600}
.mol .unit{fill:var(--u,var(--organ));stroke:var(--organ2);stroke-width:2}
.mol .unit2{fill:var(--u2,var(--gland));stroke:#B98A10;stroke-width:2}
.mol .zig{fill:none;stroke:var(--organ2);stroke-width:5;stroke-linecap:round;stroke-linejoin:round}
.mol text{font-size:11px;fill:var(--ink);font-weight:600;text-anchor:middle;pointer-events:none}
.mol .tag{fill:var(--mut);font-weight:400;font-size:9.5px}
.molbar{display:flex;gap:8px;flex-wrap:wrap;margin-bottom:12px}
.molbar .btn[aria-pressed=true]{background:var(--acc);color:var(--accfg)}
.legend2{display:flex;gap:12px;flex-wrap:wrap;font-size:.85rem;color:var(--mut);margin-top:6px}
.legend2 span::before{content:"";display:inline-block;width:11px;height:11px;border-radius:50%;margin-right:5px;background:var(--c);vertical-align:-1px}
@media(prefers-reduced-motion:reduce){.mol .piece,.mol .bond{transition:none}}
</style>
</head>
<body>
<main>
<h1>Le système digestif</h1>
<p class="sub">Clique sur les organes et les glandes, suis un aliment du début à la fin, compose un repas et teste tes connaissances.</p>
<nav role="tablist" id="tabs">
<button role="tab" data-t="s1" aria-selected="true">Tube et glandes</button>
<button role="tab" data-t="s2" aria-selected="false">Types d’aliments</button>
<button role="tab" data-t="s3" aria-selected="false">Valeur énergétique</button>
<button role="tab" data-t="s4" aria-selected="false">Transformations</button>
<button role="tab" data-t="s5" aria-selected="false">Repas et réactions</button>
<button role="tab" data-t="s6" aria-selected="false">Digestion des nutriments</button>
</nav>

<section id="s1" class="on">
<div class="bar">
<button class="btn" id="mTube" aria-pressed="true">Organes du tube digestif</button>
<button class="btn" id="mGl" aria-pressed="false">Glandes digestives</button>
<button class="btn solid" id="go">Suivre un aliment</button>
</div>
<div class="grid">
<div class="card">
<svg id="svg" viewBox="0 0 300 460" data-mode="tube" role="img" aria-label="Schéma du système digestif">
<g class="oline" data-id="oesophage"><path class="u" stroke-width="10" d="M150 54 V130 Q150 170 158 192"/><path class="t" stroke-width="6" d="M150 54 V130 Q150 170 158 192"/></g>
<path class="g" data-id="foie" style="fill:#B4584A;stroke:#8E3F33" d="M92 190 Q100 172 138 176 Q165 180 168 194 Q150 212 126 222 Q98 228 90 208 Z"/>
<ellipse class="g" data-id="vesicule" style="fill:#7DB65B;stroke:#4E8A34" cx="124" cy="219" rx="6" ry="9"/>
<text class="lbl" x="52" y="234">Vésicule biliaire</text>
<ellipse class="g" data-id="pancreas" cx="165" cy="251" rx="36" ry="8" transform="rotate(-5 165 251)"/>
<path class="o" data-id="estomac" d="M160 188 Q200 176 212 206 Q218 240 186 246 Q164 248 150 234 Q160 228 168 222 Q176 212 168 204 Q160 198 160 188Z"/>
<g class="oline" data-id="grele"><path class="u" stroke-width="13" d="M170 258 Q170 284 142 290 Q124 296 136 302 H166 Q180 302 180 314 Q180 326 166 326 H134 Q120 326 120 338 Q120 350 134 350 H166 Q180 350 180 362 Q180 374 166 374 H142"/><path class="t" stroke-width="9" d="M170 258 Q170 284 142 290 Q124 296 136 302 H166 Q180 302 180 314 Q180 326 166 326 H134 Q120 326 120 338 Q120 350 134 350 H166 Q180 350 180 362 Q180 374 166 374 H142"/></g>
<g class="oline" data-id="gros"><path class="u" stroke-width="20" d="M110 385 V285 Q110 272 124 272 Q150 290 176 272 Q190 272 190 285 V372 Q190 402 166 398 Q150 394 150 410"/><path class="t" stroke-width="15" d="M110 385 V285 Q110 272 124 272 Q150 290 176 272 Q190 272 190 285 V372 Q190 402 166 398 Q150 394 150 410"/><path class="h" stroke-width="15" d="M110 385 V285 Q110 272 124 272 Q150 290 176 272 Q190 272 190 285 V372 Q190 402 166 398 Q150 394 150 410"/></g>
<g class="oline" data-id="anus"><path class="u" stroke-width="14" d="M150 408 V434"/><path class="t" stroke-width="10" d="M150 408 V434"/></g>
<circle class="o" data-id="anus" cx="150" cy="442" r="7"/>
<circle class="g" data-id="gastriques" cx="192" cy="204" r="3.5"/><circle class="g" data-id="gastriques" cx="201" cy="220" r="3.5"/><circle class="g" data-id="gastriques" cx="188" cy="230" r="3.5"/><circle class="g" data-id="gastriques" cx="183" cy="214" r="3.5"/>
<circle class="g" data-id="intestinales" cx="150" cy="302" r="3"/><circle class="g" data-id="intestinales" cx="150" cy="326" r="3"/><circle class="g" data-id="intestinales" cx="150" cy="350" r="3"/><circle class="g" data-id="intestinales" cx="152" cy="374" r="3"/>
<ellipse class="o" data-id="bouche" cx="150" cy="44" rx="11" ry="6"/>
<circle class="g" data-id="salivaires" cx="133" cy="49" r="5.5"/><circle class="g" data-id="salivaires" cx="167" cy="49" r="5.5"/>
<text class="lbl" x="176" y="47">Bouche</text><text class="lbl2" x="176" y="58">bol alimentaire</text>
<text class="lbl" x="160" y="112">Œsophage</text><text class="lbl2" x="160" y="123">bol alimentaire</text>
<text class="lbl" x="52" y="200">Foie</text>
<text class="lbl" x="218" y="200">Estomac</text><text class="lbl2" x="218" y="211">chyme</text>
<text class="lbl" x="206" y="264">Pancréas</text>
<text class="lbl" x="204" y="332">Intestin grêle</text><text class="lbl2" x="204" y="343">chyle</text>
<text class="lbl" x="22" y="332">Gros intestin</text><text class="lbl2" x="22" y="343">matières fécales</text>
<text class="lbl" x="162" y="446">Anus</text>
<circle id="dot" r="7" cx="0" cy="0" style="transform:translate(150px,46px);opacity:0"/>
</svg>
</div>
<div class="card" id="panel" aria-live="polite"></div>
</div>
</section>

<section id="s2">
<div class="cards" id="cons"></div>
<div class="card" id="consD"></div>
<div class="card" style="margin-top:14px">
<h2>Défi : associe l’aliment</h2>
<div id="qz"></div>
</div>
</section>

<section id="s3">
<div class="card">
<h2>Compose ton assiette</h2>
<p class="sub" style="margin-bottom:8px">Ajoute des aliments et ajuste les portions. Énergie : 1 g de glucides ou de protéines ≈ 4 kcal, 1 g de lipides ≈ 9 kcal.</p>
<div class="chips" id="pick"></div>
<div id="plate"></div>
<div id="tot"></div>
</div>
</section>

<section id="s4">
<div class="card">
<h2>Mécanique ou chimique ?</h2>
<p class="sub" style="margin-bottom:8px">Transformation mécanique : les aliments sont broyés, brassés, poussés. Transformation chimique : des substances (enzymes, acides) les décomposent en nutriments. Classe chaque action.</p>
<div class="tr" id="tr"></div>
<p class="big" id="sc"></p>
</div>
</section>
<section id="s5">
<div class="grid">
<div class="card" id="live"></div>
<div class="card">
<h2>Donne à manger au système digestif</h2>
<p class="sub" style="margin-bottom:6px">Clique sur des aliments : les organes et glandes se mettent au travail. Plus ils sont sollicités, plus ils pulsent vite et fort.</p>
<div class="chips" id="feed"></div>
<div class="chips" id="meal"></div>
<p id="sum" style="font-weight:600"></p>
<div id="act"></div>
</div>
</div>
</section>

<section id="s6">
<div class="molbar">
<button class="btn" data-mol="carb" aria-pressed="true">Glucides complexes</button>
<button class="btn" data-mol="lip" aria-pressed="false">Lipides</button>
<button class="btn" data-mol="prot" aria-pressed="false">Protéines</button>
<button class="btn solid" id="digBtn" style="margin-left:auto">Digérer</button>
<button class="btn" id="absBtn" disabled>Passer dans le sang</button>
<button class="btn" id="resetBtn">Recommencer</button>
</div>
<div class="grid">
<div class="card" id="molCard">
<svg id="molCarb" class="mol on" viewBox="0 0 430 260" role="img" aria-label="Molécule de glucide complexe qui se décompose en glucoses et passe dans le sang">
<g id="cwall"></g><g id="cbonds"></g><g id="cunits"></g>
</svg>
<svg id="molLip" class="mol" viewBox="0 0 430 300" role="img" aria-label="Triglycéride qui se décompose en glycérol et acides gras et passe dans le sang">
<g id="lwall"></g><g id="lbonds"></g><g id="lunits"></g>
</svg>
<svg id="molProt" class="mol" viewBox="0 0 430 260" role="img" aria-label="Chaîne de protéine qui se décompose en acides aminés et passe dans le sang">
<g id="pwall"></g><g id="pbonds"></g><g id="punits"></g>
</svg>
</div>
<div class="card" id="molInfo"></div>
</div>
</section>
</main>

<script>
const $=s=>document.querySelector(s),$$=s=>[...document.querySelectorAll(s)];
/* ---------- Données ---------- */
const O={
bouche:{n:'Bouche',t:'mc',food:'Bol alimentaire',d:'Point d’entrée des aliments.',l:['Les dents coupent et broient les aliments; la langue les malaxe avec la salive : c’est le bol alimentaire (transformation mécanique).','La salive contient une enzyme (amylase) qui commence à digérer l’amidon (transformation chimique).'],g:'Glandes salivaires'},
oesophage:{n:'Œsophage',t:'m',food:'Bol alimentaire',d:'Tube musculeux qui relie le pharynx à l’estomac.',l:['Le pharynx, carrefour entre la bouche et l’œsophage, achemine le bol alimentaire par le réflexe de déglutition.','Ses contractions (péristaltisme) poussent ensuite le bol alimentaire vers l’estomac.','Il n’effectue pas de digestion chimique.'],g:'aucune'},
estomac:{n:'Estomac',t:'mc',food:'Chyme',d:'Poche musculeuse où les aliments séjournent quelques heures.',l:['Ses muscles brassent les aliments (mécanique).','Le suc gastrique (acide et pepsine) commence la digestion des protéines (chimique).','Le bol alimentaire devient une bouillie liquide : le chyme.'],g:'Glandes gastriques'},
grele:{n:'Intestin grêle',t:'mc',food:'Chyle',d:'Tube d’environ 6 à 7 m, replié sur lui-même.',l:['Reçoit la bile, le suc pancréatique et le suc intestinal : la digestion chimique s’y termine.','Le chyme, mélangé à ces sucs digestifs, devient le chyle, riche en nutriments.','Absorbe la plupart des nutriments du chyle vers le sang grâce à ses villosités (mécanique et absorption).'],g:'Foie, pancréas, glandes intestinales'},
gros:{n:'Gros intestin',t:'',food:'Matières fécales',d:'Tube plus large mais plus court (environ 1,5 m).',l:['Absorbe l’eau et des sels minéraux restants du chyle.','Les résidus non digérés (fibres, cellules mortes, bactéries) forment les matières fécales.','Abrite des bactéries utiles.'],g:'aucune'},
anus:{n:'Rectum et anus',t:'',food:'Matières fécales',d:'Fin du tube digestif.',l:['Les matières fécales sont stockées dans le rectum puis évacuées par l’anus (évacuation des déchets).'],g:'aucune'}};
const G={
salivaires:{n:'Glandes salivaires',o:'Bouche',s:'Salive',d:'Humidifie les aliments, facilite la mastication et la déglutition. Son amylase attaque l’amidon (glucides).'},
gastriques:{n:'Glandes gastriques',o:'Estomac (paroi)',s:'Suc gastrique',d:'Contient de l’acide chlorhydrique et la pepsine, qui décompose les protéines. Le mucus protège la paroi.'},
foie:{n:'Foie',o:'Déverse dans l’intestin grêle (duodénum)',s:'Bile',d:'Le foie sécrète en continu la bile, qui aide à digérer les lipides en les fragmentant en petites gouttelettes (émulsion). Le foie stocke aussi des nutriments.'},
vesicule:{n:'Vésicule biliaire',o:'Sous le foie, reliée au duodénum',s:'Bile (stockage)',d:'La vésicule biliaire ne fabrique pas la bile : elle la reçoit du foie, la stocke et la concentre entre les repas. Quand un repas gras arrive dans l’intestin grêle, elle se contracte et libère la bile.'},
pancreas:{n:'Pancréas',o:'Déverse dans l’intestin grêle (duodénum)',s:'Suc pancréatique',d:'Riche en enzymes qui digèrent glucides, protéines et lipides; neutralise l’acidité venue de l’estomac.'},
intestinales:{n:'Glandes intestinales',o:'Paroi de l’intestin grêle',s:'Suc intestinal',d:'Ses enzymes terminent la digestion des glucides et des protéines en nutriments absorbables.'}};
const TB={m:['Mécanique','b-m'],c:['Chimique','b-c']};
const C={
eau:{n:'Eau',f:'Transporte les nutriments et les déchets, régule la température, sert de milieu aux réactions chimiques. Elle forme environ 60 % du corps.',s:['Eau','Fruits et légumes','Soupes','Lait'],q:['concombre','melon d’eau']},
protéines:{n:'Protéines',f:'Construisent et réparent les tissus (muscles, peau); fabriquent enzymes et anticorps.',s:['Viandes et substituts','Poissons','Œufs','Légumineuses','Produits laitiers'],q:['poulet','tofu','œufs','lentilles']},
glucides:{n:'Glucides',f:'Principale source d’énergie rapide pour le corps et le cerveau.',s:['Pain et céréales','Pâtes, riz','Pommes de terre','Fruits','Sucre'],q:['pain','pâtes','riz','pomme de terre']},
lipides:{n:'Lipides',f:'Énergie de réserve, isolation, protection des organes, transport de certaines vitamines.',s:['Huiles','Beurre','Noix','Poissons gras','Avocat'],q:['huile d’olive','beurre','noix','avocat']},
vitamines:{n:'Vitamines',f:'Petites quantités indispensables au bon fonctionnement et à la protection du corps (ex. vitamine C, vitamine D).',s:['Fruits','Légumes','Produits laitiers','Céréales entières'],q:['orange','poivron','kiwi','carotte']},
sels:{n:'Sels minéraux',f:'Ex. calcium (os, dents), fer (sang), sodium et potassium (muscles, nerfs).',s:['Produits laitiers (calcium)','Viandes (fer)','Légumes verts','Sel de table'],q:['sel de table','épinards']}};
const F=[['Pomme',.3,14,.2,'Fibres, vitamine C'],['Pain blanc',9,49,3,'Glucides; peu de fibres'],['Poulet cuit',27,0,7,'Riche en protéines, fer'],['Riz cuit',2.7,28,.3,'Glucides; pauvre en lipides'],['Lait entier',3.2,4.8,3.6,'Calcium, vitamine D'],['Fromage cheddar',25,1.3,33,'Calcium; riche en lipides'],['Beurre',.9,.1,81,'Très riche en lipides'],['Huile d’olive',0,0,100,'Lipides seulement'],['Œuf',13,1,11,'Protéines, vitamines A et D'],['Lentilles cuites',9,20,.4,'Protéines végétales, fibres, fer'],['Brocoli',2.8,7,.4,'Vitamines C et K, fibres'],['Saumon',20,0,13,'Protéines, oméga-3, vitamine D'],['Chocolat noir',8,46,31,'Énergie concentrée; fer'],['Frites',3.4,41,15,'Glucides et lipides'],['Salade verte',1.4,2,.2,'Fibres, vitamines, beaucoup d’eau']];
const TR=[['Les dents broient un morceau de pain','m','Bouche'],['L’amylase de la salive attaque l’amidon','c','Bouche'],['Les muscles de l’estomac brassent les aliments','m','Estomac'],['Le suc gastrique décompose les protéines','c','Estomac'],['Le péristaltisme pousse le bol vers l’estomac','m','Œsophage'],['Le suc pancréatique digère glucides, protéines, lipides','c','Intestin grêle (via pancréas)'],['Les enzymes intestinales terminent la digestion','c','Intestin grêle'],['La langue malaxe le bol alimentaire','m','Bouche']];

/* ---------- Onglets ---------- */
$$('#tabs button').forEach(b=>b.onclick=()=>{$$('#tabs button').forEach(x=>x.setAttribute('aria-selected',x==b));$$('section').forEach(s=>s.classList.toggle('on',s.id==b.dataset.t))});

/* ---------- Tube et glandes ---------- */
const intro=()=>{$('#panel').innerHTML=`<h2>À quoi sert le tube digestif ?</h2><ul><li><b>Décomposer</b> les aliments en petites molécules (nutriments).</li><li><b>Absorber</b> les nutriments et l’eau vers le sang.</li><li><b>Évacuer</b> les déchets non digérés.</li></ul><p class="sub">Clique sur un organe (rose) ou une glande (jaune), ou lance « Suivre un aliment ».</p><p class="sub"><b>Vocabulaire :</b> bol alimentaire (bouche, pharynx, œsophage) → chyme (estomac) → chyle (intestin grêle) → matières fécales (gros intestin).</p>`};
function show(id){
$$('.sel').forEach(e=>e.classList.remove('sel'));$$(`[data-id="${id}"]`).forEach(e=>e.classList.add('sel'));
if(O[id]){const o=O[id];const b=o.t?[...o.t].map(k=>`<span class="badge ${TB[k][1]}">${TB[k][0]}</span>`).join(''):'<span class="badge b-k">Absorption / évacuation</span>';
const fb=o.food?`<span class="badge" style="color:var(--acc);border-color:var(--acc)">Contenu : ${o.food}</span>`:'';
$('#panel').innerHTML=`<span class="badge b-k">Organe du tube digestif</span><h2>${o.n}</h2>${b}${fb}<p>${o.d}</p><ul>${o.l.map(x=>`<li>${x}</li>`).join('')}</ul><p><b>Glandes associées :</b> ${o.g}</p>`}
else{const g=G[id];$('#panel').innerHTML=`<span class="badge b-k">Glande digestive</span><h2>${g.n}</h2><span class="badge b-c">Chimique</span><p><b>Sécrète :</b> ${g.s}</p><p><b>Où :</b> ${g.o}</p><p>${g.d}</p>`}}
$$('[data-id]').forEach(e=>{e.setAttribute('tabindex',0);e.setAttribute('role','button');const id=e.dataset.id;e.setAttribute('aria-label',(O[id]||G[id]).n);e.onclick=()=>{stop();show(id)};e.onkeydown=k=>{if(k.key=='Enter'||k.key==' '){k.preventDefault();stop();show(id)}}});
const mode=m=>{$('#svg').dataset.mode=m;$('#mTube').setAttribute('aria-pressed',m=='tube');$('#mGl').setAttribute('aria-pressed',m=='glandes')};
$('#mTube').onclick=()=>mode('tube');$('#mGl').onclick=()=>mode('glandes');
const path=[['bouche',150,46],['oesophage',150,130],['estomac',186,215],['grele',150,300],['grele',150,364],['gros',110,330],['gros',150,282],['gros',190,330],['anus',150,442]];
let tm=[];function stop(){tm.forEach(clearTimeout);tm=[];$('#go').textContent='Suivre un aliment';$('#dot').style.opacity=0}
$('#go').onclick=()=>{stop();mode('tube');const d=$('#dot');$('#go').textContent='En cours…';d.style.transition='none';d.style.transform=`translate(150px,20px)`;d.style.opacity=1;void d.getBoundingClientRect();d.style.transition='';
path.forEach((p,i)=>tm.push(setTimeout(()=>{d.style.transform=`translate(${p[1]}px,${p[2]}px)`;show(p[0])},i*2400+100)));
tm.push(setTimeout(()=>{$('#go').textContent='Suivre un aliment';d.style.opacity=0},path.length*2400+1200))};
intro();

/* ---------- Types d'aliments ---------- */
$('#cons').innerHTML=Object.entries(C).map(([k,c])=>`<button data-k="${k}" aria-pressed="false"><b>${c.n}</b><small>${c.s[0]}</small></button>`).join('');
function cons(k){$$('#cons button').forEach(b=>b.setAttribute('aria-pressed',b.dataset.k==k));const c=C[k];$('#consD').innerHTML=`<h2>${c.n}</h2><p>${c.f}</p><b>Sources principales</b><div class="chips">${c.s.map(s=>`<span class="chip">${s}</span>`).join('')}</div>`}
$$('#cons button').forEach(b=>b.onclick=()=>cons(b.dataset.k));
$('#consD').innerHTML='<p class="sub" style="margin:0">Choisis un constituant pour voir sa fonction et ses sources.</p>';
let qs=0,qn=0;
function quiz(){const keys=Object.keys(C),k=keys[Math.floor(Math.random()*keys.length)],c=C[k];
const good=c.q[Math.floor(Math.random()*c.q.length)];
const bad=keys.filter(x=>x!=k).map(x=>C[x].q[Math.floor(Math.random()*C[x].q.length)]).filter(x=>!c.q.includes(x)).sort(()=>Math.random()-.5).slice(0,3);
const opts=[...bad,good].sort(()=>Math.random()-.5);
$('#qz').innerHTML=`<p>Lequel de ces aliments est une source principale de <b>${c.n.toLowerCase()}</b> ?</p><div class="opts">${opts.map(o=>`<button>${o}</button>`).join('')}</div><p class="fb" id="fb">Score : ${qs} / ${qn}</p>`;
$$('#qz .opts button').forEach(b=>b.onclick=()=>{qn++;const ok=b.textContent==good;if(ok)qs++;$$('#qz .opts button').forEach(x=>{x.disabled=true;if(x.textContent==good)x.classList.add('ok')});if(!ok)b.classList.add('ko');
$('#fb').innerHTML=`${ok?'Bravo !':'Pas tout à fait.'} ${good[0].toUpperCase()+good.slice(1)} : source de ${c.n.toLowerCase()}. Score : ${qs} / ${qn} <button class="btn" id="nx">Question suivante</button>`;$('#nx').onclick=quiz})}
quiz();

/* ---------- Valeur énergétique ---------- */
const Q={};[['Poulet cuit',100],['Riz cuit',150],['Brocoli',80]].forEach(([n,g])=>Q[n]=g);
const kc=f=>4*f[1]+4*f[2]+9*f[3];
$('#pick').innerHTML=F.map(f=>`<button class="chip" data-n="${f[0]}">+ ${f[0]} <small>(${Math.round(kc(f))} kcal/100 g)</small></button>`).join('');
$$('#pick button').forEach(b=>b.onclick=()=>{Q[b.dataset.n]=Q[b.dataset.n]||100;plate()});
function plate(){const rows=F.filter(f=>Q[f[0]]!=null);let P=0,Gl=0,L=0;
$('#plate').innerHTML=rows.length?rows.map(f=>{const q=Q[f[0]],r=q/100;P+=f[1]*r;Gl+=f[2]*r;L+=f[3]*r;
return `<div class="row"><div><b>${f[0]}</b><small>${f[4]}</small></div><input type="range" min="10" max="400" step="10" value="${q}" data-n="${f[0]}" aria-label="Portion de ${f[0]}"><span>${q} g · ${Math.round(kc(f)*r)} kcal</span><button class="x" data-r="${f[0]}" aria-label="Retirer ${f[0]}">×</button></div>`}).join(''):'<p class="sub">Ton assiette est vide. Ajoute un aliment ci-dessus.</p>';
const e=[P*4,Gl*4,L*9],T=e[0]+e[1]+e[2],pc=x=>T?Math.round(x/T*100):0;
$('#tot').innerHTML=`<p style="margin:14px 0 0"><span class="big">${Math.round(T)} kcal</span> <span class="sub">(${Math.round(T*4.184)} kJ)</span></p>
<div class="stack" aria-hidden="true"><i style="width:${pc(e[0])}%;background:#3F7CAC"></i><i style="width:${pc(e[1])}%;background:#E0A81F"></i><i style="width:${pc(e[2])}%;background:#C4574C"></i></div>
<div class="lg"><span style="--c:#3F7CAC">Protéines ${Math.round(P)} g · ${pc(e[0])} %</span><span style="--c:#E0A81F">Glucides ${Math.round(Gl)} g · ${pc(e[1])} %</span><span style="--c:#C4574C">Lipides ${Math.round(L)} g · ${pc(e[2])} %</span></div>
<p class="sub" style="margin-top:10px">Repère : environ ${Math.round(T/20)} % d’un besoin de 2 000 kcal/jour (varie selon l’âge, le sexe et l’activité).${T&&e[2]/T>.4?' Ce repas est riche en lipides.':''}${T&&Gl<10&&P>0?'':''}</p>`;
$$('#plate input').forEach(i=>i.oninput=()=>{Q[i.dataset.n]=+i.value;plate();$(`#plate input[data-n="${i.dataset.n}"]`).focus()});
$$('#plate .x').forEach(x=>x.onclick=()=>{delete Q[x.dataset.r];plate()})}
plate();

/* ---------- Transformations ---------- */
let sc=0,done=0;
$('#tr').innerHTML=TR.map((t,i)=>`<div class="it" data-i="${i}"><span class="a">${t[0]}</span><span><button class="btn" data-a="m">Mécanique</button> <button class="btn" data-a="c">Chimique</button></span><span class="fbk"></span></div>`).join('');
const upd=()=>$('#sc').textContent=`Score : ${sc} / ${TR.length}`;upd();
$$('#tr .it').forEach(it=>it.querySelectorAll('button').forEach(b=>b.onclick=()=>{const t=TR[it.dataset.i],ok=b.dataset.a==t[1];
it.querySelectorAll('button').forEach(x=>x.disabled=true);if(ok)sc++;done++;
it.querySelector('.fbk').innerHTML=`<b style="color:var(--${ok?'ok':'ko'})">${ok?'Correct.':'Non.'}</b> Transformation ${t[1]=='m'?'mécanique':'chimique'} · ${t[2]}.`;upd()}));

/* ---------- Repas et réactions ---------- */
{const s2=$('#svg').cloneNode(true);s2.id='svg2';s2.dataset.mode='live';s2.setAttribute('aria-label','Organes en activité');s2.querySelector('#dot').remove();
s2.querySelectorAll('[data-id]').forEach(e=>{e.removeAttribute('tabindex');e.removeAttribute('role');e.removeAttribute('aria-label');e.classList.remove('sel')});$('#live').appendChild(s2);
const PORT={'Beurre':30,'Huile d’olive':15,'Fromage cheddar':40,'Chocolat noir':30},FIB={'Pomme':2.4,'Lentilles cuites':8,'Brocoli':2.6,'Salade verte':1.5,'Pain blanc':2.7,'Frites':3.8,'Chocolat noir':10,'Riz cuit':.4};
const M={},pt=n=>PORT[n]||100;
const lv=(x,a,b,c)=>x>=c?3:x>=b?2:x>=a?1:0;
const S=[
['salivaires','Glandes salivaires',['Aucune salive requise.','Un peu de salive pour humidifier.','Salive abondante : l’amidon est attaqué dès la bouche.','Salive très abondante : beaucoup de glucides à digérer.'],['salivaires','bouche','oesophage']],
['estomac','Estomac (brassage)',['Au repos.','Brassage léger.','Brassage soutenu : le repas est copieux.','Brassage prolongé : un repas gras ou copieux reste plus longtemps dans l’estomac.'],['estomac']],
['gastriques','Glandes gastriques',['Peu de suc gastrique.','Un peu de suc gastrique.','Beaucoup d’acide et de pepsine pour les protéines.','Sécrétion importante de pepsine : repas très riche en protéines.'],['gastriques']],
['foie','Foie et vésicule biliaire',['Peu de bile nécessaire.','Un peu de bile.','Le foie sécrète davantage de bile, et la vésicule biliaire se contracte pour la libérer.','Sécrétion importante de bile : repas très gras, digestion plus longue.'],['foie','vesicule']],
['pancreas','Pancréas',['Au repos.','Peu d’enzymes.','Il libère beaucoup d’enzymes (glucides, protéines, lipides).','Production intense d’enzymes pancréatiques : repas riche et lourd.'],['pancreas']],
['intestinales','Glandes intestinales',['Au repos.','Un peu de suc intestinal.','Suc intestinal abondant pour finir la digestion.','Sécrétion intense : beaucoup de glucides et de protéines à terminer.'],['intestinales']],
['grele','Intestin grêle',['Au repos.','Absorption modérée.','Forte absorption de nutriments.','Absorption très intense : repas très énergétique.'],['grele']],
['gros','Gros intestin',['Peu de résidus.','Quelques résidus, un peu d’eau à récupérer.','Résidus de fibres à traiter : eau récupérée, selles formées.','Beaucoup de fibres : le transit s’active.'],['gros','anus']]];
$('#feed').innerHTML=F.map(f=>`<button class="chip" data-n="${f[0]}">${f[0]} <small>(${pt(f[0])} g)</small></button>`).join('');
$$('#feed button').forEach(b=>b.onclick=()=>{M[b.dataset.n]=(M[b.dataset.n]||0)+pt(b.dataset.n);run()});
function run(){let P=0,G=0,L=0,fib=0,mass=0;const list=F.filter(f=>M[f[0]]);
list.forEach(f=>{const r=M[f[0]]/100;P+=f[1]*r;G+=f[2]*r;L+=f[3]*r;fib+=(FIB[f[0]]||0)*r;mass+=M[f[0]]});
const kcal=4*P+4*G+9*L,on=mass>0;
const lev={salivaires:on?Math.max(1,lv(G,10,30,60)):0,estomac:on?Math.max(1,lv(mass,150,300,500),lv(L,10,25,45)):0,gastriques:lv(P,3,12,30),foie:lv(L,3,10,25),pancreas:Math.max(lv(L,5,15,30),lv(G,20,50,100),lv(P,8,20,40)),intestinales:Math.max(lv(G,15,40,80),lv(P,8,20,40)),grele:lv(kcal,50,300,600),gros:lv(fib,1,4,8)};
$('#meal').innerHTML=list.length?list.map(f=>`<button class="chip" data-r="${f[0]}" title="Retirer une portion">${f[0]} ${M[f[0]]} g ×</button>`).join('')+'<button class="btn" id="clr">Vider</button>':'';
$$('#meal [data-r]').forEach(b=>b.onclick=()=>{const n=b.dataset.r;M[n]-=pt(n);if(M[n]<=0)delete M[n];run()});
if($('#clr'))$('#clr').onclick=()=>{for(const k in M)delete M[k];run()};
$('#act').innerHTML=S.map(([id,n,msg])=>{const l=lev[id];return `<div class="rw"><b>${n}</b><span class="mt" aria-label="Niveau ${l} sur 3">${[1,2,3].map(i=>`<i class="${i<=l?'on':''}"></i>`).join('')}</span><small>${msg[l]}</small></div>`}).join('');
s2.querySelectorAll('[data-id]').forEach(e=>e.classList.remove('act'));
S.forEach(([id,,,ids])=>{const l=lev[id];ids.forEach(i=>{const l2=on&&i!=id?Math.max(l,1):l;s2.querySelectorAll(`[data-id="${i}"]`).forEach(e=>{if(l2>0){e.classList.add('act');e.style.setProperty('--s',1+.1*l2);e.style.setProperty('--d',(2-.5*l2)+'s')}})})});
const top=S.filter(s=>lev[s[0]]>=2).map(s=>s[1].toLowerCase());
const e3=[['protéines',P*4],['glucides',G*4],['lipides',L*9]].sort((a,b)=>b[1]-a[1])[0];
$('#sum').textContent=!on?'Ajoute des aliments pour voir les organes réagir.':`Repas d’environ ${Math.round(kcal)} kcal, surtout riche en ${e3[0]}.${top.length?' Les plus sollicités : '+top.join(', ')+'.':' Digestion légère.'}`}
run()}

/* ---------- Digestion des nutriments (niveau moléculaire) ---------- */
{const hex=(cx,cy,r)=>{const p=[];for(let i=0;i<6;i++){const a=Math.PI/180*(60*i-90);p.push((cx+r*Math.cos(a)).toFixed(1)+','+(cy+r*Math.sin(a)).toFixed(1))}return p.join(' ')};
const zig=(x0,y0,drift,segs)=>{const pts=[[x0,y0]],segH=140/segs;for(let i=1;i<=segs;i++){const x=x0+drift*(i/segs)+((i<segs)?(i%2?15:-15):0);const y=y0-segH*i;pts.push([x,y])}return{s:pts.map(p=>p[0].toFixed(1)+','+p[1].toFixed(1)).join(' '),last:pts[pts.length-1]}};
const WX=290,BX0=302,BX1=420; // position de la paroi et zone sanguine (communes aux 3 schémas)
const wall=(h,y0)=>`<line class="wall" x1="${WX}" y1="${y0}" x2="${WX}" y2="${y0+h}"/><rect class="blood" x="${BX0}" y="${y0}" width="${BX1-BX0}" height="${h}" rx="10"/><text class="wlbl" x="${WX-88}" y="${y0+16}">Intestin grêle (lumière)</text><text class="wlbl" x="${BX0+16}" y="${y0+16}">Sang</text>`;
const fmt=n=>Math.round(n*10)/10;

/* Glucides : chaîne d'amidon -> glucoses -> sang */
{const cy=120,r=21,cx=[45,90,135,180,225];
const coff=[{tx:-15,ty:-42,rz:-22},{tx:-8,ty:44,rz:14},{tx:0,ty:-55,rz:0},{tx:8,ty:44,rz:-14},{tx:15,ty:-42,rz:22}];
const targets=[{x:360,y:35},{x:360,y:80},{x:360,y:125},{x:360,y:170},{x:360,y:215}];
let bonds='',units='';
for(let i=0;i<cx.length-1;i++)bonds+=`<line class="bond" x1="${cx[i]}" y1="${cy}" x2="${cx[i+1]}" y2="${cy}" stroke="var(--organ2)" stroke-width="9"/>`;
cx.forEach((x,i)=>{const o=coff[i],bx=fmt(targets[i].x-x-o.tx),by=fmt(targets[i].y-cy-o.ty);
units+=`<g class="piece" style="--tx:${o.tx}px;--ty:${o.ty}px;--rz:${o.rz}deg;--bx:${bx}px;--by:${by}px"><polygon class="unit" points="${hex(x,cy,r)}"/></g>`});
$('#cwall').innerHTML=wall(250,10);$('#cbonds').innerHTML=bonds;$('#cunits').innerHTML=units}

/* Lipides : triglycéride -> glycérol + 3 acides gras -> sang */
{const gx=[110,150,190],gy=270,gr=13,sy=236,drift=[-45,0,45];
const goff={tx:0,ty:10},foff=[{tx:-25,ty:-18},{tx:0,ty:-30},{tx:25,ty:-18}];
const targets=[{x:360,y:250},{x:360,y:60},{x:360,y:110},{x:360,y:160}]; // glycérol puis 3 acides gras
let bonds='',units='';
{const bx=fmt(targets[0].x-gx[1]-goff.tx),by=fmt(targets[0].y-gy-goff.ty);
units+=`<g class="piece" style="--tx:${goff.tx}px;--ty:${goff.ty}px;--bx:${bx}px;--by:${by}px"><line x1="${gx[0]}" y1="${gy}" x2="${gx[2]}" y2="${gy}" stroke="var(--gland)" stroke-width="8"/>${gx.map(x=>`<circle class="unit2" cx="${x}" cy="${gy}" r="${gr}"/>`).join('')}</g>`}
gx.forEach((x,i)=>bonds+=`<line class="bond" x1="${x}" y1="${gy-gr}" x2="${x}" y2="${sy}" stroke="var(--organ2)" stroke-width="6"/>`);
gx.forEach((x,i)=>{const z=zig(x,sy,drift[i],6),o=foff[i],t=targets[i+1],bx=fmt(t.x-z.last[0]-o.tx),by=fmt(t.y-z.last[1]-o.ty);
units+=`<g class="piece" style="--tx:${o.tx}px;--ty:${o.ty}px;--bx:${bx}px;--by:${by}px"><polyline class="zig" points="${z.s}"/><circle class="unit" cx="${z.last[0].toFixed(1)}" cy="${z.last[1].toFixed(1)}" r="9"/></g>`});
$('#lwall').innerHTML=wall(290,10);$('#lbonds').innerHTML=bonds;$('#lunits').innerHTML=units}

/* Protéines : chaîne d'acides aminés -> sang */
{const cy=120,r=17,cx0=[35,72,109,146,183,220];
const poff=[{tx:-15,ty:-28},{tx:-9,ty:32},{tx:-3,ty:-36},{tx:3,ty:36},{tx:9,ty:-32},{tx:15,ty:28}];
const targets=[{x:360,y:25},{x:360,y:63},{x:360,y:101},{x:360,y:139},{x:360,y:177},{x:360,y:215}];
let bonds='',units='';const cx=[],cyy=[];
cx0.forEach((x,i)=>{const y=cy+(i%2?15:-15);cx.push(x);cyy.push(y);if(i<cx0.length-1){const y2=cy+((i+1)%2?15:-15);bonds+=`<line class="bond" x1="${x}" y1="${y}" x2="${cx0[i+1]}" y2="${y2}" stroke="var(--organ2)" stroke-width="8"/>`}});
cx.forEach((x,i)=>{const o=poff[i],y=cyy[i],bx=fmt(targets[i].x-x-o.tx),by=fmt(targets[i].y-y-o.ty);
units+=`<g class="piece" style="--tx:${o.tx}px;--ty:${o.ty}px;--bx:${bx}px;--by:${by}px"><circle class="${i%2?'unit2':'unit'}" cx="${x}" cy="${y}" r="${r}"/></g>`});
$('#pwall').innerHTML=wall(250,10);$('#pbonds').innerHTML=bonds;$('#punits').innerHTML=units}

const INFO={
carb:{n:'Glucides complexes',before:`<span class="badge b-c">Digestion chimique</span><h2>Amidon → glucose</h2><p>L’amidon (glucide complexe) est une longue chaîne de molécules de <b>glucose</b> reliées entre elles.</p><ul><li><b>Bouche :</b> l’amylase salivaire commence à couper la chaîne.</li><li><b>Intestin grêle :</b> l’amylase pancréatique et les enzymes intestinales terminent le travail.</li></ul><p class="sub">Clique sur « Digérer » pour casser les liaisons.</p>`,
after:`<span class="badge b-c">Digestion chimique</span><h2>Amidon → glucose</h2><p><b>Résultat :</b> la chaîne est coupée en molécules de <b>glucose</b>, un glucide simple. Assez petit pour franchir la paroi de l’intestin grêle.</p><p class="sub">Clique sur « Passer dans le sang » pour l’absorption.</p>`,
abs:`<span class="badge b-k">Absorption</span><h2>Le glucose passe dans le sang</h2><p>Les molécules de glucose traversent la paroi de l’intestin grêle et entrent dans les vaisseaux sanguins. Le sang les distribue ensuite à toutes les cellules du corps, qui les utilisent comme source d’énergie.</p>`},
lip:{n:'Lipides',before:`<span class="badge b-c">Digestion chimique</span><h2>Triglycéride → glycérol + acides gras</h2><p>Un lipide alimentaire (triglycéride) est formé d’un <b>glycérol</b> relié à trois <b>acides gras</b>.</p><ul><li><b>Foie :</b> la bile émulsionne les lipides (les fragmente en petites gouttelettes) pour faciliter le travail des enzymes.</li><li><b>Pancréas :</b> la lipase pancréatique coupe les liaisons dans l’intestin grêle.</li></ul><p class="sub">Clique sur « Digérer » pour séparer les acides gras du glycérol.</p>`,
after:`<span class="badge b-c">Digestion chimique</span><h2>Triglycéride → glycérol + acides gras</h2><p><b>Résultat :</b> un <b>glycérol</b> et trois <b>acides gras</b>, assez petits pour traverser la paroi de l’intestin grêle.</p><p class="sub">Clique sur « Passer dans le sang » pour l’absorption.</p>`,
abs:`<span class="badge b-k">Absorption</span><h2>Le glycérol et les acides gras passent dans le sang</h2><p>Une fois dans la paroi intestinale, le glycérol et les acides gras sont souvent réassemblés puis passent dans la circulation (sang et lymphe), qui les transporte vers les cellules pour fournir de l’énergie ou être mis en réserve.</p>`},
prot:{n:'Protéines',before:`<span class="badge b-c">Digestion chimique</span><h2>Protéine → acides aminés</h2><p>Une protéine est une longue chaîne d’<b>acides aminés</b> reliés entre eux.</p><ul><li><b>Estomac :</b> la pepsine du suc gastrique commence à couper la chaîne.</li><li><b>Intestin grêle :</b> les enzymes du pancréas et de la paroi intestinale terminent le découpage.</li></ul><p class="sub">Clique sur « Digérer » pour casser les liaisons.</p>`,
after:`<span class="badge b-c">Digestion chimique</span><h2>Protéine → acides aminés</h2><p><b>Résultat :</b> la chaîne est coupée en <b>acides aminés</b> individuels, assez petits pour traverser la paroi de l’intestin grêle.</p><p class="sub">Clique sur « Passer dans le sang » pour l’absorption.</p>`,
abs:`<span class="badge b-k">Absorption</span><h2>Les acides aminés passent dans le sang</h2><p>Les acides aminés traversent la paroi de l’intestin grêle et entrent dans le sang, qui les transporte vers les cellules du corps pour construire de nouvelles protéines (muscles, enzymes, etc.).</p>`}};
let curMol='carb';
function molInfo(stage){$('#molInfo').innerHTML=INFO[curMol][stage]}
function switchMol(k){curMol=k;$$('.molbar [data-mol]').forEach(x=>x.setAttribute('aria-pressed',x.dataset.mol==k));
$$('.mol').forEach(s=>{s.classList.toggle('on',s.id=='mol'+(k=='carb'?'Carb':k=='lip'?'Lip':'Prot'));s.classList.remove('split','absorbed')});
$('#digBtn').disabled=false;$('#absBtn').disabled=true;molInfo('before')}
$$('.molbar [data-mol]').forEach(b=>b.onclick=()=>switchMol(b.dataset.mol));
$('#digBtn').onclick=()=>{$('.mol.on').classList.add('split');molInfo('after');$('#digBtn').disabled=true;$('#absBtn').disabled=false};
$('#absBtn').onclick=()=>{$('.mol.on').classList.add('absorbed');molInfo('abs');$('#absBtn').disabled=true};
$('#resetBtn').onclick=()=>{$('.mol.on').classList.remove('split','absorbed');molInfo('before');$('#digBtn').disabled=false;$('#absBtn').disabled=true};
molInfo('before')}
</script>
</body>
</html>
