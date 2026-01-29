<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Earning Hub 2x | Pro Panel</title>
    
    <script src='//libtl.com/sdk.js' data-zone='10531705' data-sdk='show_10531705'></script>
    
    <style>
        :root { --primary: #0088cc; --accent: #ffd700; --bg: #0f172a; --card: #1e293b; --text: #f8fafc; --success: #2ecc71; }
        * { box-sizing: border-box; font-family: 'Poppins', sans-serif; }
        body { background: var(--bg); color: var(--text); margin: 0; padding-bottom: 90px; overflow-x: hidden; }
        
        /* Header & Balance */
        .header { background: linear-gradient(135deg, var(--primary), #005580); padding: 40px 20px; text-align: center; border-bottom-left-radius: 40px; border-bottom-right-radius: 40px; }
        .balance-box { background: rgba(255,255,255,0.1); padding: 15px; border-radius: 20px; display: inline-block; min-width: 160px; backdrop-filter: blur(10px); border: 1px solid rgba(255,255,255,0.2); }
        
        /* Scrolling Notice */
        .notice { background: #1e293b; color: var(--accent); padding: 10px; font-size: 13px; overflow: hidden; white-space: nowrap; border-bottom: 1px solid #333; position: sticky; top: 0; z-index: 100; }
        .notice-text { display: inline-block; animation: scroll 15s linear infinite; }
        @keyframes scroll { from { transform: translateX(100%); } to { transform: translateX(-100%); } }

        .container { padding: 15px; }
        .section { display: none; animation: fadeIn 0.3s ease; }
        .section.active { display: block; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        /* Task Cards */
        .card-box { background: var(--card); padding: 18px; border-radius: 18px; margin-bottom: 12px; border: 1px solid rgba(255,255,255,0.05); display: flex; justify-content: space-between; align-items: center; }
        .btn-main { background: var(--primary); color: white; border: none; padding: 12px 20px; border-radius: 12px; font-weight: bold; cursor: pointer; transition: 0.2s; }
        .btn-main:disabled { background: #475569; opacity: 0.7; }

        /* Bottom Navigation */
        .bottom-nav { position: fixed; bottom: 0; left: 0; right: 0; background: #111827; display: flex; padding: 15px 0 25px; border-top: 1px solid #333; z-index: 1000; }
        .nav-item { flex: 1; text-align: center; color: #64748b; font-size: 11px; cursor: pointer; }
        .nav-item.active { color: var(--primary); }
        .nav-item i { font-size: 22px; display: block; margin-bottom: 4px; }

        input { width: 100%; padding: 14px; margin-bottom: 12px; border-radius: 12px; border: none; background: #0f172a; color: white; }
        .rank-item { display: flex; justify-content: space-between; padding: 12px; background: rgba(255,255,255,0.03); margin-bottom: 8px; border-radius: 12px; }
    </style>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
</head>
<body>

    <div class="notice">
        <div class="notice-text" id="adminNotice">🎁 ১০০০টি ভিডিও টাস্ক কমপ্লিট করে প্রতিদিন ইনকাম করুন! ভিপিএন ছাড়া কাজ করবেন।</div>
    </div>

    <div class="header">
        <div class="balance-box">
            <h1 id="uBalance" style="margin:0;">0.00</h1>
            <p style="margin:0; font-size: 12px; opacity:0.8;">TK Balance</p>
        </div>
    </div>

    <div class="container">
        <div id="tab-video" class="section active">
            <h3 style="margin: 15px 0;"><i class="fas fa-play-circle" style="color:var(--primary);"></i> Daily Video Tasks (1000)</h3>
            <div id="taskList" style="max-height: 500px; overflow-y: auto; padding-right: 5px;">
                </div>
        </div>

        <div id="tab-leader" class="section">
            <h3 style="margin: 15px 0;"><i class="fas fa-trophy" style="color:var(--accent);"></i> Top 10 Earners</h3>
            <div id="leaderList"></div>
        </div>

        <div id="tab-profile" class="section">
            <div class="card-box" style="flex-direction: column; text-align: center;">
                <h2 id="pTele" style="margin: 0; color: var(--primary);">@user</h2>
                <p>Refer Code: <b id="uRefCode" style="color:var(--accent);">---</b></p>
                <div style="display:grid; grid-template-columns: 1fr 1fr; gap:10px; width: 100%; margin-top: 15px;">
                    <button class="btn-main" onclick="window.open('https://t.me/EarningHub2x')"><i class="fab fa-telegram"></i> Channel</button>
                    <button class="btn-main" onclick="shareRef()" style="background:var(--success);"><i class="fas fa-share-alt"></i> Invite</button>
                </div>
            </div>
        </div>

        <div id="tab-wallet" class="section">
            <div class="card-box" style="flex-direction: column;">
                <h3 style="margin:0 0 15px 0;">Withdraw Money</h3>
                <input type="number" id="wNum" placeholder="bKash/Nagad Number">
                <input type="number" id="wAmt" placeholder="Minimum 1000 TK">
                <button class="btn-main" style="width:100%;" onclick="withdrawReq()">Withdraw Now</button>
            </div>
        </div>
    </div>

    <nav class="bottom-nav">
        <div class="nav-item active" onclick="showTab('tab-video', this)"><i class="fas fa-play"></i>Video</div>
        <div class="nav-item" onclick="showTab('tab-leader', this)"><i class="fas fa-trophy"></i>Top</div>
        <div class="nav-item" onclick="showTab('tab-profile', this)"><i class="fas fa-user"></i>Profile</div>
        <div class="nav-item" onclick="showTab('tab-wallet', this)"><i class="fas fa-wallet"></i>Wallet</div>
    </nav>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getFirestore, doc, onSnapshot, getDoc, updateDoc, setDoc, collection, query, orderBy, limit, addDoc, where, getDocs } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";

        const firebaseConfig = {
            apiKey: "AIzaSyBaxt0kpDNSp_023Ny2cNr9cdJ5uQ9Wvn0",
            projectId: "telegram-adult--content",
            storageBucket: "telegram-adult--content.appspot.com",
            messagingSenderId: "367156943896",
            appId: "1:367156943896:web:12185203366a5067204684"
        };

        const app = initializeApp(firebaseConfig);
        const db = getFirestore(app);

        // --- User ID Sync ---
        const currentUserId = localStorage.getItem('eh_pro_uid') || localStorage.getItem('eh_uid') || "U" + Math.floor(Math.random()*10000);
        localStorage.setItem('eh_pro_uid', currentUserId);

        onSnapshot(doc(db, "users", currentUserId), async (d) => {
            if(!d.exists()){
                let tid = prompt("Enter Telegram @username:");
                const myCode = "EH" + Math.floor(100+Math.random()*899);
                await setDoc(doc(db, "users", currentUserId), { 
                    telegramID: tid || "User", balance: 0, status: 'active', referCode: myCode, referCount: 0 
                });
                return;
            }
            const data = d.data();
            document.getElementById('uBalance').innerText = data.balance.toFixed(2);
            document.getElementById('pTele').innerText = data.telegramID;
            document.getElementById('uRefCode').innerText = data.referCode;
        });

        // --- Generate 1000 Tasks ---
        const taskArea = document.getElementById('taskList');
        for(let i=1; i<=1000; i++) {
            const div = document.createElement('div');
            div.className = 'card-box';
            div.innerHTML = `<div><b>Task #${i}</b><br><small style="color:var(--success);">Earn: 2.50 TK</small></div>
                             <button class="btn-main" onclick="watchVideo(this, 2.5)">Watch</button>`;
            taskArea.appendChild(div);
        }

        window.watchVideo = async (btn, rew) => {
            btn.disabled = true;
            if (typeof show_10531705 === 'function') {
                show_10531705().then(async () => {
                    const uRef = doc(db, "users", currentUserId);
                    const snap = await getDoc(uRef);
                    const newBal = (snap.data().balance || 0) + rew;
                    await updateDoc(uRef, { balance: newBal });
                    
                    // 2% Commission to Referrer
                    const bossCode = snap.data().referredBy;
                    if(bossCode){
                        const q = query(collection(db, "users"), where("referCode", "==", bossCode));
                        const snapBoss = await getDocs(q);
                        snapBoss.forEach(b => {
                            updateDoc(doc(db, "users", b.id), { balance: b.data().balance + (rew * 0.02) });
                        });
                    }
                    btn.innerText = "Done";
                }).catch(() => btn.disabled = false);
            }
        };

        // --- Leaderboard ---
        onSnapshot(query(collection(db, "users"), orderBy("balance", "desc"), limit(10)), (snap) => {
            const list = document.getElementById('leaderList');
            list.innerHTML = "";
            let r = 1;
            snap.forEach(u => {
                list.innerHTML += `<div class="rank-item"><span>${r++}. ${u.data().telegramID}</span><b>${u.data().balance.toFixed(2)}৳</b></div>`;
            });
        });

        // --- Wallet ---
        window.withdrawReq = async () => {
            const num = document.getElementById('wNum').value;
            const amt = parseFloat(document.getElementById('wAmt').value);
            const uRef = doc(db, "users", currentUserId);
            const snap = await getDoc(uRef);
            if(amt >= 1000 && snap.data().balance >= amt){
                await addDoc(collection(db, "withdrawals"), { 
                    telegramID: snap.data().telegramID, number: num, amount: amt, time: Date.now() 
                });
                await updateDoc(uRef, { balance: snap.data().balance - amt });
                alert("Withdrawal Requested!");
            } else { alert("Insufficient balance or invalid amount!"); }
        };

        window.showTab = (id, el) => {
            document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
            document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
            document.getElementById(id).classList.add('active');
            el.classList.add('active');
        };

        window.shareRef = () => {
            const code = document.getElementById('uRefCode').innerText;
            const txt = `Join Earning Hub 2x and earn money daily! My Invite Code: ${code}`;
            navigator.clipboard.writeText(txt);
            alert("Invite text copied to clipboard!");
        };

        onSnapshot(doc(db, "admin_settings", "notice"), (d) => {
            if(d.exists()) document.getElementById('adminNotice').innerText = d.data().text;
        });
    </script>
</body>
</html>
