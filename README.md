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
      background: rgba(30, 41, 59, 0.82);
      backdrop-filter: blur(12px);
      border: 1px solid rgba(255, 255, 255, 0.14);
    }
    @keyframes countPulse {
      0% { transform: scale(0.85); opacity: 0.5; }
      60% { transform: scale(1.12); opacity: 1; }
      100% { transform: scale(1); opacity: 1; }
    }
    .count-anim { animation: countPulse 0.35s ease-out; }
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
    <div class="flex flex-wrap items-center gap-2.5">
      <span id="header-stats" class="hidden text-xs font-bold bg-amber-500/20 border border-amber-400/40 text-amber-200 px-3 py-1 rounded-full">
        רמה 1 • 0 נק׳ • 0 נצ׳ / 0 הפס׳
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
        <button type="button" data-tab="games" class="tab-btn px-4 py-2 rounded-xl text-sm font-semibold glass text-slate-300">4. משחקים 🎮</button>
      </div><div id="tab-profile" class="tab-content max-w-4xl mx-auto glass rounded-3xl p-6 sm:p-8 shadow-2xl space-y-6">
        <div class="flex flex-wrap items-center justify-between gap-3 border-b border-white/10 pb-4">
          <div>
            <h2 class="text-2xl font-bold">הפרופיל האישי שלי</h2>
            <p class="text-xs text-slate-300 mt-1">כל השדות אופציונליים — בחר מה שמתאים לך ושמור</p>
          </div>
          <button type="button" id="edit-profile-btn" class="hidden px-4 py-2 rounded-xl text-xs font-semibold bg-slate-800 hover:bg-slate-700 border border-slate-600">
            ✏️ ערוך פרופיל
          </button>
        </div>

        <div id="profile-summary-card" class="hidden bg-slate-900/80 border border-pink-500/30 rounded-2xl p-6 space-y-6">
          <div class="flex flex-col sm:flex-row items-center gap-6">
            <img id="summary-avatar" src="https://api.dicebear.com/9.x/avataaars/svg?seed=TopLove" alt="תמונת פרופיל"
              class="w-32 h-32 rounded-2xl object-cover border-2 border-pink-400 bg-slate-800 shrink-0 shadow-lg" />
            <div class="space-y-2 text-center sm:text-right flex-1">
              <div class="flex flex-wrap items-center justify-center sm:justify-start gap-2">
                <h3 id="summary-name" class="text-2xl font-bold text-white"></h3>
                <span id="summary-age-gender" class="text-xs px-3 py-1 rounded-full bg-pink-500/20 text-pink-200 border border-pink-400/30"></span>
              </div>
              <p id="summary-location" class="text-sm text-indigo-200 font-medium"></p>
              <p id="summary-bio" class="text-sm text-slate-300 leading-relaxed"></p>
            </div>
          </div>

          <div class="grid grid-cols-1 md:grid-cols-3 gap-4 pt-2 border-t border-white/10">
            <div class="bg-slate-950/70 rounded-xl p-4 border border-slate-800 space-y-2">
              <div class="text-xs font-bold text-pink-300">✨ מה אני אוהב/ת לעשות</div>
              <div id="summary-likes" class="flex flex-wrap gap-1.5 text-xs text-slate-200"></div>
            </div>
            <div class="bg-slate-950/70 rounded-xl p-4 border border-slate-800 space-y-2">
              <div class="text-xs font-bold text-indigo-300">🎯 תחביבים</div>
              <div id="summary-hobbies" class="flex flex-wrap gap-1.5 text-xs text-slate-200"></div>
            </div>
            <div class="bg-slate-950/70 rounded-xl p-4 border border-slate-800 space-y-2">
              <div class="text-xs font-bold text-emerald-300">🎓 השכלה</div>
              <div id="summary-education" class="text-xs text-slate-200"></div>
            </div>
          </div>
        </div>

        <form id="profile-form" class="space-y-6">
          <div class="flex flex-col md:flex-row items-center gap-6 bg-slate-900/75 p-5 rounded-2xl border border-slate-700">
            <img id="prof-avatar-preview" src="https://api.dicebear.com/9.x/avataaars/svg?seed=TopLove" alt="תמונת פרופיל"
              class="w-28 h-28 rounded-2xl object-cover border-2 border-pink-500 bg-slate-800 shrink-0 shadow-md" />
            <div class="w-full space-y-3">
              <label class="block text-sm font-semibold text-pink-300">בחירת תמונת פרופיל מהמחשב או קישור</label>
              <input type="file" id="prof-avatar-file" accept="image/*"
                class="block w-full text-xs text-slate-300 file:ml-3 file:py-2 file:px-4 file:rounded-xl file:border-0 file:bg-pink-600 file:text-white file:font-semibold" />
              <input type="url" id="prof-avatar-url" placeholder="קישור לתמונה (https://...)" dir="ltr"
                class="w-full px-4 py-2 text-sm rounded-xl bg-slate-950 border border-slate-700 text-left" />
            </div>
          </div>

          <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-3.5">
            <div>
              <label class="block text-xs text-slate-300 mb-1">שם משתמש / כינוי</label>
              <input type="text" id="prof-name" placeholder="שם משתמש"
                class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700 text-sm" />
            </div>
            <div>
              <label class="block text-xs text-slate-300 mb-1">מין / מגדר</label>
              <select id="prof-gender" class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700 text-sm">
                <option value="">לא צוין</option>
                <option value="גבר">גבר</option>
                <option value="אישה">אישה</option>
                <option value="אחר">אחר</option>
              </select>
            </div>
            <div>
              <label class="block text-xs text-slate-300 mb-1">בן/בת כמה (18+)</label>
              <input type="number" id="prof-age" min="18" max="99" placeholder="גיל"
                class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700 text-sm" />
            </div>
            <div>
              <label class="block text-xs text-slate-300 mb-1">מדינה</label>
              <input type="text" id="prof-country" placeholder="למשל: ישראל"
                class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700 text-sm" />
            </div>
          </div>

          <div class="grid grid-cols-1 sm:grid-cols-2 gap-3.5">
            <div>
              <label class="block text-xs text-slate-300 mb-1">עיר / יישוב</label>
              <input type="text" id="prof-city" placeholder="למשל: תל אביב / כרמיאל"
                class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700 text-sm" />
            </div>
            <div>
              <label class="block text-xs text-slate-300 mb-1">השכלה (לא חובה)</label>
              <input type="text" id="prof-education" placeholder="למשל: תואר ראשון, הנדסאי, תיכון..."
                class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700 text-sm" />
            </div>
          </div>

          <div class="bg-slate-900/70 p-4 rounded-2xl border border-slate-800 space-y-2.5">
            <label class="block text-sm font-bold text-pink-300">מה אתה אוהב לעשות? (לא חובה)</label>
            <div id="likes-options" class="flex flex-wrap gap-2"></div>
          </div>

          <div class="bg-slate-900/70 p-4 rounded-2xl border border-slate-800 space-y-2.5">
            <label class="block text-sm font-bold text-indigo-300">מה התחביבים שלך? (לא חובה)</label>
            <div id="hobbies-options" class="flex flex-wrap gap-2"></div>
          </div>

          <div>
            <label class="block text-xs text-slate-300 mb-1">כמה מילים עליי (לא חובה)</label>
            <textarea id="prof-bio" rows="2" placeholder="ספר בקצרה על עצמך..."
              class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700 text-sm"></textarea>
          </div>

          <p id="profile-error" class="text-rose-400 text-xs hidden"></p>
          <div class="flex items-center justify-between">
            <span id="save-feedback" class="text-emerald-400 text-sm opacity-0 transition-opacity">✓ נשמר והועבר לפרופיל!</span>
            <button type="submit" class="px-7 py-3 rounded-xl font-semibold bg-gradient-to-l from-pink-600 to-indigo-600 shadow-lg">
              שמור פרופיל
            </button>
          </div>
        </form>
      </div><div id="tab-users" class="tab-content hidden max-w-4xl mx-auto glass rounded-2xl p-6 space-y-4">
        <h2 class="text-xl font-bold">👥 משתמשים אמיתיים במערכת</h2>
        <div id="real-users-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4"></div>
      </div>

      <div id="tab-chat" class="tab-content hidden max-w-5xl mx-auto glass rounded-2xl p-6 space-y-5">
        <div class="bg-slate-900/80 border border-slate-700 rounded-xl p-4 space-y-3">
          <h3 class="text-sm font-bold text-pink-300">➕ פתיחת חדר שיחה חדש (עד 50 משתתפים בחדר)</h3>
          <form id="create-room-form" class="flex flex-col sm:flex-row gap-2.5">
            <input type="text" id="new-room-topic" required placeholder="שם / נושא החדר החדש..."
              class="flex-1 px-3.5 py-2 rounded-xl bg-slate-950 border border-slate-700 text-sm" />
            <button type="submit" class="px-5 py-2 rounded-xl text-sm font-semibold bg-gradient-to-l from-pink-600 to-indigo-600">
              פתח חדר שיחה
            </button>
          </form>
        </div>

        <div class="grid grid-cols-1 lg:grid-cols-3 gap-5">
          <div class="space-y-2">
            <h3 class="text-sm font-bold text-slate-200">🗂️ חדרי שיחה (מקס׳ 50 משתתפים)</h3>
            <div id="rooms-list" class="space-y-2 max-h-96 overflow-y-auto"></div>
          </div>

          <div class="lg:col-span-2 bg-slate-900/70 border border-slate-800 rounded-2xl p-4 flex flex-col justify-between min-h-[380px] space-y-3">
            <div class="border-b border-white/10 pb-2 flex flex-wrap items-center justify-between gap-2">
              <div>
                <h3 id="active-room-title" class="font-bold text-base">בחר חדר</h3>
                <p id="active-room-meta" class="text-xs text-slate-400">חדר שיחה פתוח</p>
              </div>
              <span id="room-capacity-badge" class="text-xs px-3 py-1 rounded-full bg-indigo-500/20 border border-indigo-400/40 text-indigo-200">
                0 / 50 משתתפים
              </span>
            </div>

            <div id="chat-messages" class="space-y-2 max-h-60 overflow-y-auto py-1"></div>

            <div class="space-y-2 pt-2 border-t border-white/10">
              <div class="flex flex-wrap items-center justify-between gap-2">
                <button type="button" id="record-voice-btn" class="px-4 py-1.5 rounded-xl text-xs font-semibold bg-amber-600 hover:bg-amber-500">
                  🎤 התחל הקלטה
                </button>
                <span id="voice-status" class="text-xs text-slate-300">אפשר לשלוח גם הודעה קולית</span>
              </div>

              <form id="chat-form" class="flex gap-2">
                <input type="text" id="chat-input" required placeholder="כתוב הודעה בחדר..."
                  class="flex-1 px-4 py-2 rounded-xl bg-slate-950 border border-slate-700 text-sm" />
                <button type="submit" class="px-5 py-2 rounded-xl text-sm font-semibold bg-pink-600">שלח</button>
              </form>
            </div>
          </div>
        </div>
      </div><div id="tab-games" class="tab-content hidden space-y-6">
        <div class="glass rounded-2xl p-4 sm:p-5 border border-amber-400/30 space-y-4">
          <div class="grid grid-cols-2 sm:grid-cols-4 gap-3 text-center">
            <div class="bg-slate-900/85 rounded-xl p-3 border border-slate-700">
              <div class="text-xs text-slate-400">רמה נוכחית</div>
              <div id="stat-level" class="text-xl font-extrabold text-pink-300 mt-0.5">רמה 1</div>
            </div>
            <div class="bg-slate-900/85 rounded-xl p-3 border border-slate-700">
              <div class="text-xs text-slate-400">נקודות</div>
              <div id="stat-points" class="text-xl font-extrabold text-amber-300 mt-0.5">0</div>
            </div>
            <div class="bg-slate-900/85 rounded-xl p-3 border border-slate-700">
              <div class="text-xs text-slate-400">ניצחונות</div>
              <div id="stat-wins" class="text-xl font-extrabold text-emerald-300 mt-0.5">0</div>
            </div>
            <div class="bg-slate-900/85 rounded-xl p-3 border border-slate-700">
              <div class="text-xs text-slate-400">הפסדים</div>
              <div id="stat-losses" class="text-xl font-extrabold text-rose-300 mt-0.5">0</div>
            </div>
          </div>

          <div class="bg-slate-950/70 rounded-xl p-3.5 border border-indigo-500/25 flex flex-wrap items-center justify-between gap-3">
            <div class="flex items-center gap-2">
              <span class="text-xl">🎁</span>
              <div>
                <div class="text-xs font-bold text-indigo-200">ארון פרסים ותגמולים (תצוגה מקדימה)</div>
                <div class="text-[11px] text-slate-400">הפרסים הסופיים ייקבעו בהמשך — בינתיים צוברים רמות ונקודות</div>
              </div>
            </div>
            <div class="flex items-center gap-2 text-xs">
              <span class="px-2.5 py-1 rounded-lg bg-slate-800 border border-slate-700 text-slate-300">🥉 פרס רמה 1</span>
              <span class="px-2.5 py-1 rounded-lg bg-slate-800 border border-slate-700 text-slate-300">🥈 פרס רמה 3</span>
              <span class="px-2.5 py-1 rounded-lg bg-slate-800 border border-slate-700 text-slate-300">🥇 פרס רמה 5</span>
            </div>
          </div>
        </div>

        <div class="flex flex-wrap gap-2 justify-center">
          <button type="button" data-game="ttt" class="game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold bg-pink-600">1. איקס עיגול (100+ חדרים)</button>
          <button type="button" data-game="rps" class="game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold glass text-slate-300">2. אבן נייר מספריים</button>
          <button type="button" data-game="memory" class="game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold glass text-slate-300">3. זיכרון קשה (50+ חדרים • עד 6)</button>
          <button type="button" data-game="number" class="game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold glass text-slate-300">4. ניחוש מספר</button>
        </div>

        <div id="game-ttt" class="game-panel max-w-4xl mx-auto glass rounded-2xl p-6 space-y-5">
          <div class="flex flex-wrap items-center justify-between gap-2 border-b border-white/10 pb-3">
            <div>
              <h3 class="text-xl font-bold">📦 איקס עיגול — חדרים פעילים (100 חדרים)</h3>
              <p class="text-xs text-slate-300">לחץ על חדר פנוי כדי להיכנס ולהמתין שמישהו ילחץ להצטרף מולך</p>
            </div>
            <div class="flex flex-wrap items-center gap-2">
              <span id="ttt-timer" class="px-3 py-1 rounded-full text-xs font-bold bg-amber-500/20 border border-amber-400/40 text-amber-200">⏱️ 00:30</span>
              <button type="button" id="ttt-add-room" class="px-3.5 py-1.5 rounded-xl text-xs font-semibold bg-emerald-600 hover:bg-emerald-500">+ הוסף חדר נוסף</button>
              <button type="button" id="ttt-leave-room" class="hidden px-3 py-1.5 rounded-xl text-xs font-semibold bg-rose-600 hover:bg-rose-500">צא מהחדר</button>
            </div>
          </div>

          <div id="ttt-rooms-grid" class="grid grid-cols-2 sm:grid-cols-4 md:grid-cols-5 gap-2 max-h-56 overflow-y-auto p-1"></div>

          <div class="bg-slate-950/75 border border-amber-500/25 rounded-2xl p-4 space-y-4">
            <div class="grid grid-cols-3 items-center gap-2 text-center">
              <div class="flex flex-col items-center gap-1">
                <div class="w-12 h-12 rounded-full border-2 border-amber-400 bg-slate-800 flex items-center justify-center text-lg">❌</div>
                <span id="ttt-p1-name" class="text-xs font-bold text-slate-300">ריק</span>
              </div>
              <div id="ttt-board" class="grid grid-cols-3 gap-1.5 bg-amber-950/70 p-2.5 rounded-xl border border-amber-700/60 max-w-[220px] w-full mx-auto"></div>
              <div class="flex flex-col items-center gap-1">
                <div class="w-12 h-12 rounded-full border-2 border-pink-400 bg-slate-800 flex items-center justify-center text-lg">⭕</div>
                <span id="ttt-p2-name" class="text-xs font-bold text-slate-400">ממתין לכניסה...</span>
              </div>
            </div>
            <div class="flex flex-wrap items-center justify-between gap-2">
              <p id="ttt-status" class="text-sm text-pink-200">לחץ על אחד החדרים למעלה כדי להיכנס</p>
              <button type="button" id="ttt-reset" class="text-xs bg-slate-800 px-3 py-1.5 rounded-lg border border-slate-600">איפוס לוח</button>
            </div>
          </div>
        </div>

        <div id="game-rps" class="game-panel hidden max-w-2xl mx-auto glass rounded-2xl p-6 space-y-4 text-center">
          <div class="flex flex-wrap items-center justify-between gap-2">
            <h3 class="text-xl font-bold">✂️ אבן נייר מספריים</h3>
            <div class="flex items-center gap-2">
              <span id="rps-timer" class="px-3 py-1 rounded-full text-xs font-bold bg-pink-500/20 border border-pink-400/40 text-pink-200">⏱️ 00:15</span>
              <button type="button" id="rps-join-btn" class="px-3.5 py-1.5 rounded-xl text-xs font-semibold bg-emerald-600 hover:bg-emerald-500">
                היכנס לשחק
              </button>
              <button type="button" id="rps-leave-btn" class="hidden px-3 py-1.5 rounded-xl text-xs font-semibold bg-rose-600 hover:bg-rose-500">
                צא מהמשחק
              </button>
            </div>
          </div>

          <div class="grid grid-cols-3 items-center gap-3 bg-slate-950/70 border border-white/10 rounded-2xl p-4">
            <div class="flex flex-col items-center gap-1.5">
              <div id="rps-left-avatar" class="w-14 h-14 rounded-full border-2 border-pink-400 bg-slate-800 flex items-center justify-center text-xl">🪑</div>
              <span id="rps-left-name" class="text-xs font-bold text-slate-400">מושב 1 פנוי</span>
              <div id="rps-left-sign" class="w-16 h-16 rounded-2xl bg-slate-900 border border-slate-700 flex items-center justify-center text-3xl">✊</div>
            </div>

            <div class="flex flex-col items-center justify-center gap-1">
              <span class="text-xs text-slate-400">ספירה:</span>
              <div id="rps-count-num" class="text-3xl font-extrabold text-pink-300 count-anim">1 • 2 • 3</div>
              <span id="rps-round-phase" class="text-xs text-indigo-200">ממתין לשני שחקנים</span>
            </div>

            <div class="flex flex-col items-center gap-1.5">
              <div id="rps-right-avatar" class="w-14 h-14 rounded-full border-2 border-indigo-400 bg-slate-800 flex items-center justify-center text-xl">🪑</div>
              <span id="rps-right-name" class="text-xs font-bold text-slate-400">מושב 2 פנוי</span>
              <div id="rps-right-sign" class="w-16 h-16 rounded-2xl bg-slate-900 border border-slate-700 flex items-center justify-center text-3xl">✊</div>
            </div>
          </div>

          <div class="flex justify-center gap-3">
            <button type="button" data-rps="rock" class="rps-choice px-5 py-3 rounded-xl bg-slate-800 hover:bg-pink-600 text-base font-semibold">🪨 אבן</button>
            <button type="button" data-rps="paper" class="rps-choice px-5 py-3 rounded-xl bg-slate-800 hover:bg-pink-600 text-base font-semibold">📄 נייר</button>
            <button type="button" data-rps="scissors" class="rps-choice px-5 py-3 rounded-xl bg-slate-800 hover:bg-pink-600 text-base font-semibold">✂️ מספריים</button>
          </div>
          <p id="rps-result" class="text-sm text-pink-200 bg-slate-900 p-3.5 rounded-xl">לחץ "היכנס לשחק" והמתן ששחקן נוסף ילחץ להיכנס מולך</p>
        </div><div id="game-memory" class="game-panel hidden max-w-4xl mx-auto glass rounded-2xl p-6 space-y-4">
          <div class="flex flex-wrap items-center justify-between gap-2 border-b border-white/10 pb-3">
            <div>
              <h3 class="text-xl font-bold">💎 זיכרון קשה — 50 חדרים (עד 6 שחקנים בחדר)</h3>
              <p class="text-xs text-slate-300">לוח 6×6 מאתגר עם אימוג'ים דומים — עד 6 שחקנים מתחרים על נקודות באותו חדר</p>
            </div>
            <div class="flex flex-wrap items-center gap-2">
              <span id="memory-timer" class="px-3 py-1 rounded-full text-xs font-bold bg-emerald-500/20 border border-emerald-400/40 text-emerald-200">⏱️ 02:00</span>
              <button type="button" id="memory-leave-room" class="hidden px-3 py-1.5 rounded-xl text-xs font-semibold bg-rose-600 hover:bg-rose-500">צא מהחדר</button>
              <button type="button" id="memory-reset" class="text-xs bg-pink-600 px-3.5 py-1.5 rounded-xl font-semibold">ערבב לוח</button>
            </div>
          </div>

          <div id="memory-rooms-grid" class="grid grid-cols-2 sm:grid-cols-5 md:grid-cols-10 gap-1.5 max-h-40 overflow-y-auto p-1"></div>

          <div id="memory-players-board" class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-6 gap-2 bg-slate-950/75 p-3 rounded-xl border border-white/10 text-xs"></div>

          <div id="memory-grid" class="grid grid-cols-6 gap-2 max-w-xl mx-auto"></div>
          <p id="memory-status" class="text-sm text-center text-pink-200">בחר אחד מ-50 חדרי הזיכרון כדי להצטרף (עד 6 שחקנים)</p>
        </div>

        <div id="game-number" class="game-panel hidden max-w-2xl mx-auto glass rounded-2xl p-6 space-y-4">
          <div class="border-b border-white/10 pb-3">
            <h3 class="text-xl font-bold">🎯 ניחוש מספר — חדרים ומנהל חדר</h3>
            <p class="text-xs text-slate-300">פתח חדר עם טווח מספרים, מנהל החדר קובע מספר בשקט והמשתתפים מנחשים</p>
          </div>

          <form id="num-create-room-form" class="flex flex-col sm:flex-row gap-2.5 bg-slate-900/75 p-3.5 rounded-xl border border-slate-700">
            <input type="text" id="num-room-name" required placeholder="שם חדר ניחוש מספר..."
              class="flex-1 px-3.5 py-2 rounded-xl bg-slate-950 border border-slate-700 text-sm" />
            <input type="number" id="num-room-max" min="50" max="10000" value="1000" required
              class="w-32 px-3.5 py-2 rounded-xl bg-slate-950 border border-slate-700 text-sm text-center" />
            <button type="submit" class="px-4 py-2 rounded-xl text-xs font-semibold bg-emerald-600 hover:bg-emerald-500">
              פתח חדר
            </button>
          </form>

          <div id="num-rooms-list" class="grid grid-cols-1 sm:grid-cols-2 gap-2.5"></div>

          <div class="bg-slate-950/75 border border-indigo-500/30 rounded-2xl p-4 space-y-4">
            <div class="flex flex-wrap items-center justify-between gap-2">
              <div id="num-room-header" class="font-bold text-sm text-pink-200"></div>
              <div id="num-host-badge" class="text-xs px-3 py-1 rounded-full bg-indigo-500/20 text-indigo-200"></div>
            </div>

            <div class="bg-slate-900/90 border border-amber-500/30 rounded-xl p-3.5 space-y-2">
              <div class="flex items-center justify-between">
                <span class="text-xs font-bold text-amber-300">🤫 בחירת מספר סודי על ידי מנהל החדר (בשקט)</span>
                <button type="button" id="num-toggle-secret" class="text-xs text-slate-300 underline">הצג/הסתר למנהל</button>
              </div>
              <div class="flex flex-wrap gap-2 items-center">
                <input type="password" id="num-secret-input" placeholder="הכנס מספר סודי בשקט..."
                  class="flex-1 min-w-[160px] px-3 py-2 rounded-xl bg-slate-950 border border-slate-700 text-sm" />
                <button type="button" id="num-set-secret-btn" class="px-4 py-2 rounded-xl text-xs font-semibold bg-amber-600 hover:bg-amber-500">
                  קבע מספר סודי
                </button>
              </div>
              <p id="num-secret-status" class="text-xs text-emerald-300"></p>
            </div>

            <div class="space-y-2.5">
              <div class="flex flex-wrap gap-2 items-center">
                <input type="number" id="num-guess-input" placeholder="הכנס ניחוש..."
                  class="flex-1 min-w-[140px] px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700 text-sm" />
                <button type="button" id="num-guess-btn" class="px-5 py-2.5 rounded-xl text-sm font-semibold bg-pink-600 hover:bg-pink-500">
                  בדוק ניחוש
                </button>
              </div>
              <p id="num-guess-feedback" class="text-sm font-medium text-pink-200 bg-slate-900 p-3 rounded-xl"></p>
              <div id="num-guesses-log" class="space-y-1.5 max-h-40 overflow-y-auto text-xs"></div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </main><script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/11.0.0/firebase-app.js";
    import { getAnalytics } from "https://www.gstatic.com/firebasejs/11.0.0/firebase-analytics.js";
    import {
      getFirestore, collection, doc, setDoc, addDoc,
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
    const MAX_ROOM_USERS = 50;

    const likesChoices = ["לצאת לבתי קפה", "לראות סרטים וסדרות", "להכיר אנשים חדשים", "מוזיקה חיה והופעות", "אוכל טוב ומסעדות", "שיחות עמוקות וצחוק"];
    const hobbiesChoices = ["טיולים", "ספורט וכושר", "צילום", "בישול ואפייה", "גיימינג", "קריאה", "ריקוד", "נגינה"];

    const me = {
      uid: "", email: "", name: "", gender: "", age: 18,
      country: "", city: "", education: "", bio: "",
      likes: [], hobbies: [],
      avatar: "https://api.dicebear.com/9.x/avataaars/svg?seed=TopLove",
      profileCompleted: false,
      points: 0,
      wins: 0,
      losses: 0
    };

    function getLevel(pts) {
      return Math.floor((pts || 0) / 100) + 1;
    }

    function renderStats() {
      const lvl = getLevel(me.points);
      $("stat-level").textContent = `רמה ${lvl}`;
      $("stat-points").textContent = String(me.points || 0);
      $("stat-wins").textContent = String(me.wins || 0);
      $("stat-losses").textContent = String(me.losses || 0);
      $("header-stats").textContent = `רמה ${lvl} • ${me.points || 0} נק׳ • ${me.wins || 0} נצ׳ / ${me.losses || 0} הפס׳`;
      localStorage.setItem("toplove_session", JSON.stringify(me));
    }

    async function awardWin(pts = 25) {
      me.wins = (me.wins || 0) + 1;
      me.points = (me.points || 0) + pts;
      renderStats();
      try { if (me.uid) await setDoc(doc(db, "users", me.uid), { points: me.points, wins: me.wins }, { merge: true }); } catch {}
    }

    async function awardLoss(pts = 5) {
      me.losses = (me.losses || 0) + 1;
      me.points = (me.points || 0) + pts;
      renderStats();
      try { if (me.uid) await setDoc(doc(db, "users", me.uid), { points: me.points, losses: me.losses }, { merge: true }); } catch {}
    }function renderQuestionnaireOptions() {
      $("likes-options").innerHTML = likesChoices.map((item) => {
        const active = me.likes.includes(item);
        return `<button type="button" data-like="${item}" class="px-3 py-1.5 rounded-full text-xs border transition ${active ? "bg-pink-600 border-pink-400 text-white" : "bg-slate-950 border-slate-700 text-slate-300"}">${item}</button>`;
      }).join("");
      $("likes-options").querySelectorAll("[data-like]").forEach((btn) => {
        btn.onclick = () => {
          const val = btn.dataset.like;
          me.likes = me.likes.includes(val) ? me.likes.filter((x) => x !== val) : [...me.likes, val];
          renderQuestionnaireOptions();
        };
      });

      $("hobbies-options").innerHTML = hobbiesChoices.map((item) => {
        const active = me.hobbies.includes(item);
        return `<button type="button" data-hobby="${item}" class="px-3 py-1.5 rounded-full text-xs border transition ${active ? "bg-indigo-600 border-indigo-400 text-white" : "bg-slate-950 border-slate-700 text-slate-300"}">${item}</button>`;
      }).join("");
      $("hobbies-options").querySelectorAll("[data-hobby]").forEach((btn) => {
        btn.onclick = () => {
          const val = btn.dataset.hobby;
          me.hobbies = me.hobbies.includes(val) ? me.hobbies.filter((x) => x !== val) : [...me.hobbies, val];
          renderQuestionnaireOptions();
        };
      });
    }

    function applyProfileViewMode() {
      const showSummary = Boolean(me.profileCompleted);
      $("profile-summary-card").classList.toggle("hidden", !showSummary);
      $("profile-form").classList.toggle("hidden", showSummary);
      $("edit-profile-btn").classList.toggle("hidden", !showSummary);

      if (showSummary) {
        $("summary-avatar").src = me.avatar;
        $("summary-name").textContent = me.name || "משתמש";
        const metaParts = [];
        if (me.gender) metaParts.push(me.gender);
        if (me.age) metaParts.push(`גיל ${me.age}`);
        $("summary-age-gender").textContent = metaParts.join(" • ") || "18+";
        const locParts = [me.country, me.city].filter(Boolean);
        $("summary-location").textContent = locParts.length ? `📍 ${locParts.join(", ")}` : "";
        $("summary-bio").textContent = me.bio || "";
        $("summary-likes").innerHTML = me.likes.length
          ? me.likes.map((l) => `<span class="px-2.5 py-1 rounded-full bg-pink-500/20 border border-pink-400/30">${l}</span>`).join("")
          : `<span class="text-slate-400">לא נבחרו פריטים</span>`;
        $("summary-hobbies").innerHTML = me.hobbies.length
          ? me.hobbies.map((h) => `<span class="px-2.5 py-1 rounded-full bg-indigo-500/20 border border-indigo-400/30">${h}</span>`).join("")
          : `<span class="text-slate-400">לא נבחרו תחביבים</span>`;
        $("summary-education").textContent = me.education || "לא צוינה השכלה";
      }
    }

    $("edit-profile-btn").onclick = () => { me.profileCompleted = false; applyProfileViewMode(); };

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
      me.likes = Array.isArray(session.likes) ? session.likes : [];
      me.hobbies = Array.isArray(session.hobbies) ? session.hobbies : [];
      me.points = Number(session.points) || 0;
      me.wins = Number(session.wins) || 0;
      me.losses = Number(session.losses) || 0;

      $("auth-section").classList.add("hidden");
      $("app-section").classList.remove("hidden");
      $("user-badge").classList.remove("hidden");
      $("header-stats").classList.remove("hidden");
      $("logout-btn").classList.remove("hidden");
      $("user-badge").textContent = `${me.name || me.email.split("@")[0]} • ${me.age || 18}`;

      $("prof-name").value = me.name || "";
      $("prof-gender").value = me.gender || "";
      $("prof-age").value = me.age || 18;
      $("prof-country").value = me.country || "";
      $("prof-city").value = me.city || "";
      $("prof-education").value = me.education || "";
      $("prof-bio").value = me.bio || "";
      $("prof-avatar-preview").src = me.avatar;

      renderStats();
      renderQuestionnaireOptions();
      applyProfileViewMode();
      switchTab("profile");
      renderRooms();
      subscribeUsers();
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
        uid, email, name: email.split("@")[0] || "משתמש", gender: "", age,
        country: "", city: "", education: "", bio: "", likes: [], hobbies: [],
        avatar: `https://api.dicebear.com/9.x/avataaars/svg?seed=${encodeURIComponent(uid)}`,
        profileCompleted: false, points: 0, wins: 0, losses: 0
      };
      localStorage.setItem("toplove_session", JSON.stringify(session));
      try { await setDoc(doc(db, "users", uid), { ...session, updatedAt: serverTimestamp() }, { merge: true }); } catch {}
      openApp(session);
    };

    $("logout-btn").onclick = () => { localStorage.removeItem("toplove_session"); location.reload(); };
    document.querySelectorAll(".tab-btn").forEach((btn) => { btn.onclick = () => switchTab(btn.dataset.tab); });

    $("prof-avatar-file").onchange = (e) => {
      const f = e.target.files?.[0];
      if (!f) return;
      const rd = new FileReader();
      rd.onload = () => { me.avatar = String(rd.result); $("prof-avatar-preview").src = me.avatar; };
      rd.readAsDataURL(f);
    };
    $("prof-avatar-url").oninput = (e) => {
      if (e.target.value.trim()) { me.avatar = e.target.value.trim(); $("prof-avatar-preview").src = me.avatar; }
    };

    $("profile-form").onsubmit = async (e) => {
      e.preventDefault();
      const ageVal = $("prof-age").value ? Number($("prof-age").value) : 18;
      if (ageVal < 18) {
        $("profile-error").textContent = "גיל מינימלי הוא 18.";
        $("profile-error").classList.remove("hidden");
        return;
      }
      $("profile-error").classList.add("hidden");
      me.name = $("prof-name").value.trim() || me.name || "משתמש";
      me.gender = $("prof-gender").value;
      me.age = ageVal;
      me.country = $("prof-country").value.trim();
      me.city = $("prof-city").value.trim();
      me.education = $("prof-education").value.trim();
      me.bio = $("prof-bio").value.trim();
      me.profileCompleted = true;

      localStorage.setItem("toplove_session", JSON.stringify(me));
      $("user-badge").textContent = `${me.name} • ${me.age}`;
      try { await setDoc(doc(db, "users", me.uid), { ...me, updatedAt: serverTimestamp() }, { merge: true }); } catch {}
      applyProfileViewMode();
      $("save-feedback").classList.remove("opacity-0");
      setTimeout(() => $("save-feedback").classList.add("opacity-0"), 1500);
    };

    let allUsers = [];
    function subscribeUsers() {
      onSnapshot(collection(db, "users"), (snap) => {
        allUsers = snap.docs.map((d) => ({ id: d.id, ...d.data() })).filter((u) => u.id !== me.uid);
        $("real-users-grid").innerHTML = allUsers.length
          ? allUsers.map((u) => {
              const loc = [u.country, u.city].filter(Boolean).join(", ");
              return `<div class="bg-slate-900/80 border border-slate-700 rounded-xl p-4 flex flex-col justify-between gap-3">
                <div class="flex items-center gap-3">
                  <img src="${u.avatar || "https://api.dicebear.com/9.x/avataaars/svg?seed=" + u.id}" alt="" class="w-12 h-12 rounded-full object-cover border border-pink-500" />
                  <div>
                    <div class="font-bold text-sm">${u.name || "משתמש"} • רמה ${getLevel(u.points)}</div>
                    <div class="text-xs text-slate-300">${[u.gender, u.age ? "גיל " + u.age : "", loc].filter(Boolean).join(" • ")}</div>
                  </div>
                </div>
                <p class="text-xs text-slate-400">${u.bio || "אין תיאור"}</p>
                <button type="button" data-dm-user="${u.id}" class="w-full py-1.5 rounded-lg text-xs font-semibold bg-pink-600">שיחה אישית</button>
              </div>`;
            }).join("")
          : `<p class="text-xs text-slate-400 col-span-full">עדיין אין משתמשים אחרים רשומים במערכת.</p>`;

        document.querySelectorAll("[data-dm-user]").forEach((btn) => {
          btn.onclick = () => {
            const other = allUsers.find((x) => x.id === btn.dataset.dmUser);
            if (!other) return;
            const dmId = "dm_" + [me.uid, other.id].sort().join("_");
            if (!chatRooms.some((r) => r.id === dmId)) chatRooms.unshift({ id: dmId, topic: `שיחה עם ${other.name || "משתמש"}`, members: [me.uid, other.id] });
            activeRoomId = dmId;
            switchTab("chat");
            renderRooms();
          };
        });
      });
    }

    const chatRooms = [
      { id: "r-general", topic: "כללי וצ׳אט פתוח", members: [] },
      { id: "r-music", topic: "מוזיקה, פלייליסטים והופעות", members: [] },
      { id: "r-movies", topic: "סרטים, סדרות ואנימה", members: [] },
      { id: "r-food", topic: "אוכל, מסעדות ומתכונים", members: [] },
      { id: "r-travel", topic: "טיולים בארץ ובחו״ל", members: [] },
      { id: "r-gaming", topic: "גיימינג ומשחקי רשת", members: [] },
      { id: "r-fitness", topic: "ספורט, חדר כושר ואורח חיים", members: [] },
      { id: "r-dating", topic: "היכרויות, דייטים ושיחות", members: [] },
      { id: "r-humor", topic: "בדיחות, ממים וצחוקים", members: [] },
      { id: "r-night", topic: "ציפורי לילה ושיחות מאוחרות", members: [] }
    ];
    let activeRoomId = chatRooms[0].id, unsubMsgs = null;

    function ensureUserInRoom(room) {
      room.members = Array.isArray(room.members) ? room.members : [];
      if (!room.members.includes(me.uid)) {
        if (room.members.length >= MAX_ROOM_USERS) return false;
        room.members.push(me.uid);
      }
      return true;
    }

    function listenMsgs(roomId) {
      if (unsubMsgs) { unsubMsgs(); unsubMsgs = null; }
      const q = query(collection(db, "rooms", roomId, "messages"), orderBy("createdAt", "asc"));
      unsubMsgs = onSnapshot(q, (snap) => {
        const msgs = snap.docs.map((d) => d.data());
        $("chat-messages").innerHTML = msgs.length
          ? msgs.map((m) => m.audioData
              ? `<div class="bg-slate-800 px-3 py-2 rounded-xl text-sm space-y-1">
                  <div class="text-xs font-bold text-amber-300">🎤 ${m.from || "משתמש"} (הקלטה קולית)</div>
                  <audio controls src="${m.audioData}" class="w-full max-w-xs h-8"></audio>
                </div>`
              : `<div class="bg-slate-800 px-3 py-2 rounded-xl text-sm"><strong class="text-pink-300">${m.from || "משתמש"}:</strong> ${m.text || ""}</div>`
            ).join("")
          : `<p class="text-xs text-slate-400">אין עדיין הודעות בחדר הזה.</p>`;
      });
    }

    function renderRooms() {
      $("rooms-list").innerHTML = chatRooms.map((r) => {
        const count = (r.members || []).length;
        return `<button type="button" data-room="${r.id}" class="w-full text-right p-3 rounded-xl border text-xs flex items-center justify-between gap-2 ${r.id === activeRoomId ? "bg-pink-600/30 border-pink-400" : "bg-slate-950/70 border-slate-800"}">
          <span class="truncate">💬 ${r.topic}</span>
          <span class="text-[11px] px-2 py-0.5 rounded-full bg-slate-800 text-slate-200 shrink-0">${count}/${MAX_ROOM_USERS}</span>
        </button>`;
      }).join("");

      document.querySelectorAll("[data-room]").forEach((b) => {
        b.onclick = () => {
          const target = chatRooms.find((r) => r.id === b.dataset.room);
          if (!target) return;
          if (!ensureUserInRoom(target)) { alert(`החדר מלא (מקסימום ${MAX_ROOM_USERS} משתתפים).`); return; }
          activeRoomId = target.id;
          renderRooms();
        };
      });

      const cur = chatRooms.find((r) => r.id === activeRoomId) || chatRooms[0];
      ensureUserInRoom(cur);
      $("active-room-title").textContent = cur.topic;
      $("active-room-meta").textContent = `חדר שיחה פתוח • עד ${MAX_ROOM_USERS} משתתפים`;
      $("room-capacity-badge").textContent = `${cur.members.length} / ${MAX_ROOM_USERS} משתתפים`;
      listenMsgs(cur.id);
    }

    $("create-room-form").onsubmit = async (e) => {
      e.preventDefault();
      const topic = $("new-room-topic").value.trim();
      if (!topic) return;
      const room = { id: `r-${Date.now()}`, topic, members: [me.uid] };
      chatRooms.unshift(room);
      activeRoomId = room.id;
      $("new-room-topic").value = "";
      try { await setDoc(doc(db, "rooms", room.id), { id: room.id, topic: room.topic, createdAt: serverTimestamp() }, { merge: true }); } catch {}
      renderRooms();
    };

    $("chat-form").onsubmit = async (e) => {
      e.preventDefault();
      const txt = $("chat-input").value.trim();
      if (!txt) return;
      $("chat-input").value = "";
      await addDoc(collection(db, "rooms", activeRoomId, "messages"), { from: me.name || "משתמש", text: txt, createdAt: serverTimestamp() });
    };

    let mediaRecorder = null, audioChunks = [];
    $("record-voice-btn").onclick = async () => {
      if (mediaRecorder && mediaRecorder.state === "recording") {
        mediaRecorder.stop();
        $("record-voice-btn").textContent = "🎤 התחל הקלטה";
        $("record-voice-btn").classList.replace("bg-rose-600", "bg-amber-600");
        $("voice-status").textContent = "שולח הקלטה...";
        return;
      }
      if (!navigator.mediaDevices?.getUserMedia) { $("voice-status").textContent = "הדפדפן לא תומך בהקלטה קולית."; return; }
      try {
        const stream = await navigator.mediaDevices.getUserMedia({ audio: true });
        audioChunks = [];
        mediaRecorder = new MediaRecorder(stream);
        mediaRecorder.ondataavailable = (ev) => { if (ev.data.size > 0) audioChunks.push(ev.data); };
        mediaRecorder.onstop = async () => {
          stream.getTracks().forEach((t) => t.stop());
          const blob = new Blob(audioChunks, { type: "audio/webm" });
          const reader = new FileReader();
          reader.onloadend = async () => {
            await addDoc(collection(db, "rooms", activeRoomId, "messages"), { from: me.name || "משתמש", audioData: String(reader.result), createdAt: serverTimestamp() });
            $("voice-status").textContent = "ההקלטה נשלחה לחדר!";
          };
          reader.readAsDataURL(blob);
        };
        mediaRecorder.start();
        $("record-voice-btn").textContent = "⏹️ עצור ושלח הקלטה";
        $("record-voice-btn").classList.replace("bg-amber-600", "bg-rose-600");
        $("voice-status").textContent = "מקליט כעת...";
      } catch { $("voice-status").textContent = "לא ניתנה הרשאה למיקרופון."; }
    };const timerIntervals = {};
    function startCountdown(key, seconds, elId, onExpire) {
      if (timerIntervals[key]) clearInterval(timerIntervals[key]);
      let rem = seconds;
      const paint = () => {
        const m = String(Math.floor(rem / 60)).padStart(2, "0");
        const s = String(rem % 60).padStart(2, "0");
        if ($(elId)) $(elId).textContent = `⏱️ ${m}:${s}`;
      };
      paint();
      timerIntervals[key] = setInterval(() => {
        rem -= 1;
        if (rem <= 0) {
          clearInterval(timerIntervals[key]);
          if ($(elId)) $(elId).textContent = "⏱️ 00:00";
          if (onExpire) onExpire();
        } else paint();
      }, 1000);
    }

    document.querySelectorAll(".game-tab-btn").forEach((btn) => {
      btn.onclick = () => {
        const g = btn.dataset.game;
        document.querySelectorAll(".game-tab-btn").forEach((b) => {
          b.className = b.dataset.game === g
            ? "game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold bg-pink-600"
            : "game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold glass text-slate-300";
        });
        document.querySelectorAll(".game-panel").forEach((p) => p.classList.add("hidden"));
        $(`game-${g}`).classList.remove("hidden");
        if (g === "ttt") startCountdown("ttt", 30, "ttt-timer");
        if (g === "rps") startCountdown("rps", 15, "rps-timer");
        if (g === "memory") startCountdown("memory", 120, "memory-timer");
      };
    });

    const tttRooms = Array.from({ length: 100 }, (_, i) => ({
      id: `ttt-room-${i + 1}`, num: i + 1, p1: null, p2: null, board: Array(9).fill(""), turn: "X", scored: false
    }));
    let activeTttRoomId = null;

    function renderTttRooms() {
      $("ttt-rooms-grid").innerHTML = tttRooms.map((r) => {
        const isSel = r.id === activeTttRoomId;
        const count = (r.p1 ? 1 : 0) + (r.p2 ? 1 : 0);
        const label = count === 0 ? "חדר ריק" : count === 1 ? "ממתין לשחקן 2" : "2/2 פעיל";
        return `<button type="button" data-ttt-room="${r.id}" class="text-right p-2 rounded-xl border text-[11px] transition ${isSel ? "bg-pink-600/35 border-pink-400" : count === 0 ? "bg-slate-900/75 border-slate-700 hover:border-emerald-400" : "bg-slate-900/95 border-amber-500/40"}">
          <div class="font-bold">חדר #${r.num}</div>
          <div class="text-slate-300 truncate">${label}</div>
        </button>`;
      }).join("");

      document.querySelectorAll("[data-ttt-room]").forEach((b) => {
        b.onclick = () => {
          const r = tttRooms.find((x) => x.id === b.dataset.tttRoom);
          if (!r) return;
          const myLabel = me.name || "שחקן";
          if (r.p1 !== myLabel && r.p2 !== myLabel) {
            if (!r.p1) r.p1 = myLabel;
            else if (!r.p2) r.p2 = myLabel;
            else { alert("החדר מלא (2/2 שחקנים). בחר חדר אחר."); return; }
          }
          activeTttRoomId = r.id;
          $("ttt-leave-room").classList.remove("hidden");
          startCountdown("ttt", 30, "ttt-timer");
          renderTttRooms();
          renderTttBoard();
        };
      });
    }

    $("ttt-add-room").onclick = () => {
      const nextNum = tttRooms.length + 1;
      tttRooms.push({ id: `ttt-room-${nextNum}`, num: nextNum, p1: null, p2: null, board: Array(9).fill(""), turn: "X", scored: false });
      renderTttRooms();
    };

    $("ttt-leave-room").onclick = () => {
      const r = tttRooms.find((x) => x.id === activeTttRoomId);
      const myLabel = me.name || "שחקן";
      if (r) { if (r.p1 === myLabel) r.p1 = null; if (r.p2 === myLabel) r.p2 = null; }
      activeTttRoomId = null;
      $("ttt-leave-room").classList.add("hidden");
      renderTttRooms();
      renderTttBoard();
    };

    function checkTttWin(b) {
      const lines = [[0,1,2],[3,4,5],[6,7,8],[0,3,6],[1,4,7],[2,5,8],[0,4,8],[2,4,6]];
      for (const [a, c, d] of lines) if (b[a] && b[a] === b[c] && b[a] === b[d]) return b[a];
      return b.every(Boolean) ? "DRAW" : null;
    }

    function renderTttBoard() {
      const r = tttRooms.find((x) => x.id === activeTttRoomId);
      const board = r ? r.board : Array(9).fill("");
      $("ttt-p1-name").textContent = r?.p1 || "מושב 1 ריק";
      $("ttt-p2-name").textContent = r?.p2 || "ממתין לשחקן 2...";
      const el = $("ttt-board");
      el.innerHTML = "";
      const win = checkTttWin(board);
      const canMove = Boolean(r && r.p1 && r.p2 && !win);

      board.forEach((cell, idx) => {
        const btn = document.createElement("button");
        btn.type = "button";
        btn.disabled = !canMove || Boolean(cell);
        btn.className = "aspect-square rounded-lg bg-amber-900/90 border border-amber-500/40 text-lg font-bold flex items-center justify-center disabled:opacity-60";
        btn.textContent = cell === "X" ? "❌" : cell === "O" ? "⭕" : "";
        btn.onclick = async () => {
          if (!canMove || board[idx]) return;
          board[idx] = r.turn;
          const resultNow = checkTttWin(board);
          if (resultNow && !r.scored) {
            r.scored = true;
            const myLabel = me.name || "שחקן";
            if ((resultNow === "X" && r.p1 === myLabel) || (resultNow === "O" && r.p2 === myLabel)) await awardWin(25);
            else if (resultNow === "X" || resultNow === "O") await awardLoss(5);
          }
          r.turn = r.turn === "X" ? "O" : "X";
          startCountdown("ttt", 30, "ttt-timer");
          renderTttBoard();
          renderTttRooms();
        };
        el.appendChild(btn);
      });

      if (!r) $("ttt-status").textContent = "לחץ על אחד מ-100 החדרים כדי להיכנס";
      else if (!r.p1 || !r.p2) $("ttt-status").textContent = `נמצא בחדר #${r.num} — ממתין שחקן נוסף שייכנס מולך`;
      else if (win === "DRAW") $("ttt-status").textContent = `תיקו בחדר #${r.num}!`;
      else if (win) $("ttt-status").textContent = `המנצח בחדר #${r.num}: ${win === "X" ? r.p1 : r.p2} 🎉`;
      else $("ttt-status").textContent = `חדר #${r.num} • תור ${r.turn === "X" ? r.p1 + " (❌)" : r.p2 + " (⭕)"}`;
    }

    $("ttt-reset").onclick = () => {
      const r = tttRooms.find((x) => x.id === activeTttRoomId);
      if (!r) return;
      r.board = Array(9).fill(""); r.turn = "X"; r.scored = false;
      startCountdown("ttt", 30, "ttt-timer");
      renderTttBoard();
    };
    renderTttRooms();
    renderTttBoard();

    let rpsSeat1 = null, rpsSeat2 = null, rpsBusy = false;
    function syncRpsSeatsUI() {
      $("rps-left-name").textContent = rpsSeat1 || "מושב 1 פנוי";
      $("rps-right-name").textContent = rpsSeat2 || "מושב 2 פנוי";
      $("rps-left-avatar").textContent = rpsSeat1 ? "🧑" : "🪑";
      $("rps-right-avatar").textContent = rpsSeat2 ? "🧑" : "🪑";
      const myLabel = me.name || "שחקן";
      const inGame = rpsSeat1 === myLabel || rpsSeat2 === myLabel;
      $("rps-join-btn").classList.toggle("hidden", inGame);
      $("rps-leave-btn").classList.toggle("hidden", !inGame);
      const ready = Boolean(rpsSeat1 && rpsSeat2);
      document.querySelectorAll(".rps-choice").forEach((b) => { b.disabled = !ready || rpsBusy; b.classList.toggle("opacity-50", !ready || rpsBusy); });
      $("rps-round-phase").textContent = ready ? "שני שחקנים מוכנים!" : "ממתין לשחקן נוסף שילחץ להיכנס";
    }

    $("rps-join-btn").onclick = () => {
      const myLabel = me.name || "שחקן";
      if (!rpsSeat1) rpsSeat1 = myLabel;
      else if (!rpsSeat2 && rpsSeat1 !== myLabel) rpsSeat2 = myLabel;
      else { alert("שני המקומות תפוסים כרגע."); return; }
      syncRpsSeatsUI();
    };

    $("rps-leave-btn").onclick = () => {
      const myLabel = me.name || "שחקן";
      if (rpsSeat1 === myLabel) rpsSeat1 = null;
      if (rpsSeat2 === myLabel) rpsSeat2 = null;
      syncRpsSeatsUI();
    };

    document.querySelectorAll(".rps-choice").forEach((btn) => {
      btn.onclick = async () => {
        if (!rpsSeat1 || !rpsSeat2 || rpsBusy) return;
        rpsBusy = true; syncRpsSeatsUI();
        startCountdown("rps", 15, "rps-timer");
        const opts = ["rock", "paper", "scissors"];
        const labels = { rock: "🪨 אבן", paper: "📄 נייר", scissors: "✂️ מספריים" };
        const signs = { rock: "🪨", paper: "📄", scissors: "✂️" };
        const p1Choice = btn.dataset.rps;
        const p2Choice = opts[Math.floor(Math.random() * 3)];
        $("rps-left-sign").textContent = "✊"; $("rps-right-sign").textContent = "✊";
        const seq = ["1", "2", "3!"]; let i = 0;
        $("rps-count-num").textContent = seq[0]; $("rps-round-phase").textContent = "סופרים עד 3...";

        const iv = setInterval(async () => {
          i += 1;
          if (i < seq.length) $("rps-count-num").textContent = seq[i];
          else {
            clearInterval(iv);
            $("rps-left-sign").textContent = signs[p1Choice]; $("rps-right-sign").textContent = signs[p2Choice];
            $("rps-round-phase").textContent = "חשיפה!";
            let msg = "תיקו!";
            if ((p1Choice === "rock" && p2Choice === "scissors") || (p1Choice === "paper" && p2Choice === "rock") || (p1Choice === "scissors" && p2Choice === "paper")) {
              msg = `${rpsSeat1} ניצח/ה! 🎉`;
              if (rpsSeat1 === (me.name || "שחקן")) await awardWin(20);
            } else if (p1Choice !== p2Choice) {
              msg = `${rpsSeat2} ניצח/ה! 🎉`;
              if (rpsSeat1 === (me.name || "שחקן")) await awardLoss(5);
            }
            $("rps-result").textContent = `${labels[p1Choice]} מול ${labels[p2Choice]} — ${msg}`;
            rpsBusy = false; syncRpsSeatsUI();
          }
        }, 420);
      };
    });
    syncRpsSeatsUI();const memRooms = Array.from({ length: 50 }, (_, i) => ({ id: `mem-room-${i + 1}`, num: i + 1, players: [], turnIdx: 0 }));
    let activeMemRoomId = null;
    const hardEmojis = ["😀","😃","😄","😁","😆","😅","🙂","🙃","😉","😊","😇","🥰","😍","🤩","😘","😗","😚","😙"];
    let memCards = [], memFlipped = [], memMatched = new Set();

    function buildHardMemoryBoard() {
      memCards = [...hardEmojis, ...hardEmojis].sort(() => Math.random() - 0.5);
      memFlipped = []; memMatched = new Set();
      startCountdown("memory", 120, "memory-timer", () => { $("memory-status").textContent = "הזמן נגמר! לחץ 'ערבב לוח' להתחלה חדשה."; });
      renderMemoryGrid();
    }

    function renderMemRooms() {
      $("memory-rooms-grid").innerHTML = memRooms.map((r) => {
        const isSel = r.id === activeMemRoomId;
        return `<button type="button" data-mem-room="${r.id}" class="p-1.5 rounded-lg border text-[10px] font-bold transition ${isSel ? "bg-pink-600/35 border-pink-400" : "bg-slate-900/80 border-slate-700 hover:border-emerald-400"}">
          <div>חדר ${r.num}</div>
          <div class="text-slate-300 font-normal">${r.players.length}/6</div>
        </button>`;
      }).join("");

      document.querySelectorAll("[data-mem-room]").forEach((b) => {
        b.onclick = () => {
          const r = memRooms.find((x) => x.id === b.dataset.memRoom);
          if (!r) return;
          const myLabel = me.name || "שחקן";
          if (!r.players.some((p) => p.name === myLabel)) {
            if (r.players.length >= 6) { alert("החדר מלא (מקסימום 6 שחקנים)."); return; }
            r.players.push({ name: myLabel, score: 0 });
          }
          activeMemRoomId = r.id;
          $("memory-leave-room").classList.remove("hidden");
          buildHardMemoryBoard(); renderMemRooms(); renderMemPlayersBoard();
        };
      });
    }

    $("memory-leave-room").onclick = () => {
      const r = memRooms.find((x) => x.id === activeMemRoomId);
      const myLabel = me.name || "שחקן";
      if (r) r.players = r.players.filter((p) => p.name !== myLabel);
      activeMemRoomId = null;
      $("memory-leave-room").classList.add("hidden");
      renderMemRooms(); renderMemPlayersBoard();
    };

    function renderMemPlayersBoard() {
      const r = memRooms.find((x) => x.id === activeMemRoomId);
      const slots = Array.from({ length: 6 }, (_, idx) => r?.players[idx] || null);
      $("memory-players-board").innerHTML = slots.map((p, idx) => {
        const isTurn = r && r.players.length > 0 && (r.turnIdx % r.players.length) === idx && p;
        return `<div class="p-2 rounded-lg border ${isTurn ? "bg-pink-600/25 border-pink-400" : "bg-slate-900 border-slate-800"}">
          <div class="font-bold truncate">${p ? p.name : `מושב ${idx + 1} פנוי`}</div>
          <div class="text-amber-300">${p ? `${p.score} נק׳` : "ממתין לשחקן"}</div>
        </div>`;
      }).join("");
    }

    function renderMemoryGrid() {
      const g = $("memory-grid"); g.innerHTML = "";
      memCards.forEach((sym, i) => {
        const show = memFlipped.includes(i) || memMatched.has(i);
        const btn = document.createElement("button");
        btn.type = "button";
        btn.className = "aspect-square rounded-xl bg-slate-900 border border-slate-700 text-xl flex items-center justify-center hover:border-pink-400";
        btn.textContent = show ? sym : "❓";
        btn.onclick = async () => {
          if (show || memFlipped.length === 2) return;
          memFlipped.push(i); renderMemoryGrid();
          if (memFlipped.length === 2) {
            const [a, b] = memFlipped;
            const r = memRooms.find((x) => x.id === activeMemRoomId);
            if (memCards[a] === memCards[b]) {
              memMatched.add(a); memMatched.add(b); memFlipped = [];
              if (r && r.players.length) {
                const curP = r.players[r.turnIdx % r.players.length];
                curP.score += 10;
                if (curP.name === (me.name || "שחקן")) await awardWin(10);
              }
              if (memMatched.size === memCards.length) $("memory-status").textContent = "כל 18 הזוגות נמצאו! 🎉";
              renderMemPlayersBoard(); renderMemoryGrid();
            } else {
              setTimeout(() => {
                memFlipped = [];
                if (r && r.players.length) r.turnIdx = (r.turnIdx + 1) % r.players.length;
                renderMemPlayersBoard(); renderMemoryGrid();
              }, 700);
            }
          }
        };
        g.appendChild(btn);
      });
      if (activeMemRoomId) {
        const r = memRooms.find((x) => x.id === activeMemRoomId);
        $("memory-status").textContent = `חדר זיכרון #${r.num} • ${r.players.length}/6 שחקנים • תור ${r.players[r.turnIdx % r.players.length]?.name || ""}`;
      }
    }

    $("memory-reset").onclick = buildHardMemoryBoard;
    renderMemRooms(); renderMemPlayersBoard(); buildHardMemoryBoard();

    let numRooms = [
      { id: "nr-1", name: "חדר עד 1,000", maxNum: 1000, hostName: "מנהל החדר", secret: null, guesses: [] },
      { id: "nr-2", name: "חדר עד 1,500", maxNum: 1500, hostName: "מנהל החדר", secret: null, guesses: [] }
    ];
    let activeNumRoomId = numRooms[0].id;

    function renderNumRooms() {
      $("num-rooms-list").innerHTML = numRooms.map((r) => `
        <button type="button" data-num-room="${r.id}" class="text-right p-3 rounded-xl border text-xs ${r.id === activeNumRoomId ? "bg-pink-600/30 border-pink-400" : "bg-slate-900/80 border-slate-700"}">
          <div class="font-bold">🎯 ${r.name}</div>
          <div class="text-slate-300 mt-0.5">טווח: 1 עד ${r.maxNum.toLocaleString()} • מנהל: ${r.hostName}</div>
        </button>
      `).join("");
      document.querySelectorAll("[data-num-room]").forEach((b) => {
        b.onclick = () => { activeNumRoomId = b.dataset.numRoom; renderNumRooms(); renderActiveNumRoom(); };
      });
    }

    function renderActiveNumRoom() {
      const r = numRooms.find((x) => x.id === activeNumRoomId) || numRooms[0];
      $("num-room-header").textContent = `${r.name} (טווח: 1 עד ${r.maxNum.toLocaleString()})`;
      $("num-host-badge").textContent = `מנהל חדר: ${r.hostName}`;
      $("num-guess-input").min = 1; $("num-guess-input").max = r.maxNum;
      $("num-secret-input").value = r.secret !== null ? String(r.secret) : "";
      $("num-secret-status").textContent = r.secret !== null
        ? "✓ מספר סודי נקבע בשקט! אפשר לנחש."
        : "טרם נקבע מספר סודי — הזן מספר בשקט או לחץ 'קבע מספר סודי'.";
      $("num-guesses-log").innerHTML = r.guesses.map((g) =>
        `<div class="px-3 py-1.5 rounded-lg bg-slate-900 border border-slate-800 flex justify-between">
          <span><strong>${g.player}</strong> ניחש <strong>${g.value}</strong></span>
          <span class="${g.hit ? "text-emerald-300 font-bold" : "text-rose-300"}">${g.msg}</span>
        </div>`
      ).join("");
    }

    $("num-create-room-form").onsubmit = (e) => {
      e.preventDefault();
      const name = $("num-room-name").value.trim();
      const maxNum = Math.max(10, Number($("num-room-max").value) || 1000);
      if (!name) return;
      const nr = { id: `nr-${Date.now()}`, name, maxNum, hostName: me.name || "מנהל החדר", secret: null, guesses: [] };
      numRooms.unshift(nr); activeNumRoomId = nr.id; $("num-room-name").value = "";
      renderNumRooms(); renderActiveNumRoom();
    };

    $("num-toggle-secret").onclick = () => {
      $("num-secret-input").type = $("num-secret-input").type === "password" ? "number" : "password";
    };

    $("num-set-secret-btn").onclick = () => {
      const r = numRooms.find((x) => x.id === activeNumRoomId) || numRooms[0];
      const typed = Number($("num-secret-input").value);
      r.secret = (typed >= 1 && typed <= r.maxNum) ? typed : Math.floor(Math.random() * r.maxNum) + 1;
      r.guesses = [];
      $("num-guess-feedback").textContent = "מספר סודי נקבע בשקט! התחילו לנחש.";
      renderActiveNumRoom();
    };

    $("num-guess-btn").onclick = async () => {
      const r = numRooms.find((x) => x.id === activeNumRoomId) || numRooms[0];
      if (r.secret === null) r.secret = Math.floor(Math.random() * r.maxNum) + 1;
      const val = Number($("num-guess-input").value);
      if (!val || val < 1 || val > r.maxNum) {
        $("num-guess-feedback").textContent = `הכנס מספר בין 1 ל-${r.maxNum.toLocaleString()}.`;
        return;
      }
      let hit = false, msg = "";
      if (val === r.secret) {
        hit = true; msg = "ניחש נכון! 🎉";
        $("num-guess-feedback").textContent = `🎉 בול! ${me.name || "שחקן"} ניחש את המספר ${r.secret}!`;
        await awardWin(30);
      } else if (val < r.secret) {
        msg = "נמוך מדי (לא נכון)";
        $("num-guess-feedback").textContent = `המספר ${val} נמוך מהמספר הסודי ⬆️`;
      } else {
        msg = "גבוה מדי (לא נכון)";
        $("num-guess-feedback").textContent = `המספר ${val} גבוה מהמספר הסודי ⬇️`;
      }
      r.guesses.unshift({ player: me.name || "משתמש", value: val, hit, msg });
      $("num-guess-input").value = "";
      renderActiveNumRoom();
    };

    renderNumRooms(); renderActiveNumRoom();

    const savedSession = localStorage.getItem("toplove_session");
    if (savedSession) {
      try { openApp(JSON.parse(savedSession)); } catch {}
    }
  </script>
</body>
</html>
