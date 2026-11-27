<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>TopLove</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    body {
      background: radial-gradient(circle at top right, #3b0764, #0f172a 55%, #020617);
      color: #f8fafc;
      min-height: 100vh;
    }
    .glass {
      background: rgba(15, 23, 42, 0.72);
      backdrop-filter: blur(14px);
      border: 1px solid rgba(255, 255, 255, 0.12);
    }
    .bg-aurora { background: linear-gradient(135deg, #ec4899, #8b5cf6, #06b6d4); }
    .bg-sunset { background: linear-gradient(135deg, #f97316, #ec4899, #9333ea); }
    .bg-ocean  { background: linear-gradient(135deg, #0284c7, #14b8a6, #2563eb); }
    .bg-gold   { background: linear-gradient(135deg, #f59e0b, #eab308, #d97706); }
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
        </div>
        <div class="grid grid-cols-2 gap-3">
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
        <button type="button" data-tab="profile" class="tab-btn px-5 py-2.5 rounded-xl text-sm font-semibold bg-pink-600 text-white">✨ פרופיל אישי</button>
        <button type="button" data-tab="users" class="tab-btn px-5 py-2.5 rounded-xl text-sm font-semibold glass text-slate-300">💘 היכרויות</button>
        <button type="button" data-tab="chat" class="tab-btn px-5 py-2.5 rounded-xl text-sm font-semibold glass text-slate-300">💬 חדרי צ׳אט</button>
        <button type="button" data-tab="games" class="tab-btn px-5 py-2.5 rounded-xl text-sm font-semibold glass text-slate-300">🎮 משחקים</button>
      </nav>

      <div id="tab-profile" class="tab-content space-y-5">
        <div class="glass rounded-3xl p-4 flex flex-wrap items-center justify-between gap-3">
          <div class="flex items-center gap-3">
            <span id="profile-completion-badge" class="text-xs font-bold px-3 py-1.5 rounded-full bg-pink-500/20 border border-pink-400/30 text-pink-200">✨ השלמת פרופיל: 0%</span>
            <span id="save-feedback" class="opacity-0 transition-opacity text-xs text-emerald-300 font-bold">✓ נשמר</span>
          </div>
          <button id="edit-profile-btn" type="button" class="hidden px-4 py-2 rounded-xl bg-indigo-600 text-xs font-bold">✏️ ערוך פרופיל</button>
        </div><div id="profile-summary-card" class="hidden glass rounded-3xl overflow-hidden space-y-4">
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
          </div>
          <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-3 text-xs">
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
            <div class="font-bold text-indigo-300">תחביבים ואימוג׳י</div>
            <div id="hobbies-options" class="flex flex-wrap gap-1.5"></div>
          </div>
          <button type="submit" class="px-6 py-3 rounded-xl bg-pink-600 text-sm font-extrabold">שמור פרופיל</button>
        </form>
      </div><div id="tab-users" class="tab-content hidden space-y-6">
        <div class="glass rounded-3xl p-5 space-y-4">
          <div class="flex flex-wrap items-center justify-between gap-2">
            <h2 class="text-lg font-extrabold">סינון ודפדוף פרופילים</h2>
            <span id="following-count-badge" class="text-xs px-3 py-1 rounded-full bg-indigo-500/20 border border-indigo-400/30 text-indigo-200">עוקב אחרי 0 משתמשים</span>
          </div>
          <div class="grid grid-cols-2 sm:grid-cols-5 gap-3 text-xs">
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
          </div>
          <div class="border-t border-white/10 pt-4 space-y-3">
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
            <h2 class="text-base font-extrabold">חדרי שיחה (עד 50–60 משתתפים • איפוס שבועי)</h2>
            <form id="create-room-form" class="space-y-2">
              <input id="new-room-topic" type="text" placeholder="נושא חדר חדש..." class="w-full px-3 py-2 rounded-xl bg-slate-950 border border-slate-700 text-xs" />
              <input id="new-room-code" type="text" placeholder="קוד לחדר פרטי (אופציונלי)" class="w-full px-3 py-2 rounded-xl bg-slate-950 border border-slate-700 text-xs" />
              <button type="submit" class="w-full py-2 rounded-xl bg-indigo-600 text-xs font-bold">+ פתח חדר (עד 50)</button>
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
                <button id="leave-room-btn" type="button" class="hidden px-3 py-1.5 rounded-xl bg-rose-600/80 text-xs font-semibold">צא מהחדר</button>
              </div>
            </div>
            <div id="chat-messages" class="flex-1 space-y-2 max-h-96 overflow-y-auto"></div>
            <div class="space-y-2 border-t border-white/10 pt-3">
              <div class="flex items-center justify-between text-[11px] text-slate-400">
                <span id="voice-status"></span>
                <button id="record-voice-btn" type="button" class="px-3 py-1 rounded-lg bg-amber-600 text-white font-bold text-xs">🎤 הקלטה קולית</button>
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
              <button id="ttt-join-room" type="button" class="px-3 py-1.5 rounded-lg bg-emerald-600 font-bold">כנס לחדר</button>
              <button id="ttt-leave-room" type="button" class="hidden px-3 py-1.5 rounded-lg bg-rose-600 font-bold">צא מהחדר</button>
              <button id="ttt-reset" type="button" class="px-3 py-1.5 rounded-lg bg-slate-800 font-bold">אפס</button>
              <button id="ttt-add-room" type="button" class="px-3 py-1.5 rounded-lg bg-indigo-600 font-bold">+ חדר</button>
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
                <input id="ttt-room-chat-input" type="text" placeholder="הודעה לחדר..." class="flex-1 px-3 py-2 rounded-xl bg-slate-950 border border-slate-700 text-xs" />
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
              <button id="rps-join-room" type="button" class="px-3 py-1.5 rounded-lg bg-emerald-600 font-bold">כנס לחדר</button>
              <button id="rps-leave-room" type="button" class="hidden px-3 py-1.5 rounded-lg bg-rose-600 font-bold">צא מהחדר</button>
              <button id="rps-add-room" type="button" class="px-3 py-1.5 rounded-lg bg-indigo-600 font-bold">+ חדר</button>
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
            <input id="rps-room-chat-input" type="text" placeholder="הודעה לחדר..." class="flex-1 px-3 py-2 rounded-xl bg-slate-950 border border-slate-700 text-xs" />
            <button type="button" data-voice-target="rps" class="room-voice-btn px-3 py-2 rounded-xl bg-amber-600 text-xs font-bold">🎤</button>
            <button type="submit" class="px-4 py-2 rounded-xl bg-pink-600 text-xs font-bold">שלח</button>
          </form>
        </div><div id="game-memory" class="game-panel hidden glass rounded-3xl p-5 space-y-4">
          <div class="flex flex-wrap items-center justify-between gap-2">
            <h3 class="font-extrabold">משחק זיכרון</h3>
            <div class="flex items-center gap-2 text-xs">
              <span id="memory-timer" class="px-2.5 py-1 rounded-lg bg-slate-900 border border-slate-700">⏱️ 03:00</span>
              <button id="memory-join-room" type="button" class="px-3 py-1.5 rounded-lg bg-emerald-600 font-bold">כנס לחדר</button>
              <button id="memory-leave-room" type="button" class="hidden px-3 py-1.5 rounded-lg bg-rose-600 font-bold">צא מהחדר</button>
              <button id="memory-reset" type="button" class="px-3 py-1.5 rounded-lg bg-slate-800 font-bold">ערבב</button>
            </div>
          </div>
          <div id="memory-status" class="text-xs text-pink-200 font-semibold"></div>
          <div id="memory-rooms-grid" class="grid grid-cols-2 sm:grid-cols-5 gap-2 max-h-32 overflow-y-auto"></div>
          <form id="mem-create-room-form" class="flex flex-wrap gap-2">
            <input id="mem-room-name" type="text" placeholder="שם חדר זיכרון..." class="flex-1 px-3 py-2 rounded-xl bg-slate-950 border border-slate-700 text-xs" />
            <select id="mem-room-mode" class="px-3 py-2 rounded-xl bg-slate-950 border border-slate-700 text-xs">
              <option value="6x6">6×6</option>
              <option value="10x10">10×10</option>
              <option value="20x20">20×20</option>
              <option value="30x30">30×30</option>
              <option value="50x50">50×50</option>
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
              <span id="num-room-cap" class="px-2.5 py-1 rounded-lg bg-slate-900 border border-slate-700">0 / 10</span>
              <button id="num-join-room" type="button" class="px-3 py-1.5 rounded-lg bg-emerald-600 font-bold">כנס לחדר</button>
              <button id="num-leave-room" type="button" class="hidden px-3 py-1.5 rounded-lg bg-rose-600 font-bold">צא מהחדר</button>
            </div>
          </div>
          <div id="num-rooms-list" class="grid grid-cols-2 sm:grid-cols-5 gap-2 max-h-36 overflow-y-auto"></div>
          <form id="num-create-room-form" class="flex flex-wrap gap-2">
            <input id="num-room-name" type="text" placeholder="שם חדר ניחושים..." class="flex-1 px-3 py-2 rounded-xl bg-slate-950 border border-slate-700 text-xs" />
            <input id="num-room-max" type="number" min="10" max="100" value="100" class="w-28 px-3 py-2 rounded-xl bg-slate-950 border border-slate-700 text-xs" />
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
              <button id="rr-join-btn" type="button" class="px-3 py-1.5 rounded-lg bg-emerald-600 font-bold">כנס לחדר</button>
              <button id="rr-leave-btn" type="button" class="hidden px-3 py-1.5 rounded-lg bg-rose-600 font-bold">צא מהחדר</button>
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
          <button id="modal-dm-btn" type="button" class="px-3 py-2 rounded-xl bg-emerald-600 text-xs font-bold">💬 הודעה אישית</button>
        </div>
      </div>
    </div>
  </div><script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-app.js";
    import { getAuth, signInWithEmailAndPassword, createUserWithEmailAndPassword, signOut } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-auth.js";
    import { getFirestore, collection, doc, setDoc, addDoc, query, orderBy, onSnapshot, serverTimestamp } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-firestore.js";

    const firebaseConfig = {
      apiKey: "YOUR_API_KEY",
      authDomain: "YOUR_PROJECT.firebaseapp.com",
      projectId: "YOUR_PROJECT_ID",
      storageBucket: "YOUR_PROJECT.appspot.com",
      messagingSenderId: "YOUR_SENDER_ID",
      appId: "YOUR_APP_ID"
    };
    const hasRealFirebaseConfig = Boolean(firebaseConfig.apiKey && !firebaseConfig.apiKey.startsWith("YOUR_"));
    const fbApp = hasRealFirebaseConfig ? initializeApp(firebaseConfig) : null;
    const auth = fbApp ? getAuth(fbApp) : null;
    const db = fbApp ? getFirestore(fbApp) : null;
    const $ = (id) => document.getElementById(id);

    function escapeHtml(val) {
      return String(val ?? "").replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;").replace(/"/g, "&quot;").replace(/'/g, "&#39;");
    }
    function safeUrl(url) {
      const s = String(url ?? "").trim();
      return (s.startsWith("data:image/") || s.startsWith("data:audio/") || s.startsWith("https://") || s.startsWith("http://")) ? s : "";
    }

    const gameNames = { ttt: "איקס עיגול", rps: "אבן נייר מספריים", memory: "משחק זיכרון", number: "ניחוש מספר", roulette: "רולטה רוסית" };
    const tripsChoices = ["🏖️ ים המלח", "🌴 אילת", "⛰️ צפון וגולן", "🏛️ ירושלים", "🌲 טבע ומסלולים", "✈️ חו״ל"];
    const nightChoices = ["🍹 בר / פאב", "🎤 הופעה חיה", "🎬 קולנוע", "🍽️ ארוחת ערב", "🛋️ ישיבה בבית", "💃 ריקודים"];
    const hobbiesChoices = ["🎵 מוזיקה", "🍳 בישול", "📚 קריאה", "🏋️ כושר", "📷 צילום", "🗺️ טיולים", "🎮 גיימינג", "☕ קפה", "🐶 כלבים", "🐱 חתולים"];
    const gameLeaderboards = { ttt: [], rps: [], memory: [], number: [], roulette: [] };
    let allUsers = [];

    let me = {
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
    };let currentGameKey = "ttt", deckIdx = 0, modalPhotos = [], modalPhotoIdx = 0;
    const chatTopics = ["✈️ טיולים", "🛫 טיסות לחו״ל", "🍳 אוכל ובישולים", "🐶 שמות לכלבים", "🐱 חיות מחמד", "☕ קפה ושיחות", "🎮 גיימינג", "🎬 קולנוע", "🏋️ כושר", "🎵 מוזיקה"];
    const defaultRooms = Array.from({ length: 100 }, (_, i) => ({
      id: `r-${i + 1}`,
      topic: `${chatTopics[i % chatTopics.length]} #${i + 1}`,
      maxUsers: 50 + (i % 11),
      code: "",
      members: [],
      messages: []
    }));
    const WEEK_MS = 7 * 24 * 60 * 60 * 1000;
    let lastWeeklyReset = Number(localStorage.getItem("toplove_week_reset") || Date.now());
    if (Date.now() - lastWeeklyReset >= WEEK_MS) {
      lastWeeklyReset = Date.now();
      localStorage.setItem("toplove_week_reset", String(lastWeeklyReset));
      defaultRooms.forEach((r) => { r.messages = []; });
    }
    let chatRooms = [...defaultRooms], activeRoomId = defaultRooms[0].id, joinedRoomId = null, unsubMsgs = null, unsubRooms = null, unsubUsers = null;

    function getLevel(pts) { return Math.max(1, Math.floor((Number(pts) || 0) / 50) + 1); }
    function getRewardLabel(i) { return i === 0 ? "🥇 מקום 1" : i === 1 ? "🥈 מקום 2" : i === 2 ? "🥉 מקום 3" : "🎖️ טופ-100"; }
    function upsertPlayerBoard(gameKey, name, st) {
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
      $("rr-gold-balls").textContent = String(me.rrRewards.goldBalls || 0);
      $("rr-magazines").textContent = String(me.rrRewards.magazines || 0);
      $("rr-pistols").textContent = String(me.rrRewards.pistols || 0);
      $("rr-grand-gifts").textContent = String(me.rrRewards.grandGifts || 0);
      const list = gameLeaderboards[gameKey] || [];
      $("top100-count-badge").textContent = `${list.length} / 100`;
      $("top5-title").textContent = `🏅 טופ-5 ב${gameNames[gameKey]}`;
      $("top5-board").innerHTML = list.length ? list.slice(0, 5).map((p, i) => `<div class="p-2.5 rounded-xl bg-slate-900 border border-slate-800"><div class="font-bold truncate">${i + 1}. ${escapeHtml(p.name)}</div><div class="text-pink-300">רמה ${p.level} • ${p.points} נק׳</div><div class="text-[11px] text-amber-300">${escapeHtml(getRewardLabel(i))}</div></div>`).join("") : `<p class="text-slate-400 col-span-full">שחק משחק אחד לפחות כדי להיכנס לדירוג.</p>`;
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
    }
    function formatPetLine(p) {
      const parts = [];
      if (p.hasPets) parts.push(escapeHtml(p.hasPets));
      if (p.favPet === "אחר") parts.push(p.otherPetText ? `מעדיף/ה: ${escapeHtml(p.otherPetText)}` : "מעדיף/ה: אחר");
      else if (p.favPet) parts.push(`מעדיף/ה: ${escapeHtml(p.favPet)}`);
      if (p.petName) parts.push(`שם: ${escapeHtml(p.petName)}`);
      return parts.length ? `🐾 ${parts.join(" • ")}` : "";
    }
    function updateModalPhotoView() {
      if (!modalPhotos.length) { $("modal-main-photo").classList.add("hidden"); $("modal-gallery").innerHTML = ""; return; }
      const src = safeUrl(modalPhotos[modalPhotoIdx]);
      if (src) { $("modal-main-photo").src = src; $("modal-main-photo").classList.remove("hidden"); }
      $("modal-gallery").innerHTML = modalPhotos.map((u, i) => `<img src="${escapeHtml(u)}" alt="" data-mphoto="${i}" class="w-12 h-12 rounded-lg object-cover border cursor-pointer ${i === modalPhotoIdx ? "border-pink-400" : "border-slate-700"}" />`).join("");
      $("modal-gallery").querySelectorAll("[data-mphoto]").forEach((img) => { img.onclick = () => { modalPhotoIdx = Number(img.dataset.mphoto) || 0; updateModalPhotoView(); }; });
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
      $("modal-action-msg").textContent = "";
      updateModalPhotoView();
      const targetId = person.uid || person.id;
      $("modal-follow-btn").textContent = (me.following || []).includes(targetId) ? "✓ עוקב" : "➕ עקוב";
      $("modal-like-btn").onclick = () => { $("modal-action-msg").textContent = `שלחת לייק ל${person.name || "משתמש"} 👍`; };
      $("modal-heart-btn").onclick = () => { $("modal-action-msg").textContent = `שלחת לב ל${person.name || "משתמש"} 💖 — אפשר לפתוח הודעה אישית.`; };
      $("modal-follow-btn").onclick = async () => {
        if (!targetId || targetId === me.uid) return;
        me.following = me.following || [];
        me.following = me.following.includes(targetId) ? me.following.filter((x) => x !== targetId) : [...me.following, targetId];
        localStorage.setItem("toplove_session", JSON.stringify(me));
        try { if (db && me.uid) await setDoc(doc(db, "users", me.uid), { following: me.following }, { merge: true }); } catch {}
        syncHeaderUserBadge(); openUserModal(person); renderRealUsers();
      };
      $("modal-dm-btn").onclick = async () => {
        if (!targetId || targetId === me.uid || !me.uid) return;
        const dmId = "dm_" + [me.uid, targetId].sort().join("_");
        await ensureRoomInFirestore({ id: dmId, topic: `שיחה אישית עם ${person.name || "משתמש"}`, code: "", maxUsers: 2 });
        activeRoomId = dmId; joinedRoomId = dmId; $("user-modal").classList.add("hidden"); switchTab("chat"); renderRooms(); listenMsgs(dmId);
      };
      $("user-modal").classList.remove("hidden");
    }
    $("close-modal-btn").onclick = () => $("user-modal").classList.add("hidden");
    $("modal-prev-photo").onclick = () => { if (modalPhotos.length) { modalPhotoIdx = (modalPhotoIdx - 1 + modalPhotos.length) % modalPhotos.length; updateModalPhotoView(); } };
    $("modal-next-photo").onclick = () => { if (modalPhotos.length) { modalPhotoIdx = (modalPhotoIdx + 1) % modalPhotos.length; updateModalPhotoView(); } };

    function syncHeaderUserBadge() {
      $("user-badge").textContent = `${me.name || (me.email ? me.email.split("@")[0] : "משתמש")} • ${me.age || 18}`;
      const av = safeUrl(me.avatar || (me.photos && me.photos[0]) || "");
      $("header-avatar-slot").innerHTML = av ? `<img src="${escapeHtml(av)}" alt="" class="w-full h-full object-cover" />` : "👤";
      $("following-count-badge").textContent = `עוקב אחרי ${(me.following || []).length} משתמשים`;
    }
    function computeProfileCompletion() {
      const fields = [me.name, me.gender, me.location, me.goal, me.bio, me.tagline, me.job, me.education, me.trips.length, me.hobbies.length];
      $("profile-completion-badge").textContent = `✨ השלמת פרופיל: ${Math.min(100, Math.round((fields.filter(Boolean).length / fields.length) * 100))}%`;
    }
    $("prof-fav-pet").onchange = () => $("prof-other-pet-wrap").classList.toggle("hidden", $("prof-fav-pet").value !== "אחר");
    $("prof-avatar-file").onchange = (e) => {
      Array.from(e.target.files || []).slice(0, 5).forEach((f) => {
        if (!f.type.startsWith("image/") || f.size > 1500000) return;
        const r = new FileReader();
        r.onload = () => {
          const url = safeUrl(r.result); if (!url) return;
          me.photos = [...(me.photos || []), url].slice(0, 6);
          me.avatar = me.photos[0]; me.hasCustomPhoto = true;
          $("prof-avatar-preview").src = url; $("prof-avatar-preview").classList.remove("hidden"); $("prof-avatar-placeholder").classList.add("hidden");
          $("prof-photos-thumbs").innerHTML = me.photos.map((p) => `<img src="${escapeHtml(p)}" alt="" class="w-12 h-12 rounded-xl object-cover border border-white/15" />`).join("");
          syncHeaderUserBadge();
        };
        r.readAsDataURL(f);
      });
    };
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
      syncHeaderUserBadge(); computeProfileCompletion();
      const showSummary = Boolean(me.profileCompleted);
      $("profile-summary-card").classList.toggle("hidden", !showSummary);
      $("profile-form").classList.toggle("hidden", showSummary);
      $("edit-profile-btn").classList.toggle("hidden", !showSummary);
      if (showSummary) {
        const b = ["bg-aurora", "bg-sunset", "bg-ocean", "bg-gold"].includes(me.banner) ? me.banner : "bg-aurora";
        $("summary-banner").className = `h-36 ${b} p-5 flex items-start justify-between`;
        $("summary-name").className = `text-2xl font-extrabold ${me.nameStyle || ""}`;
        $("summary-name").textContent = me.name || "משתמש"; $("summary-tagline").textContent = me.tagline || "";
        $("summary-age-gender-loc").textContent = [me.gender, me.age ? `גיל ${me.age}` : "", me.location].filter(Boolean).join(" • ");
        $("summary-bio").textContent = me.bio || "";
        $("summary-col-dating").innerHTML = `<div>💘 מחפש/ת: ${escapeHtml(me.lookingFor)}</div><div>🎯 מטרה: ${escapeHtml(me.goal)}</div><div>💍 מצב: ${escapeHtml(me.marital)}</div>`;
        $("summary-col-lifestyle").innerHTML = `<div>💼 עיסוק: ${escapeHtml(me.job)}</div><div>🎓 השכלה: ${escapeHtml(me.education)}</div><div>✨ מזל: ${escapeHtml(me.zodiac)}</div>`;
        $("summary-col-pets").textContent = formatPetLine(me);
        $("summary-col-trips").innerHTML = (me.trips || []).map((t) => `<span class="px-2 py-0.5 rounded-full bg-emerald-500/20">${escapeHtml(t)}</span>`).join("");
        $("summary-col-night").textContent = (me.nightActivities || []).join(" • ");
        $("summary-col-extra").innerHTML = (me.hobbies || []).map((h) => `<span class="px-2 py-0.5 rounded-full bg-indigo-500/20">${escapeHtml(h)}</span>`).join("");
      }
    }
    $("profile-form").onsubmit = async (e) => {
      e.preventDefault();
      const ageVal = Number($("prof-age").value) || me.age || 18;
      if (ageVal < 18 || ageVal > 80) { $("profile-error").textContent = "גיל חייב להיות בין 18 ל-80."; $("profile-error").classList.remove("hidden"); return; }
      $("profile-error").classList.add("hidden");
      Object.assign(me, {
        name: $("prof-name").value.trim().slice(0, 60) || me.name, nickname: $("prof-nickname").value.trim().slice(0, 40),
        gender: $("prof-gender").value, lookingFor: $("prof-looking-for").value || "הכל", age: ageVal,
        location: $("prof-location").value.trim().slice(0, 60), distanceKm: Math.max(0, Math.min(500, Number($("prof-distance").value) || 15)),
        goal: $("prof-goal").value.trim().slice(0, 80), marital: $("prof-marital").value.trim().slice(0, 50),
        children: $("prof-children").value.trim().slice(0, 50), height: $("prof-height").value.trim().slice(0, 20),
        job: $("prof-job").value.trim().slice(0, 60), zodiac: $("prof-zodiac").value.trim().slice(0, 30),
        smoking: $("prof-smoking").value.trim().slice(0, 40), alcohol: $("prof-alcohol").value.trim().slice(0, 40),
        education: $("prof-education").value.trim().slice(0, 60), hasPets: $("prof-has-pets").value.trim().slice(0, 40),
        favPet: $("prof-fav-pet").value, petName: $("prof-pet-name").value.trim().slice(0, 40),
        otherPetText: $("prof-other-pet-text").value.trim().slice(0, 50), firstDate: $("prof-first-date").value.trim().slice(0, 80),
        tagline: $("prof-tagline").value.trim().slice(0, 100), banner: $("prof-banner").value || "bg-aurora",
        bio: $("prof-bio").value.trim().slice(0, 800), profileCompleted: true
      });
      localStorage.setItem("toplove_session", JSON.stringify(me));
      $("save-feedback").classList.remove("opacity-0"); setTimeout(() => $("save-feedback").classList.add("opacity-0"), 1500);
      try { if (db && me.uid) await setDoc(doc(db, "users", me.uid), { ...me, updatedAt: serverTimestamp() }, { merge: true }); } catch {}
      applyProfileViewMode(); renderRealUsers();
    };
    $("edit-profile-btn").onclick = () => { me.profileCompleted = false; applyProfileViewMode(); };
    function switchTab(t) {
      document.querySelectorAll(".tab-btn").forEach((b) => { b.className = b.dataset.tab === t ? "tab-btn px-5 py-2.5 rounded-xl text-sm font-semibold bg-pink-600 text-white" : "tab-btn px-5 py-2.5 rounded-xl text-sm font-semibold glass text-slate-300"; });
      document.querySelectorAll(".tab-content").forEach((c) => c.classList.add("hidden"));
      $(`tab-${t}`).classList.remove("hidden");
    }
    $("user-profile-trigger").onclick = () => switchTab("profile");
    document.querySelectorAll(".tab-btn").forEach((btn) => { btn.onclick = () => switchTab(btn.dataset.tab); });

    async function ensureRoomInFirestore(room) {
      if (!db || !room?.id) return;
      try { await setDoc(doc(db, "rooms", room.id), { id: room.id, topic: String(room.topic || "").slice(0, 80), code: String(room.code || "").slice(0, 30), maxUsers: Number(room.maxUsers) || 50, isDm: String(room.id).startsWith("dm_"), updatedAt: serverTimestamp() }, { merge: true }); } catch {}
    }
    function subscribeAllRooms() {
      if (unsubRooms) { unsubRooms(); unsubRooms = null; }
      if (!db) { renderRooms(); return; }
      unsubRooms = onSnapshot(collection(db, "rooms"), (snap) => {
        const byId = new Map(defaultRooms.map((r) => [r.id, { ...r }]));
        snap.docs.forEach((d) => { const rr = d.data(); const prev = byId.get(d.id); byId.set(d.id, { id: d.id, topic: rr.topic || prev?.topic || d.id, code: rr.code || "", maxUsers: Number(rr.maxUsers) || prev?.maxUsers || 50, members: prev?.members || [], messages: prev?.messages || [] }); });
        chatRooms = Array.from(byId.values()).filter((r) => !String(r.id).startsWith("dm_") || (me.uid && String(r.id).includes(me.uid)));
        renderRooms();
      });
    }
    function subscribeRealUsers() {
      if (unsubUsers) { unsubUsers(); unsubUsers = null; }
      if (!db) { renderRealUsers(); return; }
      unsubUsers = onSnapshot(collection(db, "users"), (snap) => {
        allUsers = snap.docs.map((d) => ({ id: d.id, ...d.data() })).filter((u) => (u.uid || u.id) !== me.uid);
        renderRealUsers();
      });
    }
    function renderLocalRoomMsgs(room) {
      const msgs = room?.messages || [];
      $("chat-messages").innerHTML = msgs.length ? msgs.map((m) => {
        const aud = safeUrl(m.audioUrl || "");
        return `<div class="bg-slate-800/90 px-3 py-2 rounded-xl text-xs space-y-1"><strong class="text-pink-300">${escapeHtml(m.from || "משתמש")}:</strong> ${escapeHtml(m.text || "")}${aud ? `<audio controls src="${escapeHtml(aud)}" class="w-full h-8 mt-1"></audio>` : ""}</div>`;
      }).join("") : `<p class="text-xs text-slate-400">אין עדיין הודעות בחדר.</p>`;
    }
    function listenMsgs(roomId) {
      const curRoom = chatRooms.find((r) => r.id === roomId);
      renderLocalRoomMsgs(curRoom);
      if (unsubMsgs) { unsubMsgs(); unsubMsgs = null; }
      if (!db) return;
      unsubMsgs = onSnapshot(query(collection(db, "rooms", roomId, "messages"), orderBy("createdAt", "asc")), (snap) => {
        const msgs = snap.docs.map((d) => d.data());
        if (msgs.length) {
          $("chat-messages").innerHTML = msgs.map((m) => {
            const aud = safeUrl(m.audioUrl || "");
            return `<div class="bg-slate-800/90 px-3 py-2 rounded-xl text-xs space-y-1"><strong class="text-pink-300">${escapeHtml(m.from || "משתמש")}:</strong> ${escapeHtml(m.text || "")}${aud ? `<audio controls src="${escapeHtml(aud)}" class="w-full h-8 mt-1"></audio>` : ""}</div>`;
          }).join("");
        }
      });
    }
    function renderRooms() {
      $("rooms-list").innerHTML = chatRooms.slice(0, 100).map((r) => `<div class="p-3 rounded-xl border text-xs flex items-center justify-between gap-2 ${joinedRoomId === r.id ? "bg-pink-600/25 border-pink-400" : "bg-slate-950/75 border-slate-800"}"><div class="truncate"><div class="font-bold truncate">${escapeHtml(r.topic)}</div><div class="text-[11px] text-slate-400">${(r.members || []).length} / ${r.maxUsers || 50} משתתפים${r.code ? " • 🔒" : ""}</div></div><button type="button" data-enter-room="${escapeHtml(r.id)}" class="px-3 py-1.5 rounded-lg bg-pink-600 font-bold shrink-0">${joinedRoomId === r.id ? "בתוך החדר" : "כנס"}</button></div>`).join("");
      document.querySelectorAll("[data-enter-room]").forEach((btn) => {
        btn.onclick = async () => {
          const target = chatRooms.find((r) => r.id === btn.dataset.enterRoom); if (!target) return;
          const cap = Number(target.maxUsers) || 50;
          target.members = target.members || [];
          if (!target.members.includes(me.uid || "me") && target.members.length >= cap) return alert("החדר מלא");
          if (target.code) { const entered = prompt("הכנס קוד לחדר הפרטי:") || ""; if (entered !== target.code) return alert("קוד שגוי"); }
          if (!target.members.includes(me.uid || "me")) target.members.push(me.uid || "me");
          await ensureRoomInFirestore(target); activeRoomId = target.id; joinedRoomId = target.id; renderRooms(); listenMsgs(target.id);
        };
      });
      const cur = chatRooms.find((r) => r.id === activeRoomId) || chatRooms[0];
      $("active-room-title").textContent = cur.topic;
      $("active-room-meta").textContent = `משתתפים: ${(cur.members || []).length} / ${cur.maxUsers || 50} • איפוס שבועי אוטומטי`;
      $("leave-room-btn").classList.toggle("hidden", joinedRoomId !== cur.id);
    }
    $("create-room-form").onsubmit = async (e) => {
      e.preventDefault();
      const topic = $("new-room-topic").value.trim().slice(0, 80); if (!topic) return;
      const code = $("new-room-code").value.trim().slice(0, 30);
      const room = { id: "r-" + Date.now(), topic, code, maxUsers: 50, members: [me.uid || "me"], messages: [] };
      $("new-room-topic").value = ""; $("new-room-code").value = "";
      chatRooms = [room, ...chatRooms]; activeRoomId = room.id; joinedRoomId = room.id;
      await ensureRoomInFirestore(room); renderRooms(); listenMsgs(room.id);
    };
    $("invite-friend-btn").onclick = () => {
      const cur = chatRooms.find((r) => r.id === activeRoomId) || chatRooms[0];
      const inv = prompt("הזן שם או קוד הזמנה לחבר לחדר:"); if (!inv) return;
      cur.messages = cur.messages || [];
      cur.messages.push({ from: "מערכת", text: `הוזמן חבר (${escapeHtml(inv.slice(0, 40))}) לחדר ${escapeHtml(cur.topic)}` });
      renderLocalRoomMsgs(cur);
    };
    $("leave-room-btn").onclick = () => {
      if (unsubMsgs) { unsubMsgs(); unsubMsgs = null; }
      const cur = chatRooms.find((r) => r.id === joinedRoomId);
      if (cur) {
        cur.members = (cur.members || []).filter((id) => id !== (me.uid || "me"));
        if (cur.members.length === 0) cur.messages = [];
      }
      joinedRoomId = null; renderRooms();
    };
    $("chat-form").onsubmit = async (e) => {
      e.preventDefault();
      if (joinedRoomId !== activeRoomId) return alert("היכנס קודם לחדר");
      const txt = $("chat-input").value.trim().slice(0, 1000); if (!txt) return;
      $("chat-input").value = "";
      const cur = chatRooms.find((r) => r.id === activeRoomId);
      if (cur) { cur.messages = cur.messages || []; cur.messages.push({ from: me.name || "משתמש", text: txt }); renderLocalRoomMsgs(cur); }
      if (db) await addDoc(collection(db, "rooms", activeRoomId, "messages"), { senderUid: me.uid, from: me.name || "משתמש", text: txt, createdAt: serverTimestamp() });
    };

    let activeRecorder = null, recordedChunks = [];
    async function toggleVoiceRecording(onAudioReady) {
      if (activeRecorder && activeRecorder.state === "recording") { activeRecorder.stop(); return; }
      if (!navigator.mediaDevices?.getUserMedia) return alert("הקלטה קולית אינה נתמכת בדפדפן זה");
      const stream = await navigator.mediaDevices.getUserMedia({ audio: true });
      recordedChunks = [];
      activeRecorder = new MediaRecorder(stream);
      $("voice-status").textContent = "מקליט...";
      activeRecorder.ondataavailable = (ev) => { if (ev.data.size > 0) recordedChunks.push(ev.data); };
      activeRecorder.onstop = () => {
        stream.getTracks().forEach((t) => t.stop());
        $("voice-status").textContent = "";
        const blob = new Blob(recordedChunks, { type: "audio/webm" });
        const reader = new FileReader();
        reader.onload = () => { const u = safeUrl(reader.result); if (u) onAudioReady(u); };
        reader.readAsDataURL(blob);
      };
      activeRecorder.start();
    }
    $("record-voice-btn").onclick = () => {
      if (joinedRoomId !== activeRoomId) return alert("היכנס קודם לחדר");
      toggleVoiceRecording(async (audioUrl) => {
        const cur = chatRooms.find((r) => r.id === activeRoomId);
        if (cur) { cur.messages = cur.messages || []; cur.messages.push({ from: me.name || "משתמש", text: "הקלטה קולית 🎤", audioUrl }); renderLocalRoomMsgs(cur); }
        if (db) await addDoc(collection(db, "rooms", activeRoomId, "messages"), { senderUid: me.uid, from: me.name || "משתמש", text: "הקלטה קולית 🎤", audioUrl, createdAt: serverTimestamp() });
      });
    };
    document.querySelectorAll(".room-voice-btn").forEach((btn) => {
      btn.onclick = () => {
        const target = btn.dataset.voiceTarget;
        toggleVoiceRecording((audioUrl) => {
          const logId = target === "ttt" ? "ttt-room-chat-log" : target === "rps" ? "rps-room-chat-log" : target === "mem" ? "mem-room-chat-log" : target === "num" ? "num-room-chat-log" : "rr-room-chat-log";
          $(logId).innerHTML += `<div class="p-2 rounded-lg bg-slate-900 border border-slate-800"><strong>${escapeHtml(me.name || "משתמש")}:</strong> 🎤 <audio controls src="${escapeHtml(audioUrl)}" class="h-7 align-middle"></audio></div>`;
        });
      };
    });

    document.querySelectorAll(".game-tab-btn").forEach((b) => {
      b.onclick = () => {
        const g = b.dataset.game;
        document.querySelectorAll(".game-tab-btn").forEach((x) => { x.className = x.dataset.game === g ? "game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold bg-pink-600" : "game-tab-btn px-4 py-2 rounded-xl text-xs font-semibold glass text-slate-300"; });
        document.querySelectorAll(".game-panel").forEach((p) => p.classList.add("hidden"));
        $(`game-${g}`).classList.remove("hidden"); renderGameStatsAndTop5(g);
      };
    });

    let tttBoard = Array(9).fill(""), tttTurn = "X", tttMySym = "X", tttRoomIdx = 0, tttJoined = false, tttOpponent = false;
    const tttRooms = Array.from({ length: 20 }, (_, i) => ({ name: `חדר איקס עיגול ${i + 1}`, players: i % 2 === 0 ? ["אורח"] : [], chat: [] }));
    function checkTttWin(b) {
      for (const [a, c, d] of [[0,1,2],[3,4,5],[6,7,8],[0,3,6],[1,4,7],[2,5,8],[0,4,8],[2,4,6]]) if (b[a] && b[a] === b[c] && b[a] === b[d]) return b[a];
      return b.every(Boolean) ? "DRAW" : "";
    }
    function renderTtt() {
      const rm = tttRooms[tttRoomIdx];
      $("ttt-p1-name").textContent = tttJoined ? (me.name || "אתה") : "ממתין";
      $("ttt-p2-name").textContent = tttOpponent ? "שחקן נוסף" : "ממתין לשחקן";
      $("ttt-join-room").classList.toggle("hidden", tttJoined);
      $("ttt-leave-room").classList.toggle("hidden", !tttJoined);
      $("ttt-status").textContent = !tttJoined ? `${rm.name} — לחץ "כנס לחדר" כדי להצטרף` : (!tttOpponent ? `${rm.name} — ממתין לשחקן אחר שיצטרף לפני תחילת המשחק` : `${rm.name} • תור: ${tttTurn === "X" ? "❌" : "⭕"}`);
      $("ttt-board").innerHTML = tttBoard.map((v, idx) => `<button type="button" data-ttt-i="${idx}" class="h-20 rounded-2xl bg-slate-900 border border-slate-700 text-3xl font-black flex items-center justify-center">${v === "X" ? "❌" : v === "O" ? "⭕" : ""}</button>`).join("");
      $("ttt-board").querySelectorAll("[data-ttt-i]").forEach((btn) => {
        btn.onclick = async () => {
          if (!tttJoined || !tttOpponent) return alert("יש להיכנס לחדר ולהמתין לשחקן נוסף לפני תחילת המשחק");
          const i = Number(btn.dataset.tttI); if (tttBoard[i] || checkTttWin(tttBoard)) return;
          tttBoard[i] = tttMySym;
          const res = checkTttWin(tttBoard);
          if (res === tttMySym) { $("ttt-status").textContent = "ניצחת! +25 נק׳"; await awardGameWin("ttt", 25); }
          else if (res === "DRAW") { $("ttt-status").textContent = "תיקו! +10 נק׳"; await awardGameWin("ttt", 10); }
          else { tttTurn = tttMySym === "X" ? "O" : "X"; }
          renderTtt();
        };
      });
      $("ttt-rooms-grid").innerHTML = tttRooms.map((r, i) => `<button type="button" data-tttr="${i}" class="p-1.5 rounded-lg text-[11px] border ${i === tttRoomIdx ? "bg-pink-600 border-pink-400" : "bg-slate-900 border-slate-800"}">${escapeHtml(r.name)}</button>`).join("");
      $("ttt-rooms-grid").querySelectorAll("[data-tttr]").forEach((b) => { b.onclick = () => { tttRoomIdx = Number(b.dataset.tttr) || 0; tttBoard = Array(9).fill(""); renderTtt(); }; });
      $("ttt-room-chat-log").innerHTML = rm.chat.map((c) => `<div class="p-1.5 rounded-lg bg-slate-900/90">${escapeHtml(c)}</div>`).join("");
    }
    $("ttt-join-room").onclick = () => { tttJoined = true; tttOpponent = true; renderTtt(); };
    $("ttt-leave-room").onclick = () => { tttJoined = false; tttOpponent = false; tttBoard = Array(9).fill(""); tttRooms[tttRoomIdx].chat = []; renderTtt(); };
    $("ttt-pick-x").onclick = () => { tttMySym = "X"; renderTtt(); };
    $("ttt-pick-o").onclick = () => { tttMySym = "O"; renderTtt(); };
    $("ttt-reset").onclick = () => { tttBoard = Array(9).fill(""); tttTurn = "X"; renderTtt(); };
    $("ttt-add-room").onclick = () => { tttRooms.push({ name: `חדר איקס עיגול ${tttRooms.length + 1}`, players: [me.name || "אתה"], chat: [] }); tttRoomIdx = tttRooms.length - 1; tttJoined = true; tttOpponent = false; renderTtt(); };
    $("ttt-room-chat-form").onsubmit = (e) => { e.preventDefault(); const t = $("ttt-room-chat-input").value.trim().slice(0, 400); if (!t) return; $("ttt-room-chat-input").value = ""; tttRooms[tttRoomIdx].chat.push(`${me.name || "שחקן"}: ${t}`); renderTtt(); };

    const rpsMap = { rock: "🪨", paper: "📄", scissors: "✂️" };
    let rpsRoomIdx = 0, rpsJoined = false, rpsOpponent = false;
    const rpsRooms = Array.from({ length: 20 }, (_, i) => ({ name: `חדר אבן נייר מספריים ${i + 1}`, chat: [] }));
    function renderRps() {
      const rm = rpsRooms[rpsRoomIdx];
      $("rps-left-name").textContent = rpsJoined ? (me.name || "אתה") : "ממתין";
      $("rps-right-name").textContent = rpsOpponent ? "שחקן נוסף" : "ממתין לשחקן";
      $("rps-join-room").classList.toggle("hidden", rpsJoined);
      $("rps-leave-room").classList.toggle("hidden", !rpsJoined);
      $("rps-round-phase").textContent = !rpsJoined ? `${rm.name} — לחץ "כנס לחדר"` : (!rpsOpponent ? "ממתין לשחקן נוסף שיצטרף" : `${rm.name} — מוכן למשחק`);
      $("rps-rooms-grid").innerHTML = rpsRooms.map((r, i) => `<button type="button" data-rpsr="${i}" class="p-1.5 rounded-lg text-[11px] border ${i === rpsRoomIdx ? "bg-pink-600 border-pink-400" : "bg-slate-900 border-slate-800"}">${escapeHtml(r.name)}</button>`).join("");
      $("rps-rooms-grid").querySelectorAll("[data-rpsr]").forEach((b) => { b.onclick = () => { rpsRoomIdx = Number(b.dataset.rpsr) || 0; renderRps(); }; });
      $("rps-room-chat-log").innerHTML = rm.chat.map((c) => `<div class="p-1.5 rounded-lg bg-slate-900/90">${escapeHtml(c)}</div>`).join("");
    }
    $("rps-join-room").onclick = () => { rpsJoined = true; rpsOpponent = true; renderRps(); };
    $("rps-leave-room").onclick = () => { rpsJoined = false; rpsOpponent = false; rpsRooms[rpsRoomIdx].chat = []; renderRps(); };
    document.querySelectorAll(".rps-choice").forEach((b) => {
      b.onclick = async () => {
        if (!rpsJoined || !rpsOpponent) return alert("יש להיכנס לחדר ולהמתין לשחקן נוסף לפני תחילת המשחק");
        const mine = b.dataset.rps, keys = ["rock", "paper", "scissors"], bot = keys[Math.floor(Math.random() * 3)];
        $("rps-left-sign").textContent = rpsMap[mine]; $("rps-right-sign").textContent = rpsMap[bot];
        if (mine === bot) { $("rps-result").textContent = "תיקו! +10 נק׳"; await awardGameWin("rps", 10); }
        else if ((mine === "rock" && bot === "scissors") || (mine === "paper" && bot === "rock") || (mine === "scissors" && bot === "paper")) { $("rps-result").textContent = "ניצחת! +25 נק׳"; await awardGameWin("rps", 25); }
        else { $("rps-result").textContent = "הפסדת בסיבוב +5 נק׳"; await awardGameLoss("rps", 5); }
      };
    });
    $("rps-add-room").onclick = () => { rpsRooms.push({ name: `חדר אבן נייר מספריים ${rpsRooms.length + 1}`, chat: [] }); rpsRoomIdx = rpsRooms.length - 1; rpsJoined = true; rpsOpponent = false; renderRps(); };
    $("rps-room-chat-form").onsubmit = (e) => { e.preventDefault(); const t = $("rps-room-chat-input").value.trim().slice(0, 400); if (!t) return; $("rps-room-chat-input").value = ""; rpsRooms[rpsRoomIdx].chat.push(`${me.name || "שחקן"}: ${t}`); renderRps(); };

    let memMode = "6x6", memCards = [], memOpen = [], memMatched = new Set(), memPlayers = ["שחקן 1", "שחקן 2", "שחקן 3", "שחקן 4", "שחקן 5", "שחקן 6"], memTurnIdx = 0, memJoined = false, memRoomIdx = 0;
    const memRooms = Array.from({ length: 20 }, (_, i) => ({ name: `חדר זיכרון ${i + 1}`, mode: i % 5 === 0 ? "6x6" : i % 5 === 1 ? "10x10" : i % 5 === 2 ? "20x20" : i % 5 === 3 ? "30x30" : "50x50", chat: [] }));
    const memEmojis = ["💖","🔥","⚡","🎯","🎲","🌙","☀️","🍀","🎵","💎","🚀","👑","🍕","🐱","🐶","🌸","⭐","🎈","🍩","🍒"];
    function renderMemPlayers() {
      $("memory-players-board").innerHTML = memPlayers.map((p, idx) => `<div class="p-2 rounded-xl border ${idx === memTurnIdx ? "bg-pink-600/25 border-pink-400 font-bold" : "bg-slate-900 border-slate-800"}">${idx + 1}. ${escapeHtml(p)} ${idx === memTurnIdx ? "◀ תור" : ""}</div>`).join("");
    }
    function buildMemoryBoard() {
      const size = memMode === "50x50" ? 50 : memMode === "30x30" ? 30 : memMode === "20x20" ? 20 : memMode === "10x10" ? 10 : 6;
      const total = size * size, list = [];
      for (let i = 0; i < total; i += 2) { const em = memEmojis[(i / 2) % memEmojis.length]; list.push(em, em); }
      memCards = list.slice(0, total).sort(() => Math.random() - 0.5); memOpen = []; memMatched = new Set(); memTurnIdx = 0;
      $("memory-status").textContent = `${memRooms[memRoomIdx].name} • לוח ${memMode} • תור: ${memPlayers[memTurnIdx]}`;
      renderMemPlayers();
      $("memory-grid").style.gridTemplateColumns = `repeat(${size}, minmax(24px, 1fr))`;
      $("memory-grid").innerHTML = memCards.map((_, idx) => `<button type="button" data-memi="${idx}" class="h-7 rounded-md bg-slate-800 border border-slate-700 text-xs font-bold">❓</button>`).join("");
      $("memory-grid").querySelectorAll("[data-memi]").forEach((btn) => {
        btn.onclick = async () => {
          if (!memJoined) return alert("לחץ על כנס לחדר כדי לשחק");
          const idx = Number(btn.dataset.memi);
          if (memMatched.has(idx) || memOpen.includes(idx) || memOpen.length >= 2) return;
          btn.textContent = memCards[idx]; memOpen.push(idx);
          if (memOpen.length === 2) {
            const [a, c] = memOpen;
            if (memCards[a] === memCards[c]) {
              memMatched.add(a); memMatched.add(c); memOpen = [];
              $("memory-status").textContent = `התאמה נכונה! ${memPlayers[memTurnIdx]} ממשיך לשחק`;
              await awardGameWin("memory", 10);
            } else {
              setTimeout(() => {
                const ba = $("memory-grid").querySelector(`[data-memi="${a}"]`), bc = $("memory-grid").querySelector(`[data-memi="${c}"]`);
                if (ba && !memMatched.has(a)) ba.textContent = "❓"; if (bc && !memMatched.has(c)) bc.textContent = "❓";
                memOpen = []; memTurnIdx = (memTurnIdx + 1) % memPlayers.length;
                $("memory-status").textContent = `לא תואם — התור עבר ל${memPlayers[memTurnIdx]}`;
                renderMemPlayers();
              }, 500);
            }
          }
        };
      });
    }
    function renderMemRooms() {
      $("memory-rooms-grid").innerHTML = memRooms.map((r, i) => `<button type="button" data-memr="${i}" class="p-1.5 rounded-lg text-[11px] border ${i === memRoomIdx ? "bg-pink-600 border-pink-400" : "bg-slate-900 border-slate-800"}">${escapeHtml(r.name)} (${r.mode})</button>`).join("");
      $("memory-rooms-grid").querySelectorAll("[data-memr]").forEach((b) => { b.onclick = () => { memRoomIdx = Number(b.dataset.memr) || 0; memMode = memRooms[memRoomIdx].mode; renderMemRooms(); buildMemoryBoard(); }; });
      $("mem-room-chat-log").innerHTML = memRooms[memRoomIdx].chat.map((c) => `<div class="p-1.5 rounded-lg bg-slate-900/90">${escapeHtml(c)}</div>`).join("");
    }
    $("memory-join-room").onclick = () => { memJoined = true; $("memory-join-room").classList.add("hidden"); $("memory-leave-room").classList.remove("hidden"); };
    $("memory-leave-room").onclick = () => { memJoined = false; memRooms[memRoomIdx].chat = []; $("memory-leave-room").classList.add("hidden"); $("memory-join-room").classList.remove("hidden"); renderMemRooms(); };
    $("mem-create-room-form").onsubmit = (e) => { e.preventDefault(); const nm = $("mem-room-name").value.trim().slice(0, 40) || `חדר זיכרון ${memRooms.length + 1}`; memMode = $("mem-room-mode").value || "6x6"; memRooms.push({ name: nm, mode: memMode, chat: [] }); memRoomIdx = memRooms.length - 1; $("mem-room-name").value = ""; renderMemRooms(); buildMemoryBoard(); };
    $("memory-reset").onclick = buildMemoryBoard;
    $("mem-room-chat-form").onsubmit = (e) => { e.preventDefault(); const t = $("mem-room-chat-input").value.trim().slice(0, 400); if (!t) return; $("mem-room-chat-input").value = ""; memRooms[memRoomIdx].chat.push(`${me.name || "שחקן"}: ${t}`); renderMemRooms(); };

    const numRanges = [10, 20, 30, 40, 50, 60, 70, 80, 90, 100];
    const numRooms = Array.from({ length: 20 }, (_, i) => ({ name: `חדר ניחושים 1–${numRanges[i % numRanges.length]} #${i + 1}`, max: numRanges[i % numRanges.length], members: [], chat: [] }));
    let numRoomIdx = 0, numSecret = Math.floor(Math.random() * 10) + 1, numGuesses = [], numJoined = false;
    function renderNumRooms() {
      const rm = numRooms[numRoomIdx];
      $("num-room-header").textContent = `${rm.name} (1–${rm.max})`;
      $("num-room-cap").textContent = `${(rm.members || []).length} / 10+`;
      $("num-rooms-list").innerHTML = numRooms.map((r, i) => `<button type="button" data-numr="${i}" class="p-1.5 rounded-lg text-[11px] border ${i === numRoomIdx ? "bg-pink-600 border-pink-400" : "bg-slate-900 border-slate-800"}">${escapeHtml(r.name)}</button>`).join("");
      $("num-rooms-list").querySelectorAll("[data-numr]").forEach((b) => { b.onclick = () => { numRoomIdx = Number(b.dataset.numr) || 0; numSecret = Math.floor(Math.random() * numRooms[numRoomIdx].max) + 1; numGuesses = []; renderNumRooms(); }; });
      $("num-room-chat-log").innerHTML = rm.chat.map((c) => `<div class="p-1.5 rounded-lg bg-slate-900/90">${escapeHtml(c)}</div>`).join("");
    }
    $("num-join-room").onclick = () => { numJoined = true; const rm = numRooms[numRoomIdx]; if (!rm.members.includes(me.uid || "me")) rm.members.push(me.uid || "me"); $("num-join-room").classList.add("hidden"); $("num-leave-room").classList.remove("hidden"); renderNumRooms(); };
    $("num-leave-room").onclick = () => { numJoined = false; const rm = numRooms[numRoomIdx]; rm.members = rm.members.filter((x) => x !== (me.uid || "me")); if (!rm.members.length) rm.chat = []; $("num-leave-room").classList.add("hidden"); $("num-join-room").classList.remove("hidden"); renderNumRooms(); };
    $("num-create-room-form").onsubmit = (e) => { e.preventDefault(); const nm = $("num-room-name").value.trim().slice(0, 40) || `חדר ניחושים ${numRooms.length + 1}`; const mx = Math.max(10, Math.min(100, Number($("num-room-max").value) || 100)); numRooms.push({ name: nm, max: mx, members: [], chat: [] }); numRoomIdx = numRooms.length - 1; numSecret = Math.floor(Math.random() * mx) + 1; $("num-room-name").value = ""; renderNumRooms(); };
    $("num-toggle-secret").onclick = () => { $("num-secret-input").type = $("num-secret-input").type === "password" ? "text" : "password"; };
    $("num-set-secret-btn").onclick = () => { const mx = numRooms[numRoomIdx].max; const val = Number($("num-secret-input").value); if (!val || val < 1 || val > mx) return alert(`בחר מספר בין 1 ל-${mx}`); numSecret = val; numGuesses = []; $("num-secret-input").value = ""; $("num-secret-status").textContent = `מספר סודי נקבע (1–${mx})`; };
    $("num-guess-btn").onclick = async () => {
      const g = Number($("num-guess-input").value); if (!g) return;
      $("num-guess-input").value = "";
      const hint = g < numSecret ? "נמוך מדי ⬆️" : g > numSecret ? "גבוה מדי ⬇️" : "פגיעה בול! 🎯";
      numGuesses.unshift(`${escapeHtml(me.name || "שחקן")}: ${g} (${hint})`);
      $("num-guess-feedback").textContent = hint;
      $("num-guesses-log").innerHTML = numGuesses.map((x) => `<div class="p-2 rounded-lg bg-slate-900 border border-slate-800">${x}</div>`).join("");
      if (g === numSecret) { numSecret = Math.floor(Math.random() * numRooms[numRoomIdx].max) + 1; await awardGameWin("number", 30); }
    };
    $("num-declare-winner-btn").onclick = async () => { await awardGameWin("number", 15); $("num-guess-feedback").textContent = "חושבו נקודות בונוס +15!"; };
    $("num-room-chat-form").onsubmit = (e) => { e.preventDefault(); const t = $("num-room-chat-input").value.trim().slice(0, 400); if (!t) return; $("num-room-chat-input").value = ""; numRooms[numRoomIdx].chat.push(`${me.name || "שחקן"}: ${t}`); renderNumRooms(); };

    const rrRooms = Array.from({ length: 20 }, (_, i) => ({ name: `שולחן רולטה ${i + 1}`, seats: ["מושב 1", "מושב 2", "מושב 3", "מושב 4", "מושב 5", "מושב 6"], alive: [true, true, true, true, true, true], chat: [] }));
    let rrRoomIdx = 0, rrChamber = Math.floor(Math.random() * 6), rrTargetIdx = 1, rrJoined = false;
    function renderRoulette() {
      const rm = rrRooms[rrRoomIdx];
      const aliveCount = rm.alive.filter(Boolean).length;
      $("rr-aimed-label").textContent = `${rm.name} • 6 תאים • כוון ל: ${rm.seats[rrTargetIdx]}`;
      $("rr-seats-ring").innerHTML = rm.seats.map((s, i) => `<button type="button" data-rrseat="${i}" class="p-2.5 rounded-xl border text-xs flex items-center justify-between ${rm.alive[i] ? (i === rrTargetIdx ? "bg-amber-600/25 border-amber-400 font-bold" : "bg-slate-900 border-slate-700") : "bg-rose-950/50 border-rose-800 opacity-50 line-through"}"><span>${escapeHtml(s)}</span><span>${rm.alive[i] ? "🎯 ירה" : "פסול"}</span></button>`).join("");
      $("rr-seats-ring").querySelectorAll("[data-rrseat]").forEach((btn) => {
        btn.onclick = async () => {
          if (!rrJoined) return alert("לחץ על כנס לחדר כדי לשחק");
          const idx = Number(btn.dataset.rrseat);
          if (!rm.alive[idx]) return;
          rrTargetIdx = idx;
          $("rr-gun-spinner").style.transform = `rotate(${(idx + 1) * 90 + 360}deg)`;
          if (Math.floor(Math.random() * 6) === rrChamber) {
            rrChamber = Math.floor(Math.random() * 6);
            rm.alive[idx] = false;
            me.rrRewards.goldBalls += 1; me.rrRewards.grandGifts += 1;
            $("rr-confetti-banner").classList.remove("hidden"); setTimeout(() => $("rr-confetti-banner").classList.add("hidden"), 1800);
            const left = rm.alive.filter(Boolean);
            $("rr-status").textContent = left.length <= 1 ? `🏆 ${left[0] ? rm.seats[rm.alive.indexOf(true)] : "השחקן האחרון"} הוא המנצח!` : `💥 ${rm.seats[idx]} נורה וסיים את הסיבוב!`;
            await awardGameWin("roulette", 35);
          } else {
            me.rrRewards.magazines += 1;
            $("rr-status").textContent = `😅 לחיצה ריקה — ${rm.seats[idx]} שרד!`;
            await awardGameWin("roulette", 10);
          }
          renderRoulette();
        };
      });
      $("rr-rooms-grid").innerHTML = rrRooms.map((r, i) => `<button type="button" data-rrr="${i}" class="p-1.5 rounded-lg text-[11px] border ${i === rrRoomIdx ? "bg-pink-600 border-pink-400" : "bg-slate-900 border-slate-800"}">${escapeHtml(r.name)}</button>`).join("");
      $("rr-rooms-grid").querySelectorAll("[data-rrr]").forEach((b) => { b.onclick = () => { rrRoomIdx = Number(b.dataset.rrr) || 0; renderRoulette(); }; });
      $("rr-room-chat-log").innerHTML = rm.chat.map((c) => `<div class="p-1.5 rounded-lg bg-slate-900/90">${escapeHtml(c)}</div>`).join("");
      if (aliveCount === 1) $("rr-status").textContent = `🏆 נשאר שחקן אחד — ${rm.seats[rm.alive.indexOf(true)]} המנצח!`;
    }
    $("rr-join-btn").onclick = () => { rrJoined = true; $("rr-join-btn").classList.add("hidden"); $("rr-leave-btn").classList.remove("hidden"); $("rr-status").textContent = "נכנסת לשולחן העגול — בחר משתמש לירי"; };
    $("rr-leave-btn").onclick = () => { rrJoined = false; rrRooms[rrRoomIdx].chat = []; $("rr-leave-btn").classList.add("hidden"); $("rr-join-btn").classList.remove("hidden"); renderRoulette(); };
    $("rr-add-room").onclick = () => { rrRooms.push({ name: `שולחן רולטה ${rrRooms.length + 1}`, seats: ["מושב 1", "מושב 2", "מושב 3", "מושב 4", "מושב 5", "מושב 6"], alive: [true, true, true, true, true, true], chat: [] }); rrRoomIdx = rrRooms.length - 1; renderRoulette(); };
    $("rr-room-chat-form").onsubmit = (e) => { e.preventDefault(); const t = $("rr-room-chat-input").value.trim().slice(0, 400); if (!t) return; $("rr-room-chat-input").value = ""; rrRooms[rrRoomIdx].chat.push(`${me.name || "שחקן"}: ${t}`); renderRoulette(); };

    function getFilteredUsers() {
      const lf = $("filter-looking-for").value, dist = $("filter-distance").value;
      const loc = $("filter-location").value.trim().toLowerCase(), minA = Number($("filter-min-age").value) || 18, maxA = Number($("filter-max-age").value) || 80;
      return allUsers.filter((u) => {
        const age = Number(u.age) || 25;
        if (age < minA || age > maxA) return false;
        if (loc && !String(u.location || "").toLowerCase().includes(loc)) return false;
        if (dist !== "all" && Number(u.distanceKm || 0) > Number(dist)) return false;
        if (lf === "preferred" && me.lookingFor && me.lookingFor !== "הכל") return u.gender === me.lookingFor;
        return (lf === "preferred" || lf === "all") ? true : u.gender === lf;
      });
    }
    function renderRealUsers() {
      const pool = getFilteredUsers();
      $("real-users-grid").innerHTML = pool.length ? pool.map((u) => `<div class="bg-slate-900/85 border border-slate-700 rounded-2xl p-4 space-y-2"><div class="font-bold text-sm">${escapeHtml(u.name || "משתמש")} • גיל ${Number(u.age) || 25}</div><div class="text-xs text-slate-300">${escapeHtml(u.location || "")} ${u.distanceKm !== undefined ? `• ${Number(u.distanceKm)} ק״מ` : ""}</div><button type="button" data-open-id="${escapeHtml(u.uid || u.id || "")}" class="px-3 py-1.5 rounded-lg bg-pink-600 text-xs font-bold">פתח כרטיס</button></div>`).join("") : `<p class="text-xs text-slate-400 col-span-full">אין פרופילים רשומים התואמים לסינון כרגע.</p>`;
      document.querySelectorAll("[data-open-id]").forEach((b) => { b.onclick = () => { const f = pool.find((x) => (x.uid || x.id) === b.dataset.openId); if (f) openUserModal(f); }; });
      $("match-deck-counter").textContent = `${pool.length} פרופילים`;
      const cur = pool.length ? pool[deckIdx % pool.length] : null;
      $("match-deck-card").innerHTML = cur ? `<div class="font-bold">${escapeHtml(cur.name)} • גיל ${Number(cur.age) || 25}</div><div class="text-xs text-slate-300">${escapeHtml(cur.tagline || "")}</div>` : `<div class="text-xs text-slate-400">אין כרטיסים להצגה</div>`;
    }
    ["filter-looking-for", "filter-distance", "filter-location", "filter-min-age", "filter-max-age"].forEach((id) => { $(id).addEventListener("input", renderRealUsers); $(id).addEventListener("change", renderRealUsers); });
    $("deck-skip-btn").onclick = () => { deckIdx += 1; renderRealUsers(); };
    $("deck-like-btn").onclick = () => { const pool = getFilteredUsers(), cur = pool[deckIdx % pool.length]; if (cur) openUserModal(cur); };
    $("deck-follow-btn").onclick = async () => {
      const pool = getFilteredUsers(), cur = pool[deckIdx % pool.length]; if (!cur) return;
      const tid = cur.uid || cur.id; if (!tid || tid === me.uid) return;
      me.following = me.following || []; if (!me.following.includes(tid)) me.following.push(tid);
      localStorage.setItem("toplove_session", JSON.stringify(me));
      try { if (db && me.uid) await setDoc(doc(db, "users", me.uid), { following: me.following }, { merge: true }); } catch {}
      syncHeaderUserBadge();
    };
    $("toggle-password-btn").onclick = () => { $("auth-password").type = $("auth-password").type === "password" ? "text" : "password"; };

    function openApp(session) {
      Object.assign(me, session);
      $("auth-section").classList.add("hidden"); $("app-section").classList.remove("hidden");
      $("user-profile-trigger").classList.remove("hidden"); $("user-profile-trigger").classList.add("flex");
      $("logout-btn").classList.remove("hidden");
      syncHeaderUserBadge(); renderQuestionnaireOptions(); applyProfileViewMode();
      renderGameStatsAndTop5("ttt"); renderTtt(); renderRps(); buildMemoryBoard(); renderMemRooms(); renderNumRooms(); renderRoulette();
      subscribeAllRooms(); subscribeRealUsers(); renderRooms(); renderRealUsers();
    }
    $("auth-form").onsubmit = async (e) => {
      e.preventDefault();
      const email = $("auth-email").value.trim().toLowerCase(), password = $("auth-password").value, age = Number($("auth-age").value), lookingFor = $("auth-looking-for").value;
      if (!age || age < 18 || age > 80) { $("auth-error").textContent = "גילאי 18 עד 80 בלבד."; $("auth-error").classList.remove("hidden"); return; }
      $("auth-error").classList.add("hidden");
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
    $("logout-btn").onclick = async () => {
      try { if (unsubMsgs) unsubMsgs(); if (unsubRooms) unsubRooms(); if (unsubUsers) unsubUsers(); } catch {}
      try { if (auth) await signOut(auth); } catch {}
      localStorage.removeItem("toplove_session"); location.reload();
    };
    const savedSession = localStorage.getItem("toplove_session");
    if (savedSession) { try { openApp(JSON.parse(savedSession)); } catch {} }
  </script>
</body>
</html>
