!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>منصتي</title>
<style>
body { font-family: Arial, sans-serif; padding: 20px; }
input, button { display: block; margin: 10px 0; padding: 8px; width: 100%; max-width: 300px; }
h2 { margin-top: 30px; }
#message { color: green; }
#error { color: red; }
</style>
</head>
<body>

<h1>منصة تجريبية</h1>

<h2>تسجيل مستخدم جديد</h2>
<input type="email" id="regEmail" placeholder="الإيميل">
<input type="password" id="regPassword" placeholder="كلمة المرور">
<button onclick="register()">تسجيل</button>

<h2>تسجيل دخول</h2>
<input type="email" id="loginEmail" placeholder="الإيميل">
<input type="password" id="loginPassword" placeholder="كلمة المرور">
<button onclick="login()">دخول</button>

<h2>إعادة تعيين كلمة المرور</h2>
<input type="email" id="resetEmail" placeholder="الإيميل">
<button onclick="resetPassword()">إرسال رابط إعادة التعيين</button>

<h2>لوحة الإدارة</h2>
<button onclick="goAdmin()">فتح لوحة الإدارة</button>

<p id="message"></p>
<p id="error"></p>

<script>
const baseURL = "https://YOUR-GLITCH-PROJECT.glitch.me"; // عدّل هذا إلى رابط مشروعك

function setMessage(msg){ document.getElementById("message").innerText = msg; document.getElementById("error").innerText = ""; }
function setError(msg){ document.getElementById("error").innerText = msg; document.getElementById("message").innerText = ""; }

async function register(){
  const email = document.getElementById("regEmail").value;
  const password = document.getElementById("regPassword").value;
  try {
    const res = await fetch(baseURL+"/register", {
      method:"POST",
      headers: {"Content-Type":"application/json"},
      body: JSON.stringify({email,password})
    });
    const data = await res.json();
    if(res.ok) setMessage(data.message);
    else setError(data.error);
  } catch(err){ setError(err.message); }
}

async function login(){
  const email = document.getElementById("loginEmail").value;
  const password = document.getElementById("loginPassword").value;
  try {
    const res = await fetch(baseURL+"/login", {
      method:"POST",
      headers: {"Content-Type":"application/json"},
      body: JSON.stringify({email,password})
    });
    const data = await res.json();
    if(res.ok) setMessage(data.message);
    else setError(data.error);
  } catch(err){ setError(err.message); }
}

async function resetPassword(){
  const email = document.getElementById("resetEmail").value;
  try {
    const res = await fetch(baseURL+"/reset-password", {
      method:"POST",
      headers: {"Content-Type":"application/json"},
      body: JSON.stringify({email})
    });
    const data = await res.json();
    if(res.ok) setMessage(data.message);
    else setError(data.error);
  } catch(err){ setError(err.message); }
}

function goAdmin(){
  window.open(baseURL+"/admin","_blank");
}
</script>

</body>
</html>

