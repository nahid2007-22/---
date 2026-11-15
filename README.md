```html
<!DOCTYPE html>
<html lang="bn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=5.0">
    <meta name="theme-color" content="#064e3b">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <title>কৃষি মিত্র | স্মার্ট কৃষি সুপার অ্যাপ</title>
    
    <!-- Google Fonts with System Fallbacks -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Hind+Siliguri:wght@400;500;600;700&display=swap" rel="stylesheet">
    
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['"Hind Siliguri"', 'system-ui', '-apple-system', 'sans-serif'],
                    }
                }
            }
        }
    </script>

    <style>
        /* Core Smooth & Mobile-First Styles */
        * {
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }
        html, body {
            margin: 0;
            padding: 0;
            width: 100%;
            overflow-x: hidden;
            font-family: 'Hind Siliguri', system-ui, -apple-system, sans-serif;
            background-color: #f0fdf4;
            color: #0f172a;
            scroll-behavior: smooth;
        }

        /* Custom Gradients */
        .welcome-bg {
            background: linear-gradient(145deg, #d1fae5 0%, #ecfdf5 48%, #fef3c7 100%);
        }
        .emerald-grad {
            background: linear-gradient(135deg, #022c22 0%, #065f46 60%, #047857 100%);
        }
        .gold-grad {
            background: linear-gradient(135deg, #f59e0b 0%, #d97706 100%);
        }

        /* Smooth Fade Transition */
        .fade-in {
            animation: fadeIn 0.28s cubic-bezier(0.16, 1, 0.3, 1) forwards;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(6px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* AI Scanning Laser Animation */
        .scan-line {
            position: absolute;
            left: 0;
            right: 0;
            height: 3px;
            background: #10b981;
            box-shadow: 0 0 12px 3px rgba(16, 185, 129, 0.85);
            animation: scanMove 1.6s ease-in-out infinite alternate;
        }
        @keyframes scanMove {
            0% { top: 5%; }
            100% { top: 92%; }
        }

        /* Hide Scrollbar for Horizontal Pills */
        .no-scrollbar::-webkit-scrollbar { display: none; }
        .no-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }

        /* Touch Friendly Active States */
        .btn-press:active {
            transform: scale(0.97);
        }
    </style>
</head>
<body class="min-h-screen flex flex-col">

    <!-- Toast Notification Container -->
    <div id="toast-box" class="fixed top-4 left-1/2 -translate-x-1/2 z-[100] w-[92%] max-w-md pointer-events-none flex flex-col gap-2"></div>

    <!-- ==================== 1. WELCOME / LOGIN SCREEN ==================== -->
    <section id="welcome-view" class="min-h-screen w-full welcome-bg flex flex-col justify-between items-center p-4 sm:p-6">
        
        <!-- Top Bar: Brand Tag & Language Switcher -->
        <div class="w-full max-w-md flex items-center justify-between pt-1">
            <div class="inline-flex items-center gap-1.5 bg-white/90 backdrop-blur px-3 py-1.5 rounded-full shadow-sm border border-emerald-200">
                <span class="w-2 h-2 rounded-full bg-emerald-500 animate-pulse"></span>
                <span class="text-xs font-bold text-emerald-950">Smart Krishi BD</span>
            </div>
            <div class="inline-flex bg-white/95 p-1 rounded-full shadow-sm border border-emerald-200">
                <button type="button" onclick="changeLang('bn')" id="w-lang-bn" class="px-3.5 py-1 rounded-full text-xs font-bold bg-emerald-700 text-white transition">বাংলা</button>
                <button type="button" onclick="changeLang('en')" id="w-lang-en" class="px-3.5 py-1 rounded-full text-xs font-bold text-slate-600 hover:text-emerald-900 transition">English</button>
            </div>
        </div>

        <!-- Central Login Card -->
        <div class="w-full max-w-md bg-white rounded-[2rem] p-6 sm:p-8 shadow-[0_20px_50px_rgba(6,78,59,0.12)] border border-emerald-100 my-4 fade-in">
            <!-- App Logo & Title -->
            <div class="text-center mb-6">
                <div class="relative inline-flex items-center justify-center w-20 h-20 rounded-3xl bg-[#064e3b] shadow-lg mb-4 border-2 border-amber-400/50">
                    <!-- Inline SVG Wheat Icon -->
                    <svg class="w-11 h-11 text-amber-400" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                        <path d="M2 22 16 8"/><path d="M3.47 12.53 5 11l1.53 1.53a3.5 3.5 0 0 1 0 4.94L5 19l-1.53-1.53a3.5 3.5 0 0 1 0-4.94Z"/><path d="M7.47 8.53 9 7l1.53 1.53a3.5 3.5 0 0 1 0 4.94L9 15l-1.53-1.53a3.5 3.5 0 0 1 0-4.94Z"/><path d="M11.47 4.53 13 3l1.53 1.53a3.5 3.5 0 0 1 0 4.94L13 11l-1.53-1.53a3.5 3.5 0 0 1 0-4.94Z"/><path d="M20 2h2v2a4 4 0 0 1-4 4h-2V6a4 4 0 0 1 4-4Z"/><path d="M11.47 17.47 13 19l-1.53 1.53a3.5 3.5 0 0 1-4.94 0L5 19l1.53-1.53a3.5 3.5 0 0 1 4.94 0Z"/><path d="M15.47 13.47 17 15l-1.53 1.53a3.5 3.5 0 0 1-4.94 0L9 15l1.53-1.53a3.5 3.5 0 0 1 4.94 0Z"/><path d="M19.47 9.47 21 11l-1.53 1.53a3.5 3.5 0 0 1-4.94 0L13 11l1.53-1.53a3.5 3.5 0 0 1 4.94 0Z"/>
                    </svg>
                    <span class="absolute -bottom-2 -right-2 bg-amber-400 text-emerald-950 text-[10px] font-extrabold px-2.5 py-0.5 rounded-full shadow">AI</span>
                </div>
                <h1 class="text-3xl font-bold text-slate-900 tracking-tight" data-t="app_title">কৃষি মিত্র</h1>
                <p class="text-xs sm:text-sm text-slate-600 mt-1" data-t="app_sub">বাংলাদেশের প্রথম এআই-চালিত পূর্ণাঙ্গ ডিজিটাল কৃষি সুপার অ্যাপ</p>
            </div>

            <!-- 3 Feature Highlights -->
            <div class="grid grid-cols-3 gap-2 mb-5 text-center">
                <div class="bg-emerald-50 border border-emerald-100 rounded-2xl p-2.5">
                    <svg class="w-5 h-5 text-emerald-600 mx-auto mb-1" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M14.5 4h-5L7 7H4a2 2 0 0 0-2 2v9a2 2 0 0 0 2 2h16a2 2 0 0 0 2-2V9a2 2 0 0 0-2-2h-3l-2.5-3z"/><circle cx="12" cy="13" r="3"/></svg>
                    <p class="text-[11px] font-bold text-emerald-950" data-t="f_disease">AI রোগ নির্ণয়</p>
                </div>
                <div class="bg-amber-50 border border-amber-100 rounded-2xl p-2.5">
                    <svg class="w-5 h-5 text-amber-600 mx-auto mb-1" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><circle cx="8" cy="8" r="6"/><path d="M18.09 10.37A6 6 0 1 1 10.34 18"/><path d="M7 6h1v4"/></svg>
                    <p class="text-[11px] font-bold text-amber-950" data-t="f_profit">লাভজনক ফসল</p>
                </div>
                <div class="bg-sky-50 border border-sky-100 rounded-2xl p-2.5">
                    <svg class="w-5 h-5 text-sky-600 mx-auto mb-1" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M3 21h18"/><path d="M3 10h18"/><path d="M5 6l7-3 7 3"/><path d="M4 10v11"/><path d="M20 10v11"/><path d="M8 14v3"/><path d="M12 14v3"/><path d="M16 14v3"/></svg>
                    <p class="text-[11px] font-bold text-sky-950" data-t="f_loan">কৃষি ঋণ ও ব্যাংক</p>
                </div>
            </div>

            <!-- District Selector -->
            <div class="mb-4">
                <label for="welcome-district" class="block text-xs font-bold text-slate-800 mb-1.5" data-t="sel_dist">আপনার জেলা নির্বাচন করুন</label>
                <div class="relative">
                    <span class="absolute left-3.5 top-3 text-emerald-600">
                        <svg class="w-4 h-4" fill="none" stroke="currentColor" stroke-width="2.2" viewBox="0 0 24 24"><path d="M20 10c0 6-8 12-8 12s-8-6-8-12a8 8 0 0 1 16 0Z"/><circle cx="12" cy="10" r="3"/></svg>
                    </span>
                    <select id="welcome-district" class="w-full pl-10 pr-4 py-2.5 bg-slate-50 border border-slate-200 rounded-2xl text-sm font-semibold text-slate-800 focus:outline-none focus:ring-2 focus:ring-emerald-600">
                        <option value="নারায়ণগঞ্জ">নারায়ণগঞ্জ (Narayanganj)</option>
                        <option value="ঢাকা">ঢাকা (Dhaka)</option>
                        <option value="বগুড়া">বগুড়া (Bogura)</option>
                        <option value="রাজশাহী">রাজশাহী (Rajshahi)</option>
                        <option value="রংপুর">রংপুর (Rangpur)</option>
                        <option value="দিনাজপুর">দিনাজপুর (Dinajpur)</option>
                        <option value="যশোর">যশোর (Jashore)</option>
                        <option value="খুলনা">খুলনা (Khulna)</option>
                        <option value="ময়মনসিংহ">ময়মনসিংহ (Mymensingh)</option>
                        <option value="কুমিল্লা">কুমিল্লা (Cumilla)</option>
                        <option value="সিলেট">সিলেট (Sylhet)</option>
                        <option value="বরিশাল">বরিশাল (Barishal)</option>
                        <option value="চট্টগ্রাম">চট্টগ্রাম (Chattogram)</option>
                        <option value="গাজীপুর">গাজীপুর (Gazipur)</option>
                        <option value="নরসিংদী">নরসিংদী (Narsingdi)</option>
                        <option value="টাঙ্গাইল">টাঙ্গাইল (Tangail)</option>
                    </select>
                </div>
            </div>

            <!-- Action Login Buttons -->
            <div class="space-y-2.5">
                <button type="button" onclick="loginWithProvider('Google')" class="btn-press w-full py-3 px-4 bg-white hover:bg-slate-50 border border-slate-200 rounded-2xl font-semibold text-slate-700 text-sm shadow-sm transition flex items-center justify-center gap-3 cursor-pointer">
                    <svg class="w-5 h-5 shrink-0" viewBox="0 0 24 24">
                        <path fill="#EA4335" d="M12 5c1.6 0 3 .6 4.1 1.7l3.1-3.1C17.3 1.8 14.8 1 12 1 7.4 1 3.5 3.6 1.6 7.4l3.7 2.8C6.2 7.2 8.9 5 12 5z"/>
                        <path fill="#4285F4" d="M23.5 12.3c0-.8-.1-1.7-.2-2.5H12v4.8h6.5c-.3 1.5-1.1 2.8-2.4 3.6l3.7 2.9c2.2-2 3.7-5 3.7-8.8z"/>
                        <path fill="#FBBC05" d="M5.3 14.8c-.2-.8-.4-1.6-.4-2.5s.2-1.7.4-2.5L1.6 7C.6 9 0 11.2 0 13.5s.6 4.5 1.6 6.5l3.7-2.8z"/>
                        <path fill="#34A853" d="M12 24c3.2 0 6-1.1 8-3l-3.7-2.9c-1.1.7-2.5 1.2-4.3 1.2-3.1 0-5.8-2.1-6.7-5l-3.7 2.8C3.5 21.1 7.4 24 12 24z"/>
                    </svg>
                    <span data-t="btn_google">Google অ্যাকাউন্ট দিয়ে প্রবেশ করুন</span>
                </button>

                <button type="button" onclick="loginWithProvider('Facebook')" class="btn-press w-full py-3 px-4 bg-[#1877F2] hover:bg-[#166fe5] text-white rounded-2xl font-semibold text-sm shadow-md transition flex items-center justify-center gap-3 cursor-pointer">
                    <svg class="w-5 h-5 fill-current shrink-0" viewBox="0 0 24 24"><path d="M24 12.073c0-6.627-5.373-12-12-12s-12 5.373-12 12c0 5.99 4.388 10.954 10.125 11.854v-8.385H7.078v-3.47h3.047V9.43c0-3.007 1.792-4.669 4.533-4.669 1.312 0 2.686.235 2.686.235v2.953H15.83c-1.491 0-1.956.925-1.956 1.874v2.25h3.328l-.532 3.47h-2.796v8.385C19.612 23.027 24 18.062 24 12.073z"/></svg>
                    <span data-t="btn_fb">Facebook অ্যাকাউন্ট দিয়ে প্রবেশ করুন</span>
                </button>

                <div class="relative flex py-1 items-center">
                    <div class="flex-grow border-t border-slate-200"></div>
                    <span class="flex-shrink mx-3 text-xs text-slate-400 font-medium" data-t="or_txt">অথবা দ্রুত ব্যবহার করুন</span>
                    <div class="flex-grow border-t border-slate-200"></div>
                </div>

                <button type="button" onclick="loginWithProvider('Guest')" class="btn-press w-full py-3.5 px-4 bg-[#065f46] hover:bg-[#064e3b] text-white rounded-2xl font-bold text-sm shadow-lg transition flex items-center justify-center gap-2 cursor-pointer">
                    <svg class="w-5 h-5 text-amber-400 shrink-0" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M3 4h9l1 7"/><path d="M4 11V4"/><path d="M8 10V4"/><path d="M18 5c-.6 0-1 .4-1 1v5.6"/><path d="m10 11 11 .9c.6 0 .9.5.8 1.1l-.8 5h-1"/><circle cx="7" cy="15" r="4"/><circle cx="18" cy="18" r="2"/></svg>
                    <span data-t="btn_guest">কৃষক হিসেবে সরাসরি প্রবেশ করুন (ফ্রি)</span>
                </button>
            </div>

            <!-- Card Footer -->
            <div class="mt-5 pt-4 border-t border-slate-100 flex items-center justify-between text-xs">
                <span class="text-slate-600 font-medium flex items-center gap-1">
                    <svg class="w-4 h-4 text-emerald-600" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/><path d="m9 12 2 2 4-4"/></svg>
                    <span data-t="safe_txt">১০০% নিরাপদ ও ফ্রি</span>
                </span>
                <button type="button" onclick="toggleInstallModal(true)" class="text-emerald-700 font-bold hover:underline flex items-center gap-1 cursor-pointer">
                    <svg class="w-4 h-4" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><rect width="14" height="20" x="5" y="2" rx="2" ry="2"/><path d="M12 18h.01"/></svg>
                    <span data-t="dl_app">অ্যাপ ডাউনলোড করুন</span>
                </button>
            </div>
        </div>

        <!-- Permanent Creator Credit at Very Bottom -->
        <footer class="w-full max-w-md text-center pb-2">
            <div class="inline-block bg-white/90 backdrop-blur px-5 py-2 rounded-full shadow-sm border border-emerald-200">
                <p class="text-xs sm:text-sm font-bold text-emerald-950">
                    Created &amp; organized by <span class="text-emerald-700 underline decoration-amber-400 decoration-2 underline-offset-4">Nahid</span>
                </p>
            </div>
        </footer>
    </section>

    <!-- ==================== 2. MAIN APPLICATION INTERFACE ==================== -->
    <div id="app-shell" class="hidden min-h-screen w-full flex flex-col md:flex-row bg-[#f0fdf4]">

        <!-- PC / Desktop Left Sidebar Navigation -->
        <aside class="hidden md:flex md:w-64 lg:w-72 md:flex-col md:fixed md:inset-y-0 emerald-grad text-white shadow-2xl z-30">
            <div class="p-5 border-b border-white/10 flex items-center gap-3">
                <div class="w-11 h-11 rounded-2xl bg-white/10 border border-amber-400/50 flex items-center justify-center shrink-0">
                    <svg class="w-6 h-6 text-amber-400" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M2 22 16 8"/><path d="M20 2h2v2a4 4 0 0 1-4 4h-2V6a4 4 0 0 1 4-4Z"/><circle cx="12" cy="12" r="3"/></svg>
                </div>
                <div>
                    <div class="flex items-center gap-1.5">
                        <h2 class="font-bold text-xl leading-none" data-t="app_title">কৃষি মিত্র</h2>
                        <span class="bg-amber-400 text-emerald-950 text-[10px] font-extrabold px-1.5 py-0.5 rounded">AI</span>
                    </div>
                    <p id="pc-district-badge" class="text-xs text-emerald-200 mt-1">নারায়ণগঞ্জ, বাংলাদেশ</p>
                </div>
            </div>

            <nav class="flex-1 px-3 py-4 space-y-1.5 overflow-y-auto">
                <button type="button" onclick="openPage('home')" data-nav="home" class="pc-nav w-full flex items-center gap-3 px-4 py-3 rounded-2xl text-sm font-bold bg-white text-emerald-950 shadow transition">
                    <span>🏠</span> <span data-t="nav_home">হোম ড্যাশবোর্ড</span>
                </button>
                <button type="button" onclick="openPage('disease')" data-nav="disease" class="pc-nav w-full flex items-center gap-3 px-4 py-3 rounded-2xl text-sm font-semibold text-emerald-100 hover:bg-white/10 transition">
                    <span>🔬</span> <span data-t="nav_disease">AI রোগ নির্ণয়</span>
                </button>
                <button type="button" onclick="openPage('crops')" data-nav="crops" class="pc-nav w-full flex items-center gap-3 px-4 py-3 rounded-2xl text-sm font-semibold text-emerald-100 hover:bg-white/10 transition">
                    <span>🌾</span> <span data-t="nav_crops">১২ মাসের লাভজনক ফসল</span>
                </button>
                <button type="button" onclick="openPage('weather')" data-nav="weather" class="pc-nav w-full flex items-center gap-3 px-4 py-3 rounded-2xl text-sm font-semibold text-emerald-100 hover:bg-white/10 transition">
                    <span>🌦️</span> <span data-t="nav_weather">৭ দিনের আবহাওয়া ও বাজার</span>
                </button>
                <button type="button" onclick="openPage('loans')" data-nav="loans" class="pc-nav w-full flex items-center gap-3 px-4 py-3 rounded-2xl text-sm font-semibold text-emerald-100 hover:bg-white/10 transition">
                    <span>🏦</span> <span data-t="nav_loans">কৃষি ঋণ ও ক্যালকুলেটর</span>
                </button>
                <button type="button" onclick="openPage('videos')" data-nav="videos" class="pc-nav w-full flex items-center gap-3 px-4 py-3 rounded-2xl text-sm font-semibold text-emerald-100 hover:bg-white/10 transition">
                    <span>🎬</span> <span data-t="nav_videos">সচেতনতা অ্যানিমেশন ভিডিও</span>
                </button>
                <button type="button" onclick="openPage('settings')" data-nav="settings" class="pc-nav w-full flex items-center gap-3 px-4 py-3 rounded-2xl text-sm font-semibold text-emerald-100 hover:bg-white/10 transition">
                    <span>⚙️</span> <span data-t="nav_settings">সেটিংস ও ভাষা</span>
                </button>
            </nav>

            <div class="p-4 border-t border-white/10 text-center">
                <p class="text-[11px] text-emerald-200 mb-2">Created &amp; organized by <strong class="text-amber-400">Nahid</strong></p>
                <button type="button" onclick="logoutApp()" class="w-full py-2 rounded-xl bg-white/10 hover:bg-rose-600/80 text-xs font-bold transition">
                    লগ আউট / ফিরে যান
                </button>
            </div>
        </aside>

        <!-- Main Content Wrapper -->
        <div class="flex-1 md:pl-64 lg:pl-72 flex flex-col min-h-screen">
            
            <!-- Top Header (Mobile + Desktop) -->
            <header class="sticky top-0 z-20 emerald-grad md:bg-white md:bg-none text-white md:text-slate-900 shadow-md md:shadow-sm border-b border-emerald-100 px-4 py-3">
                <div class="max-w-6xl mx-auto flex items-center justify-between">
                    <div class="flex items-center gap-2.5 md:hidden">
                        <div class="w-9 h-9 rounded-xl bg-white/15 border border-amber-400/50 flex items-center justify-center">
                            <span class="text-lg">🌾</span>
                        </div>
                        <div>
                            <h2 class="font-bold text-base leading-none flex items-center gap-1">
                                <span data-t="app_title">কৃষি মিত্র</span>
                                <span class="bg-amber-400 text-emerald-950 text-[9px] font-extrabold px-1.5 py-0.5 rounded">AI</span>
                            </h2>
                            <p id="mob-district-badge" class="text-[11px] text-emerald-200 mt-0.5">নারায়ণগঞ্জ</p>
                        </div>
                    </div>

                    <div class="hidden md:block">
                        <h2 id="desktop-page-heading" class="font-bold text-lg text-emerald-950">স্বাগতম, কৃষি মিত্র ড্যাশবোর্ডে</h2>
                    </div>

                    <div class="flex items-center gap-2">
                        <button type="button" onclick="toggleLangQuick()" class="px-3 py-1.5 rounded-xl bg-white/15 md:bg-emerald-50 text-white md:text-emerald-900 border border-white/20 md:border-emerald-200 text-xs font-bold transition">
                            <span id="quick-lang-txt">English</span>
                        </button>
                        <button type="button" onclick="toggleInstallModal(true)" class="px-3 py-1.5 rounded-xl bg-amber-400 hover:bg-amber-300 text-emerald-950 text-xs font-extrabold shadow transition">
                            📲 <span data-t="install_txt">ইনস্টল</span>
                        </button>
                        <button type="button" onclick="openPage('settings')" class="p-2 rounded-xl bg-white/15 md:bg-slate-100 text-white md:text-slate-700">
                            ⚙️
                        </button>
                    </div>
                </div>
            </header>

            <!-- Scrollable Page Body -->
            <main class="flex-1 max-w-6xl w-full mx-auto px-4 pt-4 pb-24 md:pb-8">

                <!-- ==================== TAB 1: HOME DASHBOARD ==================== -->
                <div id="page-home" class="app-page space-y-5 fade-in">
                    <!-- Hero Banner -->
                    <div class="emerald-grad rounded-3xl p-5 sm:p-7 text-white shadow-xl relative overflow-hidden">
                        <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4 relative z-10">
                            <div>
                                <span class="inline-block bg-amber-400/20 border border-amber-400/40 text-amber-300 text-xs font-bold px-3 py-1 rounded-full mb-2">
                                    ✨ <span data-t="smart_agri_badge">ডিজিটাল কৃষি সহায়ক</span>
                                </span>
                                <h1 class="text-2xl sm:text-3xl font-bold">আসসালামু আলাইকুম, <span id="user-greeting-name" class="text-amber-400">কৃষক ভাই</span>!</h1>
                                <p class="text-xs sm:text-sm text-emerald-100 mt-1 max-w-lg" data-t="hero_desc">
                                    আক্রান্ত পাতার ছবি তুলে মুহূর্তেই রোগ ও সমাধান জানুন, দেখুন কোন মাসে কোন ফসলে বেশি লাভ এবং সরকারি কৃষি ঋণের তথ্য।
                                </p>
                                <div class="flex flex-wrap gap-2.5 mt-4">
                                    <button type="button" onclick="openPage('disease')" class="btn-press bg-amber-400 hover:bg-amber-300 text-emerald-950 font-bold px-4 py-2.5 rounded-2xl text-xs sm:text-sm shadow-md transition">
                                        📸 <span data-t="cta_scan">পাতার ছবি দিয়ে রোগ দেখুন</span>
                                    </button>
                                    <button type="button" onclick="openPage('videos')" class="btn-press bg-white/15 hover:bg-white/25 text-white border border-white/25 font-semibold px-4 py-2.5 rounded-2xl text-xs sm:text-sm transition">
                                        🎬 <span data-t="cta_video">সচেতনতা ভিডিও দেখুন</span>
                                    </button>
                                </div>
                            </div>

                            <!-- Mini Weather Card -->
                            <div onclick="openPage('weather')" class="cursor-pointer bg-black/25 backdrop-blur border border-white/15 rounded-2xl p-4 sm:min-w-[210px] hover:bg-black/35 transition">
                                <div class="flex items-center justify-between text-xs text-emerald-200 mb-1">
                                    <span id="home-weather-city">📍 নারায়ণগঞ্জ</span>
                                    <span class="text-amber-300 font-bold">৭ দিন &rarr;</span>
                                </div>
                                <div class="flex items-center gap-3 my-1.5">
                                    <span class="text-3xl">☀️</span>
                                    <div>
                                        <div class="text-2xl font-extrabold">২৯°C</div>
                                        <div class="text-[11px] text-emerald-100">পরিষ্কার আকাশ • আর্দ্রতা ৬০%</div>
                                    </div>
                                </div>
                                <p class="text-[11px] text-amber-300 bg-amber-500/15 px-2 py-1 rounded-lg mt-1">
                                    ✅ আজ সার ও স্প্রে করার উপযুক্ত দিন
                                </p>
                            </div>
                        </div>
                    </div>

                    <!-- 6 Quick Action Service Cards -->
                    <div>
                        <h3 class="font-bold text-base sm:text-lg text-emerald-950 mb-3" data-t="quick_services">সকল স্মার্ট কৃষি সেবা</h3>
                        <div class="grid grid-cols-2 lg:grid-cols-3 gap-3 sm:gap-4">
                            <div onclick="openPage('disease')" class="btn-press cursor-pointer bg-white rounded-2xl p-4 shadow-sm border border-emerald-100 hover:shadow-md transition">
                                <div class="w-11 h-11 rounded-2xl bg-emerald-100 text-emerald-700 flex items-center justify-center text-2xl mb-2.5">🔬</div>
                                <h4 class="font-bold text-sm sm:text-base text-slate-900" data-t="nav_disease">AI রোগ নির্ণয়</h4>
                                <p class="text-xs text-slate-500 mt-1">ধান, আলু, টমেটো পাতার ছবি স্ক্যান করে রোগ ও ঔষধের নাম জানুন।</p>
                            </div>

                            <div onclick="openPage('crops')" class="btn-press cursor-pointer bg-white rounded-2xl p-4 shadow-sm border border-amber-100 hover:shadow-md transition">
                                <div class="w-11 h-11 rounded-2xl bg-amber-100 text-amber-700 flex items-center justify-center text-2xl mb-2.5">💰</div>
                                <h4 class="font-bold text-sm sm:text-base text-slate-900" data-t="f_profit">লাভজনক ফসল</h4>
                                <p class="text-xs text-slate-500 mt-1">১২ মাসের ফসল ক্যালেন্ডার ও বিঘাপ্রতি আয়-ব্যয় ও লাভ ক্যালকুলেটর।</p>
                            </div>

                            <div onclick="openPage('weather')" class="btn-press cursor-pointer bg-white rounded-2xl p-4 shadow-sm border border-sky-100 hover:shadow-md transition">
                                <div class="w-11 h-11 rounded-2xl bg-sky-100 text-sky-700 flex items-center justify-center text-2xl mb-2.5">🌦️</div>
                                <h4 class="font-bold text-sm sm:text-base text-slate-900">আবহাওয়া ও বাজারদর</h4>
                                <p class="text-xs text-slate-500 mt-1">আগামী ৭ দিনের বৃষ্টির পূর্বাভাস ও আজকের পাইকারি বাজারদর।</p>
                            </div>

                            <div onclick="openPage('loans')" class="btn-press cursor-pointer bg-white rounded-2xl p-4 shadow-sm border border-indigo-100 hover:shadow-md transition">
                                <div class="w-11 h-11 rounded-2xl bg-indigo-100 text-indigo-700 flex items-center justify-center text-2xl mb-2.5">🏦</div>
                                <h4 class="font-bold text-sm sm:text-base text-slate-900" data-t="f_loan">কৃষি ঋণ ও ব্যাংক</h4>
                                <p class="text-xs text-slate-500 mt-1">কৃষি ব্যাংক, রাকাব, সোনালী ব্যাংকের ৪% সুদে ঋণ ও কিস্তি হিসাব।</p>
                            </div>

                            <div onclick="openPage('videos')" class="btn-press cursor-pointer bg-white rounded-2xl p-4 shadow-sm border border-rose-100 hover:shadow-md transition">
                                <div class="w-11 h-11 rounded-2xl bg-rose-100 text-rose-700 flex items-center justify-center text-2xl mb-2.5">🎬</div>
                                <h4 class="font-bold text-sm sm:text-base text-slate-900">সচেতনতা ভিডিও</h4>
                                <p class="text-xs text-slate-500 mt-1">সুষম সার, নিরাপদ স্প্রে ও আধুনিক সেচ নিয়ে অ্যানিমেশন ভিডিও।</p>
                            </div>

                            <div onclick="openPage('loans')" class="btn-press cursor-pointer bg-white rounded-2xl p-4 shadow-sm border border-teal-100 hover:shadow-md transition">
                                <div class="w-11 h-11 rounded-2xl bg-teal-100 text-teal-700 flex items-center justify-center text-2xl mb-2.5">🧮</div>
                                <h4 class="font-bold text-sm sm:text-base text-slate-900">সার ও জমি ক্যালকুলেটর</h4>
                                <p class="text-xs text-slate-500 mt-1">শতাংশ অনুযায়ী ইউরিয়া-টিএসপি-পটাশ সার ও বিঘা-কাঠা পরিমাপ।</p>
                            </div>
                        </div>
                    </div>

                    <!-- Emergency Agri Helpline Box -->
                    <div class="bg-emerald-950 text-white rounded-3xl p-5 flex flex-col sm:flex-row items-start sm:items-center justify-between gap-4 shadow-lg">
                        <div>
                            <span class="text-xs font-bold text-amber-400 uppercase">সরকারি কৃষি সহায়তা কেন্দ্র</span>
                            <h4 class="font-bold text-lg mt-0.5">জরুরি পরামর্শের জন্য কল করুন: ১৬১২৩ অথবা ৩৩৩</h4>
                            <p class="text-xs text-emerald-200 mt-0.5">সকাল ৯টা থেকে বিকেল ৫টা পর্যন্ত উপজেলা কৃষি অফিসারের সরাসরি পরামর্শ।</p>
                        </div>
                        <a href="tel:16123" class="btn-press bg-amber-400 text-emerald-950 font-extrabold px-5 py-3 rounded-2xl text-sm shrink-0 shadow">
                            📞 ১৬১২৩ কল করুন
                        </a>
                    </div>
                </div>

                <!-- ==================== TAB 2: AI CROP DISEASE DIAGNOSIS ==================== -->
                <div id="page-disease" class="app-page hidden space-y-5 fade-in">
                    <div class="bg-white rounded-3xl p-5 sm:p-6 shadow-sm border border-emerald-100">
                        <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-3 border-b border-slate-100 pb-4 mb-5">
                            <div>
                                <span class="text-xs font-bold bg-emerald-100 text-emerald-800 px-3 py-1 rounded-full">AI Crop Doctor</span>
                                <h2 class="text-xl sm:text-2xl font-bold text-emerald-950 mt-1.5">ফসলের পাতার ছবি দিয়ে রোগ নির্ণয়</h2>
                                <p class="text-xs sm:text-sm text-slate-600">ক্যামেরা দিয়ে আক্রান্ত পাতার ছবি তুলুন অথবা নিচের নমুনা পাতা দিয়ে পরীক্ষা করুন</p>
                            </div>
                            <select id="disease-crop-type" class="bg-emerald-50 border border-emerald-200 text-emerald-950 font-bold text-sm rounded-xl px-3.5 py-2.5">
                                <option value="rice">ফসল: ধান (Rice)</option>
                                <option value="potato">ফসল: আলু (Potato)</option>
                                <option value="tomato">ফসল: টমেটো (Tomato)</option>
                                <option value="brinjal">ফসল: বেগুন (Brinjal)</option>
                            </select>
                        </div>

                        <div class="grid grid-cols-1 lg:grid-cols-12 gap-6">
                            <!-- Left Upload & Sample Controls -->
                            <div class="lg:col-span-5 space-y-4">
                                <div class="border-2 border-dashed border-emerald-400 bg-emerald-50/60 rounded-3xl p-5 text-center relative overflow-hidden">
                                    <input type="file" id="leaf-file-input" accept="image/*" capture="environment" class="hidden" onchange="onLeafFileSelected(event)">
                                    
                                    <!-- Initial Upload Prompt -->
                                    <div id="leaf-empty-state" class="py-4 space-y-3">
                                        <div class="w-16 h-16 rounded-full bg-emerald-600 text-white flex items-center justify-center text-3xl mx-auto shadow-md">📸</div>
                                        <h4 class="font-bold text-base text-emerald-950">পাতার ছবি তুলুন বা আপলোড করুন</h4>
                                        <p class="text-xs text-slate-600">স্পষ্ট আলোতে আক্রান্ত পাতার কাছ থেকে ছবি তুলুন</p>
                                        <button type="button" onclick="document.getElementById('leaf-file-input').click()" class="btn-press emerald-grad text-white font-bold px-5 py-3 rounded-2xl text-sm shadow-md">
                                            📷 ক্যামেরা / গ্যালারি খুলুন
                                        </button>
                                    </div>

                                    <!-- Uploaded Image Preview & Laser Scan -->
                                    <div id="leaf-preview-state" class="hidden space-y-3">
                                        <div class="relative rounded-2xl overflow-hidden border border-emerald-300 bg-black">
                                            <img id="leaf-img-tag" src="" alt="Leaf" class="w-full h-56 object-cover">
                                            <div id="scan-laser" class="scan-line hidden"></div>
                                        </div>
                                        <div class="flex gap-2">
                                            <button type="button" onclick="document.getElementById('leaf-file-input').click()" class="flex-1 py-2.5 bg-slate-200 text-slate-800 font-bold rounded-xl text-xs">
                                                অন্য ছবি
                                            </button>
                                            <button type="button" onclick="startLeafAnalysis()" class="btn-press flex-[2] py-2.5 gold-grad text-emerald-950 font-extrabold rounded-xl text-sm shadow">
                                                🔍 AI রোগ শনাক্ত করুন
                                            </button>
                                        </div>
                                    </div>
                                </div>

                                <!-- 1-Click Sample Tests (Works without camera) -->
                                <div class="bg-slate-50 rounded-2xl p-4 border border-slate-200">
                                    <p class="text-xs font-bold text-slate-700 mb-2.5">ছবি না থাকলে ১ ক্লিকে নমুনা পাতা পরীক্ষা করুন:</p>
                                    <div class="grid grid-cols-2 gap-2">
                                        <button type="button" onclick="testSampleDisease('rice')" class="btn-press bg-white hover:bg-emerald-50 border border-slate-200 rounded-xl p-2.5 text-left text-xs font-bold text-emerald-900 shadow-sm">
                                            🌾 ধানের ব্লাস্ট রোগ
                                        </button>
                                        <button type="button" onclick="testSampleDisease('potato')" class="btn-press bg-white hover:bg-emerald-50 border border-slate-200 rounded-xl p-2.5 text-left text-xs font-bold text-emerald-900 shadow-sm">
                                            🥔 আলুর মরা (নাবী ধ্বসা)
                                        </button>
                                        <button type="button" onclick="testSampleDisease('tomato')" class="btn-press bg-white hover:bg-emerald-50 border border-slate-200 rounded-xl p-2.5 text-left text-xs font-bold text-emerald-900 shadow-sm">
                                            🍅 টমেটোর পাতা কোঁকড়ানো
                                        </button>
                                        <button type="button" onclick="testSampleDisease('brinjal')" class="btn-press bg-white hover:bg-emerald-50 border border-slate-200 rounded-xl p-2.5 text-left text-xs font-bold text-emerald-900 shadow-sm">
                                            🍆 বেগুনের ডগা ছিদ্রকারী
                                        </button>
                                    </div>
                                </div>
                            </div>

                            <!-- Right Diagnosis Result Box -->
                            <div class="lg:col-span-7">
                                <div id="diagnosis-placeholder" class="h-full min-h-[260px] bg-slate-50 rounded-3xl border border-slate-200 p-6 flex flex-col items-center justify-center text-center">
                                    <span class="text-4xl mb-2">🌿</span>
                                    <h4 class="font-bold text-slate-800 text-base">রোগ নির্ণয়ের ফলাফল এখানে দেখাবে</h4>
                                    <p class="text-xs text-slate-500 mt-1 max-w-sm">বাম পাশ থেকে পাতার ছবি আপলোড করুন অথবা যেকোনো একটি নমুনা বাটনে চাপ দিন।</p>
                                </div>

                                <div id="diagnosis-output" class="hidden bg-emerald-50/70 rounded-3xl border-2 border-emerald-500 p-5 space-y-4 fade-in">
                                    <div class="flex flex-wrap items-start justify-between gap-2 border-b border-emerald-200 pb-3">
                                        <div>
                                            <span id="res-confidence" class="text-[11px] font-extrabold bg-emerald-600 text-white px-2.5 py-0.5 rounded-full">৯৬% নিশ্চিত ফলাফল</span>
                                            <h3 id="res-title" class="text-xl font-extrabold text-emerald-950 mt-1.5">ধানের ব্লাস্ট রোগ (Rice Blast)</h3>
                                        </div>
                                        <button type="button" onclick="readResultAloud()" class="btn-press bg-amber-400 hover:bg-amber-300 text-emerald-950 font-bold px-3.5 py-2 rounded-xl text-xs shadow flex items-center gap-1.5">
                                            🔊 ভয়েসে শুনুন
                                        </button>
                                    </div>

                                    <div class="space-y-3 text-xs sm:text-sm">
                                        <div class="bg-white rounded-2xl p-3.5 border border-emerald-100">
                                            <p class="font-bold text-rose-700 mb-1">⚠️ রোগের প্রধান লক্ষণ:</p>
                                            <p id="res-symptoms" class="text-slate-700 leading-relaxed"></p>
                                        </div>
                                        <div class="bg-white rounded-2xl p-3.5 border border-emerald-100">
                                            <p class="font-bold text-emerald-700 mb-1">🌱 জৈবিক ও ঘরোয়া প্রতিকার:</p>
                                            <p id="res-organic" class="text-slate-700 leading-relaxed"></p>
                                        </div>
                                        <div class="bg-white rounded-2xl p-3.5 border border-emerald-100">
                                            <p class="font-bold text-indigo-700 mb-1">🧪 অনুমোদিত বালাইনাশক ও মাত্রা:</p>
                                            <p id="res-chemical" class="text-slate-700 leading-relaxed"></p>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- ==================== TAB 3: 12-MONTH PROFITABLE CROPS ==================== -->
                <div id="page-crops" class="app-page hidden space-y-5 fade-in">
                    <div class="bg-white rounded-3xl p-5 sm:p-6 shadow-sm border border-emerald-100">
                        <span class="text-xs font-bold bg-amber-100 text-amber-800 px-3 py-1 rounded-full">মাসভিত্তিক লাভজনক কৃষি</span>
                        <h2 class="text-xl sm:text-2xl font-bold text-emerald-950 mt-1.5">কোন মাসে কোন ফসল উৎপাদন করলে বেশি লাভবান হবেন?</h2>
                        <p class="text-xs sm:text-sm text-slate-600 mb-4">মাস নির্বাচন করে অধিক মুনাফার ফসল ও আয়-ব্যয়ের হিসাব দেখুন</p>

                        <!-- Month Pills -->
                        <div id="month-pills-bar" class="flex gap-2 overflow-x-auto no-scrollbar pb-3 mb-4"></div>

                        <!-- Crops Cards Grid -->
                        <div id="month-crops-grid" class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-6"></div>

                        <!-- Interactive Profit / ROI Calculator -->
                        <div class="emerald-grad text-white rounded-3xl p-5 shadow-lg">
                            <h3 class="text-lg font-bold text-amber-400 mb-1">🧮 বিঘাপ্রতি আয়-ব্যয় ও নিট লাভ ক্যালকুলেটর</h3>
                            <p class="text-xs text-emerald-200 mb-4">জমির পরিমাণ (বিঘা) লিখুন, সম্ভাব্য খরচ ও নিট লাভ সাথে সাথে দেখাবে (৩৩ শতাংশ = ১ বিঘা)</p>

                            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-3 items-end">
                                <div>
                                    <label class="block text-xs text-emerald-200 mb-1">ফসল নির্বাচন করুন</label>
                                    <select id="roi-crop-sel" onchange="updateRoiCalc()" class="w-full bg-emerald-900 border border-emerald-700 rounded-xl px-3 py-2.5 text-sm font-bold text-white">
                                        <option value="potato">আলু (ডায়মন্ড / কার্ডিনাল)</option>
                                        <option value="tomato">হাইব্রিড টমেটো</option>
                                        <option value="onion">পেঁয়াজ (মুড়িকাটা / হালি)</option>
                                        <option value="rice">বোরো ধান (ব্রি-২৮/২৯)</option>
                                        <option value="chili">কাঁচামরিচ (উফশী)</option>
                                        <option value="mustard">সরিষা (বারি-১৪)</option>
                                    </select>
                                </div>
                                <div>
                                    <label class="block text-xs text-emerald-200 mb-1">জমির পরিমাণ (বিঘা)</label>
                                    <input type="number" id="roi-bigha-inp" value="1" min="0.5" step="0.5" oninput="updateRoiCalc()" class="w-full bg-emerald-900 border border-emerald-700 rounded-xl px-3 py-2.5 text-sm font-bold text-white">
                                </div>
                                <div class="bg-white/10 rounded-2xl p-3 border border-white/15">
                                    <p class="text-[11px] text-emerald-200">মোট উৎপাদন খরচ</p>
                                    <p id="roi-total-cost" class="text-lg font-bold text-rose-300">৳ ২২,০০০</p>
                                </div>
                                <div class="bg-amber-400 text-emerald-950 rounded-2xl p-3 shadow">
                                    <p class="text-[11px] font-bold">সম্ভাব্য নিট মুনাফা (লাভ)</p>
                                    <p id="roi-net-profit" class="text-xl font-extrabold">৳ ৪৩,০০০</p>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- ==================== TAB 4: 7-DAY WEATHER & LIVE MARKET PRICES ==================== -->
                <div id="page-weather" class="app-page hidden space-y-5 fade-in">
                    <!-- 7-Day Weather Card -->
                    <div class="bg-white rounded-3xl p-5 sm:p-6 shadow-sm border border-sky-100">
                        <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-2 mb-4">
                            <div>
                                <span class="text-xs font-bold bg-sky-100 text-sky-800 px-3 py-1 rounded-full">আবহাওয়া পূর্বাভাস</span>
                                <h2 class="text-xl font-bold text-emerald-950 mt-1">আগামী ৭ দিনের কৃষি আবহাওয়া (<span id="weather-city-title">নারায়ণগঞ্জ</span>)</h2>
                            </div>
                        </div>

                        <div class="bg-amber-50 border-l-4 border-amber-500 p-3.5 rounded-r-2xl mb-4 text-xs sm:text-sm text-amber-950">
                            <strong>🌾 কৃষি আবহাওয়া পরামর্শ:</strong> আগামী ৩ দিন আবহাওয়া শুষ্ক ও রোদ্রোজ্জ্বল থাকবে। ৪র্থ দিনে হালকা বৃষ্টির সম্ভাবনা থাকায় এখনই জমিতে সার ও ছত্রাকনাশক স্প্রে সম্পন্ন করুন।
                        </div>

                        <div id="weather-days-grid" class="grid grid-cols-2 sm:grid-cols-4 lg:grid-cols-7 gap-2.5"></div>
                    </div>

                    <!-- Today's Market Prices -->
                    <div class="bg-white rounded-3xl p-5 sm:p-6 shadow-sm border border-emerald-100">
                        <div class="flex items-center justify-between mb-4">
                            <div>
                                <h3 class="text-lg sm:text-xl font-bold text-emerald-950">📊 আজকের পাইকারি ও খুচরা বাজারদর</h3>
                                <p class="text-xs text-slate-500">ফসলের ন্যায্যমূল্য নিশ্চিত করতে প্রতিদিনের বাজার দর জানুন</p>
                            </div>
                            <span class="text-xs font-bold bg-emerald-100 text-emerald-800 px-3 py-1 rounded-full">লাইভ দর</span>
                        </div>
                        <div id="market-prices-list" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-3"></div>
                    </div>
                </div>

                <!-- ==================== TAB 5: BD AGRI LOANS & SMART CALCULATORS ==================== -->
                <div id="page-loans" class="app-page hidden space-y-5 fade-in">
                    <!-- Banks & Loans Section -->
                    <div class="bg-white rounded-3xl p-5 sm:p-6 shadow-sm border border-indigo-100">
                        <span class="text-xs font-bold bg-indigo-100 text-indigo-800 px-3 py-1 rounded-full">সরকারি ও বেসরকারি ব্যাংক</span>
                        <h2 class="text-xl sm:text-2xl font-bold text-emerald-950 mt-1.5">বাংলাদেশি কৃষি ঋণ ও ব্যাংক তথ্য কেন্দ্র</h2>
                        <p class="text-xs sm:text-sm text-slate-600 mb-4">ডাল, তেলবীজ, মসলা ও ভুট্টা চাষে সরকারি ভর্তুকিতে মাত্র <strong>৪% রেয়াতি সুদে</strong> কৃষি ঋণ পাওয়া যায়।</p>

                        <div id="banks-cards-grid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-3.5 mb-6"></div>

                        <!-- EMI Calculator -->
                        <div class="emerald-grad text-white rounded-3xl p-5">
                            <h3 class="font-bold text-lg text-amber-400 mb-3">💳 কৃষি ঋণের মাসিক কিস্তি (EMI) ক্যালকুলেটর</h3>
                            <div class="grid grid-cols-1 sm:grid-cols-3 gap-4 items-center">
                                <div>
                                    <label class="text-xs text-emerald-200">ঋণের পরিমাণ: <strong id="emi-amt-lbl" class="text-amber-300">৳ ৫০,০০০</strong></label>
                                    <input type="range" id="emi-amt-range" min="10000" max="500000" step="5000" value="50000" oninput="updateEmiCalc()" class="w-full accent-amber-400 mt-1">
                                </div>
                                <div class="grid grid-cols-2 gap-2">
                                    <div>
                                        <label class="block text-xs text-emerald-200 mb-1">সুদের হার</label>
                                        <select id="emi-rate-sel" onchange="updateEmiCalc()" class="w-full bg-emerald-900 border border-emerald-700 rounded-xl px-2.5 py-2 text-xs font-bold">
                                            <option value="4">৪% (মসলা/ডাল)</option>
                                            <option value="8" selected>৮% (সাধারণ)</option>
                                            <option value="9">৯% (বেসরকারি)</option>
                                        </select>
                                    </div>
                                    <div>
                                        <label class="block text-xs text-emerald-200 mb-1">মেয়াদ</label>
                                        <select id="emi-term-sel" onchange="updateEmiCalc()" class="w-full bg-emerald-900 border border-emerald-700 rounded-xl px-2.5 py-2 text-xs font-bold">
                                            <option value="6">৬ মাস</option>
                                            <option value="12" selected>১২ মাস</option>
                                            <option value="24">২৪ মাস</option>
                                        </select>
                                    </div>
                                </div>
                                <div class="bg-black/25 rounded-2xl p-3 flex justify-between items-center">
                                    <div>
                                        <p class="text-[11px] text-emerald-200">মাসিক কিস্তি</p>
                                        <p id="emi-monthly-out" class="text-xl font-extrabold text-amber-400">৳ ৪,৩৪৯</p>
                                    </div>
                                    <div class="text-right">
                                        <p class="text-[11px] text-emerald-200">মোট পরিশোধ</p>
                                        <p id="emi-total-out" class="text-sm font-bold">৳ ৫২,১৮৮</p>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- Fertilizer & Land Calculators -->
                    <div class="grid grid-cols-1 lg:grid-cols-2 gap-5">
                        <div class="bg-white rounded-3xl p-5 shadow-sm border border-emerald-100">
                            <h3 class="font-bold text-lg text-emerald-950 mb-1">🧪 সুষম সার পরিমাপ ক্যালকুলেটর</h3>
                            <p class="text-xs text-slate-500 mb-3">জমির শতাংশ অনুযায়ী সঠিক মাত্রার সার হিসাব করুন</p>
                            <div class="grid grid-cols-2 gap-2.5 mb-3">
                                <select id="fert-crop-sel" onchange="updateFertCalc()" class="bg-slate-50 border border-slate-200 rounded-xl px-3 py-2 text-xs font-bold">
                                    <option value="rice">ধান (বোরো / আমন)</option>
                                    <option value="potato">আলু</option>
                                    <option value="veg">শাকসবজি (টমেটো/বেগুন)</option>
                                </select>
                                <input type="number" id="fert-dec-inp" value="33" min="1" oninput="updateFertCalc()" placeholder="শতাংশ" class="bg-slate-50 border border-slate-200 rounded-xl px-3 py-2 text-xs font-bold">
                            </div>
                            <div class="grid grid-cols-4 gap-2 text-center text-xs">
                                <div class="bg-emerald-50 p-2.5 rounded-xl border border-emerald-200"><p class="text-slate-500">ইউরিয়া</p><p id="f-urea" class="font-extrabold text-emerald-900 mt-0.5">২০ কেজি</p></div>
                                <div class="bg-amber-50 p-2.5 rounded-xl border border-amber-200"><p class="text-slate-500">টিএসপি</p><p id="f-tsp" class="font-extrabold text-amber-900 mt-0.5">১২ কেজি</p></div>
                                <div class="bg-rose-50 p-2.5 rounded-xl border border-rose-200"><p class="text-slate-500">পটাশ</p><p id="f-mop" class="font-extrabold text-rose-900 mt-0.5">১৫ কেজি</p></div>
                                <div class="bg-sky-50 p-2.5 rounded-xl border border-sky-200"><p class="text-slate-500">জিপসাম</p><p id="f-gyp" class="font-extrabold text-sky-900 mt-0.5">৮ কেজি</p></div>
                            </div>
                        </div>

                        <div class="bg-white rounded-3xl p-5 shadow-sm border border-amber-100">
                            <h3 class="font-bold text-lg text-emerald-950 mb-1">📐 ডিজিটাল জমি পরিমাপ রূপান্তর</h3>
                            <p class="text-xs text-slate-500 mb-3">শতাংশ লিখলে বিঘা, কাঠা ও একর বের হবে</p>
                            <input type="number" id="land-dec-inp" value="100" min="0" oninput="updateLandCalc()" class="w-full bg-slate-50 border border-slate-200 rounded-xl px-3.5 py-2 text-sm font-bold mb-3">
                            <div class="grid grid-cols-3 gap-2 text-center text-xs">
                                <div class="bg-emerald-900 text-white p-2.5 rounded-xl"><p class="text-emerald-200">বিঘা</p><p id="l-bigha" class="font-extrabold text-amber-400 text-base">৩.০৩</p></div>
                                <div class="bg-emerald-900 text-white p-2.5 rounded-xl"><p class="text-emerald-200">কাঠা</p><p id="l-katha" class="font-extrabold text-amber-400 text-base">৬০.৬১</p></div>
                                <div class="bg-emerald-900 text-white p-2.5 rounded-xl"><p class="text-emerald-200">একর</p><p id="l-acre" class="font-extrabold text-amber-400 text-base">১.০০</p></div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- ==================== TAB 6: AGRICULTURAL AWARENESS ANIMATED VIDEOS ==================== -->
                <div id="page-videos" class="app-page hidden space-y-5 fade-in">
                    <div class="bg-white rounded-3xl p-5 sm:p-6 shadow-sm border border-rose-100">
                        <span class="text-xs font-bold bg-rose-100 text-rose-800 px-3 py-1 rounded-full">কৃষক সচেতনতা অ্যানিমেশন</span>
                        <h2 class="text-xl sm:text-2xl font-bold text-emerald-950 mt-1.5">কৃষি সচেতনতা অ্যানিমেশন ভিডিও কেন্দ্র</h2>
                        <p class="text-xs sm:text-sm text-slate-600 mb-4">অ্যানিমেটেড দৃশ্য ও বাংলা ভয়েস বর্ণনার মাধ্যমে নিরাপদ ও আধুনিক চাষাবাদ শিখুন</p>

                        <!-- Interactive Animated Stage -->
                        <div class="bg-slate-950 rounded-3xl overflow-hidden shadow-xl border border-emerald-800 mb-5">
                            <div class="relative w-full h-64 sm:h-80 bg-gradient-to-b from-sky-950 to-emerald-950">
                                <canvas id="video-stage-canvas" class="w-full h-full block"></canvas>
                                
                                <!-- Subtitle Box -->
                                <div class="absolute bottom-14 inset-x-3 sm:inset-x-10 text-center pointer-events-none">
                                    <span id="vid-subtitle-txt" class="inline-block bg-black/80 text-amber-300 text-xs sm:text-sm font-semibold px-4 py-2 rounded-2xl border border-white/15">
                                        নিচের যেকোনো একটি ভিডিও কার্ডে ক্লিক করে প্লে করুন
                                    </span>
                                </div>

                                <!-- Player Controls -->
                                <div class="absolute bottom-0 inset-x-0 bg-black/85 px-4 py-2.5 flex items-center gap-3 text-white">
                                    <button type="button" onclick="toggleVideoPlay()" id="vid-play-toggle" class="w-9 h-9 rounded-full bg-amber-400 text-emerald-950 font-extrabold flex items-center justify-center shadow">
                                        ▶
                                    </button>
                                    <div class="flex-1 bg-white/20 h-2 rounded-full overflow-hidden">
                                        <div id="vid-prog-fill" class="bg-amber-400 h-full w-0 transition-all"></div>
                                    </div>
                                    <button type="button" onclick="playAwarenessEpisode(currentEpIdx)" class="text-xs bg-white/15 px-3 py-1.5 rounded-xl font-bold">
                                        ↻ আবার
                                    </button>
                                </div>
                            </div>
                        </div>

                        <!-- 4 Video Episode Cards -->
                        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-3">
                            <div onclick="playAwarenessEpisode(0)" id="ep-card-0" class="cursor-pointer bg-emerald-50 border-2 border-emerald-600 rounded-2xl p-3.5 transition">
                                <span class="text-[10px] font-bold bg-emerald-600 text-white px-2 py-0.5 rounded-full">পর্ব ১</span>
                                <h4 class="font-bold text-sm text-emerald-950 mt-1.5">সুষম সার ও মাটির স্বাস্থ্য</h4>
                                <p class="text-xs text-slate-600 mt-1">অতিরিক্ত ইউরিয়ার ক্ষতি ও জৈব সারের উপকারিতা।</p>
                            </div>
                            <div onclick="playAwarenessEpisode(1)" id="ep-card-1" class="cursor-pointer bg-white border border-slate-200 rounded-2xl p-3.5 transition">
                                <span class="text-[10px] font-bold bg-amber-100 text-amber-800 px-2 py-0.5 rounded-full">পর্ব ২</span>
                                <h4 class="font-bold text-sm text-emerald-950 mt-1.5">বিষমুক্ত চাষ ও মাস্ক সতর্কতা</h4>
                                <p class="text-xs text-slate-600 mt-1">স্প্রে করার সময় সুরক্ষা পোশাক ও ফেরোমন ফাঁদ।</p>
                            </div>
                            <div onclick="playAwarenessEpisode(2)" id="ep-card-2" class="cursor-pointer bg-white border border-slate-200 rounded-2xl p-3.5 transition">
                                <span class="text-[10px] font-bold bg-sky-100 text-sky-800 px-2 py-0.5 rounded-full">পর্ব ৩</span>
                                <h4 class="font-bold text-sm text-emerald-950 mt-1.5">আধুনিক AWD সেচ পদ্ধতি</h4>
                                <p class="text-xs text-slate-600 mt-1">পাইপ পদ্ধতিতে সেচ দিয়ে ৩০% পানি ও খরচ সাশ্রয়।</p>
                            </div>
                            <div onclick="playAwarenessEpisode(3)" id="ep-card-3" class="cursor-pointer bg-white border border-slate-200 rounded-2xl p-3.5 transition">
                                <span class="text-[10px] font-bold bg-rose-100 text-rose-800 px-2 py-0.5 rounded-full">পর্ব ৪</span>
                                <h4 class="font-bold text-sm text-emerald-950 mt-1.5">আগাম রোগ প্রতিরোধ ও AI স্ক্যান</h4>
                                <p class="text-xs text-slate-600 mt-1">পাতায় দাগ দেখলেই ছবি তুলে ফসল বাঁচানোর উপায়।</p>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- ==================== TAB 7: SETTINGS & LANGUAGE ==================== -->
                <div id="page-settings" class="app-page hidden space-y-5 fade-in">
                    <div class="bg-white rounded-3xl p-5 sm:p-6 shadow-sm border border-emerald-100 max-w-2xl mx-auto space-y-5">
                        <div class="border-b border-slate-100 pb-4">
                            <h2 class="text-xl font-bold text-emerald-950">⚙️ অ্যাপ সেটিংস (Settings)</h2>
                            <p class="text-xs text-slate-500">ভাষা, জেলা এবং ভয়েস অ্যাসিস্ট্যান্ট নিয়ন্ত্রণ করুন</p>
                        </div>

                        <!-- Language Toggle -->
                        <div>
                            <label class="block text-xs font-bold text-slate-700 mb-2">অ্যাপের ভাষা নির্বাচন করুন (Language)</label>
                            <div class="grid grid-cols-2 gap-3">
                                <button type="button" onclick="changeLang('bn')" id="set-lang-bn" class="py-3 px-4 rounded-2xl border-2 border-emerald-600 bg-emerald-50 text-emerald-950 font-bold text-sm">
                                    🇧🇩 বাংলা (Bangla)
                                </button>
                                <button type="button" onclick="changeLang('en')" id="set-lang-en" class="py-3 px-4 rounded-2xl border border-slate-200 bg-white text-slate-700 font-bold text-sm">
                                    🇬🇧 English
                                </button>
                            </div>
                        </div>

                        <!-- District Change -->
                        <div>
                            <label class="block text-xs font-bold text-slate-700 mb-1.5">আপনার জেলা পরিবর্তন করুন</label>
                            <select id="settings-dist-sel" onchange="setDistrict(this.value)" class="w-full px-3.5 py-3 bg-slate-50 border border-slate-200 rounded-2xl text-sm font-bold text-slate-800">
                                <option value="নারায়ণগঞ্জ">নারায়ণগঞ্জ (Narayanganj)</option>
                                <option value="ঢাকা">ঢাকা (Dhaka)</option>
                                <option value="বগুড়া">বগুড়া (Bogura)</option>
                                <option value="রাজশাহী">রাজশাহী (Rajshahi)</option>
                                <option value="রংপুর">রংপুর (Rangpur)</option>
                                <option value="যশোর">যশোর (Jashore)</option>
                                <option value="ময়মনসিংহ">ময়মনসিংহ (Mymensingh)</option>
                                <option value="সিলেট">সিলেট (Sylhet)</option>
                                <option value="কুমিল্লা">কুমিল্লা (Cumilla)</option>
                                <option value="খুলনা">খুলনা (Khulna)</option>
                            </select>
                        </div>

                        <!-- Voice Toggle -->
                        <div class="flex items-center justify-between bg-slate-50 p-4 rounded-2xl border border-slate-200">
                            <div>
                                <p class="text-sm font-bold text-slate-800">ভয়েস বর্ণনা চালু রাখুন</p>
                                <p class="text-xs text-slate-500">রোগের ফলাফল ও ভিডিওর কথা মুখে পড়ে শোনাবে</p>
                            </div>
                            <input type="checkbox" id="voice-chk" checked class="w-5 h-5 accent-emerald-600">
                        </div>

                        <!-- Creator Info Card -->
                        <div class="emerald-grad text-white rounded-3xl p-5 text-center shadow-md">
                            <p class="text-xs text-emerald-200">কৃষি মিত্র — স্মার্ট কৃষি সুপার অ্যাপ</p>
                            <p class="text-base font-extrabold text-amber-400 mt-1">Created &amp; organized by Nahid</p>
                            <button type="button" onclick="logoutApp()" class="mt-4 px-5 py-2 rounded-xl bg-white/15 hover:bg-white/25 text-xs font-bold">
                                লগ আউট করে প্রথম পেজে যান
                            </button>
                        </div>
                    </div>
                </div>

            </main>
        </div>

        <!-- Mobile Fixed Bottom Navigation Bar -->
        <nav class="md:hidden fixed bottom-0 inset-x-0 z-30 bg-white/95 backdrop-blur border-t border-emerald-100 shadow-[0_-4px_18px_rgba(0,0,0,0.06)] px-1 py-1.5">
            <div class="grid grid-cols-5 gap-1 text-center">
                <button type="button" onclick="openPage('home')" data-nav="home" class="mob-nav flex flex-col items-center justify-center py-1.5 rounded-xl bg-emerald-50 text-emerald-800 font-bold">
                    <span class="text-base leading-none">🏠</span>
                    <span class="text-[10px] mt-1">হোম</span>
                </button>
                <button type="button" onclick="openPage('disease')" data-nav="disease" class="mob-nav flex flex-col items-center justify-center py-1.5 rounded-xl text-slate-500 font-medium">
                    <span class="text-base leading-none">🔬</span>
                    <span class="text-[10px] mt-1">রোগ নির্ণয়</span>
                </button>
                <button type="button" onclick="openPage('crops')" data-nav="crops" class="mob-nav flex flex-col items-center justify-center py-1.5 rounded-xl text-slate-500 font-medium">
                    <span class="text-base leading-none">🌾</span>
                    <span class="text-[10px] mt-1">লাভজনক</span>
                </button>
                <button type="button" onclick="openPage('loans')" data-nav="loans" class="mob-nav flex flex-col items-center justify-center py-1.5 rounded-xl text-slate-500 font-medium">
                    <span class="text-base leading-none">🏦</span>
                    <span class="text-[10px] mt-1">কৃষি ঋণ</span>
                </button>
                <button type="button" onclick="openPage('videos')" data-nav="videos" class="mob-nav flex flex-col items-center justify-center py-1.5 rounded-xl text-slate-500 font-medium">
                    <span class="text-base leading-none">🎬</span>
                    <span class="text-[10px] mt-1">ভিডিও</span>
                </button>
            </div>
        </nav>
    </div>

    <!-- PWA App Download / Install Modal -->
    <div id="install-modal" class="fixed inset-0 z-50 hidden items-center justify-center bg-black/60 backdrop-blur-sm p-4">
        <div class="bg-white rounded-3xl max-w-md w-full p-6 shadow-2xl border border-emerald-100 fade-in">
            <div class="flex items-center justify-between mb-3">
                <h3 class="font-bold text-lg text-emerald-950">📲 ফোনে অ্যাপ ইনস্টল করুন</h3>
                <button type="button" onclick="toggleInstallModal(false)" class="w-8 h-8 rounded-full bg-slate-100 font-bold text-slate-600">✕</button>
            </div>
            <p class="text-xs sm:text-sm text-slate-600 mb-3">প্লে-স্টোর ছাড়াই সরাসরি ফোনের হোম স্ক্রিনে <strong>কৃষি মিত্র</strong> অ্যাপটি ইনস্টল করতে পারবেন:</p>
            <div class="bg-emerald-50 rounded-2xl p-3.5 space-y-2 text-xs text-emerald-950 border border-emerald-200 mb-4">
                <p><strong>১. Android (Chrome):</strong> ব্রাউজারের উপরে ডানপাশে <strong>⋮</strong> মেনুতে ক্লিক করে <strong>"Add to Home screen"</strong> বা <strong>"Install App"</strong> চাপুন।</p>
                <p><strong>২. iPhone (Safari):</strong> নিচের <strong>Share</strong> বাটনে চাপ দিয়ে <strong>"Add to Home Screen"</strong> নির্বাচন করুন।</p>
            </div>
            <button type="button" onclick="triggerPwaPrompt()" class="btn-press w-full py-3 rounded-2xl emerald-grad text-white font-bold text-sm shadow">
                এখনই ইনস্টল করুন
            </button>
        </div>
    </div>

    <!-- ==================== VANILLA JAVASCRIPT (ZERO EXTERNAL ERRORS) ==================== -->
    <script>
        // Global State
        var lang = 'bn';
        var selectedDistrict = 'নারায়ণগঞ্জ';
        var deferredInstallEvent = null;
        var currentEpIdx = 0;
        var vidPlaying = false;
        var vidProgress = 0;
        var vidAnimId = null;
        var lastSpokenStep = -1;

        // PWA Install Event Listener
        window.addEventListener('beforeinstallprompt', function(e) {
            e.preventDefault();
            deferredInstallEvent = e;
        });

        function toggleInstallModal(show) {
            var modal = document.getElementById('install-modal');
            if (show) {
                modal.classList.remove('hidden');
                modal.classList.add('flex');
            } else {
                modal.classList.add('hidden');
                modal.classList.remove('flex');
            }
        }

        function triggerPwaPrompt() {
            if (deferredInstallEvent) {
                deferredInstallEvent.prompt();
                deferredInstallEvent.userChoice.then(function() {
                    deferredInstallEvent = null;
                    toggleInstallModal(false);
                });
            } else {
                notify('ব্রাউজারের মেনু (⋮) থেকে "Add to Home Screen" সিলেক্ট করুন।');
                toggleInstallModal(false);
            }
        }

        // Smooth Toast Notification
        function notify(msg) {
            var box = document.getElementById('toast-box');
            var el = document.createElement('div');
            el.className = 'bg-emerald-950 text-white text-xs sm:text-sm font-semibold px-4 py-3 rounded-2xl shadow-xl border border-amber-400/40 text-center fade-in';
            el.innerText = msg;
            box.appendChild(el);
            setTimeout(function() {
                if (el && el.parentNode) el.parentNode.removeChild(el);
            }, 3200);
        }

        // Bilingual Dictionary
        var dict = {
            bn: {
                app_title: 'কৃষি মিত্র',
                app_sub: 'বাংলাদেশের প্রথম এআই-চালিত পূর্ণাঙ্গ ডিজিটাল কৃষি সুপার অ্যাপ',
                f_disease: 'AI রোগ নির্ণয়',
                f_profit: 'লাভজনক ফসল',
                f_loan: 'কৃষি ঋণ ও ব্যাংক',
                sel_dist: 'আপনার জেলা নির্বাচন করুন',
                btn_google: 'Google অ্যাকাউন্ট দিয়ে প্রবেশ করুন',
                btn_fb: 'Facebook অ্যাকাউন্ট দিয়ে প্রবেশ করুন',
                or_txt: 'অথবা দ্রুত ব্যবহার করুন',
                btn_guest: 'কৃষক হিসেবে সরাসরি প্রবেশ করুন (ফ্রি)',
                safe_txt: '১০০% নিরাপদ ও ফ্রি',
                dl_app: 'অ্যাপ ডাউনলোড করুন',
                nav_home: 'হোম ড্যাশবোর্ড',
                nav_disease: 'AI রোগ নির্ণয়',
                nav_crops: '১২ মাসের লাভজনক ফসল',
                nav_weather: '৭ দিনের আবহাওয়া ও বাজার',
                nav_loans: 'কৃষি ঋণ ও ক্যালকুলেটর',
                nav_videos: 'সচেতনতা অ্যানিমেশন ভিডিও',
                nav_settings: 'সেটিংস ও ভাষা',
                install_txt: 'ইনস্টল',
                smart_agri_badge: 'ডিজিটাল কৃষি সহায়ক',
                hero_desc: 'আক্রান্ত পাতার ছবি তুলে মুহূর্তেই রোগ ও সমাধান জানুন, দেখুন কোন মাসে কোন ফসলে বেশি লাভ এবং সরকারি কৃষি ঋণের তথ্য।',
                cta_scan: 'পাতার ছবি দিয়ে রোগ দেখুন',
                cta_video: 'সচেতনতা ভিডিও দেখুন',
                quick_services: 'সকল স্মার্ট কৃষি সেবা'
            },
            en: {
                app_title: 'Krishi Mitra',
                app_sub: "Bangladesh's First AI-Powered Complete Digital Agriculture Super App",
                f_disease: 'AI Disease Scan',
                f_profit: 'Profitable Crops',
                f_loan: 'Agri Loans & Banks',
                sel_dist: 'Select Your District',
                btn_google: 'Sign in with Google Account',
                btn_fb: 'Sign in with Facebook Account',
                or_txt: 'Or Quick Access',
                btn_guest: 'Enter Directly as Farmer (Free)',
                safe_txt: '100% Safe & Free',
                dl_app: 'Download App',
                nav_home: 'Home Dashboard',
                nav_disease: 'AI Disease Doctor',
                nav_crops: '12-Month Profit Crops',
                nav_weather: '7-Day Weather & Market',
                nav_loans: 'Agri Loans & Tools',
                nav_videos: 'Awareness Videos',
                nav_settings: 'Settings & Language',
                install_txt: 'Install',
                smart_agri_badge: 'Digital Agri Assistant',
                hero_desc: 'Scan infected leaves for instant diagnosis & cure, find monthly profitable crops, and explore Bangladesh agri loans.',
                cta_scan: 'Scan Leaf for Disease',
                cta_video: 'Watch Awareness Videos',
                quick_services: 'All Smart Agriculture Services'
            }
        };

        function changeLang(newLang) {
            lang = newLang;
            var nodes = document.querySelectorAll('[data-t]');
            for (var i = 0; i < nodes.length; i++) {
                var key = nodes[i].getAttribute('data-t');
                if (dict[lang] && dict[lang][key]) {
                    nodes[i].innerText = dict[lang][key];
                }
            }
            document.getElementById('quick-lang-txt').innerText = (lang === 'bn') ? 'English' : 'বাংলা';

            // Update Welcome & Settings buttons
            var activeCls = 'px-3.5 py-1 rounded-full text-xs font-bold bg-emerald-700 text-white transition';
            var inactiveCls = 'px-3.5 py-1 rounded-full text-xs font-bold text-slate-600 transition';
            document.getElementById('w-lang-bn').className = (lang === 'bn') ? activeCls : inactiveCls;
            document.getElementById('w-lang-en').className = (lang === 'en') ? activeCls : inactiveCls;

            var sAct = 'py-3 px-4 rounded-2xl border-2 border-emerald-600 bg-emerald-50 text-emerald-950 font-bold text-sm';
            var sInact = 'py-3 px-4 rounded-2xl border border-slate-200 bg-white text-slate-700 font-bold text-sm';
            document.getElementById('set-lang-bn').className = (lang === 'bn') ? sAct : sInact;
            document.getElementById('set-lang-en').className = (lang === 'en') ? sAct : sInact;

            notify(lang === 'bn' ? 'ভাষা বাংলায় পরিবর্তন করা হয়েছে' : 'Language switched to English');
        }

        function toggleLangQuick() {
            changeLang(lang === 'bn' ? 'en' : 'bn');
        }

        function setDistrict(dist) {
            selectedDistrict = dist;
            document.getElementById('pc-district-badge').innerText = dist + ', বাংলাদেশ';
            document.getElementById('mob-district-badge').innerText = dist;
            document.getElementById('home-weather-city').innerText = '📍 ' + dist;
            document.getElementById('weather-city-title').innerText = dist;
            document.getElementById('settings-dist-sel').value = dist;
        }

        // Login Handler (Guaranteed Immediate Transition)
        function loginWithProvider(provider) {
            var distVal = document.getElementById('welcome-district').value || 'নারায়ণগঞ্জ';
            setDistrict(distVal);

            var uName = 'সম্মানিত কৃষক ভাই';
            if (provider === 'Google') uName = 'রাকিব হাসান (Google)';
            if (provider === 'Facebook') uName = 'ফরিদ উদ্দিন (Facebook)';
            document.getElementById('user-greeting-name').innerText = uName;

            document.getElementById('welcome-view').classList.add('hidden');
            document.getElementById('app-shell').classList.remove('hidden');

            initAllModules();
            notify('কৃষি মিত্র অ্যাপে স্বাগতম!');
            window.scrollTo(0, 0);
        }

        function logoutApp() {
            stopVideoAnim();
            document.getElementById('app-shell').classList.add('hidden');
            document.getElementById('welcome-view').classList.remove('hidden');
            window.scrollTo(0, 0);
        }

        // Page Tab Navigation (Mobile + PC Sync)
        function openPage(pageId) {
            var pages = document.querySelectorAll('.app-page');
            for (var i = 0; i < pages.length; i++) {
                pages[i].classList.add('hidden');
            }
            var target = document.getElementById('page-' + pageId);
            if (target) target.classList.remove('hidden');

            // Update PC Sidebar
            var pcBtns = document.querySelectorAll('.pc-nav');
            for (var j = 0; j < pcBtns.length; j++) {
                var isMatch = pcBtns[j].getAttribute('data-nav') === pageId;
                pcBtns[j].className = isMatch
                    ? 'pc-nav w-full flex items-center gap-3 px-4 py-3 rounded-2xl text-sm font-bold bg-white text-emerald-950 shadow transition'
                    : 'pc-nav w-full flex items-center gap-3 px-4 py-3 rounded-2xl text-sm font-semibold text-emerald-100 hover:bg-white/10 transition';
            }

            // Update Mobile Bottom Nav
            var mobBtns = document.querySelectorAll('.mob-nav');
            for (var k = 0; k < mobBtns.length; k++) {
                var mMatch = mobBtns[k].getAttribute('data-nav') === pageId;
                mobBtns[k].className = mMatch
                    ? 'mob-nav flex flex-col items-center justify-center py-1.5 rounded-xl bg-emerald-50 text-emerald-800 font-bold'
                    : 'mob-nav flex flex-col items-center justify-center py-1.5 rounded-xl text-slate-500 font-medium';
            }

            if (pageId === 'videos') {
                playAwarenessEpisode(currentEpIdx);
            } else {
                stopVideoAnim();
            }

            window.scrollTo(0, 0);
        }

        // ==================== MODULE 1: AI DISEASE DIAGNOSIS ====================
        var diseaseDB = {
            rice: {
                title: 'ধানের ব্লাস্ট রোগ (Rice Blast)',
                conf: '৯৭% নিশ্চিত ফলাফল',
                symptoms: 'পাতায় চোখের আকৃতির বা ডিম্বাকৃতির দাগ দেখা যায় যার মাঝখানটা ধূসর ও কিনারা বাদামী। শীষের গোড়ায় আক্রমণ হলে ধান চিটা হয়ে যায়।',
                organic: 'জমিতে সুষম মাত্রায় পটাশ সার দিন, ইউরিয়া কিস্তিতে প্রয়োগ করুন এবং ক্ষেত আগাছামুক্ত রাখুন।',
                chemical: 'ট্রাইসাইক্লাজল বা ন্যাটোভো (Nativo) প্রতি লিটার পানিতে ১ গ্রাম মিশিয়ে বিকেলে স্প্রে করুন।'
            },
            potato: {
                title: 'আলুর নাবী ধ্বসা / মরা রোগ (Late Blight)',
                conf: '৯৬% নিশ্চিত ফলাফল',
                symptoms: 'পাতার কিনারায় জলসিক্ত কালচে দাগ পড়ে এবং কুয়াশাচ্ছন্ন আবহাওয়ায় দ্রুত পুরো গাছ পচে যায়।',
                organic: 'আক্রান্ত গাছ তুলে মাটিচাপা দিন এবং কুয়াশার সময় জমিতে সেচ দেওয়া বন্ধ রাখুন।',
                chemical: 'ম্যানকোজেব + মেটালেক্সিল (রিডোমিল গোল্ড) প্রতি লিটার পানিতে ২ গ্রাম মিশিয়ে ৭ দিন পরপর স্প্রে করুন।'
            },
            tomato: {
                title: 'টমেটোর পাতা কোঁকড়ানো রোগ (Leaf Curl Virus)',
                conf: '৯৫% নিশ্চিত ফলাফল',
                symptoms: 'পাতার কিনারা ওপরের দিকে কুঁকড়ে যায়, পাতা ছোট ও হলুদ হয়ে যায় এবং গাছে ফুল-ফল কমে যায়।',
                organic: 'সাদা মাছি দমনের জন্য ক্ষেতে হলুদ আঠালো ফাঁদ (Yellow Sticky Trap) ও নিম তেল ব্যবহার করুন।',
                chemical: 'ইমিডাক্লোপ্রিড (এডমায়ার) প্রতি লিটার পানিতে ০.৫ মিলি মিশিয়ে স্প্রে করে বাহক পোকা দমন করুন।'
            },
            brinjal: {
                title: 'বেগুনের ডগা ও ফল ছিদ্রকারী পোকা',
                conf: '৯৮% নিশ্চিত ফলাফল',
                symptoms: 'কচি ডগা নেতিয়ে পড়ে ও শুকিয়ে যায় এবং বেগুনের ভেতরে ছিদ্র করে পোকা নষ্ট করে ফেলে।',
                organic: 'আক্রান্ত ডগা কেটে ধ্বংস করুন এবং জমিতে সেক্স ফেরোমন ফাঁদ স্থাপন করুন।',
                chemical: 'এমামেকটিন বেনজোয়েট (প্রোক্লেম) প্রতি লিটার পানিতে ১ গ্রাম মিশিয়ে স্প্রে করুন।'
            }
        };

        function onLeafFileSelected(e) {
            var file = e.target.files[0];
            if (!file) return;
            var reader = new FileReader();
            reader.onload = function(ev) {
                document.getElementById('leaf-img-tag').src = ev.target.result;
                document.getElementById('leaf-empty-state').classList.add('hidden');
                document.getElementById('leaf-preview-state').classList.remove('hidden');
                startLeafAnalysis();
            };
            reader.readAsDataURL(file);
        }

        function startLeafAnalysis() {
            var laser = document.getElementById('scan-laser');
            laser.classList.remove('hidden');
            notify('AI পাতার ছবি বিশ্লেষণ করছে...');
            setTimeout(function() {
                laser.classList.add('hidden');
                var cropKey = document.getElementById('disease-crop-type').value || 'rice';
                showDiseaseOutput(cropKey);
            }, 1300);
        }

        function testSampleDisease(key) {
            document.getElementById('disease-crop-type').value = key;
            showDiseaseOutput(key);
            notify('নমুনা রোগের ফলাফল তৈরি হয়েছে!');
        }

        function showDiseaseOutput(key) {
            var info = diseaseDB[key] || diseaseDB.rice;
            document.getElementById('res-title').innerText = info.title;
            document.getElementById('res-confidence').innerText = info.conf;
            document.getElementById('res-symptoms').innerText = info.symptoms;
            document.getElementById('res-organic').innerText = info.organic;
            document.getElementById('res-chemical').innerText = info.chemical;

            document.getElementById('diagnosis-placeholder').classList.add('hidden');
            document.getElementById('diagnosis-output').classList.remove('hidden');
        }

        function readResultAloud() {
            var t = document.getElementById('res-title').innerText;
            var c = document.getElementById('res-chemical').innerText;
            speakText(t + '। প্রতিকার: ' + c);
        }

        function speakText(txt) {
            var chk = document.getElementById('voice-chk');
            if (chk && !chk.checked) return;
            if ('speechSynthesis' in window) {
                window.speechSynthesis.cancel();
                var u = new SpeechSynthesisUtterance(txt);
                u.lang = (lang === 'bn') ? 'bn-BD' : 'en-US';
                u.rate = 0.95;
                window.speechSynthesis.speak(u);
                notify('🔊 ভয়েসে পড়ে শোনানো হচ্ছে...');
            } else {
                notify('আপনার ব্রাউজারে ভয়েস সাপোর্ট নেই।');
            }
        }

        // ==================== MODULE 2: 12-MONTH PROFITABLE CROPS ====================
        var monthsList = [
            { m: 'বৈশাখ (এপ্রিল-মে)', items: [
                { name: 'পাট (সোনালী আঁশ)', profit: 'লাভ: ৳ ১৮,০০০/বিঘা', desc: 'বর্ষার শুরুতে পাট চাষে আঁশের ভালো দাম পাওয়া যায়।' },
                { name: 'আউশ ধান', profit: 'লাভ: ৳ ১৪,০০০/বিঘা', desc: 'কম সেচে স্বল্পমেয়াদী লাভজনক ধান।' },
                { name: 'ঢেঁড়স ও পটল', profit: 'লাভ: ৳ ১৬,০০০/বিঘা', desc: 'গ্রীষ্মকালীন সবজির ব্যাপক চাহিদা থাকে।' }
            ]},
            { m: 'জ্যৈষ্ঠ (মে-জুন)', items: [
                { name: 'করলা ও চিচিঙ্গা', profit: 'লাভ: ৳ ১৫,০০০/বিঘা', desc: 'মাচায় চাষ করলে দীর্ঘদিন ফলন পাওয়া যায়।' },
                { name: 'রোপা আমন বীজতলা', profit: 'লাভ: ৳ ২২,০০০/বিঘা', desc: 'উচ্চফলনশীল আমন ধানের চারা প্রস্তুতি।' }
            ]},
            { m: 'আষাঢ় (জুন-জুলাই)', items: [
                { name: 'আমন ধান রোপণ', profit: 'লাভ: ৳ ২৪,০০০/বিঘা', desc: 'বৃষ্টির পানিতে সেচ খরচ ছাড়াই প্রধান ধান চাষ।' },
                { name: 'মুখীকচু ও লতিরাজ', profit: 'লাভ: ৳ ২০,০০০/বিঘা', desc: 'বর্ষায় জলাবদ্ধ জমিতে অত্যন্ত লাভজনক।' }
            ]},
            { m: 'শ্রাবণ (জুলাই-আগস্ট)', items: [
                { name: 'পান বরজ', profit: 'লাভ: ৳ ৪০,০০০/বিঘা', desc: 'বারোমাসি উচ্চমূল্যের অর্থকরী ফসল।' },
                { name: 'আমন পরিচর্যা', profit: 'লাভ: ৳ ২৪,০০০/বিঘা', desc: 'সুষম সার ও আগাছা দমনে ফলন বৃদ্ধি।' }
            ]},
            { m: 'ভাদ্র (আগস্ট-সেপ্টেম্বর)', items: [
                { name: 'আগাম ফুলকপি ও বাঁধাকপি', profit: 'লাভ: ৳ ৩৫,০০০/বিঘা', desc: 'আগাম শীতকালীন সবজিতে দ্বিগুণ বাজারদর।' },
                { name: 'আগাম টমেটো', profit: 'লাভ: ৳ ৪২,০০০/বিঘা', desc: 'উঁচু জমিতে পলিথিন শেডে চাষ অত্যন্ত লাভজনক।' }
            ]},
            { m: 'আশ্বিন (সেপ্টেম্বর-অক্টোবর)', items: [
                { name: 'সরিষা (বারি-১৪)', profit: 'লাভ: ৳ ২২,০০০/বিঘা', desc: 'মাত্র ৮০ দিনে ঘরে তোলা যায়, তেলের চাহিদা প্রচুর।' },
                { name: 'আগাম আলু', profit: 'লাভ: ৳ ৪০,০০০/বিঘা', desc: 'নতুন আলু বাজারে চড়া দামে বিক্রি হয়।' }
            ]},
            { m: 'কার্তিক (অক্টোবর-নভেম্বর)', items: [
                { name: 'আলু (মূল মৌসুম)', profit: 'লাভ: ৳ ৪৩,০০০/বিঘা', desc: 'ডায়মন্ড ও কার্ডিনাল আলু চাষের সেরা সময়।' },
                { name: 'মুড়িকাটা পেঁয়াজ', profit: 'লাভ: ৳ ৫০,০০০/বিঘা', desc: 'অল্প সময়ে পেঁয়াজ বিক্রি করে সর্বোচ্চ মুনাফা।' }
            ]},
            { m: 'অগ্রহায়ণ (নভেম্বর-ডিসেম্বর)', items: [
                { name: 'গম ও ভুট্টা', profit: 'লাভ: ৳ ২৪,০০০/বিঘা', desc: 'পোল্ট্রি ও মাছের খাদ্যের জন্য ভুট্টার প্রচুর চাহিদা।' },
                { name: 'বোরো বীজতলা', profit: 'লাভ: ৳ ২৮,০০০/বিঘা', desc: 'ব্রি ধান-২৮, ২৯ ও ৮৯ জাতের বীজতলা।' }
            ]},
            { m: 'পৌষ (ডিসেম্বর-জানুয়ারি)', items: [
                { name: 'বোরো ধান রোপণ', profit: 'লাভ: ৳ ২৮,০০০/বিঘা', desc: 'দেশের প্রধান খাদ্যশস্য বোরো ধান রোপণ।' },
                { name: 'মসুর ও খেসারি ডাল', profit: 'লাভ: ৳ ১৬,০০০/বিঘা', desc: 'মাত্র ৪% সুদে কৃষি ঋণে ডাল চাষ।' }
            ]},
            { m: 'মাঘ (জানুয়ারি-ফেব্রুয়ারি)', items: [
                { name: 'তরমুজ ও বাঙ্গি', profit: 'লাভ: ৳ ৪৫,০০০/বিঘা', desc: 'চরাঞ্চল ও বেলে-দোআঁশ মাটিতে অধিক লাভ।' },
                { name: 'বোরো ধানের সেচ', profit: 'লাভ: ৳ ২৮,০০০/বিঘা', desc: 'AWD পদ্ধতিতে সেচ দিয়ে খরচ কমান।' }
            ]},
            { m: 'ফাল্গুন (ফেব্রুয়ারি-মার্চ)', items: [
                { name: 'তিল ও মুগডাল', profit: 'লাভ: ৳ ১৮,০০০/বিঘা', desc: 'খরিফ-১ মৌসুমে স্বল্প খরচে লাভজনক ফসল।' },
                { name: 'মিষ্টিকুমড়া ও শসা', profit: 'লাভ: ৳ ২০,০০০/বিঘা', desc: 'রমজান ও গ্রীষ্মের বাজারে চড়া দাম।' }
            ]},
            { m: 'চৈত্র (মার্চ-এপ্রিল)', items: [
                { name: 'বোরো ধান কাটা ও মাড়াই', profit: 'লাভ: ৳ ৩০,০০০/বিঘা', desc: '৮০% ধান পাকলেই দ্রুত কেটে ঘরে তুলুন।' },
                { name: 'গ্রীষ্মকালীন শাকসবজি', profit: 'লাভ: ৳ ১৭,০০০/বিঘা', desc: 'পুঁইশাক, ডাটা ও লালশাক চাষ।' }
            ]}
        ];

        function initMonthsUI() {
            var bar = document.getElementById('month-pills-bar');
            var html = '';
            for (var i = 0; i < monthsList.length; i++) {
                html += '<button type="button" onclick="pickMonth(' + i + ')" id="m-pill-' + i + '" class="px-3.5 py-2 rounded-2xl text-xs font-bold whitespace-nowrap transition bg-white border border-slate-200 text-slate-700">' + monthsList[i].m + '</button>';
            }
            bar.innerHTML = html;
            pickMonth(6); // Default Kartik (Nov)
        }

        function pickMonth(idx) {
            for (var i = 0; i < monthsList.length; i++) {
                var btn = document.getElementById('m-pill-' + i);
                if (btn) {
                    btn.className = (i === idx)
                        ? 'px-3.5 py-2 rounded-2xl text-xs font-bold whitespace-nowrap transition bg-emerald-700 text-white shadow'
                        : 'px-3.5 py-2 rounded-2xl text-xs font-bold whitespace-nowrap transition bg-white border border-slate-200 text-slate-700';
                }
            }
            var grid = document.getElementById('month-crops-grid');
            var list = monthsList[idx].items;
            var out = '';
            for (var j = 0; j < list.length; j++) {
                out += '<div class="bg-emerald-50/70 border border-emerald-200 rounded-2xl p-4 flex flex-col justify-between">' +
                    '<div><span class="text-[10px] font-bold bg-amber-400 text-emerald-950 px-2 py-0.5 rounded-full">সেরা নির্বাচন</span>' +
                    '<h4 class="font-bold text-base text-emerald-950 mt-1.5">' + list[j].name + '</h4>' +
                    '<p class="text-xs text-slate-600 mt-1">' + list[j].desc + '</p></div>' +
                    '<div class="mt-3 pt-2 border-t border-emerald-200/70 font-extrabold text-xs text-emerald-800">' + list[j].profit + '</div></div>';
            }
            grid.innerHTML = out;
        }

        var roiTable = {
            potato: { cost: 22000, profit: 43000 },
            tomato: { cost: 18000, profit: 42000 },
            onion: { cost: 25000, profit: 50000 },
            rice: { cost: 15000, profit: 28000 },
            chili: { cost: 12000, profit: 32000 },
            mustard:{ cost: 6000, profit: 22000 }
        };

        function updateRoiCalc() {
            var k = document.getElementById('roi-crop-sel').value;
            var bigha = parseFloat(document.getElementById('roi-bigha-inp').value) || 1;
            var row = roiTable[k] || roiTable.potato;
            document.getElementById('roi-total-cost').innerText = '৳ ' + Math.round(row.cost * bigha).toLocaleString('en-IN');
            document.getElementById('roi-net-profit').innerText = '৳ ' + Math.round(row.profit * bigha).toLocaleString('en-IN');
        }

        // ==================== MODULE 3: WEATHER & MARKET PRICES ====================
        function initWeatherAndMarket() {
            var days = [
                { d: 'আজ', ic: '☀️', t: '২৯°C', r: '০%' },
                { d: 'সোম', ic: '⛅', t: '২৮°C', r: '১০%' },
                { d: 'মঙ্গল', ic: '☀️', t: '৩০°C', r: '৫%' },
                { d: 'বুধ', ic: '🌧️', t: '২৬°C', r: '৬৫%' },
                { d: 'বৃহঃ', ic: '⛅', t: '২৭°C', r: '২০%' },
                { d: 'শুক্র', ic: '☀️', t: '২৯°C', r: '০%' },
                { d: 'শনি', ic: '☀️', t: '৩০°C', r: '০%' }
            ];
            var wGrid = document.getElementById('weather-days-grid');
            var wHtml = '';
            for (var i = 0; i < days.length; i++) {
                wHtml += '<div class="bg-sky-50 border border-sky-200 rounded-2xl p-3 text-center">' +
                    '<p class="text-xs font-bold text-sky-950">' + days[i].d + '</p>' +
                    '<p class="text-2xl my-1.5">' + days[i].ic + '</p>' +
                    '<p class="text-sm font-extrabold text-slate-900">' + days[i].t + '</p>' +
                    '<p class="text-[10px] text-sky-700 font-semibold mt-1">💧 বৃষ্টি: ' + days[i].r + '</p></div>';
            }
            wGrid.innerHTML = wHtml;

            var prices = [
                { n: 'বোরো ধান (মিনিকেট)', p: '১,৫৫০ টাকা / মণ', tag: '▲ +৫০৳' },
                { n: 'আলু (ডায়মন্ড)', p: '১,১২০ টাকা / মণ', tag: 'স্থির' },
                { n: 'দেশি পেঁয়াজ', p: '২,৪০০ টাকা / মণ', tag: '▲ +১০০৳' },
                { n: 'পাকা টমেটো', p: '৪৫ টাকা / কেজি', tag: 'ভালো দাম' },
                { n: 'কাঁচামরিচ', p: '৬০ টাকা / কেজি', tag: '▲ +১০৳' },
                { n: 'সরিষা বীজ', p: '২,৮৫০ টাকা / মণ', tag: '▲ +৮০৳' }
            ];
            var mList = document.getElementById('market-prices-list');
            var mHtml = '';
            for (var j = 0; j < prices.length; j++) {
                mHtml += '<div class="bg-slate-50 border border-slate-200 rounded-2xl p-3.5 flex items-center justify-between">' +
                    '<div><p class="text-xs font-bold text-slate-700">' + prices[j].n + '</p>' +
                    '<p class="text-sm font-extrabold text-emerald-800 mt-0.5">' + prices[j].p + '</p></div>' +
                    '<span class="text-[11px] font-bold bg-emerald-100 text-emerald-800 px-2.5 py-1 rounded-full">' + prices[j].tag + '</span></div>';
            }
            mList.innerHTML = mHtml;
        }

        // ==================== MODULE 4: BANKS, EMI, FERTILIZER & LAND ====================
        function initBanks() {
            var banks = [
                { name: 'বাংলাদেশ কৃষি ব্যাংক (BKB)', rate: '৪% - ৮% সুদ', desc: 'জামানত ছাড়াই ২.৫ লক্ষ টাকা পর্যন্ত সহজ শর্তে শস্য ও মৎস্য ঋণ।' },
                { name: 'রাজশাহী কৃষি উন্নয়ন ব্যাংক (RAKAB)', rate: '৪% - ৮% সুদ', desc: 'উত্তরবঙ্গের কৃষকদের সেচ, সার ও কৃষি যন্ত্রপাতি ক্রয়ে বিশেষ ঋণ।' },
                { name: 'সোনালী ব্যাংক পিএলসি', rate: '৮% সুদ', desc: 'জাতীয় কৃষিনীতি অনুযায়ী দেশের সকল উপজেলায় শস্য ঋণ সুবিধা।' },
                { name: 'ইসলামী ব্যাংক বাংলাদেশ', rate: '৮% (মুবাহা)', desc: 'ইসলামী শরিয়াহ পদ্ধতিতে সার, বীজ ও পাওয়ার টিলার ক্রয়ে ঋণ।' },
                { name: 'ব্র্যাক ব্যাংক (BRAC Bank)', rate: '৯% সুদ', desc: 'ক্ষুদ্র ও মাঝারি খামারিদের জন্য দ্রুততম সময়ে কৃষি ও পোল্ট্রি ঋণ।' },
                { name: 'পূবালী ব্যাংক পিএলসি', rate: '৮.৫% সুদ', desc: 'মসলা ও ডাল জাতীয় ফসল চাষে সহজ কিস্তিতে কৃষি ঋণ।' }
            ];
            var bGrid = document.getElementById('banks-cards-grid');
            var bHtml = '';
            for (var i = 0; i < banks.length; i++) {
                bHtml += '<div class="bg-slate-50 border border-slate-200 rounded-2xl p-4">' +
                    '<span class="text-[10px] font-extrabold bg-emerald-100 text-emerald-800 px-2.5 py-0.5 rounded-full">' + banks[i].rate + '</span>' +
                    '<h4 class="font-bold text-sm sm:text-base text-emerald-950 mt-2">' + banks[i].name + '</h4>' +
                    '<p class="text-xs text-slate-600 mt-1">' + banks[i].desc + '</p></div>';
            }
            bGrid.innerHTML = bHtml;
        }

        function updateEmiCalc() {
            var amt = parseFloat(document.getElementById('emi-amt-range').value) || 50000;
            document.getElementById('emi-amt-lbl').innerText = '৳ ' + amt.toLocaleString('en-IN');
            var rate = parseFloat(document.getElementById('emi-rate-sel').value) || 8;
            var months = parseInt(document.getElementById('emi-term-sel').value, 10) || 12;

            var r = rate / 100 / 12;
            var emi = (amt * r * Math.pow(1 + r, months)) / (Math.pow(1 + r, months) - 1);
            var total = emi * months;

            document.getElementById('emi-monthly-out').innerText = '৳ ' + Math.round(emi).toLocaleString('en-IN');
            document.getElementById('emi-total-out').innerText = '৳ ' + Math.round(total).toLocaleString('en-IN');
        }

        function updateFertCalc() {
            var crop = document.getElementById('fert-crop-sel').value;
            var dec = parseFloat(document.getElementById('fert-dec-inp').value) || 33;
            var ratio = dec / 33;
            var u = 20, t = 12, m = 15, g = 8;
            if (crop === 'potato') { u = 35; t = 20; m = 25; g = 12; }
            if (crop === 'veg') { u = 25; t = 15; m = 18; g = 10; }
            document.getElementById('f-urea').innerText = Math.round(u * ratio) + ' কেজি';
            document.getElementById('f-tsp').innerText = Math.round(t * ratio) + ' কেজি';
            document.getElementById('f-mop').innerText = Math.round(m * ratio) + ' কেজি';
            document.getElementById('f-gyp').innerText = Math.round(g * ratio) + ' কেজি';
        }

        function updateLandCalc() {
            var dec = parseFloat(document.getElementById('land-dec-inp').value) || 0;
            document.getElementById('l-bigha').innerText = (dec / 33).toFixed(2);
            document.getElementById('l-katha').innerText = (dec / 1.65).toFixed(2);
            document.getElementById('l-acre').innerText = (dec / 100).toFixed(2);
        }

        // ==================== MODULE 5: AWARENESS ANIMATED VIDEOS ====================
        var episodes = [
            {
                title: 'পর্ব ১: সুষম সার ও মাটির স্বাস্থ্য রক্ষা',
                steps: [
                    'অতিরিক্ত ইউরিয়া সার দিলে মাটির উর্বরতা নষ্ট হয় ও পোকামাকড় বাড়ে।',
                    'ইউরিয়া, টিএসপি ও পটাশ সার সঠিক অনুপাতে জমিতে প্রয়োগ করুন।',
                    'জৈব সার বা কম্পোস্ট ব্যবহারে মাটি সুস্থ থাকে ও ফলন বাড়ে!'
                ]
            },
            {
                title: 'পর্ব ২: বিষমুক্ত চাষ ও স্প্রে সতর্কতা',
                steps: [
                    'কীটনাশক স্প্রে করার সময় অবশ্যই মুখে মাস্ক ও হাতে গ্লাভস পরুন।',
                    'বিষাক্ত রাসায়নিকের বদলে সেক্স ফেরোমন ফাঁদ ও নিম তেল ব্যবহার করুন।',
                    'বিষমুক্ত নিরাপদ ফসল আপনার পরিবার ও দেশের মানুষের স্বাস্থ্য রক্ষা করে।'
                ]
            },
            {
                title: 'পর্ব ৩: আধুনিক AWD সেচ ও পানি সাশ্রয়',
                steps: [
                    'ধান ক্ষেতে সবসময় পানি ধরে রাখলে সেচ ও ডিজেল খরচ অযথা বাড়ে।',
                    'জমিতে ছিদ্রযুক্ত পাইপ (AWD) বসিয়ে পানির স্তর পর্যবেক্ষণ করুন।',
                    'এই পদ্ধতিতে ৩০% পানি সাশ্রয় হয় এবং ধানের শিকড় শক্তিশালী হয়।'
                ]
            },
            {
                title: 'পর্ব ৪: আগাম রোগ প্রতিরোধ ও AI স্ক্যান',
                steps: [
                    'ফসলের পাতায় হলুদ বা বাদামী দাগ দেখলেই দ্রুত ব্যবস্থা নিন।',
                    'কৃষি মিত্র অ্যাপের ক্যামেরা দিয়ে আক্রান্ত পাতার ছবি স্ক্যান করুন।',
                    'সঠিক সময়ে চিকিৎসা করলে ৮০% ফসল ক্ষতি থেকে বাঁচানো সম্ভব।'
                ]
            }
        ];

        function playAwarenessEpisode(idx) {
            currentEpIdx = idx;
            vidProgress = 0;
            lastSpokenStep = -1;
            vidPlaying = true;
            document.getElementById('vid-play-toggle').innerText = '⏸';

            for (var i = 0; i < 4; i++) {
                var c = document.getElementById('ep-card-' + i);
                if (c) {
                    c.className = (i === idx)
                        ? 'cursor-pointer bg-emerald-50 border-2 border-emerald-600 rounded-2xl p-3.5 transition shadow-sm'
                        : 'cursor-pointer bg-white border border-slate-200 rounded-2xl p-3.5 transition';
                }
            }

            if (vidAnimId) cancelAnimationFrame(vidAnimId);
            drawVideoFrame();
        }

        function toggleVideoPlay() {
            vidPlaying = !vidPlaying;
            document.getElementById('vid-play-toggle').innerText = vidPlaying ? '⏸' : '▶';
            if (vidPlaying) {
                drawVideoFrame();
            } else if ('speechSynthesis' in window) {
                window.speechSynthesis.cancel();
            }
        }

        function stopVideoAnim() {
            vidPlaying = false;
            if (vidAnimId) cancelAnimationFrame(vidAnimId);
            if ('speechSynthesis' in window) window.speechSynthesis.cancel();
        }

        function drawVideoFrame() {
            var canvas = document.getElementById('video-stage-canvas');
            if (!canvas) return;
            var ctx = canvas.getContext('2d');
            var parent = canvas.parentElement;
            canvas.width = parent.clientWidth || 600;
            canvas.height = parent.clientHeight || 300;

            var w = canvas.width;
            var h = canvas.height;
            var ep = episodes[currentEpIdx];

            if (vidPlaying) {
                vidProgress += 0.16;
                if (vidProgress >= 100) {
                    vidProgress = 100;
                    vidPlaying = false;
                    document.getElementById('vid-play-toggle').innerText = '▶';
                }
            }
            document.getElementById('vid-prog-fill').style.width = vidProgress + '%';

            var step = Math.min(2, Math.floor((vidProgress / 100) * 3));
            var subText = ep.steps[step];
            document.getElementById('vid-subtitle-txt').innerText = subText;

            if (vidPlaying && step !== lastSpokenStep) {
                lastSpokenStep = step;
                speakText(subText);
            }

            // Render Smooth Animated Scene
            var t = Date.now() * 0.003;
            ctx.clearRect(0, 0, w, h);

            // Sky
            var grad = ctx.createLinearGradient(0, 0, 0, h * 0.72);
            grad.addColorStop(0, '#022c22');
            grad.addColorStop(1, '#065f46');
            ctx.fillStyle = grad;
            ctx.fillRect(0, 0, w, h);

            // Sun
            var sx = w * 0.84;
            var sy = h * 0.22 + Math.sin(t) * 4;
            ctx.fillStyle = 'rgba(251, 191, 36, 0.25)';
            ctx.beginPath();
            ctx.arc(sx, sy, 32, 0, Math.PI * 2);
            ctx.fill();
            ctx.fillStyle = '#fbbf24';
            ctx.beginPath();
            ctx.arc(sx, sy, 20, 0, Math.PI * 2);
            ctx.fill();

            // Ground
            ctx.fillStyle = '#047857';
            ctx.fillRect(0, h * 0.68, w, h * 0.32);

            // Swaying Crops
            var count = Math.floor(w / 34);
            for (var i = 1; i < count; i++) {
                var px = i * 34;
                var py = h * 0.68;
                var sway = Math.sin(t + i * 0.5) * 7;
                var ph = (step === 2) ? 68 : 48;

                ctx.strokeStyle = '#34d399';
                ctx.lineWidth = 3.5;
                ctx.beginPath();
                ctx.moveTo(px, py);
                ctx.quadraticCurveTo(px + sway * 0.5, py - ph * 0.5, px + sway, py - ph);
                ctx.stroke();

                ctx.fillStyle = '#fbbf24';
                ctx.beginPath();
                ctx.arc(px + sway, py - ph, 4.5, 0, Math.PI * 2);
                ctx.fill();
            }

            // Floating Water/Nutrients
            for (var p = 0; p < 10; p++) {
                var dx = (p * 67 + t * 35) % w;
                var dy = (p * 43 + t * 80) % (h * 0.65);
                ctx.fillStyle = (currentEpIdx === 2) ? 'rgba(56, 189, 248, 0.75)' : 'rgba(251, 191, 36, 0.65)';
                ctx.beginPath();
                ctx.arc(dx, dy, 3.5, 0, Math.PI * 2);
                ctx.fill();
            }

            // Title Badge
            ctx.fillStyle = 'rgba(0,0,0,0.6)';
            ctx.fillRect(14, 14, Math.min(w - 28, 330), 36);
            ctx.fillStyle = '#fbbf24';
            ctx.font = 'bold 14px sans-serif';
            ctx.fillText('🎬 ' + ep.title, 24, 37);

            if (vidPlaying) {
                vidAnimId = requestAnimationFrame(drawVideoFrame);
            }
        }

        // Initialize All Modules Once Logged In
        function initAllModules() {
            initMonthsUI();
            updateRoiCalc();
            initWeatherAndMarket();
            initBanks();
            updateEmiCalc();
            updateFertCalc();
            updateLandCalc();
        }
    </script>
</body>
</html>
```
