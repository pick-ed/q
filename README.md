<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PICK: Грант в Корею. Программа подготовки к поступлению</title>
    <!-- Load Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@100..900&display=swap" rel="stylesheet">
    
    <!-- Load Firebase SDKs for future persistence if needed, as per instructions -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInAnonymously, signInWithCustomToken } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, setLogLevel } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        // Global variables provided by the Canvas environment
        const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';
        const firebaseConfig = typeof __firebase_config !== 'undefined' ? JSON.parse(__firebase_config) : null;
        const initialAuthToken = typeof __initial_auth_token !== 'undefined' ? __initial_auth_token : null;

        let app, db, auth;

        if (firebaseConfig) {
            setLogLevel('Debug');
            app = initializeApp(firebaseConfig);
            db = getFirestore(app);
            auth = getAuth(app);

            // Authentication logic
            (async () => {
                try {
                    if (initialAuthToken) {
                        await signInWithCustomToken(auth, initialAuthToken);
                        // console.log("Firebase signed in with custom token.");
                    } else {
                        await signInAnonymously(auth);
                        // console.log("Firebase signed in anonymously.");
                    }
                } catch (error) {
                    console.error("Firebase Auth Error:", error);
                }
            })();
        } else {
            console.warn("Firebase config not available. Running in static mode.");
        }
    </script>

    <style>
        /* Custom CSS to match the deep black/blue block style */
        body {
            font-family: 'Inter', sans-serif;
            background-color: #101010; /* Very deep dark background, nearly black */
            color: #ffffff; /* Bright white text for maximum contrast */
        }
        .hero-bg {
            background-color: #1e293b; /* Dark Slate/Navy for the Hero area */
            border-bottom: 4px solid #3b82f6; /* Blue dividing line */
        }
        .cta-button {
            transition: background-color 0.2s, box-shadow 0.2s;
            background-color: #3b82f6; /* Vibrant Blue accent */
            color: #ffffff;
            font-weight: 700;
            border: 2px solid #3b82f6;
        }
        .cta-button:hover {
            background-color: #2563eb;
            box-shadow: 0 4px 15px rgba(59, 130, 246, 0.5); 
        }
        .secondary-cta {
             background-color: #ffffff;
             color: #101010;
        }
        .secondary-cta:hover {
             background-color: #e2e8f0;
        }
        .section-heading {
            border-bottom: 4px solid #3b82f6; /* Blue underline */
            padding-bottom: 8px;
            display: inline-block;
            color: #ffffff;
        }
        .process-card {
            background-color: #1f2937; /* Darker card background (Slate-800) */
            border-radius: 8px; /* Slightly less rounded corners for block style */
            box-shadow: 0 6px 12px rgba(0, 0, 0, 0.5);
            transition: border 0.3s;
            border-left: 4px solid transparent;
        }
        .process-card:hover {
            border-left: 4px solid #3b82f6; /* Blue border hover effect */
        }
        .step-number {
            color: #3b82f6; /* Vibrant Blue number */
        }
        .input-style {
            background-color: #1f2937;
            color: #ffffff;
            border: 1px solid #374151;
            padding: 1rem;
            border-radius: 0.5rem;
            width: 100%;
        }
        .result-card {
            background-color: #101010;
            border: 1px solid #374151;
            padding: 1.5rem;
            border-radius: 0.75rem;
        }
        /* Spinner for loading state */
        .spinner {
            border: 4px solid rgba(255, 255, 255, 0.3);
            border-top: 4px solid #ffffff;
            border-radius: 50%;
            width: 24px;
            height: 24px;
            animation: spin 1s linear infinite;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
    </style>
</head>
<body>

    <!-- Navigation Bar (Dark) -->
    <header class="p-4 bg-gray-900 shadow-xl sticky top-0 z-20">
        <div class="max-w-7xl mx-auto flex justify-between items-center">
            <!-- LOGO: Using 6.png (The white logo on a dark background) -->
            <a href="#">
                <img src="6.png" alt="PICK EdTech Logo" class="h-8 md:h-10" onerror="this.onerror=null;this.src='https://placehold.co/100x40/101010/ffffff?text=PICK+LOGO';">
            </a>
            
            <nav class="space-x-6 hidden sm:block font-medium">
                <a href="#process" class="text-white hover:text-blue-400 transition">Процесс</a>
                <a href="#ai-coordinator" class="text-white hover:text-blue-400 transition">AI-Координатор 🎯</a>
                <a href="#prize" class="text-white hover:text-blue-400 transition">Авиабилеты ✈️</a>
            </nav>
            <!-- CTA Button in Nav now links directly to Google Form -->
            <a href="https://docs.google.com/forms/d/e/1FAIpQLSfVxNrfayVQuPa5MRNCPeyZI9GVcbfDg0KitNgAwAT3CkEiCw/viewform?usp=dialog" target="_blank" 
               class="px-5 py-2 cta-button text-sm rounded-lg shadow-md hidden sm:block flex items-center justify-center">
                Записаться
            </a>
            <button class="sm:hidden text-2xl text-white">☰</button>
        </div>
    </header>

    <!-- 1. Hero Section (Deep Blue Block) -->
    <section class="hero-bg text-white pb-16 md:pb-24">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-center pt-24 md:pt-32 hero-text-container">
            <p class="text-lg font-light mb-2 text-blue-400 uppercase tracking-widest">PICK EDUCATION</p>
            <h1 class="text-4xl sm:text-6xl font-extrabold mb-6 tracking-tight">
                <strong>Стипендия</strong> в Корею: Легче, чем кажется.
            </h1>
            <p class="text-xl sm:text-2xl font-light mb-10 max-w-4xl mx-auto opacity-90">
                Твой путь к <strong>100% гранту</strong>. Не просто консультации, а полноценная 2-х годовая программа с индивидуальным подходом.
            </p>
            <!-- Main Call-to-Action Buttons (UPDATED: Primary CTA now links directly to Google Form) -->
            <div class="space-y-4 sm:space-y-0 sm:space-x-6">
                <a href="https://docs.google.com/forms/d/e/1FAIpQLSfVxNrfayVQuPa5MRNCPeyZI9GVcbfDg0KitNgAwAT3CkEiCw/viewform?usp=dialog" target="_blank" 
                   class="cta-button inline-block px-10 py-3 text-lg font-bold rounded-lg shadow-lg uppercase tracking-wider flex items-center justify-center">
                    Сделать первый шаг
                </a>
                <a href="#process" class="secondary-cta inline-block px-10 py-3 text-lg font-bold rounded-lg shadow-lg uppercase tracking-wider text-black">
                    Узнать подробнее
                </a>
            </div>
            <div class="mt-8 text-sm font-medium opacity-80">
                Уже <strong>50+ студентов</strong> достигли своих целей вместе с PICK.
            </div>
        </div>
    </section>

    <!-- 2. The 4-Step Process Section (Главный Процесс - Block Style) -->
    <section id="process" class="py-16 md:py-24 bg-black">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
            <h2 class="text-3xl md:text-4xl font-bold mb-12 section-heading mx-auto">
                Основа Программы PICK
            </h2>
            <p class="mb-12 max-w-3xl mx-auto text-gray-400">
                PICK — это тщательно разработанный 2-х годовой план, который начинается с языковой подготовки и заканчивается стратегической подачей документов.
            </p>

            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
                
                <!-- Step 1: TOPIK (Korean Language) - Emphasizing learning -->
                <div class="process-card p-6 text-left">
                    <div class="step-number text-5xl font-extrabold mb-3">1</div>
                    <h3 class="text-xl font-bold mb-3 text-white">Обучение Корейскому и TOPIK</h3>
                    <p class="text-gray-400 text-sm">
                        Начинаем с нуля и доводим до уровня **TOPIK 4-6**. Наша цель — не только сертификат, но и **свободное владение** языком для успешной академической жизни.
                    </p>
                </div>

                <!-- Step 2: Portfolio/Profile (Профайл) -->
                <div class="process-card p-6 text-left">
                    <div class="step-number text-5xl font-extrabold mb-3">2</div>
                    <h3 class="text-xl font-bold mb-3 text-white">Развитие Внешкольного Профайла</h3>
                    <p class="text-gray-400 text-sm">
                        **Второй шаг**: индивидуальная работа над профайлом, чтобы создать яркое досье. Мы помогаем с волонтёрством, сбором сертификатов и участием в олимпиадах.
                    </p>
                </div>

                <!-- Step 3: Motivational Letter (Мотивационное Письмо) -->
                <div class="process-card p-6 text-left">
                    <div class="step-number text-5xl font-extrabold mb-3">3</div>
                    <h3 class="text-xl font-bold mb-3 text-white">Идеальное Эссе и Интервью</h3>
                    <p class="text-gray-400 text-sm">
                        Разработка убедительного мотивационного письма и учебного плана. **Третий шаг**: подготовка к интервью, чтобы студент уверенно доказал свою ценность приемной комиссии.
                    </p>
                </div>

                <!-- Step 4: Application (Подача) -->
                <div class="process-card p-6 text-left">
                    <div class="step-number text-5xl font-extrabold mb-3">4</div>
                    <h3 class="text-xl font-bold mb-3 text-white">Стратегическая Подача</h3>
                    <p class="text-gray-400 text-sm">
                        **Четвертый шаг**: обучение правильному сбору документов и подаче заявлений (онлайн/офлайн) в несколько ВУЗов для выбора самого выгодного гранта.
                    </p>
                </div>
            </div>
        </div>
    </section>

    <!-- 3. LLM Feature: AI Coordinator (Оценка Шансов) -->
    <section id="ai-coordinator" class="py-16 md:py-24 bg-[#1f2937]">
        <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
            <h2 class="text-3xl md:text-4xl font-bold mb-12 text-center section-heading mx-auto">
                AI-Координатор: Реалистичный Анализ Гранта 🎯
            </h2>
            <div class="bg-[#1f2937] p-8 rounded-xl shadow-2xl border-2 border-blue-600 space-y-6">
                <p class="text-gray-300 text-center">
                    Введите ваши текущие данные, чтобы получить **строгий, реалистичный** анализ шансов на стипендию и увидеть, как программа PICK увеличивает ваш потенциал.
                </p>

                <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                    <input type="text" id="targetMajor" placeholder="Желаемая Специальность (напр., Computer Science)" class="input-style" required>
                    <input type="text" id="currentTOPIK" placeholder="Текущий уровень TOPIK (напр., 5 или 6)" class="input-style" required>
                </div>
                <textarea type="text" id="currentGPA" placeholder="Средний балл (GPA) из аттестата/транскрипта (напр., 4.7/5.0)" rows="1" class="input-style resize-none" required></textarea>
                <textarea id="currentAchievements" placeholder="Ключевые достижения, внеклассная деятельность, награды (ВАЖНО!)" rows="3" class="input-style resize-none" required></textarea>

                <button id="evaluateButton" class="cta-button w-full px-8 py-3 rounded-lg uppercase tracking-wider disabled:opacity-50 flex items-center justify-center">
                    <span id="buttonText">Получить Реалистичный Анализ</span>
                    <div id="loader" class="hidden ml-3 spinner"></div>
                </button>
                
                <div id="resultOutputContainer" class="mt-6 p-6 result-card hidden border-blue-400">
                    <h4 class="text-2xl font-bold text-blue-400 mb-4">Анализ AI-Координатора:</h4>
                    <div id="resultOutput" class="text-gray-200 whitespace-pre-wrap leading-relaxed"></div>
                    <p class="mt-6 text-sm italic text-gray-500">
                        <strong>Этот анализ</strong> основан на исторических данных. Для получения **гарантированного сопровождения** и индивидуальной стратегии, запишитесь на консультацию.
                    </p>
                </div>
            </div>
        </div>
    </section>

    <!-- 4. The Grand Prize Section (Спонсорство Авиабилетов) -->
    <section id="prize" class="py-16 md:py-24 bg-[#101010]">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <h2 class="text-3xl md:text-4xl font-bold mb-12 text-center section-heading mx-auto">
                Бесплатные Авиабилеты: Шанс для Топ-Студентов ✈️
            </h2>
            
            <div class="flex flex-col md:flex-row items-stretch bg-[#1f2937] p-6 md:p-10 rounded-lg shadow-2xl border-2 border-blue-500">
                
                <div class="md:w-full md:pr-10 mb-6 md:mb-0">
                    <h3 class="text-3xl font-extrabold text-blue-400 mb-4 flex items-center">
                        <svg class="w-8 h-8 mr-3" fill="currentColor" viewBox="0 0 24 24"><path d="M12 2C6.477 2 2 6.477 2 12s4.477 10 10 10 10-4.477 10-10S17.523 2 12 2zm-1 15.938v-3.876h2v3.876H11zm0-4.876V6.062h2v7.001H11z"/></svg>
                        Перелет в Корею: Бонус за 100% Грант!
                    </h3>
                    <p class="text-lg text-yellow-400 font-semibold mb-4">
                        Получите <strong class="text-white">ОПЛАЧЕННЫЙ АВИАБИЛЕТ</strong> от PICK! Студенты, <strong class="underline">зарегистрировавшиеся до 31 ОКТЯБРЯ</strong> и вошедшие в тройку лучших (<strong class="text-blue-300">Топ-3</strong>) по результатам поступления на 100% грант, получат наш специальный спонсорский бонус.
                    </p>
                    <p class="text-lg text-gray-300 mb-6">
                        Мы ценим стремление к совершенству. PICK спонсирует авиабилеты для трех самых успешных студентов каждого семестра, которые добились максимального 100% гранта в топовых университетах Кореи.
                    </p>
                    <ul class="space-y-3 text-gray-300">
                        <li class="flex items-center">
                            <span class="text-blue-400 text-2xl mr-3 flex-shrink-0">✈️</span>
                            <span class="font-medium"><strong>Топ-3 студента</strong>, успешно поступивших с 100% грантом.</span>
                        </li>
                        <li class="flex items-center">
                            <span class="text-blue-400 text-2xl mr-3 flex-shrink-0">🚀</span>
                            <span class="font-medium">Билеты на перелет в Корею **БЕСПЛАТНО** за счет PICK.</span>
                        </li>
                    </ul>
                </div>
            </div>
        </div>
    </section>

    <!-- 5. Testimonials Section (Feedback Block) -->
    <section class="py-16 md:py-24 bg-black">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
            <h2 class="text-3xl md:text-4xl font-bold mb-12 section-heading mx-auto">
                Истории Успеха
            </h2>

            <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
                <!-- Testimonial 1 (Mock) -->
                <div class="process-card p-6 border-t-4 border-blue-500">
                    <p class="italic text-gray-300 mb-4">"Когда я только узнала о программе PICK, даже не могла представить, насколько сильно она изменит мою жизнь. За два года я не только улучшила свой корейский и прошла серьезную подготовку, но и поняла, в каком направлении хочу развиваться. Благодаря поддержке кураторов и преподавателей, я смогла поступить в K-ARTS – вуз моей мечты – и получить полную стипендию на одном из самых конкурентных направлений. Я безмерно благодарна всей команде PICK и Диане за веру в меня и за ту невероятную возможность, которую они мне дали."</p>
                    <p class="font-semibold text-white">— Карина, 17 лет, г. Алматы. Поступила в K-ARTS (Сеул), специальность – арт-менеджмент. Самая престижная стипендия.</p>

                </div>

                <!-- Testimonial 2 (Mock) -->
                <div class="process-card p-6 border-t-4 border-blue-500">
                    <p class="italic text-gray-300 mb-4">"Программа PICK стала для меня настоящим трамплином. Я всегда интересовался IT, но не знал, с чего начать, и не верил, что реально поступить за границу на полную стипендию. Благодаря PICK я систематизировал знания, подтянул язык и научился правильно подавать себя на международном уровне. Поступление в Inha University на 100% стипендию – это результат не только моего труда, но и той огромной поддержки, которую я получил в PICK."</p>
                    <p class="font-semibold text-white">— Азамат, 18 лет, г. Астана. Поступил в Inha University (Южная Корея), специальность – информационные технологии. 100% стипендия на 4 года.</p>
                </div>

                <!-- Testimonial 3 (Mock) -->
                <div class="process-card p-6 border-t-4 border-blue-500">
                    <p class="italic text-gray-300 mb-4">"С самого детства я мечтала стать врачом, но обучение за границей казалось чем-то недостижимым, тем более в Корее. PICK изменил это. Здесь я получила не только академическую подготовку, но и уверенность в себе. Каждое занятие, консультации, подготовка к собеседованиям – всё это сыграло ключевую роль. Сейчас я начинаю обучение в медицинском университете в Южной Корее, и моя мечта становится реальностью. Я искренне благодарна команде PICK за их профессионализм и человечность."</p>
                    <p class="font-semibold text-white">— Милана, 17 лет, г. Актобе. Поступила в Ulsan University, специальность – медицина. 100% стипендия.</p>
                </div>
            </div>
        </div>
    </section>
    
    <!-- 6. Final CTA Section (Deep Indigo Block) -->
    <section id="free-trial" class="py-16 md:py-24 bg-blue-900 text-white text-center">
        <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
            <h2 class="text-3xl sm:text-4xl font-bold mb-4">
                Начните <strong>бесплатную консультацию</strong>.
            </h2>
            <p class="text-xl font-light mb-8 opacity-90">
                Запишитесь, чтобы составить индивидуальный план поступления и узнать свой реальный шанс на грант.
            </p>
            <!-- CTA Button now links directly to Google Form -->
            <div class="max-w-md mx-auto">
                 <a href="https://docs.google.com/forms/d/e/1FAIpQLSfVxNrfayVQuPa5MRNCPeyZI9GVcbfDg0KitNgAwAT3CkEiCw/viewform?usp=dialog" target="_blank"
                    class="cta-button w-full sm:w-auto px-8 py-3 rounded-lg uppercase tracking-wider flex items-center justify-center">
                    Записаться сейчас
                </a>
            </div>
        </div>
    </section>

    <!-- 7. Footer (Darkest Black) -->
    <footer id="contacts" class="bg-gray-900 text-gray-400 py-10">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 flex flex-col md:flex-row justify-between items-center space-y-6 md:space-y-0">
            
            <div class="text-center md:text-left">
                <a href="#" class="text-3xl font-extrabold text-white mb-2 block">PICK</a>
                <p class="text-sm">EdTech Platform &copy; 2025. Все права защищены.</p>
            </div>

            <div class="flex space-x-6 text-xl">
                <!-- 1. INSTAGRAM LINK (Updated SVG) -->
                <a href="https://www.instagram.com/pick_topik/?igsh=YWU4NnEwMG1jdGk1#" target="_blank" class="hover:text-blue-400 transition" aria-label="Instagram">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="lucide lucide-instagram">
                        <rect width="20" height="20" x="2" y="2" rx="5" ry="5"></rect>
                        <path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z"></path>
                        <line x1="17.5" x2="17.5" y1="6.5" y2="6.5"></line>
                    </svg>
                </a>
                
                <!-- 2. WHATSAPP LINK (Updated SVG) -->
                <a href="https://wa.me/77764392660" target="_blank" class="hover:text-green-400 transition" aria-label="WhatsApp">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="lucide lucide-message-circle">
                        <path d="M7.9 20A9.3 9.3 0 0 1 4 16.1L2 22l6-2"></path>
                        <path d="M19 19a2 2 0 0 0 2-2V7a2 2 0 0 0-2-2H5a2 2 0 0 0-2 2v10a2 2 0 0 0 2 2h14z"></path>
                    </svg>
                </a>
            </div>
    </footer>


    <script>
        // --- AI Coordinator Elements ---
        const targetMajorInput = document.getElementById('targetMajor');
        const currentTOPIKInput = document.getElementById('currentTOPIK');
        const currentGPAInput = document.getElementById('currentGPA');
        const currentAchievementsInput = document.getElementById('currentAchievements');
        const evaluateButton = document.getElementById('evaluateButton');
        const resultOutput = document.getElementById('resultOutput');
        const resultOutputContainer = document.getElementById('resultOutputContainer');
        const buttonText = document.getElementById('buttonText');
        const loader = document.getElementById('loader');
        
        // --- API Configuration ---
        const apiKey = "AIzaSyAjqR2AGOvW-nqQdFGqk1BoXdrsQNMBbEw"; 
        const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-05-20:generateContent?key=${apiKey}`;
        
        // --- AI Coordinator Logic ---
        
        async function runLLMEvaluation() {
            // Main function for AI evaluation logic
            const major = targetMajorInput.value.trim();
            const topik = currentTOPIKInput.value.trim();
            const gpa = currentGPAInput.value.trim();
            const achievements = currentAchievementsInput.value.trim();
            
            if (!major || !topik || !gpa || !achievements) {
                resultOutput.textContent = "Пожалуйста, заполните все поля. Для проведения серьезного анализа нужны полные данные.";
                resultOutputContainer.classList.remove('hidden');
                return;
            }

            evaluateButton.disabled = true;
            buttonText.textContent = "Проводим глубокий анализ...";
            loader.classList.remove('hidden');
            resultOutputContainer.classList.add('hidden');
            resultOutput.textContent = '';
            
            // NEW SYSTEM PROMPT: Updated Sections 3 and 4 as per user request
            const systemPrompt = `
Вы — строгий, реалистичный и стратегический AI-координатор PICK. Ваша цель — предоставить студенту максимально честный и реалистичный анализ его шансов на получение стипендии (100% гранта или 70% скидки) в Корее. **Полностью исключите любое упоминание об английском языке или экзаменах IELTS/TOEFL из вашего анализа.**

Ваш ответ должен быть структурирован в четыре обязательных раздела:

### 1. Реалистичная Оценка Шансов (Самостоятельное Поступление)
* Оцените, что шансы студента на 100% грант при самостоятельной подаче в ТОП-5 университеты (SNU, Yonsei, Korea, KAIST, POSTECH) без профессиональной подготовки составляют не более **10-20%**.
* Объясните, что даже при высоком TOPIK **${topik}** и GPA **${gpa}**, **конкуренция за стипендию** в Южной Корее — это не только баллы, но и безупречность документов (Motivational Letter, Study Plan, Recommendation Letters), а также **высочайший уровень владения корейским языком, который не ограничивается только оценкой TOPIK.**
* Строго подчеркните, что достижения (**${achievements}**) должны быть идеально представлены, иначе они бесполезны.

### 2. Повышение Шансов с Программой PICK
* Заявите, что с программой PICK шансы увеличиваются до **70-85%** (для 70%-100% гранта).
* Объясните, почему:
    * **Гарантия TOPIK:** PICK обеспечивает всестороннее обучение корейскому языку, гарантируя не только успешную сдачу TOPIK на высокий балл, но и **свободное владение, необходимое для академической среды.**
    * **2-летняя структура:** Мы не готовим за 3 месяца, а создаем профайл 2 года, включая помощь в организации волонтёрства и сборе сертификатов.
    * **Специализация Эссе:** Идеальная подача достижения **${achievements}** и GPA **${gpa}** в Motivational Letter, адаптированная под каждый ВУЗ.
    * **Стратегический Выбор:** Использование нашей внутренней базы данных для выбора ВУЗов, которые **реально ищут** студентов, подходящих под профиль **${major}**.

### 3. Стратегический Список Университетов (Максимальный Грант)
* На основе данных: TOPIK **${topik}**, GPA **${gpa}**, Достижения **${achievements}** и Специальность **${major}**, предложите **3-4 университета**, которые не относятся к "недостижимому" ТОП-3, но максимально щедры на гранты для студентов с сильной корейской подготовкой и профилем.
* **Используйте ТОЛЬКО этот список (без объяснения, что это именно TOPIK-гранты):** Chung-Ang University (CAU), Dongguk University, Inha University, Pusan National University (PNU).
* Для каждого ВУЗа укажите, почему он стратегически выгоден (например, сильное инженерное направление, расположен в Сеуле, низкая конкуренция за стипендию по сравнению с SKY).

---

### 4. Дорожная Карта PICK: Ваш 2-летний Путь к Успеху 🗺️
**Этот раздел является вашим пошаговым планом, который PICK реализует для каждого студента. Он показывает, как мы превращаем ваш текущий потенциал в 100% грант.**

| Этап и Период | Фокус | Детали и Задачи |
| :--- | :--- | :--- |
| **🟢 ЭТАП 1: Интенсивное Изучение Языка (Первый Год)** | | |
| Месяцы 1–6 | База и TOPIK I (Уровни 1-2) | Изучение основ грамматики и лексики. Ежедневная практика. |
| Месяцы 7–12 | TOPIK II (Уровни 3-4+) | Углубленное изучение академической грамматики. Интенсивная подготовка к секции "Письмо". **Сдача официального экзамена TOPIK.** |
| **🟡 ЭТАП 2: Академическая Подготовка (Второй Год, Начало)** | | |
| Месяцы 13–18 | Специализация и GPA | Фокусировка на профильных предметах. Прохождение дополнительных курсов/олимпиад, связанных с выбранной специальностью. |
| Параллельно | Портфолио и Сертификаты | **Активная работа над профайлом**: участие в волонтёрстве, сбор сертификатов и наград. |
| **🔴 ЭТАП 3: Документы и Стратегическое Эссе (Второй Год, Середина)** | | |
| Месяцы 19–21 | Академические Документы | Запрос выписок. **Апостилирование** или легализация ВСЕХ необходимых документов. |
| Месяцы 21 | Мотивационное Письмо (ML) и SP | Написание и редактирование финальных версий **Мотивационного Письма** и **Учебного Плана**. |
| **🟣 ЭТАП 4: Интервью, Подача и Отъезд (Второй Год, Конец)** | | |
| Месяцы 22 | Подготовка к Интервью | Интенсивная подготовка к собеседованию (чаще всего на корейском), фокусировка на вопросах по специальности. |
| Месяцы 23 | Финальная Подача | Обучение правильной **онлайн и офлайн подаче** документов. |
| Месяцы 24 | Зачисление и Виза | Получение уведомления о зачислении на грант. Планирование отъезда. |
`;
            
            const userQuery = `Проведи анализ. Мои данные: Специальность: ${major}. Текущий TOPIK: ${topik}. GPA: ${gpa}. Достижения: ${achievements}. Мне нужно понять мои реальные шансы и увидеть, как PICK может их повысить.`;
            
            const payload = {
                contents: [{ parts: [{ text: userQuery }] }],
                systemInstruction: { parts: [{ text: systemPrompt }] },
                tools: [{ "google_search": {} }], // Use search for grounding on current university data
            };
            
            let attempts = 0;
            const maxAttempts = 3;
            const initialDelay = 1000;

            const makeApiCall = async () => {
                const response = await fetch(apiUrl, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload)
                });

                if (response.ok) {
                    return response.json();
                }

                // Handle server errors or rate limiting by retrying
                throw new Error(`API call failed with status: ${response.status}`);
            };

            while (attempts < maxAttempts) {
                try {
                    const result = await makeApiCall();
                    
                    const text = result.candidates?.[0]?.content?.parts?.[0]?.text || "Ошибка: Не удалось получить ответ от AI. Попробуйте еще раз.";

                    resultOutput.textContent = text;
                    resultOutputContainer.classList.remove('hidden');
                    
                    // Cleanup
                    evaluateButton.disabled = false;
                    buttonText.textContent = "Получить Реалистичный Анализ";
                    loader.classList.add('hidden');

                    return; // Exit successfully

                } catch (error) {
                    attempts++;
                    console.error(`Attempt ${attempts} failed:`, error.message);
                    if (attempts >= maxAttempts) {
                        resultOutput.textContent = "Извините, произошла ошибка связи с аналитической системой. Пожалуйста, попробуйте позже или не теряйте время — запишитесь на консультацию сейчас.";
                        resultOutputContainer.classList.remove('hidden');
                        
                        // Cleanup on final failure
                        evaluateButton.disabled = false;
                        buttonText.textContent = "Получить Реалистичный Анализ";
                        loader.classList.add('hidden');
                        
                        return;
                    }
                    // Exponential backoff
                    const delay = initialDelay * Math.pow(2, attempts - 1);
                    await new Promise(resolve => setTimeout(resolve, delay));
                }
            }
        }
        
        // Attach listener for the AI button
        if (evaluateButton) {
            evaluateButton.addEventListener('click', runLLMEvaluation);
        }

    </script>


</body>
</html>

