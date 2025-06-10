<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8">
  <title>Carvesta Konfigurator</title>
  <style>
    html, body {
      margin: 0;
      padding: 0;
      height: 100%;
      overflow: hidden;
      font-family: sans-serif;
    }

    .container {
      position: relative;
      width: 100%;
      height: 100%;
    }

    .aidaform-wrapper {
      width: 100%;
      height: 100%;
    }

    .preview-box {
      position: fixed;
      top: 20px;
      right: 20px;
      width: 300px;
      height: 300px;
      background-color: black;
      display: flex;
      justify-content: center;
      align-items: center;
      z-index: 1000;
      border-radius: 12px;
      box-shadow: 0 0 12px rgba(0,0,0,0.4);
    }

    .preview-box img {
      max-width: 100%;
      max-height: 100%;
      border-radius: 8px;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="aidaform-wrapper">
      <div data-aidaform-app="form202405"
           data-url="https://carvesta.aidaform.com/konfiguration"
           data-width="100%"
           data-height="100%"
           data-do-resize>
      </div>
    </div>

    <div class="preview-box">
      <img id="previewImage" src="https://jana62.github.io/carvesta-configurator/boden-original.png" alt="Vorschau">
    </div>
  </div>

  <script>
    (function(){
      var r, d = document, gt = d.getElementById, cr = d.createElement, tg = d.getElementsByTagName, id = "aidaform-app";
      if(!gt.call(d, id)){
        r = cr.call(d, "script");
        r.id = id;
        r.src = "https://widget.aidaform.com/embed.js";
        (d.head || tg.call(d, "head")[0]).appendChild(r);
      }
    })();
  </script>

  <script>
    const previewMap = {
      "Original": "boden-original.png",
      "Marmor Hell": "boden-marmor-weiss.png",
      "Marmor Dunkel": "boden-marmor-schwarz.png",
      "Carbon": "boden-carbon.png",
      "Beton": "boden-beton.png",
      "Dunkel Holz": "boden-holz-schwarz.png",
      "Sockel": "sockel-normal.png",
      "Led-Sockel": "sockel-led.png",
      "Hexagon": "licht-hexagon.png",
      "Licht-Streifen": "licht-streifen.png",
      "Lichtreihe": "licht-panelreihe.png",
      "Lichtrahmen": "licht-rahmen.png",
      "Flächenlicht": "licht-panelgross.png",
      "Langgriff": "griff-lang.png",
      "Winkelgriff": "griff-eckig.png",
      "Kurzgriff": "griff-kurz.png",
      "Ja": "fenster-getoent.png",
      "Nein": "fenster-klar.png"
    };

    const observer = new MutationObserver(() => {
      const iframe = document.querySelector("iframe");
      const labels = iframe?.contentDocument?.querySelectorAll("label");

      if (labels) {
        labels.forEach(label => {
          label.addEventListener("click", () => {
            const selected = label.innerText.trim();
            const file = previewMap[selected];
            if (file) {
              document.getElementById("previewImage").src =
                `https://jana62.github.io/carvesta-configurator/${file}`;
            }
          });
        });
      }
    });

    const interval = setInterval(() => {
      const iframe = document.querySelector("iframe");
      const form = iframe?.contentDocument?.querySelector("form");
      if (form) {
        observer.observe(form, { childList: true, subtree: true });
        clearInterval(interval);
      }
    }, 1000);
  </script>
</body>
</html>
