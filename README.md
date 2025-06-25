
<!DOCTYPE html>
<html lang="en">
<head>
    <meta  charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Beta Life Premium Lotto & Betting</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #0F172A; /* Slate 900 */
        }
        .main-container {
            background: #1E293B; /* Slate 800 */
            color: #F1F5F9; /* Slate 100 */
        }
        .number-grid-item {
            transition: all 0.2s ease-in-out;
            box-shadow: 0 2px 4px rgba(0,0,0,0.2);
        }
        .number-grid-item:hover {
            transform: translateY(-2px);
            background-color: #38BDF8; /* Sky 400 */
        }
        .number-grid-item.selected {
            background-color: #0EA5E9; /* Sky 500 */
            color: #fff;
            transform: scale(1.05);
            box-shadow: 0 4px 10px rgba(14, 165, 233, 0.4);
        }
        .btn-primary {
            background: linear-gradient(to right, #14B8A6, #0891B2);
            transition: all 0.3s ease;
            box-shadow: 0 4px 6px rgba(0,0,0,0.2);
        }
        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 12px rgba(0,0,0,0.3);
        }
        .tab-button {
            transition: all 0.2s ease;
        }
        .tab-button.active {
            background-color: #0EA5E9;
            color: white;
        }
        .result-ball {
            animation: bounceIn 0.5s ease;
        }
        @keyframes bounceIn {
            0% { transform: scale(0.5); opacity: 0; }
            50% { transform: scale(1.1); }
            100% { transform: scale(1); opacity: 1; }
        }
        /* Scratch Card styles */
        #scratch-card-container {
            position: relative;
            width: 100%;
            height: 200px;
            cursor: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 32 32"><path fill="%2314B8A6" d="M16 0 A16 16 0 0 1 16 32 A16 16 0 0 1 16 0 M16 4 A12 12 0 0 0 16 28 A12 12 0 0 0 16 4"/></svg>') 16 16, auto;
        }
        #scratch-layer {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(to right, #A855F7, #EC4899);
            border-radius: 0.5rem;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.25rem;
            font-weight: 600;
            color: white;
            text-align: center;
        }
        #prize-layer {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2rem;
            font-weight: 800;
            color: #FBBF24;
            background-color: #334155;
            border-radius: 0.5rem;
        }
        .modal-backdrop {
            background-color: rgba(0,0,0,0.7);
        }
    </style>
