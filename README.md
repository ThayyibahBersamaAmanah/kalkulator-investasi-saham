# kalkulator-investasi-saham
<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Kalkulator Investasi Saham</title>
  <style>
    body { font-family: Arial, sans-serif; padding: 20px; background: #f9f9f9; }
    .container { max-width: 500px; margin: auto; background: #fff; padding: 20px; border-radius: 10px; box-shadow: 0 0 10px rgba(0,0,0,0.1); }
    h2 { text-align: center; color: #333; }
    label { font-weight: bold; display: block; margin-top: 20px; }
    input[type=number] { width: 100%; padding: 10px; margin-top: 5px; border-radius: 5px; border: 1px solid #ccc; }
    .output { margin-top: 20px; font-size: 1.2em; }
    .output span { font-weight: bold; color: #2b7a78; }
  </style>
</head>
<body>
  <div class="container">
    <h2>Kalkulator Investasi Saham</h2>
    <label for="lembar">Jumlah Lembar Saham:</label>
    <input type="number" id="lembar" min="1" max="20000" value="1" oninput="hitung()">

    <div class="output">
      <p>Persentase Kepemilikan: <span id="persentase">0.001%</span></p>
      <p>Total Investasi: <span id="investasi">Rp11.760</span></p>
    </div>
  </div>

  <script>
    const hargaPerLembar = 11760;
    const totalSaham = 100000; // 100% saham

    function formatRupiah(angka) {
      return 'Rp' + angka.toLocaleString('id-ID');
    }

    function hitung() {
      const lembar = parseInt(document.getElementById('lembar').value) || 0;
      const investasi = lembar * hargaPerLembar;
      const persentase = (lembar / totalSaham * 100).toFixed(3);

      document.getElementById('persentase').textContent = persentase + '%';
      document.getElementById('investasi').textContent = formatRupiah(investasi);
    }

    window.onload = hitung;
  </script>
