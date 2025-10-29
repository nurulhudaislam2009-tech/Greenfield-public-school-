# Greenfield-public-school-
<!DOCTYPE html>
<html lang="bn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Greenfield Public School - Play, Learn, Shine</title>
    <!-- Tailwind CSS লোড করা হচ্ছে -->
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* ইন্টার (Inter) ফন্ট ব্যবহার করা হয়েছে */
        body {
            font-family: 'Inter', sans-serif;
            background-color: #111827; /* Dark Grey/Black for Dark Theme */
            color: #f3f4f6; /* Light text color */
            min-height: 100vh;
        }
        
        /* কাস্টম কালার প্যালেট: গভীর সবুজ অ্যাকসেন্ট */
        .primary-green-bg {
            background-color: #059669; /* Emerald 600 - Deep Green */
        }
        .text-primary-green {
            color: #059669;
        }
        .primary-green-hover:hover {
            background-color: #047857; /* Emerald 700 - Darker Green for hover */
        }
        .secondary-blue-bg {
            background-color: #3b82f6; /* Bright Blue for CTA */
        }
        .secondary-blue-hover:hover {
            background-color: #2563eb; /* Darker Blue for hover */
        }
        
        /* ডার্ক সেকশন ব্যাকগ্রাউন্ড */
        .dark-section-bg {
            background-color: #1f2937; /* Gray 800 */
        }
        
        /* সমস্ত প্রধান কন্টেন্টে বোল্ড এবং ইটালিক স্টাইল প্রয়োগ করা হয়েছে (ম্যান্ডেটরি) */
        body, p, a, li, td, th, label, input, textarea, select, h1, h2, h3, h4, span, button {
            font-weight: 700 !important; /* Bold */
            font-style: italic !important; /* Italic */
        }
        
        /* SPA স্টাইল: কেবল সক্রিয় কন্টেন্ট দেখাবে */
        .page-content {
            display: none;
            animation: fadeIn 0.5s ease-in-out;
            min-height: 70vh; /* মেনু বাদে যেন স্ক্রিন ভরে থাকে */
        }
        .page-content.active {
            display: block;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        /* ফর্ম ইনপুট স্টাইল ডার্ক থিমের জন্য */
        .form-input {
            background-color: #374151; /* Gray 700 */
            color: #f3f4f6; /* Light text */
            border-color: #4b5563; /* Gray 600 */
        }
        .form-input:focus {
            border-color: #059669; 
            outline: none;
            box-shadow: 0 0 0 2px rgba(5, 150, 105, 0.5); /* Primary Green Ring */
        }
    </style>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        'primary': '#059669', 
                        'secondary': '#3b82f6', 
                    }
                }
            }
        }
        
        // SPA নেভিগেশন ফাংশন
        function showPage(pageId) {
            // সমস্ত পেজ ডি-অ্যাকটিভেট করা
            const allPages = document.querySelectorAll('.page-content');
            allPages.forEach(page => {
                page.classList.remove('active');
            });

            // নির্বাচিত পেজটি অ্যাকটিভেট করা
            const targetPage = document.getElementById(pageId);
            if (targetPage) {
                targetPage.classList.add('active');
                window.scrollTo({ top: 0, behavior: 'smooth' }); // স্ক্রল টপ-এ নিয়ে আসা
                history.pushState(null, '', `#${pageId}`); // URL আপডেট করা
            }
            
            // মোবাইল মেনু বন্ধ করা
            const mobileMenu = document.getElementById('mobile-menu');
            if (mobileMenu && !mobileMenu.classList.contains('hidden')) {
                mobileMenu.classList.add('hidden');
            }
        }

        // পেজ লোড হলে ডিফল্ট বা ইউআরএল হ্যাশ অনুযায়ী পেজ দেখানো
        window.onload = function() {
            const hash = window.location.hash.replace('#', '');
            if (hash && document.getElementById(hash)) {
                showPage(hash);
            } else {
                showPage('home');
            }
        };
    </script>
