<!DOCTYPE html>
<html lang="fr">
<head> 
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
  <title>Portail Privé</title>
  
  <!-- Configuration PWA standalone pour masquer la barre de navigation sur mobile -->
  <link rel="manifest" href="manifest.json">
  <meta name="theme-color" content="#030712">
  <meta name="apple-mobile-web-app-capable" content="yes">
  <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">

  <!-- Tailwind CSS pour un rendu haut de gamme -->
  <script src="https://cdn.tailwindcss.com"></script>

  <style>
    /* Palette personnalisée Jaune (#FACC15), Bleu Cobalt (#1D4ED8), et Blanc */
    body {
      background-color: #030712; /* Bleu nuit ultra-sombre */
      overflow: hidden;
      margin: 0;
      padding: 0;
      width: 100vw;
      height: 100vh;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
    }

    /* Écran de chargement ultra-premium */
    #splash-screen {
      position: fixed;
      inset: 0;
      background: radial-gradient(circle at center, #0b1528 0%, #030712 100%);
      z-index: 100;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: space-between;
      padding: 40px 20px;
      transition: opacity 0.8s cubic-bezier(0.16, 1, 0.3, 1), transform 0.8s cubic-bezier(0.16, 1, 0.3, 1);
    }

    /* Halo Lumineux Interactif Gemini (Bleu Cobalt + Jaune Or + Blanc) */
    .gemini-glow-container {
      position: relative;
      width: 180px;
      height: 180px;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .gemini-glow-outer {
      position: absolute;
      width: 140px;
      height: 140px;
      border-radius: 50%;
      /* Fusion de dégradés bleu cobalt, jaune or intense et blanc */
      background: linear-gradient(135deg, #1d4ed8 0%, #facc15 50%, #ffffff 100%);
      filter: blur(35px);
      opacity: 0.75;
      animation: morphingGlow 6s infinite alternate, rotateGlow 10s linear infinite;
    }

    .gemini-glow-core {
      position: absolute;
      width: 80px;
      height: 80px;
      border-radius: 50%;
      background: radial-gradient(circle, #ffffff 0%, rgba(250, 204, 21, 0.6) 40%, rgba(29, 78, 216, 0) 70%);
      filter: blur(10px);
      animation: pulseCore 2.5s infinite ease-in-out;
      z-index: 2;
    }

    /* Animation de particules stellaires en arrière-plan */
    .particle {
      position: absolute;
      background-color: rgba(250, 204, 21, 0.4);
      border-radius: 50%;
      pointer-events: none;
      animation: floatUp 8s infinite linear;
    }

    /* Keyframes d'animations fluides */
    @keyframes morphingGlow {
      0% { border-radius: 40% 60% 70% 30% / 40% 50% 60% 50%; transform: scale(0.9); }
      50% { border-radius: 65% 35% 55% 45% / 55% 45% 65% 35%; transform: scale(1.15); }
      100% { border-radius: 35% 65% 65% 35% / 45% 55% 45% 55%; transform: scale(0.95); }
    }

    @keyframes rotateGlow {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }

    @keyframes pulseCore {
      0%, 100% { transform: scale(0.9); opacity: 0.8; }
      50% { transform: scale(1.15); opacity: 1; filter: blur(14px); }
    }

    @keyframes floatUp {
      0% { transform: translateY(100vh) scale(0); opacity: 0; }
      50% { opacity: 0.8; }
      100% { transform: translateY(-10vh) scale(1); opacity: 0; }
    }

    /* Barre de progression haut de gamme style Pixel 9 Pro */
    .progress-bar-container {
      width: 160px;
      height: 3px;
      background: rgba(255, 255, 255, 0.08);
      border-radius: 10px;
      overflow: hidden;
      margin-top: 20px;
      border: 1px solid rgba(255, 255, 255, 0.05);
    }

    .progress-bar-fill {
      height: 100%;
      width: 0%;
      background: linear-gradient(90deg, #1d4ed8, #facc15, #ffffff);
      border-radius: 10px;
      transition: width 0.1s linear;
    }

    /* Structure d'intégration plein écran (Masquée initialement) */
    #main-frame-container {
      position: fixed;
      inset: 0;
      width: 100vw;
      height: 100vh;
      z-index: 10;
      opacity: 0;
      transform: scale(0.97);
      transition: opacity 1s cubic-bezier(0.16, 1, 0.3, 1), transform 1s cubic-bezier(0.16, 1, 0.3, 1);
      display: none;
    }

    iframe {
      width: 100%;
      height: 100%;
      border: none;
      outline: none;
    }

    /* Bannière d'aide à l'installation style PWA WhatsApp */
    #install-guide {
      position: fixed;
      bottom: 24px;
      left: 50%;
      transform: translateX(-50%) translateY(100px);
      width: 90%;
      max-width: 380px;
      z-index: 150;
      background: rgba(11, 21, 40, 0.95);
      backdrop-filter: blur(20px);
      border: 1px solid rgba(250, 204, 21, 0.2);
      border-radius: 24px;
      transition: transform 0.6s cubic-bezier(0.16, 1, 0.3, 1);
      box-shadow: 0 15px 35px rgba(0, 0, 0, 0.6);
    }

    #install-guide.show {
      transform: translateX(-50%) translateY(0);
    }

    /* Style du panneau d'annonces au bas du splash screen */
    .partner-carousel {
      width: 100%;
      max-width: 440px;
      background: rgba(255, 255, 255, 0.03);
      border: 1px solid rgba(250, 204, 21, 0.1);
      border-radius: 24px;
      padding: 16px;
      backdrop-filter: blur(10px);
    }

    /* Bouton flottant de retour aux annonces ou bascule */
    #dock-launcher {
      position: fixed;
      bottom: 20px;
      right: 20px;
      z-index: 90;
      background: linear-gradient(135deg, #1d4ed8 0%, #facc15 100%);
      border: 2px solid #ffffff;
      box-shadow: 0 8px 24px rgba(0, 0, 0, 0.5);
      transition: transform 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
    }
    #dock-launcher:hover {
      transform: scale(1.1) rotate(15deg);
    }

    /* Tiroir de sélection d'applications alternatives */
    #apps-drawer {
      position: fixed;
      inset: 0;
      z-index: 200;
      background-color: rgba(3, 7, 18, 0.9);
      backdrop-filter: blur(15px);
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      padding: 24px;
      opacity: 0;
      pointer-events: none;
      transition: opacity 0.4s ease;
    }
    #apps-drawer.open {
      opacity: 1;
      pointer-events: auto;
    }
  </style>
