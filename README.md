# Jakey9903.github.io
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>SharkNinja Dual-Zone Toastie Machine Control Panel</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700;800;900&family=Share+Tech+Mono&display=swap" rel="stylesheet">
  <style>
    body {
      font-family: 'Inter', sans-serif;
      background-color: #0b0d10;
      color: #e2e8f0;
      user-select: none;
    }

    .font-digital {
      font-family: 'Share Tech Mono', monospace;
    }

    /* Metallic Brushed Stainless Steel Finish */
    .metallic-chassis {
      background: linear-gradient(145deg, #8a929a 0%, #4a5158 35%, #9aa2aa 70%, #3e444a 100%);
      box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.8), 0 0 2px 1px rgba(255, 255, 255, 0.2) inset;
    }

    /* Glossy Dark Control Surface */
    .glass-panel {
      background: radial-gradient(circle at 50% 20%, #1a1c23 0%, #0c0d11 90%);
      box-shadow: inset 0 0 20px rgba(0, 0, 0, 0.9), 0 1px 1px rgba(255, 255, 255, 0.1);
    }

    /* Physical Push Buttons */
    .btn-tactile {
      background: linear-gradient(145deg, #2c3038, #181a1f);
      box-shadow: 0 5px 10px rgba(0, 0, 0, 0.7), inset 0 1px 1px rgba(255, 255, 255, 0.15), 0 -1px 2px rgba(0,0,0,0.5) inset;
      transition: all 0.12s cubic-bezier(0.4, 0, 0.2, 1);
    }

    .btn-tactile:active:not(:disabled) {
      transform: translateY(2px);
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.9), inset 0 2px 4px rgba(0, 0, 0, 0.8);
    }

    /* Dynamic Glow Effects */
    .glow-led-red {
      box-shadow: 0 0 10px #ff3b30, 0 0 3px #ff3b30;
    }

    .glow-led-cyan {
      box-shadow: 0 0 12px #00f0ff, 0 0 3px #00f0ff;
    }

    .glow-led-white {
      box-shadow: 0 0 14px rgba(255, 255, 255, 0.9), 0 0 4px #ffffff;
    }

    .glow-display {
      text-shadow: 0 0 12px rgba(255, 255, 255, 0.85), 0 0 3px rgba(255, 255, 255, 0.5);
    }

    /* Smooth LED transition */
    .led-transition {
      transition: background-color 0.2s ease, box-shadow 0.2s ease, border-color 0.2s ease, opacity 0.2s ease;
    }
  </style>
</head>
<body class="min-h-screen flex items-center justify-center p-4 sm:p-6">

  <!-- Main Machine Body Outer Frame -->
  <div class="metallic-chassis p-5 sm:p-8 rounded-3xl max-w-3xl w-full">
    
    <!-- Inner Dark Glass Panel -->
    <div id="controlPanel" class="glass-panel border-2 border-zinc-800/80 rounded-2xl p-5 sm:p-8 flex flex-col gap-6 relative overflow-hidden">
      
      <!-- Brand Header -->
      <div class="flex justify-center items-center pt-1">
        <div class="tracking-wider text-2xl sm:text-3xl font-black italic uppercase text-slate-100 flex items-center gap-0.5 opacity-90 drop-shadow">
          SHARK<span class="font-light tracking-normal text-slate-300">NINJA</span>
        </div>
      </div>

      <!-- TOP BAR: Controls & Main Display -->
      <div class="grid grid-cols-6 gap-2 sm:gap-4 items-center">
        
        <!-- Power Button -->
        <div class="flex flex-col items-center gap-1.5 col-span-1">
          <button id="powerBtn" onclick="togglePower()" class="btn-tactile w-12 h-12 sm:w-16 sm:h-16 rounded-full flex items-center justify-center border border-zinc-700/60 group relative">
            <svg class="w-5 h-5 sm:w-6 sm:h-6 stroke-zinc-500 led-transition group-hover:stroke-zinc-300" id="powerIcon" fill="none" viewBox="0 0 24 24" stroke-width="2.2" stroke-linecap="round">
              <path d="M18.36 6.64a9 9 0 1 1-12.73 0M12 2v10"/>
            </svg>
          </button>
          <span class="text-[10px] sm:text-xs font-bold tracking-wider text-zinc-500 uppercase" id="powerLabel">POWER</span>
        </div>

        <!-- Zone 1 Selector -->
        <div class="flex flex-col items-center gap-1.5 col-span-1">
          <button id="zone1Btn" onclick="selectZone(1)" class="btn-tactile w-12 h-12 sm:w-16 sm:h-16 rounded-full flex flex-col items-center justify-center border border-zinc-700/60 relative">
            <div id="zone1Led" class="w-2 h-2 rounded-full bg-zinc-800 mb-0.5 led-transition"></div>
            <svg class="w-4 h-4 sm:w-5 sm:h-5 stroke-zinc-500 led-transition" id="zone1Icon" fill="none" viewBox="0 0 24 24" stroke-width="2">
              <rect x="4" y="4" width="16" height="16" rx="3"/>
            </svg>
          </button>
          <span class="text-[10px] sm:text-xs font-bold tracking-wider text-zinc-500 uppercase" id="zone1Label">ZONE 1</span>
        </div>

        <!-- Timer Display (7-Segment LED Style) -->
        <div class="col-span-2 flex justify-center">
          <div class="bg-black/90 border-2 border-zinc-900 rounded-xl px-4 py-2 sm:px-6 sm:py-3 shadow-inner text-center min-w-[120px] sm:min-w-[150px]">
            <div id="timerDisplay" class="font-digital text-3xl sm:text-5xl font-bold text-zinc-800 tracking-wider leading-none select-none">
              88:88
            </div>
            <div class="text-[9px] sm:text-[10px] font-semibold text-zinc-600 tracking-widest uppercase mt-1">COOK TIME</div>
          </div>
        </div>

        <!-- Zone 2 Selector -->
        <div class="flex flex-col items-center gap-1.5 col-span-1">
          <button id="zone2Btn" onclick="selectZone(2)" class="btn-tactile w-12 h-12 sm:w-16 sm:h-16 rounded-full flex flex-col items-center justify-center border border-zinc-700/60 relative">
            <div id="zone2Led" class="w-2 h-2 rounded-full bg-zinc-800 mb-0.5 led-transition"></div>
            <svg class="w-4 h-4 sm:w-5 sm:h-5 stroke-zinc-500 led-transition" id="zone2Icon" fill="none" viewBox="0 0 24 24" stroke-width="2">
              <rect x="4" y="4" width="16" height="16" rx="3"/>
            </svg>
          </button>
          <span class="text-[10px] sm:text-xs font-bold tracking-wider text-zinc-500 uppercase" id="zone2Label">ZONE 2</span>
        </div>

        <!-- Right Controls: Cancel & Start Group -->
        <div class="flex col-span-1 justify-center gap-2 sm:gap-3">
          <!-- Cancel -->
          <div class="flex flex-col items-center gap-1.5">
            <button id="cancelBtn" onclick="pressCancel()" class="btn-tactile w-11 h-11 sm:w-14 sm:h-14 rounded-full flex items-center justify-center border border-zinc-700/60">
              <svg class="w-4 h-4 sm:w-5 sm:h-5 stroke-zinc-500 led-transition" id="cancelIcon" fill="none" viewBox="0 0 24 24" stroke-width="2.2" stroke-linecap="round">
                <line x1="18" y1="6" x2="6" y2="18"/>
                <line x1="6" y1="6" x2="18" y2="18"/>
              </svg>
            </button>
            <span class="text-[9px] sm:text-[10px] font-bold tracking-wider text-zinc-500 uppercase" id="cancelLabel">CANCEL</span>
          </div>

          <!-- Start -->
          <div class="flex flex-col items-center gap-1.5">
            <button id="startBtn" onclick="pressStart()" class="btn-tactile w-11 h-11 sm:w-14 sm:h-14 rounded-full flex items-center justify-center border border-zinc-700/60">
              <svg class="w-4 h-4 sm:w-5 sm:h-5 stroke-zinc-500 led-transition ml-0.5" id="startIcon" fill="none" viewBox="0 0 24 24" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
                <polygon points="5 3 19 12 5 21 5 3"/>
              </svg>
            </button>
            <span class="text-[9px] sm:text-[10px] font-bold tracking-wider text-zinc-500 uppercase" id="startLabel">START</span>
          </div>
        </div>

      </div>

      <!-- Divider: MODE -->
      <div class="relative my-1 flex items-center justify-center">
        <div class="absolute inset-0 flex items-center"><div class="w-full border-t border-zinc-800"></div></div>
        <span class="relative bg-[#111217] px-4 text-[11px] font-extrabold tracking-widest text-zinc-600 uppercase" id="modeHeader">MODE SELECT</span>
      </div>

      <!-- MODE SELECTION ROW -->
      <div class="grid grid-cols-4 gap-2 sm:gap-6">
        
        <!-- Toastie Mode -->
        <div class="flex flex-col items-center gap-2">
          <button id="modeToastie" onclick="selectMode('toastie')" class="btn-tactile w-14 h-14 sm:w-20 sm:h-20 rounded-2xl flex items-center justify-center border border-zinc-700/60 relative">
            <svg class="w-7 h-7 sm:w-9 sm:h-9 stroke-zinc-500 led-transition" fill="none" viewBox="0 0 24 24" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
              <path d="M5 9a3 3 0 0 1 3-3h8a3 3 0 0 1 3 3v8a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V9z"/>
              <line x1="5" y1="12" x2="19" y2="12"/>
            </svg>
          </button>
          <span class="text-[10px] sm:text-xs font-bold tracking-wider text-zinc-500 uppercase" id="labelToastie">TOASTIE</span>
        </div>

        <!-- Waffle Mode -->
        <div class="flex flex-col items-center gap-2">
          <button id="modeWaffle" onclick="selectMode('waffle')" class="btn-tactile w-14 h-14 sm:w-20 sm:h-20 rounded-2xl flex items-center justify-center border border-zinc-700/60 relative">
            <svg class="w-7 h-7 sm:w-9 sm:h-9 stroke-zinc-500 led-transition" fill="none" viewBox="0 0 24 24" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
              <rect x="4" y="4" width="16" height="16" rx="3"/>
              <line x1="9" y1="4" x2="9" y2="20"/>
              <line x1="15" y1="4" x2="15" y2="20"/>
              <line x1="4" y1="9" x2="20" y2="9"/>
              <line x1="4" y1="15" x2="20" y2="15"/>
            </svg>
          </button>
          <span class="text-[10px] sm:text-xs font-bold tracking-wider text-zinc-500 uppercase" id="labelWaffle">WAFFLE</span>
        </div>

        <!-- Egg Fry Mode -->
        <div class="flex flex-col items-center gap-2">
          <button id="modeEgg" onclick="selectMode('egg')" class="btn-tactile w-14 h-14 sm:w-20 sm:h-20 rounded-2xl flex items-center justify-center border border-zinc-700/60 relative">
            <svg class="w-7 h-7 sm:w-9 sm:h-9 stroke-zinc-500 led-transition" fill="none" viewBox="0 0 24 24" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
              <path d="M12 3c-4.5 0-8 4.5-8 9.5 0 4.5 3.5 7.5 8 7.5s8-3 8-7.5C20 7.5 16.5 3 12 3z"/>
              <circle cx="12" cy="13" r="3"/>
            </svg>
          </button>
          <span class="text-[10px] sm:text-xs font-bold tracking-wider text-zinc-500 uppercase" id="labelEgg">EGG FRY</span>
        </div>

        <!-- BBQ / Grill Mode -->
        <div class="flex flex-col items-center gap-2">
          <button id="modeBbq" onclick="selectMode('bbq')" class="btn-tactile w-14 h-14 sm:w-20 sm:h-20 rounded-2xl flex items-center justify-center border border-zinc-700/60 relative">
            <svg class="w-7 h-7 sm:w-9 sm:h-9 stroke-zinc-500 led-transition" fill="none" viewBox="0 0 24 24" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
              <path d="M4 11a8 8 0 0 0 16 0H4z"/>
              <line x1="6" y1="16" x2="4" y2="20"/>
              <line x1="18" y1="16" x2="20" y2="20"/>
              <line x1="8" y1="11" x2="8" y2="7"/>
              <line x1="12" y1="11" x2="12" y2="6"/>
              <line x1="16" y1="11" x2="16" y2="7"/>
            </svg>
          </button>
          <span class="text-[10px] sm:text-xs font-bold tracking-wider text-zinc-500 uppercase" id="labelBbq">BBQ / GRILL</span>
        </div>

      </div>

      <!-- Divider: BROWNING & HEAT -->
      <div class="relative my-1 flex items-center justify-center">
        <div class="absolute inset-0 flex items-center"><div class="w-full border-t border-zinc-800"></div></div>
        <span class="relative bg-[#111217] px-4 text-[11px] font-extrabold tracking-widest text-zinc-600 uppercase" id="browningHeader">BROWNING & HEAT CONTROL</span>
      </div>

      <!-- BROWNING SHADES & HEAT CONTROL ROW -->
      <div class="grid grid-cols-7 gap-2 sm:gap-3 items-end pt-1">
        
        <!-- 6 Browning Shades (Col-span 5) -->
        <div class="col-span-5 grid grid-cols-6 gap-1.5 sm:gap-2">
          
          <!-- Shade 1 -->
          <div class="flex flex-col items-center gap-1.5 cursor-pointer" onclick="selectShade(0)">
            <div id="shadeLed0" class="w-6 sm:w-8 h-1.5 rounded-sm bg-zinc-800 led-transition"></div>
            <div id="shadeBox0" class="w-full h-9 sm:h-11 rounded-md border-2 border-zinc-800 bg-[#faecd0] opacity-30 led-transition"></div>
          </div>

          <!-- Shade 2 -->
          <div class="flex flex-col items-center gap-1.5 cursor-pointer" onclick="selectShade(1)">
            <div id="shadeLed1" class="w-6 sm:w-8 h-1.5 rounded-sm bg-zinc-800 led-transition"></div>
            <div id="shadeBox1" class="w-full h-9 sm:h-11 rounded-md border-2 border-zinc-800 bg-[#e7be7c] opacity-30 led-transition"></div>
          </div>

          <!-- Shade 3 -->
          <div class="flex flex-col items-center gap-1.5 cursor-pointer" onclick="selectShade(2)">
            <div id="shadeLed2" class="w-6 sm:w-8 h-1.5 rounded-sm bg-zinc-800 led-transition"></div>
            <div id="shadeBox2" class="w-full h-9 sm:h-11 rounded-md border-2 border-zinc-800 bg-[#c78b3f] opacity-30 led-transition"></div>
          </div>

          <!-- Shade 4 -->
          <div class="flex flex-col items-center gap-1.5 cursor-pointer" onclick="selectShade(3)">
            <div id="shadeLed3" class="w-6 sm:w-8 h-1.5 rounded-sm bg-zinc-800 led-transition"></div>
            <div id="shadeBox3" class="w-full h-9 sm:h-11 rounded-md border-2 border-zinc-800 bg-[#985822] opacity-30 led-transition"></div>
          </div>

          <!-- Shade 5 -->
          <div class="flex flex-col items-center gap-1.5 cursor-pointer" onclick="selectShade(4)">
            <div id="shadeLed4" class="w-6 sm:w-8 h-1.5 rounded-sm bg-zinc-800 led-transition"></div>
            <div id="shadeBox4" class="w-full h-9 sm:h-11 rounded-md border-2 border-zinc-800 bg-[#65330a] opacity-30 led-transition"></div>
          </div>

          <!-- Shade 6 -->
          <div class="flex flex-col items-center gap-1.5 cursor-pointer" onclick="selectShade(5)">
            <div id="shadeLed5" class="w-6 sm:w-8 h-1.5 rounded-sm bg-zinc-800 led-transition"></div>
            <div id="shadeBox5" class="w-full h-9 sm:h-11 rounded-md border-2 border-zinc-800 bg-[#3a1b02] opacity-30 led-transition"></div>
          </div>

        </div>

        <!-- Heat Control Option (Col-span 2) -->
        <div class="col-span-2 flex flex-col items-center gap-1.5 border-l border-zinc-800/80 pl-2 sm:pl-4">
          
          <!-- 4 Red Heat Level LEDs Indicator -->
          <div class="flex items-center justify-between w-full max-w-[100px] px-1">
            <div id="heatLed0" class="w-3.5 h-1.5 rounded-sm bg-zinc-800 led-transition"></div>
            <div id="heatLed1" class="w-3.5 h-1.5 rounded-sm bg-zinc-800 led-transition"></div>
            <div id="heatLed2" class="w-3.5 h-1.5 rounded-sm bg-zinc-800 led-transition"></div>
            <div id="heatLed3" class="w-3.5 h-1.5 rounded-sm bg-zinc-800 led-transition"></div>
          </div>

          <!-- Heat Button -->
          <button id="heatBtn" onclick="cycleHeat()" class="btn-tactile w-full h-9 sm:h-11 rounded-lg flex items-center justify-center gap-1.5 border border-zinc-700/60 relative">
            <svg class="w-5 h-5 stroke-zinc-500 led-transition" id="heatIcon" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M12 2c0 3-3 4.5-3 7.5 0 2.5 2 4.5 5 4.5s5-2 5-4.5c0-3-3-4.5-3-7.5z"/>
              <path d="M7 14.5C7 18 9.5 21 12 21s5-3 5-6.5"/>
            </svg>
            <span class="text-[10px] sm:text-xs font-bold tracking-wider text-zinc-500 uppercase" id="heatLabel">HEAT</span>
          </button>

        </div>

      </div>

    </div>
  </div>

  <script>
    // Machine State Data
    let powerOn = false;
    let activeZone = 1;
    let timerInterval = null;

    // Default configuration for each cooking zone
    const zones = {
      1: {
        mode: 'toastie',   // 'toastie', 'waffle', 'egg', 'bbq'
        shade: 2,          // 0 to 5
        heatLevel: 2,      // 1 to 4
        cooking: false,
        secondsLeft: 240
      },
      2: {
        mode: 'toastie',
        shade: 3,
        heatLevel: 3,
        cooking: false,
        secondsLeft: 270
      }
    };

    // Preset Cook Times in Seconds [Level 1..6]
    const timePresets = {
      toastie: [150, 195, 240, 285, 330, 375],
      waffle:  [180, 225, 270, 315, 360, 405],
      egg:     [120, 180, 240, 300], // tied to heat levels 1..4
      bbq:     [300, 420, 540, 660]  // tied to heat levels 1..4
    };

    // Toggle Power State ON/OFF
    function togglePower() {
      powerOn = !powerOn;
      if (!powerOn) {
        // Turn Off Cooking Timers
        clearInterval(timerInterval);
        zones[1].cooking = false;
        zones[2].cooking = false;
      }
      render();
    }

    // Select Active Zone 1 or 2
    function selectZone(zone) {
      if (!powerOn) return;
      activeZone = zone;
      render();
    }

    // Mode Selection Function
    function selectMode(mode) {
      if (!powerOn) return;
      const z = zones[activeZone];
      z.mode = mode;

      // Calculate initial cook time based on mode
      if (mode === 'toastie' || mode === 'waffle') {
        z.secondsLeft = timePresets[mode][z.shade];
      } else {
        z.secondsLeft = timePresets[mode][z.heatLevel - 1];
      }
      render();
    }

    // Select Browning Shade (Toastie & Waffle modes only)
    function selectShade(index) {
      if (!powerOn) return;
      const z = zones[activeZone];
      if (z.mode === 'toastie' || z.mode === 'waffle') {
        z.shade = index;
        z.secondsLeft = timePresets[z.mode][index];
        render();
      }
    }

    // Cycle Heat Level (1-4)
    function cycleHeat() {
      if (!powerOn) return;
      const z = zones[activeZone];
      // Heat cycle works primarily on BBQ and Egg mode, or can adjust heat preset
      z.heatLevel = (z.heatLevel % 4) + 1;
      
      if (z.mode === 'egg' || z.mode === 'bbq') {
        z.secondsLeft = timePresets[z.mode][z.heatLevel - 1];
      }
      render();
    }

    // Press Start Cooking
    function pressStart() {
      if (!powerOn) return;
      const z = zones[activeZone];
      if (z.secondsLeft > 0) {
        z.cooking = true;
        startTimerLoop();
        render();
      }
    }

    // Press Cancel Cooking
    function pressCancel() {
      if (!powerOn) return;
      const z = zones[activeZone];
      z.cooking = false;
      
      // Reset timer to current mode default
      if (z.mode === 'toastie' || z.mode === 'waffle') {
        z.secondsLeft = timePresets[z.mode][z.shade];
      } else {
        z.secondsLeft = timePresets[z.mode][z.heatLevel - 1];
      }
      
      if (!zones[1].cooking && !zones[2].cooking) {
        clearInterval(timerInterval);
        timerInterval = null;
      }
      render();
    }

    // Global Timer Loop
    function startTimerLoop() {
      if (timerInterval) return;
      timerInterval = setInterval(() => {
        let anyCooking = false;
        [1, 2].forEach(zId => {
          if (zones[zId].cooking) {
            if (zones[zId].secondsLeft > 0) {
              zones[zId].secondsLeft--;
              anyCooking = true;
            } else {
              zones[zId].cooking = false;
            }
          }
        });

        if (!anyCooking) {
          clearInterval(timerInterval);
          timerInterval = null;
        }
        render();
      }, 1000);
    }

    // Helper: Format Seconds to MM:SS
    function formatTime(seconds) {
      const m = Math.floor(seconds / 60).toString().padStart(2, '0');
      const s = (seconds % 60).toString().padStart(2, '0');
      return `${m}:${s}`;
    }

    // Main UI Render Function
    function render() {
      // Elements
      const powerIcon = document.getElementById('powerIcon');
      const powerLabel = document.getElementById('powerLabel');
      const timerDisplay = document.getElementById('timerDisplay');

      const zone1Btn = document.getElementById('zone1Btn');
      const zone1Led = document.getElementById('zone1Led');
      const zone1Icon = document.getElementById('zone1Icon');
      const zone1Label = document.getElementById('zone1Label');

      const zone2Btn = document.getElementById('zone2Btn');
      const zone2Led = document.getElementById('zone2Led');
      const zone2Icon = document.getElementById('zone2Icon');
      const zone2Label = document.getElementById('zone2Label');

      const startIcon = document.getElementById('startIcon');
      const startLabel = document.startLabel;
      const cancelIcon = document.getElementById('cancelIcon');

      // Mode Elements
      const modes = {
        toastie: { btn: document.getElementById('modeToastie'), label: document.getElementById('labelToastie') },
        waffle:  { btn: document.getElementById('modeWaffle'),  label: document.getElementById('labelWaffle') },
        egg:     { btn: document.getElementById('modeEgg'),     label: document.getElementById('labelEgg') },
        bbq:     { btn: document.getElementById('modeBbq'),     label: document.getElementById('labelBbq') }
      };

      const browningHeader = document.getElementById('browningHeader');

      // POWER OFF STATE
      if (!powerOn) {
        // Power Icon Off
        powerIcon.setAttribute('class', 'w-5 h-5 sm:w-6 sm:h-6 stroke-zinc-600 led-transition');
        powerLabel.className = "text-[10px] sm:text-xs font-bold tracking-wider text-zinc-600 uppercase";

        // Display Blank
        timerDisplay.innerText = "88:88";
        timerDisplay.className = "font-digital text-3xl sm:text-5xl font-bold text-zinc-900 tracking-wider leading-none select-none";

        // Zone LEDs Off
        zone1Led.className = "w-2 h-2 rounded-full bg-zinc-900 led-transition";
        zone1Icon.setAttribute('class', 'w-4 h-4 sm:w-5 sm:h-5 stroke-zinc-700');
        zone1Label.className = "text-[10px] sm:text-xs font-bold tracking-wider text-zinc-700 uppercase";

        zone2Led.className = "w-2 h-2 rounded-full bg-zinc-900 led-transition";
        zone2Icon.setAttribute('class', 'w-4 h-4 sm:w-5 sm:h-5 stroke-zinc-700');
        zone2Label.className = "text-[10px] sm:text-xs font-bold tracking-wider text-zinc-700 uppercase";

        startIcon.setAttribute('class', 'w-4 h-4 sm:w-5 sm:h-5 stroke-zinc-700 ml-0.5');
        cancelIcon.setAttribute('class', 'w-4 h-4 sm:w-5 sm:h-5 stroke-zinc-700');

        // Reset Modes
        Object.keys(modes).forEach(m => {
          modes[m].btn.querySelector('svg').setAttribute('class', 'w-7 h-7 sm:w-9 sm:h-9 stroke-zinc-700 led-transition');
          modes[m].btn.style.borderColor = "rgba(63, 63, 70, 0.4)";
          modes[m].label.className = "text-[10px] sm:text-xs font-bold tracking-wider text-zinc-700 uppercase";
        });

        // Reset Browning Shades Off
        for (let i = 0; i < 6; i++) {
          document.getElementById(`shadeLed${i}`).className = "w-6 sm:w-8 h-1.5 rounded-sm bg-zinc-900 led-transition";
          document.getElementById(`shadeBox${i}`).style.opacity = "0.08";
          document.getElementById(`shadeBox${i}`).style.borderColor = "#27272a";
        }

        // Reset Heat LEDs Off
        for (let i = 0; i < 4; i++) {
          document.getElementById(`heatLed${i}`).className = "w-3.5 h-1.5 rounded-sm bg-zinc-900 led-transition";
        }
        document.getElementById('heatIcon').setAttribute('class', 'w-5 h-5 stroke-zinc-700 led-transition');
        document.getElementById('heatLabel').className = "text-[10px] sm:text-xs font-bold tracking-wider text-zinc-700 uppercase";
        
        browningHeader.innerText = "BROWNING & HEAT CONTROL";
        browningHeader.className = "relative bg-[#111217] px-4 text-[11px] font-extrabold tracking-widest text-zinc-700 uppercase";
        return;
      }

      // POWER ON STATE ACTIVE
      powerIcon.setAttribute('class', 'w-5 h-5 sm:w-6 sm:h-6 stroke-white led-transition drop-shadow-[0_0_8px_rgba(255,255,255,0.8)]');
      powerLabel.className = "text-[10px] sm:text-xs font-bold tracking-wider text-slate-200 uppercase";

      const current = zones[activeZone];

      // Update Timer Display
      timerDisplay.innerText = formatTime(current.secondsLeft);
      timerDisplay.className = "font-digital text-3xl sm:text-5xl font-bold text-white tracking-wider leading-none select-none glow-display";

      // Zone 1 Active Visuals
      if (activeZone === 1) {
        zone1Led.className = "w-2 h-2 rounded-full bg-cyan-400 glow-led-cyan led-transition";
        zone1Icon.setAttribute('class', 'w-4 h-4 sm:w-5 sm:h-5 stroke-white');
        zone1Label.className = "text-[10px] sm:text-xs font-bold tracking-wider text-cyan-400 uppercase";

        zone2Led.className = zones[2].cooking ? "w-2 h-2 rounded-full bg-red-500 glow-led-red led-transition" : "w-2 h-2 rounded-full bg-zinc-700";
        zone2Icon.setAttribute('class', 'w-4 h-4 sm:w-5 sm:h-5 stroke-zinc-400');
        zone2Label.className = "text-[10px] sm:text-xs font-bold tracking-wider text-zinc-400 uppercase";
      } else {
        zone2Led.className = "w-2 h-2 rounded-full bg-cyan-400 glow-led-cyan led-transition";
        zone2Icon.setAttribute('class', 'w-4 h-4 sm:w-5 sm:h-5 stroke-white');
        zone2Label.className = "text-[10px] sm:text-xs font-bold tracking-wider text-cyan-400 uppercase";

        zone1Led.className = zones[1].cooking ? "w-2 h-2 rounded-full bg-red-500 glow-led-red led-transition" : "w-2 h-2 rounded-full bg-zinc-700";
        zone1Icon.setAttribute('class', 'w-4 h-4 sm:w-5 sm:h-5 stroke-zinc-400');
        zone1Label.className = "text-[10px] sm:text-xs font-bold tracking-wider text-zinc-400 uppercase";
      }

      // Start & Cancel Buttons Active State
      startIcon.setAttribute('class', current.cooking ? 'w-4 h-4 sm:w-5 sm:h-5 stroke-emerald-400 ml-0.5 drop-shadow-[0_0_8px_#34d399]' : 'w-4 h-4 sm:w-5 sm:h-5 stroke-slate-200 ml-0.5');
      cancelIcon.setAttribute('class', 'w-4 h-4 sm:w-5 sm:h-5 stroke-slate-200');

      // Mode Selection Active Visuals
      Object.keys(modes).forEach(m => {
        if (current.mode === m) {
          modes[m].btn.querySelector('svg').setAttribute('class', 'w-7 h-7 sm:w-9 sm:h-9 stroke-white led-transition drop-shadow-[0_0_8px_rgba(255,255,255,0.8)]');
          modes[m].btn.style.borderColor = "#ffffff";
          modes[m].label.className = "text-[10px] sm:text-xs font-bold tracking-wider text-white uppercase";
        } else {
          modes[m].btn.querySelector('svg').setAttribute('class', 'w-7 h-7 sm:w-9 sm:h-9 stroke-zinc-500 led-transition');
          modes[m].btn.style.borderColor = "rgba(63, 63, 70, 0.6)";
          modes[m].label.className = "text-[10px] sm:text-xs font-bold tracking-wider text-zinc-500 uppercase";
        }
      });

      // BROWNING & HEAT LOGIC RENDERING
      browningHeader.innerText = `ZONE ${activeZone} - ${current.mode.toUpperCase()} SETTINGS`;
      browningHeader.className = "relative bg-[#111217] px-4 text-[11px] font-extrabold tracking-widest text-slate-300 uppercase";

      // 1. Toastie & Waffle Mode: Browning active, Heat inactive
      if (current.mode === 'toastie' || current.mode === 'waffle') {
        for (let i = 0; i < 6; i++) {
          if (i === current.shade) {
            document.getElementById(`shadeLed${i}`).className = "w-6 sm:w-8 h-1.5 rounded-sm bg-red-500 glow-led-red led-transition";
            document.getElementById(`shadeBox${i}`).style.opacity = "1";
            document.getElementById(`shadeBox${i}`).style.borderColor = "#ffffff";
          } else {
            document.getElementById(`shadeLed${i}`).className = "w-6 sm:w-8 h-1.5 rounded-sm bg-zinc-800 led-transition";
            document.getElementById(`shadeBox${i}`).style.opacity = "0.35";
            document.getElementById(`shadeBox${i}`).style.borderColor = "#27272a";
          }
        }

        // Heat LEDs dimmed in Toastie / Waffle
        for (let i = 0; i < 4; i++) {
          document.getElementById(`heatLed${i}`).className = "w-3.5 h-1.5 rounded-sm bg-zinc-800 led-transition";
        }
        document.getElementById('heatIcon').setAttribute('class', 'w-5 h-5 stroke-zinc-500 led-transition');
        document.getElementById('heatLabel').className = "text-[10px] sm:text-xs font-bold tracking-wider text-zinc-500 uppercase";
      } 
      // 2. Egg Fry Mode: Browning ALL OFF! Heat active
      else if (current.mode === 'egg') {
        // Browning shades dark
        for (let i = 0; i < 6; i++) {
          document.getElementById(`shadeLed${i}`).className = "w-6 sm:w-8 h-1.5 rounded-sm bg-zinc-800 led-transition";
          document.getElementById(`shadeBox${i}`).style.opacity = "0.15";
          document.getElementById(`shadeBox${i}`).style.borderColor = "#27272a";
        }

        // Cycle 4 Red LEDs for Heat Settings
        for (let i = 0; i < 4; i++) {
          if (i < current.heatLevel) {
            document.getElementById(`heatLed${i}`).className = "w-3.5 h-1.5 rounded-sm bg-red-500 glow-led-red led-transition";
          } else {
            document.getElementById(`heatLed${i}`).className = "w-3.5 h-1.5 rounded-sm bg-zinc-800 led-transition";
          }
        }
        document.getElementById('heatIcon').setAttribute('class', 'w-5 h-5 stroke-white drop-shadow-[0_0_8px_rgba(255,255,255,0.8)] led-transition');
        document.getElementById('heatLabel').className = "text-[10px] sm:text-xs font-bold tracking-wider text-white uppercase";
      }
      // 3. BBQ / Grill Mode: Browning dark, Heat active
      else if (current.mode === 'bbq') {
        for (let i = 0; i < 6; i++) {
          document.getElementById(`shadeLed${i}`).className = "w-6 sm:w-8 h-1.5 rounded-sm bg-zinc-800 led-transition";
          document.getElementById(`shadeBox${i}`).style.opacity = "0.15";
          document.getElementById(`shadeBox${i}`).style.borderColor = "#27272a";
        }

        for (let i = 0; i < 4; i++) {
          if (i < current.heatLevel) {
            document.getElementById(`heatLed${i}`).className = "w-3.5 h-1.5 rounded-sm bg-red-500 glow-led-red led-transition";
          } else {
            document.getElementById(`heatLed${i}`).className = "w-3.5 h-1.5 rounded-sm bg-zinc-800 led-transition";
          }
        }
        document.getElementById('heatIcon').setAttribute('class', 'w-5 h-5 stroke-white drop-shadow-[0_0_8px_rgba(255,255,255,0.8)] led-transition');
        document.getElementById('heatLabel').className = "text-[10px] sm:text-xs font-bold tracking-wider text-white uppercase";
      }
    }

    // Initialize initial power off state on load
    window.onload = function() {
      render();
    };
  </script>
</body>
</html>