</head>
<body class="antialiased">

    <!-- নেভিগেশন বার (Header) - Sticky -->
    <header class="primary-green-bg shadow-2xl sticky top-0 z-50">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between items-center h-20">
                <!-- লোগো/শিরোনাম -->
                <div class="flex-shrink-0 flex items-center">
                    <!-- উড়ন্ত হলুদ পাখি SVG লোগো -->
                    <svg class="w-8 h-8 mr-2 text-yellow-300" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                        <path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2z"></path>
                        <path d="M17 10s-3 3-4 3-4-3-4-3 1-3 4-3 4 3 4 3zM12 16v-4"></path>
                        <path d="M8 8l1 1m6-1l-1 1"></path>
                    </svg>
                    <span class="text-3xl font-extrabold text-white tracking-wide italic">Greenfield Public School</span>
                </div>
                <!-- নেভিগেশন লিঙ্কস (ডেস্কটপ) - প্রতিটির জন্য আলাদা বাটন -->
                <nav class="hidden lg:flex space-x-2">
                    <button onclick="showPage('home')" class="py-2 px-3 rounded-lg text-white hover:bg-green-700 transition duration-150">হোম</button>
                    <button onclick="showPage('facilities')" class="py-2 px-3 rounded-lg text-white hover:bg-green-700 transition duration-150">সুবিধা ও বৈশিষ্ট্য</button>
                    <button onclick="showPage('fees_schedule')" class="py-2 px-3 rounded-lg text-white hover:bg-green-700 transition duration-150">ভর্তি ও বেতন</button>
                    <button onclick="showPage('authority')" class="py-2 px-3 rounded-lg text-white hover:bg-green-700 transition duration-150">কর্তৃপক্ষ</button>
                    <button onclick="showPage('before_admission')" class="py-2 px-3 rounded-lg text-white hover:bg-green-700 transition duration-150">ভর্তির পূর্বে কিছু কথা</button>
                    <button onclick="showPage('about')" class="py-2 px-3 rounded-lg text-white hover:bg-green-700 transition duration-150">কিছু কথা</button>
                    <button onclick="showPage('why_different')" class="py-2 px-3 rounded-lg text-white hover:bg-green-700 transition duration-150">আমরা কেন ব্যতিক্রম??</button>
                    <button onclick="showPage('contact')" class="py-2 px-3 rounded-lg text-white hover:bg-green-700 transition duration-150">যোগাযোগ</button>
                </nav>
                <!-- মোবাইল মেনু বাটন -->
                <button id="mobile-menu-button" class="lg:hidden p-2 rounded-md text-white hover:bg-green-700 transition duration-150" onclick="document.getElementById('mobile-menu').classList.toggle('hidden')">
                    <svg class="w-7 h-7" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7"></path></svg>
                </button>
            </div>
        </div>
        
        <!-- মোবাইল মেনু (Hidden by default) -->
        <div id="mobile-menu" class="hidden lg:hidden primary-green-bg border-t border-green-700 pb-2">
            <div class="px-2 pt-2 pb-3 space-y-1 flex flex-col">
                <button onclick="showPage('home')" class="text-white hover:bg-green-700 block px-3 py-2 rounded-md text-left">হোম</button>
                <button onclick="showPage('facilities')" class="text-white hover:bg-green-700 block px-3 py-2 rounded-md text-left">সুবিধা ও বৈশিষ্ট্য</button>
                <button onclick="showPage('fees_schedule')" class="text-white hover:bg-green-700 block px-3 py-2 rounded-md text-left">ভর্তি ও বেতন</button>
                <button onclick="showPage('authority')" class="text-white hover:bg-green-700 block px-3 py-2 rounded-md text-left">কর্তৃপক্ষ</button>
                <button onclick="showPage('before_admission')" class="text-white hover:bg-green-700 block px-3 py-2 rounded-md text-left">ভর্তির পূর্বে কিছু কথা</button>
                <button onclick="showPage('about')" class="text-white hover:bg-green-700 block px-3 py-2 rounded-md text-left">কিছু কথা</button>
                <button onclick="showPage('why_different')" class="text-white hover:bg-green-700 block px-3 py-2 rounded-md text-left">আমরা কেন ব্যতিক্রম??</button>
                <button onclick="showPage('contact')" class="text-white hover:bg-green-700 block px-3 py-2 rounded-md text-left">যোগাযোগ</button>
            </div>
        </div>
    </header>

    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
        
        <!-- ==================================== ১. হোম সেকশন ==================================== -->
        <section id="home" class="page-content dark-section-bg p-8 sm:p-12 rounded-xl shadow-2xl">
            <div class="text-center py-10 sm:py-16">
                <p class="text-3xl sm:text-4xl font-extrabold mb-3 text-yellow-300 tracking-wider italic">
                    Play, Learn, Shine
                </p>
                <h1 class="text-5xl sm:text-7xl font-extrabold mb-6 leading-tight text-primary-green italic">
                    Greenfield Public School
                </h1>
                <p class="text-lg sm:text-xl font-medium mb-8 max-w-3xl mx-auto text-gray-300 italic">
                    স্থাপিত: **২০২৫** | স্থান: **Ribor, Barodi, Sonargaon, Narayanganj**
                    <br>
                    ক্লাস শুরু: **জানুয়ারী ২০২৬**
                </p>
                <!-- CTA Button - নীল রঙের -->
                <button onclick="showPage('admission_form')" class="inline-flex items-center justify-center px-8 py-3 border border-transparent text-lg font-semibold rounded-full shadow-2xl text-white secondary-blue-bg secondary-blue-hover transition duration-300 transform hover:scale-105 italic">
                    ভর্তির বিস্তারিত জানুন
                </button>
                
                <div class="mt-12 p-6 bg-gray-800 rounded-lg">
                    <h3 class="text-2xl font-extrabold mb-3 text-yellow-300 italic">স্কুলের সময়সূচি:</h3>
                    <ul class="space-y-1 text-base text-gray-300 italic">
                        <li><span class="font-extrabold text-white">শিফট ১ (প্লে - ২য় শ্রেণি):</span> সকাল ৮:০০ টা থেকে সকাল ১০:০০ টা পর্যন্ত।</li>
                        <li><span class="font-extrabold text-white">শিফট ২ (৩য় শ্রেণি থেকে বাকি সকল):</span> সকাল ১০:২০ টা থেকে দুপুর ৩:৩০ টা পর্যন্ত।</li>
                    </ul>
                </div>
            </div>
        </section>

        <!-- ==================================== ২. কিছু কথা (Principal's Message) ==================================== -->
        <section id="about" class="page-content dark-section-bg p-8 sm:p-12 rounded-xl shadow-2xl">
            <h2 class="text-4xl font-extrabold text-center mb-10 text-primary-green italic">কিছু কথা</h2>
            <div class="bg-gray-800 p-6 rounded-xl text-gray-300 italic">
                <p class="mb-6 leading-relaxed italic">
                    সম্মানিত সুধী,
                </p>
                <p class="mb-6 leading-relaxed italic">
                    আসসালামু আলাইকুম
                </p>
                <p class="mb-6 leading-relaxed italic">
                    মহান স্রষ্টার অপার মহিমায় আর আপনাদের দোয়ায় মানসম্পন্ন শিক্ষা প্রদানের লক্ষ্যে কয়েকজন স্বপ্নদর্শী শিক্ষানুরাগী ব্যক্তির উদ্যোগে ২০২৫ সালের অক্টোবর মাসে গ্রিনফিল্ড পাবলিক স্কুল আত্মপ্রকাশ করে।
                </p>
                <p class="mb-6 leading-relaxed italic">
                    গ্রিনফিল্ড পাবলিক স্কুল প্রাথমিক ও মাধ্যমিক স্তরের শিক্ষার্থীদের সর্বনিম্ন খরচে সর্বোত্তম মানের শিক্ষা প্রদান করার একটি উচ্চাভিলাষী প্ল্যাটফর্ম। গ্রিনফিল্ড পাবলিক স্কুল এর "টিচার্স প্যানেল” ঢাকা বিশ্ববিদ্যালয়সহ দেশসেরা মেধাবী গ্র্যাজুয়েটদের নিয়ে সুগঠিত ও সুনিয়ন্ত্রিত। পাশাপাশি রয়েছে বিজ্ঞ ও দূরদর্শী উপদেষ্টা পরিষদ। এখানে আমরা আমাদের শিক্ষার্থীদের স্বতন্ত্রভাবে উপযোগী শিক্ষা নির্দেশিকা প্রদানের প্রতিশ্রুতি দিচ্ছি যাতে তারা আত্মবিশ্বাসী হয়ে উজ্জ্বল ভবিষ্যতের প্রত্যাশা করে। সেই সাথে দেশ ও দশের সেবায় আত্মনিয়োগ করে যুগের সাথে তাল মিলিয়ে স্বপ্নের স্বর্ণ শিখরে আরোহণ করতে পারে।
                </p>
                <p class="text-right text-yellow-300 font-extrabold mt-8 italic">
                    প্রিন্সিপাল<br>
                    গ্রিনফিল্ড পাবলিক স্কুল
                </p>
            </div>
        </section>

        <!-- ==================================== ৩. আমরা কেন ব্যতিক্রম?? ==================================== -->
        <section id="why_different" class="page-content dark-section-bg p-8 sm:p-12 rounded-xl shadow-2xl">
            <h2 class="text-4xl font-extrabold text-center mb-10 text-primary-green italic">আমরা কেন ব্যতিক্রম??</h2>
            <div class="bg-gray-800 p-6 rounded-xl text-gray-300 italic">
                <ul class="space-y-4 list-none pl-0 italic">
                    <li class="flex items-start">
                        <span class="text-xl text-yellow-300 mr-3">»</span>
                        <p class="flex-1 italic">সাপ্তাহিক ফিডব্যাক শীটের মাধ্যমে সমস্যা চিহ্নিত করে অভিভাবকদের সাথে আলোচনা সাপেক্ষে সমস্যা সমাধান।</p>
                    </li>
                    <li class="flex items-start">
                        <span class="text-xl text-yellow-300 mr-3">»</span>
                        <p class="flex-1 italic">সাপ্তাহিক সিটি (মূল্যায়ন) পরীক্ষার মাধ্যমে শিক্ষার্থীদের মেধা মূল্যায়ন।</p>
                    </li>
                    <li class="flex items-start">
                        <span class="text-xl text-yellow-300 mr-3">»</span>
                        <p class="flex-1 italic">অভিজ্ঞ ও দূরদর্শী উপদেষ্টা পর্ষদের মাধ্যমে শিক্ষা কার্যক্রম পরিচালনা।</p>
                    </li>
                    <li class="flex items-start">
                        <span class="text-xl text-yellow-300 mr-3">»</span>
                        <p class="flex-1 italic">বিষয়ভিত্তিক অভিজ্ঞ শিক্ষকমণ্ডলী দ্বারা পাঠদান।</p>
                    </li>
                    <li class="flex items-start">
                        <span class="text-xl text-yellow-300 mr-3">»</span>
                        <p class="flex-1 italic">ক্লাসে পড়া না পারলে ক্লাস শেষে বিদ্যালয় বসে পড়া কমপ্লিট করা।</p>
                    </li>
                    <li class="flex items-start">
                        <span class="text-xl text-yellow-300 mr-3">»</span>
                        <p class="flex-1 italic">আপনার সন্তানের নিরাপত্তার জন্য সার্বক্ষণিক পর্যবেক্ষণ (সিসি ক্যামেরা)।</p>
                    </li>
                    <li class="flex items-start">
                        <span class="text-xl text-yellow-300 mr-3">»</span>
                        <p class="flex-1 italic">সুন্দর ও মনোরম পরিবেশে শিক্ষা-কার্যক্রম সম্পাদন।</p>
                    </li>
                </ul>
            </div>
        </section>

        <!-- ==================================== ৪. সুবিধা ও বৈশিষ্ট্য সেকশন (Facilities) ==================================== -->
        <section id="facilities" class="page-content dark-section-bg p-8 sm:p-12 rounded-xl shadow-2xl">
            <h2 class="text-4xl font-extrabold text-center mb-10 text-primary-green italic">সুবিধা ও বৈশিষ্ট্য</h2>
            
            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6 text-gray-100">
                
                <!-- সুবিধা কার্ড ১: শিক্ষাদান পদ্ধতি -->
                <div class="bg-gray-800 p-6 rounded-xl shadow-lg border-l-4 border-yellow-300 italic">
                    <h3 class="text-xl font-extrabold mb-2 text-secondary-blue italic">আধুনিক শিক্ষা ও ক্লাস</h3>
                    <ul class="space-y-1 list-disc pl-5 text-sm text-gray-300 italic">
                        <li>ক্লাসের পড়া ক্লাসে শেষ করা হবে।</li>
                        <li>দুর্বল শিক্ষার্থীদের জন্য স্পেশাল ক্লাসের ব্যবস্থা।</li>
                        <li>রয়েছে Kids English Spoken এর ব্যবস্থা।</li>
                        <li>প্রতি সেমিস্টারে মেধাবৃত্তির ব্যবস্থা।</li>
                    </ul>
                </div>

                <!-- সুবিধা কার্ড ২: প্রযুক্তি ও নিরাপত্তা -->
                <div class="bg-gray-800 p-6 rounded-xl shadow-lg border-l-4 border-yellow-300 italic">
                    <h3 class="text-xl font-extrabold mb-2 text-secondary-blue italic">প্রযুক্তি ও নিরাপত্তা</h3>
                    <ul class="space-y-1 list-disc pl-5 text-sm text-gray-300 italic">
                        <li>মাল্টিমিডিয়া ক্লাসরুমের ব্যবস্থা। **(Highlighted)**</li>
                        <li>ডিজিটাল অ্যাটেন্ডেন্স থাকবে।</li>
                        <li>সিসি ক্যামেরা দ্বারা সার্বক্ষণিক পর্যবেক্ষণ। **(Highlighted)**</li>
                        <li>SMS এর মাধ্যমে রেজাল্ট প্রদান।</li>
                    </ul>
                </div>

                <!-- সুবিধা কার্ড ৩: অবকাঠামো ও যত্ন -->
                <div class="bg-gray-800 p-6 rounded-xl shadow-lg border-l-4 border-yellow-300 italic">
                    <h3 class="text-xl font-extrabold mb-2 text-secondary-blue italic">অবকাঠামো ও যত্ন</h3>
                    <ul class="space-y-1 list-disc pl-5 text-sm text-gray-300 italic">
                        <li>স্কুলে সুবিশাল লাইব্রেরি ও নিজস্ব ক্যান্টিন থাকবে।</li>
                        <li>বড় খেলার মাঠ আছে।</li>
                        <li>ছেলেদের জন্য ২টি ও মেয়েদের জন্য ২টি আলাদা ওয়াশব্লক আছে।</li>
                        <li>বিদ্যালয়ে সার্বক্ষণিক আয়ার ব্যবস্থা।</li>
                    </ul>
                </div>
                
                <!-- সুবিধা কার্ড ৪: পরিবেশ ও কার্যক্রম -->
                <div class="bg-gray-800 p-6 rounded-xl shadow-lg border-l-4 border-yellow-300 italic sm:col-span-2 lg:col-span-1 mx-auto w-full lg:w-auto">
                    <h3 class="text-xl font-extrabold mb-2 text-secondary-blue italic">অতিরিক্ত সুবিধা</h3>
                    <ul class="space-y-1 list-disc pl-5 text-sm text-gray-300 italic">
                        <li>সার্বক্ষণিক বিদ্যুৎ সরবরাহ। **(Highlighted)**</li>
                        <li>ক্রীড়া ও সাংস্কৃতিক কার্যক্রম।</li>
                        <li>কম্পিউটার ল্যাব আছে।</li>
                        <li>সপ্তাহে একবার অভিভাবক মিটিং হবে।</li>
                    </ul>
                </div>

            </div>
        </section>


        <!-- ==================================== ৫. ভর্তি তথ্য ও বেতন (Fees) ==================================== -->
        <section id="fees_schedule" class="page-content dark-section-bg p-8 sm:p-12 rounded-xl shadow-2xl">
            <h2 class="text-4xl font-extrabold text-center mb-10 text-yellow-300 italic">ভর্তি ও মাসিক বেতন</h2>
            
            <!-- মূল তথ্য -->
            <div class="mb-8 text-center text-xl font-extrabold text-primary-green italic">
                ভর্তি কার্যক্রম চলবে: প্লে থেকে নবম শ্রেণি পর্যন্ত।
            </div>

            <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 text-gray-100">
                
                <!-- ভর্তি ফি শিডিউল টেবিল -->
                <div class="bg-gray-800 p-6 rounded-xl shadow-2xl border-t-4 border-primary-green italic">
                    <h3 class="text-2xl font-extrabold mb-6 text-secondary-blue border-b border-gray-700 pb-2 italic">ভর্তি ফি শিডিউল (Admission Fee Schedule)</h3>
                    <p class="text-xl font-extrabold mb-4 text-white italic">ভর্তি ফর্মের মূল্য: <span class="text-yellow-300">১০০ টাকা</span></p>

                    <div class="overflow-x-auto">
                        <table class="min-w-full divide-y divide-gray-700 rounded-lg overflow-hidden text-sm italic">
                            <thead class="bg-gray-700">
                                <tr>
                                    <th class="px-4 py-3 text-left font-extrabold uppercase tracking-wider text-white">সময়কাল (Period)</th>
                                    <th class="px-4 py-3 text-right font-extrabold uppercase tracking-wider text-white">ভর্তি ফি (Admission Fee)</th>
                                </tr>
                            </thead>
                            <tbody class="divide-y divide-gray-700">
                                <tr class="hover:bg-gray-700">
                                    <td class="px-4 py-3 text-white">১৫ অক্টোবর - ১৫ নভেম্বর</td>
                                    <td class="px-4 py-3 text-right text-primary-green font-extrabold">২০০০ টাকা</td>
                                </tr>
                                <tr class="hover:bg-gray-700">
                                    <td class="px-4 py-3 text-white">১৬ নভেম্বর - ১৫ ডিসেম্বর</td>
                                    <td class="px-4 py-3 text-right text-yellow-500 font-extrabold">২৫০০ টাকা</td>
                                </tr>
                                <tr class="hover:bg-gray-700 bg-gray-700/50">
                                    <td class="px-4 py-3 text-white">১৬ ডিসেম্বর থেকে পরবর্তী</td>
                                    <td class="px-4 py-3 text-right text-red-500 font-extrabold">৩০০০ টাকা</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>

                <!-- মাসিক বেতন শিডিউল টেবিল -->
                <div class="bg-gray-800 p-6 rounded-xl shadow-2xl border-t-4 border-primary-green italic">
                    <h3 class="text-2xl font-extrabold mb-6 text-secondary-blue border-b border-gray-700 pb-2 italic">মাসিক বেতন (Monthly Fees)</h3>
                    <div class="overflow-x-auto">
                        <table class="min-w-full divide-y divide-gray-700 rounded-lg overflow-hidden text-sm italic">
                            <thead class="bg-gray-700">
                                <tr>
                                    <th class="px-4 py-3 text-left font-extrabold uppercase tracking-wider text-white">শ্রেণি (Class)</th>
                                    <th class="px-4 py-3 text-right font-extrabold uppercase tracking-wider text-white">বেতন (Fee)</th>
                                </tr>
                            </thead>
                            <tbody class="divide-y divide-gray-700">
                                <tr class="hover:bg-gray-700">
                                    <td class="px-4 py-3 text-white">প্লে গ্রুপ - ২য় শ্রেণি</td>
                                    <td class="px-4 py-3 text-right text-primary-green font-extrabold">৬০০ টাকা</td>
                                </tr>
                                <tr class="hover:bg-gray-700">
                                    <td class="px-4 py-3 text-white">৩য় - ৪র্থ শ্রেণি</td>
                                    <td class="px-4 py-3 text-right text-primary-green font-extrabold">৭০০ টাকা</td>
                                </tr>
                                <tr class="hover:bg-gray-700">
                                    <td class="px-4 py-3 text-white">৫ম শ্রেণি</td>
                                    <td class="px-4 py-3 text-right text-primary-green font-extrabold">৮০০ টাকা</td>
                                </tr>
                                <tr class="hover:bg-gray-700">
                                    <td class="px-4 py-3 text-white">৬ষ্ঠ - ৮ম শ্রেণি</td>
                                    <td class="px-4 py-3 text-right text-primary-green font-extrabold">১০০০ টাকা</td>
                                </tr>
                                <tr class="hover:bg-gray-700">
                                    <td class="px-4 py-3 text-white">৯ম - ১০ম শ্রেণি</td>
                                    <td class="px-4 py-3 text-right text-primary-green font-extrabold">১২০০ টাকা</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </section>

        <!-- ==================================== ৬. কর্তৃপক্ষের তথ্য (Authority) ==================================== -->
        <section id="authority" class="page-content dark-section-bg p-8 sm:p-12 rounded-xl shadow-2xl">
            <h2 class="text-4xl font-extrabold text-center mb-10 text-primary-green italic">স্কুলের কর্তৃপক্ষ হিসেবে থাকছেন যারা</h2>
            
            <div class="bg-gray-800 p-8 rounded-xl shadow-2xl border-l-4 border-yellow-300 space-y-6 text-gray-200 italic">
                
                <div class="border-b border-gray-700 pb-4">
                    <h4 class="text-xl font-extrabold text-secondary-blue italic">১. চেয়ারম্যান (Chairman)</h4>
                    <p class="ml-4 italic">মো: শাহ আলম, ব্যবস্থাপনা পরিচালক, সিসিমপুর</p>
                    <p class="ml-4 text-sm text-gray-400 italic">(Md. Shah Alam, Managing Director, Sisimpur)</p>
                </div>
                
                <div class="border-b border-gray-700 pb-4">
                    <h4 class="text-xl font-extrabold text-secondary-blue italic">২. ভাইস চেয়ারম্যান (Vice Chairman)</h4>
                    <p class="ml-4 italic">মোসা: নাসিমা আলম</p>
                    <p class="ml-4 text-sm text-gray-400 italic">(Mosa: Nasima Alam)</p>
                </div>

                <div class="border-b border-gray-700 pb-4">
                    <h4 class="text-xl font-extrabold text-secondary-blue italic">৩. কোষাধ্যক্ষ (Treasurer)</h4>
                    <p class="ml-4 italic">মো: রিপন আহসান, সহকারী শিক্ষক, সোনারগাঁ জি. আর. ইন্সটিটিউট</p>
                    <p class="ml-4 text-sm text-gray-400 italic">(Md. Ripon Ahsan, Assistant Teacher, Sonargaon G. R. Institute)</p>
                </div>

                <div>
                    <h4 class="text-xl font-extrabold text-secondary-blue italic">৪. শিক্ষা বিষয়ক প্রধান ও সদস্য সচিব (Head of Education & Member Secretary)</h4>
                    <p class="ml-4 italic">মোসা: শিরিনা আক্তার, প্রিন্সিপাল, গ্রিনফিল্ড পাবলিক স্কুল</p>
                    <p class="ml-4 text-sm text-gray-400 italic">(Mosa: Shirina Akhter, Principal, Greenfield Public School)</p>
                </div>

            </div>
        </section>

        <!-- ==================================== ৭. ভর্তির পূর্বে কিছু কথা ==================================== -->
        <section id="before_admission" class="page-content dark-section-bg p-8 sm:p-12 rounded-xl shadow-2xl">
            <h2 class="text-4xl font-extrabold text-center mb-10 text-primary-green italic">ভর্তির পূর্বে কিছু কথা (Guidelines Before Admission)</h2>
            <div class="bg-gray-800 p-6 rounded-xl text-gray-300 italic">
                <ul class="space-y-4 list-disc pl-5 italic text-lg">
                    <li>প্রতিদিন পরিষ্কার পরিচ্ছন্ন হয়ে স্কুলে আসতে হবে। (Must come to school clean every day.)</li>
                    <li>নির্ধারিত ড্রেস পরিধান করে স্কুলে আসতে হবে। (Must wear the prescribed dress to school.)</li>
                    <li>ক্লাস শুরুর ১৫ মিনিট আগে স্কুলে আসতে হবে। (Must arrive at school 15 minutes before class starts.)</li>
                    <li>৯০% উপস্থিতি নিশ্চিত করতে হবে। (90% attendance must be ensured.)</li>
                </ul>
            </div>
        </section>


        <!-- ==================================== ৮. ভর্তি ফর্ম সেকশন (Admission Form) ==================================== -->
        <section id="admission_form" class="page-content dark-section-bg p-8 sm:p-12 rounded-xl shadow-2xl">
            <h2 class="text-4xl font-extrabold text-center mb-10 text-yellow-300 italic">ভর্তির আবেদন ফর্ম (Admission Application Form)</h2>
            <div class="bg-gray-800 p-6 sm:p-10 rounded-xl shadow-2xl border-t-4 border-primary-green text-gray-100 italic">
                
                <!-- মক ফর্ম, যা সাবমিট হলে একটি বার্তা দেখায় -->
                <form onsubmit="alert('আপনার আবেদন সফলভাবে জমা দেওয়া হয়েছে। কর্তৃপক্ষ শীঘ্রই আপনার সাথে যোগাযোগ করবেন। (Your application has been successfully submitted. The authorities will contact you soon.)'); return false;" class="space-y-6">
                    
                    <!-- কোন শ্রেণিতে ভর্তি হতে ইচ্ছুক (Class) -->
                    <div>
                        <label for="class_seeking" class="block text-sm font-extrabold mb-1 italic">কোন শ্রেণিতে ভর্তি হতে ইচ্ছুক (Class Seeking Admission)</label>
                        <select id="class_seeking" name="class_seeking" class="w-full px-4 py-3 rounded-lg border form-input focus:ring-1" required>
                            <option value="" disabled selected>-- একটি শ্রেণি নির্বাচন করুন (Select a Class) --</option>
                            <option value="Play">প্লে গ্রুপ (Play Group)</option>
                            <option value="Nursery">নার্সারি (Nursery)</option>
                            <option value="KG">কেজি (KG)</option>
                            <option value="Class1">১ম শ্রেণি (Class 1)</option>
                            <option value="Class2">২য় শ্রেণি (Class 2)</option>
                            <option value="Class3">৩য় শ্রেণি (Class 3)</option>
                            <option value="Class4">৪র্থ শ্রেণি (Class 4)</option>
                            <option value="Class5">৫ম শ্রেণি (Class 5)</option>
                            <option value="Class6">৬ষ্ঠ শ্রেণি (Class 6)</option>
                            <option value="Class7">৭ম শ্রেণি (Class 7)</option>
                            <option value="Class8">৮ম শ্রেণি (Class 8)</option>
                            <option value="Class9">৯ম শ্রেণি (Class 9)</option>
                        </select>
                    </div>

                    <!-- নাম (Name) -->
                    <div>
                        <label for="student_name" class="block text-sm font-extrabold mb-1 italic">শিক্ষার্থীর নাম (Student's Name)</label>
                        <input type="text" id="student_name" name="student_name" class="w-full px-4 py-3 rounded-lg border form-input focus:ring-1" required>
                    </div>

                    <!-- ঠিকানা (Address) -->
                    <div>
                        <label for="address" class="block text-sm font-extrabold mb-1 italic">ঠিকানা (Address)</label>
                        <input type="text" id="address" name="address" class="w-full px-4 py-3 rounded-lg border form-input focus:ring-1" required>
                    </div>
                    
                    <!-- বাবার নাম (Father's Name) -->
                    <div>
                        <label for="father_name" class="block text-sm font-extrabold mb-1 italic">বাবার নাম (Father's Name)</label>
                        <input type="text" id="father_name" name="father_name" class="w-full px-4 py-3 rounded-lg border form-input focus:ring-1" required>
                    </div>

                    <!-- মায়ের নাম (Mother's Name) -->
                    <div>
                        <label for="mother_name" class="block text-sm font-extrabold mb-1 italic">মায়ের নাম (Mother's Name)</label>
                        <input type="text" id="mother_name" name="mother_name" class="w-full px-4 py-3 rounded-lg border form-input focus:ring-1" required>
                    </div>

                    <!-- জন্মতারিখ (Date of Birth) -->
                    <div>
                        <label for="dob" class="block text-sm font-extrabold mb-1 italic">জন্মতারিখ (Date of Birth)</label>
                        <input type="date" id="dob" name="dob" class="w-full px-4 py-3 rounded-lg border form-input focus:ring-1" required>
                    </div>

                    <!-- রক্তের গ্রুপ (Blood Group) -->
                    <div>
                        <label for="blood_group" class="block text-sm font-extrabold mb-1 italic">রক্তের গ্রুপ (Blood Group)</label>
                        <select id="blood_group" name="blood_group" class="w-full px-4 py-3 rounded-lg border form-input focus:ring-1" required>
                            <option value="" disabled selected>-- নির্বাচন করুন (Select) --</option>
                            <option value="A+">A+ (এ পজিটিভ)</option>
                            <option value="A-">A- (এ নেগেটিভ)</option>
                            <option value="B+">B+ (বি পজিটিভ)</option>
                            <option value="B-">B- (বি নেগেটিভ)</option>
                            <option value="AB+">AB+ (এবি পজিটিভ)</option>
                            <option value="AB-">AB- (এবি নেগেটিভ)</option>
                            <option value="O+">O+ (ও পজিটিভ)</option>
                            <option value="O-">O- (ও নেগেটিভ)</option>
                        </select>
                    </div>

                    <!-- ধর্ম (Religion) -->
                    <div>
                        <label for="religion" class="block text-sm font-extrabold mb-1 italic">ধর্ম (Religion)</label>
                        <input type="text" id="religion" name="religion" class="w-full px-4 py-3 rounded-lg border form-input focus:ring-1" required>
                    </div>

                    <!-- জন্ম নিবন্ধন নাম্বার (Birth Registration Number) -->
                    <div>
                        <label for="birth_reg" class="block text-sm font-extrabold mb-1 italic">জন্ম নিবন্ধন নাম্বার (Birth Registration Number)</label>
                        <input type="text" id="birth_reg" name="birth_reg" class="w-full px-4 py-3 rounded-lg border form-input focus:ring-1" required>
                    </div>

                    <!-- বর্তমানে অধ্যয়নরত বিদ্যালয়ের নাম (Current School Name) -->
                    <div>
                        <label for="current_school" class="block text-sm font-extrabold mb-1 italic">বর্তমানে অধ্যয়নরত বিদ্যালয়ের নাম (Name of Current School)</label>
                        <input type="text" id="current_school" name="current_school" class="w-full px-4 py-3 rounded-lg border form-input focus:ring-1" placeholder="প্রযোজ্য না হলে 'N/A' লিখুন (Write 'N/A' if not applicable)" required>
                    </div>
                    
                    <!-- সাবমিট বাটন -->
                    <button type="submit" class="w-full py-3 mt-6 text-xl font-extrabold rounded-full text-white primary-green-bg primary-green-hover transition duration-300 shadow-lg transform hover:scale-[1.01] italic">
                        আবেদন জমা দিন (Submit Application)
                    </button>
                </form>
            </div>
        </section>

        <!-- ==================================== ৯. যোগাযোগ সেকশন (Contact) ==================================== -->
        <section id="contact" class="page-content dark-section-bg p-8 sm:p-12 rounded-xl shadow-2xl">
            <h2 class="text-4xl font-extrabold text-center mb-10 text-yellow-300 italic">যোগাযোগ (Contact Us)</h2>
            <div class="bg-gray-800 p-8 rounded-xl shadow-2xl border-l-4 border-primary-green text-gray-200 italic max-w-xl mx-auto">
                <div class="space-y-4 text-lg">
                    <p class="font-extrabold italic text-primary-green">স্কুলের অবস্থান (Location):</p>
                    <p class="ml-4 italic">Ribor, Barodi, Sonargaon, Narayanganj</p>
                </div>

                <div class="space-y-4 text-lg mt-6 border-t border-gray-700 pt-4">
                    <p class="font-extrabold italic text-primary-green">মোবাইল নাম্বার (Mobile Numbers):</p>
                    <p class="ml-4 italic text-white">০১৯৮১৮৩৯১৩২</p>
                    <p class="ml-4 italic text-white">০১৮৮৩০০৪২৩০</p>
                </div>
                
                <div class="space-y-4 text-lg mt-6 border-t border-gray-700 pt-4">
                    <p class="font-extrabold italic text-primary-green">ইমেইল (Email):</p>
                    <p class="ml-4 italic text-white">greenfieldpublicschool@gmail.com</p>
                </div>

                <div class="space-y-4 text-lg mt-6 border-t border-gray-700 pt-4">
                    <p class="font-extrabold italic text-primary-green">ফেইসবুক পেইজ (Facebook Page):</p>
                    <p class="ml-4 italic text-white">Greenfield Public School</p>
                </div>
            </div>
        </section>
        
    </main>

    <!-- ফুটার (Footer) -->
    <footer class="bg-gray-900 text-white py-8 border-t border-primary-green">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-center text-gray-400 italic">
            <p class="text-sm mb-2 italic">© ২০২৫ Greenfield Public School. সর্বস্বত্ব সংরক্ষিত।</p>
            <p class="text-xs italic">স্থান: Ribor, Barodi, Sonargaon, Narayanganj</p>
        </div>
    </footer>

</body>
</html>

