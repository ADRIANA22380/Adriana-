<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<title>Pagamento PIX</title>
<style>
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #000;
  color: #fff;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.card {
  background: #111;
  border: 2px solid #ff2f92;
  border-radius: 16px;
  padding: 25px;
  width: 320px;
  text-align: center;
  box-shadow: 0 0 20px #ff2f92;
}

h1 { color: #ff2f92; }

.valor {
  font-size: 24px;
  margin: 10px 0;
}

.status {
  margin-top: 10px;
  font-weight: bold;
  color: #ffcc00;
}

.status.pago {
  color: #00ff88;
}

button {
  background: #ff2f92;
  color: #000;
  border: none;
  padding: 14px;
  width: 100%;
  font-size: 16px;
  border-radius: 10px;
  cursor: pointer;
  margin-top: 10px;
}

button:hover { background: #ff5fa7; }

.secundario {
  background: transparent;
  color: #ff2f92;
  border: 1px solid #ff2f92;
}

.secundario:hover {
  background: #ff2f92;
  color: #000;
}

.pix {
  margin-top: 15px;
  font-size: 12px;
  word-break: break-all;
  background: #000;
  padding: 10px;
  border-radius: 8px;
  border: 1px solid #ff2f92;
}

.qr {
  margin-top: 15px;
  display: none;
}

.qr img {
  width: 200px;
  border-radius: 12px;
  border: 2px solid #ff2f92;
  animation: pulsar 1.5s infinite;
}

@keyframes pulsar {
  0% { box-shadow: 0 0 5px #ff2f92; }
  50% { box-shadow: 0 0 25px #ff2f92; }
  100% { box-shadow: 0 0 5px #ff2f92; }
}
</style>
</head>
<body>

<div class="card">
  <h1>Pagamento PIX</h1>
  <div class="valor">R$ 9,99</div>
  <p>Descrição: pagamento + 18</p>

  <div class="status" id="status">⏳ Aguardando ação</div>

  <button onclick="pagarPix()">💗 Pagar com PIX</button>
  <button class="secundario" onclick="pagarMensal()">🔁 Pagar por mês</button>
  <button class="secundario" onclick="mostrarQR()">📷 Mostrar QR Code</button>
  <button class="secundario" onclick="marcarPago()">✅ Marcar como Pago</button>

  <div class="pix">
    20bd9f29-7a78-4b48-8b8f-e28d30fdb23b
  </div>

  <div class="qr" id="qrCode">
    <img id="qrImg" src="" alt="QR Code PIX">
  </div>
</div>

<script>
const chavePix = "20bd9f29-7a78-4b48-8b8f-e28d30fdb23b";
const valor = "9.99";
const statusEl = document.getElementById("status");

function pagarPix() {
  statusEl.textContent = "⏳ Aguardando pagamento...";
  window.location.href =
    "pix://pay?key=" + chavePix + "&amount=" + valor + "&description=pagamento%20%2B%2018";
}

function pagarMensal() {
  statusEl.textContent = "⏳ Aguardando pagamento mensal...";
  window.location.href =
    "pix://pay?key=" + chavePix + "&amount=" + valor + "&description=pagamento%20mensal";
}

function mostrarQR() {
  const qrDiv = document.getElementById("qrCode");
  const qrImg = document.getElementById("qrImg");
  const dados = "PIX|" + chavePix + "|R$" + valor;
  qrImg.src =
    "https://api.qrserver.com/v1/create-qr-code/?size=300x300&data=" +
    encodeURIComponent(dados);
  qrDiv.style.display = "block";
}

function marcarPago() {
  statusEl.textContent = "✅ Pago";
  statusEl.classList.add("pago");
}
</script>

</body>
</html>