</head>
<body>

  <!-- Particules dynamiques en arrière-plan (Générées en JS) -->
  <div id="particle-container" class="absolute inset-0 overflow-hidden pointer-events-none z-0"></div>

  <!-- ======================================================== -->
  <!-- 1. ÉCRAN DE CHARGEMENT PREMIUM (JAUNE + BLEU + BLANC)  -->
  <!-- ======================================================== -->
  <div id="splash-screen">
    <!-- Espace de remplissage supérieur -->
    <div></div>

    <div class="flex flex-col items-center z-10 my-auto">
      <!-- Halo de démarrage stylisé -->
      <div class="gemini-glow-container">
        <div class="gemini-glow-outer"></div>
        <div class="gemini-glow-core"></div>
        <!-- Logo central dynamique -->
        <img id="splash-logo" src="https://res.cloudinary.com/dyxob1wcj/image/upload/v1781134790/oeqlbzjhuvhbpmrzdpgh.jpg" alt="Logo" class="absolute w-16 h-16 rounded-2xl object-cover z-10 shadow-2xl border-2 border-white/20 transition-transform duration-500 hover:scale-105">
      </div>

      <!-- Marque & Statuts de chargement -->
      <h2 id="splash-title" class="text-xl font-black tracking-widest text-white mt-8 uppercase flex items-center gap-1.5">
        <span>INITIALISATION</span>
        <span class="w-2 h-2 rounded-full bg-yellow-400 animate-ping"></span>
      </h2>
      <p id="splash-status" class="text-xs text-slate-300 mt-2 font-mono font-medium tracking-wide">Démarrage sécurisé en cours...</p>

      <!-- Barre de progression -->
      <div class="progress-bar-container">
        <div class="progress-bar-fill" id="progress-indicator"></div>
      </div>
      <span id="progress-text" class="text-[11px] text-yellow-400 font-bold font-mono mt-2.5">0%</span>
    </div>

    <!-- ZONE DE PUBLICITÉS ET APPLICATIONS COMPAGNONNES -->
    <div class="partner-carousel z-10 w-full">
      <div class="flex items-center justify-between mb-3 border-b border-white/5 pb-2">
        <span class="text-[10px] font-bold text-yellow-400 tracking-wider uppercase">Nos autres applications & services</span>
        <span class="text-[9px] bg-blue-600/30 text-blue-300 px-2 py-0.5 rounded-full font-semibold">Pub</span>
      </div>
      <div id="partner-list" class="space-y-2">
        <!-- Généré dynamiquement par JavaScript -->
      </div>
    </div>
  </div>


  <!-- ======================================================== -->
  <!-- 2. CONTENEUR DU GOOGLE SITE PLEIN ÉCRAN                  -->
  <!-- ======================================================== -->
  <div id="main-frame-container">
    <iframe id="target-app-frame" src="about:blank" allow="autoplay; camera; microphone; geolocation"></iframe>
  </div>

  <!-- BOUTON FLOTTANT DE RACCOURCI (AFFICHE LE PORTAIL D'APPLICATIONS) -->
  <button id="dock-launcher" onclick="toggleAppsDrawer(true)" class="w-12 h-12 rounded-full flex items-center justify-center pointer-events-auto hidden">
    <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.5" d="M4 6a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2H6a2 2 0 01-2-2V6zM14 6a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2V6zM4 16a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2H6a2 2 0 01-2-2v-2zM14 16a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2v-2z"></path>
    </svg>
  </button>

  <!-- ======================================================== -->
  <!-- TIROIR PRIVÉ D'APPLICATIONS ET PUBLICITÉS (DRAWER)       -->
  <!-- ======================================================== -->
  <div id="apps-drawer">
    <div class="w-full max-w-md bg-slate-900/90 border border-yellow-500/20 rounded-[2rem] p-6 text-center shadow-2xl relative">
      <button onclick="toggleAppsDrawer(false)" class="absolute top-4 right-4 text-slate-400 hover:text-white transition-colors">
        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
        </svg>
      </button>

      <h3 class="text-lg font-black text-white tracking-wide uppercase mb-1">Passer à une autre application</h3>
      <p class="text-xs text-slate-400 mb-6">Sélectionnez l'un de nos portails partenaires ci-dessous.</p>

      <!-- Liste d'applications dans le tiroir -->
      <div id="drawer-apps-list" class="space-y-3 mb-6">
        <!-- Inséré dynamiquement -->
      </div>

      <button onclick="switchApplication(APPS_PRODUCTION_CONFIG.targetAppUrl)" class="w-full bg-blue-600 hover:bg-blue-700 text-white font-bold py-3 rounded-xl transition-all text-sm">
        Retourner à l'Application Principale
      </button>
    </div>
  </div>


  <!-- ======================================================== -->
  <!-- 3. INSTRUCTION D'INSTALLATION (STYLE WHATSAPP NATIVE)     -->
  <!-- ======================================================== -->
  <div id="install-guide" class="p-5 flex items-center justify-between text-left">
    <div class="flex items-center space-x-3.5">
      <img id="guide-logo" src="https://res.cloudinary.com/dyxob1wcj/image/upload/v1781134790/oeqlbzjhuvhbpmrzdpgh.jpg" alt="App Logo" class="w-11 h-11 rounded-xl object-cover border border-yellow-500/20">
      <div>
        <h4 class="text-sm font-extrabold text-white">Installer l'Application</h4>
        <p class="text-[10px] text-slate-400 mt-0.5" id="install-instructions">Ajoutez-la à l'accueil pour masquer la barre d'adresse.</p>
      </div>
    </div>
    <button onclick="hideInstallGuide()" class="bg-yellow-400 hover:bg-yellow-500 text-slate-950 text-xs font-bold px-4 py-2 rounded-xl transition-all shadow-md">
      OK
    </button>
  </div>


  <!-- ========================================== -->
  <!-- 4. LOGIQUE SCRIPT & CONFIGURATIONS         -->
  <!-- ========================================== -->
  <script>
    // =========================================================================
    // 🛠️ CONFIGURATION UNIQUE : VOS LOGOS, VOTRE LIEN GOOGLE SITES ET VOS PUBS
    // =========================================================================
    const APPS_PRODUCTION_CONFIG = {
      // Lien direct de votre image Logo générée sur ImgBB (ex: https://i.ibb.co/xxxx/monlogo.png)
      logoUrl: "https://res.cloudinary.com/dyxob1wcj/image/upload/v1781134790/oeqlbzjhuvhbpmrzdpgh.jpg",

      // Votre application Google Sites à lancer en mode autonome et masqué
      targetAppUrl: "https://sites.google.com/view/x-press-livraison-gabon-/accueil",

      // --- AJOUTEZ VOS APPLICATIONS PARTENAIRES OU PUBLICITÉS ICI ---
      partnerApps: [
        {
          name: "Demande de livraison",
          desc: "Gérez vos rapports et fiches de suivi en direct.",
          logoUrl: "https://res.cloudinary.com/dyxob1wcj/image/upload/v1781134790/oeqlbzjhuvhbpmrzdpgh.jpg",
          link: "https://newsmiley21-star.github.io/1.2.html/" // Exemple identique
        },
        {
          name: "suivre un colis",
          desc: "Visualisez les métriques et KPIs de performance.",
          logoUrl: "https://i.ibb.co/68gZbyz/whatsapp-logo-placeholder.png",
          link: "https://newsmiley21-star.github.io/consultation.html/" // Remplacez par le vrai lien vers votre autre site HTML ou pub
        }
      ],

      apiKey: "VOTRE_CLE_API_PROD_ICI"
    };
    // =========================================================================


    document.addEventListener("DOMContentLoaded", () => {
      // 1. Initialiser les images et les variables
      document.getElementById('splash-logo').src = APPS_PRODUCTION_CONFIG.logoUrl;
      document.getElementById('guide-logo').src = APPS_PRODUCTION_CONFIG.logoUrl;
      
      // Injecter l'URL du Google Site dans notre Iframe de production
      document.getElementById('target-app-frame').src = APPS_PRODUCTION_CONFIG.targetAppUrl;

      // 2. Générer les étoiles/particules scintillantes en fond
      createStarsBackground();

      // 3. Générer la liste des applications/publicités
      renderPartnerApps();

      // 4. Lancer la barre de chargement ultra fluide
      runPremiumLoader();

      // 5. Détecter si l'application est ouverte hors-navigateur (Mode PWA installé)
      checkPwaStandalone();
    });

    // Générateur de particules
    function createStarsBackground() {
      const container = document.getElementById('particle-container');
      const particleCount = 20;

      for (let i = 0; i < particleCount; i++) {
        const p = document.createElement('div');
        p.className = 'particle';
        p.style.left = `${Math.random() * 100}vw`;
        p.style.width = `${Math.random() * 4 + 2}px`;
        p.style.height = p.style.width;
        p.style.animationDelay = `${Math.random() * 8}s`;
        p.style.animationDuration = `${Math.random() * 6 + 6}s`;
        container.appendChild(p);
      }
    }

    // Générer dynamiquement la liste d'applications complémentaires
    function renderPartnerApps() {
      const partnerList = document.getElementById('partner-list');
      const drawerList = document.getElementById('drawer-apps-list');
      
      partnerList.innerHTML = '';
      drawerList.innerHTML = '';

      APPS_PRODUCTION_CONFIG.partnerApps.forEach(app => {
        // Rendu pour l'écran de chargement
        const partnerItem = document.createElement('a');
        partnerItem.href = app.link;
        partnerItem.target = "_blank";
        partnerItem.className = "flex items-center space-x-3 bg-white/5 hover:bg-white/10 border border-white/5 hover:border-yellow-500/20 p-2.5 rounded-xl transition-all";
        partnerItem.innerHTML = `
          <img src="${app.logoUrl}" alt="Logo ${app.name}" class="w-9 h-9 rounded-lg object-cover">
          <div class="text-left flex-1 min-w-0">
            <h4 class="text-xs font-bold text-white truncate">${app.name}</h4>
            <p class="text-[9px] text-slate-400 truncate">${app.desc}</p>
          </div>
          <svg class="w-4 h-4 text-yellow-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3"></path>
          </svg>
        `;
        partnerList.appendChild(partnerItem);

        // Rendu pour le tiroir d'applications d'accès rapide
        const drawerItem = document.createElement('button');
        drawerItem.onclick = () => {
          switchApplication(app.link);
          toggleAppsDrawer(false);
        };
        drawerItem.className = "w-full flex items-center space-x-3 bg-slate-800 hover:bg-slate-700/80 border border-white/5 p-3 rounded-xl transition-all text-left";
        drawerItem.innerHTML = `
          <img src="${app.logoUrl}" alt="Logo ${app.name}" class="w-10 h-10 rounded-lg object-cover">
          <div class="flex-1 min-w-0">
            <h4 class="text-sm font-bold text-white">${app.name}</h4>
            <p class="text-[10px] text-slate-400">${app.desc}</p>
          </div>
          <svg class="w-5 h-5 text-yellow-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"></path>
          </svg>
        `;
        drawerList.appendChild(drawerItem);
      });
    }

    // Gestionnaire de chargement
    function runPremiumLoader() {
      const progressFill = document.getElementById('progress-indicator');
      const progressText = document.getElementById('progress-text');
      const splashStatus = document.getElementById('splash-status');
      const splashTitle = document.getElementById('splash-title');

      const messagesEtapes = {
        10: "Vérification des accès de sécurité...",
        35: "Négociation du tunnel SSL...",
        60: "Synchronisation avec Google Cloud...",
        80: "Activation de l'interface plein écran...",
        98: "Connexion sécurisée établie !"
      };

      let percent = 0;

      const loaderInterval = setInterval(() => {
        const increment = Math.floor(Math.random() * 7) + 2;
        percent = Math.min(percent + increment, 100);

        progressFill.style.width = `${percent}%`;
        progressText.textContent = `${percent}%`;

        // Changement de message dynamique
        for (let step in messagesEtapes) {
          if (percent >= parseInt(step)) {
            splashStatus.textContent = messagesEtapes[step];
          }
        }

        if (percent >= 100) {
          clearInterval(loaderInterval);
          splashTitle.innerHTML = "ACCÈS AUTORISÉ <span class='text-yellow-400'>✓</span>";
          
          // Lancer l'ouverture applicative
          setTimeout(launchMainApplication, 800);
        }
      }, 75);
    }

    // Transition animée vers l'iframe Google Sites
    function launchMainApplication() {
      const splash = document.getElementById('splash-screen');
      const frameContainer = document.getElementById('main-frame-container');
      const dockLauncher = document.getElementById('dock-launcher');

      // Rendre l'iframe et le bouton raccourci visibles
      frameContainer.style.display = "block";
      dockLauncher.classList.remove('hidden');

      // Effet de transition d'opacité
      splash.style.opacity = '0';
      splash.style.transform = 'scale(1.1)';

      setTimeout(() => {
        splash.style.display = 'none';
        
        // Transition douce pour révéler le site en plein écran
        frameContainer.style.opacity = '1';
        frameContainer.style.transform = 'scale(1)';
      }, 800);
    }

    // Permet de changer à la volée le Google Site affiché dans l'iframe
    function switchApplication(url) {
      document.getElementById('target-app-frame').src = url;
    }

    // Afficher ou masquer le tiroir d'applications
    function toggleAppsDrawer(isOpen) {
      const drawer = document.getElementById('apps-drawer');
      if (isOpen) {
        drawer.classList.add('open');
      } else {
        drawer.classList.remove('open');
      }
    }

    // Détection PWA pour guider l'utilisateur
    function checkPwaStandalone() {
      const isStandalone = window.navigator.standalone || window.matchMedia('(display-mode: standalone)').matches;
      
      if (!isStandalone) {
        // Si l'utilisateur est sur un navigateur Web classique, on affiche l'aide à l'installation après 5s
        setTimeout(() => {
          const instructionsText = document.getElementById('install-instructions');
          const isIOS = /iPad|iPhone|iPod/.test(navigator.userAgent) && !window.MSStream;

          if (isIOS) {
            instructionsText.innerHTML = "Cliquez sur <strong class='text-yellow-400'>Partager</strong> puis <strong class='text-yellow-400'>Sur l'écran d'accueil</strong> pour l'utiliser en plein écran.";
          } else {
            instructionsText.innerHTML = "Cliquez sur les <strong class='text-yellow-400'>3 points verticaux</strong> puis sur <strong class='text-yellow-400'>Installer l'application</strong>.";
          }
          
          document.getElementById('install-guide').classList.add('show');
        }, 5000);
      }
    }

    function hideInstallGuide() {
      document.getElementById('install-guide').classList.remove('show');
    }

    // --- ENREGISTREMENT DU SERVICE WORKER (Indispensable pour l'installation) ---
    if ('serviceWorker' in navigator) {
      window.addEventListener('load', () => {
        navigator.serviceWorker.register('/sw.js')
          .then(() => console.log('Service Worker de Production Opérationnel.'))
          .catch((err) => console.error('Erreur d\'initialisation du Service Worker :', err));
      });
    }
  </script>
</body>
</html>
