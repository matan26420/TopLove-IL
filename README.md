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
    .chess-board {
      display: grid;
      grid-template-columns: repeat(8, minmax(0, 1fr));
      border: 2px solid #f472b6;
      border-radius: 12px;
      overflow: hidden;
    }
    .chess-cell {
      aspect-ratio: 1 / 1;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: clamp(1.1rem, 3vw, 1.8rem);
      cursor: pointer;
      user-select: none;
    }
    .chess-light { background: #e2e8f0; color: #0f172a; }
    .chess-dark { background: #475569; color: #ffffff; }
    .chess-selected { outline: 3px solid #ec4899; background: #fbcfe8 !important; color: #0f172a !important; }
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
    <div class="flex items-center gap-3">
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

        <!-- כרטיס פרופיל מוצג (מוצג בצורה מסודרת ומכובדת לאחר שמירה) -->
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

        <!-- טופס פרופיל ושאלון היכרות (נעלם לאחר שמירה) -->
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
            <label class="block text-sm font-bold text-pink-300">מה אתה אוהב לעשות? (בחירה חופשית — לא חובה)</label>
            <div id="likes-options" class="flex flex-wrap gap-2"></div>
          </div>

          <div class="bg-slate-900/70 p-4 rounded-2xl border border-slate-800 space-y-2.5">
            <label class="block text-sm font-bold text-indigo-300">מה התחביבים שלך? (בחירה חופשית — לא חובה)</label>
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
      </div>

      <div id="tab-users" class="tab-content hidden max-w-4xl mx-auto glass rounded-2xl p-6 space-y-4">
        <h2 class="text-xl font-bold">👥 משתמשים אמיתיים במערכת</h2>
        <p class="text-xs text-slate-300">כאן מופיעים משתמשים שנרשמו למערכת. אפשר לפתוח שיחה אישית או לעבור למשחקים.</p>
        <div id="real-users-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4"></div>
      </div><div id="tab-chat" class="tab-content hidden max-w-5xl mx-auto glass rounded-2xl p-6 space-y-5">
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
            <h3 class="text-sm font-bold text-slate-200">🗂️ חדרי שיחה פתוחים (מקס׳ 50 משתתפים)</h3>
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
        <div class="flex flex-wrap gap-2 justify-center">
          <button type="button" data-game="ttt" class="game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold bg-pink-600">1. איקס עיגול ⏱️</button>
          <button type="button" data-game="rps" class="game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold glass text-slate-300">2. אבן נייר מספריים ⏱️</button>
          <button type="button" data-game="chess" class="game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold glass text-slate-300">3. שחמט ⏱️</button>
          <button type="button" data-game="memory" class="game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold glass text-slate-300">4. זיכרון ⏱️</button>
          <button type="button" data-game="number" class="game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold glass text-slate-300">5. ניחוש מספר 🎯</button>
        </div>

        <!-- 1. איקס עיגול עם חדרים שאנשים פותחים ונכנסים/יוצאים + טיימר -->
        <div id="game-ttt" class="game-panel max-w-3xl mx-auto glass rounded-2xl p-6 space-y-5">
          <div class="flex flex-wrap items-center justify-between gap-2 border-b border-white/10 pb-3">
            <div>
              <h3 class="text-xl font-bold">📦 איקס עיגול — חדרים פעילים</h3>
              <p class="text-xs text-slate-300">פתח חדר שממתין לשחקן נוסף, או היכנס וצא מחדרים קיימים</p>
            </div>
            <div class="flex items-center gap-2">
              <span id="ttt-timer" class="px-3 py-1 rounded-full text-xs font-bold bg-amber-500/20 border border-amber-400/40 text-amber-200">⏱️ 00:30</span>
              <button type="button" id="ttt-create-room" class="px-3.5 py-1.5 rounded-xl text-xs font-semibold bg-emerald-600 hover:bg-emerald-500">+ פתח חדר איקס עיגול</button>
              <button type="button" id="ttt-leave-room" class="hidden px-3 py-1.5 rounded-xl text-xs font-semibold bg-rose-600 hover:bg-rose-500">צא מהחדר</button>
            </div>
          </div>

          <div id="ttt-rooms-grid" class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-2.5"></div>

          <div class="bg-slate-950/75 border border-amber-500/25 rounded-2xl p-4 space-y-4">
            <div class="grid grid-cols-3 items-center gap-2 text-center">
              <div class="flex flex-col items-center gap-1">
                <img id="ttt-p1-img" src="https://api.dicebear.com/9.x/avataaars/svg?seed=TTT1" alt="" class="w-12 h-12 rounded-full border-2 border-amber-400 bg-slate-800" />
                <span id="ttt-p1-name" class="text-xs font-bold">ממתין...</span>
                <span class="text-[10px] text-amber-300">❌</span>
              </div>
              <div id="ttt-board" class="grid grid-cols-3 gap-1.5 bg-amber-950/70 p-2.5 rounded-xl border border-amber-700/60"></div>
              <div class="flex flex-col items-center gap-1">
                <img id="ttt-p2-img" src="https://api.dicebear.com/9.x/avataaars/svg?seed=TTT2" alt="" class="w-12 h-12 rounded-full border-2 border-pink-400 bg-slate-800 opacity-60" />
                <span id="ttt-p2-name" class="text-xs font-bold text-slate-400">ממתין לשחקן...</span>
                <span class="text-[10px] text-pink-300">⭕</span>
              </div>
            </div>
            <div class="flex items-center justify-between gap-2">
              <p id="ttt-status" class="text-sm text-pink-200">בחר או פתח חדר איקס עיגול</p>
              <button type="button" id="ttt-reset" class="text-xs bg-slate-800 px-3 py-1.5 rounded-lg border border-slate-600">איפוס לוח</button>
            </div>
          </div>
        </div>

        <!-- 2. אבן נייר ומספריים: שתי דמויות מול זו, ספירה עד 3 + טיימר -->
        <div id="game-rps" class="game-panel hidden max-w-2xl mx-auto glass rounded-2xl p-6 space-y-4 text-center">
          <div class="flex flex-wrap items-center justify-between gap-2">
            <h3 class="text-xl font-bold">✂️ אבן נייר מספריים</h3>
            <span id="rps-timer" class="px-3 py-1 rounded-full text-xs font-bold bg-pink-500/20 border border-pink-400/40 text-pink-200">⏱️ 00:15</span>
          </div>

          <div class="grid grid-cols-3 items-center gap-3 bg-slate-950/70 border border-white/10 rounded-2xl p-4">
            <div class="flex flex-col items-center gap-1.5">
              <img id="rps-left-img" src="https://api.dicebear.com/9.x/avataaars/svg?seed=LeftRPS" alt="" class="w-16 h-16 rounded-full border-2 border-pink-400 bg-slate-800" />
              <span id="rps-left-name" class="text-xs font-bold">דמות 1</span>
              <div id="rps-left-sign" class="w-16 h-16 rounded-2xl bg-slate-900 border border-slate-700 flex items-center justify-center text-3xl">✊</div>
            </div>

            <div class="flex flex-col items-center justify-center gap-1">
              <span class="text-xs text-slate-400">ספירה:</span>
              <div id="rps-count-num" class="text-3xl font-extrabold text-pink-300 count-anim">1 • 2 • 3</div>
              <span id="rps-round-phase" class="text-xs text-indigo-200">עומדים זה מול זה</span>
            </div>

            <div class="flex flex-col items-center gap-1.5">
              <img id="rps-right-img" src="https://api.dicebear.com/9.x/avataaars/svg?seed=RightRPS" alt="" class="w-16 h-16 rounded-full border-2 border-indigo-400 bg-slate-800" />
              <span id="rps-right-name" class="text-xs font-bold">דמות 2</span>
              <div id="rps-right-sign" class="w-16 h-16 rounded-2xl bg-slate-900 border border-slate-700 flex items-center justify-center text-3xl">✊</div>
            </div>
          </div>

          <div class="flex justify-center gap-3">
            <button type="button" data-rps="rock" class="rps-choice px-5 py-3 rounded-xl bg-slate-800 hover:bg-pink-600 text-base font-semibold">🪨 אבן</button>
            <button type="button" data-rps="paper" class="rps-choice px-5 py-3 rounded-xl bg-slate-800 hover:bg-pink-600 text-base font-semibold">📄 נייר</button>
            <button type="button" data-rps="scissors" class="rps-choice px-5 py-3 rounded-xl bg-slate-800 hover:bg-pink-600 text-base font-semibold">✂️ מספריים</button>
          </div>
          <p id="rps-result" class="text-sm text-pink-200 bg-slate-900 p-3.5 rounded-xl">בחר אבן, נייר או מספריים — הדמויות יספרו עד 3</p>
        </div>

        <!-- 3. שחמט + טיימר -->
        <div id="game-chess" class="game-panel hidden max-w-lg mx-auto glass rounded-2xl p-6 text-center space-y-4">
          <div class="flex flex-wrap items-center justify-between gap-2">
            <h3 class="text-xl font-bold">♟️ שחמט</h3>
            <div class="flex items-center gap-2">
              <span id="chess-timer" class="px-3 py-1 rounded-full text-xs font-bold bg-indigo-500/20 border border-indigo-400/40 text-indigo-200">⏱️ 03:00</span>
              <button type="button" id="chess-reset" class="text-xs bg-slate-800 px-3 py-1.5 rounded-lg border border-slate-600">אפס לוח</button>
            </div>
          </div>
          <p id="chess-turn" class="text-sm text-pink-200">תור: לבן</p>
          <div id="chess-board" class="chess-board"></div>
        </div>

        <!-- 4. משחק זיכרון מתקדם עם לוחות מגוונים, יותר אימוג'ים וטיימר -->
        <div id="game-memory" class="game-panel hidden max-w-2xl mx-auto glass rounded-2xl p-6 text-center space-y-4">
          <div class="flex flex-wrap items-center justify-between gap-2">
            <h3 class="text-xl font-bold">💎 זיכרון מתקדם</h3>
            <div class="flex flex-wrap items-center gap-2">
              <select id="memory-size" class="px-3 py-1.5 rounded-xl bg-slate-900 border border-slate-700 text-xs">
                <option value="16">לוח 4x4 (8 זוגות)</option>
                <option value="24">לוח 6x4 (12 זוגות — קשה יותר)</option>
                <option value="36">לוח 6x6 (18 זוגות — אתגר)</option>
              </select>
              <span id="memory-timer" class="px-3 py-1 rounded-full text-xs font-bold bg-emerald-500/20 border border-emerald-400/40 text-emerald-200">⏱️ 01:15</span>
              <button type="button" id="memory-reset" class="text-xs bg-pink-600 px-3 py-1.5 rounded-lg font-semibold">ערבב מחדש</button>
            </div>
          </div>
          <div id="memory-grid" class="grid grid-cols-4 gap-2 max-w-xl mx-auto"></div>
          <p id="memory-status" class="text-sm text-pink-200"></p>
        </div>

        <!-- 5. ניחוש מספר עם חדרים, טווח מותאם ומנהל חדר שבוחר מספר בשקט -->
        <div id="game-number" class="game-panel hidden max-w-2xl mx-auto glass rounded-2xl p-6 space-y-4">
          <div class="border-b border-white/10 pb-3">
            <h3 class="text-xl font-bold">🎯 ניחוש מספר — חדרים ומנהל חדר</h3>
            <p class="text-xs text-slate-300">פתח חדר עם טווח מספרים (למשל 100, 1000 או 1500), מנהל החדר בוחר מספר בשקט והשאר מנחשים</p>
          </div>

          <form id="num-create-room-form" class="flex flex-col sm:flex-row gap-2.5 bg-slate-900/75 p-3.5 rounded-xl border border-slate-700">
            <input type="text" id="num-room-name" required placeholder="שם חדר ניחוש מספר..."
              class="flex-1 px-3.5 py-2 rounded-xl bg-slate-950 border border-slate-700 text-sm" />
            <input type="number" id="num-room-max" min="50" max="10000" value="1000" required
              class="w-32 px-3 py-2 rounded-xl bg-slate-950 border border-slate-700 text-sm text-center" />
            <button type="submit" class="px-4 py-2 rounded-xl text-xs font-semibold bg-emerald-600 hover:bg-emerald-500">
              פתח חדר
            </button>
          </form>

          <div id="num-rooms-list" class="grid grid-cols-1 sm:grid-cols-2 gap-2.5"></div>

          <div id="num-active-panel" class="bg-slate-950/75 border border-indigo-500/30 rounded-2xl p-4 space-y-4">
            <div class="flex flex-wrap items-center justify-between gap-2">
              <div id="num-room-header" class="font-bold text-sm text-pink-200">חדר ברירת מחדל (1–1,000)</div>
              <div id="num-host-badge" class="text-xs px-3 py-1 rounded-full bg-indigo-500/20 text-indigo-200">מנהל חדר: אתה</div>
            </div>

            <!-- אזור מנהל החדר לבחירת מספר בשקט -->
            <div class="bg-slate-900/90 border border-amber-500/30 rounded-xl p-3.5 space-y-2">
              <div class="flex items-center justify-between">
                <span class="text-xs font-bold text-amber-300">🤫 בחירת מספר סודי על ידי מנהל החדר (נשמר בשקט)</span>
                <button type="button" id="num-toggle-secret" class="text-xs text-slate-300 underline">הצג/הסתר למנהל</button>
              </div>
              <div class="flex flex-wrap gap-2 items-center">
                <input type="password" id="num-secret-input" placeholder="הכנס מספר סודי בשקט..."
                  class="flex-1 min-w-[160px] px-3 py-2 rounded-xl bg-slate-950 border border-slate-700 text-sm" />
                <button type="button" id="num-set-secret-btn" class="px-4 py-2 rounded-xl text-xs font-semibold bg-amber-600 hover:bg-amber-500">
                  קבע מספר סודי
                </button>
              </div>
              <p id="num-secret-status" class="text-xs text-emerald-300">עדיין לא נקבע מספר סודי — אפשר גם ללחוץ "קבע מספר סודי" כדי שהמערכת תגריל בשקט.</p>
            </div>

            <!-- אזור ניחוש של המשתתפים ובדיקת המחשב -->
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
      profileCompleted: false
    };

    function renderQuestionnaireOptions() {
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

    $("edit-profile-btn").onclick = () => {
      me.profileCompleted = false;
      applyProfileViewMode();
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
      me.likes = Array.isArray(session.likes) ? session.likes : [];
      me.hobbies = Array.isArray(session.hobbies) ? session.hobbies : [];
      $("auth-section").classList.add("hidden");
      $("app-section").classList.remove("hidden");
      $("user-badge").classList.remove("hidden");
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
      $("rps-left-img").src = me.avatar;
      $("rps-left-name").textContent = me.name || "אתה";

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
        profileCompleted: false
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
        $("rps-left-img").src = me.avatar;
      };
      rd.readAsDataURL(f);
    };

    $("prof-avatar-url").oninput = (e) => {
      if (e.target.value.trim()) {
        me.avatar = e.target.value.trim();
        $("prof-avatar-preview").src = me.avatar;
        $("rps-left-img").src = me.avatar;
      }
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
      $("rps-left-name").textContent = me.name;
      try { await setDoc(doc(db, "users", me.uid), { ...me, updatedAt: serverTimestamp() }, { merge: true }); } catch {}

      applyProfileViewMode();
      $("save-feedback").classList.remove("opacity-0");
      setTimeout(() => $("save-feedback").classList.add("opacity-0"), 1500);
    };

    let allUsers = [];
    function subscribeUsers() {
      onSnapshot(collection(db, "users"), (snap) => {
        allUsers = snap.docs.map((d) => ({ id: d.id, ...d.data() })).filter((u) => u.id !== me.uid);
        if (allUsers[0]) {
          $("rps-right-img").src = allUsers[0].avatar || `https://api.dicebear.com/9.x/avataaars/svg?seed=${allUsers[0].id}`;
          $("rps-right-name").textContent = allUsers[0].name || "שחקן 2";
        }
        $("real-users-grid").innerHTML = allUsers.length
          ? allUsers.map((u) => {
              const loc = [u.country, u.city].filter(Boolean).join(", ");
              return `
                <div class="bg-slate-900/80 border border-slate-700 rounded-xl p-4 flex flex-col justify-between gap-3">
                  <div class="flex items-center gap-3">
                    <img src="${u.avatar || "https://api.dicebear.com/9.x/avataaars/svg?seed=" + u.id}" alt="" class="w-12 h-12 rounded-full object-cover border border-pink-500" />
                    <div>
                      <div class="font-bold text-sm">${u.name || "משתמש"}</div>
                      <div class="text-xs text-slate-300">${[u.gender, u.age ? "גיל " + u.age : "", loc].filter(Boolean).join(" • ")}</div>
                    </div>
                  </div>
                  <p class="text-xs text-slate-400">${u.bio || (u.hobbies?.length ? "תחביבים: " + u.hobbies.join(", ") : "אין תיאור")}</p>
                  <button type="button" data-dm-user="${u.id}" class="w-full py-1.5 rounded-lg text-xs font-semibold bg-pink-600">שיחה אישית</button>
                </div>
              `;
            }).join("")
          : `<p class="text-xs text-slate-400 col-span-full">עדיין אין משתמשים אחרים רשומים במערכת.</p>`;

        document.querySelectorAll("[data-dm-user]").forEach((btn) => {
          btn.onclick = () => {
            const other = allUsers.find((x) => x.id === btn.dataset.dmUser);
            if (!other) return;
            const dmId = "dm_" + [me.uid, other.id].sort().join("_");
            if (!chatRooms.some((r) => r.id === dmId)) {
              chatRooms.unshift({ id: dmId, topic: `שיחה עם ${other.name || "משתמש"}`, members: [me.uid, other.id] });
            }
            activeRoomId = dmId;
            switchTab("chat");
            renderRooms();
          };
        });
      });
    }

    // --- חדרי שיחה (10 חדרים קיימים + פתיחת חדרים, עד 50 משתתפים והקלטות קוליות) ---
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
    let activeRoomId = chatRooms[0].id;
    let unsubMsgs = null;

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
          ? msgs.map((m) => {
              if (m.audioData) {
                return `<div class="bg-slate-800 px-3 py-2 rounded-xl text-sm space-y-1">
                  <div class="text-xs font-bold text-amber-300">🎤 ${m.from || "משתמש"} (הקלטה קולית)</div>
                  <audio controls src="${m.audioData}" class="w-full max-w-xs h-8"></audio>
                </div>`;
              }
              return `<div class="bg-slate-800 px-3 py-2 rounded-xl text-sm"><strong class="text-pink-300">${m.from || "משתמש"}:</strong> ${m.text || ""}</div>`;
            }).join("")
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
          if (!ensureUserInRoom(target)) {
            alert(`החדר מלא (מקסימום ${MAX_ROOM_USERS} משתתפים).`);
            return;
          }
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
      await addDoc(collection(db, "rooms", activeRoomId, "messages"), {
        from: me.name || "משתמש", text: txt, createdAt: serverTimestamp()
      });
    };

    // הקלטת הודעה קולית בחדר שיחה
    let mediaRecorder = null;
    let audioChunks = [];
    $("record-voice-btn").onclick = async () => {
      if (mediaRecorder && mediaRecorder.state === "recording") {
        mediaRecorder.stop();
        $("record-voice-btn").textContent = "🎤 התחל הקלטה";
        $("record-voice-btn").classList.replace("bg-rose-600", "bg-amber-600");
        $("voice-status").textContent = "שולח הקלטה...";
        return;
      }
      if (!navigator.mediaDevices?.getUserMedia) {
        $("voice-status").textContent = "הדפדפן לא תומך בהקלטה קולית.";
        return;
      }
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
            await addDoc(collection(db, "rooms", activeRoomId, "messages"), {
              from: me.name || "משתמש",
              audioData: String(reader.result),
              createdAt: serverTimestamp()
            });
            $("voice-status").textContent = "ההקלטה נשלחה לחדר!";
          };
          reader.readAsDataURL(blob);
        };
        mediaRecorder.start();
        $("record-voice-btn").textContent = "⏹️ עצור ושלח הקלטה";
        $("record-voice-btn").classList.replace("bg-amber-600", "bg-rose-600");
        $("voice-status").textContent = "מקליט כעת...";
      } catch {
        $("voice-status").textContent = "לא ניתנה הרשאה למיקרופון.";
      }
    };

    // --- מעבר בין המשחקים + טיימרים ---
    const timerIntervals = {};
    function startCountdown(key, seconds, elId, onExpireText) {
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
          if (onExpireText) onExpireText();
        } else {
          paint();
        }
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
        if (g === "chess") startCountdown("chess", 180, "chess-timer");
        if (g === "memory") startCountdown("memory", 75, "memory-timer", () => {
          $("memory-status").textContent = "הזמן נגמר! לחץ על 'ערבב מחדש' לסיבוב נוסף.";
        });
      };
    });

    // 1. איקס עיגול עם חדרים שניתן לפתוח, להיכנס אליהם ולצאת מהם
    let tttRooms = [
      { id: "ttt-1", title: "חדר מחסן #1", host: "דניאל", guest: null, board: Array(9).fill(""), turn: "X" },
      { id: "ttt-2", title: "חדר מהיר #2", host: "נועה", guest: null, board: Array(9).fill(""), turn: "X" }
    ];
    let activeTttRoomId = null;

    function renderTttRoomsList() {
      $("ttt-rooms-grid").innerHTML = tttRooms.map((r) => {
        const isCurrent = r.id === activeTttRoomId;
        const playersLabel = r.guest ? `${r.host} מול ${r.guest}` : `ממתין לשחקן (מארח: ${r.host})`;
        return `<button type="button" data-ttt-room="${r.id}" class="text-right p-3 rounded-xl border text-xs transition ${isCurrent ? "bg-pink-600/30 border-pink-400" : "bg-slate-900/80 border-slate-700 hover:border-pink-400/50"}">
          <div class="font-bold">📦 ${r.title}</div>
          <div class="text-slate-300 mt-0.5">${playersLabel}</div>
        </button>`;
      }).join("");

      document.querySelectorAll("[data-ttt-room]").forEach((b) => {
        b.onclick = () => {
          const room = tttRooms.find((x) => x.id === b.dataset.tttRoom);
          if (!room) return;
          if (room.host !== me.name && !room.guest) {
            room.guest = me.name || "שחקן 2";
          }
          activeTttRoomId = room.id;
          $("ttt-leave-room").classList.remove("hidden");
          startCountdown("ttt", 30, "ttt-timer");
          renderTttRoomsList();
          renderTttBoard();
        };
      });
    }

    $("ttt-create-room").onclick = () => {
      const id = `ttt-${Date.now()}`;
      const r = {
        id,
        title: `חדר של ${me.name || "משתמש"}`,
        host: me.name || "משתמש",
        guest: null,
        board: Array(9).fill(""),
        turn: "X"
      };
      tttRooms.unshift(r);
      activeTttRoomId = id;
      $("ttt-leave-room").classList.remove("hidden");
      startCountdown("ttt", 30, "ttt-timer");
      renderTttRoomsList();
      renderTttBoard();
    };

    $("ttt-leave-room").onclick = () => {
      const room = tttRooms.find((x) => x.id === activeTttRoomId);
      if (room && room.guest === (me.name || "שחקן 2")) room.guest = null;
      activeTttRoomId = null;
      $("ttt-leave-room").classList.add("hidden");
      renderTttRoomsList();
      renderTttBoard();
    };

    function checkTttWin(b) {
      const lines = [[0,1,2],[3,4,5],[6,7,8],[0,3,6],[1,4,7],[2,5,8],[0,4,8],[2,4,6]];
      for (const [a, c, d] of lines) if (b[a] && b[a] === b[c] && b[a] === b[d]) return b[a];
      return b.every(Boolean) ? "DRAW" : null;
    }

    function renderTttBoard() {
      const room = tttRooms.find((x) => x.id === activeTttRoomId);
      const board = room ? room.board : Array(9).fill("");
      $("ttt-p1-name").textContent = room ? room.host : "ממתין...";
      $("ttt-p2-name").textContent = room?.guest ? room.guest : "ממתין לשחקן...";
      $("ttt-p2-img").classList.toggle("opacity-60", !room?.guest);

      const el = $("ttt-board");
      el.innerHTML = "";
      const win = checkTttWin(board);
      board.forEach((cell, idx) => {
        const btn = document.createElement("button");
        btn.type = "button";
        btn.disabled = !room || Boolean(cell) || Boolean(win);
        btn.className = "aspect-square rounded-lg bg-amber-900/90 border border-amber-500/40 text-xl font-bold flex items-center justify-center";
        btn.textContent = cell === "X" ? "❌" : cell === "O" ? "⭕" : "";
        btn.onclick = () => {
          if (!room || board[idx] || win) return;
          board[idx] = room.turn;
          room.turn = room.turn === "X" ? "O" : "X";
          startCountdown("ttt", 30, "ttt-timer");
          renderTttBoard();
        };
        el.appendChild(btn);
      });

      if (!room) {
        $("ttt-status").textContent = "בחר חדר קיים או פתח חדר חדש כדי לשחק";
      } else if (win === "DRAW") {
        $("ttt-status").textContent = "תיקו! אפשר ללחוץ על איפוס לוח";
      } else if (win) {
        $("ttt-status").textContent = `ניצחון ל-${win === "X" ? "❌ (" + room.host + ")" : "⭕ (" + (room.guest || "אורח") + ")"}!`;
      } else {
        $("ttt-status").textContent = `בחדר "${room.title}" — תור ${room.turn === "X" ? "❌" : "⭕"}`;
      }
    }

    $("ttt-reset").onclick = () => {
      const room = tttRooms.find((x) => x.id === activeTttRoomId);
      if (!room) return;
      room.board = Array(9).fill("");
      room.turn = "X";
      startCountdown("ttt", 30, "ttt-timer");
      renderTttBoard();
    };
    renderTttRoomsList();
    renderTttBoard();

    // 2. אבן נייר מספריים — שתי דמויות מול זו שסופרות עד 3
    let rpsBusy = false;
    document.querySelectorAll(".rps-choice").forEach((btn) => {
      btn.onclick = () => {
        if (rpsBusy) return;
        rpsBusy = true;
        startCountdown("rps", 15, "rps-timer");
        const opts = ["rock", "paper", "scissors"];
        const labels = { rock: "🪨 אבן", paper: "📄 נייר", scissors: "✂️ מספריים" };
        const signs = { rock: "🪨", paper: "📄", scissors: "✂️" };
        const p1 = btn.dataset.rps;
        const p2 = opts[Math.floor(Math.random() * 3)];

        $("rps-left-sign").textContent = "✊";
        $("rps-right-sign").textContent = "✊";
        const seq = ["1", "2", "3!"];
        let i = 0;
        $("rps-count-num").textContent = seq[0];
        $("rps-round-phase").textContent = "סופרים עד 3...";

        const iv = setInterval(() => {
          i += 1;
          if (i < seq.length) {
            $("rps-count-num").textContent = seq[i];
          } else {
            clearInterval(iv);
            $("rps-left-sign").textContent = signs[p1];
            $("rps-right-sign").textContent = signs[p2];
            $("rps-round-phase").textContent = "נחשף!";
            let out = "תיקו!";
            if ((p1 === "rock" && p2 === "scissors") || (p1 === "paper" && p2 === "rock") || (p1 === "scissors" && p2 === "paper")) {
              out = `${$("rps-left-name").textContent} ניצח/ה! 🎉`;
            } else if (p1 !== p2) {
              out = `${$("rps-right-name").textContent} ניצח/ה! 🎉`;
            }
            $("rps-result").textContent = `${labels[p1]} מול ${labels[p2]} — ${out}`;
            rpsBusy = false;
          }
        }, 450);
      };
    });

    // 3. שחמט
    const initChess = () => [
      ["♜","♞","♝","♛","♚","♝","♞","♜"],
      ["♟","♟","♟","♟","♟","♟","♟","♟"],
      ["","","","","","","",""],
      ["","","","","","","",""],
      ["","","","","","","",""],
      ["","","","","","","",""],
      ["♙","♙","♙","♙","♙","♙","♙","♙"],
      ["♖","♘","♗","♕","♔","♗","♘","♖"]
    ];
    let chessBoard = initChess(), chessSel = null, chessTurn = "לבן";
    function renderChess() {
      const el = $("chess-board");
      el.innerHTML = "";
      $("chess-turn").textContent = `תור: ${chessTurn}`;
      chessBoard.forEach((row, r) => {
        row.forEach((piece, c) => {
          const cell = document.createElement("div");
          const isLight = (r + c) % 2 === 0;
          const isSel = chessSel && chessSel[0] === r && chessSel[1] === c;
          cell.className = `chess-cell ${isLight ? "chess-light" : "chess-dark"} ${isSel ? "chess-selected" : ""}`;
          cell.textContent = piece;
          cell.onclick = () => {
            if (!chessSel) {
              if (piece) { chessSel = [r, c]; renderChess(); }
            } else {
              const [sr, sc] = chessSel;
              if (sr !== r || sc !== c) {
                chessBoard[r][c] = chessBoard[sr][sc];
                chessBoard[sr][sc] = "";
                chessTurn = chessTurn === "לבן" ? "שחור" : "לבן";
              }
              chessSel = null;
              renderChess();
            }
          };
          el.appendChild(cell);
        });
      });
    }
    $("chess-reset").onclick = () => {
      chessBoard = initChess(); chessSel = null; chessTurn = "לבן";
      startCountdown("chess", 180, "chess-timer");
      renderChess();
    };
    renderChess();

    // 4. זיכרון עם לוחות מגוונים ויותר אימוג'ים
    const allEmojis = ["💜","🔥","⭐","🌹","💎","⚡","🎯","🍀","🦄","🍕","🎸","🚀","🌊","🦊","👑","🍩","🌙","🎲"];
    let memCards = [], memFlipped = [], memMatched = new Set();
    function initMemory() {
      const total = Number($("memory-size").value) || 16;
      const pairsCount = total / 2;
      const chosen = allEmojis.slice(0, pairsCount);
      memCards = [...chosen, ...chosen].sort(() => Math.random() - 0.5);
      memFlipped = [];
      memMatched = new Set();
      $("memory-grid").className = total === 16 ? "grid grid-cols-4 gap-2 max-w-md mx-auto" : "grid grid-cols-6 gap-2 max-w-xl mx-auto";
      $("memory-status").textContent = `מצא את כל ${pairsCount} הזוגות לפני שהזמן נגמר!`;
      startCountdown("memory", total === 16 ? 75 : total === 24 ? 105 : 140, "memory-timer", () => {
        $("memory-status").textContent = "הזמן נגמר! לחץ על 'ערבב מחדש'.";
      });
      renderMemory();
    }
    function renderMemory() {
      const g = $("memory-grid");
      g.innerHTML = "";
      memCards.forEach((sym, i) => {
        const show = memFlipped.includes(i) || memMatched.has(i);
        const btn = document.createElement("button");
        btn.type = "button";
        btn.className = "aspect-square rounded-xl bg-slate-900 border border-slate-700 text-xl flex items-center justify-center";
        btn.textContent = show ? sym : "❓";
        btn.onclick = () => {
          if (show || memFlipped.length === 2) return;
          memFlipped.push(i);
          renderMemory();
          if (memFlipped.length === 2) {
            const [a, b] = memFlipped;
            if (memCards[a] === memCards[b]) {
              memMatched.add(a); memMatched.add(b);
              memFlipped = [];
              if (memMatched.size === memCards.length) $("memory-status").textContent = "כל הכבוד! השלמת את כל הלוח 🎉";
              renderMemory();
            } else {
              setTimeout(() => { memFlipped = []; renderMemory(); }, 650);
            }
          }
        };
        g.appendChild(btn);
      });
    }
    $("memory-size").onchange = initMemory;
    $("memory-reset").onclick = initMemory;
    initMemory();

    // 5. ניחוש מספר עם חדרים, טווח מותאם ומנהל חדר שבוחר מספר בשקט
    let numRooms = [
      { id: "nr-1", name: "חדר עד 1,000", maxNum: 1000, hostName: "מנהל החדר", secret: null, guesses: [] },
      { id: "nr-2", name: "אתגר עד 1,500", maxNum: 1500, hostName: "מנהל החדר", secret: null, guesses: [] }
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
      $("num-guess-input").min = 1;
      $("num-guess-input").max = r.maxNum;
      $("num-secret-input").value = r.secret !== null ? String(r.secret) : "";
      $("num-secret-status").textContent = r.secret !== null
        ? "✓ מספר סודי נקבע בשקט לחדר זה! המשתתפים יכולים לנחש."
        : "עדיין לא נקבע מספר סודי — הזן מספר בשקט או לחץ 'קבע מספר סודי' להגרלה שקטה.";

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
      const newRoom = { id: `nr-${Date.now()}`, name, maxNum, hostName: me.name || "מנהל החדר", secret: null, guesses: [] };
      numRooms.unshift(newRoom);
      activeNumRoomId = newRoom.id;
      $("num-room-name").value = "";
      renderNumRooms();
      renderActiveNumRoom();
    };

    $("num-toggle-secret").onclick = () => {
      $("num-secret-input").type = $("num-secret-input").type === "password" ? "number" : "password";
    };

    $("num-set-secret-btn").onclick = () => {
      const r = numRooms.find((x) => x.id === activeNumRoomId) || numRooms[0];
      const typed = Number($("num-secret-input").value);
      const chosen = (typed >= 1 && typed <= r.maxNum)
        ? typed
        : Math.floor(Math.random() * r.maxNum) + 1;
      r.secret = chosen;
      r.guesses = [];
      $("num-guess-feedback").textContent = "מספר סודי עודכן בשקט! אפשר להתחיל לנחש.";
      renderActiveNumRoom();
    };

    $("num-guess-btn").onclick = () => {
      const r = numRooms.find((x) => x.id === activeNumRoomId) || numRooms[0];
      if (r.secret === null) {
        r.secret = Math.floor(Math.random() * r.maxNum) + 1;
      }
      const val = Number($("num-guess-input").value);
      if (!val || val < 1 || val > r.maxNum) {
        $("num-guess-feedback").textContent = `הכנס מספר בין 1 ל-${r.maxNum.toLocaleString()}.`;
        return;
      }
      let hit = false;
      let msg = "";
      if (val === r.secret) {
        hit = true;
        msg = "ניחש נכון! 🎉";
        $("num-guess-feedback").textContent = `🎉 בול! ${me.name || "שחקן"} ניחש את המספר ${r.secret}!`;
      } else if (val < r.secret) {
        msg = "נמוך מהמספר (לא נכון)";
        $("num-guess-feedback").textContent = `המספר ${val} נמוך מהמספר הסודי — נסה מספר גבוה יותר ⬆️`;
      } else {
        msg = "גבוה מהמספר (לא נכון)";
        $("num-guess-feedback").textContent = `המספר ${val} גבוה מהמספר הסודי — נסה מספר נמוך יותר ⬇️`;
      }
      r.guesses.unshift({ player: me.name || "משתמש", value: val, hit, msg });
      $("num-guess-input").value = "";
      renderActiveNumRoom();
    };

    renderNumRooms();
    renderActiveNumRoom();

    const savedSession = localStorage.getItem("toplove_session");
    if (savedSession) {
      try { openApp(JSON.parse(savedSession)); } catch {}
    }
  </script>
</body>
</html>
