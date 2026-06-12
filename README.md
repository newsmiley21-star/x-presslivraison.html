<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
  <title>X-PRESS LIVRAISON</title>
  
  <!-- Importation de la police Google Plus Jakarta Sans (Style Google Pixel) -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">

  <meta name="theme-color" content="#36a100">
  
  <!-- Compatibilité iOS / Apple pour l'icône de l'écran d'accueil -->
  <meta name="apple-mobile-web-app-capable" content="yes">
  <meta name="apple-mobile-web-app-status-bar-style" content="default">
  <meta name="apple-mobile-web-app-title" content="Workspace">
  <link id="apple-touch-icon" rel="apple-touch-icon" href="https://res.cloudinary.com/dyxob1wcj/image/upload/v1781134790/oeqlbzjhuvhbpmrzdpgh.jpg">

  <!-- Manifeste PWA généré à la volée via un Blob (Logique WhatsApp du Fichier 2) -->
  <script>
    const manifest = {
        "name": "X-PRESS LIVRAISON ",
        "short_name": "X-PRESS LIVRAISON Workspace",
        "description": "Portail des livraison ",
        "start_url": "./index.html",
        "display": "standalone",
        "background_color": "#f8fafc",
        "theme_color": "#36a100",
        "icons": [
            {
                "src": "https://res.cloudinary.com/dyxob1wcj/image/upload/v1781134790/oeqlbzjhuvhbpmrzdpgh.jpg",
                "sizes": "192x192",
                "type": "image/png",
                "purpose": "any maskable"
            },
            {
                "src": "https://res.cloudinary.com/dyxob1wcj/image/upload/v1781134790/oeqlbzjhuvhbpmrzdpgh.jpg",
                "sizes": "512x512",
                "type": "image/png",
                "purpose": "any"
            }
        ],
        "screenshots": [
            {
                "src": "https://res.cloudinary.com/dyxob1wcj/image/upload/v1781134790/oeqlbzjhuvhbpmrzdpgh.jpg",
                "sizes": "1024x1024",
                "type": "image/png",
                "form_factor": "wide",
                "label": "Dashboard X-PRESS Gabon"
            }
        ]
    };
    const stringManifest = JSON.stringify(manifest);
    const blob = new Blob([stringManifest], {type: 'application/json'});
    const manifestURL = URL.createObjectURL(blob);
    const link = document.createElement('link');
    link.rel = 'manifest';
    link.href = manifestURL;
    document.head.appendChild(link);
  </script>

  <!-- Tailwind CSS pour un rendu haut de gamme -->
  <script src="https://cdn.tailwindcss.com"></script>

  <script>
    tailwind.config = {
      theme: {
        extend: {
          fontFamily: {
            sans: ['"Plus Jakarta Sans"', 'sans-serif'],
          },
          colors: {
            gabon: {
              green: '#36a100', // Vert drapeau
              yellow: '#ffcf00', // Jaune drapeau
              blue: '#007fff',   // Bleu drapeau
            }
          }
        },
      },
    }
  </script>

  <!-- Styling CSS de la plateforme et des animations -->
  <style>
    body {
      background-color: #f8fafc; /* Blanc/gris doux haut de gamme */
      overflow-x: hidden;
      font-family: "Plus Jakarta Sans", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
    }

    /* Écran de démarrage style Gemini Google Pixel 9 Pro XL (Mode Clair) */
    #splash-screen {
      position: fixed;
      inset: 0;
      background: radial-gradient(circle at center, #ffffff 0%, #f1f5f9 100%);
      z-index: 100;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: space-between;
      padding: 60px 24px;
      transition: opacity 0.8s cubic-bezier(0.16, 1, 0.3, 1), transform 0.8s cubic-bezier(0.16, 1, 0.3, 1);
    }

    /* Halo Lumineux Google AI Multicolore */
    .ai-glow-container {
      position: relative;
      width: 190px;
      height: 190px;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .ai-glow-outer {
      position: absolute;
      width: 150px;
      height: 150px;
      border-radius: 50%;
      /* Dégradé officiel Google : Bleu, Rouge, Jaune, Vert */
      background: linear-gradient(135deg, #4285f4 0%, #ea4335 30%, #fbbc05 70%, #34a853 100%);
      filter: blur(32px);
      opacity: 0.55;
      animation: morphingGlow 6s infinite alternate, rotateGlow 10s linear infinite;
    }

    .ai-glow-core {
      position: absolute;
      width: 90px;
      height: 90px;
      border-radius: 50%;
      background: radial-gradient(circle, rgba(255,255,255,1) 0%, rgba(66, 133, 244, 0.15) 60%, rgba(255,255,255,0) 100%);
      filter: blur(8px);
      animation: pulseCore 2.5s infinite ease-in-out;
      z-index: 2;
    }

    @keyframes morphingGlow {
      0% { border-radius: 42% 58% 70% 30% / 45% 45% 55% 55%; transform: scale(0.9); }
      50% { border-radius: 70% 30% 52% 48% / 60% 40% 60% 40%; transform: scale(1.15); }
      100% { border-radius: 30% 70% 70% 30% / 50% 60% 40% 50%; transform: scale(0.95); }
    }

    @keyframes rotateGlow {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }

    @keyframes pulseCore {
      0%, 100% { transform: scale(0.92); opacity: 0.9; }
      50% { transform: scale(1.1); opacity: 1; filter: blur(10px); }
    }

    /* Barre de progression épurée Google Pixel */
    .progress-bar-container {
      width: 180px;
      height: 4px;
      background: rgba(0, 0, 0, 0.05);
      border-radius: 10px;
      overflow: hidden;
      margin-top: 24px;
    }

    .progress-bar-fill {
      height: 100%;
      width: 0%;
      background: linear-gradient(90deg, #4285f4, #ea4335, #fbbc05, #34a853);
      border-radius: 10px;
      transition: width 0.1s linear;
    }

    /* Conteneur principal */
    #main-app-container {
      opacity: 0;
      transform: translateY(24px);
      transition: opacity 1s cubic-bezier(0.16, 1, 0.3, 1), transform 1s cubic-bezier(0.16, 1, 0.3, 1);
    }

    /* Cartes en verre blanc flouté haut de gamme */
    .glass-card-light {
      background: rgba(255, 255, 255, 0.85);
      backdrop-filter: blur(20px);
      -webkit-backdrop-filter: blur(20px);
      border: 1px solid rgba(255, 255, 255, 0.6);
      box-shadow: 0 20px 40px -15px rgba(0, 0, 0, 0.06);
    }

    /* Animations tactiles et effets clic (RIPPLE EFFECT) */
    .ripple-btn {
      position: relative;
      overflow: hidden;
      transition: transform 0.2s cubic-bezier(0.175, 0.885, 0.32, 1.275), box-shadow 0.2s ease;
    }
    
    .ripple-btn:active {
      transform: scale(0.96); /* Enfoncement élastique haptique */
    }

    .ripple-element {
      position: absolute;
      border-radius: 50%;
      transform: scale(0);
      animation: rippleEffect 0.6s linear;
      background-color: rgba(66, 133, 244, 0.15);
      pointer-events: none;
    }

    @keyframes rippleEffect {
      to {
        transform: scale(4);
        opacity: 0;
      }
    }

    /* Particules d'arrière-plan */
    .particle {
      position: absolute;
      border-radius: 90%;
      pointer-events: none;
      animation: floatUp 12s infinite linear;
    }
    @keyframes floatUp {
      0% { transform: translateY(110vh) scale(0); opacity: 2; }
      10% { opacity: 0.5; }
      90% { opacity: 0.8; }
      100% { transform: translateY(-10vh) scale(1); opacity: 0; }
    }

    /* Bannière d'aide à l'installation style PWA WhatsApp */
    #install-guide {
      position: fixed;
      bottom: 24px;
      left: 50%;
      transform: translateX(-50%) translateY(160px);
      width: 92%;
      max-width: 420px;
      z-index: 150;
      background: rgba(255, 255, 255, 0.95);
      backdrop-filter: blur(24px);
      -webkit-backdrop-filter: blur(24px);
      border: 1px solid rgba(0, 0, 0, 0.06);
      border-radius: 28px;
      transition: transform 0.6s cubic-bezier(0.16, 1, 0.3, 1);
      box-shadow: 0 20px 45px rgba(0, 0, 0, 0.12);
    }
    #install-guide.show {
      transform: translateX(-50%) translateY(0);
    }

    .gabon-gradient {
      background: linear-gradient(135deg, #36a100 0%, #ffcf00 50%, #007fff 100%);
    }

    /* Toasts de notification modernes */
    #toast-container {
      position: fixed;
      top: 24px;
      left: 50%;
      transform: translateX(-50%);
      z-index: 200;
      width: 90%;
      max-width: 380px;
      pointer-events: none;
    }

    .toast-anim {
      animation: slideDownIn 0.4s cubic-bezier(0.16, 1, 0.3, 1) forwards, slideUpOut 0.4s cubic-bezier(0.16, 1, 0.3, 1) 3s forwards;
    }

    @keyframes slideDownIn {
      0% { transform: translateY(-40px); opacity: 0; }
      100% { transform: translateY(0); opacity: 1; }
    }

    @keyframes slideUpOut {
      0% { transform: translateY(0); opacity: 1; }
      100% { transform: translateY(-40px); opacity: 0; }
    }
  </style>
