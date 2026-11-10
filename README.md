# evropa_2_rock_radio_player_pwa_3D_music
<!DOCTYPE html>
<html lang="cs" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
    <title>Rádio Player – Evropa 2 & Rock Radio | Živé Vysílání</title>

    <!-- iOS Standalone PWA Meta Tags -->
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="apple-mobile-web-app-title" content="Rádio Player">
    <meta name="mobile-web-app-capable" content="yes">
    <meta name="theme-color" content="#0B0D14">
    <meta name="application-name" content="Rádio Player">

    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Font Awesome Pro Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts Inter & Orbitron -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&family=Orbitron:wght@500;700;900&display=swap" rel="stylesheet">
    
    <script>
        // Official SVG Logotypes Data URLs (Matching exact user uploaded design for Rock Radio & Evropa 2)
        const ROCK_RADIO_SVG = `data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1200 520" width="1200" height="520"><g transform="rotate(-2 600 260)"><polygon points="20,130 760,140 1180,0 900,510 120,490" fill="%231E1E1E"/><polygon points="25,135 755,145 1170,10 895,500 125,480" fill="%23121212"/><g><text x="75" y="325" font-family="'Impact', 'Arial Black', sans-serif" font-weight="900" font-size="210" fill="%23ED1C24" letter-spacing="-3">ROCK</text><text x="155" y="445" font-family="'Impact', 'Arial Black', sans-serif" font-weight="900" font-size="145" fill="%23FFFFFF" letter-spacing="1">RADIO</text></g><g transform="translate(680, 50)"><polygon points="175,0 230,150 390,155 260,250 310,400 175,300 40,400 90,250 -40,155 120,150" fill="%23121212" stroke="%23C59B27" stroke-width="16" stroke-linejoin="round"/><polygon points="175,40 215,150 335,155 235,228 275,340 175,260 75,340 115,228 15,155 135,150" fill="%23121212" stroke="%23D4A017" stroke-width="10" stroke-linejoin="round"/></g></g></svg>`;

        const E2_LOGO_URL = "https://upload.wikimedia.org/wikipedia/commons/5/50/Evropa_2_Logo.png";

        const E2_ICON_SVG = `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512">
            <rect width="512" height="512" rx="115" fill="#0b0d14"/>
            <circle cx="256" cy="256" r="200" fill="#141824" stroke="#E30613" stroke-width="10"/>
            <path d="M 120 340 L 390 340 L 160 375 Z" fill="#E30613"/>
            <text x="110" y="270" font-family="Arial, sans-serif" font-weight="900" font-style="italic" font-size="95" fill="#ffffff">RADIO</text>
            <text x="360" y="270" font-family="Arial, sans-serif" font-weight="900" font-style="italic" font-size="110" fill="#E30613">LIVE</text>
        </svg>`;
        const iconDataUrl = 'data:image/svg+xml;base64,' + btoa(E2_ICON_SVG);

        // Add Apple Touch Icon & Favicon links dynamically
        const appleIconLink = document.createElement('link');
        appleIconLink.rel = 'apple-touch-icon';
        appleIconLink.href = iconDataUrl;
        document.head.appendChild(appleIconLink);

        const faviconLink = document.createElement('link');
        faviconLink.rel = 'icon';
        faviconLink.type = 'image/svg+xml';
        faviconLink.href = iconDataUrl;
        document.head.appendChild(faviconLink);

        // Dynamic Web App Manifest Injection
        const manifestObj = {
            name: "Rádio Player – Evropa 2 & Rock Radio",
            short_name: "Rádio Live",
            description: "Přehrávač živého vysílání – Evropa 2 & Rock Radio",
            start_url: "./",
            display: "standalone",
            orientation: "portrait",
            background_color: "#0B0D14",
            theme_color: "#0B0D14",
            icons: [
                { src: iconDataUrl, sizes: "512x512", type: "image/svg+xml", purpose: "any maskable" }
            ]
        };
        const manifestBlob = new Blob([JSON.stringify(manifestObj)], { type: 'application/json' });
        const manifestLink = document.createElement('link');
        manifestLink.rel = 'manifest';
        manifestLink.href = URL.createObjectURL(manifestBlob);
        document.head.appendChild(manifestLink);

        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        brand: {
                            red: '#E30613',
                            blue: '#0040A8',
                            accentBlue: '#0066FF',
                            rockRed: '#E30613',
                            rockGold: '#D4A017',
                            dark: '#0B0D14',
                            card: '#141824'
                        }
                    },
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                        tech: ['Orbitron', 'sans-serif']
                    },
                    animation: {
                        'pulse-glow': 'pulseGlow 2s infinite alternate',
                        'float': 'float 6s ease-in-out infinite'
                    },
                    keyframes: {
                        pulseGlow: {
                            '0%': { boxShadow: '0 0 15px rgba(227, 6, 19, 0.4), 0 0 30px rgba(0, 102, 255, 0.3)' },
                            '100%': { boxShadow: '0 0 25px rgba(227, 6, 19, 0.8), 0 0 50px rgba(0, 102, 255, 0.5)' }
                        },
                        float: {
                            '0%, 100%': { transform: 'translateY(0px)' },
                            '50%': { transform: 'translateY(-8px)' }
                        }
                    }
                }
            }
        }
    </script>

    <style>
        /* iOS Safe Area Padding & Fit */
        body {
            padding-top: env(safe-area-inset-top);
            padding-bottom: env(safe-area-inset-bottom);
            padding-left: env(safe-area-inset-left);
            padding-right: env(safe-area-inset-right);
            -webkit-tap-highlight-color: transparent;
            -webkit-user-select: none;
            user-select: none;
        }

        /* Modern Scrollbar */
        ::-webkit-scrollbar {
            width: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #0B0D14;
        }
        ::-webkit-scrollbar-thumb {
            background: #2D3748;
            border-radius: 3px;
        }
        
        /* Glassmorphic card styling */
        .glass-panel {
            background: rgba(20, 24, 36, 0.75);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            border: 1px solid rgba(255, 255, 255, 0.08);
        }

        .glass-button {
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(8px);
            -webkit-backdrop-filter: blur(8px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .glass-button:hover, .glass-button:active {
            background: rgba(255, 255, 255, 0.14);
            border-color: rgba(255, 255, 255, 0.25);
            transform: translateY(-1px);
        }

        /* Ambient Glow Backgrounds */
        .ambient-glow {
            position: absolute;
            border-radius: 50%;
            filter: blur(110px);
            opacity: 0.35;
            pointer-events: none;
            z-index: 0;
            transition: all 0.7s ease;
        }

        /* Range Slider Styling */
        input[type="range"] {
            -webkit-appearance: none;
            appearance: none;
            background: transparent;
            cursor: pointer;
        }

        input[type="range"]::-webkit-slider-runnable-track {
            background: #2A2F45;
            height: 6px;
            border-radius: 9999px;
        }

        input[type="range"]::-webkit-slider-thumb {
            -webkit-appearance: none;
            appearance: none;
            height: 18px;
            width: 18px;
            background-color: var(--accent-color, #E30613);
            border-radius: 50%;
            margin-top: -6px;
            box-shadow: 0 0 10px rgba(227, 6, 19, 0.8);
            transition: transform 0.1s ease, background-color 0.3s ease;
        }
    
        /* Full-window fallback also works without the Fullscreen API (iOS). */
        #visualizerFullscreen[hidden] { display: none !important; }
        #visualizerFullscreen {
            position: fixed; inset: 0; z-index: 9999; background: #070910;
            width: 100%; height: 100%; height: 100dvh;
            isolation: isolate; overflow: hidden;
        }
        #visualizerFullscreen::backdrop { background: #070910; }
        #visualizerFullscreen canvas { position: absolute; inset: 0; width: 100%; height: 100%; }
        .fullscreen-controls {
            position: absolute; z-index: 2; top: 0; left: 0; right: 0;
            padding: max(16px, env(safe-area-inset-top)) max(16px, env(safe-area-inset-right)) 16px max(16px, env(safe-area-inset-left));
            display: flex; flex-wrap: wrap; align-items: center; justify-content: space-between; gap: 12px;
            background: linear-gradient(rgba(7,9,16,.92), transparent);
        }
        .fullscreen-controls button, .fullscreen-controls select {
            background: rgba(22,26,40,.9); color: white; border: 1px solid rgba(255,255,255,.25);
            border-radius: 12px; padding: 10px 14px; font-size: 13px; min-height: 44px;
        }
        .fullscreen-controls button:focus-visible, .fullscreen-controls select:focus-visible {
            outline: 2px solid #60a5fa; outline-offset: 3px;
        }
        .fullscreen-caption {
            position: absolute; bottom: max(18px, env(safe-area-inset-bottom));
            left: 20px; right: 20px; text-align: center; font-size: 11px; color: #aab1c2;
            pointer-events: none; text-shadow: 0 1px 4px black;
        }
    </style>
</head>
<body class="bg-brand-dark text-white font-sans min-h-screen flex flex-col justify-between overflow-x-hidden relative selection:bg-brand-red selection:text-white">

    <!-- Ambient Glow FX Background -->
    <div id="glowLeft" class="ambient-glow w-[450px] h-[450px] bg-brand-red top-[-120px] left-[-100px]"></div>
    <div id="glowRight" class="ambient-glow w-[550px] h-[550px] bg-brand-accentBlue bottom-[-150px] right-[-100px]"></div>

    <!-- AUDIO ELEMENT -->
    <audio id="audioStream" crossorigin="anonymous" preload="none">
        <source id="audioSource" src="https://ice.actve.net/fm-evropa2-aac" type="audio/aac">
        Váš prohlížeč nepodporuje tento typ audio přehrávače.
    </audio>

    <!-- HEADER -->
    <header class="relative z-10 w-full max-w-6xl mx-auto px-4 py-4 sm:py-6 flex items-center justify-between">
        <div class="flex items-center space-x-3">
            <!-- Dynamic Logo Header Image -->
            <div class="h-12 px-3 py-1.5 rounded-xl bg-white/95 backdrop-blur-md flex items-center justify-center shadow-lg shadow-black/40 border border-white/20 transition-all">
                <img id="headerStationLogo" 
                     src="https://upload.wikimedia.org/wikipedia/commons/5/50/Evropa_2_Logo.png" 
                     onerror="this.onerror=null; this.src='https://placehold.co/160x50/ffffff/0f4c81?text=EVROPA+2';" 
                     alt="Station Logo" 
                     class="h-full w-auto object-contain">
            </div>
            <div>
                <h1 class="font-tech font-bold text-base sm:text-xl tracking-wider uppercase text-white flex items-center gap-2">
                    Živé Vysílání <span class="text-[10px] px-2 py-0.5 rounded bg-brand-red/20 text-brand-red font-sans font-medium border border-brand-red/30" id="badgeTag">PWA HD</span>
                </h1>
                <p id="headerSubtag" class="text-xs text-gray-400 font-medium hidden sm:block">Maxxximum muziky</p>
            </div>
        </div>

        <!-- Header Controls & iOS PWA Status -->
        <div class="flex items-center gap-2 sm:gap-3">
            <!-- PWA Install Status Indicator / Guide Trigger -->
            <button id="pwaInstallBtn" class="hidden glass-button px-3 py-2 rounded-xl text-xs text-brand-red font-semibold flex items-center gap-2 border-brand-red/30">
                <i class="fa-solid fa-arrow-down-to-square"></i>
                <span class="hidden sm:inline">Přidat na plochu</span>
            </button>
            
            <div id="pwaStandaloneBadge" class="hidden glass-button px-3 py-2 rounded-xl text-xs text-emerald-400 font-semibold flex items-center gap-1.5 border-emerald-500/30">
                <i class="fa-solid fa-mobile-screen-button"></i>
                <span class="hidden sm:inline">Aplikace na ploše</span>
            </div>

            <button id="infoBtn" class="glass-button p-2.5 rounded-xl text-gray-300 hover:text-brand-accentBlue transition-colors" title="Informace o stanici">
                <i class="fa-solid fa-circle-info text-lg"></i>
            </button>
        </div>
    </header>

    <!-- MAIN PLAYER SECTION -->
    <main class="relative z-10 w-full max-w-4xl mx-auto px-4 py-2 sm:py-4 my-auto flex flex-col items-center space-y-4 sm:space-y-6">

        <!-- STATION SELECTION BAR -->
        <div class="w-full glass-panel rounded-2xl p-2 sm:p-3 shadow-xl flex items-center justify-center gap-2 sm:gap-4 border border-white/10">
            <!-- Evropa 2 Card -->
            <button id="selectEvropa2" class="station-tab flex-1 py-2.5 px-3 sm:px-5 rounded-xl border flex items-center justify-center gap-2.5 transition-all duration-300 bg-brand-red/20 border-brand-red text-white shadow-lg shadow-brand-red/20">
                <i class="fa-solid fa-radio text-brand-red"></i>
                <div class="text-left">
                    <div class="font-bold text-xs sm:text-sm">Evropa 2</div>
                    <div class="text-[10px] text-gray-400 hidden sm:block">Maxxximum muziky</div>
                </div>
            </button>

            <!-- Rock Radio Card -->
            <button id="selectRockRadio" class="station-tab flex-1 py-2.5 px-3 sm:px-5 rounded-xl border border-white/10 text-gray-400 hover:text-white flex items-center justify-center gap-2.5 transition-all duration-300 bg-black/30">
                <i class="fa-solid fa-star text-gray-400"></i>
                <div class="text-left">
                    <div class="font-bold text-xs sm:text-sm">Rock Radio</div>
                    <div class="text-[10px] text-gray-400 hidden sm:block">Rock je slušná muzika</div>
                </div>
            </button>
        </div>
        
        <!-- MAIN GLASS CARD -->
        <div class="w-full glass-panel rounded-3xl p-5 sm:p-10 shadow-2xl relative overflow-hidden flex flex-col items-center">
            
            <!-- Dynamic Background Canvas Visualizer Overlay -->
            <canvas id="canvasVisualizer" class="absolute inset-0 w-full h-full opacity-35 pointer-events-none"></canvas>

            <!-- Top Row: LIVE Badge & Stream Info -->
            <div class="w-full flex justify-between items-center z-10 mb-4 sm:mb-6">
                <!-- LIVE Badge -->
                <div id="liveBadge" class="flex items-center space-x-2 bg-gray-800/60 border border-gray-700/50 px-3.5 py-1.5 rounded-full backdrop-blur-md transition-all duration-300">
                    <span id="liveDot" class="w-2.5 h-2.5 rounded-full bg-gray-500 transition-colors duration-300"></span>
                    <span id="liveText" class="text-xs font-bold tracking-wider uppercase text-gray-400">Připraveno</span>
                </div>

                <!-- Quality Indicator -->
                <div class="text-xs text-gray-400 flex items-center gap-2 bg-black/40 px-3 py-1.5 rounded-full border border-white/5">
                    <i class="fa-solid fa-signal text-brand-accentBlue text-[10px]"></i>
                    <span id="bitrateLabel" class="font-mono">320 kbps AAC</span>
                </div>
            </div>

            <!-- ALBUM ART / OFFICIAL LOGO DISPLAY -->
            <div class="relative z-10 my-3 sm:my-6 group">
                <!-- Outer Glow Ring -->
                <div id="albumGlow" class="absolute -inset-2 bg-gradient-to-r from-brand-red via-brand-accentBlue to-brand-blue rounded-3xl blur-xl opacity-30 group-hover:opacity-75 transition duration-500"></div>
                
                <div id="logoCardBg" class="relative w-48 h-48 sm:w-64 sm:h-64 rounded-3xl bg-gradient-to-br from-white via-gray-100 to-gray-200 p-6 border border-white/40 shadow-2xl overflow-hidden flex flex-col items-center justify-center text-center transition-all duration-500">
                    
                    <!-- Dynamic Equalizer Bars Overlay -->
                    <div id="fakeEqBars" class="absolute inset-x-0 bottom-0 h-20 flex items-end justify-center gap-1.5 opacity-20 px-4 pointer-events-none">
                        <div class="w-2 bg-brand-red h-6 rounded-t"></div>
                        <div class="w-2 bg-brand-blue h-12 rounded-t"></div>
                        <div class="w-2 bg-brand-accentBlue h-16 rounded-t"></div>
                        <div class="w-2 bg-brand-red h-8 rounded-t"></div>
                        <div class="w-2 bg-brand-blue h-14 rounded-t"></div>
                        <div class="w-2 bg-brand-accentBlue h-7 rounded-t"></div>
                    </div>

                    <!-- Main Logo / Album Art Image -->
                    <img id="mainStationLogo" 
                         src="https://upload.wikimedia.org/wikipedia/commons/5/50/Evropa_2_Logo.png" 
                         onerror="this.onerror=null; this.src=currentStation.fallbackLogo;" 
                         alt="Station Emblem" 
                         class="w-full h-auto max-h-28 sm:max-h-36 object-contain filter drop-shadow-md z-10 transform group-hover:scale-105 transition duration-300">
                    
                    <div class="z-10 mt-2">
                        <p id="stationSlogan" class="text-[10px] text-gray-500 font-bold uppercase tracking-widest">MaXXXimum Muziky</p>
                    </div>
                </div>
            </div>

            <!-- SONG INFO / STREAM DESCRIPTION -->
            <div class="text-center z-10 my-2 max-w-md">
                <h3 id="streamTitle" class="text-lg sm:text-2xl font-bold tracking-tight text-white mb-1">Evropa 2 – Živé Vysílání</h3>
                <p id="streamSubtitle" class="text-xs sm:text-sm text-gray-400">Poslouchejte rádia v ČR online v iOS PWA</p>
            </div>

            <!-- CONTROLS CONTAINER -->
            <div class="w-full max-w-md z-10 mt-4 sm:mt-6 space-y-4 sm:space-y-6">

                <!-- MAIN PLAY / PAUSE BUTTON & SECONDARY CONTROLS -->
                <div class="flex items-center justify-center space-x-6 sm:space-x-8">
                    
                    <!-- Sleep Timer Trigger Button -->
                    <button id="sleepTimerBtn" class="glass-button w-12 h-12 rounded-2xl flex items-center justify-center text-gray-300 hover:text-brand-accentBlue relative" title="Časovač vypnutí">
                        <i class="fa-solid fa-moon text-lg"></i>
                        <span id="sleepTimerBadge" class="hidden absolute -top-1 -right-1 bg-brand-accentBlue text-white text-[9px] font-bold px-1.5 py-0.5 rounded-full"></span>
                    </button>

                    <!-- PLAY / PAUSE MAIN BUTTON -->
                    <button id="playBtn" class="w-20 h-20 rounded-full bg-gradient-to-r from-brand-red via-red-600 to-brand-accentBlue hover:from-red-600 hover:to-blue-700 text-white flex items-center justify-center text-3xl shadow-xl shadow-brand-red/40 transform hover:scale-105 active:scale-95 transition-all duration-200">
                        <i id="playIcon" class="fa-solid fa-play ml-1"></i>
                    </button>

                    <!-- Reload / Reconnect Button -->
                    <button id="reloadBtn" class="glass-button w-12 h-12 rounded-2xl flex items-center justify-center text-gray-300 hover:text-white" title="Obnovit načtení streamu">
                        <i class="fa-solid fa-rotate-right text-lg"></i>
                    </button>
                </div>

                <!-- VOLUME CONTROL BAR & PRESETS -->
                <div class="space-y-2 bg-black/20 p-3.5 sm:p-4 rounded-2xl border border-white/5">
                    <div class="flex items-center justify-between text-xs text-gray-400 mb-1">
                        <div class="flex items-center space-x-2">
                            <button id="muteBtn" class="hover:text-white transition-colors">
                                <i id="volumeIcon" class="fa-solid fa-volume-high text-brand-red text-base w-5"></i>
                            </button>
                            <span class="font-medium text-gray-300">Hlasitost</span>
                        </div>
                        <span id="volumeValue" class="font-mono text-gray-300 font-semibold">80%</span>
                    </div>

                    <!-- Volume Slider -->
                    <input id="volumeSlider" type="range" min="0" max="100" value="80" class="w-full accent-brand-red">

                    <!-- Volume Quick Presets -->
                    <div class="flex justify-between gap-2 pt-2">
                        <button class="vol-preset glass-button text-[11px] font-mono py-1 px-2 rounded-lg text-gray-400 hover:text-white flex-1" data-vol="25">25%</button>
                        <button class="vol-preset glass-button text-[11px] font-mono py-1 px-2 rounded-lg text-gray-400 hover:text-white flex-1" data-vol="50">50%</button>
                        <button class="vol-preset glass-button text-[11px] font-mono py-1 px-2 rounded-lg text-gray-400 hover:text-white flex-1" data-vol="75">75%</button>
                        <button class="vol-preset glass-button text-[11px] font-mono py-1 px-2 rounded-lg text-gray-400 hover:text-white flex-1" data-vol="100">100%</button>
                    </div>
                </div>

                <!-- Responsive 2D / 3D visualizer selector -->
                <div class="flex flex-col gap-3 text-xs text-gray-400 pt-2 border-t border-white/10">
                    <span class="flex items-center gap-1.5"><i class="fa-solid fa-sliders text-brand-blue"></i> Vizualizace:</span>
                    <div id="visualizerButtons" class="flex flex-wrap gap-1 bg-black/40 p-1 rounded-xl border border-white/5" role="group" aria-label="Režim vizualizace">
                        <button type="button" id="visBarsBtn" data-vis="bars" aria-pressed="true" class="px-3 py-1 rounded-lg text-[11px] font-medium bg-brand-blue text-white transition-all">Sloupce</button>
                        <button type="button" id="visWaveBtn" data-vis="wave" aria-pressed="false" class="px-3 py-1 rounded-lg text-[11px] font-medium text-gray-400 hover:text-white transition-all">Vlny</button>
                        <button type="button" id="visCircleBtn" data-vis="circle" aria-pressed="false" class="px-3 py-1 rounded-lg text-[11px] font-medium text-gray-400 hover:text-white transition-all">Kruh</button>
                        <button type="button" id="visSphereBtn" data-vis="sphere3d" aria-pressed="false" class="px-3 py-1 rounded-lg text-[11px] font-medium text-gray-400 hover:text-white transition-all">Koule 3D</button>
                        <button type="button" id="visTunnelBtn" data-vis="tunnel3d" aria-pressed="false" class="px-3 py-1 rounded-lg text-[11px] font-medium text-gray-400 hover:text-white transition-all">Tunel 3D</button>
                        <button type="button" id="visSpectrumBtn" data-vis="spectrum3d" aria-pressed="false" class="px-3 py-1 rounded-lg text-[11px] font-medium text-gray-400 hover:text-white transition-all">Spektrum 3D</button>
                        <button type="button" id="visGalaxyBtn" data-vis="galaxy3d" aria-pressed="false" class="px-3 py-1 rounded-lg text-[11px] font-medium text-gray-400 hover:text-white transition-all">Galaxie 3D</button>
                    </div>
                    <button type="button" id="fullscreenVisBtn" class="glass-button rounded-xl px-4 py-2 text-xs text-white self-start" aria-haspopup="dialog" aria-controls="visualizerFullscreen">
                        <i class="fa-solid fa-expand" aria-hidden="true"></i> 3D přes celou obrazovku
                    </button>
                    <span id="visualizerStatus" class="text-[10px] text-gray-500" role="status">Vizualizace se spustí při přehrávání.</span>
                </div>

            </div>

        </div>

    </main>

    <!-- FOOTER INFO WITH AUTHOR JAN ROJKO -->
    <footer class="relative z-10 w-full max-w-6xl mx-auto px-4 py-4 flex flex-col sm:flex-row items-center justify-between border-t border-white/5 text-xs text-gray-500 gap-2">
        <div class="flex flex-col sm:flex-row items-center gap-1 sm:gap-3">
            <span>&copy; Rádiový Přehrávač PWA</span>
            <span class="hidden sm:inline">•</span>
            <span>Autor: <strong class="text-white font-semibold">Jan Rojko</strong></span>
            <span class="hidden sm:inline">•</span>
            <span id="footerStreamUrl" class="text-gray-400">etický hacking — Jan Rojko</span>
        </div>
        <div class="flex items-center space-x-3">
            <span class="flex items-center gap-1.5"><span class="w-2 h-2 rounded-full bg-emerald-500"></span> Online</span>
            <span>•</span>
            <span>iOS Standalone Ready</span>
        </div>
    </footer>

    <!-- iOS PWA INSTALLATION INSTRUCTIONS MODAL -->
    <div id="iosInstallModal" class="fixed inset-0 bg-black/80 backdrop-blur-md z-50 flex items-center justify-center p-4 hidden opacity-0 transition-opacity duration-300">
        <div class="glass-panel w-full max-w-md rounded-3xl p-6 border border-white/10 space-y-5 text-center relative">
            <button id="closeIosModal" class="absolute top-4 right-4 text-gray-400 hover:text-white">
                <i class="fa-solid fa-xmark text-xl"></i>
            </button>

            <!-- Header Icon -->
            <div class="w-16 h-16 rounded-2xl bg-white p-2.5 mx-auto shadow-xl border border-white/20 flex items-center justify-center">
                <img id="modalStationLogo" src="https://upload.wikimedia.org/wikipedia/commons/5/50/Evropa_2_Logo.png" alt="Station Logo" class="w-full h-auto object-contain">
            </div>

            <div>
                <h3 class="font-bold text-xl text-white">Nainstalujte přehrávač na iPhone / iPad</h3>
                <p class="text-xs text-gray-400 mt-1">Spouštějte rádiový přehrávač přímo z Plochy jako samostatnou aplikaci bez lišt Safari.</p>
            </div>

            <!-- Steps List -->
            <div class="bg-black/30 p-4 rounded-2xl border border-white/5 text-left space-y-3.5 text-xs">
                <div class="flex items-start space-x-3">
                    <div class="w-6 h-6 rounded-full bg-brand-red text-white flex items-center justify-center font-bold text-xs shrink-0">1</div>
                    <p class="text-gray-200">Klepněte dole v Safari na tlačítko <strong class="text-white"><i class="fa-solid fa-share-from-square text-brand-blue text-sm"></i> Sdílet</strong> (ikona čtverce se šipkou).</p>
                </div>
                <div class="flex items-start space-x-3">
                    <div class="w-6 h-6 rounded-full bg-brand-red text-white flex items-center justify-center font-bold text-xs shrink-0">2</div>
                    <p class="text-gray-200">V nabídce posuňte dolů a vyberte <strong class="text-white"><i class="fa-regular fa-square-plus text-sm"></i> Přidat na plochu</strong> (Add to Home Screen).</p>
                </div>
                <div class="flex items-start space-x-3">
                    <div class="w-6 h-6 rounded-full bg-brand-red text-white flex items-center justify-center font-bold text-xs shrink-0">3</div>
                    <p class="text-gray-200">Potvrďte vpravo nahoře tlačítkem <strong class="text-emerald-400">Přidat</strong>. Na ploše se vytvoří ikona přehrávače!</p>
                </div>
            </div>

            <button id="closeIosModalBtn" class="w-full py-3 bg-brand-red hover:bg-red-600 text-white rounded-xl text-xs font-bold transition-colors">
                Rozumím
            </button>
        </div>
    </div>

    <!-- SLEEP TIMER MODAL -->
    <div id="sleepModal" class="fixed inset-0 bg-black/70 backdrop-blur-sm z-50 flex items-center justify-center hidden opacity-0 transition-opacity duration-300">
        <div class="glass-panel w-full max-w-sm rounded-2xl p-6 border border-white/10 space-y-4">
            <div class="flex justify-between items-center">
                <h3 class="font-bold text-lg text-white flex items-center gap-2">
                    <i class="fa-solid fa-moon text-brand-blue"></i> Časovač vypnutí
                </h3>
                <button id="closeSleepModal" class="text-gray-400 hover:text-white">
                    <i class="fa-solid fa-xmark text-lg"></i>
                </button>
            </div>
            <p class="text-xs text-gray-400">Vyberte za jak dlouho se má přehrávání rádia automaticky pozastavit:</p>
            <div class="grid grid-cols-2 gap-2">
                <button class="sleep-option glass-button py-2.5 rounded-xl text-sm text-gray-200 hover:border-brand-blue" data-minutes="15">15 minut</button>
                <button class="sleep-option glass-button py-2.5 rounded-xl text-sm text-gray-200 hover:border-brand-blue" data-minutes="30">30 minut</button>
                <button class="sleep-option glass-button py-2.5 rounded-xl text-sm text-gray-200 hover:border-brand-blue" data-minutes="45">45 minut</button>
                <button class="sleep-option glass-button py-2.5 rounded-xl text-sm text-gray-200 hover:border-brand-blue" data-minutes="60">60 minut</button>
            </div>
            <button id="cancelSleepTimer" class="w-full py-2 bg-red-500/20 text-red-400 hover:bg-red-500/30 rounded-xl text-xs font-semibold border border-red-500/30 transition-colors hidden">
                Zrušit aktivní časovač
            </button>
        </div>
    </div>

    <!-- STATION INFO MODAL -->
    <div id="infoModal" class="fixed inset-0 bg-black/70 backdrop-blur-sm z-50 flex items-center justify-center hidden opacity-0 transition-opacity duration-300">
        <div class="glass-panel w-full max-w-md rounded-2xl p-6 border border-white/10 space-y-4">
            <div class="flex justify-between items-center">
                <h3 class="font-bold text-lg text-white flex items-center gap-2">
                    <i class="fa-solid fa-circle-info text-brand-red"></i> O stanicích & PWA
                </h3>
                <button id="closeInfoModal" class="text-gray-400 hover:text-white">
                    <i class="fa-solid fa-xmark text-lg"></i>
                </button>
            </div>
            <div class="text-xs text-gray-300 space-y-3 leading-relaxed">
                <p><strong class="text-white">Přehrávač rádio stanic</strong> umožňuje živý poslech českých stanic **Evropa 2** a **Rock Radio**. Podporuje samostatný provoz v iOS PWA i rozšířené audio efekty.</p>
                <div class="bg-black/30 p-3 rounded-xl border border-white/5 space-y-1.5">
                    <div class="flex justify-between">
                        <span class="text-gray-400">Aktuální stanice:</span>
                        <span id="infoStationName" class="font-bold text-white">Evropa 2</span>
                    </div>
                    <div class="flex justify-between">
                        <span class="text-gray-400">Informace:</span>
                        <span id="infoStreamUrl" class="text-brand-blue text-right">etický hacking — Jan Rojko</span>
                    </div>
                    <div class="flex justify-between">
                        <span class="text-gray-400">Režim:</span>
                        <span class="text-gray-200">Progressive Web App (PWA)</span>
                    </div>
                    <div class="flex justify-between">
                        <span class="text-gray-400">Autor aplikace:</span>
                        <span class="text-emerald-400 font-semibold">Jan Rojko</span>
                    </div>
                </div>
            </div>
            <button id="closeInfoModalBtn" class="w-full py-2.5 bg-brand-red hover:bg-red-600 text-white rounded-xl text-xs font-bold transition-colors">
                Zavřít
            </button>
        </div>
    </div>

    <!-- TOAST MESSAGES -->
    <div id="toast" class="fixed bottom-6 right-6 z-50 glass-panel border border-white/10 px-4 py-3 rounded-xl text-xs text-white shadow-2xl flex items-center space-x-3 transform translate-y-20 opacity-0 transition-all duration-300 pointer-events-none">
        <i id="toastIcon" class="fa-solid fa-circle-check text-emerald-400 text-base"></i>
        <span id="toastMessage">Zpráva systému</span>
    </div>

    <!-- JAVASCRIPT LOGIC & PWA / SERVICE WORKER REGISTRATION -->
    <script>
        document.addEventListener('DOMContentLoaded', () => {
            // Stations Configuration
            const STATIONS = {
                evropa2: {
                    id: 'evropa2',
                    name: 'Evropa 2',
                    slogan: 'MaXXXimum Muziky',
                    subtitle: 'Poslouchejte rádia v ČR online v iOS PWA',
                    url: 'https://ice.actve.net/fm-evropa2-aac',
                    logo: E2_LOGO_URL,
                    fallbackLogo: 'https://placehold.co/220x100/ffffff/0f4c81?text=EVROPA+2',
                    cardBg: 'bg-gradient-to-br from-white via-gray-100 to-gray-200',
                    bitrate: '320 kbps AAC',
                    primaryColor: '#E30613',
                    secondaryColor: '#0040A8',
                    glowLeft: '#E30613',
                    glowRight: '#0066FF'
                },
                rockradio: {
                    id: 'rockradio',
                    name: 'Rock Radio',
                    slogan: 'Rock je slušná muzika!',
                    subtitle: 'Nejlepší nářez rockové muziky v kvalitě 320 kbps AAC',
                    url: 'https://25443.live.streamtheworld.com/ROCK_RADIOAAC.aac',
                    logo: ROCK_RADIO_SVG,
                    fallbackLogo: ROCK_RADIO_SVG,
                    cardBg: 'bg-gradient-to-br from-gray-900 via-neutral-900 to-black border-amber-500/30',
                    bitrate: '320 kbps AAC',
                    primaryColor: '#E30613',
                    secondaryColor: '#D4A017',
                    glowLeft: '#E30613',
                    glowRight: '#D4A017'
                }
            };

            let currentStation = STATIONS.evropa2;

            // Register Dynamic Inline Service Worker for PWA Offline Caching
            if ('serviceWorker' in navigator) {
                const swCode = `
                    const CACHE_NAME = 'radio-pwa-v4';
                    self.addEventListener('install', (e) => {
                        self.skipWaiting();
                    });
                    self.addEventListener('activate', (e) => {
                        e.waitUntil(clients.claim());
                    });
                    self.addEventListener('fetch', (e) => {
                        if (e.request.url.includes('ice.actve.net') || e.request.url.includes('radia.cz')) {
                            return;
                        }
                        e.respondWith(
                            fetch(e.request).catch(() => caches.match(e.request))
                        );
                    });
                `;
                const swBlob = new Blob([swCode], { type: 'application/javascript' });
                const swUrl = URL.createObjectURL(swBlob);

                navigator.serviceWorker.register(swUrl)
                    .then(() => console.log('PWA Service Worker zaregistrován'))
                    .catch(err => console.warn('Service Worker registrační chyba:', err));
            }

            // iOS Standalone Detection
            const isIosStandalone = window.navigator.standalone === true || window.matchMedia('(display-mode: standalone)').matches;
            const pwaInstallBtn = document.getElementById('pwaInstallBtn');
            const pwaStandaloneBadge = document.getElementById('pwaStandaloneBadge');
            const iosInstallModal = document.getElementById('iosInstallModal');
            const closeIosModal = document.getElementById('closeIosModal');
            const closeIosModalBtn = document.getElementById('closeIosModalBtn');

            if (isIosStandalone) {
                pwaStandaloneBadge.classList.remove('hidden');
            } else {
                pwaInstallBtn.classList.remove('hidden');
            }

            pwaInstallBtn.addEventListener('click', () => {
                iosInstallModal.classList.remove('hidden');
                setTimeout(() => iosInstallModal.classList.remove('opacity-0'), 10);
            });

            const hideIosModal = () => {
                iosInstallModal.classList.add('opacity-0');
                setTimeout(() => iosInstallModal.classList.add('hidden'), 300);
            };

            closeIosModal.addEventListener('click', hideIosModal);
            closeIosModalBtn.addEventListener('click', hideIosModal);

            // Audio Player Controls & Web Audio Visualizer
            const audio = document.getElementById('audioStream');
            const audioSource = document.getElementById('audioSource');
            const playBtn = document.getElementById('playBtn');
            const playIcon = document.getElementById('playIcon');
            const reloadBtn = document.getElementById('reloadBtn');
            const volumeSlider = document.getElementById('volumeSlider');
            const volumeValue = document.getElementById('volumeValue');
            const volumeIcon = document.getElementById('volumeIcon');
            const muteBtn = document.getElementById('muteBtn');
            const liveBadge = document.getElementById('liveBadge');
            const liveDot = document.getElementById('liveDot');
            const liveText = document.getElementById('liveText');
            const canvas = document.getElementById('canvasVisualizer');
            const ctx = canvas.getContext('2d');
            const albumGlow = document.getElementById('albumGlow');
            const logoCardBg = document.getElementById('logoCardBg');

            // Elements for station updates
            const headerStationLogo = document.getElementById('headerStationLogo');
            const mainStationLogo = document.getElementById('mainStationLogo');
            const modalStationLogo = document.getElementById('modalStationLogo');
            const headerSubtag = document.getElementById('headerSubtag');
            const stationSlogan = document.getElementById('stationSlogan');
            const streamTitle = document.getElementById('streamTitle');
            const streamSubtitle = document.getElementById('streamSubtitle');
            const bitrateLabel = document.getElementById('bitrateLabel');
            const footerStreamUrl = document.getElementById('footerStreamUrl');
            const selectEvropa2Btn = document.getElementById('selectEvropa2');
            const selectRockRadioBtn = document.getElementById('selectRockRadio');
            const glowLeft = document.getElementById('glowLeft');
            const glowRight = document.getElementById('glowRight');
            const infoStationName = document.getElementById('infoStationName');
            const infoStreamUrl = document.getElementById('infoStreamUrl');

            // Modals & Timers
            const sleepTimerBtn = document.getElementById('sleepTimerBtn');
            const sleepModal = document.getElementById('sleepModal');
            const closeSleepModal = document.getElementById('closeSleepModal');
            const sleepBadge = document.getElementById('sleepTimerBadge');
            const cancelSleepTimer = document.getElementById('cancelSleepTimer');

            const infoBtn = document.getElementById('infoBtn');
            const infoModal = document.getElementById('infoModal');
            const closeInfoModal = document.getElementById('closeInfoModal');
            const closeInfoModalBtn = document.getElementById('closeInfoModalBtn');

            const visBarsBtn = document.getElementById('visBarsBtn');
            const visWaveBtn = document.getElementById('visWaveBtn');
            const visCircleBtn = document.getElementById('visCircleBtn');

            let isPlaying = false;
            let lastVolume = 0.8;
            let sleepTimeout = null;
            let sleepInterval = null;
            let visualizerMode = 'bars';
            const visualizerButtons = Array.from(document.querySelectorAll('[data-vis]'));
            const visualizerStatus = document.getElementById('visualizerStatus');
            try {
                const savedMode = localStorage.getItem('radioVisualizerMode');
                if (visualizerButtons.some(btn => btn.dataset.vis === savedMode)) visualizerMode = savedMode;
            } catch (_) {}
            let sceneTime = 0;
            let lastFrameTime = 0;
            const reducedMotion = window.matchMedia('(prefers-reduced-motion: reduce)');
            let isCorsBlocked = false;

            let audioCtx = null;
            let analyser = null;
            let sourceNode = null;
            let dataArray = null;
            let rawFrequencyData = null;
            let waveformData = null;
            let analysisStartedAt = 0;
            const music = { bass: 0, mids: 0, highs: 0, rms: 0, pulse: 0, bassAverage: 0 };
            function resetMusicAnalysis() {
                Object.keys(music).forEach(key => music[key] = 0);
                if (dataArray) dataArray.fill(0);
                barDecayArray.fill(0);
                spectrumHistory.length = 0;
                historyTime = -1;
                analysisStartedAt = performance.now();
            }
            function bandLevel(fromHz, toHz) {
                const hzPerBin = audioCtx.sampleRate / analyser.fftSize;
                const lo = Math.max(1, Math.floor(fromHz / hzPerBin));
                const hi = Math.min(rawFrequencyData.length, Math.ceil(toHz / hzPerBin));
                let sum = 0;
                for (let i = lo; i < hi; i++) sum += rawFrequencyData[i] / 255;
                return sum / Math.max(1, hi - lo);
            }
            function sampleMusic(dt) {
                dataArray.fill(0);
                if (!analyser || isCorsBlocked || audioCtx.state !== 'running') {
                    music.bass = music.mids = music.highs = music.rms = music.pulse = 0;
                    return false;
                }
                analyser.getByteFrequencyData(rawFrequencyData);
                analyser.getFloatTimeDomainData(waveformData);
                let squares = 0;
                for (const sample of waveformData) squares += sample * sample;
                music.rms = Math.sqrt(squares / waveformData.length);
                // A silent signal is never replaced with invented spectrum values.
                const hasSignal = music.rms > 0.00001;
                const smooth = (previous, next) => previous + (next - previous) *
                    (1 - Math.exp(-dt / (next > previous ? 0.035 : 0.16)));
                const bass = hasSignal ? bandLevel(40, 250) : 0;
                music.bass = smooth(music.bass, bass);
                music.mids = smooth(music.mids, hasSignal ? bandLevel(250, 4000) : 0);
                music.highs = smooth(music.highs, hasSignal ? bandLevel(4000, 16000) : 0);
                music.bassAverage += (bass - music.bassAverage) * (1 - Math.exp(-dt / 0.65));
                // Bass transients, not a timer or synthetic beat generator.
                music.pulse = Math.max(music.pulse * Math.exp(-dt * 7),
                    Math.min(1, Math.max(0, bass - music.bassAverage) * 4));
                if (hasSignal) {
                    const maxHz = Math.min(18000, audioCtx.sampleRate / 2);
                    for (let i = 0; i < dataArray.length; i++) {
                        const hz = 35 * Math.pow(maxHz / 35, i / (dataArray.length - 1));
                        const bin = Math.min(rawFrequencyData.length - 1,
                            Math.round(hz * analyser.fftSize / audioCtx.sampleRate));
                        dataArray[i] = rawFrequencyData[bin];
                    }
                }
                return hasSignal;
            }
            let animationFrameId = null;

            // Smooth decay buffer for natural spectrum visualization
            let barDecayArray = new Float32Array(48);

            function resizeCanvas() {
                canvas.width = canvas.parentElement.clientWidth;
                canvas.height = canvas.parentElement.clientHeight;
            }
            window.addEventListener('resize', resizeCanvas);
            resizeCanvas();
            if (window.ResizeObserver) new ResizeObserver(resizeCanvas).observe(canvas.parentElement);

            function showToast(msg, iconClass = "fa-solid fa-circle-check text-emerald-400") {
                const toast = document.getElementById('toast');
                const toastMessage = document.getElementById('toastMessage');
                const toastIcon = document.getElementById('toastIcon');

                toastMessage.textContent = msg;
                toastIcon.className = iconClass;
                
                toast.classList.remove('translate-y-20', 'opacity-0');
                setTimeout(() => {
                    toast.classList.add('translate-y-20', 'opacity-0');
                }, 3000);
            }

            function switchStation(stationKey) {
                const targetStation = STATIONS[stationKey];
                if (!targetStation || currentStation.id === targetStation.id) return;

                const wasPlaying = isPlaying;
                if (isPlaying) {
                    audio.pause();
                }

                currentStation = targetStation;
                resetMusicAnalysis();

                // Update Audio Source
                audioSource.src = targetStation.url;
                audio.load();

                // Update Station Metadata Display
                mainStationLogo.src = targetStation.logo;
                mainStationLogo.onerror = () => mainStationLogo.src = targetStation.fallbackLogo;

                headerStationLogo.src = targetStation.logo;
                headerStationLogo.onerror = () => headerStationLogo.src = targetStation.fallbackLogo;

                modalStationLogo.src = targetStation.logo;
                modalStationLogo.onerror = () => modalStationLogo.src = targetStation.fallbackLogo;

                headerSubtag.textContent = targetStation.slogan;
                stationSlogan.textContent = targetStation.slogan;
                streamTitle.textContent = `${targetStation.name} – Živé Vysílání`;
                streamSubtitle.textContent = targetStation.subtitle;
                bitrateLabel.textContent = targetStation.bitrate;
                footerStreamUrl.textContent = 'etický hacking — Jan Rojko';
                infoStationName.textContent = targetStation.name;
                infoStreamUrl.textContent = 'etický hacking — Jan Rojko';

                // Card Background
                logoCardBg.className = `relative w-48 h-48 sm:w-64 sm:h-64 rounded-3xl p-6 border border-white/40 shadow-2xl overflow-hidden flex flex-col items-center justify-center text-center transition-all duration-500 ${targetStation.cardBg}`;

                // Update Ambient Glow Colors & Background Gradients
                glowLeft.style.backgroundColor = targetStation.glowLeft;
                glowRight.style.backgroundColor = targetStation.glowRight;

                albumGlow.style.background = `linear-gradient(to right, ${targetStation.primaryColor}, ${targetStation.secondaryColor})`;

                // Update Active Tab UI
                if (targetStation.id === 'evropa2') {
                    selectEvropa2Btn.className = "station-tab flex-1 py-2.5 px-3 sm:px-5 rounded-xl border flex items-center justify-center gap-2.5 transition-all duration-300 bg-brand-red/20 border-brand-red text-white shadow-lg shadow-brand-red/20";
                    selectEvropa2Btn.querySelector('i').className = "fa-solid fa-radio text-brand-red";

                    selectRockRadioBtn.className = "station-tab flex-1 py-2.5 px-3 sm:px-5 rounded-xl border border-white/10 text-gray-400 hover:text-white flex items-center justify-center gap-2.5 transition-all duration-300 bg-black/30";
                    selectRockRadioBtn.querySelector('i').className = "fa-solid fa-star text-gray-400";
                } else {
                    selectRockRadioBtn.className = "station-tab flex-1 py-2.5 px-3 sm:px-5 rounded-xl border flex items-center justify-center gap-2.5 transition-all duration-300 bg-brand-rockRed/20 border-brand-rockRed text-white shadow-lg shadow-brand-rockRed/20";
                    selectRockRadioBtn.querySelector('i').className = "fa-solid fa-star text-brand-rockGold";

                    selectEvropa2Btn.className = "station-tab flex-1 py-2.5 px-3 sm:px-5 rounded-xl border border-white/10 text-gray-400 hover:text-white flex items-center justify-center gap-2.5 transition-all duration-300 bg-black/30";
                    selectEvropa2Btn.querySelector('i').className = "fa-solid fa-radio text-gray-400";
                }

                document.documentElement.style.setProperty('--accent-color', targetStation.primaryColor);
                showToast(`Přepnuto na ${targetStation.name}`);

                if (wasPlaying) {
                    togglePlay();
                }
            }

            selectEvropa2Btn.addEventListener('click', () => switchStation('evropa2'));
            selectRockRadioBtn.addEventListener('click', () => switchStation('rockradio'));

            function initAudioContext() {
                if (!audioCtx) {
                    try {
                        const AudioContextClass = window.AudioContext || window.webkitAudioContext;
                        if (AudioContextClass) {
                            audioCtx = new AudioContextClass();
                            analyser = audioCtx.createAnalyser();
                            // Expanded FFT size for better resolution in low/mid frequencies
                            analyser.fftSize = 2048;
                            analyser.smoothingTimeConstant = 0.55;
                            analyser.minDecibels = -90;
                            analyser.maxDecibels = -15;
                            
                            sourceNode = audioCtx.createMediaElementSource(audio);
                            sourceNode.connect(analyser);
                            analyser.connect(audioCtx.destination);
                            
                            rawFrequencyData = new Uint8Array(analyser.frequencyBinCount);
                            waveformData = new Float32Array(analyser.fftSize);
                            dataArray = new Uint8Array(256);
                            analysisStartedAt = performance.now();
                        }
                    } catch (e) {
                        console.warn('Analýza zvuku není dostupná:', e);
                        isCorsBlocked = true;
                    }
                }
                
                if (audioCtx && audioCtx.state === 'suspended') {
                    audioCtx.resume().catch(error => {
                        console.warn('AudioContext resume failed:', error);
                        visualizerStatus.textContent = 'Analýza zvuku je pozastavená. Zkus znovu spustit přehrávání.';
                    });
                }
            }

            function togglePlay() {
                initAudioContext();

                if (audio.paused) {
                    audio.load();
                    const playPromise = audio.play();
                    if (playPromise !== undefined) {
                        playPromise.then(() => {
                            setPlayingState(true);
                            showToast(`Živé vysílání ${currentStation.name} spuštěno`);
                        }).catch(err => {
                            console.error("Chyba přehrávání:", err);
                            showToast("Chyba při spuštění přehrávání", "fa-solid fa-triangle-exclamation text-red-500");
                            setPlayingState(false);
                        });
                    }
                } else {
                    audio.pause();
                    setPlayingState(false);
                    showToast("Přehrávání pozastaveno");
                }
            }

            function setPlayingState(playing) {
                isPlaying = playing;
                if (playing) {
                    playIcon.className = "fa-solid fa-pause";
                    liveDot.className = "w-2.5 h-2.5 rounded-full bg-brand-red animate-pulse";
                    liveBadge.className = "flex items-center space-x-2 bg-brand-red/20 border border-brand-red/50 px-3.5 py-1.5 rounded-full backdrop-blur-md shadow-lg shadow-brand-red/20 animate-pulse-glow";
                    liveText.className = "text-xs font-bold tracking-wider uppercase text-brand-red";
                    liveText.textContent = "ŽIVĚ";
                    albumGlow.classList.remove('opacity-30');
                    albumGlow.classList.add('opacity-70');
                    analysisStartedAt = performance.now();
                    startVisualizer();
                } else {
                    if (animationFrameId) cancelAnimationFrame(animationFrameId);
                    animationFrameId = null;
                    ctx.clearRect(0, 0, canvas.width, canvas.height);
                    visualizerStatus.textContent = 'Vizualizace se spustí při přehrávání.';
                    playIcon.className = "fa-solid fa-play ml-1";
                    liveDot.className = "w-2.5 h-2.5 rounded-full bg-gray-500";
                    liveBadge.className = "flex items-center space-x-2 bg-gray-800/60 border border-gray-700/50 px-3.5 py-1.5 rounded-full backdrop-blur-md";
                    liveText.className = "text-xs font-bold tracking-wider uppercase text-gray-400";
                    liveText.textContent = "Pozastaveno";
                    albumGlow.classList.remove('opacity-70');
                    albumGlow.classList.add('opacity-30');
                }
            }

            function updateVolume(val) {
                const vol = val / 100;
                audio.volume = vol;
                volumeValue.textContent = `${Math.round(val)}%`;
                
                if (vol === 0) {
                    volumeIcon.className = "fa-solid fa-volume-xmark text-gray-500 text-base w-5";
                } else if (vol < 0.5) {
                    volumeIcon.className = "fa-solid fa-volume-low text-brand-red text-base w-5";
                } else {
                    volumeIcon.className = "fa-solid fa-volume-high text-brand-red text-base w-5";
                }
            }

            volumeSlider.addEventListener('input', (e) => updateVolume(e.target.value));

            document.querySelectorAll('.vol-preset').forEach(btn => {
                btn.addEventListener('click', () => {
                    const vol = btn.getAttribute('data-vol');
                    volumeSlider.value = vol;
                    updateVolume(vol);
                });
            });

            muteBtn.addEventListener('click', () => {
                if (audio.volume > 0) {
                    lastVolume = audio.volume;
                    audio.volume = 0;
                    volumeSlider.value = 0;
                    updateVolume(0);
                } else {
                    const restoreVol = lastVolume > 0 ? lastVolume : 0.8;
                    audio.volume = restoreVol;
                    volumeSlider.value = restoreVol * 100;
                    updateVolume(restoreVol * 100);
                }
            });

            reloadBtn.addEventListener('click', () => {
                const wasPlaying = !audio.paused;
                audio.load();
                if (wasPlaying) audio.play();
                showToast("Stream byl znovunačten");
            });

            function startVisualizer() {
                if (animationFrameId) cancelAnimationFrame(animationFrameId);
                lastFrameTime = 0;
                function render(now) {
                    if (!isPlaying || document.hidden) {
                        animationFrameId = null;
                        return;
                    }
                    animationFrameId = requestAnimationFrame(render);
                    // Limit drawing to about 30 fps on mobile, 15 with reduced motion.
                    const interval = reducedMotion.matches ? 66 : 32;
                    if (lastFrameTime && now - lastFrameTime < interval) return;
                    const dt = lastFrameTime ? Math.min((now - lastFrameTime) / 1000, 0.1) : 1 / 30;
                    lastFrameTime = now;
                    ctx.clearRect(0, 0, canvas.width, canvas.height);
                    if (!dataArray) dataArray = new Uint8Array(256);
                    const hasSignal = sampleMusic(dt);
                    // Motion slows to a stop without actual audio energy.
                    const motion = Math.min(1.8, music.rms * 6 + music.bass * 0.7 + music.pulse * 0.8);
                    sceneTime += dt * motion * (reducedMotion.matches ? 0.18 : 1);
                    const currentSpectrum = dataArray;
                    const spectrum = currentSpectrum;
                    let status;
                    if (!analyser || isCorsBlocked) {
                        status = 'Analýza zvuku není dostupná • žádný umělý rytmus se nepoužívá.';
                    } else if (audioCtx.state !== 'running') {
                        status = 'Analýza zvuku je pozastavená • zkus znovu spustit přehrávání.';
                    } else if (hasSignal) {
                        status = `${currentStation.name} • živá reakce na basy, středy a výšky`;
                    } else if (now - analysisStartedAt < 5000) {
                        status = `${currentStation.name} • čekám na zvukový signál…`;
                    } else {
                        status = 'Není dostupný zvuk pro analýzu: ticho, načítání nebo omezení CORS. Umělý rytmus je vypnutý.';
                    }
                    if (visualizerStatus.textContent !== status) visualizerStatus.textContent = status;
                    if (visualizerMode === 'bars') drawBars(spectrum);
                    else if (visualizerMode === 'wave') drawWave(spectrum);
                    else if (visualizerMode === 'circle') drawCircle(spectrum);
                    else if (visualizerMode === 'sphere3d') drawSphere3D(spectrum);
                    else if (visualizerMode === 'tunnel3d') drawTunnel3D(spectrum);
                    else if (visualizerMode === 'spectrum3d') drawSpectrum3D(spectrum);
                    else if (visualizerMode === 'galaxy3d') drawGalaxy3D(spectrum);
                }
                animationFrameId = requestAnimationFrame(render);
            }
            document.addEventListener('visibilitychange', () => {
                if (document.hidden) {
                    if (animationFrameId) cancelAnimationFrame(animationFrameId);
                    animationFrameId = null;
                } else if (isPlaying) startVisualizer();
            });

            // Logarithmic/Audible Spectrum Bar Visualizer Algorithm
            function drawBars(data) {
                const barCount = 48; // Number of responsive frequency bars
                const gap = 3;
                const totalGaps = (barCount - 1) * gap;
                const barWidth = (canvas.width - totalGaps) / barCount;

                // Sample frequency bins using logarithmic distribution (20 Hz - 18 kHz)
                const minSampleIndex = 1; // ~40 Hz
                const maxSampleIndex = Math.floor(data.length * 0.85); // ~18 kHz

                for (let i = 0; i < barCount; i++) {
                    // Logarithmic frequency sampling index calculation
                    const logRatio = Math.pow(i / (barCount - 1), 2.2); 
                    const sampleIndex = Math.floor(minSampleIndex + logRatio * (maxSampleIndex - minSampleIndex));
                    
                    // High frequency boost (equalizing treble sensitivity for human ear profile)
                    const freqBoost = 1 + (i / barCount) * 1.8;
                    const rawVal = (data[sampleIndex] || 0) * freqBoost;
                    const normalizedVal = Math.min(255, rawVal);

                    // Decay physics simulation for smooth motion
                    if (normalizedVal > barDecayArray[i]) {
                        barDecayArray[i] = normalizedVal;
                    } else {
                        barDecayArray[i] = Math.max(0, barDecayArray[i] - 7); // Smooth fall down
                    }

                    const barHeight = (barDecayArray[i] / 255) * (canvas.height * 0.72);
                    const x = i * (barWidth + gap);
                    const y = canvas.height - barHeight;

                    // Dynamic Color Gradient per bar height
                    const gradient = ctx.createLinearGradient(0, canvas.height, 0, Math.max(0, y));
                    gradient.addColorStop(0, currentStation.primaryColor);
                    gradient.addColorStop(0.55, currentStation.secondaryColor);
                    gradient.addColorStop(1, 'rgba(255, 255, 255, 0.95)');

                    // Render Rounded Top Bars
                    ctx.fillStyle = gradient;
                    const cornerRadius = Math.min(4, barWidth / 2);
                    
                    ctx.beginPath();
                    if (barHeight > cornerRadius) {
                        ctx.roundRect(x, y, barWidth, barHeight, [cornerRadius, cornerRadius, 0, 0]);
                    } else {
                        ctx.rect(x, y, barWidth, Math.max(2, barHeight));
                    }
                    ctx.fill();
                }
            }

            function drawWave(data) {
                ctx.beginPath();
                ctx.lineWidth = 3;
                ctx.strokeStyle = currentStation.primaryColor;

                const sliceWidth = canvas.width / data.length;
                let x = 0;

                for (let i = 0; i < data.length; i++) {
                    const v = data[i] / 128.0;
                    const y = (v * canvas.height) / 3 + canvas.height / 3;

                    if (i === 0) ctx.moveTo(x, y);
                    else ctx.lineTo(x, y);

                    x += sliceWidth;
                }

                ctx.lineTo(canvas.width, canvas.height / 2);
                ctx.stroke();
            }

            function drawCircle(data) {
                const centerX = canvas.width / 2;
                const centerY = canvas.height / 2;
                const radius = Math.min(centerX, centerY) * 0.4;

                ctx.beginPath();
                ctx.strokeStyle = currentStation.primaryColor;
                ctx.lineWidth = 2;

                for (let i = 0; i < data.length; i++) {
                    const rad = (Math.PI * 2 / data.length) * i;
                    const barLen = (data[i] / 255) * 50;
                    const x1 = centerX + Math.cos(rad) * radius;
                    const y1 = centerY + Math.sin(rad) * radius;
                    const x2 = centerX + Math.cos(rad) * (radius + barLen);
                    const y2 = centerY + Math.sin(rad) * (radius + barLen);

                    ctx.moveTo(x1, y1);
                    ctx.lineTo(x2, y2);
                }
                ctx.stroke();
            }

            // Software-rendered 3D: points and meshes have x/y/z coordinates,
            // camera rotation, perspective projection and back-to-front sorting.
            // No extra library, CDN or WebGL context is required.
            function project3D(x, y, z, yaw = 0, pitch = 0) {
                const rx = x * Math.cos(yaw) + z * Math.sin(yaw);
                const rz = -x * Math.sin(yaw) + z * Math.cos(yaw);
                const ry = y * Math.cos(pitch) - rz * Math.sin(pitch);
                const depth = y * Math.sin(pitch) + rz * Math.cos(pitch);
                const scale = 3.4 / Math.max(0.35, 3.4 + depth);
                const size = Math.min(canvas.width, canvas.height) * 0.33;
                return { x: canvas.width / 2 + rx * size * scale,
                         y: canvas.height / 2 + ry * size * scale,
                         z: depth, scale };
            }
            function energy(data, start = 0, end = 0.15) {
                const lo = Math.floor(data.length * start);
                const hi = Math.max(lo + 1, Math.floor(data.length * end));
                let sum = 0;
                for (let i = lo; i < hi; i++) sum += data[i] || 0;
                return sum / ((hi - lo) * 255);
            }
            function path3D(points, color, alpha = 1, width = 1, closed = false) {
                if (!points.length) return;
                ctx.globalAlpha = alpha;
                ctx.strokeStyle = color;
                ctx.lineWidth = width;
                ctx.beginPath();
                points.forEach((p, i) => i ? ctx.lineTo(p.x, p.y) : ctx.moveTo(p.x, p.y));
                if (closed) ctx.closePath();
                ctx.stroke();
                ctx.globalAlpha = 1;
            }
            function drawSphere3D(data) {
                const bass = music.bass;
                const radius = 0.9 + bass * 0.4 + music.pulse * 0.22;
                const yaw = sceneTime * 0.25;
                const pitch = 0.3;
                const lines = [];
                for (let lat = 1; lat < 13; lat++) {
                    const theta = lat / 13 * Math.PI;
                    const points = [];
                    for (let lon = 0; lon <= 64; lon++) {
                        const phi = lon / 64 * Math.PI * 2;
                        const bump = (data[(lon * 3 + lat * 5) % data.length] / 255) * (0.1 + music.mids * 0.22);
                        const r = radius + bump;
                        points.push(project3D(r * Math.sin(theta) * Math.cos(phi),
                            r * Math.cos(theta), r * Math.sin(theta) * Math.sin(phi), yaw, pitch));
                    }
                    lines.push(points);
                }
                for (let lon = 0; lon < 18; lon++) {
                    const phi = lon / 18 * Math.PI * 2;
                    const points = [];
                    for (let lat = 0; lat <= 32; lat++) {
                        const theta = lat / 32 * Math.PI;
                        points.push(project3D(radius * Math.sin(theta) * Math.cos(phi),
                            radius * Math.cos(theta), radius * Math.sin(theta) * Math.sin(phi), yaw, pitch));
                    }
                    lines.push(points);
                }
                lines.sort((a, b) => b[0].z - a[0].z);
                lines.forEach((points, i) => path3D(points,
                    i % 2 ? currentStation.primaryColor : currentStation.secondaryColor, 0.65, 1.2));
            }
            function drawTunnel3D(data) {
                const bass = music.bass;
                const rings = [];
                for (let ring = 0; ring < 22; ring++) {
                    const z = ((ring * 0.55 - sceneTime * 1.3) % 12.1 + 12.1) % 12.1 - 2.3;
                    const points = [];
                    for (let j = 0; j < 48; j++) {
                        const angle = j / 48 * Math.PI * 2 + sceneTime * 0.15 + ring * 0.03;
                        const r = 1.15 + bass * 0.35 + music.pulse * 0.22 + data[(j * 4) % data.length] / 255 * 0.22;
                        points.push(project3D(Math.cos(angle) * r, Math.sin(angle) * r, z));
                    }
                    rings.push({ z, points });
                }
                rings.sort((a, b) => b.z - a.z);
                rings.forEach((ring, i) => {
                    const alpha = Math.max(0.1, 0.85 - (ring.z + 2.3) / 15);
                    path3D(ring.points, i % 2 ? currentStation.primaryColor : currentStation.secondaryColor,
                        alpha, Math.min(3, ring.points[0].scale), true);
                });
            }
            const spectrumHistory = [];
            let historyTime = -1;
            function drawSpectrum3D(data) {
                const cols = 28, rows = 18;
                if (performance.now() - historyTime > 55 || !spectrumHistory.length) {
                    const row = Array.from({length: cols}, (_, i) =>
                        data[Math.floor(1 + Math.pow(i / (cols - 1), 1.8) * (data.length * 0.8 - 1))] / 255);
                    spectrumHistory.unshift(row);
                    if (spectrumHistory.length > rows) spectrumHistory.pop();
                    historyTime = performance.now();
                }
                const yaw = -0.32 + Math.sin(sceneTime * 0.15) * 0.08;
                for (let r = rows - 1; r >= 0; r--) {
                    const row = spectrumHistory[r] || Array(cols).fill(0);
                    const points = row.map((v, c) => project3D((c / (cols - 1) - 0.5) * 3.5,
                        0.65 - v * 1.5, r / (rows - 1) * 3.2 - 0.9, yaw, 0.38));
                    path3D(points, r % 2 ? currentStation.primaryColor : currentStation.secondaryColor,
                        0.25 + (1 - r / rows) * 0.65, 1.4);
                    if (r < spectrumHistory.length - 1) {
                        for (let c = 0; c < cols; c += 2) {
                            const back = project3D((c / (cols - 1) - 0.5) * 3.5,
                                0.65 - spectrumHistory[r + 1][c] * 1.5,
                                (r + 1) / (rows - 1) * 3.2 - 0.9, yaw, 0.38);
                            path3D([points[c], back], currentStation.secondaryColor, 0.22);
                        }
                    }
                }
            }
            const galaxyStars = Array.from({ length: 420 }, (_, i) => {
                const f = (i + 0.5) / 420;
                return { r: Math.sqrt(f) * 1.65, a: i * 2.3999632297,
                    y: Math.sin(i * 13.7) * 0.16, bin: i % 128 };
            });
            function drawGalaxy3D(data) {
                const bass = music.bass;
                const points = galaxyStars.map(star => {
                    const level = data[star.bin] / 255;
                    const angle = star.a + star.r * 2 + sceneTime * 0.22;
                    const r = star.r * (1 + bass * 0.22 + music.pulse * 0.18);
                    const p = project3D(Math.cos(angle) * r, star.y * (1 + level * 2 + music.mids * 3),
                        Math.sin(angle) * r, 0, 0.85);
                    return { ...p, level };
                }).sort((a, b) => b.z - a.z);
                points.forEach(p => {
                    ctx.globalAlpha = Math.min(1, 0.3 + p.level * 0.6);
                    ctx.fillStyle = p.level > 0.5 ? currentStation.primaryColor : currentStation.secondaryColor;
                    ctx.beginPath();
                    ctx.arc(p.x, p.y, Math.max(0.5, (0.8 + p.level * 1.7 + music.highs * 1.8) * p.scale), 0, Math.PI * 2);
                    ctx.fill();
                });
                ctx.globalAlpha = 1;
                const center = project3D(0, 0, 0);
                const radius = Math.min(canvas.width, canvas.height) * (0.035 + bass * 0.065 + music.pulse * 0.035);
                const glow = ctx.createRadialGradient(center.x, center.y, 0, center.x, center.y, radius);
                glow.addColorStop(0, 'rgba(255,255,255,0.8)');
                glow.addColorStop(0.35, currentStation.primaryColor);
                glow.addColorStop(1, 'rgba(0,0,0,0)');
                ctx.fillStyle = glow;
                ctx.fillRect(center.x - radius, center.y - radius, radius * 2, radius * 2);
            }
            visualizerButtons.forEach(btn => btn.addEventListener('click', () => setVisMode(btn.dataset.vis)));
            function setVisMode(mode) {
                visualizerMode = mode;
                spectrumHistory.length = 0;
                historyTime = -1;
                visualizerButtons.forEach(btn => {
                    const active = btn.dataset.vis === mode;
                    btn.setAttribute('aria-pressed', String(active));
                    btn.className = 'px-3 py-1 rounded-lg text-[11px] font-medium transition-all ' +
                        (active ? 'bg-brand-blue text-white' : 'text-gray-400 hover:text-white');
                });
                canvas.style.opacity = fullscreenOpen ? '1' : (mode.endsWith('3d') ? '0.65' : '0.35');
                if (fullscreenOpen) fullscreenSelect.value = mode;
                try { localStorage.setItem('radioVisualizerMode', mode); } catch (_) {}
            }

            const fullscreenPanel = document.getElementById('visualizerFullscreen');
            const fullscreenButton = document.getElementById('fullscreenVisBtn');
            const fullscreenClose = document.getElementById('closeFullscreenVis');
            const fullscreenSelect = document.getElementById('fullscreenVisMode');
            const fullscreenCaption = document.getElementById('fullscreenVisCaption');
            const canvasHome = canvas.parentElement;
            const canvasMarker = document.createComment('visualizer original position');
            canvasHome.insertBefore(canvasMarker, canvas);
            let fullscreenOpen = false;
            let fullscreenSavedFocus = null;
            let savedBodyOverflow = '';
            let backgroundStates = [];
            let priorMode = 'bars';
            function openVisualizerFullscreen() {
                if (fullscreenOpen) return;
                priorMode = visualizerMode;
                fullscreenSavedFocus = document.activeElement;
                fullscreenOpen = true;
                savedBodyOverflow = document.body.style.overflow;
                document.body.style.overflow = 'hidden';
                fullscreenPanel.hidden = false;
                fullscreenPanel.prepend(canvas);
                backgroundStates = Array.from(document.body.children)
                    .filter(el => el !== fullscreenPanel && !['SCRIPT', 'STYLE'].includes(el.tagName))
                    .map(el => ({el, inert: el.inert}));
                backgroundStates.forEach(({el}) => { el.inert = true; });
                setVisMode(visualizerMode.endsWith('3d') ? visualizerMode : 'sphere3d');
                fullscreenCaption.textContent = visualizerStatus.textContent;
                resizeCanvas();
                fullscreenClose.focus();
                if (isPlaying) startVisualizer();
                // Keep the full-window overlay if true fullscreen is unsupported or refused.
                if (fullscreenPanel.requestFullscreen && !document.fullscreenElement) {
                    try {
                        const request = fullscreenPanel.requestFullscreen();
                        if (request && request.catch) request.catch(() => {});
                    } catch (_) {}
                }
            }
            function restoreVisualizerWindow() {
                if (!fullscreenOpen) return;
                fullscreenOpen = false;
                canvasMarker.after(canvas);
                fullscreenPanel.hidden = true;
                document.body.style.overflow = savedBodyOverflow;
                backgroundStates.forEach(({el, inert}) => { el.inert = inert; });
                backgroundStates = [];
                setVisMode(priorMode);
                resizeCanvas();
                if (isPlaying) startVisualizer();
                if (fullscreenSavedFocus && fullscreenSavedFocus.isConnected) fullscreenSavedFocus.focus();
            }
            function closeVisualizerFullscreen() {
                if (document.fullscreenElement === fullscreenPanel && document.exitFullscreen) {
                    try {
                        const request = document.exitFullscreen();
                        if (request && request.catch) request.catch(() => {});
                    } catch (_) {}
                }
                restoreVisualizerWindow();
            }
            fullscreenButton.addEventListener('click', openVisualizerFullscreen);
            fullscreenClose.addEventListener('click', closeVisualizerFullscreen);
            fullscreenSelect.addEventListener('change', () => setVisMode(fullscreenSelect.value));
            document.addEventListener('fullscreenchange', () => {
                if (fullscreenOpen && document.fullscreenElement !== fullscreenPanel) restoreVisualizerWindow();
                resizeCanvas();
            });
            fullscreenPanel.addEventListener('keydown', event => {
                if (event.key === 'Escape') {
                    event.preventDefault();
                    closeVisualizerFullscreen();
                } else if (event.key === 'Tab') {
                    if (event.shiftKey && document.activeElement === fullscreenSelect) {
                        event.preventDefault(); fullscreenClose.focus();
                    } else if (!event.shiftKey && document.activeElement === fullscreenClose) {
                        event.preventDefault(); fullscreenSelect.focus();
                    }
                }
            });
            new MutationObserver(() => {
                if (fullscreenOpen) fullscreenCaption.textContent = visualizerStatus.textContent;
            }).observe(visualizerStatus, { childList: true, characterData: true, subtree: true });
            if (window.ResizeObserver) new ResizeObserver(resizeCanvas).observe(fullscreenPanel);
            if (window.visualViewport) window.visualViewport.addEventListener('resize', resizeCanvas);

            setVisMode(visualizerMode);

            playBtn.addEventListener('click', togglePlay);

            // Sleep Timer Events
            sleepTimerBtn.addEventListener('click', () => {
                sleepModal.classList.remove('hidden');
                setTimeout(() => sleepModal.classList.remove('opacity-0'), 10);
            });

            closeSleepModal.addEventListener('click', hideSleepModal);
            
            function hideSleepModal() {
                sleepModal.classList.add('opacity-0');
                setTimeout(() => sleepModal.classList.add('hidden'), 300);
            }

            document.querySelectorAll('.sleep-option').forEach(btn => {
                btn.addEventListener('click', () => {
                    const mins = parseInt(btn.getAttribute('data-minutes'));
                    setSleepTimer(mins);
                    hideSleepModal();
                });
            });

            function setSleepTimer(minutes) {
                clearSleepTimer();
                const ms = minutes * 60 * 1000;
                let remainingSecs = minutes * 60;

                sleepBadge.textContent = `${minutes}m`;
                sleepBadge.classList.remove('hidden');
                cancelSleepTimer.classList.remove('hidden');

                showToast(`Časovač nastaven na ${minutes} minut`);

                sleepInterval = setInterval(() => {
                    remainingSecs--;
                    const m = Math.floor(remainingSecs / 60);
                    sleepBadge.textContent = `${m}m`;

                    if (remainingSecs <= 0) clearSleepTimer();
                }, 1000);

                sleepTimeout = setTimeout(() => {
                    if (isPlaying) {
                        audio.pause();
                        setPlayingState(false);
                        showToast("Časovač vypnul přehrávání rádia", "fa-solid fa-moon text-brand-blue");
                    }
                }, ms);
            }

            cancelSleepTimer.addEventListener('click', () => {
                clearSleepTimer();
                hideSleepModal();
                showToast("Časovač vypnutí byl zrušen");
            });

            function clearSleepTimer() {
                if (sleepTimeout) clearTimeout(sleepTimeout);
                if (sleepInterval) clearInterval(sleepInterval);
                sleepBadge.classList.add('hidden');
                cancelSleepTimer.classList.add('hidden');
            }

            infoBtn.addEventListener('click', () => {
                infoModal.classList.remove('hidden');
                setTimeout(() => infoModal.classList.remove('opacity-0'), 10);
            });

            const hideInfoModal = () => {
                infoModal.classList.add('opacity-0');
                setTimeout(() => infoModal.classList.add('hidden'), 300);
            };

            closeInfoModal.addEventListener('click', hideInfoModal);
            closeInfoModalBtn.addEventListener('click', hideInfoModal);

            audio.addEventListener('waiting', () => {
                liveText.textContent = "Načítání...";
            });

            audio.addEventListener('playing', () => {
                setPlayingState(true);
            });

            audio.addEventListener('pause', () => setPlayingState(false));
            audio.addEventListener('ended', () => setPlayingState(false));

            audio.addEventListener('error', (e) => {
                console.error("Audio Stream Error:", e);
                setPlayingState(false);
                showToast("Chyba při připojování ke streamu", "fa-solid fa-circle-exclamation text-red-500");
            });
        });
    </script>

    <section id="visualizerFullscreen" hidden role="dialog" aria-modal="true" aria-label="3D vizualizace přes celou obrazovku" tabindex="-1">
        <div class="fullscreen-controls">
            <label style="color:white;font-size:13px;display:flex;align-items:center;gap:10px">
                3D vizualizace
                <select id="fullscreenVisMode" aria-label="Vybrat 3D vizualizaci">
                    <option value="sphere3d">Koule 3D</option>
                    <option value="tunnel3d">Tunel 3D</option>
                    <option value="spectrum3d">Spektrum 3D</option>
                    <option value="galaxy3d">Galaxie 3D</option>
                </select>
            </label>
            <button type="button" id="closeFullscreenVis" aria-label="Zavřít celou obrazovku">✕ Zpět do přehrávače</button>
        </div>
        <p id="fullscreenVisCaption" class="fullscreen-caption" role="status">Spusť přehrávání v přehrávači, aby se vizualizace rozhýbala.</p>
    </section>

</body>
</html>
