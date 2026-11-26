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
      background: rgba(30, 41, 59, 0.84);
      backdrop-filter: blur(12px);
      border: 1px solid rgba(255, 255, 255, 0.14);
    }
    .bg-aurora { background: linear-gradient(120deg, #ec4899, #8b5cf6, #06b6d4); }
    .bg-sunset { background: linear-gradient(120deg, #f97316, #ec4899, #a855f7); }
    .bg-royal  { background: linear-gradient(120deg, #4f46e5, #9333ea, #db2777); }
    .bg-emeraldLux { background: linear-gradient(120deg, #059669, #0d9488, #2563eb); }
    .name-rainbow {
      background: linear-gradient(90deg, #f472b6, #c084fc, #38bdf8, #34d399, #fbbf24);
      -webkit-background-clip: text;
      background-clip: text;
      color: transparent;
    }
    .name-roseGold {
      background: linear-gradient(90deg, #fda4af, #f43f5e, #fbbf24);
      -webkit-background-clip: text;
      background-clip: text;
      color: transparent;
    }
    .name-neon {
      color: #67e8f9;
      text-shadow: 0 0 12px rgba(103, 232, 249, 0.65);
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
  <header class="glass sticky top-0 z-40 px-6 py-4 flex flex-wrap items-center justify-between gap-3 shadow-lg">
    <div class="flex items-center gap-2">
      <span class="text-2xl">💜</span>
      <h1 class="text-xl font-bold bg-gradient-to-l from-pink-400 to-indigo-400 bg-clip-text text-transparent">TopLove IL</h1>
      <span class="text-xs bg-emerald-500/20 border border-emerald-400/40 text-emerald-200 px-2.5 py-0.5 rounded-full">
        חינם לגמרי • 18+
      </span>
    </div>
    <div class="flex flex-wrap items-center gap-2.5">
      <span id="header-stats" class="hidden text-xs font-bold bg-amber-500/20 border border-amber-400/40 text-amber-200 px-3 py-1 rounded-full">
        רמה 0 • 0 נק׳ • 0 נצ׳ / 0 הפס׳
      </span>
      <span id="user-badge" class="hidden text-sm text-slate-200 bg-slate-800 px-3 py-1 rounded-full"></span>
      <button id="logout-btn" type="button" class="hidden bg-rose-600 hover:bg-rose-500 text-sm px-4 py-1.5 rounded-lg">התנתק</button>
    </div>
  </header><div id="user-modal" class="hidden fixed inset-0 z-50 bg-black/75 backdrop-blur-sm flex items-center justify-center p-4">
    <div class="glass max-w-lg w-full rounded-3xl overflow-hidden border border-pink-400/40 shadow-2xl">
      <div id="modal-banner" class="h-28 bg-aurora relative p-4 flex justify-between items-start">
        <span id="modal-level-badge" class="text-xs font-extrabold px-3 py-1 rounded-full bg-slate-950/80 border border-white/25"></span>
        <button type="button" id="close-modal-btn" class="w-8 h-8 rounded-full bg-slate-950/80 text-white font-bold">✕</button>
      </div>
      <div class="p-6 -mt-12 space-y-4">
        <div class="flex items-end gap-4">
          <img id="modal-main-photo" src="" alt="" class="w-24 h-24 rounded-2xl object-cover border-4 border-slate-900 bg-slate-800 shadow-xl" />
          <div class="space-y-1">
            <h3 id="modal-name" class="text-xl font-extrabold"></h3>
            <div id="modal-sticker" class="text-xs text-amber-300 font-bold"></div>
            <p id="modal-tagline" class="text-xs text-pink-200"></p>
          </div>
        </div>

        <div id="modal-gallery" class="flex gap-2 overflow-x-auto pb-1"></div>

        <div class="text-xs text-slate-200 bg-slate-900/80 p-3 rounded-xl border border-slate-800 space-y-1">
          <div id="modal-meta"></div>
          <div id="modal-habits"></div>
          <div id="modal-education"></div>
          <div id="modal-bio" class="text-slate-300 pt-1"></div>
        </div>

        <div class="space-y-1.5">
          <div class="text-xs font-bold text-pink-300">✨ אוהב/ת לעשות ותחביבים:</div>
          <div id="modal-tags" class="flex flex-wrap gap-1.5 text-xs"></div>
        </div>

        <div class="flex flex-wrap gap-2 pt-2">
          <button type="button" id="modal-follow-btn" class="flex-1 py-2.5 rounded-xl text-xs font-bold bg-indigo-600 hover:bg-indigo-500">
            ➕ עקוב
          </button>
          <button type="button" id="modal-dm-btn" class="flex-1 py-2.5 rounded-xl text-xs font-bold bg-pink-600 hover:bg-pink-500">
            ✉️ שלח הודעה אישית
          </button>
        </div>
      </div>
    </div>
  </div><main class="max-w-6xl mx-auto px-4 py-8 space-y-6">
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
        <button type="button" data-tab="users" class="tab-btn px-4 py-2 rounded-xl text-sm font-semibold glass text-slate-300">2. משתמשים וצ׳אט אישי 👥</button>
        <button type="button" data-tab="chat" class="tab-btn px-4 py-2 rounded-xl text-sm font-semibold glass text-slate-300">3. חדרי שיחה 💬</button>
        <button type="button" data-tab="games" class="tab-btn px-4 py-2 rounded-xl text-sm font-semibold glass text-slate-300">4. משחקים ודירוגים 🎮</button>
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

        <div id="profile-summary-card" class="hidden bg-slate-900/85 border border-pink-500/30 rounded-2xl overflow-hidden shadow-xl">
          <div id="summary-banner" class="h-28 bg-aurora p-4 flex items-center justify-between">
            <span id="summary-level-badge" class="text-xs font-extrabold px-3 py-1 rounded-full bg-slate-950/75 border border-white/20"></span>
            <span id="summary-trophy-badge" class="text-xs font-extrabold px-3 py-1 rounded-full bg-amber-500/25 border border-amber-300/40 text-amber-200"></span>
          </div>
          <div class="p-6 -mt-12 space-y-6">
            <div class="flex flex-col sm:flex-row items-center sm:items-end gap-5">
              <img id="summary-avatar" src="https://api.dicebear.com/9.x/avataaars/svg?seed=TopLove" alt=""
                class="w-32 h-32 rounded-2xl object-cover border-4 border-slate-900 bg-slate-800 shrink-0 shadow-lg cursor-pointer" />
              <div class="space-y-1.5 text-center sm:text-right flex-1">
                <h3 id="summary-name" class="text-2xl font-extrabold"></h3>
                <div id="summary-sticker" class="text-xs font-bold text-amber-300"></div>
                <p id="summary-tagline" class="text-sm text-pink-200 font-medium"></p>
                <p id="summary-age-gender-loc" class="text-xs text-indigo-200"></p>
                <p id="summary-habits" class="text-xs text-emerald-200"></p>
                <p id="summary-bio" class="text-sm text-slate-300 pt-1"></p>
              </div>
            </div>

            <div id="summary-photos-strip" class="flex gap-2.5 overflow-x-auto pb-1"></div>

            <div class="grid grid-cols-1 md:grid-cols-3 gap-4 pt-2 border-t border-white/10">
              <div class="bg-slate-950/70 rounded-xl p-4 border border-slate-800 space-y-2">
                <div class="text-xs font-bold text-pink-300">✨ מה אני אוהב/ת לעשות</div>
                <div id="summary-likes" class="flex flex-wrap gap-1.5 text-xs"></div>
              </div>
              <div class="bg-slate-950/70 rounded-xl p-4 border border-slate-800 space-y-2">
                <div class="text-xs font-bold text-indigo-300">🎯 תחביבים</div>
                <div id="summary-hobbies" class="flex flex-wrap gap-1.5 text-xs"></div>
              </div>
              <div class="bg-slate-950/70 rounded-xl p-4 border border-slate-800 space-y-2">
                <div class="text-xs font-bold text-emerald-300">🎓 השכלה ופרסים</div>
                <div id="summary-education" class="text-xs text-slate-200"></div>
              </div>
            </div>
          </div>
        </div>

        <form id="profile-form" class="space-y-6">
          <div class="bg-slate-900/75 p-5 rounded-2xl border border-slate-700 space-y-4">
            <div class="flex flex-col md:flex-row items-center gap-6">
              <div id="prof-avatar-frame" class="p-2 rounded-3xl bg-aurora shadow-lg shrink-0">
                <img id="prof-avatar-preview" src="https://api.dicebear.com/9.x/avataaars/svg?seed=TopLove" alt=""
                  class="w-28 h-28 rounded-2xl object-cover bg-slate-800" />
              </div>
              <div class="w-full space-y-3">
                <label class="block text-sm font-semibold text-pink-300">בחירת תמונות פרופיל (אפשר להעלות כמה תמונות)</label>
                <input type="file" id="prof-avatar-file" accept="image/*" multiple
                  class="block w-full text-xs text-slate-300 file:ml-3 file:py-2 file:px-4 file:rounded-xl file:border-0 file:bg-pink-600 file:text-white file:font-semibold" />
                <input type="url" id="prof-avatar-url" placeholder="הוסף קישור לתמונה נוספת (https://...)" dir="ltr"
                  class="w-full px-4 py-2 text-sm rounded-xl bg-slate-950 border border-slate-700 text-left" />
                <div id="prof-photos-thumbs" class="flex flex-wrap gap-2"></div>
              </div>
            </div>

            <div class="grid grid-cols-1 sm:grid-cols-3 gap-3 pt-2 border-t border-white/10">
              <div>
                <label class="block text-xs text-slate-300 mb-1">רקע מעניין לפרופיל</label>
                <select id="prof-banner" class="w-full px-3 py-2 rounded-xl bg-slate-950 border border-slate-700 text-xs">
                  <option value="bg-aurora">זוהר צפוני (ורוד-סגול-טורקיז)</option>
                  <option value="bg-sunset">שקיעה חמה (כתום-ורוד-סגול)</option>
                  <option value="bg-royal">מלכותי (אינדיגו-סגול-מג׳נטה)</option>
                  <option value="bg-emeraldLux">יער יוקרתי (ירוק-טורקיז-כחול)</option>
                </select>
              </div>
              <div>
                <label class="block text-xs text-slate-300 mb-1">סגנון שם צבעוני</label>
                <select id="prof-name-style" class="w-full px-3 py-2 rounded-xl bg-slate-950 border border-slate-700 text-xs">
                  <option value="name-rainbow">צבעוני קשת</option>
                  <option value="name-roseGold">רוז-גולד זוהר</option>
                  <option value="name-neon">ניאון טורקיז</option>
                  <option value="">רגיל ונקי</option>
                </select>
              </div>
              <div>
                <label class="block text-xs text-slate-300 mb-1">כתובית מעניינת ליד השם (לא חובה)</label>
                <input type="text" id="prof-tagline" placeholder="למשל: מחפשת אנרגיות טובות ✨"
                  class="w-full px-3 py-2 rounded-xl bg-slate-950 border border-slate-700 text-xs" />
              </div>
            </div>
          </div><div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-3.5">
            <div>
              <label class="block text-xs text-slate-300 mb-1">שם משתמש</label>
              <input type="text" id="prof-name" placeholder="שם משתמש"
                class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700 text-sm" />
            </div>
            <div>
              <label class="block text-xs text-slate-300 mb-1">מין</label>
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
              <label class="block text-xs text-slate-300 mb-1">מדינה / עיר</label>
              <input type="text" id="prof-location" placeholder="למשל: ישראל, כרמיאל"
                class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700 text-sm" />
            </div>
          </div>

          <div class="grid grid-cols-1 sm:grid-cols-3 gap-3.5">
            <div>
              <label class="block text-xs text-slate-300 mb-1">עישון (לא חובה)</label>
              <select id="prof-smoking" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-900 border border-slate-700 text-sm">
                <option value="">לא צוין</option>
                <option value="לא מעשן/ת">לא מעשן/ת</option>
                <option value="מעשן/ת לעיתים רחוקות">מעשן/ת לעיתים רחוקות</option>
                <option value="מעשן/ת">מעשן/ת</option>
                <option value="מעשן/ת תמיד / כל הזמן">מעשן/ת תמיד / כל הזמן</option>
              </select>
            </div>
            <div>
              <label class="block text-xs text-slate-300 mb-1">אלכוהול (לא חובה)</label>
              <select id="prof-alcohol" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-900 border border-slate-700 text-sm">
                <option value="">לא צוין</option>
                <option value="אף פעם">אף פעם</option>
                <option value="כמעט ולא">כמעט ולא</option>
                <option value="מידי פעם">מידי פעם</option>
                <option value="קבוע">קבוע</option>
              </select>
            </div>
            <div>
              <label class="block text-xs text-slate-300 mb-1">השכלה (לא חובה)</label>
              <input type="text" id="prof-education" placeholder="למשל: תואר ראשון, הנדסאי..."
                class="w-full px-3.5 py-2.5 rounded-xl bg-slate-900 border border-slate-700 text-sm" />
            </div>
          </div>

          <div class="bg-slate-900/70 p-4 rounded-2xl border border-slate-800 space-y-2.5">
            <label class="block text-sm font-bold text-pink-300">מה אני אוהב/ת לעשות? (לא חובה)</label>
            <div id="likes-options" class="flex flex-wrap gap-2"></div>
          </div>

          <div class="bg-slate-900/70 p-4 rounded-2xl border border-slate-800 space-y-2.5">
            <label class="block text-sm font-bold text-indigo-300">תחביבים עם אימוג׳ים (מגוון רחב — לא חובה)</label>
            <div id="hobbies-options" class="flex flex-wrap gap-2"></div>
          </div>

          <div>
            <label class="block text-xs text-slate-300 mb-1">תיאור קצר (לא חובה)</label>
            <textarea id="prof-bio" rows="2" placeholder="ספר/י על עצמך..."
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
      </div><div id="tab-users" class="tab-content hidden max-w-5xl mx-auto glass rounded-2xl p-6 space-y-5">
        <div class="flex flex-wrap items-center justify-between gap-2">
          <h2 class="text-xl font-bold">👥 משתמשים, עוקבים והודעות אישיות</h2>
          <span id="following-count-badge" class="text-xs px-3 py-1 rounded-full bg-indigo-500/20 border border-indigo-400/40 text-indigo-200">
            עוקב אחרי 0 משתמשים
          </span>
        </div>
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
            <h3 class="text-sm font-bold text-slate-200">🗂️ חדרי שיחה (לחץ "כנס לחדר" לכניסה)</h3>
            <div id="rooms-list" class="space-y-2 max-h-96 overflow-y-auto"></div>
          </div>

          <div class="lg:col-span-2 bg-slate-900/70 border border-slate-800 rounded-2xl p-4 flex flex-col justify-between min-h-[390px] space-y-3">
            <div class="border-b border-white/10 pb-2 flex flex-wrap items-center justify-between gap-2">
              <div>
                <h3 id="active-room-title" class="font-bold text-base">בחר חדר ולחץ "כנס לחדר"</h3>
                <p id="active-room-meta" class="text-xs text-slate-400">לא מחובר לחדר כרגע</p>
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
                <input type="text" id="chat-input" required placeholder="כתוב הודעה..."
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
              <div class="text-xs text-slate-400">רמה (0 עד 30)</div>
              <div id="stat-level" class="text-xl font-extrabold text-pink-300 mt-0.5">רמה 0</div>
              <div id="stat-level-sticker" class="text-[11px] text-amber-300 mt-0.5">🌱 מתחיל</div>
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

          <div class="bg-slate-950/75 rounded-xl p-3.5 border border-indigo-500/25 flex flex-wrap items-center justify-between gap-3">
            <div class="space-y-1">
              <div class="text-xs font-bold text-indigo-200">🏆 פרסי טופ-1 במשחקים ובחירת סמל/חומר</div>
              <div id="top-ranks-summary" class="text-[11px] text-slate-300"></div>
            </div>
            <div class="flex flex-wrap items-center gap-2 text-xs">
              <label class="text-slate-300">סמל/חומר מועדף:</label>
              <select id="reward-pref-select" class="px-2.5 py-1 rounded-lg bg-slate-900 border border-slate-700 text-xs">
                <option value="❌ אלומיניום">❌ אלומיניום</option>
                <option value="❌ ברזל">❌ ברזל</option>
                <option value="❌ זהב">❌ זהב</option>
                <option value="❌ יהלומים">❌ יהלומים</option>
                <option value="⭕ זהב">⭕ עיגול מזהב</option>
                <option value="🪨 זהב">🪨 אבן מזהב</option>
                <option value="📄 זהב">📄 נייר מזהב</option>
                <option value="✂️ זהב">✂️ מספריים מזהב</option>
              </select>
            </div>
          </div>
        </div>

        <div class="flex flex-wrap gap-2 justify-center">
          <button type="button" data-game="ttt" class="game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold bg-pink-600">1. איקס עיגול (100+ חדרים)</button>
          <button type="button" data-game="rps" class="game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold glass text-slate-300">2. אבן נייר מספריים (100+ חדרים)</button>
          <button type="button" data-game="memory" class="game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold glass text-slate-300">3. זיכרון (קל עד קשה + חדר אישי)</button>
          <button type="button" data-game="number" class="game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold glass text-slate-300">4. ניחוש מספר (עד 50 בחדר • +3 נק׳)</button>
        </div>

        <div id="game-ttt" class="game-panel max-w-4xl mx-auto glass rounded-2xl p-6 space-y-5">
          <div class="flex flex-wrap items-center justify-between gap-2 border-b border-white/10 pb-3">
            <div>
              <h3 class="text-xl font-bold">📦 איקס עיגול — 100 חדרים + יצירת חדרים</h3>
              <p class="text-xs text-slate-300">לחץ על חדר פנוי והמתן שמשתמש נוסף יצטרף מולך</p>
            </div>
            <div class="flex flex-wrap items-center gap-2">
              <span id="ttt-timer" class="px-3 py-1 rounded-full text-xs font-bold bg-amber-500/20 border border-amber-400/40 text-amber-200">⏱️ 00:30</span>
              <button type="button" id="ttt-add-room" class="px-3.5 py-1.5 rounded-xl text-xs font-semibold bg-emerald-600 hover:bg-emerald-500">+ צור חדר איקס עיגול</button>
              <button type="button" id="ttt-leave-room" class="hidden px-3 py-1.5 rounded-xl text-xs font-semibold bg-rose-600 hover:bg-rose-500">צא מהחדר</button>
            </div>
          </div>

          <div id="ttt-rooms-grid" class="grid grid-cols-2 sm:grid-cols-4 md:grid-cols-5 gap-2 max-h-56 overflow-y-auto p-1"></div>

          <div class="bg-slate-950/75 border border-amber-500/25 rounded-2xl p-4 space-y-4">
            <div class="grid grid-cols-3 items-center gap-2 text-center">
              <div class="flex flex-col items-center gap-1">
                <div class="w-12 h-12 rounded-full border-2 border-amber-400 bg-slate-800 flex items-center justify-center text-lg">❌</div>
                <span id="ttt-p1-name" class="text-xs font-bold text-slate-300">מושב 1 ריק</span>
              </div>
              <div id="ttt-board" class="grid grid-cols-3 gap-1.5 bg-amber-950/70 p-2.5 rounded-xl border border-amber-700/60 max-w-[220px] w-full mx-auto"></div>
              <div class="flex flex-col items-center gap-1">
                <div class="w-12 h-12 rounded-full border-2 border-pink-400 bg-slate-800 flex items-center justify-center text-lg">⭕</div>
                <span id="ttt-p2-name" class="text-xs font-bold text-slate-400">ממתין לכניסה...</span>
              </div>
            </div>
            <div class="flex flex-wrap items-center justify-between gap-2">
              <p id="ttt-status" class="text-sm text-pink-200">בחר חדר איקס עיגול כדי להיכנס</p>
              <button type="button" id="ttt-reset" class="text-xs bg-slate-800 px-3 py-1.5 rounded-lg border border-slate-600">איפוס לוח</button>
            </div>
          </div>
        </div><div id="game-rps" class="game-panel hidden max-w-4xl mx-auto glass rounded-2xl p-6 space-y-5">
          <div class="flex flex-wrap items-center justify-between gap-2 border-b border-white/10 pb-3">
            <div>
              <h3 class="text-xl font-bold">✂️ אבן נייר מספריים — 100 חדרים + יצירת חדרים</h3>
              <p class="text-xs text-slate-300">היכנס לחדר פנוי והמתן שמשתמש נוסף ילחץ להיכנס מולך — ספירה עד 3</p>
            </div>
            <div class="flex flex-wrap items-center gap-2">
              <span id="rps-timer" class="px-3 py-1 rounded-full text-xs font-bold bg-pink-500/20 border border-pink-400/40 text-pink-200">⏱️ 00:15</span>
              <button type="button" id="rps-add-room" class="px-3.5 py-1.5 rounded-xl text-xs font-semibold bg-emerald-600 hover:bg-emerald-500">+ צור חדר אבן נייר מספריים</button>
              <button type="button" id="rps-leave-room" class="hidden px-3 py-1.5 rounded-xl text-xs font-semibold bg-rose-600 hover:bg-rose-500">צא מהחדר</button>
            </div>
          </div>

          <div id="rps-rooms-grid" class="grid grid-cols-2 sm:grid-cols-4 md:grid-cols-5 gap-2 max-h-56 overflow-y-auto p-1"></div>

          <div class="bg-slate-950/75 border border-white/10 rounded-2xl p-4 space-y-4 text-center">
            <div class="grid grid-cols-3 items-center gap-3">
              <div class="flex flex-col items-center gap-1.5">
                <div id="rps-left-avatar" class="w-14 h-14 rounded-full border-2 border-pink-400 bg-slate-800 flex items-center justify-center text-xl">🪑</div>
                <span id="rps-left-name" class="text-xs font-bold text-slate-400">מושב 1 פנוי</span>
                <div id="rps-left-sign" class="w-16 h-16 rounded-2xl bg-slate-900 border border-slate-700 flex items-center justify-center text-3xl">✊</div>
              </div>

              <div class="flex flex-col items-center justify-center gap-1">
                <span class="text-xs text-slate-400">ספירה:</span>
                <div id="rps-count-num" class="text-3xl font-extrabold text-pink-300 count-anim">1 • 2 • 3</div>
                <span id="rps-round-phase" class="text-xs text-indigo-200">בחר חדר כדי להיכנס</span>
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
            <p id="rps-result" class="text-sm text-pink-200 bg-slate-900 p-3.5 rounded-xl">לחץ על אחד מחדרי אבן נייר מספריים כדי להיכנס</p>
          </div>
        </div>

        <div id="game-memory" class="game-panel hidden max-w-4xl mx-auto glass rounded-2xl p-6 space-y-4">
          <div class="flex flex-wrap items-center justify-between gap-2 border-b border-white/10 pb-3">
            <div>
              <h3 class="text-xl font-bold">💎 זיכרון — חדרים קלים עד קשים + חדר משלך</h3>
              <p class="text-xs text-slate-300">הצטרף לחדר קיים או פתח חדר זיכרון משלך ובחר רמת קושי/סוג לוח</p>
            </div>
            <div class="flex flex-wrap items-center gap-2">
              <span id="memory-timer" class="px-3 py-1 rounded-full text-xs font-bold bg-emerald-500/20 border border-emerald-400/40 text-emerald-200">⏱️ 02:00</span>
              <button type="button" id="memory-leave-room" class="hidden px-3 py-1.5 rounded-xl text-xs font-semibold bg-rose-600 hover:bg-rose-500">צא מהחדר</button>
              <button type="button" id="memory-reset" class="text-xs bg-pink-600 px-3.5 py-1.5 rounded-xl font-semibold">ערבב לוח</button>
            </div>
          </div>

          <form id="mem-create-room-form" class="flex flex-col sm:flex-row gap-2.5 bg-slate-900/75 p-3 rounded-xl border border-slate-700">
            <input type="text" id="mem-room-name" required placeholder="שם חדר הזיכרון שלך..."
              class="flex-1 px-3.5 py-2 rounded-xl bg-slate-950 border border-slate-700 text-sm" />
            <select id="mem-room-mode" class="px-3.5 py-2 rounded-xl bg-slate-950 border border-slate-700 text-xs">
              <option value="easy">קל (4×4 • אימוג׳ים ברורים)</option>
              <option value="medium">בינוני (6×4 • 12 זוגות)</option>
              <option value="hard" selected>קשה (6×6 • פרצופים דומים מאוד)</option>
            </select>
            <button type="submit" class="px-4 py-2 rounded-xl text-xs font-semibold bg-emerald-600 hover:bg-emerald-500">
              + פתח חדר משלי
            </button>
          </form>

          <div id="memory-rooms-grid" class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 gap-2 max-h-48 overflow-y-auto p-1"></div>

          <div id="memory-players-board" class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-6 gap-2 bg-slate-950/75 p-3 rounded-xl border border-white/10 text-xs"></div>

          <div id="memory-grid" class="grid grid-cols-6 gap-2 max-w-xl mx-auto"></div>
          <p id="memory-status" class="text-sm text-center text-pink-200">בחר חדר זיכרון או פתח חדר חדש כדי להתחיל</p>
        </div><div id="game-number" class="game-panel hidden max-w-3xl mx-auto glass rounded-2xl p-6 space-y-4">
          <div class="border-b border-white/10 pb-3">
            <h3 class="text-xl font-bold">🎯 ניחוש מספר — עד 50 משתתפים בחדר (הכי קרוב = +3 נקודות)</h3>
            <p class="text-xs text-slate-300">מנהל החדר קובע מספר בשקט (למשל 1–1000), המשתתפים מנחשים, והכי קרוב מנצח ומקבל 3 נקודות</p>
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

          <div id="num-rooms-list" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-2.5"></div>

          <div class="bg-slate-950/75 border border-indigo-500/30 rounded-2xl p-4 space-y-4">
            <div class="flex flex-wrap items-center justify-between gap-2">
              <div id="num-room-header" class="font-bold text-sm text-pink-200"></div>
              <div id="num-room-cap" class="text-xs px-3 py-1 rounded-full bg-indigo-500/20 text-indigo-200"></div>
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
                  שלח ניחוש
                </button>
                <button type="button" id="num-declare-winner-btn" class="px-4 py-2.5 rounded-xl text-xs font-bold bg-emerald-600 hover:bg-emerald-500">
                  🏆 הכרז על הכי קרוב (+3 נק׳)
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

    const levelThresholds = Array.from({ length: 31 }, (_, lvl) => {
      if (lvl === 0) return 0;
      if (lvl === 1) return 100;
      if (lvl === 2) return 300;
      if (lvl === 3) return 600;
      return 600 + (lvl - 3) * 400;
    });

    const levelStickers = [
      "🌱 מדבקת רמה 0 • צעד ראשון", "⭐ מדבקת רמה 1 • כוכב עולה", "🔥 מדבקת רמה 2 • להבה",
      "💎 מדבקת רמה 3 • יהלום", "🚀 מדבקת רמה 4 • המראה", "👑 מדבקת רמה 5 • כתר",
      "⚡ מדבקת רמה 6 • ברק", "🦋 מדבקת רמה 7 • פרפר", "🎯 מדבקת רמה 8 • צלף",
      "🌊 מדבקת רמה 9 • גל", "🌈 מדבקת רמה 10 • קשת בענן", "🦁 מדבקת רמה 11 • אריה",
      "🔮 מדבקת רמה 12 • קסם", "🏆 מדבקת רמה 13 • אלוף", "🎼 מדבקת רמה 14 • הרמוניה",
      "🪐 מדבקת רמה 15 • גלקסיה", "🐉 מדבקת רמה 16 • דרקון", "🌸 מדבקת רמה 17 • פריחה",
      "🛡️ מדבקת רמה 18 • מגן", "☀️ מדבקת רמה 19 • זריחה", "🎇 מדבקת רמה 20 • זיקוקים",
      "🦅 מדבקת רמה 21 • נשר", "💠 מדבקת רמה 22 • קריסטל", "🌋 מדבקת רמה 23 • עוצמה",
      "🎭 מדבקת רמה 24 • כריזמה", "🧿 מדבקת רמה 25 • קמע", "🌟 מדבקת רמה 26 • סופרסטאר",
      "⚜️ מדבקת רמה 27 • אצולה", "🌌 מדבקת רמה 28 • אינסוף", "🔱 מדבקת רמה 29 • קילשון הזהב",
      "🏅 מדבקת רמה 30 • אגדת TopLove"
    ];

    function getLevel(pts = 0) {
      let current = 0;
      for (let i = 1; i < levelThresholds.length; i++) {
        if (pts >= levelThresholds[i]) current = i;
      }
      return current;
    }

    function getLevelSticker(lvl) {
      return levelStickers[Math.min(Math.max(0, lvl), 30)];
    }

    const likesChoices = [
      "☕ לצאת לבתי קפה", "🎬 לראות סרטים וסדרות", "🤝 להכיר אנשים חדשים",
      "🎶 מוזיקה חיה והופעות", "🍽️ אוכל טוב ומסעדות", "💬 שיחות עמוקות וצחוק",
      "🌅 שקיעות וחוף הים", "🛍️ שופינג ואופנה", "🎲 משחקי חברה וערב חברים"
    ];

    const hobbiesChoices = [
      "🥾 טיולים", "🏋️ ספורט וכושר", "📷 צילום", "🍳 בישול ואפייה",
      "🎮 גיימינג", "📚 קריאה", "💃 ריקוד", "🎸 נגינה", "🎨 ציור ואמנות",
      "🚴 רכיבת אופניים", "🏕️ קמפינג", "🧘 יוגה ומדיטציה", "🐶 גידול חיות מחמד",
      "✈️ נסיעות לחו״ל", "♟️ משחקי אסטרטגיה", "🌱 גינון", "🎤 שירה וקריוקי", "📸 עריכת וידאו"
    ];const me = {
      uid: "", email: "", name: "", gender: "", age: 18,
      location: "", smoking: "", alcohol: "", education: "",
      tagline: "", banner: "bg-aurora", nameStyle: "name-rainbow",
      rewardPref: "❌ זהב", bio: "",
      likes: [], hobbies: [], photos: [], following: [],
      avatar: "https://api.dicebear.com/9.x/avataaars/svg?seed=TopLove",
      profileCompleted: false, points: 0, wins: 0, losses: 0
    };

    const topGameLeaders = {
      ttt: { name: "אין עדיין מוביל", score: 0 },
      rps: { name: "אין עדיין מוביל", score: 0 },
      memory: { name: "אין עדיין מוביל", score: 0 },
      number: { name: "אין עדיין מוביל", score: 0 }
    };

    function updateTopLeader(gameKey, playerName, addPts) {
      const cur = topGameLeaders[gameKey];
      const nextScore = (cur.name === playerName ? cur.score : 0) + addPts;
      if (nextScore >= cur.score) topGameLeaders[gameKey] = { name: playerName, score: nextScore };
      renderTopRanksSummary();
    }

    function renderTopRanksSummary() {
      $("top-ranks-summary").innerHTML =
        `❌⭕ איקס עיגול: <strong>${topGameLeaders.ttt.name}</strong> (${topGameLeaders.ttt.score} נק׳) • ` +
        `✂️ אב״נ: <strong>${topGameLeaders.rps.name}</strong> (${topGameLeaders.rps.score} נק׳) • ` +
        `💎 זיכרון: <strong>${topGameLeaders.memory.name}</strong> (${topGameLeaders.memory.score} נק׳) • ` +
        `🎯 מספר: <strong>${topGameLeaders.number.name}</strong> (${topGameLeaders.number.score} נק׳)`;
    }

    function renderStats() {
      const lvl = getLevel(me.points);
      $("stat-level").textContent = `רמה ${lvl}`;
      $("stat-level-sticker").textContent = getLevelSticker(lvl);
      $("stat-points").textContent = String(me.points || 0);
      $("stat-wins").textContent = String(me.wins || 0);
      $("stat-losses").textContent = String(me.losses || 0);
      $("header-stats").textContent = `רמה ${lvl} • ${me.points || 0} נק׳ • ${me.wins || 0} נצ׳ / ${me.losses || 0} הפס׳`;
      localStorage.setItem("toplove_session", JSON.stringify(me));
    }

    async function awardWin(pts = 25, gameKey = "ttt") {
      me.wins = (me.wins || 0) + 1;
      me.points = (me.points || 0) + pts;
      updateTopLeader(gameKey, me.name || "שחקן", pts);
      renderStats();
      try { if (me.uid) await setDoc(doc(db, "users", me.uid), { points: me.points, wins: me.wins }, { merge: true }); } catch {}
    }

    async function awardLoss(pts = 5) {
      me.losses = (me.losses || 0) + 1;
      me.points = (me.points || 0) + pts;
      renderStats();
      try { if (me.uid) await setDoc(doc(db, "users", me.uid), { points: me.points, losses: me.losses }, { merge: true }); } catch {}
    }

    $("reward-pref-select").onchange = (e) => {
      me.rewardPref = e.target.value;
      renderStats(); applyProfileViewMode();
    };

    function openUserModal(person) {
      const lvl = getLevel(person.points || 0);
      const photos = Array.isArray(person.photos) && person.photos.length ? person.photos : [person.avatar];
      $("modal-banner").className = `h-28 ${person.banner || "bg-aurora"} relative p-4 flex justify-between items-start`;
      $("modal-level-badge").textContent = `רמה ${lvl} • ${person.points || 0} נק׳`;
      $("modal-main-photo").src = photos[0];
      $("modal-name").className = `text-xl font-extrabold ${person.nameStyle || ""}`;
      $("modal-name").textContent = person.name || "משתמש";
      $("modal-sticker").textContent = `${getLevelSticker(lvl)} • פרס מועדף: ${person.rewardPref || "❌ זהב"}`;
      $("modal-tagline").textContent = person.tagline || "";
      $("modal-meta").textContent = [person.gender, person.age ? `גיל ${person.age}` : "", person.location].filter(Boolean).join(" • ");
      $("modal-habits").textContent = [person.smoking ? `🚬 ${person.smoking}` : "", person.alcohol ? `🍷 ${person.alcohol}` : ""].filter(Boolean).join(" • ");
      $("modal-education").textContent = person.education ? `🎓 השכלה: ${person.education}` : "";
      $("modal-bio").textContent = person.bio || "";

      $("modal-gallery").innerHTML = photos.map((src) =>
        `<img src="${src}" alt="" class="w-14 h-14 rounded-xl object-cover border border-white/20 cursor-pointer shrink-0 modal-thumb" />`
      ).join("");
      document.querySelectorAll(".modal-thumb").forEach((img) => { img.onclick = () => { $("modal-main-photo").src = img.src; }; });

      const allTags = [...(person.likes || []), ...(person.hobbies || [])];
      $("modal-tags").innerHTML = allTags.length
        ? allTags.map((t) => `<span class="px-2.5 py-1 rounded-full bg-pink-500/20 border border-pink-400/30">${t}</span>`).join("")
        : `<span class="text-slate-400">לא נבחרו תגיות</span>`;

      const targetId = person.uid || person.id;
      const isFollowing = (me.following || []).includes(targetId);
      $("modal-follow-btn").textContent = isFollowing ? "✓ עוקב" : "➕ עקוב";
      $("modal-follow-btn").onclick = () => {
        if (!targetId || targetId === me.uid) return;
        me.following = me.following || [];
        me.following = me.following.includes(targetId) ? me.following.filter((x) => x !== targetId) : [...me.following, targetId];
        renderStats(); openUserModal(person); renderRealUsers();
      };

      $("modal-dm-btn").onclick = () => {
        if (!targetId || targetId === me.uid) return;
        const dmId = "dm_" + [me.uid, targetId].sort().join("_");
        if (!chatRooms.some((r) => r.id === dmId)) chatRooms.unshift({ id: dmId, topic: `שיחה אישית עם ${person.name || "משתמש"}`, members: [me.uid, targetId] });
        activeRoomId = dmId; joinedRoomId = dmId;
        $("user-modal").classList.add("hidden");
        switchTab("chat"); renderRooms();
      };

      $("user-modal").classList.remove("hidden");
    }

    $("close-modal-btn").onclick = () => $("user-modal").classList.add("hidden");
    $("summary-avatar").onclick = () => openUserModal(me);function renderQuestionnaireOptions() {
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

    function renderPhotoThumbs() {
      me.photos = Array.isArray(me.photos) && me.photos.length ? me.photos : [me.avatar];
      $("prof-avatar-preview").src = me.photos[0];
      $("prof-avatar-frame").className = `p-2 rounded-3xl ${me.banner || "bg-aurora"} shadow-lg shrink-0`;
      $("prof-photos-thumbs").innerHTML = me.photos.map((src, idx) =>
        `<img src="${src}" alt="" data-photo-idx="${idx}" class="w-12 h-12 rounded-xl object-cover border border-white/25 cursor-pointer" />`
      ).join("");
      document.querySelectorAll("[data-photo-idx]").forEach((img) => {
        img.onclick = () => { me.avatar = img.src; $("prof-avatar-preview").src = img.src; };
      });
    }

    function applyProfileViewMode() {
      const showSummary = Boolean(me.profileCompleted);
      $("profile-summary-card").classList.toggle("hidden", !showSummary);
      $("profile-form").classList.toggle("hidden", showSummary);
      $("edit-profile-btn").classList.toggle("hidden", !showSummary);
      if (showSummary) {
        const lvl = getLevel(me.points || 0);
        const photos = Array.isArray(me.photos) && me.photos.length ? me.photos : [me.avatar];
        $("summary-banner").className = `h-28 ${me.banner || "bg-aurora"} p-4 flex items-center justify-between`;
        $("summary-level-badge").textContent = `רמה ${lvl} • ${me.points || 0} נק׳`;
        $("summary-trophy-badge").textContent = `🏅 פרס: ${me.rewardPref || "❌ זהב"}`;
        $("summary-avatar").src = photos[0];
        $("summary-name").className = `text-2xl font-extrabold ${me.nameStyle || ""}`;
        $("summary-name").textContent = me.name || "משתמש";
        $("summary-sticker").textContent = getLevelSticker(lvl);
        $("summary-tagline").textContent = me.tagline || "";
        $("summary-age-gender-loc").textContent = [me.gender, me.age ? `גיל ${me.age}` : "", me.location].filter(Boolean).join(" • ");
        $("summary-habits").textContent = [me.smoking ? `🚬 ${me.smoking}` : "", me.alcohol ? `🍷 ${me.alcohol}` : ""].filter(Boolean).join(" • ");
        $("summary-bio").textContent = me.bio || "";
        $("summary-photos-strip").innerHTML = photos.map((src) => `<img src="${src}" alt="" class="w-16 h-16 rounded-xl object-cover border border-white/20 shrink-0" />`).join("");
        $("summary-likes").innerHTML = me.likes.length ? me.likes.map((l) => `<span class="px-2.5 py-1 rounded-full bg-pink-500/20 border border-pink-400/30">${l}</span>`).join("") : `<span class="text-slate-400">לא נבחר</span>`;
        $("summary-hobbies").innerHTML = me.hobbies.length ? me.hobbies.map((h) => `<span class="px-2.5 py-1 rounded-full bg-indigo-500/20 border border-indigo-400/30">${h}</span>`).join("") : `<span class="text-slate-400">לא נבחר</span>`;
        $("summary-education").textContent = me.education || "לא צוינה השכלה";
      }
    }

    $("edit-profile-btn").onclick = () => { me.profileCompleted = false; applyProfileViewMode(); };

    function switchTab(tabName) {
      document.querySelectorAll(".tab-btn").forEach((b) => {
        b.className = b.dataset.tab === tabName ? "tab-btn px-4 py-2 rounded-xl text-sm font-semibold bg-pink-600 text-white" : "tab-btn px-4 py-2 rounded-xl text-sm font-semibold glass text-slate-300";
      });
      document.querySelectorAll(".tab-content").forEach((c) => c.classList.add("hidden"));
      $(`tab-${tabName}`).classList.remove("hidden");
    }

    function openApp(session) {
      Object.assign(me, session);
      me.likes = Array.isArray(session.likes) ? session.likes : [];
      me.hobbies = Array.isArray(session.hobbies) ? session.hobbies : [];
      me.photos = Array.isArray(session.photos) && session.photos.length ? session.photos : [session.avatar];
      me.following = Array.isArray(session.following) ? session.following : [];
      me.points = Number(session.points) || 0; me.wins = Number(session.wins) || 0; me.losses = Number(session.losses) || 0;

      $("auth-section").classList.add("hidden"); $("app-section").classList.remove("hidden");
      $("user-badge").classList.remove("hidden"); $("header-stats").classList.remove("hidden"); $("logout-btn").classList.remove("hidden");
      $("user-badge").textContent = `${me.name || me.email.split("@")[0]} • ${me.age || 18}`;
      $("prof-name").value = me.name || ""; $("prof-gender").value = me.gender || ""; $("prof-age").value = me.age || 18;
      $("prof-location").value = me.location || ""; $("prof-smoking").value = me.smoking || ""; $("prof-alcohol").value = me.alcohol || "";
      $("prof-education").value = me.education || ""; $("prof-tagline").value = me.tagline || "";
      $("prof-banner").value = me.banner || "bg-aurora"; $("prof-name-style").value = me.nameStyle || "name-rainbow";
      $("reward-pref-select").value = me.rewardPref || "❌ זהב"; $("prof-bio").value = me.bio || "";

      renderStats(); renderTopRanksSummary(); renderPhotoThumbs(); renderQuestionnaireOptions(); applyProfileViewMode();
      switchTab("profile"); renderRooms(); subscribeUsers();
    }

    $("toggle-password-btn").onclick = () => { $("auth-password").type = $("auth-password").type === "password" ? "text" : "password"; };

    $("auth-form").onsubmit = async (e) => {
      e.preventDefault();
      const email = $("auth-email").value.trim().toLowerCase();
      const age = Number($("auth-age").value);
      if (!age || age < 18) { $("auth-error").textContent = "כניסה והרשמה מותרים מגיל 18 ומעלה בלבד."; $("auth-error").classList.remove("hidden"); return; }
      $("auth-error").classList.add("hidden");
      const uid = "u_" + email.replace(/[^a-z0-9]/g, "_");
      const av = `https://api.dicebear.com/9.x/avataaars/svg?seed=${encodeURIComponent(uid)}`;
      const session = { uid, email, name: email.split("@")[0] || "משתמש", gender: "", age, location: "", smoking: "", alcohol: "", education: "", tagline: "", banner: "bg-aurora", nameStyle: "name-rainbow", rewardPref: "❌ זהב", bio: "", likes: [], hobbies: [], photos: [av], following: [], avatar: av, profileCompleted: false, points: 0, wins: 0, losses: 0 };
      localStorage.setItem("toplove_session", JSON.stringify(session));
      try { await setDoc(doc(db, "users", uid), { ...session, updatedAt: serverTimestamp() }, { merge: true }); } catch {}
      openApp(session);
    };

    $("logout-btn").onclick = () => { localStorage.removeItem("toplove_session"); location.reload(); };
    document.querySelectorAll(".tab-btn").forEach((btn) => { btn.onclick = () => switchTab(btn.dataset.tab); });

    $("prof-avatar-file").onchange = (e) => {
      Array.from(e.target.files || []).forEach((f) => {
        const rd = new FileReader();
        rd.onload = () => { me.photos.push(String(rd.result)); me.avatar = me.photos[0]; renderPhotoThumbs(); };
        rd.readAsDataURL(f);
      });
    };
    $("prof-avatar-url").onchange = (e) => {
      const u = e.target.value.trim();
      if (!u) return;
      me.photos = [...(me.photos || []), u]; me.avatar = me.photos[0]; e.target.value = ""; renderPhotoThumbs();
    };
    $("prof-banner").onchange = (e) => { me.banner = e.target.value; renderPhotoThumbs(); };
    $("prof-name-style").onchange = (e) => { me.nameStyle = e.target.value; };

    $("profile-form").onsubmit = async (e) => {
      e.preventDefault();
      const ageVal = $("prof-age").value ? Number($("prof-age").value) : 18;
      if (ageVal < 18) { $("profile-error").textContent = "גיל מינימלי הוא 18."; $("profile-error").classList.remove("hidden"); return; }
      $("profile-error").classList.add("hidden");
      Object.assign(me, {
        name: $("prof-name").value.trim() || me.name || "משתמש", gender: $("prof-gender").value, age: ageVal,
        location: $("prof-location").value.trim(), smoking: $("prof-smoking").value, alcohol: $("prof-alcohol").value,
        education: $("prof-education").value.trim(), tagline: $("prof-tagline").value.trim(), banner: $("prof-banner").value,
        nameStyle: $("prof-name-style").value, bio: $("prof-bio").value.trim(), avatar: (me.photos && me.photos[0]) || me.avatar,
        profileCompleted: true
      });
      localStorage.setItem("toplove_session", JSON.stringify(me));
      $("user-badge").textContent = `${me.name} • ${me.age}`;
      try { await setDoc(doc(db, "users", me.uid), { ...me, updatedAt: serverTimestamp() }, { merge: true }); } catch {}
      applyProfileViewMode();
      $("save-feedback").classList.remove("opacity-0");
      setTimeout(() => $("save-feedback").classList.add("opacity-0"), 1500);
    };let allUsers = [];
    function renderRealUsers() {
      $("following-count-badge").textContent = `עוקב אחרי ${(me.following || []).length} משתמשים`;
      $("real-users-grid").innerHTML = allUsers.length
        ? allUsers.map((u) => {
            const lvl = getLevel(u.points || 0);
            const isF = (me.following || []).includes(u.id);
            return `<div class="bg-slate-900/85 border border-slate-700 rounded-2xl overflow-hidden flex flex-col justify-between">
              <div>
                <div class="h-14 ${u.banner || "bg-aurora"}"></div>
                <div class="p-4 -mt-7 space-y-2">
                  <div class="flex items-end gap-3">
                    <img src="${u.avatar || "https://api.dicebear.com/9.x/avataaars/svg?seed=" + u.id}" alt="" data-open-user="${u.id}"
                      class="w-14 h-14 rounded-xl object-cover border-2 border-slate-900 bg-slate-800 cursor-pointer shrink-0" />
                    <div>
                      <div data-open-user="${u.id}" class="font-bold text-sm cursor-pointer hover:underline ${u.nameStyle || ""}">${u.name || "משתמש"}</div>
                      <div class="text-[11px] text-amber-300">${getLevelSticker(lvl)}</div>
                    </div>
                  </div>
                  <p class="text-xs text-slate-300">${u.tagline || u.bio || u.location || ""}</p>
                </div>
              </div>
              <div class="px-4 pb-4 flex gap-2">
                <button type="button" data-follow-user="${u.id}" class="flex-1 py-1.5 rounded-lg text-xs font-semibold bg-indigo-600">${isF ? "✓ עוקב" : "➕ עקוב"}</button>
                <button type="button" data-dm-user="${u.id}" class="flex-1 py-1.5 rounded-lg text-xs font-semibold bg-pink-600">הודעה אישית</button>
              </div>
            </div>`;
          }).join("")
        : `<p class="text-xs text-slate-400 col-span-full">אין כרגע משתמשים אחרים רשומים.</p>`;

      document.querySelectorAll("[data-open-user]").forEach((el) => { el.onclick = () => { const f = allUsers.find((x) => x.id === el.dataset.openUser); if (f) openUserModal(f); }; });
      document.querySelectorAll("[data-follow-user]").forEach((btn) => {
        btn.onclick = () => {
          const id = btn.dataset.followUser;
          me.following = me.following || [];
          me.following = me.following.includes(id) ? me.following.filter((x) => x !== id) : [...me.following, id];
          renderStats(); renderRealUsers();
        };
      });
      document.querySelectorAll("[data-dm-user]").forEach((btn) => {
        btn.onclick = () => {
          const other = allUsers.find((x) => x.id === btn.dataset.dmUser);
          if (!other) return;
          const dmId = "dm_" + [me.uid, other.id].sort().join("_");
          if (!chatRooms.some((r) => r.id === dmId)) chatRooms.unshift({ id: dmId, topic: `שיחה אישית עם ${other.name || "משתמש"}`, members: [me.uid, other.id] });
          activeRoomId = dmId; joinedRoomId = dmId; switchTab("chat"); renderRooms();
        };
      });
    }

    function subscribeUsers() {
      onSnapshot(collection(db, "users"), (snap) => {
        allUsers = snap.docs.map((d) => ({ id: d.id, ...d.data() })).filter((u) => u.id !== me.uid);
        renderRealUsers();
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
    let activeRoomId = chatRooms[0].id, joinedRoomId = null, unsubMsgs = null;

    function listenMsgs(roomId) {
      if (unsubMsgs) { unsubMsgs(); unsubMsgs = null; }
      const q = query(collection(db, "rooms", roomId, "messages"), orderBy("createdAt", "asc"));
      unsubMsgs = onSnapshot(q, (snap) => {
        const msgs = snap.docs.map((d) => d.data());
        $("chat-messages").innerHTML = msgs.length
          ? msgs.map((m) => {
              const sObj = allUsers.find((u) => u.uid === m.senderUid) || (m.senderUid === me.uid ? me : {});
              const av = m.avatar || sObj.avatar || "https://api.dicebear.com/9.x/avataaars/svg?seed=TopLove";
              const lvl = getLevel(m.points ?? sObj.points ?? 0);
              const body = m.audioData ? `<audio controls src="${m.audioData}" class="w-full max-w-xs h-8 mt-1"></audio>` : `<div class="text-sm mt-0.5">${m.text || ""}</div>`;
              return `<div class="bg-slate-800/90 px-3 py-2 rounded-xl flex items-start gap-2.5">
                <img src="${av}" alt="" data-msg-user="${m.senderUid || ""}" class="w-9 h-9 rounded-full object-cover border border-pink-400 cursor-pointer shrink-0" />
                <div class="flex-1 min-w-0">
                  <div class="flex flex-wrap items-center gap-1.5">
                    <button type="button" data-msg-user="${m.senderUid || ""}" class="text-xs font-bold text-pink-300 hover:underline">${m.from || "משתמש"}</button>
                    <span class="text-[10px] px-2 py-0.5 rounded-full bg-slate-900 text-amber-300">רמה ${lvl}</span>
                  </div>
                  ${body}
                </div>
              </div>`;
            }).join("")
          : `<p class="text-xs text-slate-400">אין עדיין הודעות בחדר הזה.</p>`;
        document.querySelectorAll("[data-msg-user]").forEach((el) => {
          el.onclick = () => {
            const uid = el.dataset.msgUser;
            if (!uid) return;
            if (uid === me.uid) openUserModal(me);
            else { const f = allUsers.find((x) => (x.uid || x.id) === uid); if (f) openUserModal(f); }
          };
        });
      });
    }

    function renderRooms() {
      $("rooms-list").innerHTML = chatRooms.map((r) => {
        const count = (r.members || []).length;
        const isJoined = joinedRoomId === r.id;
        return `<div class="p-3 rounded-xl border text-xs flex items-center justify-between gap-2 ${isJoined ? "bg-pink-600/25 border-pink-400" : "bg-slate-950/75 border-slate-800"}">
          <div class="min-w-0">
            <div class="font-bold truncate">💬 ${r.topic}</div>
            <div class="text-[11px] text-slate-400">${count}/${MAX_ROOM_USERS} משתתפים</div>
          </div>
          <button type="button" data-enter-room="${r.id}" class="px-3 py-1.5 rounded-lg text-xs font-bold shrink-0 ${isJoined ? "bg-emerald-600" : "bg-pink-600 hover:bg-pink-500"}">
            ${isJoined ? "בתוך החדר" : "כנס לחדר"}
          </button>
        </div>`;
      }).join("");

      document.querySelectorAll("[data-enter-room]").forEach((btn) => {
        btn.onclick = () => {
          const target = chatRooms.find((r) => r.id === btn.dataset.enterRoom);
          if (!target) return;
          target.members = target.members || [];
          if (!target.members.includes(me.uid)) {
            if (target.members.length >= MAX_ROOM_USERS) { alert(`החדר מלא (מקסימום ${MAX_ROOM_USERS} משתתפים).`); return; }
            target.members.push(me.uid);
          }
          activeRoomId = target.id; joinedRoomId = target.id; renderRooms();
        };
      });

      const cur = chatRooms.find((r) => r.id === activeRoomId) || chatRooms[0];
      const isHere = joinedRoomId === cur.id;
      $("active-room-title").textContent = cur.topic;
      $("active-room-meta").textContent = isHere ? "מחובר לחדר • לחץ על תמונה/שם לפרופיל" : 'לחץ על "כנס לחדר" כדי להצטרף לחדר';
      $("room-capacity-badge").textContent = `${(cur.members || []).length} / ${MAX_ROOM_USERS} משתתפים`;
      listenMsgs(cur.id);
    }

    $("create-room-form").onsubmit = async (e) => {
      e.preventDefault();
      const topic = $("new-room-topic").value.trim();
      if (!topic) return;
      const room = { id: `r-${Date.now()}`, topic, members: [me.uid] };
      chatRooms.unshift(room); activeRoomId = room.id; joinedRoomId = room.id; $("new-room-topic").value = "";
      try { await setDoc(doc(db, "rooms", room.id), { id: room.id, topic: room.topic, createdAt: serverTimestamp() }, { merge: true }); } catch {}
      renderRooms();
    };

    $("chat-form").onsubmit = async (e) => {
      e.preventDefault();
      if (joinedRoomId !== activeRoomId) { alert('לחץ קודם על "כנס לחדר".'); return; }
      const txt = $("chat-input").value.trim();
      if (!txt) return;
      $("chat-input").value = "";
      await addDoc(collection(db, "rooms", activeRoomId, "messages"), { senderUid: me.uid, from: me.name || "משתמש", avatar: me.avatar, points: me.points || 0, text: txt, createdAt: serverTimestamp() });
    };

    let mediaRecorder = null, audioChunks = [];
    $("record-voice-btn").onclick = async () => {
      if (joinedRoomId !== activeRoomId) { alert('לחץ קודם על "כנס לחדר".'); return; }
      if (mediaRecorder && mediaRecorder.state === "recording") {
        mediaRecorder.stop(); $("record-voice-btn").textContent = "🎤 התחל הקלטה";
        $("record-voice-btn").classList.replace("bg-rose-600", "bg-amber-600"); $("voice-status").textContent = "שולח הקלטה..."; return;
      }
      if (!navigator.mediaDevices?.getUserMedia) { $("voice-status").textContent = "הדפדפן לא תומך בהקלטה קולית."; return; }
      try {
        const stream = await navigator.mediaDevices.getUserMedia({ audio: true });
        audioChunks = []; mediaRecorder = new MediaRecorder(stream);
        mediaRecorder.ondataavailable = (ev) => { if (ev.data.size > 0) audioChunks.push(ev.data); };
        mediaRecorder.onstop = async () => {
          stream.getTracks().forEach((t) => t.stop());
          const rd = new FileReader();
          rd.onloadend = async () => {
            await addDoc(collection(db, "rooms", activeRoomId, "messages"), { senderUid: me.uid, from: me.name || "משתמש", avatar: me.avatar, points: me.points || 0, audioData: String(rd.result), createdAt: serverTimestamp() });
            $("voice-status").textContent = "ההקלטה נשלחה לחדר!";
          };
          rd.readAsDataURL(new Blob(audioChunks, { type: "audio/webm" }));
        };
        mediaRecorder.start(); $("record-voice-btn").textContent = "⏹️ עצור ושלח הקלטה";
        $("record-voice-btn").classList.replace("bg-amber-600", "bg-rose-600"); $("voice-status").textContent = "מקליט כעת...";
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
        if (rem <= 0) { clearInterval(timerIntervals[key]); if ($(elId)) $(elId).textContent = "⏱️ 00:00"; if (onExpire) onExpire(); }
        else paint();
      }, 1000);
    }

    document.querySelectorAll(".game-tab-btn").forEach((btn) => {
      btn.onclick = () => {
        const g = btn.dataset.game;
        document.querySelectorAll(".game-tab-btn").forEach((b) => { b.className = b.dataset.game === g ? "game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold bg-pink-600" : "game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold glass text-slate-300"; });
        document.querySelectorAll(".game-panel").forEach((p) => p.classList.add("hidden"));
        $(`game-${g}`).classList.remove("hidden");
        if (g === "ttt") startCountdown("ttt", 30, "ttt-timer");
        if (g === "rps") startCountdown("rps", 15, "rps-timer");
        if (g === "memory") startCountdown("memory", 120, "memory-timer");
      };
    });

    const tttRooms = Array.from({ length: 100 }, (_, i) => ({ id: `ttt-room-${i + 1}`, num: i + 1, p1: null, p2: null, board: Array(9).fill(""), turn: "X", scored: false }));
    let activeTttRoomId = null;

    function renderTttRooms() {
      $("ttt-rooms-grid").innerHTML = tttRooms.map((r) => {
        const isSel = r.id === activeTttRoomId, count = (r.p1 ? 1 : 0) + (r.p2 ? 1 : 0);
        const label = count === 0 ? "חדר ריק" : count === 1 ? "ממתין לשחקן 2" : "2/2 פעיל";
        return `<button type="button" data-ttt-room="${r.id}" class="text-right p-2 rounded-xl border text-[11px] transition ${isSel ? "bg-pink-600/35 border-pink-400" : count === 0 ? "bg-slate-900/75 border-slate-700 hover:border-emerald-400" : "bg-slate-900/95 border-amber-500/40"}"><div class="font-bold">חדר #${r.num}</div><div class="text-slate-300 truncate">${label}</div></button>`;
      }).join("");
      document.querySelectorAll("[data-ttt-room]").forEach((b) => {
        b.onclick = () => {
          const r = tttRooms.find((x) => x.id === b.dataset.tttRoom); if (!r) return;
          const myLabel = me.name || "שחקן";
          if (r.p1 !== myLabel && r.p2 !== myLabel) { if (!r.p1) r.p1 = myLabel; else if (!r.p2) r.p2 = myLabel; else { alert("החדר מלא (2/2 שחקנים)."); return; } }
          activeTttRoomId = r.id; $("ttt-leave-room").classList.remove("hidden"); startCountdown("ttt", 30, "ttt-timer"); renderTttRooms(); renderTttBoard();
        };
      });
    }

    $("ttt-add-room").onclick = () => { const n = tttRooms.length + 1; tttRooms.push({ id: `ttt-room-${n}`, num: n, p1: null, p2: null, board: Array(9).fill(""), turn: "X", scored: false }); renderTttRooms(); };
    $("ttt-leave-room").onclick = () => {
      const r = tttRooms.find((x) => x.id === activeTttRoomId), myLabel = me.name || "שחקן";
      if (r) { if (r.p1 === myLabel) r.p1 = null; if (r.p2 === myLabel) r.p2 = null; }
      activeTttRoomId = null; $("ttt-leave-room").classList.add("hidden"); renderTttRooms(); renderTttBoard();
    };

    function checkTttWin(b) {
      const lines = [[0,1,2],[3,4,5],[6,7,8],[0,3,6],[1,4,7],[2,5,8],[0,4,8],[2,4,6]];
      for (const [a, c, d] of lines) if (b[a] && b[a] === b[c] && b[a] === b[d]) return b[a];
      return b.every(Boolean) ? "DRAW" : null;
    }

    function renderTttBoard() {
      const r = tttRooms.find((x) => x.id === activeTttRoomId), board = r ? r.board : Array(9).fill("");
      $("ttt-p1-name").textContent = r?.p1 || "מושב 1 ריק"; $("ttt-p2-name").textContent = r?.p2 || "ממתין לכניסה...";
      const el = $("ttt-board"); el.innerHTML = "";
      const win = checkTttWin(board), canMove = Boolean(r && r.p1 && r.p2 && !win);
      board.forEach((cell, idx) => {
        const btn = document.createElement("button"); btn.type = "button"; btn.disabled = !canMove || Boolean(cell);
        btn.className = "aspect-square rounded-lg bg-amber-900/90 border border-amber-500/40 text-lg font-bold flex items-center justify-center disabled:opacity-60";
        btn.textContent = cell === "X" ? "❌" : cell === "O" ? "⭕" : "";
        btn.onclick = async () => {
          if (!canMove || board[idx]) return;
          board[idx] = r.turn;
          const res = checkTttWin(board);
          if (res && !r.scored) {
            r.scored = true; const myLabel = me.name || "שחקן";
            if ((res === "X" && r.p1 === myLabel) || (res === "O" && r.p2 === myLabel)) await awardWin(25, "ttt");
            else if (res === "X" || res === "O") await awardLoss(5);
          }
          r.turn = r.turn === "X" ? "O" : "X"; startCountdown("ttt", 30, "ttt-timer"); renderTttBoard(); renderTttRooms();
        };
        el.appendChild(btn);
      });
      if (!r) $("ttt-status").textContent = "לחץ על אחד מחדרי איקס עיגול כדי להיכנס";
      else if (!r.p1 || !r.p2) $("ttt-status").textContent = `חדר #${r.num} — ממתין לשחקן נוסף שיצטרף מולך`;
      else if (win === "DRAW") $("ttt-status").textContent = `תיקו בחדר #${r.num}!`;
      else if (win) $("ttt-status").textContent = `המנצח בחדר #${r.num}: ${win === "X" ? r.p1 : r.p2} 🎉`;
      else $("ttt-status").textContent = `חדר #${r.num} • תור ${r.turn === "X" ? r.p1 + " (❌)" : r.p2 + " (⭕)"}`;
    }

    $("ttt-reset").onclick = () => { const r = tttRooms.find((x) => x.id === activeTttRoomId); if (!r) return; r.board = Array(9).fill(""); r.turn = "X"; r.scored = false; startCountdown("ttt", 30, "ttt-timer"); renderTttBoard(); };
    renderTttRooms(); renderTttBoard();

    const rpsRooms = Array.from({ length: 100 }, (_, i) => ({ id: `rps-room-${i + 1}`, num: i + 1, p1: null, p2: null }));
    let activeRpsRoomId = null, rpsBusy = false;

    function renderRpsRooms() {
      $("rps-rooms-grid").innerHTML = rpsRooms.map((r) => {
        const isSel = r.id === activeRpsRoomId, count = (r.p1 ? 1 : 0) + (r.p2 ? 1 : 0);
        const label = count === 0 ? "חדר ריק" : count === 1 ? "ממתין לשחקן 2" : "2/2 פעיל";
        return `<button type="button" data-rps-room="${r.id}" class="text-right p-2 rounded-xl border text-[11px] transition ${isSel ? "bg-pink-600/35 border-pink-400" : count === 0 ? "bg-slate-900/75 border-slate-700 hover:border-emerald-400" : "bg-slate-900/95 border-amber-500/40"}"><div class="font-bold">חדר #${r.num}</div><div class="text-slate-300 truncate">${label}</div></button>`;
      }).join("");
      document.querySelectorAll("[data-rps-room]").forEach((b) => {
        b.onclick = () => {
          const r = rpsRooms.find((x) => x.id === b.dataset.rpsRoom); if (!r) return;
          const myLabel = me.name || "שחקן";
          if (r.p1 !== myLabel && r.p2 !== myLabel) { if (!r.p1) r.p1 = myLabel; else if (!r.p2) r.p2 = myLabel; else { alert("החדר מלא (2/2 שחקנים)."); return; } }
          activeRpsRoomId = r.id; $("rps-leave-room").classList.remove("hidden"); startCountdown("rps", 15, "rps-timer"); renderRpsRooms(); syncRpsRoomUI();
        };
      });
    }

    $("rps-add-room").onclick = () => { const n = rpsRooms.length + 1; rpsRooms.push({ id: `rps-room-${n}`, num: n, p1: null, p2: null }); renderRpsRooms(); };
    $("rps-leave-room").onclick = () => {
      const r = rpsRooms.find((x) => x.id === activeRpsRoomId), myLabel = me.name || "שחקן";
      if (r) { if (r.p1 === myLabel) r.p1 = null; if (r.p2 === myLabel) r.p2 = null; }
      activeRpsRoomId = null; $("rps-leave-room").classList.add("hidden"); renderRpsRooms(); syncRpsRoomUI();
    };

    function syncRpsRoomUI() {
      const r = rpsRooms.find((x) => x.id === activeRpsRoomId);
      $("rps-left-name").textContent = r?.p1 || "מושב 1 פנוי"; $("rps-right-name").textContent = r?.p2 || "מושב 2 פנוי";
      $("rps-left-avatar").textContent = r?.p1 ? "🧑" : "🪑"; $("rps-right-avatar").textContent = r?.p2 ? "🧑" : "🪑";
      const ready = Boolean(r && r.p1 && r.p2);
      document.querySelectorAll(".rps-choice").forEach((b) => { b.disabled = !ready || rpsBusy; b.classList.toggle("opacity-50", !ready || rpsBusy); });
      if (!r) $("rps-round-phase").textContent = "בחר חדר כדי להיכנס";
      else if (!ready) $("rps-round-phase").textContent = `חדר #${r.num} — ממתין לשחקן נוסף שיצטרף מולך`;
      else $("rps-round-phase").textContent = `חדר #${r.num} מוכן!`;
    }

    document.querySelectorAll(".rps-choice").forEach((btn) => {
      btn.onclick = async () => {
        const r = rpsRooms.find((x) => x.id === activeRpsRoomId); if (!r || !r.p1 || !r.p2 || rpsBusy) return;
        rpsBusy = true; syncRpsRoomUI(); startCountdown("rps", 15, "rps-timer");
        const opts = ["rock", "paper", "scissors"], labels = { rock: "🪨 אבן", paper: "📄 נייר", scissors: "✂️ מספריים" }, signs = { rock: "🪨", paper: "📄", scissors: "✂️" };
        const p1Choice = btn.dataset.rps, p2Choice = opts[Math.floor(Math.random() * 3)];
        $("rps-left-sign").textContent = "✊"; $("rps-right-sign").textContent = "✊";
        const seq = ["1", "2", "3!"]; let i = 0; $("rps-count-num").textContent = seq[0]; $("rps-round-phase").textContent = "סופרים עד 3...";
        const iv = setInterval(async () => {
          i += 1;
          if (i < seq.length) $("rps-count-num").textContent = seq[i];
          else {
            clearInterval(iv); $("rps-left-sign").textContent = signs[p1Choice]; $("rps-right-sign").textContent = signs[p2Choice]; $("rps-round-phase").textContent = "חשיפה!";
            let msg = "תיקו!";
            if ((p1Choice === "rock" && p2Choice === "scissors") || (p1Choice === "paper" && p2Choice === "rock") || (p1Choice === "scissors" && p2Choice === "paper")) {
              msg = `${r.p1} ניצח/ה! 🎉`; if (r.p1 === (me.name || "שחקן")) await awardWin(20, "rps");
            } else if (p1Choice !== p2Choice) {
              msg = `${r.p2} ניצח/ה! 🎉`; if (r.p1 === (me.name || "שחקן")) await awardLoss(5);
            }
            $("rps-result").textContent = `${labels[p1Choice]} מול ${labels[p2Choice]} — ${msg}`;
            rpsBusy = false; syncRpsRoomUI();
          }
        }, 420);
      };
    });
    renderRpsRooms(); syncRpsRoomUI();const memRooms = [
      { id: "mr-1", title: "חדר קל #1", mode: "easy", players: [], turnIdx: 0 },
      { id: "mr-2", title: "חדר קל #2", mode: "easy", players: [], turnIdx: 0 },
      { id: "mr-3", title: "חדר בינוני #3", mode: "medium", players: [], turnIdx: 0 },
      { id: "mr-4", title: "חדר קשה #4", mode: "hard", players: [], turnIdx: 0 },
      { id: "mr-5", title: "חדר קשה #5", mode: "hard", players: [], turnIdx: 0 },
      { id: "mr-6", title: "חדר מומחים #6", mode: "hard", players: [], turnIdx: 0 }
    ];
    let activeMemRoomId = null, currentMemMode = "hard";
    const easyEmojis = ["🐶","🐱","🍕","🚗","⚽","🎸","☀️","🌈"];
    const mediumEmojis = ["💜","🔥","⭐","🌹","💎","⚡","🎯","🍀","🦄","🍩","🌙","🎲"];
    const hardEmojis = ["😀","😃","😄","😁","😆","😅","🙂","🙃","😉","😊","😇","🥰","😍","🤩","😘","😗","😚","😙"];
    let memCards = [], memFlipped = [], memMatched = new Set();

    function buildMemoryBoard(mode = "hard") {
      currentMemMode = mode;
      const pool = mode === "easy" ? easyEmojis : mode === "medium" ? mediumEmojis : hardEmojis;
      memCards = [...pool, ...pool].sort(() => Math.random() - 0.5);
      memFlipped = []; memMatched = new Set();
      $("memory-grid").className = mode === "easy" ? "grid grid-cols-4 gap-2 max-w-md mx-auto" : "grid grid-cols-6 gap-2 max-w-xl mx-auto";
      startCountdown("memory", mode === "easy" ? 90 : mode === "medium" ? 120 : 150, "memory-timer", () => { $("memory-status").textContent = "הזמן נגמר! לחץ 'ערבב לוח'."; });
      renderMemoryGrid();
    }

    function renderMemRooms() {
      const modeNames = { easy: "קל 4×4", medium: "בינוני 6×4", hard: "קשה 6×6" };
      $("memory-rooms-grid").innerHTML = memRooms.map((r) => `<button type="button" data-mem-room="${r.id}" class="text-right p-2.5 rounded-xl border text-xs transition ${r.id === activeMemRoomId ? "bg-pink-600/35 border-pink-400" : "bg-slate-900/80 border-slate-700 hover:border-emerald-400"}"><div class="font-bold truncate">💎 ${r.title}</div><div class="text-[11px] text-slate-300">${modeNames[r.mode] || "קשה"} • ${r.players.length}/6</div></button>`).join("");
      document.querySelectorAll("[data-mem-room]").forEach((b) => {
        b.onclick = () => {
          const r = memRooms.find((x) => x.id === b.dataset.memRoom); if (!r) return;
          const myLabel = me.name || "שחקן";
          if (!r.players.some((p) => p.name === myLabel)) { if (r.players.length >= 6) { alert("החדר מלא (מקסימום 6 שחקנים)."); return; } r.players.push({ name: myLabel, score: 0 }); }
          activeMemRoomId = r.id; $("memory-leave-room").classList.remove("hidden"); buildMemoryBoard(r.mode); renderMemRooms(); renderMemPlayersBoard();
        };
      });
    }

    $("mem-create-room-form").onsubmit = (e) => {
      e.preventDefault();
      const title = $("mem-room-name").value.trim(), mode = $("mem-room-mode").value; if (!title) return;
      const nr = { id: `mr-${Date.now()}`, title, mode, players: [{ name: me.name || "שחקן", score: 0 }], turnIdx: 0 };
      memRooms.unshift(nr); activeMemRoomId = nr.id; $("mem-room-name").value = ""; $("memory-leave-room").classList.remove("hidden");
      buildMemoryBoard(mode); renderMemRooms(); renderMemPlayersBoard();
    };

    $("memory-leave-room").onclick = () => {
      const r = memRooms.find((x) => x.id === activeMemRoomId), myLabel = me.name || "שחקן";
      if (r) r.players = r.players.filter((p) => p.name !== myLabel);
      activeMemRoomId = null; $("memory-leave-room").classList.add("hidden"); renderMemRooms(); renderMemPlayersBoard();
    };

    function renderMemPlayersBoard() {
      const r = memRooms.find((x) => x.id === activeMemRoomId);
      $("memory-players-board").innerHTML = Array.from({ length: 6 }, (_, idx) => {
        const p = r?.players[idx] || null, isTurn = r && r.players.length > 0 && (r.turnIdx % r.players.length) === idx && p;
        return `<div class="p-2 rounded-lg border ${isTurn ? "bg-pink-600/25 border-pink-400" : "bg-slate-900 border-slate-800"}"><div class="font-bold truncate">${p ? p.name : `מושב ${idx + 1} פנוי`}</div><div class="text-amber-300">${p ? `${p.score} נק׳` : "פנוי"}</div></div>`;
      }).join("");
    }

    function renderMemoryGrid() {
      const g = $("memory-grid"); g.innerHTML = "";
      memCards.forEach((sym, i) => {
        const show = memFlipped.includes(i) || memMatched.has(i), btn = document.createElement("button");
        btn.type = "button"; btn.className = "aspect-square rounded-xl bg-slate-900 border border-slate-700 text-xl flex items-center justify-center hover:border-pink-400";
        btn.textContent = show ? sym : "❓";
        btn.onclick = async () => {
          if (show || memFlipped.length === 2) return;
          memFlipped.push(i); renderMemoryGrid();
          if (memFlipped.length === 2) {
            const [a, b] = memFlipped, r = memRooms.find((x) => x.id === activeMemRoomId);
            if (memCards[a] === memCards[b]) {
              memMatched.add(a); memMatched.add(b); memFlipped = [];
              if (r && r.players.length) { const curP = r.players[r.turnIdx % r.players.length]; curP.score += 10; if (curP.name === (me.name || "שחקן")) await awardWin(10, "memory"); }
              if (memMatched.size === memCards.length) $("memory-status").textContent = "כל הזוגות נמצאו! 🎉";
              renderMemPlayersBoard(); renderMemoryGrid();
            } else setTimeout(() => { memFlipped = []; if (r && r.players.length) r.turnIdx = (r.turnIdx + 1) % r.players.length; renderMemPlayersBoard(); renderMemoryGrid(); }, 700);
          }
        };
        g.appendChild(btn);
      });
      if (activeMemRoomId) { const r = memRooms.find((x) => x.id === activeMemRoomId); $("memory-status").textContent = `${r.title} • ${r.players.length}/6 שחקנים • תור ${r.players[r.turnIdx % r.players.length]?.name || ""}`; }
    }

    $("memory-reset").onclick = () => buildMemoryBoard(currentMemMode);
    renderMemRooms(); renderMemPlayersBoard(); buildMemoryBoard("hard");

    let numRooms = [
      { id: "nr-1", name: "חדר ניחוש #1 (1–1,000)", maxNum: 1000, hostName: "מנהל החדר", secret: null, players: [], guesses: [] },
      { id: "nr-2", name: "חדר ניחוש #2 (1–1,000)", maxNum: 1000, hostName: "מנהל החדר", secret: null, players: [], guesses: [] },
      { id: "nr-3", name: "אתגר 1–1,500", maxNum: 1500, hostName: "מנהל החדר", secret: null, players: [], guesses: [] }
    ];
    let activeNumRoomId = numRooms[0].id;

    function renderNumRooms() {
      $("num-rooms-list").innerHTML = numRooms.map((r) => `<button type="button" data-num-room="${r.id}" class="text-right p-3 rounded-xl border text-xs ${r.id === activeNumRoomId ? "bg-pink-600/30 border-pink-400" : "bg-slate-900/80 border-slate-700"}"><div class="font-bold">🎯 ${r.name}</div><div class="text-slate-300 mt-0.5">1–${r.maxNum.toLocaleString()} • ${(r.players || []).length}/50</div></button>`).join("");
      document.querySelectorAll("[data-num-room]").forEach((b) => {
        b.onclick = () => {
          const r = numRooms.find((x) => x.id === b.dataset.numRoom); if (!r) return;
          r.players = r.players || []; const myLabel = me.name || "שחקן";
          if (!r.players.includes(myLabel)) { if (r.players.length >= 50) { alert("החדר מלא (מקסימום 50 משתתפים)."); return; } r.players.push(myLabel); }
          activeNumRoomId = r.id; renderNumRooms(); renderActiveNumRoom();
        };
      });
    }

    function renderActiveNumRoom() {
      const r = numRooms.find((x) => x.id === activeNumRoomId) || numRooms[0]; r.players = r.players || [];
      $("num-room-header").textContent = `${r.name} (1 עד ${r.maxNum.toLocaleString()})`; $("num-room-cap").textContent = `${r.players.length} / 50 משתתפים`;
      $("num-guess-input").min = 1; $("num-guess-input").max = r.maxNum; $("num-secret-input").value = r.secret !== null ? String(r.secret) : "";
      $("num-secret-status").textContent = r.secret !== null ? "✓ מספר סודי נקבע בשקט! המשתתפים יכולים לשלוח ניחושים." : "טרם נקבע מספר סודי — הזן מספר בשקט או לחץ 'קבע מספר סודי'.";
      $("num-guesses-log").innerHTML = r.guesses.map((g) => `<div class="px-3 py-1.5 rounded-lg bg-slate-900 border border-slate-800 flex justify-between"><span><strong>${g.player}</strong> ניחש <strong>${g.value}</strong></span><span class="text-indigo-200">מרחק: ${g.diff}</span></div>`).join("");
    }

    $("num-create-room-form").onsubmit = (e) => {
      e.preventDefault();
      const name = $("num-room-name").value.trim(), maxNum = Math.max(10, Number($("num-room-max").value) || 1000); if (!name) return;
      const myLabel = me.name || "שחקן", nr = { id: `nr-${Date.now()}`, name, maxNum, hostName: myLabel, secret: null, players: [myLabel], guesses: [] };
      numRooms.unshift(nr); activeNumRoomId = nr.id; $("num-room-name").value = ""; renderNumRooms(); renderActiveNumRoom();
    };

    $("num-toggle-secret").onclick = () => { $("num-secret-input").type = $("num-secret-input").type === "password" ? "number" : "password"; };
    $("num-set-secret-btn").onclick = () => {
      const r = numRooms.find((x) => x.id === activeNumRoomId) || numRooms[0], typed = Number($("num-secret-input").value);
      r.secret = (typed >= 1 && typed <= r.maxNum) ? typed : Math.floor(Math.random() * r.maxNum) + 1;
      r.guesses = []; $("num-guess-feedback").textContent = "מספר סודי נקבע בשקט! אפשר לשלוח ניחושים."; renderActiveNumRoom();
    };

    $("num-guess-btn").onclick = () => {
      const r = numRooms.find((x) => x.id === activeNumRoomId) || numRooms[0];
      if (r.secret === null) r.secret = Math.floor(Math.random() * r.maxNum) + 1;
      const val = Number($("num-guess-input").value);
      if (!val || val < 1 || val > r.maxNum) { $("num-guess-feedback").textContent = `הכנס מספר בין 1 ל-${r.maxNum.toLocaleString()}.`; return; }
      const myLabel = me.name || "שחקן";
      if (!r.players.includes(myLabel) && r.players.length < 50) r.players.push(myLabel);
      r.guesses.unshift({ player: myLabel, value: val, diff: Math.abs(val - r.secret) });
      $("num-guess-input").value = ""; $("num-guess-feedback").textContent = `הניחוש ${val} נרשם! לחץ "הכרז על הכי קרוב (+3 נק׳)".`;
      renderNumRooms(); renderActiveNumRoom();
    };

    $("num-declare-winner-btn").onclick = async () => {
      const r = numRooms.find((x) => x.id === activeNumRoomId) || numRooms[0];
      if (r.secret === null || !r.guesses.length) { $("num-guess-feedback").textContent = "יש לקבוע מספר סודי ולוודא שנשלחו ניחושים."; return; }
      const best = [...r.guesses].sort((a, b) => a.diff - b.diff)[0];
      $("num-guess-feedback").textContent = `🏆 הכי קרוב למספר הסודי (${r.secret}) הוא ${best.player} (ניחש ${best.value}, מרחק ${best.diff}) — זוכה ב-3 נקודות!`;
      if (best.player === (me.name || "שחקן")) await awardWin(3, "number");
    };

    renderNumRooms(); renderActiveNumRoom();

    const savedSession = localStorage.getItem("toplove_session");
    if (savedSession) { try { openApp(JSON.parse(savedSession)); } catch {} }
  </script>
</body>
</html>