</head>
<body class="text-slate-800 min-h-screen flex flex-col justify-between">

  <!-- Particules d'ambiance en arrière-plan (Aux couleurs Google) -->
  <div id="particle-container" class="absolute inset-0 overflow-hidden pointer-events-none z-0"></div>

  <!-- Conteneur des toasts de notification -->
  <div id="toast-container" class="flex flex-col gap-2"></div>

  <!-- ======================================================== -->
  <!-- 1. ÉCRAN DE CHARGEMENT GOOGLE CLAIR (Fichier 1 intact)    -->
  <!-- ======================================================== -->
  <div id="splash-screen">
    <div></div> <!-- Spacer -->

    <div class="flex flex-col items-center z-10 my-auto">
      <div class="ai-glow-container">
        <div class="ai-glow-outer"></div>
        <div class="ai-glow-core"></div>
        <img id="splash-logo" src="https://res.cloudinary.com/dyxob1wcj/image/upload/v1781134790/oeqlbzjhuvhbpmrzdpgh.jpg" alt="Logo" class="absolute w-28 h-20 rounded-[1.3rem] object-cover z-10 shadow-xl border-2 border-white">
      </div>

      <h2 class="text-lg font-extrabold tracking-widest text-slate-800 mt-8 uppercase flex items-center gap-2">
        <span class="tracking-[0.25em]">Chargement</span>
        <span class="flex space-x-1">
          <span class="w-1.5 h-1.5 rounded-full bg-[#4285f4] animate-bounce" style="animation-delay: 0.1s"></span>
          <span class="w-1.5 h-1.5 rounded-full bg-[#ea4335] animate-bounce" style="animation-delay: 0.2s"></span>
          <span class="w-1.5 h-1.5 rounded-full bg-[#fbbc05] animate-bounce" style="animation-delay: 0.3s"></span>
        </span>
      </h2>
      <p id="splash-status" class="text-xs text-slate-500 mt-2 font-medium tracking-wide">Sécurisation du tunnel de données...</p>

      <div class="progress-bar-container">
        <div class="progress-bar-fill" id="progress-indicator"></div>
      </div>
      <span id="progress-text" class="text-xs text-slate-800 font-bold font-mono mt-3">0%</span>
    </div>

    <!-- Pied de page chargement Google Security -->
    <div class="text-[10px] text-slate-400 tracking-wider uppercase font-semibold z-10 flex items-center gap-1">
      <svg class="w-3.5 h-3.5 text-[#34a853]" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M2.166 4.9L10 1.154l7.834 3.746A1 1 0 0118.5 5.793v5.187a9 9 0 01-4.947 8.06l-3.236 1.624a1 1 0 01-.834 0l-3.236-1.624a9 9 0 01-4.947-8.06V5.793a1 1 0 01.547-.893zm8.334 10.3l4-4a1 1 0 10-1.414-1.414L10 12.586l-1.586-1.586a1 1 0 00-1.414 1.414l2.5 2.5a1 1 0 001.414 0z" clip-rule="evenodd"></path></svg>
      <span>Google Cloud Secured</span>
    </div>
  </div>

  <!-- ======================================================== -->
  <!-- 2. TABLEAU DE BORD PRINCIPAL (PORTAIL DE PRODUCTION)     -->
  <!-- ======================================================== -->
  <main id="main-app-container" class="w-full max-w-md mx-auto px-4 py-6 z-10 hidden my-auto">
    <div class="glass-card-light rounded-[2.5rem] p-6 shadow-2xl relative overflow-hidden">
      <!-- Halos lumineux légers de fond aux couleurs Google -->
      <div class="absolute -top-24 -left-24 w-48 h-48 rounded-full bg-[#4285f4]/10 blur-3xl pointer-events-none"></div>
      <div class="absolute -bottom-24 -right-24 w-48 h-48 rounded-full bg-[#34a853]/10 blur-3xl pointer-events-none"></div>

      <!-- En-tête de l'application -->
      <div class="flex items-center space-x-4 mb-6 relative z-10">
        <img id="app-logo" src="https://res.cloudinary.com/dyxob1wcj/image/upload/v1781134790/oeqlbzjhuvhbpmrzdpgh.jpg" alt="Logo principal" class="w-16 h-16 rounded-2xl object-cover border border-white shadow-md">
        <div>
          <h1 id="app-name" class="text-xl font-extrabold text-slate-800 tracking-tight leading-none">X-press livraison</h1>
          <span class="text-[10px] bg-emerald-50 text-emerald-600 border border-emerald-100 px-2.5 py-1 rounded-full font-bold tracking-wider uppercase mt-1.5 inline-block">SALUT , déjà de retour ?</span>
        </div>
      </div>

      <!-- CARTE D'ACTION PRINCIPALE (Affiche le Workspace à l'intérieur de la PWA) -->
      <div class="bg-slate-50 border border-slate-100 rounded-3xl p-5 mb-5 relative z-10">
        <div class="flex justify-between items-start mb-3">
          <span class="text-[10px] bg-blue-50 text-[#4285f4] border border-blue-100 px-2.5 py-1 rounded-full font-bold uppercase tracking-wider">Espace Workspace</span>
          <span class="text-[11px] text-slate-500 font-semibold flex items-center gap-1.5">
            <span class="w-2.5 h-2.5 rounded-full bg-[#34a853] animate-pulse"></span> En ligne
          </span>
        </div>
        <h3 class="text-md font-bold text-slate-800 mb-1">Mon Espace Cloud</h3>
        <p class="text-xs text-slate-500 mb-5 leading-relaxed">Accédez à votre espace complet de livraisons, de formulaires et de statistiques d'administration.</p>
        
        <!-- Le gros bouton brillant d'ouverture vers votre Google Site avec effet Ripple -->
        <button onclick="openInAppViewer('https://newsmiley21-star.github.io/index.html/#suivi-des-gains', 'Espace Workspace')" class="ripple-btn w-full bg-[#4285f4] hover:bg-[#3367d6] text-white font-bold py-4 px-6 rounded-2xl shadow-lg shadow-green-500/15 flex items-center justify-between group">
          <span class="text-sm font-extrabold tracking-wide">COMMENCER</span>
          <div class="flex items-center space-x-1.5">
            <span class="text-xs text-white/95 group-hover:underline">Ouvrir</span>
            <svg class="w-4 h-4 text-white transform group-hover:translate-x-1 transition-transform" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.5" d="M14 5l7 7m0 0l-7 7m7-7H3"></path>
            </svg>
          </div>
        </button>
      </div>

      <!-- BLOC NOTES DE PRODUCTION (Notepad) -->
      <div class="bg-slate-50/50 border border-slate-100 rounded-3xl p-5 mb-5 relative z-10">
        <div class="flex items-center justify-between mb-3">
          <h4 class="text-xs font-bold text-slate-700 uppercase tracking-wider flex items-center gap-1.5">
            <svg class="w-4 h-4 text-[#fbbc05]" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z"></path></svg>
            Mémo rapide de suivi
          </h4>
          <span class="text-[9px] text-slate-400 uppercase font-bold tracking-widest">Sauvegarde automatique</span>
        </div>
        <textarea id="app-notepad" placeholder="Écrivez vos notes de suivi temporaires ici..." class="w-full h-20 bg-white border border-slate-200 rounded-xl p-3 text-xs text-slate-700 focus:outline-none focus:border-[#4285f4] focus:ring-1 focus:ring-[#4285f4] resize-none transition-all"></textarea>
      </div>

      <!-- AUTRES APPLICATIONS (Partenaires et publicités) -->
      <div class="relative z-10">
        <div class="flex items-center justify-between mb-3 border-b border-slate-100 pb-2">
          <span class="text-[12px] font-bold text-[#ea4335] tracking-wider uppercase">Nos autres applications</span>
          <span class="text-[10px] bg-red-50 text-[#ea4335] px-2.5 py-0.5 rounded-full font-bold">Services</span>
        </div>
        <div id="partner-list" class="space-y-2">
          <!-- Injecté par JS -->
        </div>
      </div>
    </div>
  </main>

  <!-- ======================================================== -->
  <!-- 3. VISIONNEUSE IN-APP INTÉGRÉE (Viewer sécurisé)         -->
  <!-- ======================================================== -->
  <div id="inapp-viewer" class="fixed inset-0 bg-white z-50 flex-col hidden">
    <!-- En-tête de la visionneuse avec boutons d'action native -->
    <div class="h-16 bg-white border-b border-slate-200 px-4 flex items-center justify-between shadow-sm">
      <div class="flex items-center space-x-3">
        <button onclick="closeInAppViewer()" class="p-2 hover:bg-slate-100 rounded-full active:scale-95 transition-all text-slate-600">
          <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.5" d="M15 19l-7-7 7-7"></path></svg>
        </button>
        <div>
          <h2 id="viewer-app-title" class="text-sm font-bold text-slate-800">Chargement...</h2>
          <p id="viewer-app-url" class="text-[10px] text-slate-400 truncate max-w-[180px]">Sécurisé</p>
        </div>
      </div>
      
      <!-- Boutons de contrôle de la page web -->
      <div class="flex items-center space-x-1.5">
        <button onclick="refreshInAppViewer()" class="p-2 hover:bg-slate-100 rounded-full active:scale-95 transition-all text-slate-600" title="Actualiser">
          <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 4v5h.582m15.356 2A8.001 8.001 0 1121.21 8H18"></path></svg>
        </button>
        <button onclick="openExternalBrowser()" class="p-2 hover:bg-slate-100 rounded-full active:scale-95 transition-all text-slate-600" title="Ouvrir dans le navigateur externe">
          <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14"></path></svg>
        </button>
      </div>
    </div>
    
    <!-- Iframe d'intégration sécurisée -->
    <iframe id="viewer-iframe" src="" class="w-full flex-1 border-none bg-slate-50"></iframe>
  </div>

  <!-- ======================================================================= -->
  <!-- 4. BANNIÈRE D'INSTALLATION WHATSAPP-LIKE (Bannière install intégrée)  -->
  <!-- ======================================================================= -->
  <div id="install-guide" class="p-5 flex items-center justify-between text-left">
    <div class="flex items-center space-x-3.5">
      <div class="p-1.5 bg-slate-100 rounded-2xl border border-slate-200">
        <img id="guide-logo" src="https://res.cloudinary.com/dyxob1wcj/image/upload/v1781134790/oeqlbzjhuvhbpmrzdpgh.jpg" alt="App Logo" class="w-10 h-10 rounded-xl object-contain">
      </div>
      <div>
        <h4 class="text-sm font-extrabold text-slate-800">Installer X-PRESS LIVRAISON</h4>
        <p class="text-[10px] text-slate-500 mt-0.5" id="install-instructions">L'app officielle de livraison du Gabon.</p>
      </div>
    </div>
    <button id="btn-install" onclick="executeInstallationPrompt()" class="ripple-btn gabon-gradient text-white text-xs font-black px-5 py-3 rounded-2xl transition-all shadow-md active:scale-95">
      INSTALLER
    </button>
  </div>

  <!-- Pied de page -->
  <footer class="text-center p-4 text-[10px] font-bold text-slate-400 tracking-wider uppercase z-10 pointer-events-none">
    &copy; 2026 Workspace — Tous droits réservés.
  </footer>

  <!-- ========================================== -->
  <!-- 5. LOGIQUE SCRIPT & CONFIGURATIONS         -->
  <!-- ========================================== -->
  <script>
    // Configuration dynamique des données du portail
    const APPS_PRODUCTION_CONFIG = {
      logoUrl: "https://res.cloudinary.com/dyxob1wcj/image/upload/v1781134790/oeqlbzjhuvhbpmrzdpgh.jpg",
      appName: "Workspace Delivery +241",

      partnerApps: [
        {
          name: "Site Web",
          desc: "",
          logoUrl: "https://res.cloudinary.com/dyxob1wcj/image/upload/v1781134790/oeqlbzjhuvhbpmrzdpgh.jpg",
          link: "https://sites.google.com/view/x-press-livraison-gabon-/accueil?read_current=1",
          accentColor: "#007fff" 
        },
        {
          name: "Demander une livraison",
          desc: "Expéditions à travers le Gabon.",
          logoUrl: "https://res.cloudinary.com/dyxob1wcj/image/upload/v1781134790/oeqlbzjhuvhbpmrzdpgh.jpg",
          link: "https://newsmiley21-star.github.io/commandes.html",
          accentColor: "#36a100" 
        },
        {
          name: "Suivre mon colis",
          desc: "Consultation et suivi en temps réel.",
          logoUrl: "https://res.cloudinary.com/dyxob1wcj/image/upload/v1781134790/oeqlbzjhuvhbpmrzdpgh.jpg",
          link: "https://newsmiley21-star.github.io/consultation.html/",
          accentColor: "#007fff" 
        }
      ]
    };

    let deferredPrompt; // Pour capturer l'événement natif d'installation PWA

    document.addEventListener("DOMContentLoaded", () => {
      // 1. Initialiser le visuel des éléments
      document.getElementById('splash-logo').src = APPS_PRODUCTION_CONFIG.logoUrl;
      document.getElementById('app-logo').src = APPS_PRODUCTION_CONFIG.logoUrl;
      document.getElementById('guide-logo').src = APPS_PRODUCTION_CONFIG.logoUrl;
      document.getElementById('app-name').textContent = APPS_PRODUCTION_CONFIG.appName;
      
      document.getElementById('apple-touch-icon').href = APPS_PRODUCTION_CONFIG.logoUrl;

      // 2. Lancer les modules de base
      initNotepad();
      createStarsBackground();
      renderPartnerApps();
      runPremiumLoader();
      checkPwaStandalone();
      initRippleEffects();
    });

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

    function createStarsBackground() {
      const container = document.getElementById('particle-container');
      const colors = ['#36a100', '#ffcf00', '#007fff'];
      const particleCount = 25;

      for (let i = 0; i < particleCount; i++) {
        const p = document.createElement('div');
        p.className = 'particle';
        p.style.left = `${Math.random() * 100}vw`;
        p.style.width = `${Math.random() * 5 + 3}px`;
        p.style.height = p.style.width;
        p.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
        p.style.animationDelay = `${Math.random() * 10}s`;
        p.style.animationDuration = `${Math.random() * 8 + 8}s`;
        container.appendChild(p);
      }
    }

    function renderPartnerApps() {
      const partnerList = document.getElementById('partner-list');
      partnerList.innerHTML = '';

      APPS_PRODUCTION_CONFIG.partnerApps.forEach(app => {
        const partnerItem = document.createElement('button');
        partnerItem.className = "ripple-btn w-full flex items-center space-x-3.5 bg-white hover:bg-slate-50 border border-slate-100 p-3 rounded-2xl transition-all shadow-sm text-left";
        partnerItem.onclick = () => openInAppViewer(app.link, app.name);
        partnerItem.innerHTML = `
          <img src="${app.logoUrl}" alt="Logo ${app.name}" class="w-10 h-10 rounded-xl object-contain border border-slate-100 bg-slate-50">
          <div class="flex-1 min-w-0">
            <h4 class="text-xs font-bold text-slate-800 truncate">${app.name}</h4>
            <p class="text-[10px] text-slate-400 truncate">${app.desc}</p>
          </div>
          <svg class="w-4 h-4" fill="none" stroke="${app.accentColor || '#36a100'}" stroke-width="2.5" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.5" d="M14 5l7 7m0 0l-7 7m7-7H3"></path>
          </svg>
        `;
        partnerList.appendChild(partnerItem);
      });
    }

    // Module de toasts de notifications (Remplacement de la fonction native d'alert)
    function showNotification(message, type = "info") {
      const container = document.getElementById('toast-container');
      const toast = document.createElement('div');
      
      let badgeColor = "bg-blue-500";
      if (type === "success") badgeColor = "bg-[#36a100]";
      if (type === "warning") badgeColor = "bg-[#ffcf00]";
      if (type === "error") badgeColor = "bg-[#cc0000]";

      toast.className = "toast-anim flex items-center space-x-3 bg-white p-4 rounded-2xl shadow-xl border border-slate-100 pointer-events-auto";
      toast.innerHTML = `
        <div class="w-2.5 h-2.5 rounded-full ${badgeColor}"></div>
        <p class="text-xs font-bold text-slate-700">${message}</p>
      `;

      container.appendChild(toast);
      setTimeout(() => {
        toast.remove();
      }, 3500);
    }

    let currentOpenUrl = "";

    function openInAppViewer(url, title) {
      currentOpenUrl = url;
      document.getElementById('viewer-app-title').textContent = title;
      document.getElementById('viewer-app-url').textContent = url;
      document.getElementById('viewer-iframe').src = url;

      const viewer = document.getElementById('inapp-viewer');
      viewer.classList.remove('hidden');
      viewer.classList.add('flex');
      
      showNotification(`Ouverture sécurisée de : ${title}`, "success");
    }

    function closeInAppViewer() {
      const viewer = document.getElementById('inapp-viewer');
      viewer.classList.add('hidden');
      viewer.classList.remove('flex');
      document.getElementById('viewer-iframe').src = "";
    }

    function refreshInAppViewer() {
      const iframe = document.getElementById('viewer-iframe');
      iframe.src = iframe.src;
      showNotification("Actualisation de la page...", "info");
    }

    function openExternalBrowser() {
      if (currentOpenUrl) {
        window.open(currentOpenUrl, '_blank');
        showNotification("Ouverture dans le navigateur", "info");
      }
    }

    function initRippleEffects() {
      document.body.addEventListener('click', function(e) {
        const target = e.target.closest('.ripple-btn');
        if (!target) return;

        const rect = target.getBoundingClientRect();
        const ripple = document.createElement('span');
        ripple.className = 'ripple-element';
        
        const size = Math.max(rect.width, rect.height);
        ripple.style.width = ripple.style.height = `${size}px`;
        
        const x = e.clientX - rect.left - size / 2;
        const y = e.clientY - rect.top - size / 2;
        
        ripple.style.left = `${x}px`;
        ripple.style.top = `${y}px`;
        
        target.appendChild(ripple);
        
        ripple.addEventListener('animationend', () => {
          ripple.remove();
        });
      });
    }

    function runPremiumLoader() {
      const progressFill = document.getElementById('progress-indicator');
      const progressText = document.getElementById('progress-text');
      const splashStatus = document.getElementById('splash-status');

      const messagesEtapes = {
        10: "Démarrage des protocoles Google Cloud...",
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

    // ==========================================
    // 📲 LOGIQUE DE DÉTECTION & INSTALLATION PWA
    // ==========================================
    window.addEventListener('beforeinstallprompt', (e) => {
        // Empêche l'affichage par défaut de l'invite d'installation Chrome/Android
        e.preventDefault();
        deferredPrompt = e;
        
        // Affiche la bannière d'installation stylisée
        document.getElementById('install-guide').classList.add('show');
    });

    async function executeInstallationPrompt() {
        if (deferredPrompt) {
            deferredPrompt.prompt();
            const { outcome } = await deferredPrompt.userChoice;
            if (outcome === 'accepted') {
                document.getElementById('install-guide').classList.remove('show');
            }
            deferredPrompt = null;
        } else {
            // Si pas d'événement prompt natif (iOS / Safari ou déjà installé)
            hideInstallGuide();
        }
    }

    function checkPwaStandalone() {
      const isStandalone = window.navigator.standalone || window.matchMedia('(display-mode: standalone)').matches;
      
      if (!isStandalone) {
        setTimeout(() => {
          const instructionsText = document.getElementById('install-instructions');
          const isIOS = /iPad|iPhone|iPod/.test(navigator.userAgent) && !window.MSStream;

          if (isIOS) {
            instructionsText.innerHTML = "Cliquez sur <strong class='text-[#007fff]'>Partager</strong> puis <strong class='text-[#36a100]'>Sur l'écran d'accueil</strong> pour l'utiliser en plein écran.";
            document.getElementById('install-guide').classList.add('show');
          } else {
            // Pour Android/Chrome, on attend l'event 'beforeinstallprompt'
            // Si l'event ne s'est pas encore déclenché après 3s, on affiche quand même de l'aide
            if (!deferredPrompt) {
               instructionsText.innerHTML = "Cliquez sur les <strong class='text-[#007fff]'>3 points</strong> puis sur <strong class='text-[#36a100]'>Ajouter à l'écran d'accueil</strong>.";
               document.getElementById('install-guide').classList.add('show');
            }
          }
        }, 4000);
      }
    }

    function hideInstallGuide() {
      document.getElementById('install-guide').classList.remove('show');
    }

    // =======================================================
    // ⚙️ INJECTION D'UN SERVICE WORKER SANS SCRIPT PHYSIQUE
    // =======================================================
    if ('serviceWorker' in navigator) {
        window.addEventListener('load', () => {
            const swCode = `
                const CACHE_NAME = 'ct241-pwa-cache-v1';
                self.addEventListener('install', (e) => {
                    self.skipWaiting();
                });
                self.addEventListener('activate', (e) => {
                    e.waitUntil(self.clients.claim());
                });
                self.addEventListener('fetch', (e) => {
                    // Stratégie d'interception réseau directe pour maintenir l'accès aux données Firebase en live
                    e.respondWith(fetch(e.request).catch(() => caches.match(e.request)));
                });
            `;
            const blob = new Blob([swCode], { type: 'text/javascript' });
            navigator.serviceWorker.register(URL.createObjectURL(blob))
              .then(() => console.log('Service Worker auto-généré activé !'))
              .catch((err) => console.error('Erreur Service Worker :', err));
        });
    }
  </script>
</body>
</html>
