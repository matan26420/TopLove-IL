<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>TopLove IL</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    body {
      background: linear-gradient(135deg, #0f172a, #1e1b4b, #311042);
      min-height: 100vh;
      font-family: system-ui, -apple-system, sans-serif;
    }
    .glass {
      background: rgba(30, 41, 59, 0.78);
      backdrop-filter: blur(12px);
      border: 1px solid rgba(255, 255, 255, 0.12);
    }
    .arena-warehouse {
      background: radial-gradient(circle at 50% 25%, rgba(245, 158, 11, 0.14), rgba(15, 23, 42, 0.92) 72%);
      border: 1px solid rgba(251, 191, 36, 0.25);
    }
    .arena-cards {
      background: radial-gradient(circle at 50% 35%, rgba(16, 185, 129, 0.2), rgba(6, 78, 59, 0.45) 55%, rgba(15, 23, 42, 0.94));
      border: 1px solid rgba(52, 211, 153, 0.3);
    }
    .arena-rps {
      background: radial-gradient(circle at 50% 30%, rgba(236, 72, 153, 0.18), rgba(30, 27, 75, 0.92) 75%);
      border: 1px solid rgba(244, 114, 182, 0.28);
    }
    .arena-rr {
      background: radial-gradient(circle at 50% 25%, rgba(244, 63, 94, 0.2), rgba(15, 23, 42, 0.95) 75%);
      border: 1px solid rgba(251, 113, 133, 0.32);
    }
    @keyframes dealPop {
      0% { transform: translateY(-28px) scale(0.75) rotate(-8deg); opacity: 0; }
      100% { transform: translateY(0) scale(1) rotate(0deg); opacity: 1; }
    }
    .card-deal {
      animation: dealPop 0.35s cubic-bezier(0.22, 1, 0.36, 1) forwards;
    }
    @keyframes gunAim {
      0%, 100% { transform: translateX(0) rotate(0deg); }
      50% { transform: translateX(-6px) rotate(-14deg); }
    }
    .gun-aim {
      animation: gunAim 0.65s ease-in-out infinite;
    }
    @keyframes confettiFall {
      0% { transform: translateY(-20px) rotate(0deg) scale(1); opacity: 1; }
      100% { transform: translateY(230px) rotate(540deg) scale(0.85); opacity: 0; }
    }
    .confetti-piece {
      position: absolute;
      top: 0;
      width: 10px;
      height: 16px;
      border-radius: 3px;
      pointer-events: none;
      animation: confettiFall 1.55s ease-out forwards;
    }
  </style>
</head>
<body class="text-white antialiased">
  <header class="glass sticky top-0 z-50 px-6 py-4 flex flex-wrap items-center justify-between gap-3 shadow-lg">
    <div class="flex items-center gap-2">
      <span class="text-2xl">💜</span>
      <h1 class="text-xl font-bold bg-gradient-to-l from-pink-400 to-indigo-400 bg-clip-text text-transparent">TopLove IL</h1>
      <span class="text-xs bg-emerald-500/20 border border-emerald-400/40 text-emerald-200 px-2.5 py-0.5 rounded-full">
        חינם לגמרי • 18+
      </span>
    </div>
    <div class="flex items-center gap-3">
      <span id="eliminated-badge" class="hidden text-xs bg-rose-500/25 border border-rose-400/50 text-rose-200 px-3 py-1 rounded-full">
        🚫 נפסלת ברולטה רוסית
      </span>
      <span id="user-badge" class="hidden text-sm text-slate-200 bg-slate-800 px-3 py-1 rounded-full"></span>
      <button id="logout-btn" type="button" class="hidden bg-rose-600 hover:bg-rose-500 text-sm px-4 py-1.5 rounded-lg">התנתק</button>
    </div>
  </header><main class="max-w-6xl mx-auto px-4 py-8 space-y-6">
    <section id="auth-section" class="max-w-md mx-auto glass rounded-2xl p-8 shadow-2xl mt-6">
      <h2 class="text-2xl font-bold text-center mb-2">ברוכים הבאים ל-TopLove IL</h2>
      <p class="text-slate-300 text-sm text-center mb-6">כניסה והרשמה חינם לגילאי 18 ומעלה בלבד</p>
      <form id="auth-form" class="space-y-4">
        <input type="email" id="auth-email" required placeholder="אימייל" dir="ltr"
          class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700 text-left" />
        <input type="number" id="auth-age" required min="18" max="99" placeholder="גיל (18+ בלבד)"
          class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700" />
        <div class="relative">
          <input type="password" id="auth-password" required minlength="6" placeholder="סיסמה (מינימום 6 תווים)" dir="ltr"
            class="w-full px-4 py-2.5 pl-11 rounded-xl bg-slate-900 border border-slate-700 text-left" />
          <button type="button" id="toggle-password-btn" class="absolute left-3 top-1/2 -translate-y-1/2 text-slate-400">👁️</button>
        </div>
        <p id="auth-error" class="text-rose-400 text-xs hidden"></p>
        <button type="submit" class="w-full py-3 rounded-xl font-semibold bg-gradient-to-l from-pink-600 to-indigo-600">
          כניסה / הרשמה
        </button>
      </form>
    </section>

    <section id="app-section" class="hidden space-y-6">
      <div class="flex flex-wrap gap-2 justify-center">
        <button type="button" data-tab="profile" class="tab-btn px-4 py-2 rounded-xl text-sm font-semibold bg-pink-600 text-white">1. הפרופיל שלי</button>
        <button type="button" data-tab="users" class="tab-btn px-4 py-2 rounded-xl text-sm font-semibold glass text-slate-300">2. משתמשים מחוברים 👥</button>
        <button type="button" data-tab="chat" class="tab-btn px-4 py-2 rounded-xl text-sm font-semibold glass text-slate-300">3. חדרי שיחה 💬</button>
        <button type="button" data-tab="games" class="tab-btn px-4 py-2 rounded-xl text-sm font-semibold glass text-slate-300">4. משחקים ושולחנות 🎮</button>
      </div><div id="tab-profile" class="tab-content max-w-2xl mx-auto glass rounded-2xl p-6 shadow-xl">
        <h2 class="text-xl font-bold mb-4">הפרופיל האישי שלי</h2>
        <form id="profile-form" class="space-y-4">
          <div class="flex flex-col sm:flex-row items-center gap-4 bg-slate-900/70 p-4 rounded-xl border border-slate-700">
            <img id="prof-avatar-preview" src="https://api.dicebear.com/9.x/avataaars/svg?seed=TopLove" alt="תמונת פרופיל"
              class="w-20 h-20 rounded-full object-cover border-2 border-pink-500 bg-slate-800 shrink-0" />
            <div class="w-full space-y-2">
              <label class="block text-xs font-semibold text-pink-300">העלה תמונה מהמחשב או הכנס קישור</label>
              <input type="file" id="prof-avatar-file" accept="image/*"
                class="block w-full text-xs text-slate-300 file:ml-3 file:py-1.5 file:px-3 file:rounded-lg file:border-0 file:bg-pink-600 file:text-white" />
              <input type="url" id="prof-avatar-url" placeholder="קישור לתמונה (https://...)" dir="ltr"
                class="w-full px-3 py-1.5 text-sm rounded-lg bg-slate-950 border border-slate-700 text-left" />
            </div>
          </div>

          <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
            <input type="text" id="prof-name" required placeholder="שם / כינוי"
              class="px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700" />
            <select id="prof-gender" class="px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700">
              <option value="זכר">מגדר: זכר</option>
              <option value="נקבה">מגדר: נקבה</option>
            </select>
          </div>

          <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
            <input type="number" id="prof-age" min="18" max="99" required value="18" placeholder="גיל (18+)"
              class="px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700" />
            <input type="text" id="prof-city" required placeholder="עיר"
              class="px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700" />
          </div>

          <textarea id="prof-bio" rows="2" placeholder="קצת עליי..."
            class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700"></textarea>

          <p id="profile-error" class="text-rose-400 text-xs hidden"></p>
          <div class="flex items-center justify-between">
            <span id="save-feedback" class="text-emerald-400 text-sm opacity-0 transition-opacity">✓ נשמר!</span>
            <button type="submit" class="px-6 py-2.5 rounded-xl font-semibold bg-gradient-to-l from-pink-600 to-indigo-600">שמור פרופיל</button>
          </div>
        </form>
      </div>

      <div id="tab-users" class="tab-content hidden max-w-4xl mx-auto glass rounded-2xl p-6 space-y-4">
        <h2 class="text-xl font-bold">👥 משתמשים אמיתיים במערכת</h2>
        <p class="text-xs text-slate-300">כאן מופיעים משתמשים שנרשמו למערכת. אפשר לפתוח שיחה אישית או להיכנס לשולחן משחק.</p>
        <div id="real-users-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4"></div>
      </div><div id="tab-chat" class="tab-content hidden max-w-5xl mx-auto glass rounded-2xl p-6 space-y-5">
        <div class="bg-slate-900/80 border border-slate-700 rounded-xl p-4 space-y-3">
          <h3 class="text-sm font-bold text-pink-300">➕ פתיחת חדר שיחה חדש לפי נושא</h3>
          <form id="create-room-form" class="flex flex-col sm:flex-row gap-2.5">
            <input type="text" id="new-room-topic" required placeholder="נושא השיחה (למשל: מוזיקה, טיולים, סרטים)"
              class="flex-1 px-3.5 py-2 rounded-xl bg-slate-950 border border-slate-700 text-sm" />
            <button type="submit" class="px-5 py-2 rounded-xl text-sm font-semibold bg-gradient-to-l from-pink-600 to-indigo-600">
              פתח חדר שיחה
            </button>
          </form>
        </div>

        <div class="grid grid-cols-1 lg:grid-cols-3 gap-5">
          <div class="space-y-2">
            <h3 class="text-sm font-bold text-slate-200">🗂️ חדרים לפי נושאי שיחה</h3>
            <div id="rooms-list" class="space-y-2 max-h-80 overflow-y-auto"></div>
          </div>

          <div class="lg:col-span-2 bg-slate-900/70 border border-slate-800 rounded-2xl p-4 flex flex-col justify-between min-h-[340px] space-y-3">
            <div class="border-b border-white/10 pb-2">
              <h3 id="active-room-title" class="font-bold text-base">בחר חדר</h3>
              <p id="active-room-meta" class="text-xs text-slate-400">חדר שיחה פתוח</p>
            </div>

            <div id="chat-messages" class="space-y-2 max-h-56 overflow-y-auto py-1"></div>

            <form id="chat-form" class="flex gap-2 pt-2 border-t border-white/10">
              <input type="text" id="chat-input" required placeholder="כתוב הודעה בחדר..."
                class="flex-1 px-4 py-2 rounded-xl bg-slate-950 border border-slate-700 text-sm" />
              <button type="submit" class="px-5 py-2 rounded-xl text-sm font-semibold bg-pink-600">שלח</button>
            </form>
          </div>
        </div>
      </div>

      <div id="tab-games" class="tab-content hidden space-y-6">
        <div id="eliminated-banner" class="hidden bg-rose-950/85 border border-rose-500/60 rounded-2xl p-4 flex flex-wrap items-center justify-between gap-3">
          <div>
            <div class="font-bold text-rose-200 text-sm">💥 נפסלת במשחק הרולטה הרוסית!</div>
            <div class="text-xs text-rose-300">הדמות שלך מחוץ לשאר המשחקים עד שתבחר לחזור למשחק.</div>
          </div>
          <button type="button" id="revive-me-btn" class="px-4 py-2 rounded-xl text-xs font-semibold bg-emerald-600 hover:bg-emerald-500">
            חזור למשחק (איפוס פסילה)
          </button>
        </div>

        <div class="glass rounded-2xl p-4 space-y-3 border border-pink-500/30">
          <div class="flex flex-wrap items-center justify-between gap-2">
            <div>
              <h3 class="text-base font-bold">🪑 שולחנות פעילים של משתמשים במשחק הנבחר</h3>
              <p class="text-xs text-slate-300">ברגע שמישהו נכנס לשולחן מולך — הדמות שלו מופיעה אוטומטית בזירה!</p>
            </div>
            <button type="button" id="create-my-table-btn" class="px-4 py-2 rounded-xl text-xs font-semibold bg-emerald-600 hover:bg-emerald-500">
              + פתח שולחן שלי במשחק זה
            </button>
          </div>

          <div id="game-tables-list" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-2.5"></div>

          <div class="pt-2 border-t border-white/10 flex flex-wrap items-center justify-between gap-2 text-xs">
            <span id="selected-table-info" class="text-pink-200 font-semibold">לא נבחר שולחן עדיין</span>
            <span id="turn-lock-banner" class="text-amber-200 bg-amber-500/20 border border-amber-400/40 px-3 py-1 rounded-full">
              ממתין למשתמש אחר
            </span>
          </div>
        </div>

        <div class="flex flex-wrap gap-2 justify-center">
          <button type="button" data-game="ttt" class="game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold bg-pink-600">1. איקס עיגול (מחסן)</button>
          <button type="button" data-game="rps" class="game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold glass text-slate-300">2. אבן נייר מספריים</button>
          <button type="button" data-game="tod" class="game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold glass text-slate-300">3. אמת או חובה</button>
          <button type="button" data-game="cards" class="game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold glass text-slate-300">4. שולחן קלפים</button>
          <button type="button" data-game="roulette" class="game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold glass text-slate-300">5. רולטה רוסית 🔫</button>
        </div><div id="game-ttt" class="game-panel max-w-2xl mx-auto arena-warehouse rounded-2xl p-6 space-y-4 shadow-xl">
          <div class="flex flex-wrap items-center justify-between gap-2">
            <div>
              <h3 class="text-xl font-bold">📦 איקס עיגול — בתוך המחסן</h3>
              <p class="text-xs text-amber-200/80">שתי דמויות יושבות מול קופסת העץ במחסן ומניחות סימנים</p>
            </div>
            <button type="button" id="ttt-reset" class="text-xs bg-slate-800 hover:bg-slate-700 px-3 py-1.5 rounded-lg border border-slate-600">איפוס לוח</button>
          </div>

          <div class="grid grid-cols-3 items-center gap-2 bg-slate-950/65 border border-amber-500/20 rounded-2xl p-4">
            <div id="ttt-host-char" class="flex flex-col items-center text-center gap-1.5 p-2 rounded-xl transition">
              <img id="ttt-host-img" src="https://api.dicebear.com/9.x/avataaars/svg?seed=Host" alt="" class="w-14 h-14 rounded-full border-2 border-amber-400 bg-slate-800" />
              <span id="ttt-host-name" class="text-xs font-bold truncate max-w-full">מארח</span>
              <span class="text-[11px] px-2 py-0.5 rounded-full bg-amber-500/20 text-amber-200">יושב מול הקופסה ❌</span>
            </div>

            <div class="bg-amber-950/90 border-4 border-amber-700/80 rounded-2xl p-3 shadow-inner space-y-2">
              <div class="text-[10px] text-center tracking-wider text-amber-300 font-semibold">📦 קופסת המחסן</div>
              <div id="ttt-board" class="grid grid-cols-3 gap-1.5"></div>
            </div>

            <div id="ttt-guest-char" class="flex flex-col items-center text-center gap-1.5 p-2 rounded-xl transition">
              <img id="ttt-guest-img" src="https://api.dicebear.com/9.x/avataaars/svg?seed=Guest" alt="" class="w-14 h-14 rounded-full border-2 border-slate-600 bg-slate-800 opacity-60" />
              <span id="ttt-guest-name" class="text-xs font-bold text-slate-400 truncate max-w-full">ממתין לשחקן...</span>
              <span id="ttt-guest-status" class="text-[11px] px-2 py-0.5 rounded-full bg-slate-800 text-slate-400">טרם נכנס ⭕</span>
            </div>
          </div>

          <p id="ttt-status" class="text-sm text-center text-pink-200 font-medium">בחר שולחן של משתמש כדי לשחק</p>
        </div>

        <div id="game-rps" class="game-panel hidden max-w-2xl mx-auto arena-rps rounded-2xl p-6 space-y-4 shadow-xl">
          <div class="text-center">
            <h3 class="text-xl font-bold">✂️ אבן, נייר ומספריים — זירת הדמויות</h3>
            <p class="text-xs text-pink-200/80">דמות סופרת ("אבן... נייר... מספריים...") ומיד נחשפת הבחירה של שתי הדמויות</p>
          </div>

          <div class="grid grid-cols-3 items-center gap-2 bg-slate-950/65 border border-pink-400/20 rounded-2xl p-4 text-center">
            <div class="flex flex-col items-center gap-1.5">
              <img id="rps-p1-img" src="https://api.dicebear.com/9.x/avataaars/svg?seed=P1" alt="" class="w-14 h-14 rounded-full border-2 border-pink-400 bg-slate-800" />
              <span id="rps-p1-name" class="text-xs font-bold">אתה</span>
              <div id="rps-p1-hand" class="text-3xl bg-slate-900 border border-slate-700 w-16 h-16 rounded-2xl flex items-center justify-center">✊</div>
            </div>

            <div class="flex flex-col items-center justify-center gap-1">
              <span class="text-[11px] text-slate-400">הדמות סופרת</span>
              <div id="rps-counter-display" class="px-3 py-1.5 rounded-xl bg-pink-600/25 border border-pink-400/50 text-pink-200 font-bold text-sm">
                מוכן לספירה
              </div>
              <span id="rps-vs-status" class="text-[11px] text-slate-300 mt-1">המתן לכניסת משתמש</span>
            </div>

            <div class="flex flex-col items-center gap-1.5">
              <img id="rps-p2-img" src="https://api.dicebear.com/9.x/avataaars/svg?seed=P2" alt="" class="w-14 h-14 rounded-full border-2 border-slate-600 bg-slate-800 opacity-60" />
              <span id="rps-p2-name" class="text-xs font-bold text-slate-400">ממתין ליריב...</span>
              <div id="rps-p2-hand" class="text-3xl bg-slate-900 border border-slate-700 w-16 h-16 rounded-2xl flex items-center justify-center">✊</div>
            </div>
          </div>

          <div class="flex flex-wrap justify-center gap-3">
            <button type="button" data-rps="rock" class="rps-choice px-5 py-3 rounded-xl bg-slate-800 hover:bg-pink-600 text-base font-semibold transition">🪨 אבן</button>
            <button type="button" data-rps="paper" class="rps-choice px-5 py-3 rounded-xl bg-slate-800 hover:bg-pink-600 text-base font-semibold transition">📄 נייר</button>
            <button type="button" data-rps="scissors" class="rps-choice px-5 py-3 rounded-xl bg-slate-800 hover:bg-pink-600 text-base font-semibold transition">✂️ מספריים</button>
          </div>

          <p id="rps-result" class="text-sm text-center text-pink-200 bg-slate-900/90 p-3.5 rounded-xl border border-white/10">
            בחר בחירה כדי להתחיל ספירה מול הדמות שמולך
          </p>
        </div>

        <div id="game-tod" class="game-panel hidden max-w-2xl mx-auto glass rounded-2xl p-6 space-y-4">
          <div class="flex items-center justify-around bg-slate-950/60 border border-white/10 rounded-2xl p-3">
            <div class="flex items-center gap-2">
              <img id="tod-p1-img" src="https://api.dicebear.com/9.x/avataaars/svg?seed=Tod1" alt="" class="w-11 h-11 rounded-full border border-indigo-400 bg-slate-800" />
              <span id="tod-p1-name" class="text-xs font-bold">שחקן 1</span>
            </div>
            <span class="text-xs font-bold px-2.5 py-1 rounded-full bg-indigo-500/20 text-indigo-200">🔥 אמת או חובה</span>
            <div class="flex items-center gap-2">
              <img id="tod-p2-img" src="https://api.dicebear.com/9.x/avataaars/svg?seed=Tod2" alt="" class="w-11 h-11 rounded-full border border-pink-400 bg-slate-800 opacity-60" />
              <span id="tod-p2-name" class="text-xs font-bold text-slate-400">ממתין לשחקן...</span>
            </div>
          </div>

          <div class="text-center space-y-3">
            <div class="flex justify-center gap-3">
              <button type="button" id="btn-truth" class="px-6 py-2.5 rounded-xl font-semibold bg-indigo-600 hover:bg-indigo-500">אמת 💭</button>
              <button type="button" id="btn-dare" class="px-6 py-2.5 rounded-xl font-semibold bg-pink-600 hover:bg-pink-500">חובה ⚡</button>
            </div>
            <p id="tod-text" class="text-base text-pink-200 bg-slate-900 p-4 rounded-xl border border-white/10">לחץ על אמת או חובה לקבלת משימה</p>
          </div>
        </div><div id="game-cards" class="game-panel hidden max-w-3xl mx-auto arena-cards rounded-2xl p-6 space-y-4 shadow-xl">
          <div class="flex flex-wrap items-center justify-between gap-2">
            <div>
              <h3 class="text-xl font-bold">🃏 שולחן קלפים וחלוקה</h3>
              <p class="text-xs text-emerald-200/80">מתיישבים לשולחן, מחלקים קלפים מהחפיסה ומניחים קלף במרכז השולחן</p>
            </div>
            <div class="flex gap-2">
              <button type="button" id="cards-sit-btn" class="px-3.5 py-1.5 rounded-xl text-xs font-semibold bg-emerald-600 hover:bg-emerald-500">
                🪑 התיישב לשולחן
              </button>
              <button type="button" id="cards-deal-btn" class="px-3.5 py-1.5 rounded-xl text-xs font-semibold bg-amber-600 hover:bg-amber-500">
                🃏 חלק קלפים
              </button>
            </div>
          </div>

          <div class="bg-emerald-950/75 border-2 border-emerald-500/35 rounded-2xl p-4 space-y-4">
            <div class="flex items-center justify-between gap-3 border-b border-emerald-500/20 pb-3">
              <div class="flex items-center gap-2.5">
                <img id="cards-opp-img" src="https://api.dicebear.com/9.x/avataaars/svg?seed=CardOpp" alt="" class="w-11 h-11 rounded-full border-2 border-emerald-400 bg-slate-800 opacity-60" />
                <div>
                  <div id="cards-opp-name" class="text-xs font-bold text-emerald-200">ממתין לשחקן שני בשולחן...</div>
                  <div id="cards-opp-count" class="text-[11px] text-emerald-300/75">0 קלפים ביד</div>
                </div>
              </div>
              <div id="cards-opp-backs" class="flex gap-1"></div>
            </div>

            <div class="flex flex-wrap items-center justify-center gap-6 py-2">
              <div class="flex flex-col items-center gap-1">
                <div class="w-16 h-24 rounded-xl bg-gradient-to-br from-indigo-700 to-rose-800 border-2 border-white/30 shadow-lg flex items-center justify-center text-2xl">
                  🂠
                </div>
                <span class="text-[11px] text-emerald-200">חפיסה</span>
              </div>

              <div class="flex flex-col items-center gap-1">
                <div id="cards-table-center" class="w-20 h-28 rounded-xl border-2 border-dashed border-emerald-400/50 bg-emerald-900/40 flex items-center justify-center text-center p-1 text-xs text-emerald-200">
                  אין קלף על השולחן
                </div>
                <span class="text-[11px] text-emerald-200">קלף במרכז השולחן</span>
              </div>
            </div>

            <div class="border-t border-emerald-500/20 pt-3 space-y-2">
              <div class="flex items-center justify-between">
                <div class="flex items-center gap-2">
                  <img id="cards-me-img" src="https://api.dicebear.com/9.x/avataaars/svg?seed=CardMe" alt="" class="w-10 h-10 rounded-full border-2 border-pink-400 bg-slate-800" />
                  <span id="cards-me-name" class="text-xs font-bold">היד שלי</span>
                </div>
                <span class="text-[11px] text-emerald-200">לחץ על קלף כדי להוריד לשולחן</span>
              </div>
              <div id="cards-my-hand" class="flex flex-wrap gap-2 min-h-[96px] items-center bg-slate-950/45 p-2.5 rounded-xl border border-white/10"></div>
            </div>
          </div>

          <p id="cards-status" class="text-sm text-center text-emerald-200">לחץ על "התיישב לשולחן" ולאחר מכן "חלק קלפים"</p>
        </div>

        <div id="game-roulette" class="game-panel hidden max-w-2xl mx-auto arena-rr rounded-2xl p-6 space-y-4 shadow-xl relative overflow-hidden">
          <div id="confetti-layer" class="inset-0 absolute pointer-events-none z-20 overflow-hidden"></div>

          <div class="flex flex-wrap items-center justify-between gap-2 relative z-10">
            <div>
              <h3 class="text-xl font-bold">🔫 רולטה רוסית</h3>
              <p class="text-xs text-rose-200/80">הדמות מקרבת אקדח לראש — אם יש כדור יוצא קונפטי והשחקן נפסל משאר המשחקים!</p>
            </div>
            <div class="flex gap-2">
              <button type="button" id="rr-spin-btn" class="px-3.5 py-1.5 rounded-xl text-xs font-semibold bg-slate-800 hover:bg-slate-700 border border-slate-600">
                🔄 סובב תוף
              </button>
              <button type="button" id="rr-reset-btn" class="px-3.5 py-1.5 rounded-xl text-xs font-semibold bg-rose-700 hover:bg-rose-600">
                איפוס סיבוב
              </button>
            </div>
          </div>

          <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 items-center bg-slate-950/70 border border-rose-500/25 rounded-2xl p-4 relative z-10">
            <div class="flex flex-col items-center text-center gap-2 p-3 rounded-xl bg-slate-900/80 border border-white/10">
              <div class="relative flex items-center justify-center">
                <img id="rr-char-img" src="https://api.dicebear.com/9.x/avataaars/svg?seed=RR" alt="" class="w-20 h-20 rounded-full border-2 border-rose-400 bg-slate-800" />
                <span id="rr-gun-icon" class="text-3xl -mr-3 mt-1 gun-aim" title="אקדח קרוב לראש">🔫</span>
              </div>
              <div id="rr-char-name" class="font-bold text-sm">הדמות שלי</div>
              <div id="rr-char-state" class="text-xs px-2.5 py-0.5 rounded-full bg-emerald-500/20 text-emerald-200">
                במשחק • אקדח מכוון
              </div>
            </div>

            <div class="space-y-3 text-center">
              <div id="rr-chamber-info" class="text-xs text-rose-200 bg-rose-950/60 border border-rose-500/30 rounded-xl py-2 px-3">
                תוף מסתובב (6 תאים, כדור אחד פעיל)
              </div>
              <button type="button" id="rr-pull-btn" class="w-full py-3.5 rounded-xl font-bold bg-gradient-to-l from-rose-600 to-amber-600 hover:opacity-95 shadow-lg">
                💥 קרבים לראש ולחץ על ההדק
              </button>
            </div>
          </div>

          <p id="rr-status" class="text-sm text-center text-rose-200 relative z-10">
            סובב תוף או לחץ על ההדק. אם יירה — יצא קונפטי והדמות תיפסל משאר המשחקים!
          </p>
        </div>
      </div>
    </section>
  </main><script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/11.0.0/firebase-app.js";
    import { getAnalytics } from "https://www.gstatic.com/firebasejs/11.0.0/firebase-analytics.js";
    import {
      getFirestore, collection, doc, setDoc, addDoc, updateDoc,
      onSnapshot, query, orderBy, serverTimestamp
    } from "https://www.gstatic.com/firebasejs/11.0.0/firebase-firestore.js";

    const firebaseConfig = {
      apiKey: "AIzaSyDU1U8pC_xrEh6Kl0yyn4p20w5jzW7bWgI",
      authDomain: "toplove-il.firebaseapp.com",
      projectId: "toplove-il",
      storageBucket: "toplove-il.firebasestorage.app",
      messagingSenderId: "143390156671",
      appId: "1:143390156671:web:f7b74f1d5d815277f75c4a",
      measurementId: "G-VNTDRK1SVV"
    };

    const app = initializeApp(firebaseConfig);
    if (location.protocol !== "file:") getAnalytics(app);
    const db = getFirestore(app);

    const $ = (id) => document.getElementById(id);
    const me = {
      uid: "", email: "", name: "משתמש", gender: "זכר", age: 18,
      city: "ישראל", bio: "", avatar: "https://api.dicebear.com/9.x/avataaars/svg?seed=TopLove",
      eliminated: false
    };
    const chatRooms = [
      { id: "r-music", topic: "מוזיקה והופעות" },
      { id: "r-travel", topic: "טיולים וסופ״ש" },
      { id: "r-games", topic: "משחקים וצחוק" }
    ];
    let activeRoomId = chatRooms[0].id;
    let unsubMsgs = null;
    let allUsers = [];

    function syncEliminationUI() {
      const elim = Boolean(me.eliminated);
      $("eliminated-badge").classList.toggle("hidden", !elim);
      $("eliminated-banner").classList.toggle("hidden", !elim);
      localStorage.setItem("toplove_session", JSON.stringify(me));
      applyTurnLockToBoard();
    }

    $("revive-me-btn").onclick = async () => {
      me.eliminated = false;
      syncEliminationUI();
      try { await setDoc(doc(db, "users", me.uid), { eliminated: false }, { merge: true }); } catch {}
    };

    function switchTab(tabName) {
      document.querySelectorAll(".tab-btn").forEach((b) => {
        b.className = b.dataset.tab === tabName
          ? "tab-btn px-4 py-2 rounded-xl text-sm font-semibold bg-pink-600 text-white"
          : "tab-btn px-4 py-2 rounded-xl text-sm font-semibold glass text-slate-300";
      });
      document.querySelectorAll(".tab-content").forEach((c) => c.classList.add("hidden"));
      $(`tab-${tabName}`).classList.remove("hidden");
    }

    function openApp(session) {
      Object.assign(me, session);
      me.eliminated = Boolean(session.eliminated);
      $("auth-section").classList.add("hidden");
      $("app-section").classList.remove("hidden");
      $("user-badge").classList.remove("hidden");
      $("logout-btn").classList.remove("hidden");
      $("user-badge").textContent = `${me.name} • ${me.gender}, ${me.age}`;
      $("prof-name").value = me.name;
      $("prof-gender").value = me.gender;
      $("prof-age").value = me.age;
      $("prof-city").value = me.city;
      $("prof-bio").value = me.bio;
      $("prof-avatar-preview").src = me.avatar;
      $("rr-char-img").src = me.avatar;
      $("rr-char-name").textContent = me.name;
      $("cards-me-img").src = me.avatar;
      $("cards-me-name").textContent = `${me.name} (היד שלי)`;
      switchTab("profile");
      renderRooms();
      subscribeUsers();
      subscribeGameTables();
      renderTttBoard(Array(9).fill(""));
      syncArenasWithPlayers();
      syncEliminationUI();
    }

    $("toggle-password-btn").onclick = () => {
      $("auth-password").type = $("auth-password").type === "password" ? "text" : "password";
    };

    $("auth-form").onsubmit = async (e) => {
      e.preventDefault();
      const email = $("auth-email").value.trim().toLowerCase();
      const age = Number($("auth-age").value);
      if (!age || age < 18) {
        $("auth-error").textContent = "כניסה והרשמה מותרים מגיל 18 ומעלה בלבד.";
        $("auth-error").classList.remove("hidden");
        return;
      }
      $("auth-error").classList.add("hidden");
      const uid = "u_" + email.replace(/[^a-z0-9]/g, "_");
      const session = {
        uid, email, name: email.split("@")[0] || "משתמש", gender: "זכר", age,
        city: "ישראל", bio: "", avatar: `https://api.dicebear.com/9.x/avataaars/svg?seed=${encodeURIComponent(uid)}`,
        eliminated: false
      };
      localStorage.setItem("toplove_session", JSON.stringify(session));
      try { await setDoc(doc(db, "users", uid), { ...session, updatedAt: serverTimestamp() }, { merge: true }); } catch {}
      openApp(session);
    };

    $("logout-btn").onclick = () => {
      localStorage.removeItem("toplove_session");
      location.reload();
    };

    document.querySelectorAll(".tab-btn").forEach((btn) => {
      btn.onclick = () => switchTab(btn.dataset.tab);
    });

    $("prof-avatar-file").onchange = (e) => {
      const f = e.target.files?.[0];
      if (!f) return;
      const rd = new FileReader();
      rd.onload = () => {
        me.avatar = String(rd.result);
        $("prof-avatar-preview").src = me.avatar;
        $("rr-char-img").src = me.avatar;
        $("cards-me-img").src = me.avatar;
      };
      rd.readAsDataURL(f);
    };
    $("prof-avatar-url").oninput = (e) => {
      if (e.target.value.trim()) {
        me.avatar = e.target.value.trim();
        $("prof-avatar-preview").src = me.avatar;
        $("rr-char-img").src = me.avatar;
        $("cards-me-img").src = me.avatar;
      }
    };

    $("profile-form").onsubmit = async (e) => {
      e.preventDefault();
      const age = Number($("prof-age").value);
      if (!age || age < 18) {
        $("profile-error").textContent = "גיל חייב להיות 18 ומעלה.";
        $("profile-error").classList.remove("hidden");
        return;
      }
      $("profile-error").classList.add("hidden");
      me.name = $("prof-name").value.trim() || me.name;
      me.gender = $("prof-gender").value;
      me.age = age;
      me.city = $("prof-city").value.trim() || me.city;
      me.bio = $("prof-bio").value.trim();
      localStorage.setItem("toplove_session", JSON.stringify(me));
      $("user-badge").textContent = `${me.name} • ${me.gender}, ${me.age}`;
      $("rr-char-name").textContent = me.name;
      $("cards-me-name").textContent = `${me.name} (היד שלי)`;
      try { await setDoc(doc(db, "users", me.uid), { ...me, updatedAt: serverTimestamp() }, { merge: true }); } catch {}
      $("save-feedback").classList.remove("opacity-0");
      setTimeout(() => $("save-feedback").classList.add("opacity-0"), 1500);
      syncArenasWithPlayers();
    };function subscribeUsers() {
      onSnapshot(collection(db, "users"), (snap) => {
        allUsers = snap.docs.map((d) => ({ id: d.id, ...d.data() })).filter((u) => u.id !== me.uid);
        $("real-users-grid").innerHTML = allUsers.length
          ? allUsers.map((u) => `
              <div class="bg-slate-900/80 border border-slate-700 rounded-xl p-4 flex flex-col justify-between gap-3">
                <div class="flex items-center gap-3">
                  <img src="${u.avatar || "https://api.dicebear.com/9.x/avataaars/svg?seed=" + u.id}" alt="" class="w-12 h-12 rounded-full object-cover border border-pink-500" />
                  <div>
                    <div class="font-bold text-sm">${u.name || "משתמש"} ${u.eliminated ? '<span class="text-rose-400 text-[11px]">(נפסל)</span>' : ""}</div>
                    <div class="text-xs text-slate-300">${u.gender || ""} • גיל ${u.age || 18} • ${u.city || ""}</div>
                  </div>
                </div>
                <p class="text-xs text-slate-400">${u.bio || "אין תיאור עדיין"}</p>
                <div class="flex gap-2">
                  <button type="button" data-dm-user="${u.id}" class="flex-1 py-1.5 rounded-lg text-xs font-semibold bg-pink-600">שיחה</button>
                  <button type="button" data-invite-user="${u.id}" class="flex-1 py-1.5 rounded-lg text-xs font-semibold bg-indigo-600">שולחן משחק</button>
                </div>
              </div>
            `).join("")
          : `<p class="text-xs text-slate-400 col-span-full">עדיין אין משתמשים אחרים רשומים במערכת.</p>`;

        document.querySelectorAll("[data-dm-user]").forEach((btn) => {
          btn.onclick = () => {
            const other = allUsers.find((x) => x.id === btn.dataset.dmUser);
            if (!other) return;
            const dmId = "dm_" + [me.uid, other.id].sort().join("_");
            if (!chatRooms.some((r) => r.id === dmId)) chatRooms.unshift({ id: dmId, topic: `שיחה עם ${other.name}` });
            activeRoomId = dmId;
            switchTab("chat");
            renderRooms();
          };
        });

        document.querySelectorAll("[data-invite-user]").forEach((btn) => {
          btn.onclick = () => switchTab("games");
        });
        syncArenasWithPlayers();
      });
    }

    function listenMsgs(roomId) {
      if (unsubMsgs) { unsubMsgs(); unsubMsgs = null; }
      const q = query(collection(db, "rooms", roomId, "messages"), orderBy("createdAt", "asc"));
      unsubMsgs = onSnapshot(q, (snap) => {
        const msgs = snap.docs.map((d) => d.data());
        $("chat-messages").innerHTML = msgs.length
          ? msgs.map((m) => `<div class="bg-slate-800 px-3 py-2 rounded-xl text-sm"><strong class="text-pink-300">${m.from || "משתמש"}:</strong> ${m.text || ""}</div>`).join("")
          : `<p class="text-xs text-slate-400">אין עדיין הודעות בחדר הזה.</p>`;
      });
    }

    function renderRooms() {
      $("rooms-list").innerHTML = chatRooms.map((r) => `
        <button type="button" data-room="${r.id}" class="w-full text-right p-3 rounded-xl border text-xs ${r.id === activeRoomId ? "bg-pink-600/30 border-pink-400" : "bg-slate-950/70 border-slate-800"}">
          💬 ${r.topic}
        </button>
      `).join("");
      document.querySelectorAll("[data-room]").forEach((b) => {
        b.onclick = () => { activeRoomId = b.dataset.room; renderRooms(); };
      });
      const cur = chatRooms.find((r) => r.id === activeRoomId) || chatRooms[0];
      $("active-room-title").textContent = cur.topic;
      $("active-room-meta").textContent = `חדר שיחה פעיל • ${cur.id}`;
      listenMsgs(cur.id);
    }

    $("create-room-form").onsubmit = async (e) => {
      e.preventDefault();
      const topic = $("new-room-topic").value.trim();
      if (!topic) return;
      const room = { id: `r-${Date.now()}`, topic };
      chatRooms.unshift(room);
      activeRoomId = room.id;
      $("new-room-topic").value = "";
      try { await setDoc(doc(db, "rooms", room.id), { ...room, createdAt: serverTimestamp() }, { merge: true }); } catch {}
      renderRooms();
    };

    $("chat-form").onsubmit = async (e) => {
      e.preventDefault();
      const txt = $("chat-input").value.trim();
      if (!txt) return;
      $("chat-input").value = "";
      await addDoc(collection(db, "rooms", activeRoomId, "messages"), { from: me.name, text: txt, createdAt: serverTimestamp() });
    };let currentGameType = "ttt";
    let allTables = [];
    let selectedTable = null;
    let unsubTableDoc = null;
    let isSubmittingMove = false;

    function getUserProfileByUid(uid) {
      if (!uid) return null;
      if (uid === me.uid) return me;
      return allUsers.find((u) => u.id === uid) || null;
    }

    function syncArenasWithPlayers() {
      const hostUid = selectedTable?.hostUid || me.uid;
      const guestUid = selectedTable?.guestUid || null;
      const hostProf = getUserProfileByUid(hostUid) || {
        name: selectedTable?.hostName || me.name,
        avatar: me.avatar
      };
      const guestProf = guestUid
        ? (getUserProfileByUid(guestUid) || {
            name: selectedTable?.guestName || "שחקן נוסף",
            avatar: `https://api.dicebear.com/9.x/avataaars/svg?seed=${encodeURIComponent(guestUid)}`
          })
        : null;

      $("ttt-host-img").src = hostProf.avatar;
      $("ttt-host-name").textContent = hostProf.name;
      if (guestProf) {
        $("ttt-guest-img").src = guestProf.avatar;
        $("ttt-guest-img").classList.remove("opacity-60", "border-slate-600");
        $("ttt-guest-img").classList.add("border-pink-400");
        $("ttt-guest-name").textContent = guestProf.name;
        $("ttt-guest-name").classList.remove("text-slate-400");
        $("ttt-guest-status").textContent = "יושב מול הקופסה ⭕";
        $("ttt-guest-status").className = "text-[11px] px-2 py-0.5 rounded-full bg-pink-500/20 text-pink-200";
      } else {
        $("ttt-guest-img").src = "https://api.dicebear.com/9.x/avataaars/svg?seed=Guest";
        $("ttt-guest-img").classList.add("opacity-60", "border-slate-600");
        $("ttt-guest-img").classList.remove("border-pink-400");
        $("ttt-guest-name").textContent = "ממתין לשחקן...";
        $("ttt-guest-name").classList.add("text-slate-400");
        $("ttt-guest-status").textContent = "טרם נכנס ⭕";
        $("ttt-guest-status").className = "text-[11px] px-2 py-0.5 rounded-full bg-slate-800 text-slate-400";
      }

      const opponentProf = selectedTable
        ? (selectedTable.hostUid === me.uid ? guestProf : hostProf)
        : (allUsers[0] || null);

      $("rps-p1-img").src = me.avatar;
      $("rps-p1-name").textContent = me.name;
      if (opponentProf) {
        $("rps-p2-img").src = opponentProf.avatar;
        $("rps-p2-img").classList.remove("opacity-60", "border-slate-600");
        $("rps-p2-img").classList.add("border-pink-400");
        $("rps-p2-name").textContent = opponentProf.name;
        $("rps-p2-name").classList.remove("text-slate-400");
        $("rps-vs-status").textContent = `${opponentProf.name} מולך בזירה`;
      } else {
        $("rps-p2-img").src = "https://api.dicebear.com/9.x/avataaars/svg?seed=P2";
        $("rps-p2-img").classList.add("opacity-60", "border-slate-600");
        $("rps-p2-img").classList.remove("border-pink-400");
        $("rps-p2-name").textContent = "ממתין ליריב...";
        $("rps-p2-name").classList.add("text-slate-400");
        $("rps-vs-status").textContent = "ברגע שייכנס משתמש — תופיע דמותו";
      }

      $("tod-p1-img").src = me.avatar;
      $("tod-p1-name").textContent = me.name;
      if (opponentProf) {
        $("tod-p2-img").src = opponentProf.avatar;
        $("tod-p2-img").classList.remove("opacity-60", "border-slate-600");
        $("tod-p2-name").textContent = opponentProf.name;
        $("tod-p2-name").classList.remove("text-slate-400");
      }

      if (opponentProf) {
        $("cards-opp-img").src = opponentProf.avatar;
        $("cards-opp-img").classList.remove("opacity-60");
        $("cards-opp-name").textContent = `${opponentProf.name} יושב מולך בשולחן`;
      } else {
        $("cards-opp-img").classList.add("opacity-60");
        $("cards-opp-name").textContent = "ממתין לשחקן שני בשולחן...";
      }
    }

    function canPlayInSelectedTable() {
      if (me.eliminated) return false;
      if (!selectedTable || isSubmittingMove) return false;
      if (!selectedTable.hostUid || !selectedTable.guestUid) return false;
      if (selectedTable.hostUid === selectedTable.guestUid) return false;
      return selectedTable.turnUid === me.uid;
    }

    function applyTurnLockToBoard() {
      const rrAllowed = !me.eliminated;
      $("rr-pull-btn").disabled = !rrAllowed;
      $("rr-spin-btn").disabled = !rrAllowed;
      $("rr-pull-btn").classList.toggle("opacity-50", !rrAllowed);
      $("rr-spin-btn").classList.toggle("opacity-50", !rrAllowed);

      const tttAllowed = canPlayInSelectedTable();
      document.querySelectorAll("#ttt-board button").forEach((el) => {
        el.disabled = !tttAllowed;
        el.classList.toggle("opacity-50", !tttAllowed);
      });

      const hasOpponent = Boolean(selectedTable && selectedTable.hostUid && selectedTable.guestUid && selectedTable.hostUid !== selectedTable.guestUid);
      const socialAllowed = !me.eliminated && (!selectedTable || hasOpponent);
      document.querySelectorAll(".rps-choice, #btn-truth, #btn-dare").forEach((el) => {
        el.disabled = !socialAllowed;
        el.classList.toggle("opacity-50", !socialAllowed);
      });

      if (me.eliminated) {
        $("turn-lock-banner").textContent = "נפסלת ברולטה רוסית — לחץ 'חזור למשחק' למעלה";
      } else if (!selectedTable) {
        $("turn-lock-banner").textContent = "בחר או פתח שולחן כדי לשחק מול משתמש";
      } else if (!selectedTable.guestUid) {
        $("turn-lock-banner").textContent = "ממתין למשתמש נוסף שייכנס מולך לשולחן...";
      } else if (tttAllowed) {
        $("turn-lock-banner").textContent = "תורך לשחק!";
      } else {
        $("turn-lock-banner").textContent = "ממתין לתור של המשתמש השני...";
      }
    }

    function renderTablesList() {
      const filtered = allTables.filter((t) => t.gameType === currentGameType);
      $("game-tables-list").innerHTML = filtered.length
        ? filtered.map((t) => {
            const isSel = selectedTable && selectedTable.id === t.id;
            const statusText = t.guestUid ? `${t.hostName} מול ${t.guestName}` : `ממתין למשתמש נוסף (שולחן של ${t.hostName})`;
            return `<button type="button" data-join-table="${t.id}" class="text-right p-3 rounded-xl border text-xs transition ${isSel ? "bg-pink-600/30 border-pink-400" : "bg-slate-900/80 border-slate-700 hover:border-pink-400/60"}">
              <div class="font-bold text-sm">🪑 שולחן של ${t.hostName || "משתמש"}</div>
              <div class="text-slate-300 mt-0.5">${statusText}</div>
            </button>`;
          }).join("")
        : `<p class="text-xs text-slate-400 col-span-full">אין שולחנות פתוחים למשחק זה עדיין. פתח שולחן משלך או הצטרף למשתמש אחר.</p>`;

      document.querySelectorAll("[data-join-table]").forEach((btn) => {
        btn.onclick = () => joinTableById(btn.dataset.joinTable);
      });
    }

    function subscribeGameTables() {
      onSnapshot(collection(db, "gameTables"), (snap) => {
        allTables = snap.docs.map((d) => ({ id: d.id, ...d.data() }));
        renderTablesList();
      });
    }

    async function joinTableById(tableId) {
      const t = allTables.find((x) => x.id === tableId);
      if (!t) return;
      if (t.hostUid !== me.uid && !t.guestUid) {
        await updateDoc(doc(db, "gameTables", t.id), { guestUid: me.uid, guestName: me.name });
      }
      if (unsubTableDoc) { unsubTableDoc(); unsubTableDoc = null; }
      unsubTableDoc = onSnapshot(doc(db, "gameTables", t.id), (snap) => {
        if (!snap.exists()) return;
        selectedTable = { id: snap.id, ...snap.data() };
        isSubmittingMove = false;
        $("selected-table-info").textContent = `שולחן: ${selectedTable.hostName} ${selectedTable.guestName ? "מול " + selectedTable.guestName : "(ממתין לשחקן שני)"}`;
        renderTttBoard(selectedTable.board || Array(9).fill(""));
        syncArenasWithPlayers();
        applyTurnLockToBoard();
        renderTablesList();
      });
    }

    $("create-my-table-btn").onclick = async () => {
      if (me.eliminated) return;
      const id = `tbl_${currentGameType}_${Date.now()}`;
      const newTbl = {
        gameType: currentGameType,
        hostUid: me.uid,
        hostName: me.name,
        guestUid: null,
        guestName: null,
        turnUid: me.uid,
        board: Array(9).fill(""),
        createdAt: serverTimestamp()
      };
      await setDoc(doc(db, "gameTables", id), newTbl);
      await joinTableById(id);
    };

    document.querySelectorAll(".game-tab-btn").forEach((btn) => {
      btn.onclick = () => {
        currentGameType = btn.dataset.game;
        document.querySelectorAll(".game-tab-btn").forEach((b) => {
          b.className = b.dataset.game === currentGameType
            ? "game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold bg-pink-600"
            : "game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold glass text-slate-300";
        });
        document.querySelectorAll(".game-panel").forEach((p) => p.classList.add("hidden"));
        $(`game-${currentGameType}`).classList.remove("hidden");
        renderTablesList();
        syncArenasWithPlayers();
      };
    });function checkTttWinner(b) {
      const lines = [[0,1,2],[3,4,5],[6,7,8],[0,3,6],[1,4,7],[2,5,8],[0,4,8],[2,4,6]];
      for (const [a, c, d] of lines) {
        if (b[a] && b[a] === b[c] && b[a] === b[d]) return b[a];
      }
      return b.every(Boolean) ? "DRAW" : null;
    }

    function renderTttBoard(board) {
      const el = $("ttt-board");
      if (!el) return;
      el.innerHTML = "";
      const winner = checkTttWinner(board);
      board.forEach((cell, idx) => {
        const btn = document.createElement("button");
        btn.type = "button";
        btn.className = "aspect-square rounded-xl bg-amber-900/80 border border-amber-500/40 text-xl font-bold flex items-center justify-center hover:border-pink-400";
        btn.textContent = cell === "X" ? "❌" : cell === "O" ? "⭕" : "";
        btn.onclick = async () => {
          if (!canPlayInSelectedTable() || board[idx] || winner) return;
          isSubmittingMove = true;
          const mark = selectedTable.hostUid === me.uid ? "X" : "O";
          const nextBoard = [...board];
          nextBoard[idx] = mark;
          const nextTurn = selectedTable.turnUid === selectedTable.hostUid ? selectedTable.guestUid : selectedTable.hostUid;
          await updateDoc(doc(db, "gameTables", selectedTable.id), { board: nextBoard, turnUid: nextTurn });
        };
        el.appendChild(btn);
      });

      if (!selectedTable) {
        $("ttt-status").textContent = "בחר שולחן של משתמש כדי לשחק מול קופסת המחסן";
      } else if (winner === "DRAW") {
        $("ttt-status").textContent = "תיקו! לחץ על איפוס לוח למשחק חדש";
      } else if (winner) {
        $("ttt-status").textContent = `המנצח במחסן: ${winner === "X" ? "❌ (" + selectedTable.hostName + ")" : "⭕ (" + (selectedTable.guestName || "אורח") + ")"}`;
      } else {
        const turnName = selectedTable.turnUid === selectedTable.hostUid ? selectedTable.hostName : (selectedTable.guestName || "ממתין לשחקן שני");
        $("ttt-status").textContent = `תור של: ${turnName}`;
      }
      applyTurnLockToBoard();
    }

    $("ttt-reset").onclick = async () => {
      if (!selectedTable) return;
      await updateDoc(doc(db, "gameTables", selectedTable.id), {
        board: Array(9).fill(""),
        turnUid: selectedTable.hostUid
      });
    };

    let rpsCounting = false;
    document.querySelectorAll(".rps-choice").forEach((btn) => {
      btn.onclick = () => {
        if (me.eliminated || rpsCounting) return;
        rpsCounting = true;
        const choices = ["rock", "paper", "scissors"];
        const labels = { rock: "🪨 אבן", paper: "📄 נייר", scissors: "✂️ מספריים" };
        const hands = { rock: "✊", paper: "✋", scissors: "✌️" };
        const userChoice = btn.dataset.rps;
        const botChoice = choices[Math.floor(Math.random() * 3)];

        $("rps-p1-hand").textContent = "✊";
        $("rps-p2-hand").textContent = "✊";
        const steps = ["אבן...", "נייר...", "מספריים!"];
        let stepIdx = 0;
        $("rps-counter-display").textContent = steps[0];
        $("rps-result").textContent = "הדמות סופרת... אבן, נייר, מספריים!";

        const timer = setInterval(() => {
          stepIdx += 1;
          if (stepIdx < steps.length) {
            $("rps-counter-display").textContent = steps[stepIdx];
          } else {
            clearInterval(timer);
            $("rps-counter-display").textContent = "חשיפה!";
            $("rps-p1-hand").textContent = hands[userChoice];
            $("rps-p2-hand").textContent = hands[botChoice];

            let outcome = "תיקו!";
            if (
              (userChoice === "rock" && botChoice === "scissors") ||
              (userChoice === "paper" && botChoice === "rock") ||
              (userChoice === "scissors" && botChoice === "paper")
            ) outcome = "ניצחת! 🎉";
            else if (userChoice !== botChoice) outcome = "הדמות שמולך ניצחה 😉";

            $("rps-result").textContent = `${labels[userChoice]} מול ${labels[botChoice]} — ${outcome}`;
            rpsCounting = false;
          }
        }, 420);
      };
    });

    const truths = ["מה הדייט הכי מצחיק שהיה לך?", "מה הדבר הספונטני האחרון שעשית?", "איזה שיר תמיד מכניס אותך למצב רוח טוב?"];
    const dares = ["שלח הודעה מצחיקה של שורה אחת לחבר/ה.", "כתוב מחמאה כנה לצד השני.", "ספר על מקום שבא לך לטייל בו השבוע."];
    $("btn-truth").onclick = () => { if (!me.eliminated) $("tod-text").textContent = "💭 אמת: " + truths[Math.floor(Math.random() * truths.length)]; };
    $("btn-dare").onclick = () => { if (!me.eliminated) $("tod-text").textContent = "⚡ חובה: " + dares[Math.floor(Math.random() * dares.length)]; };

    const suits = ["♠", "♥", "♦", "♣"];
    const ranks = ["A", "K", "Q", "J", "10", "9", "8", "7"];
    let satAtTable = false;
    let myHand = [];
    let oppCardCount = 0;
    let centerCard = null;

    function buildDeck() {
      const deck = [];
      for (const s of suits) {
        for (const r of ranks) deck.push({ r, s, isRed: s === "♥" || s === "♦" });
      }
      return deck.sort(() => Math.random() - 0.5);
    }

    function renderCardTable() {
      $("cards-opp-count").textContent = `${oppCardCount} קלפים ביד`;
      $("cards-opp-backs").innerHTML = Array.from({ length: oppCardCount }).map(() =>
        `<div class="w-6 h-9 rounded bg-gradient-to-br from-indigo-700 to-rose-800 border border-white/25"></div>`
      ).join("");

      if (centerCard) {
        $("cards-table-center").innerHTML = `
          <div class="w-full h-full rounded-xl bg-white text-slate-900 flex flex-col items-center justify-between p-1.5 shadow-md card-deal ${centerCard.isRed ? "text-rose-600" : "text-slate-900"}">
            <span class="text-xs font-bold self-start">${centerCard.r}${centerCard.s}</span>
            <span class="text-2xl">${centerCard.s}</span>
            <span class="text-xs font-bold self-end">${centerCard.r}${centerCard.s}</span>
          </div>
        `;
      } else {
        $("cards-table-center").innerHTML = `<span class="text-xs text-emerald-200">אין קלף על השולחן</span>`;
      }

      $("cards-my-hand").innerHTML = myHand.length
        ? myHand.map((c, idx) => `
            <button type="button" data-play-card="${idx}" class="w-16 h-24 rounded-xl bg-white shadow-md flex flex-col items-center justify-between p-1.5 card-deal hover:-translate-y-1.5 transition ${c.isRed ? "text-rose-600" : "text-slate-900"}">
              <span class="text-xs font-bold self-start">${c.r}${c.s}</span>
              <span class="text-2xl">${c.s}</span>
              <span class="text-xs font-bold self-end">${c.r}${c.s}</span>
            </button>
          `).join("")
        : `<span class="text-xs text-emerald-200/75">היד ריקה — לחץ "חלק קלפים" כדי לקבל קלפים</span>`;

      document.querySelectorAll("[data-play-card]").forEach((btn) => {
        btn.onclick = () => {
          if (me.eliminated) return;
          const idx = Number(btn.dataset.playCard);
          const [played] = myHand.splice(idx, 1);
          centerCard = played;
          if (oppCardCount > 0) oppCardCount -= 1;
          $("cards-status").textContent = `הנחת ${played.r}${played.s} במרכז השולחן!`;
          renderCardTable();
        };
      });
    }

    $("cards-sit-btn").onclick = () => {
      if (me.eliminated) return;
      satAtTable = true;
      $("cards-status").textContent = `${me.name} התיישב לשולחן הקלפים! לחץ "חלק קלפים".`;
    };

    $("cards-deal-btn").onclick = () => {
      if (me.eliminated) return;
      if (!satAtTable) satAtTable = true;
      const deck = buildDeck();
      myHand = deck.slice(0, 5);
      oppCardCount = 5;
      centerCard = null;
      $("cards-status").textContent = `חולקו 5 קלפים לשולחן! לחץ על קלף ביד כדי להוריד אותו למרכז.`;
      renderCardTable();
    };
    renderCardTable();

    let bulletChamber = Math.floor(Math.random() * 6);
    let currentChamber = 0;

    function launchConfetti() {
      const layer = $("confetti-layer");
      const colors = ["#ec4899", "#f59e0b", "#10b981", "#6366f1", "#f43f5e", "#38bdf8"];
      for (let i = 0; i < 42; i++) {
        const piece = document.createElement("div");
        piece.className = "confetti-piece";
        piece.style.left = `${Math.random() * 100}%`;
        piece.style.backgroundColor = colors[i % colors.length];
        piece.style.animationDelay = `${Math.random() * 0.25}s`;
        piece.style.animationDuration = `${1.2 + Math.random() * 0.8}s`;
        layer.appendChild(piece);
        setTimeout(() => piece.remove(), 2100);
      }
    }

    $("rr-spin-btn").onclick = () => {
      if (me.eliminated) return;
      bulletChamber = Math.floor(Math.random() * 6);
      currentChamber = 0;
      $("rr-chamber-info").textContent = "התוף סובב מחדש! מוכן ללחיצה";
      $("rr-status").textContent = "🔄 התוף סובב. הדמות מקרבת את האקדח לראש...";
    };

    $("rr-reset-btn").onclick = async () => {
      bulletChamber = Math.floor(Math.random() * 6);
      currentChamber = 0;
      me.eliminated = false;
      $("rr-gun-icon").textContent = "🔫";
      $("rr-gun-icon").classList.add("gun-aim");
      $("rr-char-state").textContent = "במשחק • אקדח מכוון";
      $("rr-char-state").className = "text-xs px-2.5 py-0.5 rounded-full bg-emerald-500/20 text-emerald-200";
      $("rr-chamber-info").textContent = "סיבוב חדש אופס (6 תאים)";
      $("rr-status").textContent = "הסיבוב אופס והדמות חזרה למשחק.";
      syncEliminationUI();
      try { await setDoc(doc(db, "users", me.uid), { eliminated: false }, { merge: true }); } catch {}
    };

    $("rr-pull-btn").onclick = async () => {
      if (me.eliminated) return;
      $("rr-gun-icon").textContent = "🔫";
      if (currentChamber === bulletChamber) {
        launchConfetti();
        me.eliminated = true;
        $("rr-gun-icon").textContent = "💥";
        $("rr-gun-icon").classList.remove("gun-aim");
        $("rr-char-state").textContent = "נפסל • מחוץ לשאר המשחקים";
        $("rr-char-state").className = "text-xs px-2.5 py-0.5 rounded-full bg-rose-500/30 text-rose-200";
        $("rr-chamber-info").textContent = `תא ${currentChamber + 1}/6 — בום!`;
        $("rr-status").textContent = `🎉💥 האקדח ירה בתא ${currentChamber + 1}! יצא קונפטי ו-${me.name} נפסל משאר המשחקים.`;
        syncEliminationUI();
        try { await setDoc(doc(db, "users", me.uid), { eliminated: true }, { merge: true }); } catch {}
      } else {
        $("rr-status").textContent = `😅 קליק! תא ${currentChamber + 1}/6 ריק — הדמות שרדה את הלחיצה הזו.`;
        currentChamber = (currentChamber + 1) % 6;
        $("rr-chamber-info").textContent = `תא הבא: ${currentChamber + 1}/6`;
      }
    };

    const savedSession = localStorage.getItem("toplove_session");
    if (savedSession) {
      try { openApp(JSON.parse(savedSession)); } catch {}
    }
  </script>
</body>
</html>
