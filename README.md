# kalkulator-investasi-saham
<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Kalkulator Investasi Saham</title>
  <script src="https://www.gstatic.com/firebasejs/9.22.2/firebase-app-compat.js"></script>
  <script src="https://www.gstatic.com/firebasejs/9.22.2/firebase-auth-compat.js"></script>
  <style>
    body { font-family: Arial, sans-serif; padding: 20px; background: #f9f9f9; }
    .container { max-width: 500px; margin: auto; background: #fff; padding: 20px; border-radius: 10px; box-shadow: 0 0 10px rgba(0,0,0,0.1); }
    h2 { text-align: center; color: #333; }
    label { font-weight: bold; display: block; margin-top: 20px; }
    input[type=number] { width: 100%; padding: 10px; margin-top: 5px; border-radius: 5px; border: 1px solid #ccc; }
    .output { margin-top: 20px; font-size: 1.2em; }
    .output span { font-weight: bold; color: #2b7a78; }
    #login-container { text-align: center; margin-bottom: 20px; }
  </style>
</head>
<body>
  <div class="container">
    <div id="login-container">
      <button id="login-btn">Login dengan Google</button>
      <p id="user-email" style="display:none;"></p>
    </div>

    <div id="app-content" style="display:none;">
      <h2>Kalkulator Investasi Saham</h2>
      <label for="lembar">Jumlah Lembar Saham:</label>
      <input type="number" id="lembar" min="1" max="20000" value="1" oninput="hitung()">

      <div class="output">
        <p>Persentase Kepemilikan: <span id="persentase">0.001%</span></p>
        <p>Total Investasi: <span id="investasi">Rp11.760</span></p>
      </div>
    </div>
  </div>

  <script>
    // Firebase config
    const firebaseConfig = {
      apiKey: "AIzaSyDTBZ1amBncNUcsgTpLZdSn0_z0kos-I1s",
      authDomain: "your-project-id.firebaseapp.com",
      projectId: "your-project-id",
      storageBucket: "your-project-id.appspot.com",
      messagingSenderId: "your-sender-id",
      appId: "your-app-id"
    };

    // Gmail whitelist
    const allowedEmails = ["tokobersamaamanah@gmail.com"];

    // Initialize Firebase
    firebase.initializeApp(firebaseConfig);
    const auth = firebase.auth();

    const loginBtn = document.getElementById("login-btn");
    const userEmailDisplay = document.getElementById("user-email");
    const appContent = document.getElementById("app-content");

    loginBtn.onclick = () => {
      const provider = new firebase.auth.GoogleAuthProvider();
      auth.signInWithPopup(provider).then(result => {
        const user = result.user;
        if (allowedEmails.includes(user.email)) {
          loginBtn.style.display = "none";
          userEmailDisplay.textContent = `Login sebagai: ${user.email}`;
          userEmailDisplay.style.display = "block";
          appContent.style.display = "block";
        } else {
          alert("Akses ditolak. Email tidak terdaftar.");
          auth.signOut();
        }
      }).catch(error => {
        console.error(error);
        alert("Gagal login: " + error.message);
      });
    };

    const hargaPerLembar = 11760;
    const totalSaham = 100000;

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

    window.onload = () => {
      // hide app content until login
      appContent.style.display = "none";
    };
  </script>
</body>
</html>
