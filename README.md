 <!DOCTYPE html>
<html lang="ka" data-theme="dark">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no" />
    <title>IMEDCalc - სამედიცინო კალკულატორები</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&family=Fira+Sans:wght@400;600;700&display=swap" rel="stylesheet">
    <!-- PWA Support -->
    <link rel="manifest" href="/manifest.json">
    <meta name="theme-color" content="#0f172a">
    <link rel="apple-touch-icon" href="/icon-192x192.png">
    <style>
        :root {
            --bg: #0f172a;
            --card: #1e293b;
            --surface: #334155;
            --muted: #94a3b8;
            --text: #e2e8f0;
            --brand: #22d3ee;
            --brand-2: #818cf8;
            --ok: #22c55e;
            --warn: #f59e0b;
            --err: #ef4444;
            --ring: rgba(34, 211, 238, 0.35);
            --shadow-3: 0 10px 30px rgba(0,0,0,.45), 0 2px 8px rgba(0,0,0,.35);
            --radius-2xl: 1.25rem;
            --transition: all 0.3s ease;
        }

        [data-theme="light"] {
            --bg: #f1f5f9;
            --card: #ffffff;
            --surface: #f8fafc;
            --muted: #64748b;
            --text: #1f2937;
            --brand: #06b6d4;
            --brand-2: #4f46e5;
            --ok: #059669;
            --warn: #d97706;
            --err: #dc2626;
            --ring: rgba(6, 182, 212, 0.25);
            --shadow-3: 0 10px 30px rgba(0,0,0,.1), 0 2px 8px rgba(0,0,0,.05);
        }

        * { box-sizing: border-box; }
        html, body { height: 100%; margin: 0; }
        body {
            font-family: 'Inter', sans-serif;
            background: var(--bg);
            color: var(--text);
            transition: var(--transition);
            line-height: 1.6;
            font-size: 16px;
            overscroll-behavior: none;
        }
        [data-theme="dark"] body {
            background: radial-gradient(80rem 40rem at 10% -10%, rgba(129,140,248,.08), transparent 60%),
                        radial-gradient(70rem 30rem at 110% 10%, rgba(34,211,238,.08), transparent 60%),
                        var(--bg);
        }

        .container { max-width: 1100px; margin: 0 auto; padding: 1.5rem 0.5rem 3rem; }
        header {
            background: var(--card);
            padding: 1rem;
            border-radius: var(--radius-2xl);
            box-shadow: var(--shadow-3);
            display: flex;
            align-items: center;
            gap: 0.5rem;
            justify-content: space-between;
            flex-wrap: wrap;
            border: 1px solid var(--surface);
            transition: var(--transition);
        }
        
        .brand { display: flex; align-items: center; gap: 0.8rem; }
        .logo {
            width: 40px;
            height: 40px;
            border-radius: 12px;
            background: linear-gradient(135deg, var(--brand), var(--brand-2));
            box-shadow: 0 8px 25px rgba(34,211,238,.25);
            display: flex;
            align-items: center;
            justify-content: center;
            overflow: hidden;
            transition: var(--transition);
        }
        [data-theme="light"] .logo {
            box-shadow: 0 8px 25px rgba(6, 182, 212, .2);
        }
        .logo svg {
            width: 90%;
            height: 90%;
            color: var(--card);
        }
        .brand h1 { margin: 0; font-weight: 800; font-size: 1.3rem; letter-spacing: -0.5px; }
        .brand p { margin: 0; color: var(--muted); font-size: 0.85rem; }
        .disclaimer { color: var(--muted); font-size: 0.85rem; margin: 0.75rem 0.5rem; }
        .theme-toggle {
            background: var(--surface);
            color: var(--text);
            border: 1px solid var(--muted);
            border-radius: 999px;
            padding: 0.4rem 0.8rem;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 0.4rem;
            transition: var(--transition);
            touch-action: manipulation;
        }
        .theme-toggle:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 10px rgba(0,0,0,.1);
        }

        .nav-menu {
            display: flex;
            flex-wrap: wrap;
            gap: 0.5rem;
            margin: 1rem 0.5rem;
            justify-content: center;
        }
        .nav-btn {
            background: linear-gradient(135deg, var(--brand), var(--brand-2));
            color: var(--card);
            padding: 0.6rem 1rem;
            border-radius: 0.75rem;
            font-weight: 700;
            cursor: pointer;
            transition: var(--transition);
            box-shadow: 0 8px 20px rgba(34,211,238,.25);
            border: none;
            font-size: 0.9rem;
            touch-action: manipulation;
        }
        .nav-btn:hover {
            transform: translateY(-2px);
            filter: saturate(1.1);
        }

        .grid { display: none; gap: 1rem; margin: 1.5rem 0.5rem; grid-template-columns: 1fr; }
        .grid.active { display: grid; animation: fadeIn 0.5s ease; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

        .card {
            background: var(--card);
            border: 1px solid var(--surface);
            border-radius: var(--radius-2xl);
            padding: 1rem;
            box-shadow: var(--shadow-3);
            transition: var(--transition);
        }
        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 40px rgba(0,0,0,0.55), 0 5px 15px rgba(0,0,0,0.45);
        }
        [data-theme="light"] .card:hover {
            box-shadow: 0 15px 40px rgba(0,0,0,.15), 0 5px 15px rgba(0,0,0,.1);
        }

        .card h2 { margin: 0 0 0.75rem; font-size: 1.15rem; font-weight: 800; }
        .formula {
            font-family: 'Fira Sans', monospace;
            font-size: 0.9rem;
            color: var(--brand);
            padding: 0.5rem 0;
            border-bottom: 1px dashed var(--surface);
            margin-bottom: 0.75rem;
            word-wrap: break-word;
        }
        .muted { color: var(--muted); font-size: 0.85rem; }
        .row { display: grid; gap: 0.75rem; grid-template-columns: 1fr; }
        
        label { display: block; font-size: 0.85rem; margin-bottom: 0.2rem; color: var(--text); }
        input, select {
            width: 100%;
            padding: 0.75rem;
            background: var(--surface);
            color: var(--text);
            border: 1px solid var(--muted);
            border-radius: 0.75rem;
            outline: none;
            transition: var(--transition);
            font-size: 0.9rem;
            min-height: 44px;
        }
        input:focus, select:focus { border-color: var(--brand); box-shadow: 0 0 0 4px var(--ring); }
        .btns { display: flex; gap: 0.5rem; margin-top: 1rem; flex-wrap: wrap; }
        button {
            padding: 0.75rem 1rem;
            border: none;
            border-radius: 0.75rem;
            font-weight: 700;
            cursor: pointer;
            transition: var(--transition);
            background: linear-gradient(135deg, var(--brand), var(--brand-2));
            color: var(--card);
            box-shadow: 0 8px 20px rgba(34,211,238,.25);
            font-size: 0.9rem;
            min-height: 44px;
            touch-action: manipulation;
        }
        button:hover { transform: translateY(-2px); filter: saturate(1.1); }
        .ghost {
            background: var(--surface);
            color: var(--text);
            border: 1px solid var(--muted);
            box-shadow: none;
        }
        .result {
            margin-top: 1rem;
            padding: 0.75rem 1rem;
            border-radius: 0.75rem;
            background: var(--surface);
            border: 1px dashed var(--brand-2);
            font-weight: 700;
            letter-spacing: 0.3px;
            transition: var(--transition);
            font-size: 0.9rem;
        }
        .note { margin-top: 0.75rem; padding: 0.75rem; border-left: 4px solid var(--warn); background: rgba(245, 158, 11, .1); border-radius: 0.5rem; font-size: 0.85rem; }
        .success { border-left-color: var(--ok); background: rgba(34, 197, 94, .1); }
        .danger { border-left-color: var(--err); background: rgba(239, 68, 68, .1); }
        .foot { margin-top: 1.5rem; color: var(--muted); font-size: 0.8rem; text-align: center; }
        .tag, .chip {
            display: inline-block;
            font-size: 0.75rem;
            padding: 0.25rem 0.6rem;
            border-radius: 999px;
            background: var(--surface);
            border: 1px solid var(--muted);
            margin-left: 0.5rem;
            color: var(--text);
        }
        .chip { background: rgba(34,211,238,.12); border-color: rgba(34,211,238,.25); color: #a5f3fc; }
        [data-theme="light"] .chip { background: rgba(6, 182, 212, .1); border-color: rgba(6, 182, 212, .25); color: #0891b2; }

        .recommendations {
            margin-top: 1rem;
            padding: 0.75rem;
            background: var(--surface);
            border-radius: 0.75rem;
            border: 1px solid var(--muted);
        }
        .recommendations table {
            width: 100%;
            border-collapse: collapse;
        }
        .recommendations th, .recommendations td {
            padding: 0.5rem;
            border: 1px solid var(--muted);
            text-align: left;
            font-size: 0.85rem;
        }
        .recommendations th {
            background: var(--brand-2);
            color: var(--card);
        }

        @media (max-width: 600px) {
            body { font-size: 15px; }
            .container { padding: 1rem 0.5rem 2rem; }
            header { padding: 0.75rem; flex-direction: column; align-items: flex-start; }
            .logo { width: 36px; height: 36px; }
            .brand h1 { font-size: 1.1rem; }
            .brand p { font-size: 0.8rem; }
            .theme-toggle { padding: 0.4rem 0.8rem; font-size: 0.85rem; }
            .nav-menu { gap: 0.5rem; margin: 0.75rem 0.5rem; }
            .nav-btn { padding: 0.6rem 0.8rem; font-size: 0.85rem; }
            .grid { gap: 0.75rem; margin: 1rem 0.5rem; }
            .card { padding: 0.75rem; }
            .card h2 { font-size: 1rem; }
            .formula { font-size: 0.85rem; }
            .btns button { padding: 0.6rem 0.8rem; font-size: 0.85rem; }
            .result { padding: 0.6rem 0.8rem; font-size: 0.85rem; }
            
            .recommendations table { display: block; }
            .recommendations thead { display: none; }
            .recommendations tbody, .recommendations tr { display: block; }
            .recommendations td {
                display: block;
                text-align: left;
                padding: 0.5rem;
                position: relative;
                padding-left: 40%;
                border: none;
                border-bottom: 1px solid var(--muted);
            }
            .recommendations td:before {
                content: attr(data-label);
                position: absolute;
                left: 0.5rem;
                width: 35%;
                font-weight: 700;
                color: var(--brand);
            }
            .recommendations tr { margin-bottom: 0.75rem; border: 1px solid var(--muted); border-radius: 0.5rem; }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <div class="brand">
                <div class="logo">
                    <svg width="250" height="270" viewBox="0 0 250 270" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <path fill-rule="evenodd" clip-rule="evenodd" d="M112.551 2.39243C116.516 -0.198274 121.731 -0.198274 125.696 2.39243L237.525 69.5772C241.49 72.1679 243.896 76.5332 243.896 81.2829V206.511C243.896 211.261 241.49 215.626 237.525 218.217L125.696 285.402C121.731 287.992 116.516 287.992 112.551 285.402L0.721497 218.217C-3.24357 215.626 -5.64923 211.261 -5.64923 206.511V81.2829C-5.64923 76.5332 -3.24357 72.1679 0.721497 69.5772L112.551 2.39243Z" fill="#141846"/>
                        <path fill-rule="evenodd" clip-rule="evenodd" d="M125.696 2.39243C121.731 -0.198274 116.516 -0.198274 112.551 2.39243L0.721497 69.5772C-3.24357 72.1679 -5.64923 76.5332 -5.64923 81.2829V206.511C-5.64923 211.261 -3.24357 215.626 0.721497 218.217L112.551 285.402C116.516 287.992 121.731 287.992 125.696 285.402L237.525 218.217C241.49 215.626 243.896 211.261 243.896 206.511V81.2829C243.896 76.5332 241.49 72.1679 237.525 69.5772L125.696 2.39243Z" fill="url(#paint0_linear_85_16)"/>
                        <rect x="120.304" y="143.208" width="121.848" height="126.31" fill="#FFFFFF"/>
                        <path d="M172.96 161.432V167.315H176.657V161.432H172.96ZM168.125 186.745C168.125 187.359 168.614 187.848 169.229 187.848H179.916C180.531 187.848 181.02 187.359 181.02 186.745V173.203H168.125V186.745Z" fill="#141846"/>
                        <path d="M129.894 152.028V157.912H133.591V152.028H129.894Z" fill="#141846"/>
                        <path d="M129.894 167.315V173.199H133.591V167.315H129.894Z" fill="#141846"/>
                        <path d="M129.894 182.603V188.487H133.591V182.603H129.894Z" fill="#141846"/>
                        <path d="M129.894 197.89V203.774H133.591V197.89H129.894Z" fill="#141846"/>
                        <path d="M129.894 213.178V219.062H133.591V213.178H129.894Z" fill="#141846"/>
                        <path d="M129.894 228.465V234.349H133.591V228.465H129.894Z" fill="#141846"/>
                        <path d="M129.894 243.753V249.637H133.591V243.753H129.894Z" fill="#141846"/>
                        <path d="M129.894 259.041V264.925H133.591V259.041H129.894Z" fill="#141846"/>
                        <path d="M137.601 264.925V259.041H141.298V264.925H137.601Z" fill="#141846"/>
                        <path d="M145.308 264.925V259.041H149.005V264.925H145.308Z" fill="#141846"/>
                        <path d="M153.015 264.925V259.041H156.712V264.925H153.015Z" fill="#141846"/>
                        <path d="M160.723 264.925V259.041H164.42V264.925H160.723Z" fill="#141846"/>
                        <path d="M168.43 264.925V259.041H172.127V264.925H168.43Z" fill="#141846"/>
                        <path d="M176.137 264.925V259.041H179.834V264.925H176.137Z" fill="#141846"/>
                        <path d="M183.844 264.925V259.041H187.541V264.925H183.844Z" fill="#141846"/>
                        <path d="M191.551 264.925V259.041H195.248V264.925H191.551Z" fill="#141846"/>
                        <path d="M199.258 264.925V259.041H202.955V264.925H199.258Z" fill="#141846"/>
                        <path d="M206.966 264.925V259.041H210.663V264.925H206.966Z" fill="#141846"/>
                        <path d="M214.673 264.925V259.041H218.37V264.925H214.673Z" fill="#141846"/>
                        <path d="M129.894 136.74V142.624H133.591V136.74H129.894Z" fill="#141846"/>
                        <path d="M129.894 121.452V127.336H133.591V121.452H129.894Z" fill="#141846"/>
                        <path d="M129.894 106.164V112.048H133.591V106.164H129.894Z" fill="#141846"/>
                        <path d="M129.894 90.876V96.7601H133.591V90.876H129.894Z" fill="#141846"/>
                        <path d="M129.894 75.5878V81.4719H133.591V75.5878H129.894Z" fill="#141846"/>
                        <path d="M129.894 60.3005V66.1846H133.591V60.3005H129.894Z" fill="#141846"/>
                        <path d="M129.894 45.0132V50.8973H133.591V45.0132H129.894Z" fill="#141846"/>
                        <path d="M129.894 29.7259V35.61H133.591V29.7259H129.894Z" fill="#141846"/>
                        <path d="M129.894 14.4386V20.3227H133.591V14.4386H129.894Z" fill="#141846"/>
                        <path d="M137.601 20.3227V14.4386H141.298V20.3227H137.601Z" fill="#141846"/>
                        <path d="M145.308 20.3227V14.4386H149.005V20.3227H145.308Z" fill="#141846"/>
                        <path d="M153.015 20.3227V14.4386H156.712V20.3227H153.015Z" fill="#141846"/>
                        <path d="M160.723 20.3227V14.4386H164.42V20.3227H160.723Z" fill="#141846"/>
                        <path d="M168.43 20.3227V14.4386H172.127V20.3227H168.43Z" fill="#141846"/>
                        <path d="M176.137 20.3227V14.4386H179.834V20.3227H176.137Z" fill="#141846"/>
                        <path d="M183.844 20.3227V14.4386H187.541V20.3227H183.844Z" fill="#141846"/>
                        <path d="M191.551 20.3227V14.4386H195.248V20.3227H191.551Z" fill="#141846"/>
                        <path d="M199.258 20.3227V14.4386H202.955V20.3227H199.258Z" fill="#141846"/>
                        <path d="M206.966 20.3227V14.4386H210.663V20.3227H206.966Z" fill="#141846"/>
                        <path d="M214.673 20.3227V14.4386H218.37V20.3227H214.673Z" fill="#141846"/>
                    </svg>
                </div>
                <div>
                    <!-- რეგისტრაცია / შესვლა -->
<div class="auth-container" id="auth-container">
  <h2>შესვლა ან რეგისტრაცია</h2>
  
  <form id="register-form">
    <h3>რეგისტრაცია</h3>
    <input type="text" id="reg-username" placeholder="მომხმარებლის სახელი" required>
    <input type="email" id="reg-email" placeholder="ელ. ფოსტა" required>
    <input type="password" id="reg-password" placeholder="პაროლი" required>
    <button type="submit">რეგისტრაცია</button>
  </form>

  <form id="login-form">
    <h3>შესვლა</h3>
    <input type="email" id="login-email" placeholder="ელ. ფოსტა" required>
    <input type="password" id="login-password" placeholder="პაროლი" required>
    <button type="submit">შესვლა</button>
  </form>
  
  <p id="auth-message"></p>
</div>

<script>
// რეგისტრაცია
document.getElementById("register-form").addEventListener("submit", function(e) {
  e.preventDefault();
  const username = document.getElementById("reg-username").value;
  const email = document.getElementById("reg-email").value;
  const password = document.getElementById("reg-password").value;

  if(localStorage.getItem(email)){
    document.getElementById("auth-message").innerText = "ასეთი ელ.ფოსტა უკვე არსებობს!";
  } else {
    localStorage.setItem(email, JSON.stringify({username, password}));
    document.getElementById("auth-message").innerText = "რეგისტრაცია წარმატებით დასრულდა!";
  }
});

// შესვლა
document.getElementById("login-form").addEventListener("submit", function(e) {
  e.preventDefault();
  const email = document.getElementById("login-email").value;
  const password = document.getElementById("login-password").value;

  const user = JSON.parse(localStorage.getItem(email));
  if(user && user.password === password){
    document.getElementById("auth-message").innerText = "მოგესალმები, " + user.username + "!";
    localStorage.setItem("loggedInUser", user.username);
  } else {
    document.getElementById("auth-message").innerText = "არასწორი მონაცემებია!";
  }
});
</script>

<style>
.auth-container {
  max-width: 400px;
  margin: 20px auto;
  padding: 20px;
  background: #f9f9f9;
  border-radius: 12px;
  box-shadow: 0 2px 6px rgba(0,0,0,0.15);
}
.auth-container h2, .auth-container h3 {
  text-align: center;
}
.auth-container form {
  margin-bottom: 20px;
}
.auth-container input {
  display: block;
  width: 100%;
  margin: 8px 0;
  padding: 10px;
  border-radius: 8px;
  border: 1px solid #ccc;
}
.auth-container button {
  width: 100%;
  padding: 10px;
  border: none;
  border-radius: 8px;
  background: #0077cc;
  color: #fff;
  font-size: 16px;
  cursor: pointer;
}
.auth-container button:hover {
  background: #005fa3;
}
#auth-message {
  text-align: center;
  font-weight: bold;
  margin-top: 10px;
}
</style>
                    <h1>IMEDCalc</h1>
                    <p>სამედიცინო კალკულატორები</p>
                </div>
            </div>
            <button class="theme-toggle" onclick="toggleTheme()">
                <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="theme-icon"><path d="M12 2a10 10 0 1 0 10 10A10 10 0 0 0 12 2Z"/></svg>
                <span id="theme-text">ღია თემა</span>
            </button>
        </header>
        <p class="disclaimer">დამხმარე ხელსაწყო. სავალდებულოა შედეგების გადამოწმება კლინიკურ პროტოკოლებთან.</p>
        <div class="nav-menu">
            <button class="nav-btn" onclick="showCalculator('bicarb-card')">სოდა ბუფერი</button>
            <button class="nav-btn" onclick="showCalculator('potassium-card')">კალიუმის გადასხმა</button>
            <button class="nav-btn" onclick="showCalculator('kcoef-card')">K კოეფიციენტი</button>
            <button class="nav-btn" onclick="showCalculator('solu-card')">სოლუმედროლი</button>
            <button class="nav-btn" onclick="showCalculator('crcl-card')">კრეატინინის კლირენსი</button>
        </div>
        <div class="grid" id="grid">
            <section class="card" id="bicarb-card">
                <h2>სოდა ბუფერი — გადასხმის გამოთვლა <span class="tag">ფორმულა</span></h2>
                <div class="formula">წონა × BE(act) × 2 × 0.3</div>
                <p class="muted">შეიყვანეთ პაციენტის მონაცემები. შედეგი გამოისახება ქვემოთ.</p>
                <div class="row">
                    <div>
                        <label for="bicarb-weight">პაციენტის წონა (კგ)</label>
                        <input id="bicarb-weight" type="number" min="0" step="0.1" placeholder="მაგ. 70" />
                    </div>
                    <div>
                        <label for="bicarb-be">BE(act)</label>
                        <input id="bicarb-be" type="number" step="0.1" placeholder="მაგ. -8" />
                    </div>
                </div>
                <div class="btns">
                    <button onclick="calcBicarb()">გამოთვლა</button>
                    <button class="ghost" onclick="resetCard('bicarb-card')">გასუფთავება</button>
                    <button class="ghost" onclick="copyResult('bicarb-result')">კოპირება</button>
                </div>
                <div id="bicarb-result" class="result" aria-live="polite">შედეგი: —</div>
                <div class="note">შენიშვნა: ერთეულების ინტერპრეტაცია შეადარეთ თქვენს პროტოკოლს/ხსნარის კონცენტრაციას.</div>
            </section>
            <section class="card" id="potassium-card">
                <h2>კალიუმის გადასხმა <span class="chip">ნელა გადასხმა</span></h2>
                <div class="formula">წონა × 1.74 ÷ კალიუმის მაჩვენებელი</div>
                <p class="muted">ფორმულა ითვლის საჭირო ოდენობას მითითებული დონის შესაბამისად.</p>
                <div class="row">
                    <div>
                        <label for="k-weight">პაციენტის წონა (კგ)</label>
                        <input id="k-weight" type="number" min="0" step="0.1" placeholder="მაგ. 70" />
                    </div>
                    <div>
                        <label for="k-level">კალიუმის მაჩვენებელი (mmol/L)</label>
                        <input id="k-level" type="number" min="0.1" step="0.1" placeholder="მაგ. 3.0" />
                    </div>
                </div>
                <div class="btns">
                    <button onclick="calcPotassium()">გამოთვლა</button>
                    <button class="ghost" onclick="resetCard('potassium-card')">გასუფთავება</button>
                    <button class="ghost" onclick="copyResult('potassium-result')">კოპირება</button>
                </div>
                <div id="potassium-result" class="result" aria-live="polite">შედეგი: —</div>
                <div class="note success">აუცილებლად <strong>ნელა</strong> გადაისხას ინსტიტუციური წესების შესაბამისად.</div>
            </section>
            <section class="card" id="kcoef-card">
                <h2>K კოეფიციენტი</h2>
                <div class="formula">მედიკამენტის მილიგრამი × 1000 ÷ ხსნარის რაოდენობა</div>
                <p class="muted">შედეგი პრაქტიკულად უდრის კონცენტრაციას <em>(მკგ/მლ)</em>, თუ მოცულობა შეყვანილია მლ-ში.</p>
                <div class="row">
                    <div>
                        <label for="kcoef-mg">მედიკამენტის რაოდენობა (mg)</label>
                        <input id="kcoef-mg" type="number" min="0" step="0.1" placeholder="მაგ. 500" />
                    </div>
                    <div>
                        <label for="kcoef-vol">ხსნარის რაოდენობა (მლ)</label>
                        <input id="kcoef-vol" type="number" min="0.1" step="0.1" placeholder="მაგ. 100" />
                    </div>
                </div>
                <div class="btns">
                    <button onclick="calcKcoef()">გამოთვლა</button>
                    <button class="ghost" onclick="resetCard('kcoef-card')">გასუფთავება</button>
                    <button class="ghost" onclick="copyResult('kcoef-result')">კოპირება</button>
                </div>
                <div id="kcoef-result" class="result" aria-live="polite">შედეგი: —</div>
            </section>
            <section class="card" id="solu-card">
                <h2>სოლუმედროლი — დამრტყმელი დოზა</h2>
                <div class="formula">30 mg/kg — გადასხმა 15 წუთში</div>
                <p class="muted">შეიყვანეთ მხოლოდ პაციენტის წონა. სისტემა გამოთვლის დოზას.</p>
                <div class="row">
                    <div>
                        <label for="solu-weight">პაციენტის წონა (კგ)</label>
                        <input id="solu-weight" type="number" min="0" step="0.1" placeholder="მაგ. 70" />
                    </div>
                </div>
                <div class="btns">
                    <button onclick="calcSolu()">გამოთვლა</button>
                    <button class="ghost" onclick="resetCard('solu-card')">გასუფთავება</button>
                    <button class="ghost" onclick="copyResult('solu-result')">კოპირება</button>
                </div>
                <div id="solu-result" class="result" aria-live="polite">შედეგი: —</div>
                <div class="note success">რეკომენდაცია: პამპი დააყენეთ <strong>200 მლ/სთ</strong>-ზე. გადასხმა უნდა დასრულდეს ~15 წუთში.</div>
            </section>
            <section class="card" id="crcl-card">
                <h2>კრეატინინის კლირენსი (CrCl)</h2>
                <div class="formula">[140 − ასაკი (წელი)] × წონა (კგ) × (0.85 თუ ქალი) ÷ (72 × სერუმის კრეატინინი, mg/dL)</div>
                <p class="muted">შეიყვანეთ პაციენტის მონაცემები. შედეგი გამოისახება ქვემოთ, ანტიბიოტიკების დოზირების რეკომენდაციებით.</p>
                <div class="row">
                    <div>
                        <label for="crcl-age">ასაკი (წელი)</label>
                        <input id="crcl-age" type="number" min="0" step="1" placeholder="მაგ. 60" />
                    </div>
                    <div>
                        <label for="crcl-weight">წონა (კგ)</label>
                        <input id="crcl-weight" type="number" min="0" step="0.1" placeholder="მაგ. 70" />
                    </div>
                    <div>
                        <label for="crcl-gender">სქესი</label>
                        <select id="crcl-gender">
                            <option value="male">მამრობითი</option>
                            <option value="female">მდედრობითი</option>
                        </select>
                    </div>
                    <div>
                        <label for="crcl-creatinine">სერუმის კრეატინინი</label>
                        <input id="crcl-creatinine" type="number" min="0.1" step="0.01" placeholder="მაგ. 1.2 (mg/dL) ან 106 (µmol/L)" />
                    </div>
                    <div>
                        <label for="crcl-unit">ერთეული</label>
                        <select id="crcl-unit">
                            <option value="mg/dL">mg/dL</option>
                            <option value="µmol/L">µmol/L</option>
                        </select>
                    </div>
                </div>
                <div class="btns">
                    <button onclick="calcCrCl()">გამოთვლა</button>
                    <button class="ghost" onclick="resetCard('crcl-card')">გასუფთავება</button>
                    <button class="ghost" onclick="copyResult('crcl-result')">კოპირება</button>
                </div>
                <div id="crcl-result" class="result" aria-live="polite">შედეგი: —</div>
                <div id="crcl-recommendations" class="recommendations" style="display: none;">
                    <h3>ანტიბიოტიკების დოზირების რეკომენდაციები</h3>
                    <table>
                        <thead>
                            <tr>
                                <th>ანტიბიოტიკი</th>
                                <th>CrCl (მლ/წთ)</th>
                                <th>დოზა</th>
                                <th>სიხშირე</th>
                            </tr>
                        </thead>
                        <tbody id="crcl-rec-table-body"></tbody>
                    </table>
                    <p class="muted">შენიშვნა: ეს არის ზოგადი რეკომენდაციები. გადაამოწმეთ კლინიკურ პროტოკოლებთან და პაციენტის მდგომარეობასთან.</p>
                </div>
            </section>
        </div>
        <p class="foot">© 2025 IMEDCalc • შექმნილია სამედიცინო პერსონალისთვის</p>
    </div>

    <script>
        // Theme management
        function toggleTheme() {
            const body = document.body;
            const themeText = document.getElementById('theme-text');
            const currentTheme = body.getAttribute('data-theme');
            let newTheme = currentTheme === 'dark' ? 'light' : 'dark';
            body.setAttribute('data-theme', newTheme);
            themeText.textContent = newTheme === 'dark' ? 'ღია თემა' : 'მუქი თემა';
            localStorage.setItem('theme', newTheme);
        }

        function applyTheme() {
            const savedTheme = localStorage.getItem('theme') || 'dark';
            const body = document.body;
            body.setAttribute('data-theme', savedTheme);
            const themeText = document.getElementById('theme-text');
            if (themeText) {
                themeText.textContent = savedTheme === 'dark' ? 'ღია თემა' : 'მუქი თემა';
            }
        }
        document.addEventListener('DOMContentLoaded', applyTheme);

        // PWA Service Worker Registration with Error Handling
        if ('serviceWorker' in navigator) {
            window.addEventListener('load', () => {
                navigator.serviceWorker.register('/sw.js', { scope: '/' })
                    .then(reg => {
                        console.log('Service Worker რეგისტრირებულია წარმატებით:', reg);
                    })
                    .catch(err => {
                        console.error('Service Worker-ის რეგისტრაცია ვერ მოხერხდა:', err);
                        toast('Service Worker-ის რეგისტრაცია ვერ განხორციელდა. გთხოვთ, გამოიყენოთ HTTPS ან localhost.');
                    });
            });
        } else {
            console.warn('Service Worker არ არის მხარდაჭერილი ამ ბრაუზერში.');
            toast('ბრაუზერი არ უჭერს მხარს Service Worker-ს.');
        }

        // Show specific calculator
        function showCalculator(cardId) {
            const cards = document.querySelectorAll('.card');
            cards.forEach(card => {
                card.style.display = 'none';
            });
            const selectedCard = document.getElementById(cardId);
            if (selectedCard) {
                selectedCard.style.display = 'block';
            }
            const grid = document.getElementById('grid');
            grid.classList.add('active');
        }

        // Core calculator functions
        const fmt = (n) => {
            if (isNaN(n) || !isFinite(n)) return "—";
            const abs = Math.abs(n);
            if (abs >= 1000) return n.toLocaleString(undefined, { maximumFractionDigits: 0 });
            if (abs >= 100) return n.toLocaleString(undefined, { maximumFractionDigits: 1 });
            return n.toLocaleString(undefined, { maximumFractionDigits: 2 });
        };
        
        function setResult(id, value, unitHint = '') {
            const el = document.getElementById(id);
            el.textContent = `შედეგი: ${fmt(value)} ${unitHint}`.trim();
        }
        
        function requireValidNumber(...vals) {
            return vals.every(v => typeof v === 'number' && isFinite(v));
        }

        function calcBicarb() {
            const w = parseFloat(document.getElementById('bicarb-weight').value);
            const be = parseFloat(document.getElementById('bicarb-be').value);
            if (!requireValidNumber(w, be)) { setResult('bicarb-result', NaN); return; }
            const dose = w * Math.abs(be) * 2 * 0.3;
            setResult('bicarb-result', dose, '(მლ.)');
        }

        function calcPotassium() {
            const w = parseFloat(document.getElementById('k-weight').value);
            const lvl = parseFloat(document.getElementById('k-level').value);
            if (!requireValidNumber(w, lvl) || lvl <= 0) { setResult('potassium-result', NaN); return; }
            const amount = (w * 1.74) / lvl;
            setResult('potassium-result', amount, '(მლ.)');
        }

        function calcKcoef() {
            const mg = parseFloat(document.getElementById('kcoef-mg').value);
            const vol = parseFloat(document.getElementById('kcoef-vol').value);
            if (!requireValidNumber(mg, vol) || vol <= 0) { setResult('kcoef-result', NaN); return; }
            const k = (mg * 1000) / vol;
            setResult('kcoef-result', k, 'მკგ/მლ');
        }

        function calcSolu() {
            const w = parseFloat(document.getElementById('solu-weight').value);
            if (!requireValidNumber(w)) { setResult('solu-result', NaN); return; }
            const doseMg = 30 * w;
            setResult('solu-result', doseMg, 'mg');
        }

        function calcCrCl() {
            const age = parseFloat(document.getElementById('crcl-age').value);
            const weight = parseFloat(document.getElementById('crcl-weight').value);
            const gender = document.getElementById('crcl-gender').value;
            let creatinine = parseFloat(document.getElementById('crcl-creatinine').value);
            const unit = document.getElementById('crcl-unit').value;
            if (!requireValidNumber(age, weight, creatinine) || creatinine <= 0) { 
                setResult('crcl-result', NaN); 
                document.getElementById('crcl-recommendations').style.display = 'none';
                return; 
            }
            // Convert µmol/L to mg/dL if necessary (1 mg/dL = 88.4 µmol/L)
            if (unit === 'µmol/L') {
                creatinine = creatinine / 88.4;
            }
            const genderFactor = gender === 'female' ? 0.85 : 1;
            const crcl = ((140 - age) * weight * genderFactor) / (72 * creatinine);
            setResult('crcl-result', crcl, 'მლ/წთ');
            
            // Show recommendations
            const recDiv = document.getElementById('crcl-recommendations');
            const tableBody = document.getElementById('crcl-rec-table-body');
            tableBody.innerHTML = ''; // Clear previous
            let category;
            if (crcl > 50) category = '>50';
            else if (crcl >= 30 && crcl <= 50) category = '30-50';
            else if (crcl >= 10 && crcl < 30) category = '10-30';
            else category = '<10';

            // Recommendations based on category
            const recs = [
                { antibiotic: 'ამოქსიცილინი', ...getAmoxicillinRec(category) },
                { antibiotic: 'ციპროფლოქსაცინი', ...getCiprofloxacinRec(category) },
                { antibiotic: 'გენტამიცინი', ...getGentamicinRec(category) },
                { antibiotic: 'მეროპენემი', ...getMeropenemRec(category) },
                { antibiotic: 'ვანკომიცინი', ...getVancomycinRec(category) },
                { antibiotic: 'ცეფტრიაქსონი', ...getCeftriaxoneRec(category) },
                { antibiotic: 'მეტრონიდაზოლი', ...getMetronidazoleRec(category) },
                { antibiotic: 'ამპიცილინი', ...getAmpicillinRec(category) },
                { antibiotic: 'ლევოფლოქსაცინი', ...getLevofloxacinRec(category) }
            ];

            recs.forEach(rec => {
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td data-label="ანტიბიოტიკი">${rec.antibiotic}</td>
                    <td data-label="CrCl (მლ/წთ)">${rec.range}</td>
                    <td data-label="დოზა">${rec.dose}</td>
                    <td data-label="სიხშირე">${rec.frequency}</td>
                `;
                tableBody.appendChild(row);
            });

            recDiv.style.display = 'block';
        }

        function getAmoxicillinRec(category) {
            switch (category) {
                case '>50': return { range: '>50', dose: '875 მგ ან 500 მგ', frequency: 'ყოველ 12 სთ ან 8 სთ' };
                case '30-50': return { range: '30-50', dose: '875 მგ ან 500 მგ', frequency: 'ყოველ 12 სთ ან 8 სთ' };
                case '10-30': return { range: '10-30', dose: '500 მგ', frequency: 'ყოველ 12 სთ' };
                case '<10': return { range: '<10', dose: '500 მგ', frequency: 'ყოველ 24 სთ' };
                default: return { range: 'უცნობი', dose: 'გადაამოწმეთ', frequency: 'გადაამოწმეთ' };
            }
        }

        function getCiprofloxacinRec(category) {
            switch (category) {
                case '>50': return { range: '>50', dose: '250-750 მგ (PO) ან 400 მგ (IV)', frequency: 'ყოველ 12 სთ (PO) ან 8-12 სთ (IV)' };
                case '30-50': return { range: '30-50', dose: '250-750 მგ (PO) ან 400 მგ (IV)', frequency: 'ყოველ 12 სთ (PO) ან 8-12 სთ (IV)' };
                case '10-30': return { range: '10-30', dose: '250-750 მგ (PO) ან 400 მგ (IV)', frequency: 'ყოველ 12 სთ (PO) ან 8-12 სთ (IV)' };
                case '<10': return { range: '<10', dose: '250-750 მგ (PO) ან 400 მგ (IV)', frequency: 'ყოველ 24 სთ' };
                default: return { range: 'უცნობი', dose: 'გადაამოწმეთ', frequency: 'გადაამოწმეთ' };
            }
        }

        function getGentamicinRec(category) {
            switch (category) {
                case '>50': return { range: '>50', dose: '7 მგ/კგ ან 1.5-2.5 მგ/კგ', frequency: 'ყოველ 24 სთ (გაფართოებული) ან 8 სთ (ტრადიციული)' };
                case '30-50': return { range: '30-50', dose: '1.5-2.5 მგ/კგ', frequency: 'ყოველ 12 სთ' };
                case '10-30': return { range: '10-30', dose: '1.5-2.5 მგ/კგ', frequency: 'ყოველ 24 სთ' };
                case '<10': return { range: '<10', dose: '1.5-2.5 მგ/კგ', frequency: 'ყოველ 48-72 სთ' };
                default: return { range: 'უცნობი', dose: 'გადაამოწმეთ', frequency: 'გადაამოწმეთ' };
            }
        }

        function getMeropenemRec(category) {
            switch (category) {
                case '>50': return { range: '>50', dose: '500 მგ ან 2000 მგ (მენინგიტი)', frequency: 'ყოველ 6 სთ ან 8 სთ' };
                case '30-50': return { range: '30-50', dose: '500 მგ ან 2000 მგ', frequency: 'ყოველ 6 სთ ან 8 სთ' };
                case '10-30': return { range: '10-30', dose: '500 მგ ან 2000 მგ', frequency: 'ყოველ 6 სთ ან 8 სთ' };
                case '<10': return { range: '<10', dose: '500 მგ ან 1000 მგ', frequency: 'ყოველ 12 სთ' };
                default: return { range: 'უცნობი', dose: 'გადაამოწმეთ', frequency: 'გადაამოწმეთ' };
            }
        }

        function getVancomycinRec(category) {
            switch (category) {
                case '>50': return { range: '>50', dose: '15-20 მგ/კგ ან 25 მგ/კგ (ლოუდინგი)', frequency: 'ყოველ 12 სთ' };
                case '30-50': return { range: '30-50', dose: '15-20 მგ/კგ', frequency: 'ყოველ 12-24 სთ' };
                case '10-30': return { range: '10-30', dose: '15-20 მგ/კგ', frequency: 'ყოველ 24-48 სთ' };
                case '<10': return { range: '<10', dose: 'გაზომეთ სერიუმის დონე', frequency: 'გადაამოწმეთ' };
                default: return { range: 'უცნობი', dose: 'გადაამოწმეთ', frequency: 'გადაამოწმეთ' };
            }
        }

        function getCeftriaxoneRec(category) {
            switch (category) {
                case '>50': return { range: '>50', dose: '1000-2000 მგ', frequency: 'ყოველ 24 სთ ან 12 სთ (მენინგიტი)' };
                case '30-50': return { range: '30-50', dose: '1000-2000 მგ', frequency: 'ყოველ 24 სთ ან 12 სთ' };
                case '10-30': return { range: '10-30', dose: '1000-2000 მგ', frequency: 'ყოველ 24 სთ ან 12 სთ' };
                case '<10': return { range: '<10', dose: '1000-2000 მგ', frequency: 'ყოველ 24 სთ ან 12 სთ' };
                default: return { range: 'უცნობი', dose: 'გადაამოწმეთ', frequency: 'გადაამოწმეთ' };
            }
        }

        function getMetronidazoleRec(category) {
            switch (category) {
                case '>50': return { range: '>50', dose: '500 მგ', frequency: 'ყოველ 8 სთ' };
                case '30-50': return { range: '30-50', dose: '500 მგ', frequency: 'ყოველ 8 სთ' };
                case '10-30': return { range: '10-30', dose: '500 მგ', frequency: 'ყოველ 8 სთ' };
                case '<10': return { range: '<10', dose: '500 მგ', frequency: 'ყოველ 8 სთ' };
                default: return { range: 'უცნობი', dose: 'გადაამოწმეთ', frequency: 'გადაამოწმეთ' };
            }
        }

        function getAmpicillinRec(category) {
            switch (category) {
                case '>50': return { range: '>50', dose: '1000-2000 მგ', frequency: 'ყოველ 4-6 სთ' };
                case '30-50': return { range: '30-50', dose: '1000-2000 მგ', frequency: 'ყოველ 6 სთ' };
                case '10-30': return { range: '10-30', dose: '1000-2000 მგ', frequency: 'ყოველ 8 სთ' };
                case '<10': return { range: '<10', dose: '1000-2000 მგ', frequency: 'ყოველ 12 სთ' };
                default: return { range: 'უცნობი', dose: 'გადაამოწმეთ', frequency: 'გადაამოწმეთ' };
            }
        }

        function getLevofloxacinRec(category) {
            switch (category) {
                case '>50': return { range: '>50', dose: '500-750 მგ', frequency: 'ყოველ 24 სთ' };
                case '30-50': return { range: '30-50', dose: '250-500 მგ', frequency: 'ყოველ 24 სთ' };
                case '10-30': return { range: '10-30', dose: '250-500 მგ', frequency: 'ყოველ 48 სთ' };
                case '<10': return { range: '<10', dose: '250 მგ', frequency: 'ყოველ 48 სთ' };
                default: return { range: 'უცნობი', dose: 'გადაამოწმეთ', frequency: 'გადაამოწმეთ' };
            }
        }

        function resetCard(cardId) {
            const card = document.getElementById(cardId);
            const inputs = card.querySelectorAll('input, select');
            inputs.forEach(i => {
                if (i.tagName === 'SELECT') i.value = i.options[0].value;
                else i.value = '';
            });
            const res = card.querySelector('.result');
            if (res) res.textContent = 'შედეგი: —';
            const recDiv = card.querySelector('.recommendations');
            if (recDiv) recDiv.style.display = 'none';
        }

        async function copyResult(resultId) {
            const text = document.getElementById(resultId).textContent;
            try {
                await navigator.clipboard.writeText(text);
                toast('შედეგი დაკოპირდა!');
            } catch (err) {
                toast('კოპირება ვერ მოხერხდა.');
            }
        }

        function toast(msg) {
            const t = document.createElement('div');
            t.textContent = msg;
            t.style.cssText = `
                position: fixed; bottom: 16px; left: 50%; transform: translateX(-50%);
                padding: 10px 16px; background: var(--surface); border: 1px solid var(--muted);
                border-radius: 999px; box-shadow: var(--shadow-3); z-index: 1000;
                color: var(--text); font-size: 0.85rem; transition: opacity .25s ease-in-out;
            `;
            document.body.appendChild(t);
            setTimeout(() => { t.style.opacity = '0'; }, 2000);
            setTimeout(() => t.remove(), 2300);
        }
    </script>
</body>
</html>
