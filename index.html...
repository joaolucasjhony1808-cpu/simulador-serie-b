<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<title>Simulador Série B</title>
<style>
body { font-family: Arial; padding: 15px; }
h1 { text-align: center; }
select, input, button { margin: 4px; }
table { width: 100%; border-collapse: collapse; margin-top: 15px; }
th, td { border: 1px solid #ccc; padding: 5px; text-align: center; }
.g4 { background: #c8f7c5; }
.z4 { background: #f7c5c5; }
</style>
</head>
<body>

<h1>Simulador da Série B</h1>

<h3>Inserir resultado</h3>

<select id="timeA"></select>
<input type="number" id="golsA" min="0" style="width:50px">
x
<input type="number" id="golsB" min="0" style="width:50px">
<select id="timeB"></select>

<br>
<button onclick="aplicarResultado()">Aplicar Resultado</button>

<table>
<thead>
<tr>
<th>Pos</th>
<th>Time</th>
<th>P</th>
<th>J</th>
<th>GP</th>
<th>GC</th>
<th>SG</th>
</tr>
</thead>
<tbody id="tabela"></tbody>
</table>

<script>
const times = [
"América-MG","Avaí","Botafogo-SP","Ceará","Chapecoense",
"Coritiba","CRB","Guarani","Ituano","Mirassol",
"Novorizontino","Operário","Paysandu","Ponte Preta",
"Santos","Sport","Vila Nova","Amazonas","Brusque","Goiás"
];

let dados = {};
times.forEach(t => dados[t] = {p:0,j:0,gp:0,gc:0});

const selA = document.getElementById("timeA");
const selB = document.getElementById("timeB");

times.forEach(t=>{
  selA.innerHTML += `<option>${t}</option>`;
  selB.innerHTML += `<option>${t}</option>`;
});

function aplicarResultado(){
  const A = selA.value;
  const B = selB.value;
  const gA = Number(golsA.value);
  const gB = Number(golsB.value);

  if(A===B || isNaN(gA) || isNaN(gB)){
    alert("Preencha corretamente");
    return;
  }

  dados[A].j++; dados[B].j++;
  dados[A].gp += gA; dados[A].gc += gB;
  dados[B].gp += gB; dados[B].gc += gA;

  if(gA > gB) dados[A].p += 3;
  else if(gB > gA) dados[B].p += 3;
  else { dados[A].p++; dados[B].p++; }

  atualizarTabela();
}

function atualizarTabela(){
  const corpo = document.getElementById("tabela");
  corpo.innerHTML = "";

  const ordem = Object.keys(dados).sort((a,b)=>{
    return dados[b].p - dados[a].p ||
           (dados[b].gp - dados[b].gc) - (dados[a].gp - dados[a].gc) ||
           dados[b].gp - dados[a].gp;
  });

  ordem.forEach((t,i)=>{
    let classe = "";
    if(i < 4) classe = "g4";
    if(i >= ordem.length-4) classe = "z4";

    corpo.innerHTML += `
    <tr class="${classe}">
      <td>${i+1}</td>
      <td>${t}</td>
      <td>${dados[t].p}</td>
      <td>${dados[t].j}</td>
      <td>${dados[t].gp}</td>
      <td>${dados[t].gc}</td>
      <td>${dados[t].gp - dados[t].gc}</td>
    </tr>`;
  });
}

atualizarTabela();
</script>

</body>
</html>
