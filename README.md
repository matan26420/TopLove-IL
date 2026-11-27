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
      background: rgba(30, 41, 59, 0.86);
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
      text-shadow: 0 0 12px rgba(103, 232, 249, 0.7);
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
    <div class="flex items-center gap-2.5">
      <span class="text-2xl">💜</span>
      <h1 class="text-2xl font-extrabold bg-gradient-to-l from-pink-400 to-indigo-400 bg-clip-text text-transparent">TopLove IL</h1>
      <span class="text-xs bg-emerald-500/20 border border-emerald-400/40 text-emerald-200 px-3 py-1 rounded-full">
        חינם לגמרי • 18–80
      </span>
    </div>
    <div class="flex flex-wrap items-center gap-2.5">
      <span id="weekly-reset-badge" class="text-xs bg-indigo-500/20 border border-indigo-400/40 text-indigo-200 px-3 py-1 rounded-full">
        ⏳ איפוס שבועי אוטומטי: 7 ימים
      </span>
      <span id="user-badge" class="hidden text-sm text-slate-200 bg-slate-800 px-3 py-1 rounded-full"></span>
      <button id="logout-btn" type="button" class="hidden bg-rose-600 hover:bg-rose-500 text-sm px-4 py-1.5 rounded-lg">התנתק</button>
    </div>
  </header><div id="user-modal" class="hidden fixed inset-0 z-50 bg-black/75 backdrop-blur-sm flex items-center justify-center p-4">
    <div class="glass max-w-2xl w-full rounded-3xl overflow-hidden border border-pink-400/40 shadow-2xl max-h-[90vh] overflow-y-auto">
      <div id="modal-banner" class="h-32 bg-aurora relative p-4 flex justify-between items-start">
        <span id="modal-level-badge" class="text-xs font-extrabold px-3 py-1 rounded-full bg-slate-950/80 border border-white/25"></span>
        <button type="button" id="close-modal-btn" class="w-9 h-9 rounded-full bg-slate-950/85 text-white font-bold">✕</button>
      </div>
      <div class="p-6 -mt-14 space-y-4">
        <div class="flex flex-col sm:flex-row items-center sm:items-end gap-4">
          <img id="modal-main-photo" src="" alt="" class="w-28 h-28 rounded-2xl object-cover border-4 border-slate-900 bg-slate-800 shadow-xl shrink-0" />
          <div class="space-y-1 text-center sm:text-right flex-1">
            <h3 id="modal-name" class="text-2xl font-extrabold"></h3>
            <p id="modal-tagline" class="text-xs text-pink-200"></p>
            <div class="flex justify-center sm:justify-start gap-2 pt-1">
              <button type="button" id="modal-prev-photo" class="px-3 py-1 rounded-lg text-xs bg-slate-800 hover:bg-slate-700 border border-slate-600">◀ תמונה קודמת</button>
              <button type="button" id="modal-next-photo" class="px-3 py-1 rounded-lg text-xs bg-slate-800 hover:bg-slate-700 border border-slate-600">תמונה הבאה ▶</button>
            </div>
          </div>
        </div>

        <div id="modal-gallery" class="flex gap-2 overflow-x-auto pb-1"></div>

        <div class="text-xs text-slate-200 bg-slate-900/85 p-3.5 rounded-xl border border-slate-800 space-y-1">
          <div id="modal-meta"></div>
          <div id="modal-habits"></div>
          <div id="modal-pets-info" class="text-amber-200"></div>
          <div id="modal-education"></div>
          <div id="modal-bio" class="text-slate-300 pt-1"></div>
        </div>

        <div class="space-y-1.5">
          <div class="text-xs font-bold text-pink-300">🎯 תחביבים ותחומי עניין:</div>
          <div id="modal-tags" class="flex flex-wrap gap-1.5 text-xs"></div>
        </div>

        <div class="grid grid-cols-2 sm:grid-cols-4 gap-2 pt-2">
          <button type="button" id="modal-like-btn" class="py-2.5 rounded-xl text-xs font-bold bg-amber-600 hover:bg-amber-500">👍 לייק</button>
          <button type="button" id="modal-heart-btn" class="py-2.5 rounded-xl text-xs font-bold bg-rose-600 hover:bg-rose-500">💖 לב</button>
          <button type="button" id="modal-follow-btn" class="py-2.5 rounded-xl text-xs font-bold bg-indigo-600 hover:bg-indigo-500">➕ עקוב</button>
          <button type="button" id="modal-dm-btn" class="py-2.5 rounded-xl text-xs font-bold bg-pink-600 hover:bg-pink-500">✉️ הודעה אישית</button>
        </div>
        <p id="modal-action-msg" class="text-xs text-emerald-300 font-semibold"></p>
      </div>
    </div>
  </div><main class="max-w-7xl mx-auto px-4 sm:px-6 py-7 space-y-6">
    <section id="auth-section" class="max-w-md mx-auto glass rounded-2xl p-8 shadow-2xl mt-6">
      <h2 class="text-2xl font-bold text-center mb-2">ברוכים הבאים ל-TopLove IL</h2>
      <p class="text-slate-300 text-sm text-center mb-6">כניסה והרשמה חינם לגילאי 18 עד 80</p>
      <form id="auth-form" class="space-y-4">
        <input type="email" id="auth-email" required placeholder="אימייל" dir="ltr"
          class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700 text-left" />
        <input type="number" id="auth-age" required min="18" max="80" placeholder="גיל (18–80)"
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
      <div class="flex flex-wrap gap-2.5 justify-center">
        <button type="button" data-tab="profile" class="tab-btn px-5 py-2.5 rounded-xl text-sm font-semibold bg-pink-600 text-white">1. הפרופיל שלי</button>
        <button type="button" data-tab="users" class="tab-btn px-5 py-2.5 rounded-xl text-sm font-semibold glass text-slate-300">2. משתמשים, מרחק וגיל 👥</button>
        <button type="button" data-tab="chat" class="tab-btn px-5 py-2.5 rounded-xl text-sm font-semibold glass text-slate-300">3. חדרי שיחה 💬</button>
        <button type="button" data-tab="games" class="tab-btn px-5 py-2.5 rounded-xl text-sm font-semibold glass text-slate-300">4. משחקים, טופ-100 וטופ-5 🎮</button>
      </div><div id="tab-profile" class="tab-content max-w-6xl mx-auto glass rounded-3xl p-6 sm:p-8 shadow-2xl space-y-6">
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
          <div id="summary-banner" class="h-32 bg-aurora p-4 flex items-center justify-between">
            <span id="summary-level-badge" class="text-xs font-extrabold px-3.5 py-1 rounded-full bg-slate-950/80 border border-white/20"></span>
            <span id="summary-likes-badge" class="text-xs font-extrabold px-3.5 py-1 rounded-full bg-rose-500/25 border border-rose-300/40 text-rose-200"></span>
          </div>
          <div class="p-6 -mt-14 space-y-6">
            <div class="flex flex-col sm:flex-row items-center sm:items-end gap-5">
              <img id="summary-avatar" src="https://api.dicebear.com/9.x/avataaars/svg?seed=TopLove" alt=""
                class="w-36 h-36 rounded-2xl object-cover border-4 border-slate-900 bg-slate-800 shrink-0 shadow-lg cursor-pointer" />
              <div class="space-y-1.5 text-center sm:text-right flex-1">
                <h3 id="summary-name" class="text-2xl font-extrabold"></h3>
                <p id="summary-tagline" class="text-sm text-pink-200 font-medium"></p>
                <p id="summary-age-gender-loc" class="text-xs text-indigo-200"></p>
                <p id="summary-habits" class="text-xs text-emerald-200"></p>
                <p id="summary-pets" class="text-xs text-amber-200"></p>
                <p id="summary-bio" class="text-sm text-slate-300 pt-1"></p>
                <div class="flex justify-center sm:justify-start gap-2 pt-2">
                  <button type="button" id="summary-prev-photo" class="px-3 py-1 rounded-lg text-xs bg-slate-800 hover:bg-slate-700 border border-slate-600">◀ תמונה קודמת</button>
                  <button type="button" id="summary-next-photo" class="px-3 py-1 rounded-lg text-xs bg-slate-800 hover:bg-slate-700 border border-slate-600">תמונה הבאה ▶</button>
                </div>
              </div>
            </div>

            <div id="summary-photos-strip" class="flex gap-2.5 overflow-x-auto pb-1"></div>

            <div class="grid grid-cols-1 md:grid-cols-2 gap-4 pt-2 border-t border-white/10">
              <div class="bg-slate-950/70 rounded-xl p-4 border border-slate-800 space-y-2">
                <div class="text-xs font-bold text-indigo-300">🎯 תחביבים ותחומי עניין</div>
                <div id="summary-hobbies" class="flex flex-wrap gap-1.5 text-xs"></div>
              </div>
              <div class="bg-slate-950/70 rounded-xl p-4 border border-slate-800 space-y-2">
                <div class="text-xs font-bold text-emerald-300">🐾 בעלי חיים והשכלה</div>
                <div id="summary-education" class="text-xs text-slate-200"></div>
              </div>
            </div>
          </div>
        </div><form id="profile-form" class="space-y-6">
          <div class="bg-slate-900/75 p-5 rounded-2xl border border-slate-700 space-y-4">
            <div class="flex flex-col md:flex-row items-center gap-6">
              <div id="prof-avatar-frame" class="p-2 rounded-3xl bg-aurora shadow-lg shrink-0">
                <img id="prof-avatar-preview" src="https://api.dicebear.com/9.x/avataaars/svg?seed=TopLove" alt=""
                  class="w-28 h-28 rounded-2xl object-cover bg-slate-800" />
              </div>
              <div class="w-full space-y-3">
                <label class="block text-sm font-semibold text-pink-300">בחירת תמונות מהמכשיר (מחליף את תמונת ברירת המחדל)</label>
                <input type="file" id="prof-avatar-file" accept="image/*" multiple
                  class="block w-full text-xs text-slate-300 file:ml-3 file:py-2.5 file:px-5 file:rounded-xl file:border-0 file:bg-pink-600 hover:file:bg-pink-500 file:text-white file:font-bold cursor-pointer" />
                <div id="prof-photos-thumbs" class="flex flex-wrap gap-2"></div>
              </div>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 gap-4 pt-3 border-t border-white/10">
              <div>
                <label class="block text-xs text-slate-300 mb-1.5">רקע מעניין לפרופיל</label>
                <select id="prof-banner" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-950 border border-slate-700 text-xs">
                  <option value="bg-aurora">זוהר צפוני (ורוד-סגול-טורקיז)</option>
                  <option value="bg-sunset">שקיעה חמה (כתום-ורוד-סגול)</option>
                  <option value="bg-royal">מלכותי (אינדיגו-סגול-מג׳נטה)</option>
                  <option value="bg-emeraldLux">יער יוקרתי (ירוק-טורקיז-כחול)</option>
                </select>
              </div>
              <div>
                <label class="block text-xs text-slate-300 mb-1.5">כתובית מעניינת ליד השם (לא חובה)</label>
                <input type="text" id="prof-tagline" placeholder="למשל: מחפשת אנרגיות טובות ✨"
                  class="w-full px-3.5 py-2.5 rounded-xl bg-slate-950 border border-slate-700 text-xs" />
              </div>
            </div>

            <div class="space-y-2 pt-2">
              <label class="block text-xs text-slate-300">סגנון שם וכתוביות (רואים ישר איך זה נראה לפני שלוחצים):</label>
              <div id="name-style-cards" class="grid grid-cols-2 sm:grid-cols-4 gap-2.5">
                <button type="button" data-style="name-rainbow" class="style-pick-btn p-3 rounded-xl bg-slate-950 border border-pink-400 text-center">
                  <div class="font-extrabold text-sm name-rainbow">צבעוני קשת</div>
                  <div class="text-[11px] text-slate-400 mt-0.5">קשת צבעונית חיה</div>
                </button>
                <button type="button" data-style="name-roseGold" class="style-pick-btn p-3 rounded-xl bg-slate-950 border border-slate-700 text-center">
                  <div class="font-extrabold text-sm name-roseGold">רוז-גולד זוהר</div>
                  <div class="text-[11px] text-slate-400 mt-0.5">ורוד-זהב יוקרתי</div>
                </button>
                <button type="button" data-style="name-neon" class="style-pick-btn p-3 rounded-xl bg-slate-950 border border-slate-700 text-center">
                  <div class="font-extrabold text-sm name-neon">ניאון טורקיז</div>
                  <div class="text-[11px] text-slate-400 mt-0.5">זוהר ניאון</div>
                </button>
                <button type="button" data-style="" class="style-pick-btn p-3 rounded-xl bg-slate-950 border border-slate-700 text-center">
                  <div class="font-extrabold text-sm text-white">רגיל ונקי</div>
                  <div class="text-[11px] text-slate-400 mt-0.5">לבן קלאסי</div>
                </button>
              </div>
            </div>
          </div><div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-5 gap-3.5">
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
              <label class="block text-xs text-slate-300 mb-1">גיל (18–80)</label>
              <input type="number" id="prof-age" min="18" max="80" placeholder="גיל"
                class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700 text-sm" />
            </div>
            <div>
              <label class="block text-xs text-slate-300 mb-1">מדינה / עיר</label>
              <input type="text" id="prof-location" placeholder="למשל: כרמיאל"
                class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700 text-sm" />
            </div>
            <div>
              <label class="block text-xs text-slate-300 mb-1">מרחק ממני (ק״מ)</label>
              <input type="number" id="prof-distance" min="0" max="600" value="15"
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

          <div class="bg-slate-900/75 p-4 rounded-2xl border border-slate-800 space-y-3">
            <div class="text-sm font-bold text-amber-300">🐾 בעלי חיים (אופציונלי)</div>
            <div class="grid grid-cols-1 sm:grid-cols-2 gap-3.5">
              <div>
                <label class="block text-xs text-slate-300 mb-1">האם יש לך בעלי חיים?</label>
                <select id="prof-has-pets" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-950 border border-slate-700 text-sm">
                  <option value="">לא צוין</option>
                  <option value="יש לי בעלי חיים">יש לי בעלי חיים</option>
                  <option value="אין לי בעלי חיים">אין לי בעלי חיים</option>
                  <option value="יש לי ואני אוהב/ת גם עוד">יש לי ואני אוהב/ת גם עוד</option>
                </select>
              </div>
              <div>
                <label class="block text-xs text-slate-300 mb-1">איזה בעל חיים אתה יותר אוהב?</label>
                <select id="prof-fav-pet" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-950 border border-slate-700 text-sm">
                  <option value="">לא צוין</option>
                  <option value="חתול">🐱 חתול</option>
                  <option value="כלב">🐶 כלב</option>
                  <option value="אחר">✨ אחר</option>
                </select>
              </div>
            </div>
            <div id="prof-other-pet-wrap" class="hidden">
              <label class="block text-xs text-amber-200 mb-1">איזה בעל חיים? (לא חובה)</label>
              <input type="text" id="prof-other-pet-text" placeholder="למשל: ארנב, תוכי, סוס, צב..."
                class="w-full px-3.5 py-2 rounded-xl bg-slate-950 border border-amber-500/40 text-sm" />
            </div>
          </div>

          <div class="bg-slate-900/70 p-4 rounded-2xl border border-slate-800 space-y-2.5">
            <label class="block text-sm font-bold text-indigo-300">🎯 תחביבים — סדרות, סרטים, טיולים, מוזיקה ועוד (לא חובה)</label>
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
      </div><div id="tab-users" class="tab-content hidden max-w-6xl mx-auto glass rounded-2xl p-6 space-y-5">
        <div class="flex flex-wrap items-center justify-between gap-2">
          <h2 class="text-2xl font-bold">👥 משתמשים, מרחק, גילאים והודעות אישיות</h2>
          <span id="following-count-badge" class="text-xs px-3 py-1 rounded-full bg-indigo-500/20 border border-indigo-400/40 text-indigo-200">
            עוקב אחרי 0 משתמשים
          </span>
        </div>

        <div class="bg-slate-900/80 border border-slate-700 rounded-2xl p-4 grid grid-cols-1 sm:grid-cols-3 gap-3 text-xs">
          <div>
            <label class="block text-slate-300 mb-1">מרחק ממני:</label>
            <select id="filter-distance" class="w-full px-3 py-2 rounded-xl bg-slate-950 border border-slate-700">
              <option value="all">כל הארץ</option>
              <option value="10">קרוב אליי — עד 10 ק״מ</option>
              <option value="20">עד 20 ק״מ</option>
              <option value="30">עד 30 ק״מ</option>
              <option value="100">עד 100 ק״מ</option>
              <option value="200">עד 200 ק״מ</option>
              <option value="350">עד 350 ק״מ</option>
              <option value="500">עד 500 ק״מ</option>
              <option value="600">עד 600 ק״מ</option>
            </select>
          </div>
          <div>
            <label class="block text-slate-300 mb-1">גיל מינימום (18–80):</label>
            <input type="number" id="filter-min-age" min="18" max="80" value="18"
              class="w-full px-3 py-2 rounded-xl bg-slate-950 border border-slate-700" />
          </div>
          <div>
            <label class="block text-slate-300 mb-1">גיל מקסימום (18–80):</label>
            <input type="number" id="filter-max-age" min="18" max="80" value="80"
              class="w-full px-3 py-2 rounded-xl bg-slate-950 border border-slate-700" />
          </div>
        </div>

        <div id="real-users-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4"></div>
      </div><div id="tab-chat" class="tab-content hidden max-w-6xl mx-auto glass rounded-2xl p-6 space-y-5">
        <div class="bg-slate-900/80 border border-slate-700 rounded-2xl p-4 space-y-3">
          <h3 class="text-sm font-bold text-pink-300">➕ פתיחת חדר שיחה חדש (חדר ציבורי או פרטי עם קוד לחברים בלבד)</h3>
          <form id="create-room-form" class="grid grid-cols-1 sm:grid-cols-3 gap-2.5">
            <input type="text" id="new-room-topic" required placeholder="שם / נושא החדר..."
              class="px-3.5 py-2 rounded-xl bg-slate-950 border border-slate-700 text-sm" />
            <input type="text" id="new-room-code" placeholder="קוד סודי לחדר פרטי (אופציונלי)"
              class="px-3.5 py-2 rounded-xl bg-slate-950 border border-slate-700 text-sm" />
            <button type="submit" class="px-5 py-2 rounded-xl text-sm font-semibold bg-gradient-to-l from-pink-600 to-indigo-600">
              פתח חדר שיחה
            </button>
          </form>
        </div>

        <div class="grid grid-cols-1 lg:grid-cols-3 gap-5">
          <div class="space-y-2">
            <h3 class="text-sm font-bold text-slate-200">🗂️ חדרי שיחה</h3>
            <div id="rooms-list" class="space-y-2 max-h-[440px] overflow-y-auto"></div>
          </div>

          <div class="lg:col-span-2 bg-slate-900/75 border border-slate-800 rounded-2xl p-4 flex flex-col justify-between min-h-[440px] space-y-3">
            <div class="border-b border-white/10 pb-3 flex flex-wrap items-center justify-between gap-2">
              <div>
                <h3 id="active-room-title" class="font-bold text-base">בחר חדר ולחץ "כנס לחדר"</h3>
                <p id="active-room-meta" class="text-xs text-slate-400">לא מחובר לחדר כרגע</p>
              </div>
              <div class="flex flex-wrap items-center gap-2">
                <button type="button" id="invite-friend-btn" class="px-3 py-1 rounded-lg text-xs font-semibold bg-indigo-600 hover:bg-indigo-500">
                  📨 הזמן חבר
                </button>
                <button type="button" id="leave-room-btn" class="hidden px-3 py-1 rounded-lg text-xs font-semibold bg-rose-600 hover:bg-rose-500">
                  צא מהחדר
                </button>
              </div>
            </div>

            <div id="chat-messages" class="space-y-2 max-h-64 overflow-y-auto py-1"></div>

            <div class="space-y-2 pt-2 border-t border-white/10">
              <div class="flex flex-wrap items-center justify-between gap-2">
                <button type="button" id="record-voice-btn" class="px-4 py-1.5 rounded-xl text-xs font-semibold bg-amber-600 hover:bg-amber-500">
                  🎤 התחל הקלטה
                </button>
                <span id="voice-status" class="text-xs text-slate-300">הודעות נשמרות בחדר ומתאפסות אוטומטית אחת לשבוע</span>
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
              <div class="text-xs text-slate-400">רמה אישית במשחק זה</div>
              <div id="stat-game-level" class="text-xl font-extrabold text-pink-300 mt-0.5">רמה 0</div>
              <div id="stat-game-name" class="text-[11px] text-indigo-200 mt-0.5">איקס עיגול</div>
            </div>
            <div class="bg-slate-900/85 rounded-xl p-3 border border-slate-700">
              <div class="text-xs text-slate-400">נקודות במשחק זה</div>
              <div id="stat-game-points" class="text-xl font-extrabold text-amber-300 mt-0.5">0</div>
            </div>
            <div class="bg-slate-900/85 rounded-xl p-3 border border-slate-700">
              <div class="text-xs text-slate-400">ניצחונות</div>
              <div id="stat-game-wins" class="text-xl font-extrabold text-emerald-300 mt-0.5">0</div>
            </div>
            <div class="bg-slate-900/85 rounded-xl p-3 border border-slate-700">
              <div class="text-xs text-slate-400">הפסדים</div>
              <div id="stat-game-losses" class="text-xl font-extrabold text-rose-300 mt-0.5">0</div>
            </div>
          </div>

          <div class="bg-slate-950/75 rounded-xl p-3.5 border border-amber-400/25 space-y-2">
            <div class="flex flex-wrap items-center justify-between gap-2">
              <div id="top5-title" class="text-xs font-extrabold text-amber-300">🏅 טופ-5 במשחק (מתוך רשימת הטופ-100 • נכנסים אחרי משחק אחד לפחות)</div>
              <span id="top100-count-badge" class="text-[11px] text-indigo-200">0 / 100 שחקנים מדורגים</span>
            </div>
            <div id="top5-board" class="grid grid-cols-1 sm:grid-cols-5 gap-2 text-xs"></div>
          </div>
        </div>

        <div class="flex flex-wrap gap-2 justify-center">
          <button type="button" data-game="ttt" class="game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold bg-pink-600">1. איקס עיגול (100+ חדרים)</button>
          <button type="button" data-game="rps" class="game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold glass text-slate-300">2. אבן נייר מספריים (100+ חדרים)</button>
          <button type="button" data-game="memory" class="game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold glass text-slate-300">3. זיכרון (8×8, 10×10, 30×30)</button>
          <button type="button" data-game="number" class="game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold glass text-slate-300">4. ניחוש מספר (עד 50 בחדר)</button>
          <button type="button" data-game="roulette" class="game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold glass text-slate-300">5. רולטה רוסית (6 מושבים)</button>
        </div>

        <div id="game-ttt" class="game-panel max-w-6xl mx-auto glass rounded-2xl p-6 space-y-5">
          <div class="flex flex-wrap items-center justify-between gap-2 border-b border-white/10 pb-3">
            <div>
              <h3 class="text-xl font-bold">❌⭕ איקס עיגול — 100 חדרים + יצירת חדרים</h3>
              <p class="text-xs text-slate-300">בחירת ❌ או ⭕ לשחקן הראשון • צ׳אט + הקלטות קוליות שמתאפסות כשכולם יוצאים</p>
            </div>
            <div class="flex flex-wrap items-center gap-2">
              <span id="ttt-timer" class="px-3 py-1 rounded-full text-xs font-bold bg-amber-500/20 border border-amber-400/40 text-amber-200">⏱️ 00:30</span>
              <button type="button" id="ttt-add-room" class="px-3.5 py-1.5 rounded-xl text-xs font-semibold bg-emerald-600 hover:bg-emerald-500">+ צור שולחן</button>
              <button type="button" id="ttt-join-room" class="px-3.5 py-1.5 rounded-xl text-xs font-semibold bg-pink-600 hover:bg-pink-500">כנס לשולחן</button>
              <button type="button" id="ttt-leave-room" class="hidden px-3.5 py-1.5 rounded-xl text-xs font-semibold bg-rose-600 hover:bg-rose-500">צא מהשולחן</button>
            </div>
          </div>

          <div id="ttt-rooms-grid" class="grid grid-cols-2 sm:grid-cols-4 md:grid-cols-5 gap-2 max-h-48 overflow-y-auto p-1"></div>

          <div class="grid grid-cols-1 lg:grid-cols-3 gap-4">
            <div class="lg:col-span-2 bg-slate-950/75 border border-amber-500/25 rounded-2xl p-4 space-y-4">
              <div class="flex flex-wrap items-center justify-center gap-2 text-xs">
                <span class="text-slate-300">בחר סמל פתיחה:</span>
                <button type="button" id="ttt-pick-x" class="px-3 py-1 rounded-lg bg-amber-600 font-bold">❌ איקס</button>
                <button type="button" id="ttt-pick-o" class="px-3 py-1 rounded-lg bg-slate-800 border border-slate-600 font-bold">⭕ עיגול</button>
              </div>
              <div class="grid grid-cols-3 items-center gap-2 text-center">
                <div class="flex flex-col items-center gap-1">
                  <div id="ttt-p1-sym-icon" class="w-12 h-12 rounded-full border-2 border-amber-400 bg-slate-800 flex items-center justify-center text-lg">❌</div>
                  <span id="ttt-p1-name" class="text-xs font-bold text-slate-300">מושב 1 ריק</span>
                </div>
                <div id="ttt-board" class="grid grid-cols-3 gap-1.5 bg-amber-950/70 p-2.5 rounded-xl border border-amber-700/60 max-w-[220px] w-full mx-auto"></div>
                <div class="flex flex-col items-center gap-1">
                  <div id="ttt-p2-sym-icon" class="w-12 h-12 rounded-full border-2 border-pink-400 bg-slate-800 flex items-center justify-center text-lg">⭕</div>
                  <span id="ttt-p2-name" class="text-xs font-bold text-slate-400">ממתין לכניסה...</span>
                </div>
              </div>
              <div class="flex flex-wrap items-center justify-between gap-2">
                <p id="ttt-status" class="text-sm text-pink-200">בחר שולחן ולחץ "כנס לשולחן"</p>
                <button type="button" id="ttt-reset" class="text-xs bg-slate-800 px-3 py-1.5 rounded-lg border border-slate-600">איפוס לוח</button>
              </div>
            </div>

            <div class="bg-slate-900/80 border border-slate-700 rounded-2xl p-3.5 flex flex-col justify-between space-y-2.5">
              <div class="flex items-center justify-between border-b border-white/10 pb-2">
                <span class="text-xs font-bold text-pink-300">💬 צ׳אט + הקלטות שולחן</span>
                <button type="button" data-voice-target="ttt" class="room-voice-btn px-2.5 py-1 rounded-lg text-[11px] font-bold bg-amber-600">🎤 הקלט</button>
              </div>
              <div id="ttt-room-chat-log" class="space-y-1.5 max-h-48 overflow-y-auto text-xs"></div>
              <form id="ttt-room-chat-form" class="flex gap-1.5">
                <input type="text" id="ttt-room-chat-input" required placeholder="יאללה תורך / אני שם עיגול..."
                  class="flex-1 px-3 py-1.5 rounded-xl bg-slate-950 border border-slate-700 text-xs" />
                <button type="submit" class="px-3.5 py-1.5 rounded-xl text-xs font-semibold bg-pink-600">שלח</button>
              </form>
            </div>
          </div>
        </div><div id="game-rps" class="game-panel hidden max-w-6xl mx-auto glass rounded-2xl p-6 space-y-5">
          <div class="flex flex-wrap items-center justify-between gap-2 border-b border-white/10 pb-3">
            <div>
              <h3 class="text-xl font-bold">✂️ אבן נייר מספריים — 100 חדרים + יצירת חדרים</h3>
              <p class="text-xs text-slate-300">כפתור כנס לשולחן / צא מהשולחן + צ׳אט והקלטות שמתאפסות כשכולם יוצאים</p>
            </div>
            <div class="flex flex-wrap items-center gap-2">
              <span id="rps-timer" class="px-3 py-1 rounded-full text-xs font-bold bg-pink-500/20 border border-pink-400/40 text-pink-200">⏱️ 00:15</span>
              <button type="button" id="rps-add-room" class="px-3.5 py-1.5 rounded-xl text-xs font-semibold bg-emerald-600 hover:bg-emerald-500">+ צור שולחן</button>
              <button type="button" id="rps-join-room" class="px-3.5 py-1.5 rounded-xl text-xs font-semibold bg-pink-600 hover:bg-pink-500">כנס לשולחן</button>
              <button type="button" id="rps-leave-room" class="hidden px-3.5 py-1.5 rounded-xl text-xs font-semibold bg-rose-600 hover:bg-rose-500">צא מהשולחן</button>
            </div>
          </div>

          <div id="rps-rooms-grid" class="grid grid-cols-2 sm:grid-cols-4 md:grid-cols-5 gap-2 max-h-48 overflow-y-auto p-1"></div>

          <div class="grid grid-cols-1 lg:grid-cols-3 gap-4">
            <div class="lg:col-span-2 bg-slate-950/75 border border-white/10 rounded-2xl p-4 space-y-4 text-center">
              <div class="grid grid-cols-3 items-center gap-3">
                <div class="flex flex-col items-center gap-1.5">
                  <div id="rps-left-avatar" class="w-14 h-14 rounded-full border-2 border-pink-400 bg-slate-800 flex items-center justify-center text-xl">🪑</div>
                  <span id="rps-left-name" class="text-xs font-bold text-slate-400">מושב 1 פנוי</span>
                  <div id="rps-left-sign" class="w-16 h-16 rounded-2xl bg-slate-900 border border-slate-700 flex items-center justify-center text-3xl">✊</div>
                </div>

                <div class="flex flex-col items-center justify-center gap-1">
                  <span class="text-xs text-slate-400">ספירה:</span>
                  <div id="rps-count-num" class="text-3xl font-extrabold text-pink-300 count-anim">1 • 2 • 3</div>
                  <span id="rps-round-phase" class="text-xs text-indigo-200">בחר שולחן ולחץ "כנס לשולחן"</span>
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
              <p id="rps-result" class="text-sm text-pink-200 bg-slate-900 p-3.5 rounded-xl">בחר שולחן ולחץ "כנס לשולחן"</p>
            </div>

            <div class="bg-slate-900/80 border border-slate-700 rounded-2xl p-3.5 flex flex-col justify-between space-y-2.5">
              <div class="flex items-center justify-between border-b border-white/10 pb-2">
                <span class="text-xs font-bold text-pink-300">💬 צ׳אט + הקלטות שולחן</span>
                <button type="button" data-voice-target="rps" class="room-voice-btn px-2.5 py-1 rounded-lg text-[11px] font-bold bg-amber-600">🎤 הקלט</button>
              </div>
              <div id="rps-room-chat-log" class="space-y-1.5 max-h-48 overflow-y-auto text-xs"></div>
              <form id="rps-room-chat-form" class="flex gap-1.5">
                <input type="text" id="rps-room-chat-input" required placeholder="כתוב לשחקן שמולך..."
                  class="flex-1 px-3 py-1.5 rounded-xl bg-slate-950 border border-slate-700 text-xs" />
                <button type="submit" class="px-3.5 py-1.5 rounded-xl text-xs font-semibold bg-pink-600">שלח</button>
              </form>
            </div>
          </div>
        </div>

        <div id="game-memory" class="game-panel hidden max-w-6xl mx-auto glass rounded-2xl p-6 space-y-4">
          <div class="flex flex-wrap items-center justify-between gap-2 border-b border-white/10 pb-3">
            <div>
              <h3 class="text-xl font-bold">💎 זיכרון — 8×8, 10×10 ו-30×30 + 6 מושבים בתורות</h3>
              <p class="text-xs text-slate-300">הצליח במושב? ממשיך תור נוסף! טעה? התור עובר למושב הבא • אימוג׳ים גדולים וברורים</p>
            </div>
            <div class="flex flex-wrap items-center gap-2">
              <span id="memory-timer" class="px-3 py-1 rounded-full text-xs font-bold bg-emerald-500/20 border border-emerald-400/40 text-emerald-200">⏱️ 03:00</span>
              <button type="button" id="memory-join-room" class="px-3.5 py-1.5 rounded-xl text-xs font-semibold bg-pink-600 hover:bg-pink-500">כנס לשולחן</button>
              <button type="button" id="memory-leave-room" class="hidden px-3.5 py-1.5 rounded-xl text-xs font-semibold bg-rose-600 hover:bg-rose-500">צא מהשולחן</button>
              <button type="button" id="memory-reset" class="text-xs bg-indigo-600 px-3.5 py-1.5 rounded-xl font-semibold">ערבב לוח</button>
            </div>
          </div>

          <form id="mem-create-room-form" class="flex flex-col sm:flex-row gap-2.5 bg-slate-900/75 p-3 rounded-xl border border-slate-700">
            <input type="text" id="mem-room-name" required placeholder="שם חדר הזיכרון שלך..."
              class="flex-1 px-3.5 py-2 rounded-xl bg-slate-950 border border-slate-700 text-sm" />
            <select id="mem-room-mode" class="px-3.5 py-2 rounded-xl bg-slate-950 border border-slate-700 text-xs">
              <option value="8x8" selected>8×8 (32 זוגות • אימוג׳ים גדולים)</option>
              <option value="10x10">10×10 (50 זוגות • מאתגר)</option>
              <option value="30x30">30×30 (450 זוגות • ענק)</option>
            </select>
            <button type="submit" class="px-4 py-2 rounded-xl text-xs font-semibold bg-emerald-600 hover:bg-emerald-500">
              + פתח חדר משלי
            </button>
          </form>

          <div id="memory-rooms-grid" class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 gap-2 max-h-40 overflow-y-auto p-1"></div>

          <div class="grid grid-cols-1 lg:grid-cols-3 gap-4">
            <div class="lg:col-span-2 space-y-3">
              <div id="memory-players-board" class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-6 gap-2 bg-slate-950/75 p-3 rounded-xl border border-white/10 text-xs"></div>
              <div class="overflow-x-auto max-h-[540px] bg-slate-950/60 p-3 rounded-2xl border border-slate-800">
                <div id="memory-grid" class="grid gap-2 mx-auto"></div>
              </div>
              <p id="memory-status" class="text-sm text-center text-pink-200">בחר חדר זיכרון ולחץ "כנס לשולחן"</p>
            </div>

            <div class="bg-slate-900/80 border border-slate-700 rounded-2xl p-3.5 flex flex-col justify-between space-y-2.5">
              <div class="flex items-center justify-between border-b border-white/10 pb-2">
                <span class="text-xs font-bold text-pink-300">💬 צ׳אט + הקלטות שולחן</span>
                <button type="button" data-voice-target="mem" class="room-voice-btn px-2.5 py-1 rounded-lg text-[11px] font-bold bg-amber-600">🎤 הקלט</button>
              </div>
              <div id="mem-room-chat-log" class="space-y-1.5 max-h-56 overflow-y-auto text-xs"></div>
              <form id="mem-room-chat-form" class="flex gap-1.5">
                <input type="text" id="mem-room-chat-input" required placeholder="וואלה פה אני נמצא..."
                  class="flex-1 px-3 py-1.5 rounded-xl bg-slate-950 border border-slate-700 text-xs" />
                <button type="submit" class="px-3.5 py-1.5 rounded-xl text-xs font-semibold bg-pink-600">שלח</button>
              </form>
            </div>
          </div>
        </div><div id="game-number" class="game-panel hidden max-w-6xl mx-auto glass rounded-2xl p-6 space-y-4">
          <div class="flex flex-wrap items-center justify-between gap-2 border-b border-white/10 pb-3">
            <div>
              <h3 class="text-xl font-bold">🎯 ניחוש מספר — עד 50 משתתפים בחדר</h3>
              <p class="text-xs text-slate-300">הכי קרוב = +3 עד +5 נק׳ • מקום שני = +2 נק׳ • שאר המשתתפים = +1 נק׳ • שוויון מזכה את כולם</p>
            </div>
            <div class="flex flex-wrap items-center gap-2">
              <button type="button" id="num-join-room" class="px-3.5 py-1.5 rounded-xl text-xs font-semibold bg-pink-600 hover:bg-pink-500">כנס לשולחן</button>
              <button type="button" id="num-leave-room" class="hidden px-3.5 py-1.5 rounded-xl text-xs font-semibold bg-rose-600 hover:bg-rose-500">צא מהשולחן</button>
            </div>
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

          <div class="grid grid-cols-1 lg:grid-cols-3 gap-4">
            <div class="lg:col-span-2 bg-slate-950/75 border border-indigo-500/30 rounded-2xl p-4 space-y-4">
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
                    🏆 חשב נקודות לכולם
                  </button>
                </div>
                <p id="num-guess-feedback" class="text-sm font-medium text-pink-200 bg-slate-900 p-3 rounded-xl"></p>
                <div id="num-guesses-log" class="space-y-1.5 max-h-40 overflow-y-auto text-xs"></div>
              </div>
            </div>

            <div class="bg-slate-900/80 border border-slate-700 rounded-2xl p-3.5 flex flex-col justify-between space-y-2.5">
              <div class="flex items-center justify-between border-b border-white/10 pb-2">
                <span class="text-xs font-bold text-pink-300">💬 צ׳אט + הקלטות שולחן</span>
                <button type="button" data-voice-target="num" class="room-voice-btn px-2.5 py-1 rounded-lg text-[11px] font-bold bg-amber-600">🎤 הקלט</button>
              </div>
              <div id="num-room-chat-log" class="space-y-1.5 max-h-48 overflow-y-auto text-xs"></div>
              <form id="num-room-chat-form" class="flex gap-1.5">
                <input type="text" id="num-room-chat-input" required placeholder="כתוב למשתתפים בחדר..."
                  class="flex-1 px-3 py-1.5 rounded-xl bg-slate-950 border border-slate-700 text-xs" />
                <button type="submit" class="px-3.5 py-1.5 rounded-xl text-xs font-semibold bg-pink-600">שלח</button>
              </form>
            </div>
          </div>
        </div>

        <div id="game-roulette" class="game-panel hidden max-w-6xl mx-auto glass rounded-2xl p-6 space-y-5">
          <div class="flex flex-wrap items-center justify-between gap-2 border-b border-white/10 pb-3">
            <div>
              <h3 class="text-xl font-bold">🔫 רולטה רוסית — שולחן עגול של 6 מושבים (6 כדורים)</h3>
              <p class="text-xs text-slate-300">האקדח מסתובב אל המושב • מי שנורה חווה קונפטי ולא ממשיך עד סוף הסיבוב • השורד האחרון זוכה בכדור זהב ← מחסנית ← אקדח ← מתנה גדולה</p>
            </div>
            <div class="flex flex-wrap items-center gap-2">
              <button type="button" id="rr-join-btn" class="px-3.5 py-1.5 rounded-xl text-xs font-semibold bg-pink-600 hover:bg-pink-500">כנס לשולחן</button>
              <button type="button" id="rr-leave-btn" class="hidden px-3.5 py-1.5 rounded-xl text-xs font-semibold bg-rose-600 hover:bg-rose-500">צא מהשולחן</button>
            </div>
          </div>

          <div class="grid grid-cols-2 sm:grid-cols-4 gap-2 text-center text-xs bg-slate-950/75 p-3 rounded-xl border border-amber-400/25">
            <div>🟡 כדורי זהב: <strong id="rr-gold-balls" class="text-amber-300">0</strong></div>
            <div>🎞️ מחסניות: <strong id="rr-magazines" class="text-indigo-300">0</strong></div>
            <div>🔫 אקדחים מוזהבים: <strong id="rr-pistols" class="text-pink-300">0</strong></div>
            <div>🎁 מתנות גדולות: <strong id="rr-grand-gifts" class="text-emerald-300">0</strong></div>
          </div>

          <div class="grid grid-cols-1 lg:grid-cols-3 gap-4">
            <div class="lg:col-span-2 bg-slate-950/80 border border-amber-500/30 rounded-2xl p-5 space-y-4">
              <div id="rr-seats-ring" class="grid grid-cols-2 sm:grid-cols-3 gap-3"></div>

              <div class="flex flex-col items-center justify-center py-4 bg-slate-900/90 rounded-2xl border border-slate-800 space-y-3 relative overflow-hidden">
                <div id="rr-confetti-banner" class="hidden text-sm font-extrabold text-amber-300 animate-bounce">🎉🎊 בום קונפטי! ירייה! 🎊🎉</div>
                <div id="rr-gun-spinner" class="text-5xl transition-transform duration-500 select-none">🔫</div>
                <div id="rr-aimed-label" class="text-xs font-bold text-pink-200">האקדח מכוון למושב #1</div>
                <div class="flex flex-wrap gap-2.5 justify-center">
                  <button type="button" id="rr-spin-btn" class="px-4 py-2 rounded-xl text-xs font-bold bg-indigo-600 hover:bg-indigo-500">🔄 סובב אקדח</button>
                  <button type="button" id="rr-pull-btn" class="px-5 py-2 rounded-xl text-xs font-bold bg-rose-600 hover:bg-rose-500">💥 לחץ על ההדק</button>
                  <button type="button" id="rr-new-round-btn" class="px-4 py-2 rounded-xl text-xs font-bold bg-emerald-600 hover:bg-emerald-500">🔁 סיבוב חדש</button>
                </div>
              </div>

              <p id="rr-status" class="text-sm text-center text-pink-200 bg-slate-900 p-3 rounded-xl">בחר מושב ולחץ "כנס לשולחן"</p>
            </div>

            <div class="bg-slate-900/80 border border-slate-700 rounded-2xl p-3.5 flex flex-col justify-between space-y-2.5">
              <div class="flex items-center justify-between border-b border-white/10 pb-2">
                <span class="text-xs font-bold text-pink-300">💬 צ׳אט + הקלטות שולחן</span>
                <button type="button" data-voice-target="rr" class="room-voice-btn px-2.5 py-1 rounded-lg text-[11px] font-bold bg-amber-600">🎤 הקלט</button>
              </div>
              <div id="rr-room-chat-log" class="space-y-1.5 max-h-56 overflow-y-auto text-xs"></div>
              <form id="rr-room-chat-form" class="flex gap-1.5">
                <input type="text" id="rr-room-chat-input" required placeholder="כתוב לשולחן העגול..."
                  class="flex-1 px-3 py-1.5 rounded-xl bg-slate-950 border border-slate-700 text-xs" />
                <button type="submit" class="px-3.5 py-1.5 rounded-xl text-xs font-semibold bg-pink-600">שלח</button>
              </form>
            </div>
          </div>
        </div>
      </div>
    </section>
  </main><script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/11.0.0/firebase-app.js";
    import { getAnalytics } from "https://www.gstatic.com/firebasejs/11.0.0/firebase-analytics.js";
    import {
      getFirestore, collection, doc, setDoc, addDoc, getDocs, deleteDoc,
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
    const WEEK_MS = 7 * 24 * 60 * 60 * 1000;

    const levelThresholds = Array.from({ length: 31 }, (_, lvl) => {
      if (lvl === 0) return 0;
      if (lvl === 1) return 100;
      if (lvl === 2) return 300;
      if (lvl === 3) return 600;
      return 600 + (lvl - 3) * 400;
    });

    function getLevel(pts = 0) {
      let current = 0;
      for (let i = 1; i < levelThresholds.length; i++) {
        if (pts >= levelThresholds[i]) current = i;
      }
      return current;
    }

    const hobbiesChoices = [
      "📺 לראות סדרות ובינג׳", "🎬 קולנוע וסרטים", "🥾 טיולים", "🏋️ ספורט וכושר",
      "📷 צילום", "🍳 בישול ואפייה", "🎮 גיימינג", "📚 קריאה",
      "💃 ריקוד", "🎸 נגינה", "🎨 ציור ואמנות", "🚴 רכיבת אופניים",
      "🏕️ קמפינג", "🧘 יוגה ומדיטציה", "🐶 גידול חיות מחמד", "✈️ נסיעות לחו״ל",
      "♟️ משחקי אסטרטגיה", "🌱 גינון", "🎤 שירה וקריוקי", "🎶 הופעות ומוזיקה"
    ];let weekStartTs = Number(localStorage.getItem("toplove_week_start") || Date.now());
    if (!localStorage.getItem("toplove_week_start")) localStorage.setItem("toplove_week_start", String(weekStartTs));

    async function checkWeeklyAutoReset() {
      const elapsed = Date.now() - weekStartTs;
      const remDays = Math.max(0, Math.ceil((WEEK_MS - elapsed) / (24 * 60 * 60 * 1000)));
      $("weekly-reset-badge").textContent = `⏳ איפוס שבועי אוטומטי בעוד: ${remDays} ימים`;
      if (elapsed >= WEEK_MS) {
        weekStartTs = Date.now();
        localStorage.setItem("toplove_week_start", String(weekStartTs));
        for (const r of chatRooms) {
          try {
            const snap = await getDocs(collection(db, "rooms", r.id, "messages"));
            for (const d of snap.docs) await deleteDoc(d.ref);
          } catch {}
        }
        $("weekly-reset-badge").textContent = "⏳ איפוס שבועי אוטומטי בעוד: 7 ימים";
      }
    }
    checkWeeklyAutoReset();

    const gameNames = {
      ttt: "איקס עיגול", rps: "אבן נייר מספריים",
      memory: "משחק הזיכרון", number: "ניחוש מספר", roulette: "רולטה רוסית"
    };

    const me = {
      uid: "", email: "", name: "", gender: "", age: 18,
      location: "", distanceKm: 15, smoking: "", alcohol: "", education: "",
      hasPets: "", favPet: "", otherPetText: "",
      tagline: "", banner: "bg-aurora", nameStyle: "name-rainbow", bio: "",
      hobbies: [], photos: [], following: [],
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

    let currentGameKey = "ttt";
    const gameLeaderboards = { ttt: [], rps: [], memory: [], number: [], roulette: [] };

    function upsertPlayerBoard(gameKey, playerName, st) {
      const playedCount = Number(st?.played || 0);
      if (playedCount < 1) {
        gameLeaderboards[gameKey] = gameLeaderboards[gameKey].filter((x) => x.name !== playerName);
        return;
      }
      const pts = Number(st.points || 0);
      const lvl = getLevel(pts);
      const ex = gameLeaderboards[gameKey].find((x) => x.name === playerName);
      if (ex) { ex.points = pts; ex.level = lvl; ex.played = playedCount; }
      else gameLeaderboards[gameKey].push({ name: playerName, points: pts, level: lvl, played: playedCount });
      gameLeaderboards[gameKey].sort((a, b) => b.level - a.level || b.points - a.points);
      gameLeaderboards[gameKey] = gameLeaderboards[gameKey].slice(0, 100);
    }

    function getRewardLabel(gameKey, rankIdx) {
      if (rankIdx === 0) {
        if (gameKey === "ttt") return "🥇 זהב • איקס זהב";
        if (gameKey === "rps") return "🥇 זהב • אבן/נייר/מספריים זהב";
        if (gameKey === "number") return "🥇 זהב • מוח/משקפי/כובע בלשים זהב";
        if (gameKey === "roulette") return "🥇 זהב • כדור זהב / מחסנית / אקדח";
        return "🥇 זהב • אלוף הזיכרון";
      }
      if (rankIdx === 1) return "🥈 כסף";
      if (rankIdx === 2) return "🥉 ארד";
      return "📋 טופ-100";
    }

    function renderGameStatsAndTop5(gameKey = currentGameKey) {
      currentGameKey = gameKey;
      const st = me.gameStats[gameKey] || { points: 0, wins: 0, losses: 0, played: 0 };
      upsertPlayerBoard(gameKey, me.name || "שחקן", st);

      const lvl = getLevel(st.points);
      $("stat-game-level").textContent = `רמה ${lvl}`;
      $("stat-game-name").textContent = gameNames[gameKey];
      $("stat-game-points").textContent = String(st.points);
      $("stat-game-wins").textContent = String(st.wins);
      $("stat-game-losses").textContent = String(st.losses);

      const top100List = gameLeaderboards[gameKey];
      $("top100-count-badge").textContent = `${top100List.length} / 100 שחקנים מדורגים`;
      $("top5-title").textContent = `🏅 טופ-5 ב${gameNames[gameKey]} (מתוך רשימת הטופ-100 • נכנסים אחרי משחק אחד לפחות)`;

      const top5List = top100List.slice(0, 5);
      $("top5-board").innerHTML = top5List.length
        ? top5List.map((p, i) => `
            <div class="p-2.5 rounded-xl bg-slate-900 border ${i === 0 ? "border-amber-400" : i === 1 ? "border-slate-300" : i === 2 ? "border-amber-700" : "border-slate-800"}">
              <div class="font-bold truncate">${i + 1}. ${p.name}</div>
              <div class="text-pink-300">רמה ${p.level} • ${p.points} נק׳</div>
              <div class="text-[11px] text-amber-300 mt-0.5">${getRewardLabel(gameKey, i)}</div>
            </div>
          `).join("")
        : `<p class="text-slate-400 col-span-full">שחק לפחות משחק אחד כדי להיכנס לרשימת הטופ-100 ולטופ-5.</p>`;

      localStorage.setItem("toplove_session", JSON.stringify(me));
    }

    async function awardGameWin(gameKey, pts) {
      me.gameStats[gameKey].played += 1;
      me.gameStats[gameKey].wins += 1;
      me.gameStats[gameKey].points += pts;
      renderGameStatsAndTop5(gameKey);
      try { if (me.uid) await setDoc(doc(db, "users", me.uid), { gameStats: me.gameStats, rrRewards: me.rrRewards }, { merge: true }); } catch {}
    }

    async function awardGameLoss(gameKey, pts = 5) {
      me.gameStats[gameKey].played += 1;
      me.gameStats[gameKey].losses += 1;
      me.gameStats[gameKey].points += pts;
      renderGameStatsAndTop5(gameKey);
      try { if (me.uid) await setDoc(doc(db, "users", me.uid), { gameStats: me.gameStats, rrRewards: me.rrRewards }, { merge: true }); } catch {}
    }let modalPhotos = [], modalPhotoIdx = 0;

    function formatPetLine(p) {
      const parts = [];
      if (p.hasPets) parts.push(p.hasPets);
      if (p.favPet === "אחר") parts.push(p.otherPetText ? `אוהב/ת: ${p.otherPetText}` : "אוהב/ת: אחר");
      else if (p.favPet) parts.push(`אוהב/ת: ${p.favPet}`);
      return parts.length ? `🐾 ${parts.join(" • ")}` : "";
    }

    function updateModalPhotoView() {
      if (!modalPhotos.length) return;
      $("modal-main-photo").src = modalPhotos[modalPhotoIdx];
      document.querySelectorAll(".modal-thumb").forEach((img, i) => img.classList.toggle("border-pink-400", i === modalPhotoIdx));
    }

    function openUserModal(person) {
      const gPoints = Object.values(person.gameStats || {}).reduce((acc, s) => acc + (Number(s.points) || 0), 0);
      const lvl = getLevel(gPoints);
      modalPhotos = Array.isArray(person.photos) && person.photos.length ? person.photos : [];
      modalPhotoIdx = 0;

      $("modal-banner").className = `h-32 ${person.banner || "bg-aurora"} relative p-4 flex justify-between items-start`;
      $("modal-level-badge").textContent = `רמה ${lvl} • ${gPoints} נק׳`;
      $("modal-name").className = `text-2xl font-extrabold ${person.nameStyle || ""}`;
      $("modal-name").textContent = person.name || "משתמש";
      $("modal-tagline").textContent = person.tagline || "";
      $("modal-meta").textContent = [person.gender, person.age ? `גיל ${person.age}` : "", person.location, person.distanceKm !== undefined ? `${person.distanceKm} ק״מ ממך` : ""].filter(Boolean).join(" • ");
      $("modal-habits").textContent = [person.smoking ? `🚬 ${person.smoking}` : "", person.alcohol ? `🍷 ${person.alcohol}` : ""].filter(Boolean).join(" • ");
      $("modal-pets-info").textContent = formatPetLine(person);
      $("modal-education").textContent = person.education ? `🎓 השכלה: ${person.education}` : "";
      $("modal-bio").textContent = person.bio || "";
      $("modal-action-msg").textContent = "";

      if (modalPhotos.length) {
        $("modal-main-photo").classList.remove("hidden");
        $("modal-gallery").innerHTML = modalPhotos.map((src, i) => `<img src="${src}" alt="" class="w-16 h-16 rounded-xl object-cover border ${i === 0 ? "border-pink-400" : "border-white/20"} cursor-pointer shrink-0 modal-thumb" />`).join("");
        document.querySelectorAll(".modal-thumb").forEach((img, i) => { img.onclick = () => { modalPhotoIdx = i; updateModalPhotoView(); }; });
        updateModalPhotoView();
      } else {
        $("modal-main-photo").classList.add("hidden");
        $("modal-gallery").innerHTML = `<span class="text-xs text-slate-400">לא הועלתה תמונה</span>`;
      }

      const tags = person.hobbies || [];
      $("modal-tags").innerHTML = tags.length ? tags.map((t) => `<span class="px-2.5 py-1 rounded-full bg-indigo-500/20 border border-indigo-400/30">${t}</span>`).join("") : `<span class="text-slate-400">לא נבחרו תחביבים</span>`;

      const targetId = person.uid || person.id;
      $("modal-follow-btn").textContent = (me.following || []).includes(targetId) ? "✓ עוקב" : "➕ עקוב";

      $("modal-like-btn").onclick = async () => {
        if (!targetId) return;
        const dmId = "dm_" + [me.uid, targetId].sort().join("_");
        try { await addDoc(collection(db, "rooms", dmId, "messages"), { senderUid: me.uid, from: me.name || "משתמש", avatar: me.avatar || "", text: `👍 ${me.name || "משתמש"} סימן/ה לך לייק!`, createdAt: serverTimestamp() }); } catch {}
        $("modal-action-msg").textContent = `👍 נשלחה הודעה ל${person.name || "משתמש"}: סימנת לייק!`;
      };

      $("modal-heart-btn").onclick = async () => {
        if (!targetId) return;
        const dmId = "dm_" + [me.uid, targetId].sort().join("_");
        try { await addDoc(collection(db, "rooms", dmId, "messages"), { senderUid: me.uid, from: me.name || "משתמש", avatar: me.avatar || "", text: `💖 ${me.name || "משתמש"} סימן/ה לך לב!`, createdAt: serverTimestamp() }); } catch {}
        $("modal-action-msg").textContent = `💖 נשלחה הודעה ל${person.name || "משתמש"}: סימנת לב!`;
      };

      $("modal-follow-btn").onclick = () => {
        if (!targetId || targetId === me.uid) return;
        me.following = me.following || [];
        me.following = me.following.includes(targetId) ? me.following.filter((x) => x !== targetId) : [...me.following, targetId];
        localStorage.setItem("toplove_session", JSON.stringify(me));
        openUserModal(person); renderRealUsers();
      };

      $("modal-dm-btn").onclick = () => {
        if (!targetId || targetId === me.uid) return;
        const dmId = "dm_" + [me.uid, targetId].sort().join("_");
        if (!chatRooms.some((r) => r.id === dmId)) chatRooms.unshift({ id: dmId, topic: `שיחה אישית עם ${person.name || "משתמש"}`, code: "", members: [me.uid, targetId] });
        activeRoomId = dmId; joinedRoomId = dmId; $("user-modal").classList.add("hidden"); switchTab("chat"); renderRooms();
      };

      $("user-modal").classList.remove("hidden");
    }

    $("modal-prev-photo").onclick = () => { if (modalPhotos.length) { modalPhotoIdx = (modalPhotoIdx - 1 + modalPhotos.length) % modalPhotos.length; updateModalPhotoView(); } };
    $("modal-next-photo").onclick = () => { if (modalPhotos.length) { modalPhotoIdx = (modalPhotoIdx + 1) % modalPhotos.length; updateModalPhotoView(); } };
    $("close-modal-btn").onclick = () => $("user-modal").classList.add("hidden");
    $("summary-avatar").onclick = () => openUserModal(me);let summaryPhotoIdx = 0;

    function syncOtherPetField() {
      $("prof-other-pet-wrap").classList.toggle("hidden", $("prof-fav-pet").value !== "אחר");
    }
    $("prof-fav-pet").onchange = syncOtherPetField;

    function renderQuestionnaireOptions() {
      $("hobbies-options").innerHTML = hobbiesChoices.map((item) => `<button type="button" data-hobby="${item}" class="px-3 py-1.5 rounded-full text-xs border transition ${me.hobbies.includes(item) ? "bg-indigo-600 border-indigo-400 text-white" : "bg-slate-950 border-slate-700 text-slate-300"}">${item}</button>`).join("");
      $("hobbies-options").querySelectorAll("[data-hobby]").forEach((btn) => { btn.onclick = () => { const v = btn.dataset.hobby; me.hobbies = me.hobbies.includes(v) ? me.hobbies.filter((x) => x !== v) : [...me.hobbies, v]; renderQuestionnaireOptions(); }; });
    }

    function syncStylePickUI() {
      document.querySelectorAll(".style-pick-btn").forEach((b) => {
        b.classList.toggle("border-pink-400", b.dataset.style === me.nameStyle);
        b.classList.toggle("border-slate-700", b.dataset.style !== me.nameStyle);
      });
    }
    document.querySelectorAll(".style-pick-btn").forEach((b) => { b.onclick = () => { me.nameStyle = b.dataset.style; syncStylePickUI(); }; });

    function renderPhotoThumbs() {
      $("prof-avatar-frame").className = `p-2 rounded-3xl ${me.banner || "bg-aurora"} shadow-lg shrink-0`;
      if (me.hasCustomPhoto && me.photos && me.photos.length) {
        $("prof-avatar-preview").src = me.photos[0];
        $("prof-photos-thumbs").innerHTML = me.photos.map((src, idx) => `<img src="${src}" alt="" data-photo-idx="${idx}" class="w-14 h-14 rounded-xl object-cover border border-pink-400 cursor-pointer" />`).join("");
        document.querySelectorAll("[data-photo-idx]").forEach((img) => { img.onclick = () => { me.avatar = img.src; $("prof-avatar-preview").src = img.src; }; });
      } else {
        $("prof-photos-thumbs").innerHTML = `<span class="text-xs text-slate-400">עדיין לא נבחרה תמונה מהמכשיר</span>`;
      }
    }

    function applyProfileViewMode() {
      const showSummary = Boolean(me.profileCompleted);
      $("profile-summary-card").classList.toggle("hidden", !showSummary);
      $("profile-form").classList.toggle("hidden", showSummary);
      $("edit-profile-btn").classList.toggle("hidden", !showSummary);
      if (showSummary) {
        const gPoints = Object.values(me.gameStats || {}).reduce((acc, s) => acc + (Number(s.points) || 0), 0);
        const lvl = getLevel(gPoints);
        const photos = me.hasCustomPhoto && Array.isArray(me.photos) && me.photos.length ? me.photos : [];
        $("summary-banner").className = `h-32 ${me.banner || "bg-aurora"} p-4 flex items-center justify-between`;
        $("summary-level-badge").textContent = `רמה ${lvl} • ${gPoints} נק׳`;
        $("summary-likes-badge").textContent = `👥 עוקב אחרי ${(me.following || []).length}`;

        if (photos.length) {
          summaryPhotoIdx = summaryPhotoIdx % photos.length;
          $("summary-avatar").classList.remove("hidden");
          $("summary-avatar").src = photos[summaryPhotoIdx];
          $("summary-photos-strip").innerHTML = photos.map((src, i) => `<img src="${src}" alt="" data-sum-idx="${i}" class="w-16 h-16 rounded-xl object-cover border ${i === summaryPhotoIdx ? "border-pink-400" : "border-white/20"} shrink-0 cursor-pointer" />`).join("");
          document.querySelectorAll("[data-sum-idx]").forEach((img) => { img.onclick = () => { summaryPhotoIdx = Number(img.dataset.sumIdx); applyProfileViewMode(); }; });
        } else {
          $("summary-avatar").classList.add("hidden");
          $("summary-photos-strip").innerHTML = "";
        }

        $("summary-name").className = `text-2xl font-extrabold ${me.nameStyle || ""}`;
        $("summary-name").textContent = me.name || "משתמש";
        $("summary-tagline").textContent = me.tagline || "";
        $("summary-age-gender-loc").textContent = [me.gender, me.age ? `גיל ${me.age}` : "", me.location, me.distanceKm !== undefined ? `${me.distanceKm} ק״מ` : ""].filter(Boolean).join(" • ");
        $("summary-habits").textContent = [me.smoking ? `🚬 ${me.smoking}` : "", me.alcohol ? `🍷 ${me.alcohol}` : ""].filter(Boolean).join(" • ");
        $("summary-pets").textContent = formatPetLine(me);
        $("summary-bio").textContent = me.bio || "";
        $("summary-hobbies").innerHTML = me.hobbies.length ? me.hobbies.map((h) => `<span class="px-2.5 py-1 rounded-full bg-indigo-500/20 border border-indigo-400/30">${h}</span>`).join("") : `<span class="text-slate-400">לא נבחר</span>`;
        $("summary-education").textContent = [formatPetLine(me), me.education ? `🎓 ${me.education}` : ""].filter(Boolean).join(" | ") || "לא צוין";
      }
    }

    $("summary-prev-photo").onclick = () => { const len = (me.photos || []).length || 1; summaryPhotoIdx = (summaryPhotoIdx - 1 + len) % len; applyProfileViewMode(); };
    $("summary-next-photo").onclick = () => { const len = (me.photos || []).length || 1; summaryPhotoIdx = (summaryPhotoIdx + 1) % len; applyProfileViewMode(); };
    $("edit-profile-btn").onclick = () => { me.profileCompleted = false; applyProfileViewMode(); };function switchTab(tabName) {
      document.querySelectorAll(".tab-btn").forEach((b) => { b.className = b.dataset.tab === tabName ? "tab-btn px-5 py-2.5 rounded-xl text-sm font-semibold bg-pink-600 text-white" : "tab-btn px-5 py-2.5 rounded-xl text-sm font-semibold glass text-slate-300"; });
      document.querySelectorAll(".tab-content").forEach((c) => c.classList.add("hidden"));
      $(`tab-${tabName}`).classList.remove("hidden");
    }

    function openApp(session) {
      Object.assign(me, session);
      me.hobbies = Array.isArray(session.hobbies) ? session.hobbies : [];
      me.photos = Array.isArray(session.photos) ? session.photos : [];
      me.following = Array.isArray(session.following) ? session.following : [];
      me.rrRewards = Object.assign({ goldBalls: 0, magazines: 0, pistols: 0, grandGifts: 0 }, session.rrRewards || {});
      me.gameStats = Object.assign({
        ttt: { points: 0, wins: 0, losses: 0, played: 0 },
        rps: { points: 0, wins: 0, losses: 0, played: 0 },
        memory: { points: 0, wins: 0, losses: 0, played: 0 },
        number: { points: 0, wins: 0, losses: 0, played: 0 },
        roulette: { points: 0, wins: 0, losses: 0, played: 0 }
      }, session.gameStats || {});

      $("auth-section").classList.add("hidden"); $("app-section").classList.remove("hidden");
      $("user-badge").classList.remove("hidden"); $("logout-btn").classList.remove("hidden");
      $("user-badge").textContent = `${me.name || me.email.split("@")[0]} • ${me.age || 18}`;
      $("prof-name").value = me.name || ""; $("prof-gender").value = me.gender || ""; $("prof-age").value = me.age || 18;
      $("prof-location").value = me.location || ""; $("prof-distance").value = me.distanceKm ?? 15;
      $("prof-smoking").value = me.smoking || ""; $("prof-alcohol").value = me.alcohol || "";
      $("prof-education").value = me.education || ""; $("prof-has-pets").value = me.hasPets || "";
      $("prof-fav-pet").value = me.favPet || ""; $("prof-other-pet-text").value = me.otherPetText || "";
      $("prof-tagline").value = me.tagline || ""; $("prof-banner").value = me.banner || "bg-aurora"; $("prof-bio").value = me.bio || "";

      syncOtherPetField(); syncStylePickUI(); renderRrRewardsUI(); renderGameStatsAndTop5(currentGameKey);
      renderPhotoThumbs(); renderQuestionnaireOptions(); applyProfileViewMode();
      switchTab("profile"); renderRooms(); subscribeUsers();
    }

    $("toggle-password-btn").onclick = () => { $("auth-password").type = $("auth-password").type === "password" ? "text" : "password"; };

    $("auth-form").onsubmit = async (e) => {
      e.preventDefault();
      const email = $("auth-email").value.trim().toLowerCase(), age = Number($("auth-age").value);
      if (!age || age < 18 || age > 80) { $("auth-error").textContent = "כניסה מותרת לגילאי 18 עד 80 בלבד."; $("auth-error").classList.remove("hidden"); return; }
      $("auth-error").classList.add("hidden");
      const uid = "u_" + email.replace(/[^a-z0-9]/g, "_");
      const session = {
        uid, email, name: email.split("@")[0] || "משתמש", gender: "", age, location: "ישראל", distanceKm: 10,
        smoking: "", alcohol: "", education: "", hasPets: "", favPet: "", otherPetText: "",
        tagline: "", banner: "bg-aurora", nameStyle: "name-rainbow", bio: "",
        hobbies: [], photos: [], following: [], avatar: "", hasCustomPhoto: false, profileCompleted: false,
        rrRewards: { goldBalls: 0, magazines: 0, pistols: 0, grandGifts: 0 },
        gameStats: {
          ttt: { points: 0, wins: 0, losses: 0, played: 0 },
          rps: { points: 0, wins: 0, losses: 0, played: 0 },
          memory: { points: 0, wins: 0, losses: 0, played: 0 },
          number: { points: 0, wins: 0, losses: 0, played: 0 },
          roulette: { points: 0, wins: 0, losses: 0, played: 0 }
        }
      };
      localStorage.setItem("toplove_session", JSON.stringify(session));
      try { await setDoc(doc(db, "users", uid), { ...session, updatedAt: serverTimestamp() }, { merge: true }); } catch {}
      openApp(session);
    };

    $("logout-btn").onclick = () => { localStorage.removeItem("toplove_session"); location.reload(); };
    document.querySelectorAll(".tab-btn").forEach((btn) => { btn.onclick = () => switchTab(btn.dataset.tab); });

    $("prof-avatar-file").onchange = (e) => {
      const files = Array.from(e.target.files || []);
      if (!files.length) return;
      me.photos = [];
      me.hasCustomPhoto = true;
      files.forEach((f) => {
        const rd = new FileReader();
        rd.onload = () => { me.photos.push(String(rd.result)); me.avatar = me.photos[0]; renderPhotoThumbs(); };
        rd.readAsDataURL(f);
      });
    };
    $("prof-banner").onchange = (e) => { me.banner = e.target.value; renderPhotoThumbs(); };

    $("profile-form").onsubmit = async (e) => {
      e.preventDefault();
      const ageVal = $("prof-age").value ? Number($("prof-age").value) : 18;
      if (ageVal < 18 || ageVal > 80) { $("profile-error").textContent = "הגיל חייב להיות בין 18 ל-80."; $("profile-error").classList.remove("hidden"); return; }
      $("profile-error").classList.add("hidden");
      Object.assign(me, {
        name: $("prof-name").value.trim() || me.name || "משתמש", gender: $("prof-gender").value, age: ageVal,
        location: $("prof-location").value.trim(), distanceKm: Number($("prof-distance").value) || 0,
        smoking: $("prof-smoking").value, alcohol: $("prof-alcohol").value, education: $("prof-education").value.trim(),
        hasPets: $("prof-has-pets").value, favPet: $("prof-fav-pet").value, otherPetText: $("prof-other-pet-text").value.trim(),
        tagline: $("prof-tagline").value.trim(), banner: $("prof-banner").value, bio: $("prof-bio").value.trim(),
        avatar: (me.hasCustomPhoto && me.photos && me.photos[0]) ? me.photos[0] : "", profileCompleted: true
      });
      localStorage.setItem("toplove_session", JSON.stringify(me));
      $("user-badge").textContent = `${me.name} • ${me.age}`;
      try { await setDoc(doc(db, "users", me.uid), { ...me, updatedAt: serverTimestamp() }, { merge: true }); } catch {}
      applyProfileViewMode(); renderGameStatsAndTop5(currentGameKey);
      $("save-feedback").classList.remove("opacity-0"); setTimeout(() => $("save-feedback").classList.add("opacity-0"), 1500);
    };

    let allUsers = [];
    function renderRealUsers() {
      $("following-count-badge").textContent = `עוקב אחרי ${(me.following || []).length} משתמשים`;
      const maxDist = $("filter-distance").value, minAge = Number($("filter-min-age").value) || 18, maxAge = Number($("filter-max-age").value) || 80;
      const filtered = allUsers.filter((u) => {
        const uAge = Number(u.age) || 18, uDist = Number(u.distanceKm ?? 0);
        return uAge >= minAge && uAge <= maxAge && (maxDist === "all" || uDist <= Number(maxDist));
      });
      $("real-users-grid").innerHTML = filtered.length
        ? filtered.map((u) => {
            const gPoints = Object.values(u.gameStats || {}).reduce((acc, s) => acc + (Number(s.points) || 0), 0);
            const lvl = getLevel(gPoints), isF = (me.following || []).includes(u.id);
            const avHtml = u.avatar ? `<img src="${u.avatar}" alt="" data-open-user="${u.id}" class="w-14 h-14 rounded-xl object-cover border-2 border-slate-900 bg-slate-800 cursor-pointer shrink-0" />`
              : `<div data-open-user="${u.id}" class="w-14 h-14 rounded-xl border-2 border-slate-900 bg-slate-800 flex items-center justify-center text-xl cursor-pointer shrink-0">👤</div>`;
            return `<div class="bg-slate-900/85 border border-slate-700 rounded-2xl overflow-hidden flex flex-col justify-between">
              <div>
                <div class="h-14 ${u.banner || "bg-aurora"}"></div>
                <div class="p-4 -mt-7 space-y-2">
                  <div class="flex items-end gap-3">
                    ${avHtml}
                    <div>
                      <div data-open-user="${u.id}" class="font-bold text-sm cursor-pointer hover:underline ${u.nameStyle || ""}">${u.name || "משתמש"}</div>
                      <div class="text-[11px] text-amber-300">רמה ${lvl} • ${u.age || 18} • ${u.distanceKm ?? 0} ק״מ</div>
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
        : `<p class="text-xs text-slate-400 col-span-full">אין משתמשים התואמים לסינון המרחק והגיל שנבחר.</p>`;

      document.querySelectorAll("[data-open-user]").forEach((el) => { el.onclick = () => { const f = allUsers.find((x) => x.id === el.dataset.openUser); if (f) openUserModal(f); }; });
      document.querySelectorAll("[data-follow-user]").forEach((btn) => { btn.onclick = () => { const id = btn.dataset.followUser; me.following = me.following || []; me.following = me.following.includes(id) ? me.following.filter((x) => x !== id) : [...me.following, id]; renderRealUsers(); }; });
      document.querySelectorAll("[data-dm-user]").forEach((btn) => {
        btn.onclick = () => {
          const other = allUsers.find((x) => x.id === btn.dataset.dmUser); if (!other) return;
          const dmId = "dm_" + [me.uid, other.id].sort().join("_");
          if (!chatRooms.some((r) => r.id === dmId)) chatRooms.unshift({ id: dmId, topic: `שיחה אישית עם ${other.name || "משתמש"}`, code: "", members: [me.uid, other.id] });
          activeRoomId = dmId; joinedRoomId = dmId; switchTab("chat"); renderRooms();
        };
      });
    }

    $("filter-distance").onchange = renderRealUsers;
    $("filter-min-age").oninput = renderRealUsers;
    $("filter-max-age").oninput = renderRealUsers;

    function subscribeUsers() {
      onSnapshot(collection(db, "users"), (snap) => {
        allUsers = snap.docs.map((d) => ({ id: d.id, ...d.data() })).filter((u) => u.id !== me.uid);
        for (const u of allUsers) {
          for (const gKey of ["ttt", "rps", "memory", "number", "roulette"]) {
            const st = u.gameStats?.[gKey];
            if (st && Number(st.played || 0) >= 1) upsertPlayerBoard(gKey, u.name || "משתמש", st);
          }
        }
        renderGameStatsAndTop5(currentGameKey); renderRealUsers();
      });
    }const chatRooms = [
      { id: "r-general", topic: "כללי וצ׳אט פתוח", code: "", members: [] },
      { id: "r-music", topic: "מוזיקה, פלייליסטים והופעות", code: "", members: [] },
      { id: "r-movies", topic: "סרטים, סדרות ואנימה", code: "", members: [] },
      { id: "r-food", topic: "אוכל, מסעדות ומתכונים", code: "", members: [] },
      { id: "r-travel", topic: "טיולים בארץ ובחו״ל", code: "", members: [] },
      { id: "r-gaming", topic: "גיימינג ומשחקי רשת", code: "", members: [] },
      { id: "r-fitness", topic: "ספורט, חדר כושר ואורח חיים", code: "", members: [] },
      { id: "r-dating", topic: "היכרויות, דייטים ושיחות", code: "", members: [] },
      { id: "r-humor", topic: "בדיחות, ממים וצחוקים", code: "", members: [] },
      { id: "r-night", topic: "ציפורי לילה ושיחות מאוחרות", code: "", members: [] }
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
              const av = m.avatar || sObj.avatar || "";
              const avBox = av ? `<img src="${av}" alt="" data-msg-user="${m.senderUid || ""}" class="w-9 h-9 rounded-full object-cover border border-pink-400 cursor-pointer shrink-0" />`
                : `<div data-msg-user="${m.senderUid || ""}" class="w-9 h-9 rounded-full bg-slate-900 border border-pink-400 flex items-center justify-center text-sm cursor-pointer shrink-0">👤</div>`;
              const body = m.audioData ? `<audio controls src="${m.audioData}" class="w-full max-w-xs h-8 mt-1"></audio>` : `<div class="text-sm mt-0.5">${m.text || ""}</div>`;
              return `<div class="bg-slate-800/90 px-3 py-2 rounded-xl flex items-start gap-2.5">
                ${avBox}
                <div class="flex-1 min-w-0">
                  <button type="button" data-msg-user="${m.senderUid || ""}" class="text-xs font-bold text-pink-300 hover:underline">${m.from || "משתמש"}</button>
                  ${body}
                </div>
              </div>`;
            }).join("")
          : `<p class="text-xs text-slate-400">אין עדיין הודעות בחדר הזה.</p>`;
        document.querySelectorAll("[data-msg-user]").forEach((el) => { el.onclick = () => { const uid = el.dataset.msgUser; if (!uid) return; if (uid === me.uid) openUserModal(me); else { const f = allUsers.find((x) => (x.uid || x.id) === uid); if (f) openUserModal(f); } }; });
      });
    }

    function renderRooms() {
      $("rooms-list").innerHTML = chatRooms.map((r) => {
        const count = (r.members || []).length, isJoined = joinedRoomId === r.id, isPriv = Boolean(r.code);
        return `<div class="p-3 rounded-xl border text-xs flex items-center justify-between gap-2 ${isJoined ? "bg-pink-600/25 border-pink-400" : "bg-slate-950/75 border-slate-800"}">
          <div class="min-w-0">
            <div class="font-bold truncate">${isPriv ? "🔒" : "💬"} ${r.topic}</div>
            <div class="text-[11px] text-slate-400">${count}/${MAX_ROOM_USERS} משתתפים ${isPriv ? "• חדר פרטי" : ""}</div>
          </div>
          <button type="button" data-enter-room="${r.id}" class="px-3 py-1.5 rounded-lg text-xs font-bold shrink-0 ${isJoined ? "bg-emerald-600" : "bg-pink-600 hover:bg-pink-500"}">${isJoined ? "בתוך החדר" : "כנס לחדר"}</button>
        </div>`;
      }).join("");

      document.querySelectorAll("[data-enter-room]").forEach((btn) => {
        btn.onclick = () => {
          const target = chatRooms.find((r) => r.id === btn.dataset.enterRoom); if (!target) return;
          if (target.code && !(target.members || []).includes(me.uid)) {
            const entered = prompt("זהו חדר פרטי. הזן את קוד החדר:") || "";
            if (entered.trim() !== target.code) { alert("קוד החדר שגוי."); return; }
          }
          target.members = target.members || [];
          if (!target.members.includes(me.uid)) {
            if (target.members.length >= MAX_ROOM_USERS) { alert(`החדר מלא (מקסימום ${MAX_ROOM_USERS} משתתפים).`); return; }
            target.members.push(me.uid);
          }
          activeRoomId = target.id; joinedRoomId = target.id; renderRooms();
        };
      });

      const cur = chatRooms.find((r) => r.id === activeRoomId) || chatRooms[0], isHere = joinedRoomId === cur.id;
      $("active-room-title").textContent = cur.topic;
      $("active-room-meta").textContent = isHere ? `מחובר לחדר (${(cur.members || []).length}/${MAX_ROOM_USERS})` : 'לחץ "כנס לחדר" כדי להצטרף';
      $("leave-room-btn").classList.toggle("hidden", !isHere);
      listenMsgs(cur.id);
    }

    $("leave-room-btn").onclick = () => {
      const cur = chatRooms.find((r) => r.id === activeRoomId);
      if (cur && Array.isArray(cur.members)) cur.members = cur.members.filter((id) => id !== me.uid);
      joinedRoomId = null; renderRooms();
    };

    $("invite-friend-btn").onclick = async () => {
      const cur = chatRooms.find((r) => r.id === activeRoomId); if (!cur) return;
      const friendName = prompt("הזן שם של חבר/ה להזמנה לחדר:") || ""; if (!friendName.trim()) return;
      await addDoc(collection(db, "rooms", cur.id, "messages"), { senderUid: me.uid, from: me.name || "משתמש", avatar: me.avatar || "", text: `📨 ${me.name || "משתמש"} הזמין/ה את ${friendName.trim()} לחדר "${cur.topic}"!`, createdAt: serverTimestamp() });
    };

    $("create-room-form").onsubmit = async (e) => {
      e.preventDefault();
      const topic = $("new-room-topic").value.trim(), code = $("new-room-code").value.trim(); if (!topic) return;
      const room = { id: `r-${Date.now()}`, topic, code, members: [me.uid] };
      chatRooms.unshift(room); activeRoomId = room.id; joinedRoomId = room.id; $("new-room-topic").value = ""; $("new-room-code").value = "";
      try { await setDoc(doc(db, "rooms", room.id), { id: room.id, topic: room.topic, createdAt: serverTimestamp() }, { merge: true }); } catch {}
      renderRooms();
    };

    $("chat-form").onsubmit = async (e) => {
      e.preventDefault();
      if (joinedRoomId !== activeRoomId) { alert('לחץ קודם על "כנס לחדר".'); return; }
      const txt = $("chat-input").value.trim(); if (!txt) return;
      $("chat-input").value = "";
      await addDoc(collection(db, "rooms", activeRoomId, "messages"), { senderUid: me.uid, from: me.name || "משתמש", avatar: me.avatar || "", text: txt, createdAt: serverTimestamp() });
    };

    let mediaRecorder = null, audioChunks = [];
    async function toggleAudioRecord(onReadyAudioUrl, statusEl, btnEl) {
      if (mediaRecorder && mediaRecorder.state === "recording") {
        mediaRecorder.stop();
        if (btnEl) { btnEl.textContent = "🎤 הקלט"; btnEl.classList.replace("bg-rose-600", "bg-amber-600"); }
        if (statusEl) statusEl.textContent = "שולח הקלטה...";
        return;
      }
      if (!navigator.mediaDevices?.getUserMedia) { if (statusEl) statusEl.textContent = "הדפדפן לא תומך בהקלטה קולית."; return; }
      try {
        const stream = await navigator.mediaDevices.getUserMedia({ audio: true });
        audioChunks = []; mediaRecorder = new MediaRecorder(stream);
        mediaRecorder.ondataavailable = (ev) => { if (ev.data.size > 0) audioChunks.push(ev.data); };
        mediaRecorder.onstop = () => {
          stream.getTracks().forEach((t) => t.stop());
          const rd = new FileReader();
          rd.onloadend = async () => {
            await onReadyAudioUrl(String(rd.result));
            if (statusEl) statusEl.textContent = "ההקלטה נשלחה!";
          };
          rd.readAsDataURL(new Blob(audioChunks, { type: "audio/webm" }));
        };
        mediaRecorder.start();
        if (btnEl) { btnEl.textContent = "⏹️ עצור"; btnEl.classList.replace("bg-amber-600", "bg-rose-600"); }
        if (statusEl) statusEl.textContent = "מקליט כעת...";
      } catch { if (statusEl) statusEl.textContent = "לא ניתנה הרשאה למיקרופון."; }
    }

    $("record-voice-btn").onclick = async () => {
      if (joinedRoomId !== activeRoomId) { alert('לחץ קודם על "כנס לחדר".'); return; }
      await toggleAudioRecord(async (url) => {
        await addDoc(collection(db, "rooms", activeRoomId, "messages"), { senderUid: me.uid, from: me.name || "משתמש", avatar: me.avatar || "", audioData: url, createdAt: serverTimestamp() });
      }, $("voice-status"), $("record-voice-btn"));
    };

    function renderRoomChatLog(elId, messages) {
      $(elId).innerHTML = messages.length
        ? messages.map((m) => {
            const content = m.audioData ? `<audio controls src="${m.audioData}" class="w-full h-7 mt-1"></audio>` : `<span class="text-slate-200">${m.text || ""}</span>`;
            return `<div class="px-2.5 py-1.5 rounded-lg bg-slate-950/90 border border-slate-800"><span class="font-bold text-pink-300">${m.from}:</span> ${content}</div>`;
          }).join("")
        : `<p class="text-slate-400">אין עדיין הודעות בשולחן.</p>`;
    }const timerIntervals = {};
    function startCountdown(key, seconds, elId, onExpire) {
      if (timerIntervals[key]) clearInterval(timerIntervals[key]);
      let rem = seconds;
      const paint = () => { const m = String(Math.floor(rem / 60)).padStart(2, "0"), s = String(rem % 60).padStart(2, "0"); if ($(elId)) $(elId).textContent = `⏱️ ${m}:${s}`; };
      paint();
      timerIntervals[key] = setInterval(() => { rem -= 1; if (rem <= 0) { clearInterval(timerIntervals[key]); if ($(elId)) $(elId).textContent = "⏱️ 00:00"; if (onExpire) onExpire(); } else paint(); }, 1000);
    }

    document.querySelectorAll(".game-tab-btn").forEach((btn) => {
      btn.onclick = () => {
        const g = btn.dataset.game;
        document.querySelectorAll(".game-tab-btn").forEach((b) => { b.className = b.dataset.game === g ? "game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold bg-pink-600" : "game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold glass text-slate-300"; });
        document.querySelectorAll(".game-panel").forEach((p) => p.classList.add("hidden"));
        $(`game-${g}`).classList.remove("hidden");
        renderGameStatsAndTop5(g);
        if (g === "ttt") startCountdown("ttt", 30, "ttt-timer");
        if (g === "rps") startCountdown("rps", 15, "rps-timer");
        if (g === "memory") startCountdown("memory", 180, "memory-timer");
        if (g === "roulette") renderRrTable();
      };
    });

    const tttRooms = Array.from({ length: 100 }, (_, i) => ({
      id: `ttt-room-${i + 1}`, num: i + 1, p1: null, p1Sym: "X", p2: null, p2Sym: "O",
      board: Array(9).fill(""), turn: "X", scored: false, chat: []
    }));
    let selectedTttRoomId = tttRooms[0].id, joinedTttRoomId = null;

    function syncTttSymbolButtons() {
      const r = tttRooms.find((x) => x.id === selectedTttRoomId), sym = r?.p1Sym || "X";
      $("ttt-pick-x").className = sym === "X" ? "px-3 py-1 rounded-lg bg-amber-600 font-bold" : "px-3 py-1 rounded-lg bg-slate-800 border border-slate-600 font-bold";
      $("ttt-pick-o").className = sym === "O" ? "px-3 py-1 rounded-lg bg-amber-600 font-bold" : "px-3 py-1 rounded-lg bg-slate-800 border border-slate-600 font-bold";
    }

    $("ttt-pick-x").onclick = () => { const r = tttRooms.find((x) => x.id === selectedTttRoomId); if (!r || r.p2) return; r.p1Sym = "X"; r.p2Sym = "O"; syncTttSymbolButtons(); renderTttBoard(); };
    $("ttt-pick-o").onclick = () => { const r = tttRooms.find((x) => x.id === selectedTttRoomId); if (!r || r.p2) return; r.p1Sym = "O"; r.p2Sym = "X"; syncTttSymbolButtons(); renderTttBoard(); };

    function renderTttRooms() {
      $("ttt-rooms-grid").innerHTML = tttRooms.map((r) => {
        const count = (r.p1 ? 1 : 0) + (r.p2 ? 1 : 0), isSel = r.id === selectedTttRoomId, isIn = r.id === joinedTttRoomId;
        const statusTxt = count === 0 ? "שולחן פנוי" : count === 1 ? "1/2 ממתין" : "2/2 מלא";
        return `<button type="button" data-ttt-room="${r.id}" class="text-right p-2 rounded-xl border text-[11px] transition ${isIn ? "bg-emerald-600/25 border-emerald-400" : isSel ? "bg-pink-600/30 border-pink-400" : "bg-slate-900/80 border-slate-700"}"><div class="font-bold">שולחן #${r.num}</div><div class="text-slate-300 truncate">${statusTxt}</div></button>`;
      }).join("");
      document.querySelectorAll("[data-ttt-room]").forEach((b) => { b.onclick = () => { selectedTttRoomId = b.dataset.tttRoom; syncTttSymbolButtons(); renderTttRooms(); renderTttBoard(); }; });
    }

    $("ttt-join-room").onclick = () => {
      const r = tttRooms.find((x) => x.id === selectedTttRoomId); if (!r) return;
      const myLabel = me.name || "שחקן";
      if (r.p1 !== myLabel && r.p2 !== myLabel) {
        if (!r.p1) r.p1 = myLabel;
        else if (!r.p2) { r.p2 = myLabel; r.p2Sym = r.p1Sym === "X" ? "O" : "X"; }
        else { alert("השולחן מלא (2/2 שחקנים)."); return; }
      }
      joinedTttRoomId = r.id; $("ttt-leave-room").classList.remove("hidden"); startCountdown("ttt", 30, "ttt-timer"); renderTttRooms(); renderTttBoard();
    };

    $("ttt-leave-room").onclick = () => {
      const r = tttRooms.find((x) => x.id === joinedTttRoomId); if (!r) return;
      const myLabel = me.name || "שחקן";
      if (r.p1 === myLabel) r.p1 = null; if (r.p2 === myLabel) r.p2 = null;
      joinedTttRoomId = null; $("ttt-leave-room").classList.add("hidden");
      if (!r.p1 && !r.p2) { r.board = Array(9).fill(""); r.p1Sym = "X"; r.p2Sym = "O"; r.turn = "X"; r.scored = false; r.chat = []; }
      renderTttRooms(); renderTttBoard();
    };

    $("ttt-add-room").onclick = () => { const n = tttRooms.length + 1; tttRooms.push({ id: `ttt-room-${n}`, num: n, p1: null, p1Sym: "X", p2: null, p2Sym: "O", board: Array(9).fill(""), turn: "X", scored: false, chat: [] }); renderTttRooms(); };

    function checkTttWin(b) {
      const lines = [[0,1,2],[3,4,5],[6,7,8],[0,3,6],[1,4,7],[2,5,8],[0,4,8],[2,4,6]];
      for (const [a, c, d] of lines) if (b[a] && b[a] === b[c] && b[a] === b[d]) return b[a];
      return b.every(Boolean) ? "DRAW" : null;
    }

    function renderTttBoard() {
      const r = tttRooms.find((x) => x.id === selectedTttRoomId) || tttRooms[0], board = r.board;
      $("ttt-p1-sym-icon").textContent = r.p1Sym === "X" ? "❌" : "⭕"; $("ttt-p2-sym-icon").textContent = r.p2Sym === "X" ? "❌" : "⭕";
      $("ttt-p1-name").textContent = r.p1 ? `${r.p1} (${r.p1Sym === "X" ? "❌" : "⭕"})` : "מושב 1 פנוי";
      $("ttt-p2-name").textContent = r.p2 ? `${r.p2} (${r.p2Sym === "X" ? "❌" : "⭕"})` : "ממתין לכניסה...";
      renderRoomChatLog("ttt-room-chat-log", r.chat || []);
      const el = $("ttt-board"); el.innerHTML = "";
      const win = checkTttWin(board), canMove = Boolean(joinedTttRoomId === r.id && r.p1 && r.p2 && !win);
      board.forEach((cell, idx) => {
        const btn = document.createElement("button"); btn.type = "button"; btn.disabled = !canMove || Boolean(cell);
        btn.className = "aspect-square rounded-lg bg-amber-900/90 border border-amber-500/40 text-lg font-bold flex items-center justify-center disabled:opacity-60";
        btn.textContent = cell === "X" ? "❌" : cell === "O" ? "⭕" : "";
        btn.onclick = async () => {
          if (!canMove || board[idx]) return;
          board[idx] = r.turn;
          const res = checkTttWin(board);
          if (res && !r.scored) {
            r.scored = true; const myLabel = me.name || "שחקן", winnerName = res === r.p1Sym ? r.p1 : r.p2;
            if (res === "X" || res === "O") { if (winnerName === myLabel) await awardGameWin("ttt", 25); else await awardGameLoss("ttt", 5); }
          }
          r.turn = r.turn === "X" ? "O" : "X"; startCountdown("ttt", 30, "ttt-timer"); renderTttBoard(); renderTttRooms();
        };
        el.appendChild(btn);
      });
      if (!r.p1 && !r.p2) $("ttt-status").textContent = `שולחן #${r.num} פנוי — בחר סמל ולחץ "כנס לשולחן"`;
      else if (!r.p1 || !r.p2) $("ttt-status").textContent = `שולחן #${r.num} — ממתין לשחקן נוסף שיצטרף מולך`;
      else if (win === "DRAW") $("ttt-status").textContent = `תיקו בשולחן #${r.num}!`;
      else if (win) $("ttt-status").textContent = `המנצח בשולחן #${r.num}: ${win === r.p1Sym ? r.p1 : r.p2} 🎉`;
      else $("ttt-status").textContent = `שולחן #${r.num} • תור ${r.turn === r.p1Sym ? r.p1 : r.p2}`;
    }

    $("ttt-room-chat-form").onsubmit = (e) => {
      e.preventDefault(); const r = tttRooms.find((x) => x.id === selectedTttRoomId); if (!r) return;
      const txt = $("ttt-room-chat-input").value.trim(); if (!txt) return;
      r.chat.push({ from: me.name || "שחקן", text: txt }); $("ttt-room-chat-input").value = ""; renderRoomChatLog("ttt-room-chat-log", r.chat);
    };

    $("ttt-reset").onclick = () => { const r = tttRooms.find((x) => x.id === selectedTttRoomId); if (!r) return; r.board = Array(9).fill(""); r.turn = r.p1Sym; r.scored = false; startCountdown("ttt", 30, "ttt-timer"); renderTttBoard(); };
    syncTttSymbolButtons(); renderTttRooms(); renderTttBoard();const rpsRooms = Array.from({ length: 100 }, (_, i) => ({ id: `rps-room-${i + 1}`, num: i + 1, p1: null, p2: null, chat: [] }));
    let selectedRpsRoomId = rpsRooms[0].id, joinedRpsRoomId = null, rpsBusy = false;

    function renderRpsRooms() {
      $("rps-rooms-grid").innerHTML = rpsRooms.map((r) => {
        const count = (r.p1 ? 1 : 0) + (r.p2 ? 1 : 0), isSel = r.id === selectedRpsRoomId, isIn = r.id === joinedRpsRoomId;
        const label = count === 0 ? "שולחן פנוי" : count === 1 ? "1/2 ממתין" : "2/2 מלא";
        return `<button type="button" data-rps-room="${r.id}" class="text-right p-2 rounded-xl border text-[11px] transition ${isIn ? "bg-emerald-600/25 border-emerald-400" : isSel ? "bg-pink-600/30 border-pink-400" : "bg-slate-900/80 border-slate-700"}"><div class="font-bold">שולחן #${r.num}</div><div class="text-slate-300 truncate">${label}</div></button>`;
      }).join("");
      document.querySelectorAll("[data-rps-room]").forEach((b) => { b.onclick = () => { selectedRpsRoomId = b.dataset.rpsRoom; renderRpsRooms(); syncRpsRoomUI(); }; });
    }

    $("rps-join-room").onclick = () => {
      const r = rpsRooms.find((x) => x.id === selectedRpsRoomId); if (!r) return;
      const myLabel = me.name || "שחקן";
      if (r.p1 !== myLabel && r.p2 !== myLabel) { if (!r.p1) r.p1 = myLabel; else if (!r.p2) r.p2 = myLabel; else { alert("השולחן מלא (2/2 שחקנים)."); return; } }
      joinedRpsRoomId = r.id; $("rps-leave-room").classList.remove("hidden"); startCountdown("rps", 15, "rps-timer"); renderRpsRooms(); syncRpsRoomUI();
    };

    $("rps-leave-room").onclick = () => {
      const r = rpsRooms.find((x) => x.id === joinedRpsRoomId); if (!r) return;
      const myLabel = me.name || "שחקן";
      if (r.p1 === myLabel) r.p1 = null; if (r.p2 === myLabel) r.p2 = null;
      joinedRpsRoomId = null; $("rps-leave-room").classList.add("hidden");
      if (!r.p1 && !r.p2) r.chat = [];
      renderRpsRooms(); syncRpsRoomUI();
    };

    $("rps-add-room").onclick = () => { const n = rpsRooms.length + 1; rpsRooms.push({ id: `rps-room-${n}`, num: n, p1: null, p2: null, chat: [] }); renderRpsRooms(); };

    function syncRpsRoomUI() {
      const r = rpsRooms.find((x) => x.id === selectedRpsRoomId) || rpsRooms[0];
      $("rps-left-name").textContent = r.p1 || "מושב 1 פנוי"; $("rps-right-name").textContent = r.p2 || "מושב 2 פנוי";
      $("rps-left-avatar").textContent = r.p1 ? "🧑" : "🪑"; $("rps-right-avatar").textContent = r.p2 ? "🧑" : "🪑";
      renderRoomChatLog("rps-room-chat-log", r.chat || []);
      const ready = Boolean(joinedRpsRoomId === r.id && r.p1 && r.p2);
      document.querySelectorAll(".rps-choice").forEach((b) => { b.disabled = !ready || rpsBusy; b.classList.toggle("opacity-50", !ready || rpsBusy); });
      if (!r.p1 && !r.p2) $("rps-round-phase").textContent = `שולחן #${r.num} פנוי — לחץ "כנס לשולחן"`;
      else if (!r.p1 || !r.p2) $("rps-round-phase").textContent = `שולחן #${r.num} — ממתין לשחקן נוסף`;
      else $("rps-round-phase").textContent = `שולחן #${r.num} מוכן!`;
    }

    $("rps-room-chat-form").onsubmit = (e) => {
      e.preventDefault(); const r = rpsRooms.find((x) => x.id === selectedRpsRoomId); if (!r) return;
      const txt = $("rps-room-chat-input").value.trim(); if (!txt) return;
      r.chat.push({ from: me.name || "שחקן", text: txt }); $("rps-room-chat-input").value = ""; renderRoomChatLog("rps-room-chat-log", r.chat);
    };

    document.querySelectorAll(".rps-choice").forEach((btn) => {
      btn.onclick = async () => {
        const r = rpsRooms.find((x) => x.id === joinedRpsRoomId); if (!r || !r.p1 || !r.p2 || rpsBusy) return;
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
              msg = `${r.p1} ניצח/ה! 🎉`; if (r.p1 === (me.name || "שחקן")) await awardGameWin("rps", 20);
            } else if (p1Choice !== p2Choice) {
              msg = `${r.p2} ניצח/ה! 🎉`; if (r.p1 === (me.name || "שחקן")) await awardGameLoss("rps", 5);
            }
            $("rps-result").textContent = `${labels[p1Choice]} מול ${labels[p2Choice]} — ${msg}`;
            rpsBusy = false; syncRpsRoomUI();
          }
        }, 420);
      };
    });
    renderRpsRooms(); syncRpsRoomUI();

    const memRooms = [
      { id: "mr-1", title: "זיכרון 8×8 #1", mode: "8x8", players: [], turnIdx: 0, chat: [] },
      { id: "mr-2", title: "זיכרון 10×10 #2", mode: "10x10", players: [], turnIdx: 0, chat: [] },
      { id: "mr-3", title: "זיכרון 30×30 #3", mode: "30x30", players: [], turnIdx: 0, chat: [] },
      { id: "mr-4", title: "זיכרון 8×8 #4", mode: "8x8", players: [], turnIdx: 0, chat: [] }
    ];
    let selectedMemRoomId = memRooms[0].id, joinedMemRoomId = null, currentMemMode = "8x8";
    const bigEmojiBank = [
      "🐶","🐱","🐭","🐹","🐰","🦊","🐻","🐼","🐨","🐯","🦁","🐮","🐷","🐸","🐵","🐔",
      "🐧","🐦","🦅","🦆","🦉","🦇","🐺","🐗","🐴","🦄","🐝","🐛","🦋","🐌","🐞","🐢",
      "🐍","🐙","🦑","🦐","🦀","🐡","🐠","🐟","🐬","🐳","🦈","🐊","🐅","🐆","🦓","🦍",
      "🍎","🍐","🍊","🍋","🍌","🍉","🍇","🍓","🫐","🍈","🍒","🍑","🥭","🍍","🥥","🥝",
      "🍅","🥑","🥦","🥬","🥒","🌶️","🌽","🥕","🧄","🧅","🥔","🥐","🍞","🥖","🥨","🧀",
      "🍕","🍔","🍟","🌭","🍿","🥞","🧇","🥓","🍗","🍣","🍤","🍩","🍪","🎂","🍰","🧁",
      "⚽","🏀","🏈","⚾","🎾","🏐","🏉","🎱","🏓","🏸","🥅","🥊","🥋","⛳","🏹","🎣",
      "🚗","🚕","🚙","🚌","🏎️","🚓","🚑","🚒","🚜","🏍️","🛵","🚲","🛴","✈️","🚀","🛸",
      "🎸","🎹","🥁","🎷","🎺","🎻","🎤","🎧","🎬","🎮","🎲","🎯","🎳","♟️","🧩","🧸",
      "☀️","🌙","⭐","🌟","⚡","🔥","💧","🌈","❄️","🌸","🌻","🌹","🌷","🍀","🌵","🌴"
    ];
    let memCards = [], memFlipped = [], memMatched = new Set();

    function buildMemoryBoard(mode = "8x8") {
      currentMemMode = mode;
      const cols = mode === "30x30" ? 30 : mode === "10x10" ? 10 : 8;
      const totalCells = cols * cols, pairsCount = totalCells / 2;
      const chosen = [];
      for (let i = 0; i < pairsCount; i++) chosen.push(bigEmojiBank[i % bigEmojiBank.length]);
      memCards = [...chosen, ...chosen].sort(() => Math.random() - 0.5);
      memFlipped = []; memMatched = new Set();
      $("memory-grid").style.gridTemplateColumns = `repeat(${cols}, minmax(0, 1fr))`;
      $("memory-grid").style.minWidth = mode === "30x30" ? "1180px" : mode === "10x10" ? "580px" : "480px";
      startCountdown("memory", mode === "30x30" ? 600 : mode === "10x10" ? 300 : 180, "memory-timer", () => { $("memory-status").textContent = "הזמן נגמר! לחץ 'ערבב לוח'."; });
      renderMemoryGrid();
    }

    function renderMemRooms() {
      $("memory-rooms-grid").innerHTML = memRooms.map((r) => `<button type="button" data-mem-room="${r.id}" class="text-right p-2.5 rounded-xl border text-xs transition ${r.id === joinedMemRoomId ? "bg-emerald-600/25 border-emerald-400" : r.id === selectedMemRoomId ? "bg-pink-600/30 border-pink-400" : "bg-slate-900/80 border-slate-700"}"><div class="font-bold truncate">💎 ${r.title}</div><div class="text-[11px] text-slate-300">${r.mode} • ${r.players.length}/6 מושבים</div></button>`).join("");
      document.querySelectorAll("[data-mem-room]").forEach((b) => { b.onclick = () => { selectedMemRoomId = b.dataset.memRoom; const r = memRooms.find((x) => x.id === selectedMemRoomId); if (!r) return; buildMemoryBoard(r.mode); renderMemRooms(); renderMemPlayersBoard(); }; });
    }

    $("memory-join-room").onclick = () => {
      const r = memRooms.find((x) => x.id === selectedMemRoomId); if (!r) return;
      const myLabel = me.name || "שחקן";
      if (!r.players.some((p) => p.name === myLabel)) { if (r.players.length >= 6) { alert("כל 6 המושבים תפוסים."); return; } r.players.push({ name: myLabel, score: 0 }); }
      joinedMemRoomId = r.id; $("memory-leave-room").classList.remove("hidden"); buildMemoryBoard(r.mode); renderMemRooms(); renderMemPlayersBoard();
    };

    $("memory-leave-room").onclick = () => {
      const r = memRooms.find((x) => x.id === joinedMemRoomId); if (!r) return;
      const myLabel = me.name || "שחקן";
      r.players = r.players.filter((p) => p.name !== myLabel);
      joinedMemRoomId = null; $("memory-leave-room").classList.add("hidden");
      if (r.players.length === 0) { r.turnIdx = 0; r.chat = []; buildMemoryBoard(r.mode); }
      renderMemRooms(); renderMemPlayersBoard();
    };

    $("mem-create-room-form").onsubmit = (e) => {
      e.preventDefault(); const title = $("mem-room-name").value.trim(), mode = $("mem-room-mode").value; if (!title) return;
      const nr = { id: `mr-${Date.now()}`, title, mode, players: [{ name: me.name || "שחקן", score: 0 }], turnIdx: 0, chat: [] };
      memRooms.unshift(nr); selectedMemRoomId = nr.id; joinedMemRoomId = nr.id; $("mem-room-name").value = ""; $("memory-leave-room").classList.remove("hidden");
      buildMemoryBoard(mode); renderMemRooms(); renderMemPlayersBoard();
    };

    $("mem-room-chat-form").onsubmit = (e) => {
      e.preventDefault(); const r = memRooms.find((x) => x.id === selectedMemRoomId); if (!r) return;
      const txt = $("mem-room-chat-input").value.trim(); if (!txt) return;
      r.chat.push({ from: me.name || "שחקן", text: txt }); $("mem-room-chat-input").value = ""; renderRoomChatLog("mem-room-chat-log", r.chat);
    };

    function renderMemPlayersBoard() {
      const r = memRooms.find((x) => x.id === selectedMemRoomId) || memRooms[0];
      renderRoomChatLog("mem-room-chat-log", r.chat || []);
      $("memory-players-board").innerHTML = Array.from({ length: 6 }, (_, idx) => {
        const p = r.players[idx] || null, isTurn = r.players.length > 0 && (r.turnIdx % r.players.length) === idx && p;
        return `<div class="p-2 rounded-lg border ${isTurn ? "bg-pink-600/25 border-pink-400" : "bg-slate-900 border-slate-800"}"><div class="font-bold truncate">${p ? `מושב ${idx + 1}: ${p.name}` : `מושב ${idx + 1} פנוי`}</div><div class="text-amber-300">${p ? `${p.score} נק׳ ${isTurn ? "• תורו" : ""}` : "פנוי"}</div></div>`;
      }).join("");
    }

    function renderMemoryGrid() {
      const g = $("memory-grid"); g.innerHTML = "";
      const emojiSizeClass = currentMemMode === "30x30" ? "text-xl" : currentMemMode === "10x10" ? "text-2xl" : "text-3xl";
      memCards.forEach((sym, i) => {
        const show = memFlipped.includes(i) || memMatched.has(i), btn = document.createElement("button");
        btn.type = "button";
        btn.className = `aspect-square rounded-xl bg-slate-900 border border-slate-700 ${emojiSizeClass} flex items-center justify-center hover:border-pink-400 select-none`;
        btn.textContent = show ? sym : "❓";
        btn.onclick = async () => {
          if (show || memFlipped.length === 2) return;
          memFlipped.push(i); renderMemoryGrid();
          if (memFlipped.length === 2) {
            const [a, b] = memFlipped, r = memRooms.find((x) => x.id === joinedMemRoomId);
            if (memCards[a] === memCards[b]) {
              memMatched.add(a); memMatched.add(b); memFlipped = [];
              if (r && r.players.length) { const curP = r.players[r.turnIdx % r.players.length]; curP.score += 10; if (curP.name === (me.name || "שחקן")) await awardGameWin("memory", 10); }
              if (memMatched.size === memCards.length) $("memory-status").textContent = "כל הזוגות נמצאו! 🎉";
              renderMemPlayersBoard(); renderMemoryGrid();
            } else {
              setTimeout(() => { memFlipped = []; if (r && r.players.length) r.turnIdx = (r.turnIdx + 1) % r.players.length; renderMemPlayersBoard(); renderMemoryGrid(); }, 650);
            }
          }
        };
        g.appendChild(btn);
      });
      const r = memRooms.find((x) => x.id === selectedMemRoomId) || memRooms[0];
      const activePlayer = r.players.length ? r.players[r.turnIdx % r.players.length]?.name : "";
      $("memory-status").textContent = `${r.title} (${r.mode}) • ${r.players.length}/6 מושבים ${activePlayer ? `• תור: ${activePlayer}` : ""}`;
    }

    $("memory-reset").onclick = () => buildMemoryBoard(currentMemMode);
    renderMemRooms(); renderMemPlayersBoard(); buildMemoryBoard("8x8");let numRooms = [
      { id: "nr-1", name: "חדר ניחוש #1 (1–1,000)", maxNum: 1000, secret: null, players: [], guesses: [], chat: [] },
      { id: "nr-2", name: "חדר ניחוש #2 (1–1,000)", maxNum: 1000, secret: null, players: [], guesses: [], chat: [] },
      { id: "nr-3", name: "אתגר 1–1,500", maxNum: 1500, secret: null, players: [], guesses: [], chat: [] }
    ];
    let selectedNumRoomId = numRooms[0].id, joinedNumRoomId = null;

    function renderNumRooms() {
      $("num-rooms-list").innerHTML = numRooms.map((r) => `<button type="button" data-num-room="${r.id}" class="text-right p-3 rounded-xl border text-xs ${r.id === joinedNumRoomId ? "bg-emerald-600/25 border-emerald-400" : r.id === selectedNumRoomId ? "bg-pink-600/30 border-pink-400" : "bg-slate-900/80 border-slate-700"}"><div class="font-bold">🎯 ${r.name}</div><div class="text-slate-300 mt-0.5">1–${r.maxNum.toLocaleString()} • ${(r.players || []).length}/50</div></button>`).join("");
      document.querySelectorAll("[data-num-room]").forEach((b) => { b.onclick = () => { selectedNumRoomId = b.dataset.numRoom; renderNumRooms(); renderActiveNumRoom(); }; });
    }

    $("num-join-room").onclick = () => {
      const r = numRooms.find((x) => x.id === selectedNumRoomId); if (!r) return;
      const myLabel = me.name || "שחקן";
      if (!r.players.includes(myLabel)) { if (r.players.length >= 50) { alert("החדר מלא (מקסימום 50 משתתפים)."); return; } r.players.push(myLabel); }
      joinedNumRoomId = r.id; $("num-leave-room").classList.remove("hidden"); renderNumRooms(); renderActiveNumRoom();
    };

    $("num-leave-room").onclick = () => {
      const r = numRooms.find((x) => x.id === joinedNumRoomId); if (!r) return;
      const myLabel = me.name || "שחקן";
      r.players = r.players.filter((p) => p !== myLabel);
      joinedNumRoomId = null; $("num-leave-room").classList.add("hidden");
      if (r.players.length === 0) { r.secret = null; r.guesses = []; r.chat = []; }
      renderNumRooms(); renderActiveNumRoom();
    };

    $("num-room-chat-form").onsubmit = (e) => {
      e.preventDefault(); const r = numRooms.find((x) => x.id === selectedNumRoomId); if (!r) return;
      const txt = $("num-room-chat-input").value.trim(); if (!txt) return;
      r.chat.push({ from: me.name || "שחקן", text: txt }); $("num-room-chat-input").value = ""; renderRoomChatLog("num-room-chat-log", r.chat);
    };

    function renderActiveNumRoom() {
      const r = numRooms.find((x) => x.id === selectedNumRoomId) || numRooms[0]; r.players = r.players || [];
      $("num-room-header").textContent = `${r.name} (1 עד ${r.maxNum.toLocaleString()})`; $("num-room-cap").textContent = `${r.players.length} / 50 משתתפים`;
      $("num-guess-input").min = 1; $("num-guess-input").max = r.maxNum; $("num-secret-input").value = r.secret !== null ? String(r.secret) : "";
      $("num-secret-status").textContent = r.secret !== null ? "✓ מספר סודי נקבע בשקט! המשתתפים יכולים לשלוח ניחושים." : "טרם נקבע מספר סודי — הזן מספר בשקט או לחץ 'קבע מספר סודי'.";
      renderRoomChatLog("num-room-chat-log", r.chat || []);
      $("num-guesses-log").innerHTML = r.guesses.map((g) => `<div class="px-3 py-1.5 rounded-lg bg-slate-900 border border-slate-800 flex justify-between"><span><strong>${g.player}</strong> ניחש <strong>${g.value}</strong></span><span class="text-indigo-200">מרחק: ${g.diff} ${g.awarded ? `(+${g.awarded} נק׳)` : ""}</span></div>`).join("");
    }

    $("num-create-room-form").onsubmit = (e) => {
      e.preventDefault(); const name = $("num-room-name").value.trim(), maxNum = Math.max(10, Number($("num-room-max").value) || 1000); if (!name) return;
      const myLabel = me.name || "שחקן", nr = { id: `nr-${Date.now()}`, name, maxNum, secret: null, players: [myLabel], guesses: [], chat: [] };
      numRooms.unshift(nr); selectedNumRoomId = nr.id; joinedNumRoomId = nr.id; $("num-room-name").value = ""; $("num-leave-room").classList.remove("hidden"); renderNumRooms(); renderActiveNumRoom();
    };

    $("num-toggle-secret").onclick = () => { $("num-secret-input").type = $("num-secret-input").type === "password" ? "number" : "password"; };
    $("num-set-secret-btn").onclick = () => {
      const r = numRooms.find((x) => x.id === selectedNumRoomId) || numRooms[0], typed = Number($("num-secret-input").value);
      r.secret = (typed >= 1 && typed <= r.maxNum) ? typed : Math.floor(Math.random() * r.maxNum) + 1;
      r.guesses = []; $("num-guess-feedback").textContent = "מספר סודי נקבע בשקט! אפשר לשלוח ניחושים."; renderActiveNumRoom();
    };

    $("num-guess-btn").onclick = () => {
      const r = numRooms.find((x) => x.id === selectedNumRoomId) || numRooms[0];
      if (r.secret === null) r.secret = Math.floor(Math.random() * r.maxNum) + 1;
      const val = Number($("num-guess-input").value);
      if (!val || val < 1 || val > r.maxNum) { $("num-guess-feedback").textContent = `הכנס מספר בין 1 ל-${r.maxNum.toLocaleString()}.`; return; }
      const myLabel = me.name || "שחקן";
      if (!r.players.includes(myLabel) && r.players.length < 50) r.players.push(myLabel);
      r.guesses.unshift({ player: myLabel, value: val, diff: Math.abs(val - r.secret), awarded: 0 });
      $("num-guess-input").value = ""; $("num-guess-feedback").textContent = `הניחוש ${val} נרשם! לחץ "חשב נקודות לכולם".`;
      renderNumRooms(); renderActiveNumRoom();
    };

    $("num-declare-winner-btn").onclick = async () => {
      const r = numRooms.find((x) => x.id === selectedNumRoomId) || numRooms[0];
      if (r.secret === null || !r.guesses.length) { $("num-guess-feedback").textContent = "יש לקבוע מספר סודי ולוודא שנשלחו ניחושים."; return; }
      const uniqueDiffs = [...new Set(r.guesses.map((g) => g.diff))].sort((a, b) => a - b);
      const bestDiff = uniqueDiffs[0], secondDiff = uniqueDiffs[1];
      for (const g of r.guesses) {
        if (g.diff === bestDiff) g.awarded = bestDiff === 0 ? 5 : 3;
        else if (secondDiff !== undefined && g.diff === secondDiff) g.awarded = 2;
        else g.awarded = 1;
      }
      const myLabel = me.name || "שחקן", myGuesses = r.guesses.filter((g) => g.player === myLabel);
      if (myGuesses.length) { const myPts = Math.max(...myGuesses.map((g) => g.awarded)); if (myPts >= 3) await awardGameWin("number", myPts); else await awardGameLoss("number", myPts); }
      const topWinners = r.guesses.filter((g) => g.diff === bestDiff).map((g) => g.player);
      $("num-guess-feedback").textContent = `🏆 המספר הסודי היה ${r.secret}. הכי קרובים (מרחק ${bestDiff}): ${topWinners.join(", ")} — נקודות חולקו לכל המנחשים!`;
      renderActiveNumRoom();
    };

    renderNumRooms(); renderActiveNumRoom();

    const rrTable = {
      seats: Array.from({ length: 6 }, (_, i) => ({ seatNum: i + 1, name: null, alive: true })),
      chamberIndex: 0, bulletChamber: Math.floor(Math.random() * 6),
      aimedSeatIdx: 0, roundOver: false, chat: []
    };
    let joinedRr = false;

    function renderRrRewardsUI() {
      $("rr-gold-balls").textContent = String(me.rrRewards.goldBalls || 0);
      $("rr-magazines").textContent = String(me.rrRewards.magazines || 0);
      $("rr-pistols").textContent = String(me.rrRewards.pistols || 0);
      $("rr-grand-gifts").textContent = String(me.rrRewards.grandGifts || 0);
    }

    function renderRrTable() {
      renderRrRewardsUI();
      renderRoomChatLog("rr-room-chat-log", rrTable.chat || []);
      $("rr-seats-ring").innerHTML = rrTable.seats.map((s, idx) => {
        const isAimed = idx === rrTable.aimedSeatIdx;
        const badge = !s.name ? "מושב פנוי" : s.alive ? "💚 חי בסיבוב" : "🎊 נורה (קונפטי)";
        return `<div class="p-3 rounded-xl border text-xs ${isAimed ? "bg-amber-500/20 border-amber-400" : !s.alive ? "bg-rose-950/50 border-rose-700/50 opacity-70" : "bg-slate-900 border-slate-700"}">
          <div class="font-bold">מושב #${s.seatNum}: ${s.name || "ריק"}</div>
          <div class="text-[11px] mt-0.5">${badge}</div>
        </div>`;
      }).join("");
      $("rr-aimed-label").textContent = `האקדח מכוון למושב #${rrTable.aimedSeatIdx + 1} (${rrTable.seats[rrTable.aimedSeatIdx]?.name || "פנוי"})`;
    }

    $("rr-join-btn").onclick = () => {
      const myLabel = me.name || "שחקן", free = rrTable.seats.find((s) => !s.name);
      if (!rrTable.seats.some((s) => s.name === myLabel)) {
        if (!free) { alert("כל 6 המושבים בשולחן העגול תפוסים."); return; }
        free.name = myLabel; free.alive = true;
      }
      joinedRr = true; $("rr-leave-btn").classList.remove("hidden"); renderRrTable();
    };

    $("rr-leave-btn").onclick = () => {
      const myLabel = me.name || "שחקן";
      rrTable.seats.forEach((s) => { if (s.name === myLabel) { s.name = null; s.alive = true; } });
      joinedRr = false; $("rr-leave-btn").classList.add("hidden");
      if (rrTable.seats.every((s) => !s.name)) {
        rrTable.chamberIndex = 0; rrTable.bulletChamber = Math.floor(Math.random() * 6);
        rrTable.aimedSeatIdx = 0; rrTable.roundOver = false; rrTable.chat = [];
      }
      renderRrTable();
    };

    $("rr-spin-btn").onclick = () => {
      if (!joinedRr) { alert('לחץ קודם על "כנס לשולחן".'); return; }
      const aliveIndices = rrTable.seats.map((s, idx) => (s.name && s.alive ? idx : -1)).filter((i) => i >= 0);
      if (!aliveIndices.length) return;
      rrTable.aimedSeatIdx = aliveIndices[Math.floor(Math.random() * aliveIndices.length)];
      rrTable.chamberIndex = Math.floor(Math.random() * 6);
      $("rr-gun-spinner").style.transform = `rotate(${(rrTable.aimedSeatIdx + 1) * 60}deg)`;
      $("rr-confetti-banner").classList.add("hidden");
      $("rr-status").textContent = `האקדח הסתובב וכוון למושב #${rrTable.aimedSeatIdx + 1}!`;
      renderRrTable();
    };

    $("rr-pull-btn").onclick = async () => {
      if (!joinedRr || rrTable.roundOver) return;
      const seat = rrTable.seats[rrTable.aimedSeatIdx];
      if (!seat || !seat.name || !seat.alive) { $("rr-status").textContent = "בחר/סובב למושב פעיל שחי בסיבוב."; return; }

      const isShot = rrTable.chamberIndex === rrTable.bulletChamber;
      rrTable.chamberIndex = (rrTable.chamberIndex + 1) % 6;

      if (isShot) {
        seat.alive = false;
        $("rr-confetti-banner").classList.remove("hidden");
        $("rr-status").textContent = `🎉 בום קונפטי! האקדח ירה על ${seat.name} (מושב #${seat.seatNum}) — אינו ממשיך עד סוף הסיבוב!`;
        if (seat.name === (me.name || "שחקן")) await awardGameLoss("roulette", 5);
      } else {
        $("rr-confetti-banner").classList.add("hidden");
        $("rr-status").textContent = `😅 קליק! ${seat.name} (מושב #${seat.seatNum}) שרד את התא הזה!`;
      }

      const survivors = rrTable.seats.filter((s) => s.name && s.alive);
      if (survivors.length === 1) {
        rrTable.roundOver = true;
        const winner = survivors[0];
        $("rr-status").textContent = `🏆 ${winner.name} שרד/ה את כל הסיבוב וזכה/תה בכדור זהב!`;
        if (winner.name === (me.name || "שחקן")) {
          me.rrRewards.goldBalls += 1;
          if (me.rrRewards.goldBalls % 3 === 0) me.rrRewards.magazines += 1;
          if (me.rrRewards.magazines > 0 && me.rrRewards.magazines % 2 === 0) me.rrRewards.pistols += 1;
          if (me.rrRewards.pistols > 0 && me.rrRewards.pistols % 2 === 0) me.rrRewards.grandGifts += 1;
          await awardGameWin("roulette", 30);
        }
      }
      renderRrTable();
    };

    $("rr-new-round-btn").onclick = () => {
      rrTable.seats.forEach((s) => { if (s.name) s.alive = true; });
      rrTable.chamberIndex = 0; rrTable.bulletChamber = Math.floor(Math.random() * 6);
      rrTable.aimedSeatIdx = 0; rrTable.roundOver = false;
      $("rr-confetti-banner").classList.add("hidden");
      $("rr-status").textContent = "סיבוב חדש ברולטה הרוסית התחיל!";
      renderRrTable();
    };

    $("rr-room-chat-form").onsubmit = (e) => {
      e.preventDefault(); const txt = $("rr-room-chat-input").value.trim(); if (!txt) return;
      rrTable.chat.push({ from: me.name || "שחקן", text: txt }); $("rr-room-chat-input").value = ""; renderRoomChatLog("rr-room-chat-log", rrTable.chat);
    };

    document.querySelectorAll(".room-voice-btn").forEach((btn) => {
      btn.onclick = async () => {
        const target = btn.dataset.voiceTarget;
        await toggleAudioRecord(async (audioUrl) => {
          const sender = me.name || "שחקן";
          if (target === "ttt") { const r = tttRooms.find((x) => x.id === selectedTttRoomId); if (r) { r.chat.push({ from: sender, audioData: audioUrl }); renderRoomChatLog("ttt-room-chat-log", r.chat); } }
          if (target === "rps") { const r = rpsRooms.find((x) => x.id === selectedRpsRoomId); if (r) { r.chat.push({ from: sender, audioData: audioUrl }); renderRoomChatLog("rps-room-chat-log", r.chat); } }
          if (target === "mem") { const r = memRooms.find((x) => x.id === selectedMemRoomId); if (r) { r.chat.push({ from: sender, audioData: audioUrl }); renderRoomChatLog("mem-room-chat-log", r.chat); } }
          if (target === "num") { const r = numRooms.find((x) => x.id === selectedNumRoomId); if (r) { r.chat.push({ from: sender, audioData: audioUrl }); renderRoomChatLog("num-room-chat-log", r.chat); } }
          if (target === "rr") { rrTable.chat.push({ from: sender, audioData: audioUrl }); renderRoomChatLog("rr-room-chat-log", rrTable.chat); }
        }, null, btn);
      };
    });

    renderRrTable();

    const savedSession = localStorage.getItem("toplove_session");
    if (savedSession) { try { openApp(JSON.parse(savedSession)); } catch {} }
  </script>
</body>
</html>
