# Drs-coin.
Tap to earn
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DRS Coin - Tap To Earn Web3</title>
    <!-- Tailwind CSS for UI -->
    <script src="https://jsdelivr.net"></script>
    <!-- TON Connect SDK for Real Wallet Integration -->
    <script src="https://unpkg.com"></script>
    <style>
        .tap-btn:active { transform: scale(0.95); }
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; user-select: none; }
    </style>
</head>
<body class="bg-slate-950 text-white min-h-screen flex flex-col justify-between max-w-md mx-auto shadow-2xl border-x border-slate-800">

    <!-- TOP HEADER: Balance & Real Wallet -->
    <header class="p-4 bg-slate-900/50 backdrop-blur-md sticky top-0 z-50 flex justify-between items-center border-b border-slate-800">
        <div>
            <h1 class="text-xs text-slate-400 font-bold uppercase tracking-wider">Total Earnings</h1>
            <div class="flex items-center gap-2">
                <span class="text-2xl font-black text-amber-400" id="balance">0</span>
                <span class="text-xs text-amber-950 bg-gradient-to-r from-amber-400 to-yellow-500 px-2 py-0.5 rounded-full font-black tracking-wide shadow-sm">DRS</span>
            </div>
        </div>
        <!-- Real TON Wallet Connection Button Placeholder -->
        <div id="ton-connect-btn"></div>
    </header>

    <!-- MAIN VIEW CONTAINER -->
    <main class="flex-1 overflow-y-auto p-6 flex flex-col justify-center items-center" id="main-content">
        
        <!-- TAP GAME VIEW (Default) -->
        <div id="view-tap" class="w-full flex flex-col items-center justify-between h-full py-8">
            <!-- Profit Info -->
            <div class="text-center mb-6">
                <p class="text-xs text-slate-400">Passive Income: <span class="text-emerald-400 font-bold" id="pps-display">+0 DRS/s</span></p>
            </div>

            <!-- Big Tap Button -->
            <button onclick="handleTap(event)" class="tap-btn relative w-64 h-64 bg-gradient-to-br from-amber-500 via-amber-400 to-yellow-600 rounded-full shadow-[0_0_50px_rgba(245,158,11,0.5)] flex items-center justify-center border-8 border-amber-300 cursor-pointer transition-all duration-100 ease-out my-auto">
                <span class="text-7xl font-black text-amber-950 selection:bg-transparent">DRS</span>
            </button>

            <!-- Energy Bar -->
            <div class="w-full px-4 mt-8">
                <div class="flex justify-between text-xs text-slate-400 mb-1">
                    <span>⚡ Energy</span>
                    <span id="energy-text">500 / 500</span>
                </div>
                <div class="w-full bg-slate-800 h-3 rounded-full overflow-hidden">
                    <div id="energy-bar" class="bg-gradient-to-r from-amber-400 to-yellow-500 h-full transition-all duration-200" style="width: 100%;"></div>
                </div>
            </div>
        </div>

        <!-- WALLET VIEW (Real Web3) -->
        <div id="view-wallet" class="w-full hidden space-y-6">
            <h2 class="text-xl font-black border-b border-slate-800 pb-2 flex items-center gap-2">👛 Real Crypto Wallet</h2>
            
            <!-- Real Wallet Status Card -->
            <div class="bg-slate-900 border border-slate-800 p-4 rounded-2xl">
                <p class="text-xs text-slate-400 mb-1">Your Connected Address</p>
                <p id="wallet-address" class="text-xs font-mono text-amber-400 break-all bg-slate-950 p-2 rounded-lg border border-slate-800/50">⚠️ Wallet Not Connected</p>
            </div>

            <!-- Action Buttons -->
            <div class="grid grid-cols-2 gap-4">
                <button onclick="triggerDeposit()" class="bg-emerald-600 hover:bg-emerald-500 py-3 rounded-xl font-bold transition-all shadow-lg active:scale-95">📥 Real Deposit</button>
                <button onclick="openWithdrawModal()" class="bg-sky-600 hover:bg-sky-500 py-3 rounded-xl font-bold transition-all shadow-lg active:scale-95">📤 Real Withdraw</button>
            </div>
        </div>

        <!-- TASKS VIEW -->
        <div id="view-tasks" class="w-full hidden space-y-4">
            <h2 class="text-xl font-black border-b border-slate-800 pb-2">📋 Daily Quests</h2>
            <div onclick="claimDaily()" class="bg-slate-900 p-4 rounded-xl border border-slate-800 flex justify-between items-center cursor-pointer hover:bg-slate-850">
                <div>
                    <p class="font-bold text-sm"> 📆 Daily Check-In</p>
                    <p class="text-xs text-amber-400">+1,000 DRS Coins</p>
                </div>
                <button class="bg-amber-500 text-slate-950 text-xs font-black px-3 py-1.5 rounded-lg📄">Claim</button>
            </div>
        </div>

        <!-- SHOP VIEW -->
        <div id="view-shop" class="w-full hidden space-y-4">
            <h2 class="text-xl font-black border-b border-slate-800 pb-2">🛒 DRS Upgrade Shop</h2>
            <div onclick="buyRig()" class="bg-slate-900 p-4 rounded-xl border border-slate-800 flex justify-between items-center cursor-pointer hover:bg-slate-850">
                <div>
                    <p class="font-bold text-sm">⚙️ Basic DRS Mining Rig</p>
                    <p class="text-xs text-slate-400">Generates +2 DRS/sec</p>
                    <p class="text-xs text-amber-400 font-bold mt-1">Price: 500 DRS</p>
                </div>
                <span class="text-2xl">⚡</span>
            </div>
        </div>

        <!-- INVITE VIEW -->
        <div id="view-invite" class="w-full hidden space-y-4">
            <h2 class="text-xl font-black border-b border-slate-800 pb-2">👥 Referral System</h2>
            <div class="bg-slate-900 p-4 rounded-xl border border-slate-800 text-center">
                <p class="text-xs text-slate-400 mb-2">Invite friends and get 5,000 DRS per user</p>
                <button onclick="copyRef()" class="w-full bg-slate-800 hover:bg-slate-750 text-xs py-2 rounded-lg font-mono border border-slate-700 active:scale-98">📋 Copy Invite Link</button>
            </div>
        </div>
    </main>

    <!-- WITHDRAWAL MODAL POPUP -->
    <div id="withdraw-modal" class="fixed inset-0 bg-black/80 backdrop-blur-sm z-50 hidden flex items-center justify-center p-6">
        <div class="bg-slate-900 border border-slate-800 w-full max-w-sm rounded-2xl p-6 space-y-4">
            <h3 class="text-lg font-bold text-amber-400">Request Real Withdrawal</h3>
            <p class="text-xs text-slate-400">Your DRS Coins will be converted and processed to the network.</p>
            <div class="space-y-3">
                <input type="text" id="withdraw-addr" placeholder="Enter Destination TON/USDT Address" class="w-full bg-slate-950 border border-slate-800 rounded-xl p-3 text-xs font-mono focus:outline-none focus:border-amber-500">
                <input type="number" id="withdraw-amount" placeholder="Amount of DRS to Withdraw" class="w-full bg-slate-950 border border-slate-800 rounded-xl p-3 text-xs focus:outline-none focus:border-amber-500">
            </div>
            <div class="flex gap-3 pt-2">
                <button onclick="closeWithdrawModal()" class="w-1/2 bg-slate-800 py-2 rounded-xl text-sm font-bold">Cancel</button>
                <button onclick="processWithdrawal()" class="w-1/2 bg-amber-500 text-slate-950 py-2 rounded-xl text-sm font-bold">Submit Tx</button>
            </div>
        </div>
    </div>

    <!-- BOTTOM NAVIGATION BAR -->
    <nav class="bg-slate-900 border-t border-slate-800 p-2 grid grid-cols-5 gap-1 sticky bottom-0 z-50">
        <button onclick="switchView('tap')" class="flex flex-col items-center p-2 text-amber-400" id="nav-tap"><span class="text-xl">👆</span><span class="text-[10px] mt-1 font-bold">Tap</span></button>
        <button onclick="switchView('tasks')" class="flex flex-col items-center p-2 text-slate-400" id="nav-tasks"><span class="text-xl">📋</span><span class="text-[10px] mt-1 font-bold">Tasks</span></button>
        <button onclick="switchView('shop')" class="flex flex-col items-center p-2 text-slate-400" id="nav-shop"><span class="text-xl">🛒</span><span class="text-[10px] mt-1 font-bold">Shop</span></button>
        <button onclick="switchView('invite')" class="flex flex-col items-center p-2 text-slate-400" id="nav-invite"><span class="text-xl">👥</span><span class="text-[10px] mt-1 font-bold">Invite</span></button>
        <button onclick="switchView('wallet')" class="flex flex-col items-center p-2 text-slate-400" id="nav-wallet"><span class="text-xl">👛</span><span class="text-[10px] mt-1 font-bold">Wallet</span></button>
    </nav>

    <!-- CORE GAME LOGIC & WEB3 INTEGRATION JS -->
    <script>
        // State Variables
        let coins = 0;
        let energy = 500;
        let maxEnergy = 500;
        let passiveIncome = 0;

        // Initialize TON Connect UI (Official SDK)
        const tonConnectUI = new TONConnectUI.TonConnectUI({
            manifestUrl: 'https://githubusercontent.com', 
            buttonRootId: 'ton-connect-btn'
        });

        // Listen for Real Wallet Connection Event
        tonConnectUI.onStatusChange(wallet => {
            const addrElement = document.getElementById('wallet-address');
            if (wallet) {
                const userFriendlyAddress = wallet.account.address;
                addrElement.innerText = userFriendlyAddress.substring(0, 8) + "..." + userFriendlyAddress.substring(userFriendlyAddress.length - 8);
                addrElement.classList.remove('text-rose-400');
                addrElement.classList.add('text-emerald-400');
                alert("Real Crypto Wallet Connected Successfully!");
            } else {
