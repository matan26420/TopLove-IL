<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>TopLove</title>
  <script src="https://cdn.tailwindcss.com"></script><style>
    body {
      background: radial-gradient(circle at top right, #3b0764, #0f172a 55%, #020617);
      color: #f8fafc;
      min-height: 100vh;
    }
    .glass {
      background: rgba(15, 23, 42, 0.72);
      backdrop-filter: blur(14px);
      border: 1px solid rgba(255, 255, 255, 0.12);
    }.bg-aurora { background: linear-gradient(135deg, #ec4899, #8b5cf6, #06b6d4); }
    .bg-sunset { background: linear-gradient(135deg, #f97316, #ec4899, #9333ea); }
    .bg-ocean { background: linear-gradient(135deg, #0284c7, #14b8a6, #2563eb); }
    .bg-gold { background: linear-gradient(135deg, #f59e0b, #eab308, #d97706); }
    .name-rainbow {
      background: linear-gradient(90deg, #f472b6, #c084fc, #38bdf8, #34d399);
      -webkit-background-clip: text;
      color: transparent;
    }
    .name-neon { color: #67e8f9; text-shadow: 0 0 10px rgba(103, 232, 249, 0.55); }
    .name-royal { color: #fde047; text-shadow: 0 0 8px rgba(250, 204, 21, 0.35); }
  </style>
</head><body class="antialiased selection:bg-pink-500 selection:text-white">
  <header class="sticky top-0 z-30 glass border-b border-white/10">
    <div class="max-w-7xl mx-auto px-4 py-3 flex flex-wrap items-center justify-between gap-3">
      <div class="flex items-center gap-3">
        <div class="w-10 h-10 rounded-2xl bg-aurora flex items-center justify-center text-xl font-black">💖</div>
        <div>
          <h1 class="text-lg font-extrabold">TopLove</h1>
          <p class="text-[11px] text-slate-300">קהילה, היכרויות ומשחקי לייב</p>
        </div>
      </div>
      <div class="flex items-center gap-2.5">
        <button id="user-profile-trigger" type="button" class="hidden items-center gap-2.5 px-3 py-1.5 rounded-2xl bg-slate-900/90 border border-white/15">
          <div id="header-avatar-slot" class="w-8 h-8 rounded-full bg-slate-800 flex items-center justify-center overflow-hidden text-sm">👤</div>
          <span id="user-badge" class="text-xs font-bold text-pink-200"></span>
        </button>
        <button id="logout-btn" type="button" class="hidden px-3 py-2 rounded-xl text-xs font-semibold bg-rose-600/80">יציאה</button>
      </div>
    </div>
  </header><main class="max-w-7xl mx-auto px-4 py-6">
    <section id="auth-section" class="max-w-md mx-auto glass rounded-3xl p-6 space-y-4">
      <div class="space-y-1 text-center">
        <h2 class="text-2xl font-extrabold">כניסה ל-TopLove</h2>
        <p class="text-xs text-slate-300">גילאי 18 עד 80 בלבד</p>
      </div>
      <p id="auth-error" class="hidden text-xs text-rose-300 bg-rose-950/60 border border-rose-500/40 rounded-xl p-2.5"></p>
      <form id="auth-form" class="space-y-3">
        <div>
          <label class="block text-xs text-slate-300 mb-1">אימייל</label>
          <input id="auth-email" type="email" required placeholder="name@example.com" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-950/80 border border-slate-700 text-sm" />
        </div>
        <div>
          <label class="block text-xs text-slate-300 mb-1">סיסמה</label>
          <div class="flex gap-2">
            <input id="auth-password" type="password" required minlength="6" placeholder="לפחות 6 תווים" class="flex-1 px-3.5 py-2.5 rounded-xl bg-slate-950/80 border border-slate-700 text-sm" />
            <button id="toggle-password-btn" type="button" class="px-3 rounded-xl bg-slate-800 border border-slate-700 text-xs">👁️</button>
          </div>
        </div><div class="grid grid-cols-2 gap-3">
          <div>
            <label class="block text-xs text-slate-300 mb-1">גיל (18–80)</label>
            <input id="auth-age" type="number" min="18" max="80" value="25" required class="w-full px-3.5 py-2.5 rounded-xl bg-slate-950/80 border border-slate-700 text-sm" />
          </div>
          <div>
            <label class="block text-xs text-slate-300 mb-1">מחפש/ת</label>
            <select id="auth-looking-for" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-950/80 border border-slate-700 text-sm">
              <option value="אישה">אישה</option>
              <option value="גבר">גבר</option>
              <option value="הכל">הכל</option>
            </select>
          </div>
        </div>
        <button type="submit" class="w-full py-3 rounded-xl font-bold text-sm bg-pink-600 hover:bg-pink-500">כניסה לאתר</button>
      </form>
    </section><section id="app-section" class="hidden space-y-6">
      <nav class="flex flex-wrap gap-2">
        <button type="button" data-tab="users" class="tab-btn px-5 py-2.5 rounded-xl text-sm font-semibold bg-pink-600 text-white">💘 הכרויות וגולשים</button>
        <button type="button" data-tab="chat" class="tab-btn px-5 py-2.5 rounded-xl text-sm font-semibold glass text-slate-300">💬 חדרי צ׳אט</button>
        <button type="button" data-tab="games" class="tab-btn px-5 py-2.5 rounded-xl text-sm font-semibold glass text-slate-300">🎮 משחקים ודירוג</button>
        <button type="button" data-tab="profile" class="tab-btn px-5 py-2.5 rounded-xl text-sm font-semibold glass text-slate-300">✨ הפרופיל שלי</button>
      </nav>

      <div id="tab-users" class="tab-content space-y-6">
        <div class="glass rounded-3xl p-5 space-y-4">
          <div class="flex flex-wrap items-center justify-between gap-2">
            <h2 class="text-lg font-extrabold">סינון ודפדוף פרופילים</h2>
            <span id="following-count-badge" class="text-xs px-3 py-1 rounded-full bg-indigo-500/20 border border-indigo-400/30 text-indigo-200">עוקב אחרי 0 משתמשים</span>
          </div><div class="grid grid-cols-2 sm:grid-cols-5 gap-3 text-xs">
            <select id="filter-looking-for" class="px-3 py-2 rounded-xl bg-slate-950 border border-slate-700">
              <option value="preferred">לפי ההעדפה שלי</option>
              <option value="all">הכל</option>
              <option value="אישה">אישה</option>
              <option value="גבר">גבר</option>
            </select>
            <select id="filter-distance" class="px-3 py-2 rounded-xl bg-slate-950 border border-slate-700">
              <option value="all">כל מרחק</option>
              <option value="10">עד 10 ק״מ</option>
              <option value="25">עד 25 ק״מ</option>
              <option value="50">עד 50 ק״מ</option>
              <option value="100">עד 100 ק״מ</option>
            </select>
            <input id="filter-location" type="text" placeholder="עיר / אזור / כל הארץ" class="px-3 py-2 rounded-xl bg-slate-950 border border-slate-700" />
            <input id="filter-min-age" type="number" min="18" max="80" value="18" class="px-3 py-2 rounded-xl bg-slate-950 border border-slate-700" />
            <input id="filter-max-age" type="number" min="18" max="80" value="80" class="px-3 py-2 rounded-xl bg-slate-950 border border-slate-700" />
          </div><div class="border-t border-white/10 pt-4 space-y-3">
            <div class="flex items-center justify-between text-xs text-slate-300">
              <span class="font-bold text-pink-300">כרטיס הכרות מהיר</span>
              <span id="match-deck-counter">0 פרופילים</span>
            </div>
            <div id="match-deck-card" class="p-4 rounded-2xl bg-slate-950/80 border border-slate-800"></div>
            <div class="flex flex-wrap gap-2">
              <button id="deck-skip-btn" type="button" class="px-4 py-2 rounded-xl text-xs font-bold bg-slate-800">⏭️ דלג</button>
              <button id="deck-like-btn" type="button" class="px-4 py-2 rounded-xl text-xs font-bold bg-pink-600">💖 לב והודעה</button>
              <button id="deck-follow-btn" type="button" class="px-4 py-2 rounded-xl text-xs font-bold bg-indigo-600">➕ עקוב</button>
            </div>
          </div>
        </div>
        <div id="real-users-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4"></div>
      </div><div id="tab-chat" class="tab-content hidden">
        <div class="grid grid-cols-1 lg:grid-cols-12 gap-5">
          <div class="lg:col-span-4 glass rounded-3xl p-4 space-y-4">
            <h2 class="text-base font-extrabold">חדרי שיחה</h2>
            <form id="create-room-form" class="space-y-2">
              <input id="new-room-topic" type="text" placeholder="נושא חדר חדש..." class="w-full px-3 py-2 rounded-xl bg-slate-950 border border-slate-700 text-xs" />
              <input id="new-room-code" type="text" placeholder="קוד לחדר פרטי" class="w-full px-3 py-2 rounded-xl bg-slate-950 border border-slate-700 text-xs" />
              <button type="submit" class="w-full py-2 rounded-xl bg-indigo-600 text-xs font-bold">+ פתח חדר</button>
            </form>
            <div id="rooms-list" class="space-y-2 max-h-96 overflow-y-auto"></div>
          </div>
          <div class="lg:col-span-8 glass rounded-3xl p-4 flex flex-col justify-between min-h-[500px] space-y-3">
            <div class="flex flex-wrap items-center justify-between gap-2 border-b border-white/10 pb-3">
              <div>
                <h3 id="active-room-title" class="font-extrabold text-base"></h3>
                <p id="active-room-meta" class="text-xs text-slate-400"></p>
              </div>
              <div class="flex gap-2">
                <button id="invite-friend-btn" type="button" class="px-3 py-1.5 rounded-xl bg-slate-800 text-xs font-semibold">📨 הזמן חבר</button>
                <button id="leave-room-btn" type="button" class="hidden px-3 py-1.5 rounded-xl bg-rose-600/80 text-xs font-semibold">יציאה</button>
              </div>
            </div>
            <div id="chat-messages" class="flex-1 space-y-2 max-h-96 overflow-y-auto"></div>
            <div class="space-y-2 border-t border-white/10 pt-3">
              <div class="flex items-center justify-between text-[11px] text-slate-400">
                <span id="voice-status"></span>
                <button id="record-voice-btn" type="button" class="px-3 py-1 rounded-lg bg-amber-600 text-white font-bold text-xs">🎤 הקלט</button>
              </div>
              <form id="chat-form" class="flex gap-2">
                <input id="chat-input" type="text" placeholder="כתוב הודעה..." class="flex-1 px-3.5 py-2.5 rounded-xl bg-slate-950 border border-slate-700 text-sm" />
                <button type="submit" class="px-5 py-2.5 rounded-xl bg-pink-600 text-sm font-bold">שלח</button>
              </form>
            </div>
          </div>
        </div>
      </div><div id="tab-games" class="tab-content hidden space-y-5">
        <div class="glass rounded-3xl p-4 space-y-4">
          <div class="flex flex-wrap items-center justify-between gap-2">
            <div>
              <div class="text-xs text-pink-300 font-bold" id="stat-game-name">איקס עיגול</div>
              <div class="text-xl font-extrabold"><span id="stat-game-level">רמה 1</span> • <span id="stat-game-points">0</span> נק׳</div>
            </div>
            <div class="flex gap-3 text-xs">
              <span class="px-3 py-1.5 rounded-xl bg-emerald-950/70 border border-emerald-500/30">ניצחונות: <strong id="stat-game-wins">0</strong></span>
              <span class="px-3 py-1.5 rounded-xl bg-rose-950/70 border border-rose-500/30">הפסדים: <strong id="stat-game-losses">0</strong></span>
              <span id="top100-count-badge" class="px-3 py-1.5 rounded-xl bg-slate-900 border border-slate-700">0 / 100</span>
            </div>
          </div>
          <div>
            <div id="top5-title" class="text-xs font-bold text-amber-300 mb-2"></div>
            <div id="top5-board" class="grid grid-cols-1 sm:grid-cols-5 gap-2 text-xs"></div>
          </div>
          <div class="flex flex-wrap gap-2">
            <button type="button" data-game="ttt" class="game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold bg-pink-600">❌⭕ איקס עיגול</button>
            <button type="button" data-game="rps" class="game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold glass text-slate-300">✂️ אבן נייר מספריים</button>
            <button type="button" data-game="memory" class="game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold glass text-slate-300">🧠 זיכרון</button>
            <button type="button" data-game="number" class="game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold glass text-slate-300">🎯 ניחוש מספר</button>
            <button type="button" data-game="roulette" class="game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold glass text-slate-300">🎰 רולטה רוסית</button>
          </div>
        </div><div id="game-ttt" class="game-panel glass rounded-3xl p-5 space-y-4">
          <div class="flex flex-wrap items-center justify-between gap-2">
            <h3 class="font-extrabold">איקס עיגול</h3>
            <div class="flex items-center gap-2 text-xs">
              <span id="ttt-timer" class="px-2.5 py-1 rounded-lg bg-slate-900 border border-slate-700">⏱️ 00:30</span>
              <button id="ttt-pick-x" type="button" class="px-3 py-1 rounded-lg bg-amber-600 font-bold">❌</button>
              <button id="ttt-pick-o" type="button" class="px-3 py-1 rounded-lg bg-slate-800 border border-slate-600 font-bold">⭕</button>
              <button id="ttt-join-room" type="button" class="px-3 py-1.5 rounded-lg bg-emerald-600 font-bold">כנס</button>
              <button id="ttt-leave-room" type="button" class="hidden px-3 py-1.5 rounded-lg bg-rose-600 font-bold">צא</button>
              <button id="ttt-reset" type="button" class="px-3 py-1.5 rounded-lg bg-slate-800 font-bold">אפס</button>
              <button id="ttt-add-room" type="button" class="px-3 py-1.5 rounded-lg bg-indigo-600 font-bold">+ שולחן</button>
            </div>
          </div>
          <div id="ttt-status" class="text-xs text-pink-200 font-semibold"></div>
          <div class="grid grid-cols-1 lg:grid-cols-12 gap-4">
            <div class="lg:col-span-5 space-y-3">
              <div class="flex justify-between text-xs p-2.5 rounded-xl bg-slate-900/80 border border-slate-800">
                <span><span id="ttt-p1-sym-icon">❌</span> <strong id="ttt-p1-name"></strong></span>
                <span><span id="ttt-p2-sym-icon">⭕</span> <strong id="ttt-p2-name"></strong></span>
              </div>
              <div id="ttt-board" class="grid grid-cols-3 gap-2 max-w-xs mx-auto"></div>
            </div>
            <div class="lg:col-span-7 space-y-3">
              <div id="ttt-rooms-grid" class="grid grid-cols-3 sm:grid-cols-5 gap-1.5 max-h-44 overflow-y-auto"></div>
              <div id="ttt-room-chat-log" class="space-y-1.5 max-h-32 overflow-y-auto text-xs"></div>
              <form id="ttt-room-chat-form" class="flex gap-2">
                <input id="ttt-room-chat-input" type="text" placeholder="הודעה לשולחן..." class="flex-1 px-3 py-2 rounded-xl bg-slate-950 border border-slate-700 text-xs" />
                <button type="button" data-voice-target="ttt" class="room-voice-btn px-3 py-2 rounded-xl bg-amber-600 text-xs font-bold">🎤</button>
                <button type="submit" class="px-4 py-2 rounded-xl bg-pink-600 text-xs font-bold">שלח</button>
              </form>
            </div>
          </div>
        </div><div id="game-rps" class="game-panel hidden glass rounded-3xl p-5 space-y-4">
          <div class="flex flex-wrap items-center justify-between gap-2">
            <h3 class="font-extrabold">אבן נייר מספריים</h3>
            <div class="flex items-center gap-2 text-xs">
              <span id="rps-timer" class="px-2.5 py-1 rounded-lg bg-slate-900 border border-slate-700">⏱️ 00:15</span>
              <button id="rps-join-room" type="button" class="px-3 py-1.5 rounded-lg bg-emerald-600 font-bold">כנס</button>
              <button id="rps-leave-room" type="button" class="hidden px-3 py-1.5 rounded-lg bg-rose-600 font-bold">צא</button>
              <button id="rps-add-room" type="button" class="px-3 py-1.5 rounded-lg bg-indigo-600 font-bold">+ שולחן</button>
            </div>
          </div>
          <div class="grid grid-cols-3 items-center text-center p-4 rounded-2xl bg-slate-950/70 border border-slate-800">
            <div class="space-y-1">
              <div id="rps-left-avatar" class="text-2xl">🪑</div>
              <div id="rps-left-name" class="text-xs font-bold"></div>
              <div id="rps-left-sign" class="text-4xl">✊</div>
            </div>
            <div class="space-y-1">
              <div id="rps-round-phase" class="text-xs text-pink-300 font-bold"></div>
              <div id="rps-count-num" class="text-3xl font-black text-amber-300">-</div>
              <div id="rps-result" class="text-xs text-slate-200"></div>
            </div>
            <div class="space-y-1">
              <div id="rps-right-avatar" class="text-2xl">🪑</div>
              <div id="rps-right-name" class="text-xs font-bold"></div>
              <div id="rps-right-sign" class="text-4xl">✊</div>
            </div>
          </div>
          <div class="flex justify-center gap-3">
            <button type="button" data-rps="rock" class="rps-choice px-4 py-2.5 rounded-xl bg-slate-800 text-sm font-bold">🪨 אבן</button>
            <button type="button" data-rps="paper" class="rps-choice px-4 py-2.5 rounded-xl bg-slate-800 text-sm font-bold">📄 נייר</button>
            <button type="button" data-rps="scissors" class="rps-choice px-4 py-2.5 rounded-xl bg-slate-800 text-sm font-bold">✂️ מספריים</button>
          </div>
          <div id="rps-rooms-grid" class="grid grid-cols-3 sm:grid-cols-6 gap-1.5 max-h-36 overflow-y-auto"></div>
          <div id="rps-room-chat-log" class="space-y-1.5 max-h-28 overflow-y-auto text-xs"></div>
          <form id="rps-room-chat-form" class="flex gap-2">
            <input id="rps-room-chat-input" type="text" placeholder="הודעה לשולחן..." class="flex-1 px-3 py-2 rounded-xl bg-slate-950 border border-slate-700 text-xs" />
            <button type="button" data-voice-target="rps" class="room-voice-btn px-3 py-2 rounded-xl bg-amber-600 text-xs font-bold">🎤</button>
            <button type="submit" class="px-4 py-2 rounded-xl bg-pink-600 text-xs font-bold">שלח</button>
          </form>
        </div><div id="game-memory" class="game-panel hidden glass rounded-3xl p-5 space-y-4">
          <div class="flex flex-wrap items-center justify-between gap-2">
            <h3 class="font-extrabold">משחק זיכרון</h3>
            <div class="flex items-center gap-2 text-xs">
              <span id="memory-timer" class="px-2.5 py-1 rounded-lg bg-slate-900 border border-slate-700">⏱️ 03:00</span>
              <button id="memory-join-room" type="button" class="px-3 py-1.5 rounded-lg bg-emerald-600 font-bold">הצטרף</button>
              <button id="memory-leave-room" type="button" class="hidden px-3 py-1.5 rounded-lg bg-rose-600 font-bold">צא</button>
              <button id="memory-reset" type="button" class="px-3 py-1.5 rounded-lg bg-slate-800 font-bold">ערבב</button>
            </div>
          </div>
          <div id="memory-status" class="text-xs text-pink-200 font-semibold"></div>
          <div id="memory-rooms-grid" class="grid grid-cols-2 sm:grid-cols-4 gap-2"></div>
          <form id="mem-create-room-form" class="flex flex-wrap gap-2">
            <input id="mem-room-name" type="text" placeholder="שם חדר זיכרון..." class="flex-1 px-3 py-2 rounded-xl bg-slate-950 border border-slate-700 text-xs" />
            <select id="mem-room-mode" class="px-3 py-2 rounded-xl bg-slate-950 border border-slate-700 text-xs">
              <option value="8x8">8×8</option>
              <option value="10x10">10×10</option>
              <option value="30x30">30×30</option>
            </select>
            <button type="submit" class="px-4 py-2 rounded-xl bg-indigo-600 text-xs font-bold">+ חדר</button>
          </form>
          <div id="memory-players-board" class="grid grid-cols-2 sm:grid-cols-6 gap-2 text-xs"></div>
          <div class="overflow-x-auto pb-2"><div id="memory-grid" class="grid gap-1.5"></div></div>
          <div id="mem-room-chat-log" class="space-y-1.5 max-h-28 overflow-y-auto text-xs"></div>
          <form id="mem-room-chat-form" class="flex gap-2">
            <input id="mem-room-chat-input" type="text" placeholder="הודעה לחדר..." class="flex-1 px-3 py-2 rounded-xl bg-slate-950 border border-slate-700 text-xs" />
            <button type="button" data-voice-target="mem" class="room-voice-btn px-3 py-2 rounded-xl bg-amber-600 text-xs font-bold">🎤</button>
            <button type="submit" class="px-4 py-2 rounded-xl bg-pink-600 text-xs font-bold">שלח</button>
          </form>
        </div><div id="game-number" class="game-panel hidden glass rounded-3xl p-5 space-y-4">
          <div class="flex flex-wrap items-center justify-between gap-2">
            <h3 id="num-room-header" class="font-extrabold">ניחוש מספר</h3>
            <div class="flex items-center gap-2 text-xs">
              <span id="num-room-cap" class="px-2.5 py-1 rounded-lg bg-slate-900 border border-slate-700">0 / 50</span>
              <button id="num-join-room" type="button" class="px-3 py-1.5 rounded-lg bg-emerald-600 font-bold">הצטרף</button>
              <button id="num-leave-room" type="button" class="hidden px-3 py-1.5 rounded-lg bg-rose-600 font-bold">צא</button>
            </div>
          </div>
          <div id="num-rooms-list" class="grid grid-cols-1 sm:grid-cols-3 gap-2"></div>
          <form id="num-create-room-form" class="flex flex-wrap gap-2">
            <input id="num-room-name" type="text" placeholder="שם חדר ניחושים..." class="flex-1 px-3 py-2 rounded-xl bg-slate-950 border border-slate-700 text-xs" />
            <input id="num-room-max" type="number" min="10" value="1000" class="w-28 px-3 py-2 rounded-xl bg-slate-950 border border-slate-700 text-xs" />
            <button type="submit" class="px-4 py-2 rounded-xl bg-indigo-600 text-xs font-bold">+ חדר</button>
          </form>
          <div class="grid grid-cols-1 md:grid-cols-2 gap-3 p-3 rounded-2xl bg-slate-950/70 border border-slate-800 text-xs">
            <div class="space-y-2">
              <div id="num-secret-status" class="text-amber-300 font-semibold"></div>
              <div class="flex gap-2">
                <input id="num-secret-input" type="password" placeholder="מספר סודי" class="flex-1 px-3 py-2 rounded-xl bg-slate-900 border border-slate-700" />
                <button id="num-toggle-secret" type="button" class="px-3 rounded-xl bg-slate-800">👁️</button>
                <button id="num-set-secret-btn" type="button" class="px-3 rounded-xl bg-amber-600 font-bold">קבע</button>
              </div>
            </div>
            <div class="space-y-2">
              <div class="flex gap-2">
                <input id="num-guess-input" type="number" placeholder="ניחוש..." class="flex-1 px-3 py-2 rounded-xl bg-slate-900 border border-slate-700" />
                <button id="num-guess-btn" type="button" class="px-4 rounded-xl bg-pink-600 font-bold">שלח</button>
                <button id="num-declare-winner-btn" type="button" class="px-3 rounded-xl bg-emerald-600 font-bold">חשב נקודות</button>
              </div>
              <div id="num-guess-feedback" class="text-pink-200"></div>
            </div>
          </div>
          <div id="num-guesses-log" class="space-y-1.5 max-h-40 overflow-y-auto text-xs"></div>
          <div id="num-room-chat-log" class="space-y-1.5 max-h-28 overflow-y-auto text-xs"></div>
          <form id="num-room-chat-form" class="flex gap-2">
            <input id="num-room-chat-input" type="text" placeholder="הודעה לחדר..." class="flex-1 px-3 py-2 rounded-xl bg-slate-950 border border-slate-700 text-xs" />
            <button type="button" data-voice-target="num" class="room-voice-btn px-3 py-2 rounded-xl bg-amber-600 text-xs font-bold">🎤</button>
            <button type="submit" class="px-4 py-2 rounded-xl bg-pink-600 text-xs font-bold">שלח</button>
          </form>
        </div><div id="game-roulette" class="game-panel hidden glass rounded-3xl p-5 space-y-4">
          <div class="flex flex-wrap items-center justify-between gap-2">
            <h3 class="font-extrabold">רולטה רוסית</h3>
            <div class="flex items-center gap-2 text-xs">
              <button id="rr-join-btn" type="button" class="px-3 py-1.5 rounded-lg bg-emerald-600 font-bold">הצטרף</button>
              <button id="rr-leave-btn" type="button" class="hidden px-3 py-1.5 rounded-lg bg-rose-600 font-bold">צא</button>
              <button id="rr-add-room" type="button" class="px-3 py-1.5 rounded-lg bg-indigo-600 font-bold">+ חדר</button>
            </div>
          </div>
          <div class="grid grid-cols-2 sm:grid-cols-4 gap-2 text-xs">
            <div class="p-2.5 rounded-xl bg-slate-900 border border-slate-800">🟡 כדורי זהב: <strong id="rr-gold-balls">0</strong></div>
            <div class="p-2.5 rounded-xl bg-slate-900 border border-slate-800">📦 מחסניות: <strong id="rr-magazines">0</strong></div>
            <div class="p-2.5 rounded-xl bg-slate-900 border border-slate-800">🔫 אקדחים: <strong id="rr-pistols">0</strong></div>
            <div class="p-2.5 rounded-xl bg-slate-900 border border-slate-800">🎁 פרסי על: <strong id="rr-grand-gifts">0</strong></div>
          </div>
          <div id="rr-confetti-banner" class="hidden p-3 rounded-2xl bg-amber-500/20 border border-amber-400 text-center text-xs font-extrabold text-amber-200">🎊 בום קונפטי! 🎊</div>
          <div class="flex items-center justify-between gap-3 p-3 rounded-2xl bg-slate-950/70 border border-slate-800 text-xs">
            <span id="rr-aimed-label" class="font-bold text-amber-300"></span>
            <div id="rr-gun-spinner" class="text-2xl transition-transform duration-500">🔫</div>
          </div>
          <div id="rr-status" class="text-xs text-pink-200 font-semibold"></div>
          <div id="rr-seats-ring" class="grid grid-cols-2 sm:grid-cols-3 gap-2"></div>
          <div id="rr-rooms-grid" class="grid grid-cols-4 sm:grid-cols-10 gap-1.5 max-h-36 overflow-y-auto"></div>
          <div id="rr-room-chat-log" class="space-y-1.5 max-h-28 overflow-y-auto text-xs"></div>
          <form id="rr-room-chat-form" class="flex gap-2">
            <input id="rr-room-chat-input" type="text" placeholder="הודעה לחדר..." class="flex-1 px-3 py-2 rounded-xl bg-slate-950 border border-slate-700 text-xs" />
            <button type="button" data-voice-target="rr" class="room-voice-btn px-3 py-2 rounded-xl bg-amber-600 text-xs font-bold">🎤</button>
            <button type="submit" class="px-4 py-2 rounded-xl bg-pink-600 text-xs font-bold">שלח</button>
          </form>
        </div>
      </div><div id="tab-profile" class="tab-content hidden space-y-5">
        <div class="glass rounded-3xl p-4 flex flex-wrap items-center justify-between gap-3">
          <div class="flex items-center gap-3">
            <span id="profile-completion-badge" class="text-xs font-bold px-3 py-1.5 rounded-full bg-pink-500/20 border border-pink-400/30 text-pink-200">✨ השלמת פרופיל: 0%</span>
            <span id="save-feedback" class="opacity-0 transition-opacity text-xs text-emerald-300 font-bold">✓ נשמר</span>
          </div>
          <button id="edit-profile-btn" type="button" class="hidden px-4 py-2 rounded-xl bg-indigo-600 text-xs font-bold">✏️ ערוך פרופיל</button>
        </div>
        <div id="profile-summary-card" class="hidden glass rounded-3xl overflow-hidden space-y-4">
          <div id="summary-banner" class="h-36 bg-aurora p-5 flex items-start justify-between">
            <span id="summary-level-badge" class="px-3 py-1 rounded-full bg-slate-950/70 text-xs font-bold"></span>
            <span id="summary-likes-badge" class="px-3 py-1 rounded-full bg-slate-950/70 text-xs font-bold"></span>
          </div>
          <div class="px-5 pb-5 space-y-4">
            <div class="flex flex-wrap items-end justify-between gap-4 -mt-12">
              <div class="flex items-end gap-3">
                <img id="summary-avatar" src="" alt="" class="hidden w-24 h-24 rounded-2xl object-cover border-4 border-slate-900 bg-slate-800 cursor-pointer" />
                <div class="space-y-1">
                  <div class="flex items-center gap-2">
                    <h2 id="summary-name" class="text-2xl font-extrabold"></h2>
                    <span id="summary-nickname-pill" class="hidden px-2.5 py-0.5 rounded-full bg-slate-800 text-xs"></span>
                  </div>
                  <p id="summary-tagline" class="text-xs text-pink-200"></p>
                  <p id="summary-age-gender-loc" class="text-xs text-slate-300"></p>
                </div>
              </div>
              <div id="summary-photo-nav" class="hidden gap-2">
                <button id="summary-prev-photo" type="button" class="px-3 py-1.5 rounded-xl bg-slate-800 text-xs">◀</button>
                <button id="summary-next-photo" type="button" class="px-3 py-1.5 rounded-xl bg-slate-800 text-xs">▶</button>
              </div>
            </div>
            <div id="summary-photos-strip" class="flex gap-2 overflow-x-auto"></div>
            <div id="summary-quick-pills" class="flex flex-wrap gap-2 text-xs"></div>
            <p id="summary-bio" class="text-sm text-slate-200 bg-slate-950/60 p-3.5 rounded-2xl border border-white/10"></p>
            <div class="grid grid-cols-1 md:grid-cols-3 gap-3 text-xs">
              <div id="summary-col-dating" class="p-3 rounded-2xl bg-slate-950/60 border border-slate-800 space-y-1"></div>
              <div id="summary-col-lifestyle" class="p-3 rounded-2xl bg-slate-950/60 border border-slate-800 space-y-1"></div>
              <div id="summary-col-pets" class="p-3 rounded-2xl bg-slate-950/60 border border-slate-800 space-y-1"></div>
              <div id="summary-col-trips" class="p-3 rounded-2xl bg-slate-950/60 border border-slate-800 flex flex-wrap gap-1.5"></div>
              <div id="summary-col-night" class="p-3 rounded-2xl bg-slate-950/60 border border-slate-800 space-y-1"></div>
              <div id="summary-col-extra" class="p-3 rounded-2xl bg-slate-950/60 border border-slate-800 flex flex-wrap gap-1.5"></div>
            </div>
          </div>
        </div><form id="profile-form" class="glass rounded-3xl p-6 space-y-5">
          <p id="profile-error" class="hidden text-xs text-rose-300 bg-rose-950/60 border border-rose-500/40 rounded-xl p-2.5"></p>
          <div class="flex flex-wrap items-center gap-4">
            <div id="prof-avatar-frame" class="p-2 rounded-3xl bg-aurora shrink-0">
              <div id="prof-avatar-placeholder" class="w-20 h-20 rounded-2xl bg-slate-900 flex items-center justify-center text-3xl">👤</div>
              <img id="prof-avatar-preview" src="" alt="" class="hidden w-20 h-20 rounded-2xl object-cover" />
            </div>
            <div class="space-y-2 flex-1 min-w-[200px]">
              <label class="block text-xs text-slate-300">תמונות מהמכשיר</label>
              <input id="prof-avatar-file" type="file" accept="image/*" multiple class="text-xs text-slate-300" />
              <div id="prof-photos-thumbs" class="flex flex-wrap gap-2"></div>
            </div>
          </div>
          <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-3 text-xs">
            <input id="prof-name" type="text" placeholder="שם מלא" class="px-3 py-2.5 rounded-xl bg-slate-950 border border-slate-700" />
            <input id="prof-nickname" type="text" placeholder="כינוי" class="px-3 py-2.5 rounded-xl bg-slate-950 border border-slate-700" />
            <select id="prof-gender" class="px-3 py-2.5 rounded-xl bg-slate-950 border border-slate-700">
              <option value="">מין</option>
              <option value="אישה">אישה</option>
              <option value="גבר">גבר</option>
            </select>
            <select id="prof-looking-for" class="px-3 py-2.5 rounded-xl bg-slate-950 border border-slate-700">
              <option value="אישה">מחפש/ת אישה</option>
              <option value="גבר">מחפש/ת גבר</option>
              <option value="הכל">מחפש/ת הכל</option>
            </select>
            <input id="prof-age" type="number" min="18" max="80" placeholder="גיל" class="px-3 py-2.5 rounded-xl bg-slate-950 border border-slate-700" />
            <input id="prof-location" type="text" placeholder="עיר / אזור" class="px-3 py-2.5 rounded-xl bg-slate-950 border border-slate-700" />
            <input id="prof-distance" type="number" min="0" max="500" placeholder="מרחק (ק״מ)" class="px-3 py-2.5 rounded-xl bg-slate-950 border border-slate-700" />
            <input id="prof-goal" type="text" placeholder="מטרת היכרות" class="px-3 py-2.5 rounded-xl bg-slate-950 border border-slate-700" />
            <input id="prof-marital" type="text" placeholder="מצב משפחתי" class="px-3 py-2.5 rounded-xl bg-slate-950 border border-slate-700" />
          </div><div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-3 text-xs">
            <input id="prof-children" type="text" placeholder="ילדים" class="px-3 py-2.5 rounded-xl bg-slate-950 border border-slate-700" />
            <input id="prof-height" type="text" placeholder="גובה (ס״מ)" class="px-3 py-2.5 rounded-xl bg-slate-950 border border-slate-700" />
            <input id="prof-job" type="text" placeholder="עיסוק" class="px-3 py-2.5 rounded-xl bg-slate-950 border border-slate-700" />
            <input id="prof-zodiac" type="text" placeholder="מזל" class="px-3 py-2.5 rounded-xl bg-slate-950 border border-slate-700" />
            <input id="prof-smoking" type="text" placeholder="עישון" class="px-3 py-2.5 rounded-xl bg-slate-950 border border-slate-700" />
            <input id="prof-alcohol" type="text" placeholder="אלכוהול" class="px-3 py-2.5 rounded-xl bg-slate-950 border border-slate-700" />
            <input id="prof-education" type="text" placeholder="השכלה" class="px-3 py-2.5 rounded-xl bg-slate-950 border border-slate-700" />
            <input id="prof-has-pets" type="text" placeholder="חיות מחמד" class="px-3 py-2.5 rounded-xl bg-slate-950 border border-slate-700" />
            <select id="prof-fav-pet" class="px-3 py-2.5 rounded-xl bg-slate-950 border border-slate-700">
              <option value="">חית מחמד מועדפת</option>
              <option value="כלב">כלב</option>
              <option value="חתול">חתול</option>
              <option value="אחר">אחר</option>
            </select>
          </div><div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-3 text-xs">
            <input id="prof-pet-name" type="text" placeholder="שם חיית המחמד" class="px-3 py-2.5 rounded-xl bg-slate-950 border border-slate-700" />
            <div id="prof-other-pet-wrap" class="hidden">
              <input id="prof-other-pet-text" type="text" placeholder="פרט חיית מחמד אחרת..." class="w-full px-3 py-2.5 rounded-xl bg-slate-950 border border-slate-700" />
            </div>
            <input id="prof-first-date" type="text" placeholder="דייט ראשון" class="px-3 py-2.5 rounded-xl bg-slate-950 border border-slate-700" />
            <input id="prof-tagline" type="text" placeholder="משפט פתיחה" class="px-3 py-2.5 rounded-xl bg-slate-950 border border-slate-700" />
            <select id="prof-banner" class="px-3 py-2.5 rounded-xl bg-slate-950 border border-slate-700">
              <option value="bg-aurora">רקע אורורה</option>
              <option value="bg-sunset">רקע שקיעה</option>
              <option value="bg-ocean">רקע אוקיינוס</option>
              <option value="bg-gold">רקע זהב</option>
            </select>
          </div>
          <div class="flex flex-wrap gap-2 text-xs">
            <button type="button" data-style="name-rainbow" class="style-pick-btn px-3 py-1.5 rounded-xl bg-slate-900 border border-pink-400 font-bold name-rainbow">קשת</button>
            <button type="button" data-style="name-neon" class="style-pick-btn px-3 py-1.5 rounded-xl bg-slate-900 border border-slate-700 font-bold name-neon">ניאון</button>
            <button type="button" data-style="name-royal" class="style-pick-btn px-3 py-1.5 rounded-xl bg-slate-900 border border-slate-700 font-bold name-royal">מלכותי</button>
          </div>
          <textarea id="prof-bio" rows="3" placeholder="ספר/י על עצמך..." class="w-full px-3.5 py-2.5 rounded-xl bg-slate-950 border border-slate-700 text-xs"></textarea>
          <div class="space-y-2 text-xs">
            <div class="font-bold text-emerald-300">טיולים</div>
            <div id="trips-options" class="flex flex-wrap gap-1.5"></div>
            <div class="font-bold text-purple-300">בילוי לילי</div>
            <div id="night-options" class="flex flex-wrap gap-1.5"></div>
            <div class="font-bold text-indigo-300">תחביבים</div>
            <div id="hobbies-options" class="flex flex-wrap gap-1.5"></div>
          </div>
          <button type="submit" class="px-6 py-3 rounded-xl bg-pink-600 text-sm font-extrabold">שמור פרופיל</button>
        </form>
      </div>
    </section>
  </main><div id="user-modal" class="hidden fixed inset-0 z-50 bg-black/75 flex items-center justify-center p-4">
    <div class="glass rounded-3xl max-w-lg w-full max-h-[90vh] overflow-y-auto space-y-4">
      <div id="modal-banner" class="h-32 bg-aurora relative p-4 flex justify-between items-start">
        <span id="modal-level-badge" class="px-3 py-1 rounded-full bg-slate-950/75 text-xs font-bold"></span>
        <button id="close-modal-btn" type="button" class="w-8 h-8 rounded-full bg-slate-950/80 text-white text-xs font-bold">✕</button>
      </div>
      <div class="px-5 pb-5 space-y-3">
        <h3 id="modal-name" class="text-2xl font-extrabold"></h3>
        <p id="modal-tagline" class="text-xs text-pink-200"></p>
        <p id="modal-meta" class="text-xs text-slate-300"></p>
        <img id="modal-main-photo" src="" alt="" class="hidden w-full h-56 object-cover rounded-2xl border border-white/15" />
        <div class="flex items-center justify-between gap-2">
          <button id="modal-prev-photo" type="button" class="px-3 py-1 rounded-lg bg-slate-800 text-xs">◀</button>
          <div id="modal-gallery" class="flex gap-2 overflow-x-auto"></div>
          <button id="modal-next-photo" type="button" class="px-3 py-1 rounded-lg bg-slate-800 text-xs">▶</button>
        </div>
        <div class="text-xs space-y-1 text-slate-200">
          <div id="modal-looking-for"></div>
          <div id="modal-relationship-goal"></div>
          <div id="modal-lifestyle"></div>
          <div id="modal-habits"></div>
          <div id="modal-pets-info"></div>
          <div id="modal-night-info"></div>
          <div id="modal-education"></div>
        </div>
        <p id="modal-bio" class="text-xs text-slate-300 bg-slate-950/60 p-3 rounded-xl"></p>
        <div id="modal-tags" class="flex flex-wrap gap-1.5 text-xs"></div>
        <p id="modal-action-msg" class="text-xs text-emerald-300 font-semibold"></p>
        <div class="flex flex-wrap gap-2">
          <button id="modal-like-btn" type="button" class="px-3 py-2 rounded-xl bg-slate-800 text-xs font-bold">👍 לייק</button>
          <button id="modal-heart-btn" type="button" class="px-3 py-2 rounded-xl bg-pink-600 text-xs font-bold">💖 לב</button>
          <button id="modal-follow-btn" type="button" class="px-3 py-2 rounded-xl bg-indigo-600 text-xs font-bold">➕ עקוב</button>
          <button id="modal-dm-btn" type="button" class="px-3 py-2 rounded-xl bg-emerald-600 text-xs font-bold">💬 הודעה</button>
        </div>
      </div>
    </div>
  </div><script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-app.js";
    import { getAuth, signInWithEmailAndPassword, createUserWithEmailAndPassword, signOut, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-auth.js";
    import { getFirestore, collection, doc, setDoc, addDoc, query, orderBy, onSnapshot, serverTimestamp } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-firestore.js";

    const firebaseConfig = {
      apiKey: "YOUR_API_KEY",
      authDomain: "YOUR_PROJECT.firebaseapp.com",
      projectId: "YOUR_PROJECT_ID",
      storageBucket: "YOUR_PROJECT.appspot.com",
      messagingSenderId: "YOUR_SENDER_ID",
      appId: "YOUR_APP_ID"
    };const hasRealFirebaseConfig = Boolean(firebaseConfig.apiKey && !firebaseConfig.apiKey.startsWith("YOUR_"));
    const fbApp = hasRealFirebaseConfig ? initializeApp(firebaseConfig) : null;
    const auth = fbApp ? getAuth(fbApp) : null;
    const db = fbApp ? getFirestore(fbApp) : null;

    const $ = (id) => document.getElementById(id);
    const MAX_ROOM_USERS = 50;

    function escapeHtml(val) {
      return String(val ?? "")
        .replace(/&/g, "&amp;")
        .replace(/</g, "&lt;")
        .replace(/>/g, "&gt;")
        .replace(/"/g, "&quot;")
        .replace(/'/g, "&#39;");
    }

    function safeUrl(url) {
      const s = String(url ?? "").trim();
      if (s.startsWith("data:image/") || s.startsWith("data:audio/") || s.startsWith("https://") || s.startsWith("http://")) return s;
      return "";
    }const gameNames = {
      ttt: "איקס עיגול",
      rps: "אבן נייר מספריים",
      memory: "משחק זיכרון",
      number: "ניחוש מספר",
      roulette: "רולטה רוסית"
    };
    const tripsChoices = ["ים המלח", "אילת", "צפון וגולן", "ירושלים", "טבע ומסלולים", "חו״ל"];
    const nightChoices = ["בר / פאב", "הופעה חיה", "קולנוע", "ארוחת ערב", "ישיבה בבית", "ריקודים"];
    const hobbiesChoices = ["מוזיקה", "בישול", "קריאה", "כושר", "צילום", "טיולים", "משחקים", "קפה"];
    const gameLeaderboards = { ttt: [], rps: [], memory: [], number: [], roulette: [] };
    const sampleCandidates = [
      { uid: "cand-noa", name: "נועה", gender: "אישה", lookingFor: "גבר", age: 26, location: "תל אביב", distanceKm: 5, tagline: "אוהבת שמש וקפה", banner: "bg-sunset", nameStyle: "name-rainbow", bio: "מחפשת חיבור אמיתי.", gameStats: { ttt: { points: 45, wins: 2, losses: 1, played: 3 } } },
      { uid: "cand-daniel", name: "דניאל", gender: "גבר", lookingFor: "אישה", age: 29, location: "חיפה", distanceKm: 18, tagline: "מוזיקה וריצה", banner: "bg-ocean", nameStyle: "name-neon", bio: "שיחות טובות.", gameStats: { rps: { points: 60, wins: 3, losses: 0, played: 3 } } }
    ];let me = {
      uid: "", email: "", name: "", nickname: "", gender: "", lookingFor: "אישה",
      age: 18, location: "", distanceKm: 15, goal: "", marital: "", children: "",
      height: "", job: "", smoking: "", alcohol: "", education: "", zodiac: "",
      hasPets: "", favPet: "", petName: "", otherPetText: "", firstDate: "",
      tagline: "", banner: "bg-aurora", nameStyle: "name-rainbow", bio: "",
      trips: [], nightActivities: [], hobbies: [], photos: [], following: [],
      avatar: "", hasCustomPhoto: false, profileCompleted: false,
      rrRewards: { goldBalls: 0, magazines: 0, pistols: 0, grandGifts: 0 },
      gameStats: {
        ttt: { points: 0, wins: 0, losses: 0, played: 0 },
        rps: { points: 0, wins: 0, losses: 0, played: 0 },
        memory: { points: 0, wins: 0, losses: 0, played: 0 },
        number: { points: 0, wins: 0, losses: 0, played: 0 },
        roulette: { points: 0, wins: 0, losses: 0, played: 0 }
      }
    };
    let currentGameKey = "ttt", allUsers = [], deckIdx = 0, summaryPhotoIdx = 0;

    function getLevel(pts) { return Math.max(1, Math.floor((Number(pts) || 0) / 50) + 1); }
    function getRewardLabel(gameKey, i) { return i === 0 ? "🥇 מקום 1" : i === 1 ? "🥈 מקום 2" : i === 2 ? "🥉 מקום 3" : "🎖️ טופ-100"; }function upsertPlayerBoard(gameKey, name, st) {
      if (!gameLeaderboards[gameKey]) gameLeaderboards[gameKey] = [];
      const points = Number(st?.points) || 0;
      if ((Number(st?.played) || 0) < 1) return;
      const cleanName = escapeHtml(name || "שחקן");
      const idx = gameLeaderboards[gameKey].findIndex((x) => x.name === cleanName);
      const item = { name: cleanName, points, level: getLevel(points) };
      if (idx >= 0) gameLeaderboards[gameKey][idx] = item; else gameLeaderboards[gameKey].push(item);
      gameLeaderboards[gameKey].sort((a, b) => b.points - a.points);
      gameLeaderboards[gameKey] = gameLeaderboards[gameKey].slice(0, 100);
    }

    function renderGameStatsAndTop5(gameKey = currentGameKey) {
      currentGameKey = gameKey;
      const st = me.gameStats[gameKey] || { points: 0, wins: 0, losses: 0, played: 0 };
      upsertPlayerBoard(gameKey, me.name || "שחקן", st);
      $("stat-game-level").textContent = `רמה ${getLevel(st.points)}`;
      $("stat-game-name").textContent = gameNames[gameKey];
      $("stat-game-points").textContent = String(st.points);
      $("stat-game-wins").textContent = String(st.wins);
      $("stat-game-losses").textContent = String(st.losses);
      const list = gameLeaderboards[gameKey] || [];
      $("top100-count-badge").textContent = `${list.length} / 100`;
      $("top5-title").textContent = `🏅 טופ-5 ב${gameNames[gameKey]}`;
      $("top5-board").innerHTML = list.length ? list.slice(0, 5).map((p, i) => `<div class="p-2.5 rounded-xl bg-slate-900 border border-slate-800"><div class="font-bold truncate">${i + 1}. ${escapeHtml(p.name)}</div><div class="text-pink-300">רמה ${p.level} • ${p.points} נק׳</div><div class="text-[11px] text-amber-300">${escapeHtml(getRewardLabel(gameKey, i))}</div></div>`).join("") : `<p class="text-slate-400 col-span-full">שחק משחק אחד לפחות כדי להיכנס לדירוג.</p>`;
      if (me.uid) localStorage.setItem("toplove_session", JSON.stringify(me));
    }

    async function awardGameWin(gameKey, pts) {
      me.gameStats[gameKey].played += 1; me.gameStats[gameKey].wins += 1; me.gameStats[gameKey].points += pts;
      renderGameStatsAndTop5(gameKey);
      try { if (db && me.uid) await setDoc(doc(db, "users", me.uid), { gameStats: me.gameStats, rrRewards: me.rrRewards }, { merge: true }); } catch {}
    }

    async function awardGameLoss(gameKey, pts = 5) {
      me.gameStats[gameKey].played += 1; me.gameStats[gameKey].losses += 1; me.gameStats[gameKey].points += pts;
      renderGameStatsAndTop5(gameKey);
      try { if (db && me.uid) await setDoc(doc(db, "users", me.uid), { gameStats: me.gameStats, rrRewards: me.rrRewards }, { merge: true }); } catch {}
    }function formatPetLine(p) {
      const parts = [];
      if (p.hasPets) parts.push(escapeHtml(p.hasPets));
      if (p.favPet === "אחר") parts.push(p.otherPetText ? `מעדיף/ה: ${escapeHtml(p.otherPetText)}` : "מעדיף/ה: אחר");
      else if (p.favPet) parts.push(`מעדיף/ה: ${escapeHtml(p.favPet)}`);
      if (p.petName) parts.push(`שם: ${escapeHtml(p.petName)}`);
      return parts.length ? `🐾 ${parts.join(" • ")}` : "";
    }

    let modalPhotos = [], modalPhotoIdx = 0;
    function updateModalPhotoView() {
      if (!modalPhotos.length) return;
      const src = safeUrl(modalPhotos[modalPhotoIdx]);
      if (src) $("modal-main-photo").src = src;
      document.querySelectorAll(".modal-thumb").forEach((img, i) => img.classList.toggle("border-pink-400", i === modalPhotoIdx));
    }

    function openUserModal(person) {
      const gPoints = Object.values(person.gameStats || {}).reduce((a, s) => a + (Number(s.points) || 0), 0);
      modalPhotos = Array.isArray(person.photos) ? person.photos.map(safeUrl).filter(Boolean) : [];
      modalPhotoIdx = 0;
      const b = ["bg-aurora", "bg-sunset", "bg-ocean", "bg-gold"].includes(person.banner) ? person.banner : "bg-aurora";
      const ns = ["name-rainbow", "name-neon", "name-royal", ""].includes(person.nameStyle) ? person.nameStyle : "";
      $("modal-banner").className = `h-32 ${b} relative p-4 flex justify-between items-start`;
      $("modal-level-badge").textContent = `רמה ${getLevel(gPoints)} • ${gPoints} נק׳`;
      $("modal-name").className = `text-2xl font-extrabold ${ns}`;
      $("modal-name").textContent = person.name || "משתמש";
      $("modal-tagline").textContent = person.tagline || "";
      $("modal-meta").textContent = [person.gender, person.age ? `גיל ${person.age}` : "", person.location, person.distanceKm !== undefined ? `${person.distanceKm} ק״מ` : ""].filter(Boolean).join(" • ");
      $("modal-looking-for").textContent = person.lookingFor ? `💘 מחפש/ת: ${person.lookingFor}` : "";
      $("modal-relationship-goal").textContent = [person.goal, person.marital, person.children, person.height ? `${person.height} ס״מ` : ""].filter(Boolean).join(" • ");
      $("modal-lifestyle").textContent = [person.job, person.zodiac].filter(Boolean).join(" • ");
      $("modal-habits").textContent = [person.smoking, person.alcohol].filter(Boolean).join(" • ");
      $("modal-pets-info").textContent = formatPetLine(person);
      $("modal-night-info").textContent = [...(person.nightActivities || []), person.firstDate ? `דייט: ${person.firstDate}` : ""].filter(Boolean).join(" • ");
      $("modal-education").textContent = person.education ? `השכלה: ${person.education}` : "";
      $("modal-bio").textContent = person.bio || "";
      $("modal-tags").innerHTML = [...(person.trips || []), ...(person.hobbies || [])].map((t) => `<span class="px-2.5 py-1 rounded-full bg-indigo-500/20 border border-indigo-400/30">${escapeHtml(t)}</span>`).join("");
      const targetId = person.uid || person.id;
      $("modal-follow-btn").textContent = (me.following || []).includes(targetId) ? "✓ עוקב" : "➕ עקוב";
      $("modal-follow-btn").onclick = async () => {
        if (!targetId || targetId === me.uid) return;
        me.following = me.following || [];
        me.following = me.following.includes(targetId) ? me.following.filter((x) => x !== targetId) : [...me.following, targetId];
        localStorage.setItem("toplove_session", JSON.stringify(me));
        try { if (db && me.uid) await setDoc(doc(db, "users", me.uid), { following: me.following }, { merge: true }); } catch {}
        openUserModal(person); renderRealUsers();
      };
      $("modal-dm-btn").onclick = async () => {
        if (!targetId || targetId === me.uid || !me.uid) return;
        const dmId = "dm_" + [me.uid, targetId].sort().join("_");
        await ensureRoomInFirestore({ id: dmId, topic: `שיחה אישית עם ${person.name || "משתמש"}`, code: "" });
        activeRoomId = dmId; joinedRoomId = dmId; $("user-modal").classList.add("hidden"); switchTab("chat"); renderRooms();
      };
      $("user-modal").classList.remove("hidden");
    }
    $("close-modal-btn").onclick = () => $("user-modal").classList.add("hidden");function syncHeaderUserBadge() {
      $("user-badge").textContent = `${me.name || (me.email ? me.email.split("@")[0] : "משתמש")} • ${me.age || 18}`;
      const av = safeUrl(me.avatar || (me.photos && me.photos[0]) || "");
      $("header-avatar-slot").innerHTML = av ? `<img src="${escapeHtml(av)}" alt="" class="w-full h-full object-cover" />` : "👤";
    }
    $("prof-fav-pet").onchange = () => $("prof-other-pet-wrap").classList.toggle("hidden", $("prof-fav-pet").value !== "אחר");
    function renderQuestionnaireOptions() {
      $("trips-options").innerHTML = tripsChoices.map((x) => `<button type="button" data-trip="${escapeHtml(x)}" class="px-3 py-1.5 rounded-full text-xs border ${me.trips.includes(x) ? "bg-emerald-600 border-emerald-400" : "bg-slate-950 border-slate-700"}">${escapeHtml(x)}</button>`).join("");
      $("trips-options").querySelectorAll("[data-trip]").forEach((b) => { b.onclick = () => { const v = b.dataset.trip; me.trips = me.trips.includes(v) ? me.trips.filter((i) => i !== v) : [...me.trips, v]; renderQuestionnaireOptions(); }; });
      $("night-options").innerHTML = nightChoices.map((x) => `<button type="button" data-night="${escapeHtml(x)}" class="px-3 py-1.5 rounded-full text-xs border ${me.nightActivities.includes(x) ? "bg-purple-600 border-purple-400" : "bg-slate-950 border-slate-700"}">${escapeHtml(x)}</button>`).join("");
      $("night-options").querySelectorAll("[data-night]").forEach((b) => { b.onclick = () => { const v = b.dataset.night; me.nightActivities = me.nightActivities.includes(v) ? me.nightActivities.filter((i) => i !== v) : [...me.nightActivities, v]; renderQuestionnaireOptions(); }; });
      $("hobbies-options").innerHTML = hobbiesChoices.map((x) => `<button type="button" data-hobby="${escapeHtml(x)}" class="px-3 py-1.5 rounded-full text-xs border ${me.hobbies.includes(x) ? "bg-indigo-600 border-indigo-400" : "bg-slate-950 border-slate-700"}">${escapeHtml(x)}</button>`).join("");
      $("hobbies-options").querySelectorAll("[data-hobby]").forEach((b) => { b.onclick = () => { const v = b.dataset.hobby; me.hobbies = me.hobbies.includes(v) ? me.hobbies.filter((i) => i !== v) : [...me.hobbies, v]; renderQuestionnaireOptions(); }; });
    }
    document.querySelectorAll(".style-pick-btn").forEach((b) => { b.onclick = () => { me.nameStyle = b.dataset.style; }; });
    function applyProfileViewMode() {
      syncHeaderUserBadge();
      const showSummary = Boolean(me.profileCompleted);
      $("profile-summary-card").classList.toggle("hidden", !showSummary);
      $("profile-form").classList.toggle("hidden", showSummary);
      $("edit-profile-btn").classList.toggle("hidden", !showSummary);
      if (showSummary) {
        $("summary-name").textContent = me.name || "משתמש";
        $("summary-tagline").textContent = me.tagline || "";
        $("summary-bio").textContent = me.bio || "";
      }
    }
    $("edit-profile-btn").onclick = () => { me.profileCompleted = false; applyProfileViewMode(); };
    function switchTab(t) {
      document.querySelectorAll(".tab-btn").forEach((b) => { b.className = b.dataset.tab === t ? "tab-btn px-5 py-2.5 rounded-xl text-sm font-semibold bg-pink-600 text-white" : "tab-btn px-5 py-2.5 rounded-xl text-sm font-semibold glass text-slate-300"; });
      document.querySelectorAll(".tab-content").forEach((c) => c.classList.add("hidden"));
      $(`tab-${t}`).classList.remove("hidden");
    }
    $("user-profile-trigger").onclick = () => switchTab("profile");
    document.querySelectorAll(".tab-btn").forEach((btn) => { btn.onclick = () => switchTab(btn.dataset.tab); });const defaultRooms = [
      { id: "r-general", topic: "כללי וצ׳אט פתוח", code: "", members: [] },
      { id: "r-dating", topic: "היכרויות, דייטים ושיחות", code: "", members: [] },
      { id: "r-gaming", topic: "גיימינג ומשחקי רשת", code: "", members: [] }
    ];
    let chatRooms = [...defaultRooms], activeRoomId = defaultRooms[0].id, joinedRoomId = null, unsubMsgs = null, unsubRooms = null, unsubUsers = null;

    async function ensureRoomInFirestore(room) {
      if (!db || !room?.id) return;
      try { await setDoc(doc(db, "rooms", room.id), { id: room.id, topic: String(room.topic || "").slice(0, 80), code: String(room.code || "").slice(0, 30), isDm: String(room.id).startsWith("dm_"), updatedAt: serverTimestamp() }, { merge: true }); } catch {}
    }

    function subscribeAllRooms() {
      if (unsubRooms) { unsubRooms(); unsubRooms = null; }
      if (!db) { renderRooms(); return; }
      unsubRooms = onSnapshot(collection(db, "rooms"), (snap) => {
        const byId = new Map(defaultRooms.map((r) => [r.id, { ...r, members: [] }]));
        snap.docs.forEach((d) => { const rr = d.data(); byId.set(d.id, { id: d.id, topic: rr.topic || byId.get(d.id)?.topic || d.id, code: rr.code || "", members: byId.get(d.id)?.members || [] }); });
        chatRooms = Array.from(byId.values()).filter((r) => !String(r.id).startsWith("dm_") || (me.uid && String(r.id).includes(me.uid)));
        renderRooms();
      });
    }

    function listenMsgs(roomId) {
      if (unsubMsgs) { unsubMsgs(); unsubMsgs = null; }
      if (!db) return;
      unsubMsgs = onSnapshot(query(collection(db, "rooms", roomId, "messages"), orderBy("createdAt", "asc")), (snap) => {
        const msgs = snap.docs.map((d) => d.data());
        $("chat-messages").innerHTML = msgs.length ? msgs.map((m) => `<div class="bg-slate-800/90 px-3 py-2 rounded-xl text-xs"><strong class="text-pink-300">${escapeHtml(m.from || "משתמש")}:</strong> ${escapeHtml(m.text || "")}</div>`).join("") : `<p class="text-xs text-slate-400">אין עדיין הודעות.</p>`;
      });
    }

    function renderRooms() {
      $("rooms-list").innerHTML = chatRooms.map((r) => `<div class="p-3 rounded-xl border text-xs flex items-center justify-between gap-2 ${joinedRoomId === r.id ? "bg-pink-600/25 border-pink-400" : "bg-slate-950/75 border-slate-800"}"><span class="font-bold truncate">${escapeHtml(r.topic)}</span><button type="button" data-enter-room="${escapeHtml(r.id)}" class="px-3 py-1.5 rounded-lg bg-pink-600 font-bold">${joinedRoomId === r.id ? "בתוך החדר" : "כנס"}</button></div>`).join("");
      document.querySelectorAll("[data-enter-room]").forEach((btn) => { btn.onclick = async () => { const target = chatRooms.find((r) => r.id === btn.dataset.enterRoom); if (!target) return; await ensureRoomInFirestore(target); activeRoomId = target.id; joinedRoomId = target.id; renderRooms(); listenMsgs(target.id); }; });
      const cur = chatRooms.find((r) => r.id === activeRoomId) || chatRooms[0];
      $("active-room-title").textContent = cur.topic;
      $("leave-room-btn").classList.toggle("hidden", joinedRoomId !== cur.id);
    }

    $("chat-form").onsubmit = async (e) => {
      e.preventDefault();
      if (joinedRoomId !== activeRoomId || !db) return;
      const txt = $("chat-input").value.trim().slice(0, 1000); if (!txt) return;
      $("chat-input").value = "";
      await addDoc(collection(db, "rooms", activeRoomId, "messages"), { senderUid: me.uid, from: me.name || "משתמש", text: txt, createdAt: serverTimestamp() });
    };function renderRealUsers() {
      const pool = [...allUsers, ...sampleCandidates];
      $("real-users-grid").innerHTML = pool.map((u) => `<div class="bg-slate-900/85 border border-slate-700 rounded-2xl p-4 space-y-2"><div class="font-bold text-sm">${escapeHtml(u.name || "משתמש")} • גיל ${Number(u.age) || 25}</div><div class="text-xs text-slate-300">${escapeHtml(u.location || "")}</div><button type="button" data-open-id="${escapeHtml(u.uid || u.id || "")}" class="px-3 py-1.5 rounded-lg bg-pink-600 text-xs font-bold">פתח כרטיס</button></div>`).join("");
      document.querySelectorAll("[data-open-id]").forEach((b) => { b.onclick = () => { const f = pool.find((x) => (x.uid || x.id) === b.dataset.openId); if (f) openUserModal(f); }; });
      $("match-deck-counter").textContent = `${pool.length} פרופילים`;
      $("match-deck-card").innerHTML = pool[deckIdx % pool.length] ? `<div class="font-bold">${escapeHtml(pool[deckIdx % pool.length].name)} • גיל ${Number(pool[deckIdx % pool.length].age) || 25}</div>` : "";
    }
    $("deck-skip-btn").onclick = () => { deckIdx += 1; renderRealUsers(); };

    function openApp(session) {
      Object.assign(me, session);
      $("auth-section").classList.add("hidden"); $("app-section").classList.remove("hidden");
      $("user-profile-trigger").classList.remove("hidden"); $("user-profile-trigger").classList.add("flex");
      $("logout-btn").classList.remove("hidden");
      syncHeaderUserBadge(); renderQuestionnaireOptions(); applyProfileViewMode(); renderGameStatsAndTop5("ttt"); subscribeAllRooms(); renderRooms(); renderRealUsers();
    }

    $("auth-form").onsubmit = async (e) => {
      e.preventDefault();
      const email = $("auth-email").value.trim().toLowerCase(), password = $("auth-password").value, age = Number($("auth-age").value), lookingFor = $("auth-looking-for").value;
      if (!age || age < 18 || age > 80) { $("auth-error").textContent = "גילאי 18 עד 80 בלבד."; $("auth-error").classList.remove("hidden"); return; }
      let uid = "local_" + email.replace(/[^a-z0-9]/g, "_");
      if (hasRealFirebaseConfig && auth) {
        try { const c = await signInWithEmailAndPassword(auth, email, password); uid = c.user.uid; }
        catch { const c = await createUserWithEmailAndPassword(auth, email, password); uid = c.user.uid; }
      }
      const session = { ...me, uid, email, name: email.split("@")[0], age, lookingFor };
      localStorage.setItem("toplove_session", JSON.stringify(session));
      try { if (db && uid) await setDoc(doc(db, "users", uid), { ...session, updatedAt: serverTimestamp() }, { merge: true }); } catch {}
      openApp(session);
    };

    $("logout-btn").onclick = async () => { try { if (auth) await signOut(auth); } catch {} localStorage.removeItem("toplove_session"); location.reload(); };
    const savedSession = localStorage.getItem("toplove_session");
    if (savedSession) { try { openApp(JSON.parse(savedSession)); } catch {} }
  </script>
</body>
</html>