</head>
<body class="antialiased">

    <div class="main-container max-w-lg mx-auto min-h-screen shadow-2xl flex flex-col">
        <!-- Header -->
        <header class="p-4 bg-slate-900/50 backdrop-blur-sm shadow-lg border-b border-slate-700">
            <div class="flex items-center justify-between">
                <div>
                    <h1 class="text-2xl font-extrabold text-white tracking-wider">
                        <i class="fa-solid fa-star text-yellow-400"></i> BETA LIFE
                    </h1>
                    <p class="text-sm text-slate-400">Premium Lotto & Betting</p>
                </div>
                <div class="text-right">
                    <p class="text-slate-300 text-sm">Balance</p>
                    <p class="font-bold text-lg text-green-400" id="user-balance">₦5,000.00</p>
                </div>
            </div>
        </header>

        <!-- Tabs -->
        <nav class="flex justify-around p-2 bg-slate-800 shadow-md">
            <button class="tab-button flex-1 py-2 px-4 rounded-md font-semibold text-slate-300 active" data-tab="lotto">
                <i class="fa-solid fa-dice mr-2"></i>Lotto
            </button>
            <button class="tab-button flex-1 py-2 px-4 rounded-md font-semibold text-slate-300" data-tab="sports">
                <i class="fa-solid fa-futbol mr-2"></i>Sports
            </button>
            <button class="tab-button flex-1 py-2 px-4 rounded-md font-semibold text-slate-300" data-tab="instant">
                <i class="fa-solid fa-burst mr-2"></i>Instant Win
            </button>
        </nav>

        <!-- Main Content -->
        <main class="flex-grow p-4 md:p-6 overflow-y-auto">
            <!-- Lotto Tab -->
            <div id="lotto-tab" class="space-y-6">
                <div class="text-center p-4 bg-slate-700/50 rounded-lg">
                    <h2 class="text-xl font-bold text-sky-400">Mega Jackpot Draw</h2>
                    <p class="text-slate-300">Select 6 numbers from 1 to 49. Match all 6 to win!</p>
                    <p class="text-slate-400 text-sm mt-1">Ticket Price: ₦200.00</p>
                </div>
                
                <!-- Number Selection Grid -->
                <div id="number-grid" class="grid grid-cols-7 gap-2">
                    <!-- Numbers will be generated by JS -->
                </div>

                <!-- Selected Numbers & Action -->
                <div>
                    <h3 class="font-semibold mb-2">Your Picks:</h3>
                    <div id="selected-numbers-display" class="p-3 bg-slate-900 rounded-lg min-h-[50px] flex items-center justify-center space-x-2 text-lg font-bold">
                        <span class="text-slate-500">Select your numbers above</span>
                    </div>
                </div>
                <button id="buy-ticket-btn" class="w-full btn-primary text-white font-bold py-3 px-4 rounded-lg text-lg flex items-center justify-center disabled:opacity-50 disabled:cursor-not-allowed" disabled>
                    <i class="fa-solid fa-ticket mr-3"></i>Buy Ticket & Draw
                </button>

                <!-- Draw Result -->
                <div id="result-section" class="hidden text-center space-y-3 pt-4 border-t border-slate-700">
                    <h3 class="text-xl font-bold">Winning Numbers</h3>
                    <div id="winning-numbers-display" class="flex justify-center space-x-2">
                    </div>
                    <div id="winnings-message" class="text-lg font-bold p-3 rounded-lg"></div>
                </div>
            </div>

            <!-- Sports Tab -->
            <div id="sports-tab" class="hidden space-y-4">
                <div class="text-center p-4 bg-slate-700/50 rounded-lg">
                    <h2 class="text-xl font-bold text-green-400">Simulated Sports Betting</h2>
                    <p class="text-slate-300">Place a bet on upcoming matches. For entertainment only.</p>
                </div>
                <div class="space-y-3">
                    <!-- Match 1 -->
                    <div class="bg-slate-700 p-3 rounded-lg">
                        <p class="text-sm text-slate-400 mb-1">Naija Premier League</p>
                        <div class="flex items-center justify-between">
                            <span class="font-semibold">Enyimba FC</span>
                            <span class="text-xs font-mono text-slate-400">vs</span>
                            <span class="font-semibold">Kano Pillars</span>
                        </div>
                        <div class="mt-3 grid grid-cols-3 gap-2 text-center text-sm">
                            <button class="bet-option p-2 bg-slate-600 rounded hover:bg-sky-500" data-match="1" data-outcome="Enyimba FC" data-odds="1.85">1 (1.85)</button>
                            <button class="bet-option p-2 bg-slate-600 rounded hover:bg-sky-500" data-match="1" data-outcome="Draw" data-odds="3.20">X (3.20)</button>
                            <button class="bet-option p-2 bg-slate-600 rounded hover:bg-sky-500" data-match="1" data-outcome="Kano Pillars" data-odds="4.50">2 (4.50)</button>
                        </div>
                    </div>
                     <!-- Match 2 -->
                    <div class="bg-slate-700 p-3 rounded-lg">
                        <p class="text-sm text-slate-400 mb-1">Champions League</p>
                        <div class="flex items-center justify-between">
                            <span class="font-semibold">Real Madrid</span>
                            <span class="text-xs font-mono text-slate-400">vs</span>
                            <span class="font-semibold">Man City</span>
                        </div>
                        <div class="mt-3 grid grid-cols-3 gap-2 text-center text-sm">
                            <button class="bet-option p-2 bg-slate-600 rounded hover:bg-sky-500" data-match="2" data-outcome="Real Madrid" data-odds="2.50">1 (2.50)</button>
                            <button class="bet-option p-2 bg-slate-600 rounded hover:bg-sky-500" data-match="2" data-outcome="Draw" data-odds="3.50">X (3.50)</button>
                            <button class="bet-option p-2 bg-slate-600 rounded hover:bg-sky-500" data-match="2" data-outcome="Man City" data-odds="2.75">2 (2.75)</button>
                        </div>
                    </div>
                </div>
                 <!-- Bet Slip -->
                <div class="p-4 bg-slate-900 rounded-lg space-y-3">
                    <h3 class="font-bold text-lg border-b bord
