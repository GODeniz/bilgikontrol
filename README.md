<!DOCTYPE html>
<html lang="tr">
<head>
  <meta charset="UTF-8">
  <title>BilgiKontrol</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f2f2f2;
      padding: 40px;
    }
    .kutu {
      background: white;
      padding: 20px;
      max-width: 600px;
      margin: auto;
      border-radius: 10px;
    }
    textarea {
      width: 100%;
      height: 120px;
    }
    button {
      margin-top: 10px;
      padding: 10px 20px;
      cursor: pointer;
    }
    .sonuc {
      margin-top: 15px;
      font-weight: bold;
    }
  </style>
</head>
<body>

<div class="kutu">
  <h1>BilgiKontrol</h1>
  <p>Metni yapıştır, paylaşmadan önce düşün.</p>

  <textarea id="metin" placeholder="Haber veya mesajı buraya yapıştır..."></textarea>
  <br>
  <button onclick="kontrolEt()">Kontrol Et</button>

  <div class="sonuc" id="sonuc"></div>
</div>

<script>
function kontrolEt() {
  let text = document.getElementById("metin").value.toLowerCase();
  let skor = 0;
  let nedenler = [];

  if (!text.includes("http")) {
    skor += 30;
    nedenler.push("Kaynak linki yok");
  }

  if (text.includes("şok") || text.includes("acil") || text.includes("hemen paylaş")) {
    skor += 30;
    nedenler.push("Duygu yüklü ifadeler var");
  }

  if (text.length < 60) {
    skor += 20;
    nedenler.push("Metin çok kısa");
  }

  let durum =
    skor >= 60 ? "🔴 Yüksek Risk" :
    skor >= 30 ? "🟡 Şüpheli" :
    "🟢 Düşük Risk";

  document.getElementById("sonuc").innerHTML =
    durum + "<br>Şüphe Skoru: " + skor +
    "<br><small>" + nedenler.join(" • ") + "</small>";
}
</script>

</body>
</html>
