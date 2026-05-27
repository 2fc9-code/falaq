
<!DOCTYPE html>
<html lang="ar" dir="rtl" id="html-root">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>بوابة الزمن الفلكية | Chronos Portal</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts (Tajawal & Plus Jakarta Sans) -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&family=Tajawal:wght@300;400;500;700;900&display=swap" rel="stylesheet">
    
    <style>
        body {
            font-family: 'Tajawal', 'Plus Jakarta Sans', sans-serif;
            background: radial-gradient(circle at center, #0b0f19 0%, #030712 100%);
        }
        .font-en {
            font-family: 'Plus Jakarta Sans', sans-serif;
        }
        .glass-panel {
            background: rgba(13, 18, 30, 0.75);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border: 1px rgba(255, 255, 255, 0.06) solid;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }
        .glass-panel:hover {
            border-color: rgba(99, 102, 241, 0.25);
            box-shadow: 0 10px 30px -10px rgba(99, 102, 241, 0.15);
        }
        .moon-sphere {
            position: relative;
            width: 140px;
            height: 140px;
            border-radius: 50%;
            background-color: #111827;
            overflow: hidden;
            box-shadow: inset -10px -10px 30px rgba(0,0,0,0.9), 0 0 35px rgba(253, 224, 71, 0.2);
        }
        .moon-light {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            border-radius: 50%;
            background-color: #fef08a;
            transition: all 0.6s cubic-bezier(0.4, 0, 0.2, 1);
        }
        .moon-shadow {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            border-radius: 50%;
            background-color: #0d121e;
            transition: all 0.6s cubic-bezier(0.4, 0, 0.2, 1);
        }
        /* Custom progress ring styling */
        .progress-ring__circle {
            transition: stroke-dashoffset 0.8s ease-in-out;
            transform: rotate(-90deg);
            transform-origin: 50% 50%;
        }
    </style>
</head>
<body class="text-gray-100 min-h-screen flex flex-col justify-between selection:bg-indigo-500 selection:text-white transition-colors duration-300">

    <!-- Header Section -->
    <header class="border-b border-slate-800/80 bg-slate-950/70 backdrop-blur-md sticky top-0 z-50">
        <div class="max-w-6xl mx-auto px-4 py-3 flex items-center justify-between gap-4">
            <!-- App Logo/Title -->
            <div class="flex items-center gap-3">
                <div class="bg-gradient-to-tr from-indigo-600 to-purple-600 p-2.5 rounded-xl shadow-lg shadow-indigo-500/20">
                    <i class="fa-solid fa-compass text-xl text-white animate-spin-slow"></i>
                </div>
                <div>
                    <h1 id="app-title" class="text-lg sm:text-xl font-black bg-gradient-to-l from-indigo-400 via-purple-400 to-amber-300 bg-clip-text text-transparent">بوابة الزمن الفلكية</h1>
                    <p id="app-subtitle" class="text-[11px] text-slate-400">حساب الأعمار، جميع التقويمات، وحالة رصد القمر</p>
                </div>
            </div>
            
            <!-- Controls (Language Toggle & Clock) -->
            <div class="flex items-center gap-3">
                <div class="hidden md:block text-xs bg-slate-900/90 px-3 py-2 rounded-xl border border-slate-800 text-slate-300">
                    <span id="current-date-lbl" class="font-bold text-amber-400">اليوم:</span>
                    <span id="current-date-display">...</span>
                </div>
                <button onclick="toggleLanguage()" class="bg-indigo-600 hover:bg-indigo-500 text-white font-bold text-xs px-3.5 py-2 rounded-xl shadow-md shadow-indigo-500/10 flex items-center gap-1.5 transition-all">
                    <i class="fa-solid fa-language text-sm"></i>
                    <span id="lang-btn-text">English</span>
                </button>
            </div>
        </div>
    </header>

    <!-- Main Space -->
    <main class="flex-grow max-w-6xl w-full mx-auto px-4 py-8">
        
        <!-- Hero Section -->
        <section class="mb-10 text-center">
            <h2 id="hero-title" class="text-3xl sm:text-5xl font-black text-white mb-4 leading-tight">سافر عبر التقويمات الكونية</h2>
            <p id="hero-desc" class="text-slate-400 max-w-3xl mx-auto mb-8 text-sm sm:text-base leading-relaxed">
                أدخل تاريخ ميلادك لاستكشاف عمرك بمختلف الحسابات الزمنية من التقاويم الهجرية والميلادية والفارسية والصينية، واكشف شكل قمر ليلة ولادتك، بالإضافة لأسرار برجك الفلكي وفصل ميلادك وتفاصيل مذهلة أخرى.
            </p>
            
            <!-- Input Panel -->
            <div class="glass-panel p-6 rounded-3xl max-w-xl mx-auto shadow-2xl border border-indigo-500/20">
                <div class="flex flex-col sm:flex-row items-center gap-4">
                    <div class="w-full text-right" id="input-container">
                        <label for="birth-date" id="input-label" class="block text-xs font-bold text-slate-300 mb-2 uppercase tracking-wider">اختر تاريخ ميلادك الميلادي:</label>
                        <input type="date" id="birth-date" class="w-full bg-slate-900/90 border border-slate-700 rounded-xl px-4 py-3 text-white focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:border-transparent transition-all" value="2000-01-01">
                    </div>
                    <button onclick="calculateAll()" id="calc-btn" class="w-full sm:w-auto sm:self-end bg-gradient-to-l from-indigo-600 to-purple-600 hover:from-indigo-500 hover:to-purple-500 text-white font-bold px-8 py-3.5 rounded-xl transition-all shadow-lg shadow-indigo-500/20 flex items-center justify-center gap-2 whitespace-nowrap">
                        <i class="fa-solid fa-wand-magic-sparkles animate-pulse"></i>
                        <span>احسب الآن</span>
                    </button>
                </div>
                <p id="error-msg" class="text-red-400 text-xs mt-3 hidden text-right"><i class="fa-solid fa-triangle-exclamation mr-1"></i> يرجى إدخال تاريخ ميلاد صحيح بالماضي.</p>
            </div>
        </section>

        <!-- Results Dashboard -->
        <div id="results-container" class="hidden space-y-8 animate-fade-in">
            
            <!-- Row 1: Core Age & Moon & Birth Properties -->
            <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
                
                <!-- Card 1: Gregorian Age -->
                <div class="glass-panel p-6 sm:p-8 rounded-3xl shadow-xl flex flex-col justify-between">
                    <div>
                        <div class="flex items-center justify-between mb-4">
                            <span id="gregorian-badge" class="bg-indigo-500/10 text-indigo-400 border border-indigo-500/20 text-xs px-3 py-1.5 rounded-full font-bold">التقويم الميلادي الرئيسي</span>
                            <i class="fa-solid fa-cake-candles text-xl text-indigo-400"></i>
                        </div>
                        <h3 id="gregorian-title" class="text-xl font-bold mb-6 text-white">العمر بالتفصيل الدقيق</h3>
                        
                        <!-- Big Numbers Grid -->
                        <div class="grid grid-cols-3 gap-3 text-center mb-6">
                            <div class="bg-slate-900/60 p-4 rounded-2xl border border-slate-800/80">
                                <span id="age-years" class="block text-3xl sm:text-4xl font-black text-indigo-400">0</span>
                                <span id="lbl-years" class="text-xs text-slate-400 mt-1 block">سنة</span>
                            </div>
                            <div class="bg-slate-900/60 p-4 rounded-2xl border border-slate-800/80">
                                <span id="age-months" class="block text-3xl sm:text-4xl font-black text-purple-400">0</span>
                                <span id="lbl-months" class="text-xs text-slate-400 mt-1 block">شهر</span>
                            </div>
                            <div class="bg-slate-900/60 p-4 rounded-2xl border border-slate-800/80">
                                <span id="age-days" class="block text-3xl sm:text-4xl font-black text-pink-400">0</span>
                                <span id="lbl-days" class="text-xs text-slate-400 mt-1 block">يوم</span>
                            </div>
                        </div>

                        <!-- Micro Metrics -->
                        <div class="space-y-2.5 text-xs text-slate-300 border-t border-slate-800/80 pt-5">
                            <div class="flex justify-between">
                                <span id="lbl-weekday" class="text-slate-400 font-medium">يوم الولادة:</span>
                                <span id="val-weekday" class="font-bold text-white">...</span>
                            </div>
                            <div class="flex justify-between">
                                <span id="lbl-tot-weeks" class="text-slate-400 font-medium">مجموع الأسابيع المعاشة:</span>
                                <span id="val-tot-weeks" class="font-bold text-indigo-300">...</span>
                            </div>
                            <div class="flex justify-between">
                                <span id="lbl-tot-days" class="text-slate-400 font-medium">مجموع الأيام المعاشة:</span>
                                <span id="val-tot-days" class="font-bold text-purple-300">...</span>
                            </div>
                            <div class="flex justify-between">
                                <span id="lbl-tot-hours" class="text-slate-400 font-medium">مجموع الساعات المعاشة:</span>
                                <span id="val-tot-hours" class="font-bold text-pink-300">...</span>
                            </div>
                        </div>
                    </div>

                    <!-- Next Birthday & Circular Progress -->
                    <div class="mt-6 bg-slate-900/50 p-4 rounded-2xl border border-slate-800 flex items-center justify-between gap-4">
                        <div class="flex items-center gap-3">
                            <!-- SVG Circular Progress Bar -->
                            <div class="relative w-12 h-12">
                                <svg class="w-full h-full">
                                    <circle class="text-slate-800" stroke-width="4" stroke="currentColor" fill="transparent" r="20" cx="24" cy="24"/>
                                    <circle class="text-pink-500 progress-ring__circle" stroke-width="4" id="progress-circle" stroke-linecap="round" stroke="currentColor" fill="transparent" r="20" cx="24" cy="24" stroke-dasharray="125.6" stroke-dashoffset="125.6"/>
                                </svg>
                                <span id="progress-percent" class="absolute inset-0 flex items-center justify-center text-[10px] font-bold text-pink-400">0%</span>
                            </div>
                            <div>
                                <span id="lbl-countdown-title" class="text-[10px] text-slate-400 block font-bold">يوم ميلادك القادم</span>
                                <span id="val-countdown-txt" class="text-xs text-white font-medium">...</span>
                            </div>
                        </div>
                        <span id="val-countdown-days" class="text-sm font-extrabold text-pink-400 bg-pink-500/10 px-2.5 py-1.5 rounded-lg border border-pink-500/20">...</span>
                    </div>
                </div>

                <!-- Card 2: Lunar Phase Info -->
                <div class="glass-panel p-6 sm:p-8 rounded-3xl shadow-xl flex flex-col items-center justify-between text-center moon-glow border-amber-500/10">
                    <div class="w-full">
                        <div class="flex items-center justify-between mb-4 w-full">
                            <span id="moon-badge" class="bg-amber-500/10 text-amber-400 border border-amber-500/20 text-xs px-3 py-1.5 rounded-full font-bold">الرصد القمري الفلكي</span>
                            <i class="fa-solid fa-moon text-xl text-amber-300"></i>
                        </div>
                        <h3 id="moon-title" class="text-xl font-bold text-white">حالة القمر عند ولادتك</h3>
                    </div>

                    <!-- Moon sphere visuals -->
                    <div class="my-5">
                        <div class="moon-sphere mx-auto">
                            <div id="moon-light-elem" class="moon-light"></div>
                            <div id="moon-shadow-elem" class="moon-shadow"></div>
                        </div>
                    </div>

                    <div class="w-full">
                        <h4 id="val-moon-name" class="text-lg font-black text-amber-300 mb-1">...</h4>
                        <p id="val-moon-ill" class="text-xs text-amber-400/80 mb-4 font-bold">...</p>
                        <div class="bg-slate-950/80 p-4 rounded-2xl border border-slate-800 text-xs text-slate-300 text-right leading-relaxed max-h-36 overflow-y-auto">
                            <span id="lbl-moon-desc-title" class="font-bold text-amber-400 block mb-1"><i class="fa-solid fa-wand-magic-sparkles ml-1"></i> الروح القمريّة للولادة:</span>
                            <span id="val-moon-desc">...</span>
                        </div>
                    </div>
                </div>

                <!-- Card 3: Astrological Zodiac & Season -->
                <div class="glass-panel p-6 sm:p-8 rounded-3xl shadow-xl flex flex-col justify-between" id="season-themed-card">
                    <div>
                        <div class="flex items-center justify-between mb-4">
                            <span id="zodiac-badge" class="bg-emerald-500/10 text-emerald-400 border border-emerald-500/20 text-xs px-3 py-1.5 rounded-full font-bold">الأبراج والفصول الفلكية</span>
                            <i class="fa-solid fa-sparkles text-xl text-emerald-300"></i>
                        </div>
                        <h3 id="zodiac-card-title" class="text-xl font-bold mb-4 text-white">البرج الغربي والخصائص</h3>
                        
                        <!-- Big Zodiac Icon and Title -->
                        <div class="flex items-center gap-4 bg-slate-900/60 p-4 rounded-2xl border border-slate-800/80 mb-4">
                            <div class="bg-indigo-600/20 text-indigo-400 p-4 rounded-xl text-3xl" id="val-zodiac-icon-container">
                                <i class="fa-solid fa-sun" id="val-zodiac-icon"></i>
                            </div>
                            <div class="text-right">
                                <span id="lbl-your-zodiac" class="text-[10px] text-slate-400 block font-bold">برجك الميلادي</span>
                                <span id="val-zodiac-name" class="text-lg font-black text-indigo-300">...</span>
                            </div>
                        </div>

                        <!-- Season and Extra details -->
                        <div class="space-y-3 text-xs text-slate-300 border-t border-slate-800/80 pt-4">
                            <div class="flex justify-between items-center">
                                <span id="lbl-zodiac-date" class="text-slate-400">نطاق تاريخ البرج:</span>
                                <span id="val-zodiac-range" class="font-bold text-white">...</span>
                            </div>
                            <div class="flex justify-between items-center">
                                <span id="lbl-season-born" class="text-slate-400">فصل ولادتك الفلكي:</span>
                                <span id="val-season-born" class="font-bold text-emerald-400 px-2 py-0.5 rounded bg-emerald-500/10 border border-emerald-500/20">...</span>
                            </div>
                            <div class="flex justify-between items-center">
                                <span id="lbl-lifepath" class="text-slate-400">رقم مسار الحياة (علم الأرقام):</span>
                                <span id="val-lifepath" class="font-extrabold text-amber-300 bg-amber-500/10 px-2.5 py-0.5 rounded-lg border border-amber-500/20">...</span>
                            </div>
                            <div class="flex justify-between items-center">
                                <span id="lbl-birthstone" class="text-slate-400">حجر الميلاد الفلكي:</span>
                                <span id="val-birthstone" class="font-bold text-pink-400">...</span>
                            </div>
                        </div>
                    </div>
                </div>

            </div>

            <!-- Row 2: All 6 Calendars Grid -->
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">

                <!-- 1. Hijri Calendar -->
                <div class="glass-panel p-6 rounded-2xl border border-emerald-500/10 hover:border-emerald-500/30">
                    <div class="flex justify-between items-center mb-4">
                        <h4 id="title-c1" class="font-bold text-emerald-400 flex items-center gap-2 text-sm">
                            <i class="fa-solid fa-star-and-crescent text-base"></i>
                            <span>التقويم الهجري الإسلامي</span>
                        </h4>
                        <span id="type-c1" class="text-[10px] bg-emerald-500/10 text-emerald-400 px-2 py-0.5 rounded-full font-bold">قمري</span>
                    </div>
                    <div class="space-y-3 text-xs">
                        <div class="bg-slate-900/60 p-3 rounded-xl">
                            <span id="lbl-c1-date" class="text-slate-400 block mb-1 font-bold">تاريخ الولادة بالهجري:</span>
                            <span id="val-hijri-date" class="font-black text-emerald-300 text-sm">...</span>
                        </div>
                        <div class="flex justify-between items-center px-1">
                            <span id="lbl-c1-age" class="text-slate-400">العمر الحالي بالتقويم الهجري:</span>
                            <span id="val-hijri-age" class="font-bold text-white">...</span>
                        </div>
                    </div>
                </div>

                <!-- 2. Persian Calendar (Jalali) -->
                <div class="glass-panel p-6 rounded-2xl border border-amber-500/10 hover:border-amber-500/30">
                    <div class="flex justify-between items-center mb-4">
                        <h4 id="title-c2" class="font-bold text-amber-400 flex items-center gap-2 text-sm">
                            <i class="fa-solid fa-seedling text-base"></i>
                            <span>التقويم الهجري الشمسي (الفارسي)</span>
                        </h4>
                        <span id="type-c2" class="text-[10px] bg-amber-500/10 text-amber-400 px-2 py-0.5 rounded-full font-bold">شمسي فلكي</span>
                    </div>
                    <div class="space-y-3 text-xs">
                        <div class="bg-slate-900/60 p-3 rounded-xl">
                            <span id="lbl-c2-date" class="text-slate-400 block mb-1 font-bold">تاريخ الولادة بالفارسية:</span>
                            <span id="val-persian-date" class="font-black text-amber-300 text-sm">...</span>
                        </div>
                        <div class="flex justify-between items-center px-1">
                            <span id="lbl-c2-month" class="text-slate-400">اسم البرج الشمسي (البرج الحركي):</span>
                            <span id="val-persian-month" class="font-bold text-white">...</span>
                        </div>
                    </div>
                </div>

                <!-- 3. Chinese Calendar -->
                <div class="glass-panel p-6 rounded-2xl border border-red-500/10 hover:border-red-500/30">
                    <div class="flex justify-between items-center mb-4">
                        <h4 id="title-c3" class="font-bold text-red-400 flex items-center gap-2 text-sm">
                            <i class="fa-solid fa-dragon text-base"></i>
                            <span>التقويم والبرج الصيني</span>
                        </h4>
                        <span id="type-c3" class="text-[10px] bg-red-500/10 text-red-400 px-2 py-0.5 rounded-full font-bold">قمري شمسي</span>
                    </div>
                    <div class="space-y-3 text-xs">
                        <div class="bg-slate-900/60 p-3 rounded-xl">
                            <span id="lbl-c3-date" class="text-slate-400 block mb-1 font-bold">برجك الصيني السنوي:</span>
                            <span id="val-chinese-zodiac" class="font-black text-red-300 text-sm">...</span>
                        </div>
                        <div class="flex justify-between items-center px-1">
                            <span id="lbl-c3-element" class="text-slate-400">العنصر الفلكي المرافق لولادتك:</span>
                            <span id="val-chinese-element" class="font-bold text-white">...</span>
                        </div>
                    </div>
                </div>

                <!-- 4. Daylight Saving Time (DST) & Climate -->
                <div class="glass-panel p-6 rounded-2xl border border-sky-500/10 hover:border-sky-500/30">
                    <div class="flex justify-between items-center mb-4">
                        <h4 id="title-c4" class="font-bold text-sky-400 flex items-center gap-2 text-sm">
                            <i class="fa-solid fa-clock-rotate-left text-base"></i>
                            <span>التوقيت الصيفي والمناخي</span>
                        </h4>
                        <span id="type-c4" class="text-[10px] bg-sky-500/10 text-sky-400 px-2 py-0.5 rounded-full font-bold">التوقيت المحلي</span>
                    </div>
                    <div class="space-y-3 text-xs">
                        <div class="bg-slate-900/60 p-3 rounded-xl">
                            <span id="lbl-c4-date" class="text-slate-400 block mb-1 font-bold">الحالة يوم ميلادك:</span>
                            <span id="val-dst-status" class="font-black text-sky-300 text-sm">...</span>
                        </div>
                        <div class="flex justify-between items-center px-1">
                            <span id="lbl-c4-climate" class="text-slate-400">طبيعة التوقيت الموسمي:</span>
                            <span id="val-season-details" class="font-bold text-white">...</span>
                        </div>
                    </div>
                </div>

                <!-- 5. Coptic Calendar -->
                <div class="glass-panel p-6 rounded-2xl border border-teal-500/10 hover:border-teal-500/30">
                    <div class="flex justify-between items-center mb-4">
                        <h4 id="title-c5" class="font-bold text-teal-400 flex items-center gap-2 text-sm">
                            <i class="fa-solid fa-ankh text-base"></i>
                            <span>التقويم القبطي والفرعوني القديم</span>
                        </h4>
                        <span id="type-c5" class="text-[10px] bg-teal-500/10 text-teal-400 px-2 py-0.5 rounded-full font-bold">نجمي شعراوي</span>
                    </div>
                    <div class="space-y-3 text-xs">
                        <div class="bg-slate-900/60 p-3 rounded-xl">
                            <span id="lbl-c5-date" class="text-slate-400 block mb-1 font-bold">تاريخ ميلادك القبطي:</span>
                            <span id="val-coptic-date" class="font-black text-teal-300 text-sm">...</span>
                        </div>
                        <div class="flex justify-between items-center px-1">
                            <span id="lbl-c5-month" class="text-slate-400">اسم الشهر الفرعوني التاريخي:</span>
                            <span id="val-coptic-month" class="font-bold text-white">...</span>
                        </div>
                    </div>
                </div>

                <!-- 6. Syriac Calendar -->
                <div class="glass-panel p-6 rounded-2xl border border-purple-500/10 hover:border-purple-500/30">
                    <div class="flex justify-between items-center mb-4">
                        <h4 id="title-c6" class="font-bold text-purple-400 flex items-center gap-2 text-sm">
                            <i class="fa-solid fa-feather-pointed text-base"></i>
                            <span>التقويم السرياني (الرومي)</span>
                        </h4>
                        <span id="type-c6" class="text-[10px] bg-purple-500/10 text-purple-400 px-2 py-0.5 rounded-full font-bold">شمسي قديم</span>
                    </div>
                    <div class="space-y-3 text-xs">
                        <div class="bg-slate-900/60 p-3 rounded-xl">
                            <span id="lbl-c6-date" class="text-slate-400 block mb-1 font-bold">تاريخ ميلادك بالسريانية:</span>
                            <span id="val-syriac-date" class="font-black text-purple-300 text-sm">...</span>
                        </div>
                        <div class="flex justify-between items-center px-1">
                            <span id="lbl-c6-month" class="text-slate-400">تسمية الشهر المشرقية:</span>
                            <span id="val-syriac-month" class="font-bold text-white">...</span>
                        </div>
                    </div>
                </div>

            </div>

        </div>

    </main>

    <!-- Footer Section -->
    <footer class="border-t border-slate-900 bg-slate-950/90 py-6 mt-12 text-center text-xs text-slate-500">
        <div class="max-w-6xl mx-auto px-4 flex flex-col sm:flex-row items-center justify-between gap-4">
            <p id="footer-notes">تم الاعتماد على خوارزميات فلكية ومصفوفات تحويل تاريخية مبسطة ذات موثوقية عالية.</p>
            <p class="font-bold text-slate-400 bg-slate-900 px-4 py-2 rounded-xl border border-slate-800">
                <i class="fa-solid fa-code text-indigo-500 ml-1.5 mr-1.5"></i>
                <span id="footer-credit">تمت البرمجة من قبل محمد ماجد الفريجي</span>
            </p>
        </div>
    </footer>

    <!-- Translation / Translation / Data Dictionaries and Logic -->
    <script>
        // Language state
        let currentLang = 'ar';

        // Translation Dictionary
        const translations = {
            ar: {
                appTitle: "بوابة الزمن الفلكية",
                appSubtitle: "حساب الأعمار، جميع التقويمات، وحالة رصد القمر",
                currentDateLbl: "اليوم:",
                heroTitle: "سافر عبر التقويمات الكونية",
                heroDesc: "أدخل تاريخ ميلادك لاستكشاف عمرك بمختلف الحسابات الزمنية من التقاويم الهجرية والميلادية والفارسية والصينية، واكشف شكل قمر ليلة ولادتك، بالإضافة لأسرار برجك الفلكي وفصل ميلادك وتفاصيل مذهلة أخرى.",
                inputLabel: "اختر تاريخ ميلادك الميلادي:",
                calcBtn: "احسب الآن",
                gregorianBadge: "التقويم الميلادي الرئيسي",
                gregorianTitle: "العمر بالتفصيل الدقيق",
                lblYears: "سنة",
                lblMonths: "شهر",
                lblDays: "يوم",
                lblWeekday: "يوم الولادة:",
                lblTotWeeks: "مجموع الأسابيع المعاشة:",
                lblTotDays: "مجموع الأيام المعاشة:",
                lblTotHours: "مجموع الساعات المعاشة:",
                lblCountdownTitle: "يوم ميلادك القادم",
                moonBadge: "الرصد القمري الفلكي",
                moonTitle: "حالة القمر عند ولادتك",
                lblMoonDescTitle: "الروح القمريّة للولادة:",
                zodiacBadge: "الأبراج والفصول الفلكية",
                zodiacCardTitle: "البرج الغربي والخصائص",
                lblYourZodiac: "برجك الميلادي",
                lblZodiacDate: "نطاق تاريخ البرج:",
                lblSeasonBorn: "فصل ولادتك الفلكي:",
                lblLifepath: "رقم مسار الحياة (علم الأرقام):",
                lblBirthstone: "حجر الميلاد الفلكي:",
                titleC1: "التقويم الهجري الإسلامي",
                typeC1: "قمري",
                lblC1Date: "تاريخ الولادة بالهجري:",
                lblC1Age: "العمر الحالي بالتقويم الهجري:",
                titleC2: "التقويم الهجري الشمسي (الفارسي)",
                typeC2: "شمسي فلكي",
                lblC2Date: "تاريخ الولادة بالفارسية:",
                lblC2Month: "اسم البرج الشمسي (البرج الحركي):",
                titleC3: "التقويم والبرج الصيني",
                typeC3: "قمري شمسي",
                lblC3Date: "برجك الصيني السنوي:",
                lblC3Element: "العنصر الفلكي المرافق لولادتك:",
                titleC4: "التوقيت الصيفي والمناخي",
                typeC4: "التوقيت المحلي",
                lblC4Date: "الحالة يوم ميلادك:",
                lblC4Climate: "طبيعة التوقيت الموسمي:",
                titleC5: "التقويم القبطي والفرعوني القديم",
                typeC5: "نجمي شعراوي",
                lblC5Date: "تاريخ ميلادك القبطي:",
                lblC5Month: "اسم الشهر الفرعوني التاريخي:",
                titleC6: "التقويم السرياني (الرومي)",
                typeC6: "شمسي قديم",
                lblC6Date: "تاريخ ميلادك بالسريانية:",
                lblC6Month: "تسمية الشهر المشرقية:",
                footerNotes: "تم الاعتماد على خوارزميات فلكية ومصفوفات تحويل تاريخية مبسطة ذات موثوقية عالية.",
                footerCredit: "تمت البرمجة من قبل محمد ماجد الفريجي",
                errorMsg: "يرجى إدخال تاريخ ميلاد صحيح بالماضي."
            },
            en: {
                appTitle: "Celestial Time Portal",
                appSubtitle: "Age calculations, multiple calendars, and lunar tracking",
                currentDateLbl: "Today:",
                heroTitle: "Sojourn Through Cosmic Calendars",
                heroDesc: "Enter your birthdate to chart your life across Gregorian, Hijri, Persian, and Chinese calendars. Discover the lunar phase of your birth night, astrological zodiac sign, and extra celestial insights.",
                inputLabel: "Choose your Gregorian date of birth:",
                calcBtn: "Calculate Now",
                gregorianBadge: "Primary Gregorian Calendar",
                gregorianTitle: "Detailed Age Analysis",
                lblYears: "Years",
                lblMonths: "Months",
                lblDays: "Days",
                lblWeekday: "Day of Birth:",
                lblTotWeeks: "Total Weeks Lived:",
                lblTotDays: "Total Days Lived:",
                lblTotHours: "Total Hours Lived:",
                lblCountdownTitle: "Next Birthday",
                moonBadge: "Lunar Observation",
                moonTitle: "Moon Phase at Birth",
                lblMoonDescTitle: "Lunar Birth Spirit:",
                zodiacBadge: "Astrology & Season",
                zodiacCardTitle: "Zodiac Sign & Attributes",
                lblYourZodiac: "Your Astrological Sign",
                lblZodiacDate: "Zodiac Date Range:",
                lblSeasonBorn: "Astrological Season:",
                lblLifepath: "Life Path Number (Numerology):",
                lblBirthstone: "Astro Birthstone:",
                titleC1: "Islamic Hijri Calendar",
                typeC1: "Lunar",
                lblC1Date: "Hijri Birth Date:",
                lblC1Age: "Current Hijri Age:",
                titleC2: "Persian Solar Hijri (Jalali)",
                typeC2: "Solar Astro",
                lblC2Date: "Persian Birth Date:",
                lblC2Month: "Solar Sign (Ancient Persian):",
                titleC3: "Chinese Luni-Solar Calendar",
                typeC3: "Luni-Solar",
                lblC3Date: "Chinese Zodiac Year:",
                lblC3Element: "Accompanying Element:",
                titleC4: "Daylight Saving & Season",
                typeC4: "Local Time",
                lblC4Date: "Status on Birth Day:",
                lblC4Climate: "Seasonal Alignment:",
                titleC5: "Coptic & Ancient Egyptian Calendar",
                typeC5: "Sothic (Star)",
                lblC5Date: "Coptic Birth Date:",
                lblC5Month: "Historical Egyptian Month:",
                titleC6: "Syriac Calendar (Seleucid)",
                typeC6: "Ancient Solar",
                lblC6Date: "Syriac Birth Date:",
                lblC6Month: "Levantine Month Designation:",
                footerNotes: "Astro-mathematical algorithms and historical matrix conversion simplified with high fidelity.",
                footerCredit: "Programmed by Mohamed Majid Al-Furaiji",
                errorMsg: "Please enter a valid date of birth in the past."
            }
        };

        // UI Language Switcher Handler
        function toggleLanguage() {
            currentLang = currentLang === 'ar' ? 'en' : 'ar';
            const htmlRoot = document.getElementById('html-root');
            
            if (currentLang === 'en') {
                htmlRoot.setAttribute('dir', 'ltr');
                htmlRoot.setAttribute('lang', 'en');
                document.body.classList.add('font-en');
                document.getElementById('lang-btn-text').textContent = "العربية";
                document.getElementById('input-container').className = "w-full text-left";
                document.getElementById('error-msg').className = "text-red-400 text-xs mt-3 hidden text-left";
            } else {
                htmlRoot.setAttribute('dir', 'rtl');
                htmlRoot.setAttribute('lang', 'ar');
                document.body.classList.remove('font-en');
                document.getElementById('lang-btn-text').textContent = "English";
                document.getElementById('input-container').className = "w-full text-right";
                document.getElementById('error-msg').className = "text-red-400 text-xs mt-3 hidden text-right";
            }

            // Apply translation values
            const keys = translations[currentLang];
            document.getElementById('app-title').textContent = keys.appTitle;
            document.getElementById('app-subtitle').textContent = keys.appSubtitle;
            document.getElementById('current-date-lbl').textContent = keys.currentDateLbl;
            document.getElementById('hero-title').textContent = keys.heroTitle;
            document.getElementById('hero-desc').textContent = keys.heroDesc;
            document.getElementById('input-label').textContent = keys.inputLabel;
            document.getElementById('calc-btn').querySelector('span').textContent = keys.calcBtn;
            
            document.getElementById('gregorian-badge').textContent = keys.gregorianBadge;
            document.getElementById('gregorian-title').textContent = keys.gregorianTitle;
            document.getElementById('lbl-years').textContent = keys.lblYears;
            document.getElementById('lbl-months').textContent = keys.lblMonths;
            document.getElementById('lbl-days').textContent = keys.lblDays;
            
            document.getElementById('lbl-weekday').textContent = keys.lblWeekday;
            document.getElementById('lbl-tot-weeks').textContent = keys.lblTotWeeks;
            document.getElementById('lbl-tot-days').textContent = keys.lblTotDays;
            document.getElementById('lbl-tot-hours').textContent = keys.lblTotHours;
            document.getElementById('lbl-countdown-title').textContent = keys.lblCountdownTitle;
            
            document.getElementById('moon-badge').textContent = keys.moonBadge;
            document.getElementById('moon-title').textContent = keys.moonTitle;
            document.getElementById('lbl-moon-desc-title').innerHTML = `<i class="fa-solid fa-wand-magic-sparkles ml-1.5 mr-1.5"></i> ${keys.lblMoonDescTitle}`;
            
            document.getElementById('zodiac-badge').textContent = keys.zodiacBadge;
            document.getElementById('zodiac-card-title').textContent = keys.zodiacCardTitle;
            document.getElementById('lbl-your-zodiac').textContent = keys.lblYourZodiac;
            document.getElementById('lbl-zodiac-date').textContent = keys.lblZodiacDate;
            document.getElementById('lbl-season-born').textContent = keys.lblSeasonBorn;
            document.getElementById('lbl-lifepath').textContent = keys.lblLifepath;
            document.getElementById('lbl-birthstone').textContent = keys.lblBirthstone;
            
            document.getElementById('title-c1').querySelector('span').textContent = keys.titleC1;
            document.getElementById('type-c1').textContent = keys.typeC1;
            document.getElementById('lbl-c1-date').textContent = keys.lblC1Date;
            document.getElementById('lbl-c1-age').textContent = keys.lblC1Age;
            
            document.getElementById('title-c2').querySelector('span').textContent = keys.titleC2;
            document.getElementById('type-c2').textContent = keys.typeC2;
            document.getElementById('lbl-c2-date').textContent = keys.lblC2Date;
            document.getElementById('lbl-c2-month').textContent = keys.lblC2Month;
            
            document.getElementById('title-c3').querySelector('span').textContent = keys.titleC3;
            document.getElementById('type-c3').textContent = keys.typeC3;
            document.getElementById('lbl-c3-date').textContent = keys.lblC3Date;
            document.getElementById('lbl-c3-element').textContent = keys.lblC3Element;
            
            document.getElementById('title-c4').querySelector('span').textContent = keys.titleC4;
            document.getElementById('type-c4').textContent = keys.typeC4;
            document.getElementById('lbl-c4-date').textContent = keys.lblC4Date;
            document.getElementById('lbl-c4-climate').textContent = keys.lblC4Climate;
            
            document.getElementById('title-c5').querySelector('span').textContent = keys.titleC5;
            document.getElementById('type-c5').textContent = keys.typeC5;
            document.getElementById('lbl-c5-date').textContent = keys.lblC5Date;
            document.getElementById('lbl-c5-month').textContent = keys.lblC5Month;
            
            document.getElementById('title-c6').querySelector('span').textContent = keys.titleC6;
            document.getElementById('type-c6').textContent = keys.typeC6;
            document.getElementById('lbl-c6-date').textContent = keys.lblC6Date;
            document.getElementById('lbl-c6-month').textContent = keys.lblC6Month;
            
            document.getElementById('footer-notes').textContent = keys.footerNotes;
            document.getElementById('footer-credit').textContent = keys.footerCredit;

            // Re-render date display
            renderTodayDate();
            
            // If results container is already visible, recalculate to translate output data
            const resultsContainer = document.getElementById('results-container');
            if (!resultsContainer.classList.contains('hidden')) {
                calculateAll();
            }
        }

        function renderTodayDate() {
            const now = new Date();
            const langCode = currentLang === 'ar' ? 'ar-EG' : 'en-US';
            const options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
            document.getElementById('current-date-display').textContent = now.toLocaleDateString(langCode, options);
        }

        window.onload = function() {
            renderTodayDate();
        };

        // Master Calculations Starter
        function calculateAll() {
            const birthInput = document.getElementById('birth-date').value;
            const errorMsg = document.getElementById('error-msg');
            
            if (!birthInput) {
                errorMsg.classList.remove('hidden');
                return;
            }
            errorMsg.classList.add('hidden');

            const birthDate = new Date(birthInput);
            const today = new Date();

            if (birthDate > today) {
                errorMsg.textContent = translations[currentLang].errorMsg;
                errorMsg.classList.remove('hidden');
                return;
            }

            // Unveil results with fade effect
            const resultsContainer = document.getElementById('results-container');
            resultsContainer.classList.remove('hidden');
            resultsContainer.scrollIntoView({ behavior: 'smooth' });

            // Run individual system engines
            calculateGregorianAge(birthDate, today);
            calculateMoonPhase(birthDate);
            calculateHijri(birthDate);
            calculatePersianJalali(birthDate);
            calculateChineseZodiac(birthDate);
            calculateDSTandSeason(birthDate);
            calculateCopticDate(birthDate);
            calculateSyriacDate(birthDate);
            calculateHebrewDate(birthDate);
            calculateNumerologyAndStone(birthDate);
        }

        // 1. Gregorian Age Calculations & Progress Circular Ring
        function calculateGregorianAge(birthDate, today) {
            let years = today.getFullYear() - birthDate.getFullYear();
            let months = today.getMonth() - birthDate.getMonth();
            let days = today.getDate() - birthDate.getDate();

            if (days < 0) {
                months--;
                const prevMonth = new Date(today.getFullYear(), today.getMonth(), 0);
                days += prevMonth.getDate();
            }

            if (months < 0) {
                years--;
                months += 12;
            }

            document.getElementById('age-years').textContent = years;
            document.getElementById('age-months').textContent = months;
            document.getElementById('age-days').textContent = days;

            // Day of the week translation
            const arDays = ["الأحد", "الإثنين", "الثلاثاء", "الأربعاء", "الخميس", "الجمعة", "السبت"];
            const enDays = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
            document.getElementById('val-weekday').textContent = currentLang === 'ar' ? arDays[birthDate.getDay()] : enDays[birthDate.getDay()];

            // Large time statistics
            const diffTime = Math.abs(today - birthDate);
            const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24));
            const diffWeeks = Math.floor(diffDays / 7);
            
            document.getElementById('val-tot-weeks').textContent = diffWeeks.toLocaleString(currentLang === 'ar' ? 'ar-EG' : 'en-US');
            document.getElementById('val-tot-days').textContent = diffDays.toLocaleString(currentLang === 'ar' ? 'ar-EG' : 'en-US');
            document.getElementById('val-tot-hours').textContent = (diffDays * 24).toLocaleString(currentLang === 'ar' ? 'ar-EG' : 'en-US');

            // Birthday countdown and Progress calculation
            let nextBirthday = new Date(today.getFullYear(), birthDate.getMonth(), birthDate.getDate());
            if (today > nextBirthday) {
                nextBirthday.setFullYear(today.getFullYear() + 1);
            }
            const timeToNext = nextBirthday - today;
            const daysToNext = Math.ceil(timeToNext / (1000 * 60 * 60 * 24));

            // Percentage of the year elapsed toward next birthday
            const pctElapsed = Math.round(((365 - daysToNext) / 365) * 100);
            setProgress(pctElapsed);

            if (daysToNext === 365 || daysToNext === 0) {
                document.getElementById('val-countdown-txt').textContent = currentLang === 'ar' ? "عيد ميلاد مجيد وسعيد! إنه اليوم!" : "Happy Birthday! It's today!";
                document.getElementById('val-countdown-days').textContent = "🎉";
            } else {
                document.getElementById('val-countdown-txt').textContent = currentLang === 'ar' ? "المتبقي لإتمام السنة التالية بنجاح." : "Days remaining until your celebration.";
                document.getElementById('val-countdown-days').textContent = (currentLang === 'ar' ? `${daysToNext} يوم` : `${daysToNext} Days`);
            }
        }

        // Circular progress ring formula helper
        function setProgress(percent) {
            const circle = document.getElementById('progress-circle');
            const radius = circle.r.baseVal.value;
            const circumference = radius * 2 * Math.PI;
            circle.style.strokeDasharray = `${circumference} ${circumference}`;
            const offset = circumference - (percent / 100) * circumference;
            circle.style.strokeDashoffset = offset;
            document.getElementById('progress-percent').textContent = `${percent}%`;
        }

        // 2. Moon Phase Calculations with comprehensive dual-language details
        function calculateMoonPhase(date) {
            const year = date.getFullYear();
            const month = date.getMonth() + 1;
            const day = date.getDate();

            let m = month;
            let y = year;
            if (m < 3) {
                y--;
                m += 12;
            }
            let jd = Math.floor(365.25 * y) + Math.floor(30.6 * (m + 1)) + day - 730560.5;
            
            const totalCycles = jd / 29.530588853;
            const cycleFraction = totalCycles - Math.floor(totalCycles);
            let age = cycleFraction * 29.530588853;
            const phaseAngle = cycleFraction * 2 * Math.PI;
            const illuminationPercent = Math.round((1 - Math.cos(phaseAngle)) / 2 * 100);

            let phaseName = "";
            let desc = "";
            
            const shadow = document.getElementById('moon-shadow-elem');
            const light = document.getElementById('moon-light-elem');
            shadow.style.borderRadius = "50%";
            light.style.borderRadius = "50%";

            const moonTranslations = {
                ar: {
                    new: ["محاق تام (New Moon)", "ولدت في ليلة غاب فيها ضوء القمر تماماً لتسود السكينة والهدوء الفلكي. يعطيك هذا الطور شخصية هادئة وحالمة ذات حدس وبدايات قوية ومستقلة."],
                    cres1: ["هلال متزايد (Waxing Crescent)", "خيط فضي خفيف أنار سماء ليلة ولادتك. يعكس هذا الطور روحاً مبدعة ومحبة للاستكشاف والتعلم المستمر، وامتلاك طاقة حيوية دؤوبة."],
                    q1: ["تربيع أول (First Quarter)", "نصف القمر تماماً كان مضيئاً ليلة ولادتك. تمنحك هذه المرحلة شخصية متوازنة، حازمة، قادرة على مجابهة الصعوبات واتخاذ القرارات المفصلية بثبات."],
                    gib1: ["أحدب متزايد (Waxing Gibbous)", "قمر ليلتك كان مكتملاً بشكل شبه كلي. يعزز هذا الطور الرغبة الكبيرة في إصلاح وتحسين الذات، والتحلي برؤية تفصيلية وملاحظة عميقة في العمل والمحيط."],
                    full: ["بدر مكتمل (Full Moon)", "قمر ليلتك كان في قمة سطوعه وجماله الفلكي. يمنحك البدر حضوراً لافتاً، ومغناطيسية جاذبة، وقدرة تواصلية ومشاعر تعبيرية غنية وواضحة."],
                    gib2: ["أحدب متناقص (Waning Gibbous)", "بدأ ضوء البدر بالاختفاء تدريجياً. يعكس هذا الطور رغبتك الفطرية في نشر الحكمة، ومشاركة النصيحة الصادقة، وتعليم الآخرين مما تكتسبه في حياتك."],
                    q2: ["تربيع ثانٍ (Third Quarter)", "النصف الآخر من القمر مضيئاً. يتميز أصحاب هذا الطور بالقدرة العالية على التحرر من قيود الماضي، وإدارة الأزمات الصعبة بطرق منطقية وعقلانية تماماً."],
                    cres2: ["هلال متناقص (Waning Crescent)", "تلاشي الضوء للاقتراب من ولادة جديدة. يتمتع أصحاب هذا الطور بالعمق الفكري، الميل نحو التأمل، الفلسفة، وحماية سلامتهم النفسية بذكاء."]
                },
                en: {
                    new: ["New Moon", "You were born under a completely dark, peaceful night. This cycle fosters deep intuition, independent drive, and a powerful sense of fresh beginnings."],
                    cres1: ["Waxing Crescent", "A silver sliver illuminated your birth night. You possess a curious spirit, passionate imagination, and robust creative energy."],
                    q1: ["First Quarter", "Exactly half illuminated. This bestows a highly balanced, firm personality, easily overcoming hardships and maintaining stellar focus."],
                    gib1: ["Waxing Gibbous", "Almost fully complete. You have an organic urge for self-refinement, superb attention to detail, and analytical prowess."],
                    full: ["Full Moon", "Born under the radiant cosmic spotlight. The Full Moon grants magnetic charm, vivid communication skills, and intense emotional warmth."],
                    gib2: ["Waning Gibbous", "The light begins its slow retreat. This gives you a natural drive to share knowledge, act as a mentor, and guide others wisely."],
                    q2: ["Third Quarter", "The left half lit. You possess exceptional ability to release the past, process difficult issues logically, and chart independent paths."],
                    cres2: ["Waning Crescent", "A waning crescent. You are characterized by reflective wisdom, philosophical calmness, and a deep spiritual baseline."]
                }
            };

            const t = moonTranslations[currentLang];

            if (age < 1.84) {
                phaseName = t.new[0]; desc = t.new[1];
                light.style.width = "0%"; shadow.style.width = "100%"; shadow.style.left = "0%";
            } else if (age < 5.53) {
                phaseName = t.cres1[0]; desc = t.cres1[1];
                light.style.width = "100%"; shadow.style.width = "75%"; shadow.style.left = "0%";
                shadow.style.borderRadius = currentLang === 'ar' ? "50% 0 0 50% / 50% 0 0 50%" : "0 50% 50% 0 / 0 50% 50% 0";
            } else if (age < 9.22) {
                phaseName = t.q1[0]; desc = t.q1[1];
                light.style.width = "100%"; shadow.style.width = "50%"; shadow.style.left = "0%";
            } else if (age < 12.91) {
                phaseName = t.gib1[0]; desc = t.gib1[1];
                light.style.width = "100%"; shadow.style.width = "25%"; shadow.style.left = "0%";
            } else if (age < 16.61) {
                phaseName = t.full[0]; desc = t.full[1];
                light.style.width = "100%"; shadow.style.width = "0%";
            } else if (age < 20.3) {
                phaseName = t.gib2[0]; desc = t.gib2[1];
                light.style.width = "100%"; shadow.style.width = "25%"; shadow.style.left = "75%";
            } else if (age < 23.99) {
                phaseName = t.q2[0]; desc = t.q2[1];
                light.style.width = "100%"; shadow.style.width = "50%"; shadow.style.left = "50%";
            } else if (age < 27.68) {
                phaseName = t.cres2[0]; desc = t.cres2[1];
                light.style.width = "100%"; shadow.style.width = "75%"; shadow.style.left = "25%";
                shadow.style.borderRadius = currentLang === 'ar' ? "0 50% 50% 0 / 0 50% 50% 0" : "50% 0 0 50% / 50% 0 0 50%";
            } else {
                phaseName = t.new[0]; desc = t.new[1];
                light.style.width = "0%"; shadow.style.width = "100%"; shadow.style.left = "0%";
            }

            document.getElementById('val-moon-name').textContent = phaseName;
            document.getElementById('val-moon-ill').textContent = currentLang === 'ar' ? `توهج سطح القمر: ${illuminationPercent}%` : `Lunar Illumination: ${illuminationPercent}%`;
            document.getElementById('val-moon-desc').textContent = desc;
        }

        // 3. Hijri Calendar Conversion Logic
        function calculateHijri(date) {
            let jd;
            const year = date.getFullYear();
            const month = date.getMonth() + 1;
            const day = date.getDate();

            if ((year > 1582) || ((year === 1582) && (month > 10)) || ((year === 1582) && (month === 10) && (day >= 15))) {
                jd = Math.floor(365.25 * (year + 4716)) + Math.floor(30.6001 * (month + 1)) + day + 2 - Math.floor(year / 100) + Math.floor(Math.floor(year / 100) / 4) - 1524.5;
            } else {
                jd = Math.floor(365.25 * (year + 4716)) + Math.floor(30.6001 * (month + 1)) + day - 1524.5;
            }

            let b = 0;
            if (jd > 2299160) {
                let a = Math.floor((jd - 1867216.25) / 36524.25);
                b = jd + 1 + a - Math.floor(a / 4);
            } else {
                b = jd;
            }

            let c = b + 1524;
            let d = Math.floor((c - 122.1) / 365.25);
            let e = Math.floor(365.25 * d);
            let g = Math.floor((c - e) / 30.6001);

            let jd_hijri = jd - 1948440 + 10632;
            let n = Math.floor((jd_hijri - 1) / 10631);
            jd_hijri = jd_hijri - 10631 * n + 354;
            let j = (Math.floor((10985 - jd_hijri) / 5316)) * (Math.floor((50 * jd_hijri) / 17719)) + (Math.floor(jd_hijri / 5670)) * (Math.floor((43 * jd_hijri) / 15238));
            jd_hijri = jd_hijri - (Math.floor((30 - j) / 15)) * (Math.floor((17719 * j) / 50)) - (Math.floor(j / 16)) * (Math.floor((15238 * j) / 43)) + 29;
            
            let hMonth = Math.floor((24 * jd_hijri) / 709);
            let hDay = jd_hijri - Math.floor((709 * hMonth) / 24);
            let hYear = 30 * n + j - 30;

            const hijriMonthsAr = [
                "محرّم", "صفر", "ربيع الأول", "ربيع الآخر", "جمادى الأولى", "جمادى الآخرة",
                "رجب", "شعبان", "رمضان", "شوال", "ذو القعدة", "ذو الحجة"
            ];
            const hijriMonthsEn = [
                "Muharram", "Safar", "Rabi' al-Awwal", "Rabi' al-Thani", "Jumada al-Awwal", "Jumada al-Thani",
                "Rajab", "Sha'ban", "Ramadan", "Shawwal", "Dhu al-Qi'dah", "Dhu al-Hijjah"
            ];

            const activeMList = currentLang === 'ar' ? hijriMonthsAr : hijriMonthsEn;
            const hSuff = currentLang === 'ar' ? "هـ" : "AH";

            document.getElementById('val-hijri-date').textContent = `${hDay} ${activeMList[hMonth - 1]} ${hYear} ${hSuff}`;

            // Age evaluation
            const today = new Date();
            const diffTime = Math.abs(today - date);
            const diffDays = diffTime / (1000 * 60 * 60 * 24);
            const hijriAgeTotal = diffDays / 354.367;
            const hAgeY = Math.floor(hijriAgeTotal);
            const hAgeM = Math.floor((hijriAgeTotal - hAgeY) * 12);
            
            document.getElementById('val-hijri-age').textContent = currentLang === 'ar' 
                ? `${hAgeY} سنة و ${hAgeM} أشهر` 
                : `${hAgeY} Years & ${hAgeM} Months`;
        }

        // 4. Persian (Solar Hijri / Jalali) Calendar Conversion
        function calculatePersianJalali(date) {
            const gy = date.getFullYear();
            const gm = date.getMonth() + 1;
            const gd = date.getDate();

            // Jalali Conversion Algorithm
            const g_d_m = [0, 31, 59, 90, 120, 151, 181, 212, 243, 273, 304, 335];
            let jy = (gy <= 1600) ? 0 : 979;
            let gy_temp = gy - ((gy <= 1600) ? 621 : 1600);
            const gy2 = (gm > 2) ? (gy_temp + 1) : gy_temp;
            let days = (365 * gy_temp) + Math.floor((gy2 + 3) / 4) - Math.floor((gy2 + 99) / 100) + Math.floor((gy2 + 399) / 400) - 80 + gd + g_d_m[gm - 1];
            jy += 33 * Math.floor(days / 12053);
            days %= 12053;
            jy += 4 * Math.floor(days / 1461);
            days %= 1461;
            jy += Math.floor((days - 1) / 365);
            if (days > 365) days = (days - 1) % 365;
            let jm = (days < 186) ? 1 + Math.floor(days / 31) : 7 + Math.floor((days - 186) / 30);
            let jd = 1 + ((days < 186) ? (days % 31) : ((days - 186) % 30));

            const persianMonthsAr = [
                "فروردين", "أرديبهشت", "خرداد", "تير", "مرداد", "شهريور",
                "مهر", "آبان", "آذر", "دي", "بهمن", "إسفند"
            ];
            const persianMonthsEn = [
                "Farvardin", "Ordibehesht", "Khordad", "Tir", "Mordad", "Shahrivar",
                "Mehr", "Aban", "Azar", "Dey", "Bahman", "Esfand"
            ];

            const persianSignsAr = ["برج الحمل (Aries)", "برج الثور (Taurus)", "برج الجوزاء (Gemini)", "برج السرطان (Cancer)", "برج الأسد (Leo)", "برج العذراء (Virgo)", "برج الميزان (Libra)", "برج العقرب (Scorpio)", "برج القوس (Sagittarius)", "برج الجدي (Capricorn)", "برج الدلو (Aquarius)", "برج الحوت (Pisces)"];
            const persianSignsEn = ["Aries Mansion", "Taurus Mansion", "Gemini Mansion", "Cancer Mansion", "Leo Mansion", "Virgo Mansion", "Libra Mansion", "Scorpio Mansion", "Sagittarius Mansion", "Capricorn Mansion", "Aquarius Mansion", "Pisces Mansion"];

            const mList = currentLang === 'ar' ? persianMonthsAr : persianMonthsEn;
            const signList = currentLang === 'ar' ? persianSignsAr : persianSignsEn;
            const suffix = currentLang === 'ar' ? "هـ.ش" : "SH";

            document.getElementById('val-persian-date').textContent = `${jd} ${mList[jm - 1]} ${jy} ${suffix}`;
            document.getElementById('val-persian-month').textContent = signList[jm - 1];
        }

        // 5. Chinese Zodiac and Element System
        function calculateChineseZodiac(date) {
            const year = date.getFullYear();
            
            const zodiacsAr = ["الفأر (Rat) 🐀", "الثور (Ox) 🐂", "النمر (Tiger) 🐅", "الأرنب (Rabbit) 🐇", "التنين (Dragon) 🐉", "الأفعى (Snake) 🐍", "الحصان (Horse) 🐎", "الماعز (Goat) 🐐", "القرد (Monkey) 🐒", "الديك (Rooster) 🐓", "الكلب (Dog) 🐕", "الخنزير (Pig) 🐖"];
            const zodiacsEn = ["Rat 🐀", "Ox 🐂", "Tiger 🐅", "Rabbit 🐇", "Dragon 🐉", "Snake 🐍", "Horse 🐎", "Goat 🐐", "Monkey 🐒", "Rooster 🐓", "Dog 🐕", "Pig 🐖"];
            
            let zodiacIndex = (year - 1900) % 12;
            if (zodiacIndex < 0) zodiacIndex += 12;

            const elementsAr = ["معدن (Metal) 🪙", "معدن (Metal) 🪙", "ماء (Water) 💧", "ماء (Water) 💧", "خشب (Wood) 🪵", "خشب (Wood) 🪵", "نار (Fire) 🔥", "نار (Fire) 🔥", "أرض وتربة (Earth) ⛰️", "أرض وتربة (Earth) ⛰️"];
            const elementsEn = ["Metal 🪙", "Metal 🪙", "Water 💧", "Water 💧", "Wood 🪵", "Wood 🪵", "Fire 🔥", "Fire 🔥", "Earth ⛰️", "Earth ⛰️"];
            
            const lastDigit = year % 10;
            const element = currentLang === 'ar' ? elementsAr[lastDigit] : elementsEn[lastDigit];

            document.getElementById('val-chinese-zodiac').textContent = currentLang === 'ar' ? zodiacsAr[zodiacIndex] : zodiacsEn[zodiacIndex];
            document.getElementById('val-chinese-element').textContent = element;
        }

        // 6. Western Astrological Zodiac, Season & Color Theme Changes
        function calculateDSTandSeason(date) {
            const getStdTimezoneOffset = function(d) {
                const jan = new Date(d.getFullYear(), 0, 1);
                const jul = new Date(d.getFullYear(), 6, 1);
                return Math.max(jan.getTimezoneOffset(), jul.getTimezoneOffset());
            };

            const isDstObserved = function(d) {
                return d.getTimezoneOffset() < getStdTimezoneOffset(d);
            };

            const isDst = isDstObserved(date);
            
            if (currentLang === 'ar') {
                document.getElementById('val-dst-status').textContent = isDst ? "توقيت صيفي نشط (+1 ساعة)" : "توقيت شتوي قياسي (دائم)";
            } else {
                document.getElementById('val-dst-status').textContent = isDst ? "Daylight Saving Time Active (+1h)" : "Standard Standard Time (Standard)";
            }

            const month = date.getMonth() + 1;
            const day = date.getDate();
            
            let seasonAr = "";
            let seasonEn = "";
            let seasonClass = ""; // For dynamical coloring of the season card
            let seasonBorder = "";

            if ((month === 12 && day >= 21) || month === 1 || month === 2 || (month === 3 && day < 20)) {
                seasonAr = "الشتاء القارس ❄️";
                seasonEn = "Crisp Winter ❄️";
                seasonClass = "from-cyan-900/40 to-slate-900/40";
                seasonBorder = "border-cyan-500/20";
            } else if ((month === 3 && day >= 20) || month === 4 || month === 5 || (month === 6 && day < 21)) {
                seasonAr = "الربيع المعتدل 🌸";
                seasonEn = "Fresh Spring 🌸";
                seasonClass = "from-emerald-900/40 to-slate-900/40";
                seasonBorder = "border-emerald-500/20";
            } else if ((month === 6 && day >= 21) || month === 7 || month === 8 || (month === 9 && day < 22)) {
                seasonAr = "الصيف المشمس ☀️";
                seasonEn = "Radiant Summer ☀️";
                seasonClass = "from-amber-900/40 to-slate-900/40";
                seasonBorder = "border-amber-500/20";
            } else {
                seasonAr = "الخريف الهادئ 🍂";
                seasonEn = "Serene Autumn 🍂";
                seasonClass = "from-orange-900/40 to-slate-900/40";
                seasonBorder = "border-orange-500/20";
            }

            document.getElementById('val-season-born').textContent = currentLang === 'ar' ? seasonAr : seasonEn;
            document.getElementById('val-season-details').textContent = currentLang === 'ar' ? "نظام التوزيع الشمسي الحركي" : "Solar distribution system alignment";
            
            // Dynamic card styling injection
            const scard = document.getElementById('season-themed-card');
            scard.className = `glass-panel p-6 sm:p-8 rounded-3xl shadow-xl flex flex-col justify-between bg-gradient-to-br ${seasonClass} ${seasonBorder}`;
        }

        // 7. Coptic Calendar Conversion (Star of Sothis alignment)
        function calculateCopticDate(date) {
            const jd = (date.getTime() / 86400000) + 2440587.5;
            const copticEpoch = 1724220.5; 
            const daysSinceEpoch = Math.floor(jd - copticEpoch);
            
            const copYear = Math.floor(daysSinceEpoch / 365.25);
            const dayInYear = Math.floor(daysSinceEpoch % 365.25);
            
            const copMonth = Math.floor(dayInYear / 30) + 1;
            const copDay = (dayInYear % 30) + 1;

            const copticMonthsAr = [
                "توت", "بابه", "هاتور", "كيهك", "طوبة", "أمشير",
                "برمهات", "برمودة", "بشنس", "بؤونة", "أبيب", "مسرى", "النسيء"
            ];
            const copticMonthsEn = [
                "Thout", "Babah", "Hator", "Kiahk", "Toba", "Amshir",
                "Baramhat", "Baramouda", "Bashans", "Paona", "Epip", "Mesori", "Nasie"
            ];

            const mList = currentLang === 'ar' ? copticMonthsAr : copticMonthsEn;
            const suffix = currentLang === 'ar' ? "للشهداء" : "A.M.";

            const monthIndex = Math.min(copMonth - 1, 12);
            document.getElementById('val-coptic-date').textContent = `${copDay} ${mList[monthIndex]} ${copYear} ${suffix}`;
            document.getElementById('val-coptic-month').textContent = mList[monthIndex];
        }

        // 8. Syriac Calendar conversion
        function calculateSyriacDate(date) {
            const day = date.getDate();
            const month = date.getMonth(); 
            const year = date.getFullYear();

            const syriacMonthsAr = [
                "كانون الثاني", "شباط", "آذار", "نيسان", "أيار", "حزيران",
                "تموز", "آب", "أيلول", "تشرين الأول", "تشرين الثاني", "كانون الأول"
            ];
            const syriacMonthsEn = [
                "Kanun al-Thani", "Shubat", "Adar", "Nisan", "Ayyar", "Haziran",
                "Tammuz", "Ab", "Aylul", "Tishrin al-Awwal", "Tishrin al-Thani", "Kanun al-Awwal"
            ];

            const mList = currentLang === 'ar' ? syriacMonthsAr : syriacMonthsEn;
            const suffix = currentLang === 'ar' ? "م.س" : "Syr";

            document.getElementById('val-syriac-date').textContent = `${day} ${mList[month]} ${year} ${suffix}`;
            document.getElementById('val-syriac-month').textContent = mList[month];
        }

        // 9. Hebrew Calendar Calculation
        function calculateHebrewDate(date) {
            const gYear = date.getFullYear();
            let hYear = gYear + 3760;
            
            const hebrewMonthsAr = [
                "تشريه", "حشفان", "كسلو", "تيفيت", "شيفات", "أدار",
                "نيسان", "أيار", "سيفان", "تموز", "آب", "أيلول"
            ];
            const hebrewMonthsEn = [
                "Tishrei", "Cheshvan", "Kislev", "Tevet", "Shevat", "Adar",
                "Nisan", "Iyar", "Sivan", "Tammuz", "Av", "Elul"
            ];

            const month = date.getMonth();
            const approxHebrewMonth = (month + 6) % 12;
            const mList = currentLang === 'ar' ? hebrewMonthsAr : hebrewMonthsEn;
            const suffix = currentLang === 'ar' ? "هـ.ع" : "AM";

            document.getElementById('val-hebrew-date').textContent = `${date.getDate()} ${mList[approxHebrewMonth]} ${hYear}`;
            document.getElementById('val-hebrew-year').textContent = `${hYear} ${suffix}`;
        }

        // 10. Western Zodiac, Life Path Numerology, and Birthstone Engines
        function calculateNumerologyAndStone(date) {
            const day = date.getDate();
            const month = date.getMonth() + 1;
            const year = date.getFullYear();

            // Western Zodiac Sign Detection
            const zodiacs = [
                { nameAr: "الجدي (Capricorn)", nameEn: "Capricorn ♑", start: [12, 22], end: [1, 19], icon: "fa-solid fa-mountain", color: "text-slate-400", rangeAr: "22 ديسمبر - 19 يناير", rangeEn: "Dec 22 - Jan 19" },
                { nameAr: "الدلو (Aquarius)", nameEn: "Aquarius ♒", start: [1, 20], end: [2, 18], icon: "fa-solid fa-water", color: "text-sky-400", rangeAr: "20 يناير - 18 فبراير", rangeEn: "Jan 20 - Feb 18" },
                { nameAr: "الحوت (Pisces)", nameEn: "Pisces ♓", start: [2, 19], end: [3, 20], icon: "fa-solid fa-fish", color: "text-cyan-400", rangeAr: "19 فبراير - 20 مارس", rangeEn: "Feb 19 - Mar 20" },
                { nameAr: "الحمل (Aries)", nameEn: "Aries ♈", start: [3, 21], end: [4, 19], icon: "fa-solid fa-fire", color: "text-red-400", rangeAr: "21 مارس - 19 أبريل", rangeEn: "Mar 21 - Apr 19" },
                { nameAr: "الثور (Taurus)", nameEn: "Taurus ♉", start: [4, 20], end: [5, 20], icon: "fa-solid fa-gem", color: "text-emerald-400", rangeAr: "20 أبريل - 20 مايو", rangeEn: "Apr 20 - May 20" },
                { nameAr: "الجوزاء (Gemini)", nameEn: "Gemini ♊", start: [5, 21], end: [6, 20], icon: "fa-solid fa-people-half-by-half", color: "text-amber-400", rangeAr: "21 مايو - 20 يونيو", rangeEn: "May 21 - Jun 20" },
                { nameAr: "السرطان (Cancer)", nameEn: "Cancer ♋", start: [6, 21], end: [7, 22], icon: "fa-solid fa-shrimp", color: "text-blue-400", rangeAr: "21 يونيو - 22 يوليو", rangeEn: "Jun 21 - Jul 22" },
                { nameAr: "الأسد (Leo)", nameEn: "Leo ♌", start: [7, 23], end: [8, 22], icon: "fa-solid fa-crown", color: "text-orange-400", rangeAr: "23 يوليو - 22 أغسطس", rangeEn: "Jul 23 - Aug 22" },
                { nameAr: "العذراء (Virgo)", nameEn: "Virgo ♍", start: [8, 23], end: [9, 22], icon: "fa-solid fa-feather", color: "text-teal-400", rangeAr: "23 أغسطس - 22 سبتمبر", rangeEn: "Aug 23 - Sep 22" },
                { nameAr: "الميزان (Libra)", nameEn: "Libra ♎", start: [9, 23], end: [10, 22], icon: "fa-solid fa-scale-balanced", color: "text-pink-400", rangeAr: "23 سبتمبر - 22 أكتوبر", rangeEn: "Sep 23 - Oct 22" },
                { nameAr: "العقرب (Scorpio)", nameEn: "Scorpio ♏", start: [10, 23], end: [11, 21], icon: "fa-solid fa-skull-crossbones", color: "text-purple-400", rangeAr: "23 أكتوبر - 21 نوفمبر", rangeEn: "Oct 23 - Nov 21" },
                { nameAr: "القوس (Sagittarius)", nameEn: "Sagittarius ♐", start: [11, 22], end: [12, 21], icon: "fa-solid fa-location-arrow", color: "text-indigo-400", rangeAr: "22 نوفمبر - 21 ديسمبر", rangeEn: "Nov 22 - Dec 21" }
            ];

            let activeZodiac = zodiacs[0];
            for (let i = 0; i < zodiacs.length; i++) {
                const z = zodiacs[i];
                const startM = z.start[0];
                const startD = z.start[1];
                const endM = z.end[0];
                const endD = z.end[1];

                if ((month === startM && day >= startD) || (month === endM && day <= endD)) {
                    activeZodiac = z;
                    break;
                }
            }

            document.getElementById('val-zodiac-name').textContent = currentLang === 'ar' ? activeZodiac.nameAr : activeZodiac.nameEn;
            document.getElementById('val-zodiac-range').textContent = currentLang === 'ar' ? activeZodiac.rangeAr : activeZodiac.rangeEn;
            
            // Render Zodiac Icon classes safely
            const iconElem = document.getElementById('val-zodiac-icon');
            iconElem.className = `${activeZodiac.icon} ${activeZodiac.color} text-3xl`;

            // Numerology Lifepath Engine (Summing digits recursively until < 10, or masters 11, 22, 33)
            let digitsStr = day.toString() + month.toString() + year.toString();
            let sum = 0;
            for (let char of digitsStr) {
                sum += parseInt(char);
            }
            while (sum > 9 && sum !== 11 && sum !== 22 && sum !== 33) {
                let tempSum = 0;
                for (let char of sum.toString()) {
                    tempSum += parseInt(char);
                }
                sum = tempSum;
            }
            document.getElementById('val-lifepath').textContent = sum;

            // Birthstone Index By Month
            const stonesAr = [
                "العقيق الأحمر (Garnet)", "الجمشت (Amethyst)", "الأكوامارين (Aquamarine)", 
                "الألماس (Diamond)", "الزمرد (Emerald)", "اللؤلؤ (Pearl)", 
                "الياقوت الأحمر (Ruby)", "الزبرجد (Peridot)", "النيلي/الياقوت الأزرق (Sapphire)", 
                "الأوبال الفاخر (Opal)", "التوباز الأصفر (Topaz)", "الفيروز العريق (Turquoise)"
            ];
            const stonesEn = [
                "Garnet", "Amethyst", "Aquamarine", 
                "Diamond", "Emerald", "Pearl", 
                "Ruby", "Peridot", "Sapphire", 
                "Opal", "Topaz", "Turquoise"
            ];
            document.getElementById('val-birthstone').textContent = currentLang === 'ar' ? stonesAr[month - 1] : stonesEn[month - 1];
        }
    </script>
</body>
</html>


