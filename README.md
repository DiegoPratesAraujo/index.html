<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nível de Nerdice (Ndn)</title>
</head>
<body>
    <h2>Calcule seu Nível de Nerdice (Ndn)</h2>
    <form id="nerdForm">
        <input type="number" id="tn" placeholder="Tempo Nerd (TN) em horas" required><br>
        <input type="number" id="nppc" placeholder="Número de Pessoas que você Pegou Casualmente (NPPC)" required><br>
        <input type="number" id="idade" placeholder="Idade" required><br>
        <input type="number" id="pf" placeholder="Porcentagem para Ficção (F)" required><br>
        <input type="number" id="pc" placeholder="Porcentagem para Ciência (C)" required><br>
        <input type="number" id="pm" placeholder="Porcentagem para Matemática (M)" required><br>
        <input type="number" id="ph" placeholder="Porcentagem para Humanas (H)" required><br>
        <input type="number" id="pj" placeholder="Porcentagem para Jogos (J)" required><br>
        <button type="button" onclick="calcularNdn()">Calcular Ndn</button>
    </form>
    <p id="resultado"></p>

    <script>
        function calcularNdn() {
            const tn = parseFloat(document.getElementById('tn').value);
            const nppc = parseInt(document.getElementById('nppc').value);
            const idade = parseInt(document.getElementById('idade').value);
            const pf = parseFloat(document.getElementById('pf').value);
            const pc = parseFloat(document.getElementById('pc').value);
            const pm = parseFloat(document.getElementById('pm').value);
            const ph = parseFloat(document.getElementById('ph').value);
            const pj = parseFloat(document.getElementById('pj').value);

            // Cálculo de tempos dedicados a cada categoria
            const tempos = [
                (pf / 100) * tn,
                (pc / 100) * tn,
                (pm / 100) * tn,
                (ph / 100) * tn,
                (pj / 100) * tn,
            ];

            // Cálculo da VCN
            const media = tempos.reduce((a, b) => a + b, 0) / tempos.length;
            const vcn = tempos.reduce((acc, val) => acc + (val - media) ** 2, 0) / tempos.length;

            // Cálculo do Ndn
            const ndn = Math.log(tn / (((1 + nppc) ** 2 / idade) * (1 / (1 + vcn))));

            document.getElementById('resultado').textContent = `Ndn: ${ndn.toFixed(2)}`;
        }
    </script>
</body>
</html>
