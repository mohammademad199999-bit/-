<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>إدارة مبيعات جبس باب الآغا - الموصل</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
</head>
<body class="bg-slate-100 font-sans antialiased">
    <div id="app" class="min-h-screen flex flex-col justify-center items-center p-4">
        <div class="max-w-md w-full bg-white rounded-2xl shadow-xl overflow-hidden p-8 border border-slate-200">
            <div class="text-center mb-6">
                <h1 class="text-2xl font-bold text-slate-800">جبس باب الآغا</h1>
                <p class="text-sm text-slate-500 mt-1">لوحة إدارة المبيعات والتوزيع والمخازن • الموصل</p>
            </div>
            
            <div id="login-container">
                <h2 class="text-lg font-semibold text-slate-700 mb-4">تسجيل دخول المدير</h2>
                <form id="login-form" onsubmit="handleLogin(event)" class="space-y-4">
                    <div>
                        <label class="block text-xs font-medium text-slate-600 mb-1">اسم المستخدم</label>
                        <input type="text" id="username" value="admin" required class="w-full px-4 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-600 outline-none">
                    </div>
                    <div>
                        <label class="block text-xs font-medium text-slate-600 mb-1">كلمة المرور</label>
                        <input type="password" id="password" placeholder="أدخل كلمة المرور" required class="w-full px-4 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-600 outline-none">
                    </div>
                    <button type="submit" class="w-full py-3 bg-slate-900 text-white font-medium rounded-lg hover:bg-slate-800 transition">دخول</button>
                </form>
                <div id="error-msg" class="mt-4 p-3 bg-emerald-50 text-emerald-700 text-xs rounded-lg text-center hidden"></div>
            </div>
        </div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
        import { getFirestore, doc, getDoc, setDoc } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-firestore.js";

        const firebaseConfig = {
            apiKey: "AIzaSyDi7x7dCzlyubAbpHxwp1Bjul3QRSiFt8o",
            authDomain: "bab-al-agha-chips-mosul.firebaseapp.com",
            projectId: "bab-al-agha-chips-mosul",
            storageBucket: "bab-al-agha-chips-mosul.firebasestorage.app",
            messagingSenderId: "361029754180",
            appId: "1:361029754180:web:d09375f31c9ef8e5c60b11",
            measurementId: "G-3H6FC8KEC7"
        };

        const app = initializeApp(firebaseConfig);
        const db = getFirestore(app);
        window.db = db;

        window.handleLogin = async function(e) {
            e.preventDefault();
            const user = document.getElementById('username').value.trim();
            const pass = document.getElementById('password').value.trim();
            const msgBox = document.getElementById('error-msg');
            msgBox.classList.remove('hidden');

            if(user === 'admin' && pass === 'admin123') {
                msgBox.className = "mt-4 p-3 bg-emerald-50 text-emerald-700 text-xs rounded-lg text-center";
                msgBox.innerText = "تم تسجيل الدخول بنجاح! جاري الانتقال لوحة التحكم...";
                setTimeout(() => {
                    document.getElementById('app').innerHTML = `
                        <div class="max-w-4xl w-full bg-white rounded-2xl shadow-xl p-8">
                            <h2 class="text-2xl font-bold text-slate-800 mb-2">مرحباً بك يا مدير النظام (باب الآغا)</h2>
                            <p class="text-slate-600 mb-6">تم الاتصال بقاعدة البيانات السحابية بنجاح تام!</p>
                            <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-6">
                                <div class="p-4 bg-blue-50 border border-blue-100 rounded-xl">
                                    <h3 class="font-bold text-blue-900">إجمالي المبيعات</h3>
                                    <p class="text-2xl font-extrabold text-blue-600 mt-2">0 د.ع</p>
                                </div>
                                <div class="p-4 bg-emerald-50 border border-emerald-100 rounded-xl">
                                    <h3 class="font-bold text-emerald-900">السائقون والمندوبون</h3>
                                    <p class="text-2xl font-extrabold text-emerald-600 mt-2">متصل (🟢)</p>
                                </div>
                                <div class="p-4 bg-amber-50 border border-amber-100 rounded-xl">
                                    <h3 class="font-bold text-amber-900">حالة المخزن</h3>
                                    <p class="text-2xl font-extrabold text-amber-600 mt-2">نشط وسحابي</p>
                                </div>
                            </div>
                            <button onclick="location.reload()" class="px-4 py-2 bg-rose-600 text-white rounded-lg text-sm">تسجيل الخروج</button>
                        </div>
                    `;
                }, 1000);
            } else {
                msgBox.className = "mt-4 p-3 bg-rose-50 text-rose-700 text-xs rounded-lg text-center";
                msgBox.innerText = "خطأ في اسم المستخدم أو كلمة المرور (استخدم admin123).";
            }
        }
    </script>
</body>
</html>
