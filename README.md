<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
  <title>Portail Workspace Privé</title>
  
  <!-- Configuration de l'installation PWA -->
  <link rel="manifest" href="manifest.json">
  <meta name="theme-color" content="#030712">
  <meta name="apple-mobile-web-app-capable" content="yes">
  <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">

  <!-- Tailwind CSS pour un rendu haut de gamme -->
  <script src="https://cdn.tailwindcss.com"></script>

  <style>
    body {
      background-color: #030712; /* Bleu nuit profond */
      overflow-x: hidden;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
    }

    /* Écran de démarrage style Gemini / Pixel 9 Pro XL */
    #splash-screen {
      position: fixed;
      inset: 0;
      background: radial-gradient(circle at center, #0b1528 0%, #030712 100%);
      z-index: 100;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: space-between;
      padding: 50px 20px;
      transition: opacity 0.8s cubic-bezier(0.16, 1, 0.3, 1), transform 0.8s cubic-bezier(0.16, 1, 0.3, 1);
    }

    /* Halo Lumineux Google AI */
    .ai-glow-container {
      position: relative;
      width: 180px;
      height: 180px;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .ai-glow-outer {
      position: absolute;
      width: 140px;
      height: 140px;
      border-radius: 50%;
      background: linear-gradient(135deg, #1d4ed8 0%, #facc15 50%, #ffffff 100%);
      filter: blur(35px);
      opacity: 0.8;
      animation: morphingGlow 6s infinite alternate, rotateGlow 10s linear infinite;
    }

    .ai-glow-core {
      position: absolute;
      width: 80px;
      height: 80px;
      border-radius: 50%;
      background: radial-gradient(circle, #ffffff 0%, rgba(250, 204, 21, 0.6) 40%, rgba(29, 78, 216, 0) 70%);
      filter: blur(10px);
      animation: pulseCore 2.5s infinite ease-in-out;
      z-index: 2;
    }

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
      50% { transform: scale(1.15); opacity: 1; filter: blur(12px); }
    }

    /* Barre de progression haut de gamme */
    .progress-bar-container {
      width: 160px;
      height: 3px;
      background: rgba(255, 255, 255, 0.08);
      border-radius: 10px;
      overflow: hidden;
      margin-top: 20px;
    }

    .progress-bar-fill {
      height: 100%;
      width: 0%;
      background: linear-gradient(90deg, #1d4ed8, #facc15, #ffffff);
      transition: width 0.1s linear;
    }

    /* Conteneur principal de l'application */
    #main-app-container {
      opacity: 0;
      transform: translateY(20px);
      transition: opacity 1s cubic-bezier(0.16, 1, 0.3, 1), transform 1s cubic-bezier(0.16, 1, 0.3, 1);
    }

    .glass-card {
      background: rgba(15, 23, 42, 0.6);
      backdrop-filter: blur(25px);
      border: 1px solid rgba(255, 255, 255, 0.08);
    }

    /* Bouton brillant principal */
    .btn-glow-primary {
      position: relative;
      background: linear-gradient(135deg, #1d4ed8 0%, #1e40af 100%);
      overflow: hidden;
      border: 1px solid rgba(250, 204, 21, 0.3);
    }
    .btn-glow-primary::after {
      content: '';
      position: absolute;
      top: -50%;
      left: -60%;
      width: 30%;
      height: 200%;
      background: rgba(255, 255, 255, 0.25);
      transform: rotate(30deg);
      animation: sheen 4s infinite ease-in-out;
    }
    @keyframes sheen {
      0% { left: -60%; }
      30% { left: 140%; }
      100% { left: 140%; }
    }

    /* Éléments de particules d'arrière-plan */
    .particle {
      position: absolute;
      background-color: rgba(250, 204, 21, 0.3);
      border-radius: 50%;
      pointer-events: none;
      animation: floatUp 8s infinite linear;
    }
    @keyframes floatUp {
      0% { transform: translateY(100vh) scale(0); opacity: 0; }
      50% { opacity: 0.6; }
      100% { transform: translateY(-10vh) scale(1); opacity: 0; }
    }

    /* Bannière d'aide à l'installation style PWA WhatsApp */
    #install-guide {
      position: fixed;
      bottom: 16px;
      left: 50%;
      transform: translateX(-50%) translateY(120px);
      width: 92%;
      max-width: 400px;
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
  </style>
</head>
<body class="text-slate-100 min-h-screen flex flex-col justify-between">

  <!-- Particules d'ambiance en arrière-plan -->
  <div id="particle-container" class="absolute inset-0 overflow-hidden pointer-events-none z-0"></div>

  <!-- ======================================================== -->
  <!-- 1. ÉCRAN DE CHARGEMENT PREMIUM (JAUNE + BLEU + BLANC)  -->
  <!-- ======================================================== -->
  <div id="splash-screen">
    <div></div> <!-- Spacer -->

    <div class="flex flex-col items-center z-10 my-auto">
      <div class="ai-glow-container">
        <div class="ai-glow-outer"></div>
        <div class="ai-glow-core"></div>
        <img id="splash-logo" src="https://res.cloudinary.com/dyxob1wcj/image/upload/v1781134790/oeqlbzjhuvhbpmrzdpgh.jpg" alt="Logo" class="absolute w-16 h-16 rounded-2xl object-cover z-10 shadow-2xl border-2 border-white/20">
      </div>

      <h2 class="text-xl font-black tracking-widest text-white mt-8 uppercase flex items-center gap-2">
        <span>INITIALISATION</span>
        <span class="w-2 h-2 rounded-full bg-yellow-400 animate-ping"></span>
      </h2>
      <p id="splash-status" class="text-xs text-slate-300 mt-2 font-mono font-medium tracking-wide">Sécurisation de la passerelle...</p>

      <div class="progress-bar-container">
        <div class="progress-bar-fill" id="progress-indicator"></div>
      </div>
      <span id="progress-text" class="text-[11px] text-yellow-400 font-bold font-mono mt-2.5">0%</span>
    </div>

    <!-- Marque de bas de page temporaire -->
    <div class="text-[10px] text-slate-500 tracking-wider uppercase font-mono z-10">
      Powered by Google Workspace Sec
    </div>
  </div>


  <!-- ======================================================== -->
  <!-- 2. TABLEAU DE BORD PRINCIPAL (PORTAIL DE PRODUCTION)     -->
  <!-- ======================================================== -->
  <main id="main-app-container" class="w-full max-w-md mx-auto px-4 py-6 z-10 hidden my-auto">
    <div class="glass-card rounded-[2.5rem] p-6 shadow-2xl relative overflow-hidden">
      <!-- Halos lumineux légers de fond -->
      <div class="absolute -top-24 -left-24 w-48 h-48 rounded-full bg-blue-600/10 blur-3xl pointer-events-none"></div>
      <div class="absolute -bottom-24 -right-24 w-48 h-48 rounded-full bg-yellow-500/10 blur-3xl pointer-events-none"></div>

      <!-- En-tête de l'application -->
      <div class="flex items-center space-x-4 mb-6 relative z-10">
        <img id="app-logo" src="https://res.cloudinary.com/dyxob1wcj/image/upload/v1781134790/oeqlbzjhuvhbpmrzdpgh.jpg" alt="Logo principal" class="w-14 h-14 rounded-2xl object-cover border border-white/10 shadow-lg">
        <div>
          <h1 id="app-name" class="text-lg font-black text-white tracking-tight leading-none">Mon Portail Hub</h1>
          <span class="text-[11px] text-yellow-400 font-semibold tracking-wider uppercase font-mono mt-1 inline-block">Tableau de bord actif</span>
        </div>
      </div>

      <!-- CARTE D'ACTION PRINCIPALE (Redirection vers le Google Site) -->
      <div class="bg-gradient-to-br from-slate-900 to-slate-950 border border-yellow-400/20 rounded-3xl p-5 mb-5 relative z-10 shadow-inner">
        <div class="flex justify-between items-start mb-3">
          <span class="text-[10px] bg-yellow-400/10 text-yellow-400 border border-yellow-400/20 px-2.5 py-1 rounded-full font-bold uppercase tracking-wider">Espace Principal</span>
          <span class="text-[11px] text-slate-400 font-mono flex items-center gap-1">
            <span class="w-2 h-2 rounded-full bg-green-500"></span> En ligne
          </span>
        </div>
        <h3 class="text-md font-bold text-white mb-1.5">Mon Espace Cloud Google</h3>
        <p class="text-xs text-slate-400 mb-5 leading-relaxed">Accédez à votre espace complet de rapports, de formulaires et de statistiques d'administration.</p>
        
        <!-- Le gros bouton brillant d'ouverture vers votre Google Site -->
        <a href="https://sites.google.com/view/x-press-livraison-gabon-/accueil?authuser=0" target="_blank" class="btn-glow-primary w-full text-white font-bold py-4 px-6 rounded-2xl transition-all shadow-lg flex items-center justify-between group">
          <span class="text-sm font-extrabold tracking-wide">ACCÉDER À L'APPLICATION</span>
          <div class="flex items-center space-x-1.5">
            <span class="text-xs text-yellow-400 group-hover:underline">Ouvrir</span>
            <svg class="w-4 h-4 text-yellow-400 transform group-hover:translate-x-1 transition-transform" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.5" d="M14 5l7 7m0 0l-7 7m7-7H3"></path>
            </svg>
          </div>
        </a>
      </div>

      <!-- BLOC NOTES DE PRODUCTION (Fonctionnalité native pour votre utilisation de demain matin) -->
      <div class="bg-slate-900/40 border border-white/5 rounded-3xl p-5 mb-5 relative z-10">
        <div class="flex items-center justify-between mb-3">
          <h4 class="text-xs font-bold text-slate-200 uppercase tracking-wider flex items-center gap-1.5">
            <svg class="w-4 h-4 text-yellow-400" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z"></path></svg>
            Mémo rapide de suivi
          </h4>
          <span class="text-[9px] text-slate-500 uppercase font-mono">Sauvegarde locale</span>
        </div>
        <textarea id="app-notepad" placeholder="Écrivez vos notes de suivi temporaires ici..." class="w-full h-20 bg-slate-950/60 border border-white/5 rounded-xl p-3 text-xs text-slate-300 focus:outline-none focus:border-yellow-500/30 resize-none font-sans"></textarea>
      </div>

      <!-- CAROUSEL D'AUTRES APPLICATIONS & LIENS COMPAGNON -->
      <div class="relative z-10">
        <div class="flex items-center justify-between mb-3 border-b border-white/5 pb-2">
          <span class="text-[10px] font-bold text-yellow-400 tracking-wider uppercase">Nos autres applications</span>
          <span class="text-[9px] bg-blue-600/20 text-blue-300 px-2.5 py-0.5 rounded-full font-bold">Services</span>
        </div>
        <div id="partner-list" class="space-y-2">
          <!-- Injecté par JS -->
        </div>
      </div>
    </div>
  </main>


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
    // 🛠️ CONFIGURATION UNIQUE : VOS LOGOS ET VOS PUBS DE DEMAIN MATIN
    // =========================================================================
    const APPS_PRODUCTION_CONFIG = {
      // Lien direct de votre image Logo générée sur ImgBB (ex: https://i.ibb.co/xxxx/monlogo.png)
      logoUrl: "https://res.cloudinary.com/dyxob1wcj/image/upload/v1781134790/oeqlbzjhuvhbpmrzdpgh.jpg",

      // Nom de votre application Hub
      appName: "Workspace Hub Admin",

      // --- AJOUTEZ VOS AUTRES APPLICATIONS / PUBLICITÉS ICI ---
      partnerApps: [
        {
          name: "Demande de livraison",
          desc: "Fiches de commande en temps réel.",
          logoUrl: "https://res.cloudinary.com/dyxob1wcj/image/upload/v1781134790/oeqlbzjhuvhbpmrzdpgh.jpg",
          link: "https://newsmiley21-star.github.io/1.2.html/"
        },
        {
          name: "Suivre un colis",
          desc: "Activité globale.",
          logoUrl: "https://res.cloudinary.com/dyxob1wcj/image/upload/v1781134790/oeqlbzjhuvhbpmrzdpgh.jpg",
          link: "https://newsmiley21-star.github.io/consultation.html/"
        }
      ]
    };
    // =========================================================================


    document.addEventListener("DOMContentLoaded", () => {
      // 1. Initialiser les images et les variables
      document.getElementById('splash-logo').src = APPS_PRODUCTION_CONFIG.logoUrl;
      document.getElementById('app-logo').src = APPS_PRODUCTION_CONFIG.logoUrl;
      document.getElementById('guide-logo').src = APPS_PRODUCTION_CONFIG.logoUrl;
      document.getElementById('app-name').textContent = APPS_PRODUCTION_CONFIG.appName;

      // 2. Restaurer les notes sauvegardées localement
      initNotepad();

      // 3. Générer les étoiles/particules scintillantes en fond
      createStarsBackground();

      // 4. Générer la liste des applications secondaires
      renderPartnerApps();

      // 5. Lancer la barre de chargement ultra fluide
      runPremiumLoader();

      // 6. Détecter si l'application est ouverte hors-navigateur (Mode PWA installé)
      checkPwaStandalone();
    });

    // Sauvegarde automatique du Notepad en local
    function initNotepad() {
      const notepad = document.getElementById('app-notepad');
      const savedNotes = localStorage.getItem('pwa_workspace_notes');
      
      if (savedNotes) {
        notepad.value = savedNotes;
      }

      notepad.addEventListener('input', (e) => {
        localStorage.setItem('pwa_workspace_notes', e.target.value);
      });
    }

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
      partnerList.innerHTML = '';

      APPS_PRODUCTION_CONFIG.partnerApps.forEach(app => {
        const partnerItem = document.createElement('a');
        partnerItem.href = app.link;
        partnerItem.target = "_blank";
        partnerItem.className = "flex items-center space-x-3 bg-white/5 hover:bg-white/10 border border-white/5 hover:border-yellow-500/20 p-2.5 rounded-2xl transition-all";
        partnerItem.innerHTML = `
          <img src="${app.logoUrl}" alt="Logo ${app.name}" class="w-9 h-9 rounded-xl object-cover">
          <div class="text-left flex-1 min-w-0">
            <h4 class="text-xs font-bold text-white truncate">${app.name}</h4>
            <p class="text-[9px] text-slate-400 truncate">${app.desc}</p>
          </div>
          <svg class="w-4 h-4 text-yellow-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3"></path>
          </svg>
        `;
        partnerList.appendChild(partnerItem);
      });
    }

    // Gestionnaire de chargement
    function runPremiumLoader() {
      const progressFill = document.getElementById('progress-indicator');
      const progressText = document.getElementById('progress-text');
      const splashStatus = document.getElementById('splash-status');

      const messagesEtapes = {
        10: "Analyse du profil...",
        40: "Établissement du canal sécurisé...",
        70: "Chargement du bureau d'accueil...",
        98: "Tableau de bord synchronisé !"
      };

      let percent = 0;

      const loaderInterval = setInterval(() => {
        const increment = Math.floor(Math.random() * 8) + 3;
        percent = Math.min(percent + increment, 100);

        progressFill.style.width = `${percent}%`;
        progressText.textContent = `${percent}%`;

        for (let step in messagesEtapes) {
          if (percent >= parseInt(step)) {
            splashStatus.textContent = messagesEtapes[step];
          }
        }

        if (percent >= 100) {
          clearInterval(loaderInterval);
          setTimeout(revealMainDashboard, 600);
        }
      }, 70);
    }

    // Révéler le tableau de bord avec une transition douce
    function revealMainDashboard() {
      const splash = document.getElementById('splash-screen');
      const mainApp = document.getElementById('main-app-container');

      mainApp.classList.remove('hidden');

      splash.style.opacity = '0';
      splash.style.transform = 'scale(1.08)';

      setTimeout(() => {
        splash.style.display = 'none';
        
        mainApp.style.opacity = '1';
        mainApp.style.transform = 'translateY(0)';
      }, 800);
    }

    // Détection PWA pour guider l'installation (Masquage URL)
    function checkPwaStandalone() {
      const isStandalone = window.navigator.standalone || window.matchMedia('(display-mode: standalone)').matches;
      
      if (!isStandalone) {
        setTimeout(() => {
          const instructionsText = document.getElementById('install-instructions');
          const isIOS = /iPad|iPhone|iPod/.test(navigator.userAgent) && !window.MSStream;

          if (isIOS) {
            instructionsText.innerHTML = "Cliquez sur <strong class='text-yellow-400'>Partager</strong> puis <strong class='text-yellow-400'>Sur l'écran d'accueil</strong> pour l'utiliser en plein écran.";
          } else {
            instructionsText.innerHTML = "Cliquez sur les <strong class='text-yellow-400'>3 points verticaux</strong> puis sur <strong class='text-yellow-400'>Installer l'application</strong>.";
          }
          
          document.getElementById('install-guide').classList.add('show');
        }, 3000);
      }
    }

    function hideInstallGuide() {
      document.getElementById('install-guide').classList.remove('show');
    }

    // --- ENREGISTREMENT DU SERVICE WORKER (Indispensable pour l'installation) ---
    if ('serviceWorker' in navigator) {
      window.addEventListener('load', () => {
        navigator.serviceWorker.register('/sw.js')
          .then(() => console.log('Service Worker de Production Activé.'))
          .catch((err) => console.error('Erreur Service Worker :', err));
      });
    }
  </script>
</body>
</html>
