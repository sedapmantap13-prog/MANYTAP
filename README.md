<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TOKOGAME - HACKER MODE</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Share+Tech+Mono&display=swap');
        
        :root {
            --neon-green: #00ff41;
            --neon-blue: #00d4ff;
            --neon-red: #ff0040;
            --dark-bg: #0a0a0a;
            --darker-bg: #050505;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            background: var(--dark-bg);
            color: var(--neon-green);
            font-family: 'Share Tech Mono', monospace;
            overflow-x: hidden;
            position: relative;
        }
        
        /* Matrix Rain Background */
        #matrix-rain {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            opacity: 0.1;
        }
        
        /* Glitch Effect */
        .glitch {
            position: relative;
            text-shadow: 0.05em 0 0 rgba(255, 0, 0, 0.75),
                        -0.025em -0.05em 0 rgba(0, 255, 0, 0.75),
                        0.025em 0.05em 0 rgba(0, 0, 255, 0.75);
            animation: glitch 500ms infinite;
        }
        
        .glitch::before,
        .glitch::after {
            content: attr(data-text);
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
        }
        
        .glitch::before {
            left: 2px;
            text-shadow: -1px 0 red;
            clip: rect(44px, 450px, 56px, 0);
            animation: glitch-anim 3s infinite linear alternate-reverse;
        }
        
        .glitch::after {
            left: -2px;
            text-shadow: -1px 0 blue;
            clip: rect(44px, 450px, 56px, 0);
            animation: glitch-anim2 2s infinite linear alternate-reverse;
        }
        
        @keyframes glitch {
            0% { text-shadow: 0.05em 0 0 rgba(255, 0, 0, 0.75), -0.05em -0.025em 0 rgba(0, 255, 0, 0.75), 0.025em 0.05em 0 rgba(0, 0, 255, 0.75); }
            14% { text-shadow: 0.05em 0 0 rgba(255, 0, 0, 0.75), -0.05em -0.025em 0 rgba(0, 255, 0, 0.75), 0.025em 0.05em 0 rgba(0, 0, 255, 0.75); }
            15% { text-shadow: -0.05em -0.025em 0 rgba(255, 0, 0, 0.75), 0.025em 0.025em 0 rgba(0, 255, 0, 0.75), -0.05em -0.05em 0 rgba(0, 0, 255, 0.75); }
            49% { text-shadow: -0.05em -0.025em 0 rgba(255, 0, 0, 0.75), 0.025em 0.025em 0 rgba(0, 255, 0, 0.75), -0.05em -0.05em 0 rgba(0, 0, 255, 0.75); }
            50% { text-shadow: 0.025em 0.05em 0 rgba(255, 0, 0, 0.75), 0.05em 0 0 rgba(0, 255, 0, 0.75), 0 -0.05em 0 rgba(0, 0, 255, 0.75); }
            99% { text-shadow: 0.025em 0.05em 0 rgba(255, 0, 0, 0.75), 0.05em 0 0 rgba(0, 255, 0, 0.75), 0 -0.05em 0 rgba(0, 0, 255, 0.75); }
            100% { text-shadow: -0.025em 0 0 rgba(255, 0, 0, 0.75), -0.025em -0.025em 0 rgba(0, 255, 0, 0.75), -0.025em -0.05em 0 rgba(0, 0, 255, 0.75); }
        }
        
        @keyframes glitch-anim {
            0% { clip: rect(64px, 9999999px, 91px, 0); }
            100% { clip: rect(91px, 9999999px, 59px, 0); }
        }
        
        @keyframes glitch-anim2 {
            0% { clip: rect(119px, 9999999px, 19px, 0); }
            100% { clip: rect(29px, 9999999px, 98px, 0); }
        }
        
        /* Neon Glow */
        .neon-text {
            color: var(--neon-green);
            text-shadow: 0 0 10px var(--neon-green),
                         0 0 20px var(--neon-green),
                         0 0 30px var(--neon-green),
                         0 0 40px var(--neon-green);
        }
        
        .neon-border {
            border: 2px solid var(--neon-green);
            box-shadow: 0 0 10px var(--neon-green),
                        inset 0 0 10px var(--neon-green);
        }
        
        .neon-border-blue {
            border: 2px solid var(--neon-blue);
            box-shadow: 0 0 10px var(--neon-blue),
                        inset 0 0 10px var(--neon-blue);
        }
        
        .neon-border-red {
            border: 2px solid var(--neon-red);
            box-shadow: 0 0 10px var(--neon-red),
                        inset 0 0 10px var(--neon-red);
        }
        
        /* Terminal Style */
        .terminal {
            background: rgba(0, 0, 0, 0.8);
            border: 1px solid var(--neon-green);
            border-radius: 5px;
            padding: 20px;
            position: relative;
            overflow: hidden;
        }
        
        .terminal::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 30px;
            background: rgba(0, 255, 65, 0.1);
            border-bottom: 1px solid var(--neon-green);
        }
        
        .terminal-header {
            display: flex;
            align-items: center;
            margin-bottom: 15px;
            padding-top: 5px;
        }
        
        .terminal-dot {
            width: 12px;
            height: 12px;
            border-radius: 50%;
            margin-right: 8px;
        }
        
        .terminal-dot.red { background: var(--neon-red); }
        .terminal-dot.yellow { background: #ffaa00; }
        .terminal-dot.green { background: var(--neon-green); }
        
        /* Typing Animation */
        .typing {
            overflow: hidden;
            border-right: 3px solid var(--neon-green);
            white-space: nowrap;
            animation: typing 3.5s steps(40, end), blink-caret .75s step-end infinite;
        }
        
        @keyframes typing {
            from { width: 0 }
            to { width: 100% }
        }
        
        @keyframes blink-caret {
            from, to { border-color: transparent }
            50% { border-color: var(--neon-green); }
        }
        
        /* Cyber Button */
        .cyber-btn {
            background: transparent;
            border: 2px solid var(--neon-green);
            color: var(--neon-green);
            padding: 10px 20px;
            text-transform: uppercase;
            letter-spacing: 2px;
            position: relative;
            overflow: hidden;
            transition: all 0.3s;
            font-family: 'Orbitron', monospace;
            font-weight: 700;
        }
        
        .cyber-btn:hover {
            color: var(--dark-bg);
            box-shadow: 0 0 20px var(--neon-green);
        }
        
        .cyber-btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: var(--neon-green);
            transition: left 0.3s;
            z-index: -1;
        }
        
        .cyber-btn:hover::before {
            left: 0;
        }
        
        /* Cyber Card */
        .cyber-card {
            background: rgba(0, 0, 0, 0.7);
            border: 1px solid var(--neon-green);
            border-radius: 5px;
            padding: 15px;
            position: relative;
            overflow: hidden;
            transition: all 0.3s;
        }
        
        .cyber-card::before {
            content: '';
            position: absolute;
            top: -2px;
            left: -2px;
            right: -2px;
            bottom: -2px;
            background: linear-gradient(45deg, var(--neon-green), var(--neon-blue), var(--neon-red));
            z-index: -1;
            opacity: 0;
            transition: opacity 0.3s;
            filter: blur(5px);
        }
        
        .cyber-card:hover::before {
            opacity: 0.7;
        }
        
        .cyber-card:hover {
            transform: translateY(-5px);
            border-color: transparent;
        }
        
        /* Loading Animation */
        .loading {
            display: inline-block;
            width: 20px;
            height: 20px;
            border: 3px solid rgba(0, 255, 65, 0.3);
            border-radius: 50%;
            border-top-color: var(--neon-green);
            animation: spin 1s ease-in-out infinite;
        }
        
        @keyframes spin {
            to { transform: rotate(360deg); }
        }
        
        /* Scanline Effect */
        .scanline {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 2px;
            background: linear-gradient(to bottom, transparent, var(--neon-green), transparent);
            animation: scanline 8s linear infinite;
            z-index: 1;
        }
        
        @keyframes scanline {
            0% { transform: translateY(0); }
            100% { transform: translateY(100vh); }
        }
        
        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 10px;
        }
        
        ::-webkit-scrollbar-track {
            background: var(--darker-bg);
        }
        
        ::-webkit-scrollbar-thumb {
            background: var(--neon-green);
            border-radius: 5px;
        }
        
        ::-webkit-scrollbar-thumb:hover {
            background: var(--neon-blue);
        }
        
        /* Tawk.to Custom Styles */
        .tawk-custom {
            position: fixed;
            bottom: 6rem;
            right: 1.5rem;
            width: 320px;
            height: 400px;
            background: rgba(0, 0, 0, 0.9);
            border: 2px solid var(--neon-green);
            border-radius: 5px;
            z-index: 1000000;
            display: none;
            overflow: hidden;
            box-shadow: 0 0 20px var(--neon-green);
        }
        
        .tawk-custom-header {
            background: var(--neon-green);
            color: var(--dark-bg);
            padding: 10px;
            font-weight: bold;
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-family: 'Orbitron', monospace;
        }
        
        .tawk-custom-body {
            height: calc(100% - 40px);
            position: relative;
        }
        
        .tawk-custom iframe {
            width: 100% !important;
            height: 100% !important;
            border: none !important;
            background: transparent !important;
        }
        
        /* Hide default Tawk.to widget */
        iframe[title="chat widget"] {
            display: none !important;
        }
    </style>
</head>
<body>
    <!-- Matrix Rain Background -->
    <canvas id="matrix-rain"></canvas>
    
    <!-- Scanline Effect -->
    <div class="scanline"></div>
    
    <!-- Header -->
    <header class="py-6 px-4 border-b border-green-500 relative z-10">
        <div class="container mx-auto">
            <div class="flex justify-between items-center">
                <div class="flex items-center space-x-4">
                    <div class="text-4xl">
                        <i class="fas fa-terminal"></i>
                    </div>
                    <div>
                        <h1 class="text-3xl font-bold glitch" data-text="TOKOGAME">TOKOGAME</h1>
                        <p class="text-sm text-green-400">SYSTEM ACCESS GRANTED</p>
                    </div>
                </div>
                <div class="hidden md:flex items-center space-x-6">
                    <a href="#" class="hover:text-blue-400 transition">HOME</a>
                    <a href="#" class="hover:text-blue-400 transition">GAMES</a>
                    <a href="#" class="hover:text-blue-400 transition">VOUCHER</a>
                    <a href="#" class="hover:text-blue-400 transition">HACK</a>
                    <a href="#" class="hover:text-blue-400 transition">SUPPORT</a>
                </div>
                <button class="md:hidden text-2xl">
                    <i class="fas fa-bars"></i>
                </button>
            </div>
        </div>
    </header>

    <!-- Main Content -->
    <main class="container mx-auto px-4 py-8">
        <!-- Game Selection Section -->
        <div id="gameSelection" class="fade-in">
            <div class="terminal mb-8">
                <div class="terminal-header">
                    <div class="terminal-dot red"></div>
                    <div class="terminal-dot yellow"></div>
                    <div class="terminal-dot green"></div>
                    <span class="ml-4 text-sm">root@tokogame:~$ ./game_selector</span>
                </div>
                <div class="text-xl mb-2 typing">INITIALIZING GAME MODULES...</div>
                <div class="text-green-400 text-sm">
                    > Scanning available games...<br>
                    > Loading game databases...<br>
                    > System ready. Select target:
                </div>
            </div>
            
            <h3 class="text-2xl font-bold mb-6 text-center neon-text">SELECT TARGET</h3>
            
            <div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6 mb-8">
                <!-- Game Cards -->
                <div class="cyber-card cursor-pointer" onclick="selectGame('Free Fire', 'orange', 'fa-fire')">
                    <div class="text-center">
                        <div class="text-5xl mb-3 text-orange-500">
                            <i class="fas fa-fire"></i>
                        </div>
                        <h4 class="font-bold text-lg mb-1">FREE FIRE</h4>
                        <p class="text-xs text-green-400">BATTLE ROYALE</p>
                        <div class="mt-2 text-xs">
                            <span class="inline-block px-2 py-1 bg-green-900 text-green-400 rounded">ACTIVE</span>
                        </div>
                    </div>
                </div>
                
                <div class="cyber-card cursor-pointer" onclick="selectGame('Mobile Legends', 'blue', 'fa-mobile-alt')">
                    <div class="text-center">
                        <div class="text-5xl mb-3 text-blue-500">
                            <i class="fas fa-mobile-alt"></i>
                        </div>
                        <h4 class="font-bold text-lg mb-1">MOBILE LEGENDS</h4>
                        <p class="text-xs text-green-400">MOBA</p>
                        <div class="mt-2 text-xs">
                            <span class="inline-block px-2 py-1 bg-green-900 text-green-400 rounded">ACTIVE</span>
                        </div>
                    </div>
                </div>
                
                <div class="cyber-card cursor-pointer" onclick="selectGame('PUBG Mobile', 'red', 'fa-crosshairs')">
                    <div class="text-center">
                        <div class="text-5xl mb-3 text-red-500">
                            <i class="fas fa-crosshairs"></i>
                        </div>
                        <h4 class="font-bold text-lg mb-1">PUBG MOBILE</h4>
                        <p class="text-xs text-green-400">BATTLE ROYALE</p>
                        <div class="mt-2 text-xs">
                            <span class="inline-block px-2 py-1 bg-green-900 text-green-400 rounded">ACTIVE</span>
                        </div>
                    </div>
                </div>
                
                <div class="cyber-card cursor-pointer" onclick="selectGame('Garena Shell', 'yellow', 'fa-coins')">
                    <div class="text-center">
                        <div class="text-5xl mb-3 text-yellow-500">
                            <i class="fas fa-coins"></i>
                        </div>
                        <h4 class="font-bold text-lg mb-1">GARENA SHELL</h4>
                        <p class="text-xs text-green-400">CURRENCY</p>
                        <div class="mt-2 text-xs">
                            <span class="inline-block px-2 py-1 bg-green-900 text-green-400 rounded">ACTIVE</span>
                        </div>
                    </div>
                </div>
                
                <div class="cyber-card cursor-pointer" onclick="selectGame('Steam Wallet', 'gray', 'fa-steam')">
                    <div class="text-center">
                        <div class="text-5xl mb-3 text-gray-400">
                            <i class="fab fa-steam"></i>
                        </div>
                        <h4 class="font-bold text-lg mb-1">STEAM WALLET</h4>
                        <p class="text-xs text-green-400">PLATFORM</p>
                        <div class="mt-2 text-xs">
                            <span class="inline-block px-2 py-1 bg-green-900 text-green-400 rounded">ACTIVE</span>
                        </div>
                    </div>
                </div>
                
                <div class="cyber-card cursor-pointer" onclick="selectGame('Google Play', 'green', 'fa-google-play')">
                    <div class="text-center">
                        <div class="text-5xl mb-3 text-green-500">
                            <i class="fab fa-google-play"></i>
                        </div>
                        <h4 class="font-bold text-lg mb-1">GOOGLE PLAY</h4>
                        <p class="text-xs text-green-400">STORE</p>
                        <div class="mt-2 text-xs">
                            <span class="inline-block px-2 py-1 bg-green-900 text-green-400 rounded">ACTIVE</span>
                        </div>
                    </div>
                </div>
                
                <div class="cyber-card cursor-pointer" onclick="selectGame('Call of Duty', 'indigo', 'fa-fighter-jet')">
                    <div class="text-center">
                        <div class="text-5xl mb-3 text-indigo-500">
                            <i class="fas fa-fighter-jet"></i>
                        </div>
                        <h4 class="font-bold text-lg mb-1">CALL OF DUTY</h4>
                        <p class="text-xs text-green-400">FPS</p>
                        <div class="mt-2 text-xs">
                            <span class="inline-block px-2 py-1 bg-green-900 text-green-400 rounded">ACTIVE</span>
                        </div>
                    </div>
                </div>
                
                <div class="cyber-card cursor-pointer" onclick="selectGame('Arena of Valor', 'purple', 'fa-hat-wizard')">
                    <div class="text-center">
                        <div class="text-5xl mb-3 text-purple-500">
                            <i class="fas fa-hat-wizard"></i>
                        </div>
                        <h4 class="font-bold text-lg mb-1">ARENA OF VALOR</h4>
                        <p class="text-xs text-green-400">MOBA</p>
                        <div class="mt-2 text-xs">
                            <span class="inline-block px-2 py-1 bg-green-900 text-green-400 rounded">ACTIVE</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Top Up Form Section (Hidden by default) -->
        <div id="topUpForm" class="hidden">
            <div class="flex items-center mb-6">
                <button onclick="backToGameSelection()" class="flex items-center text-green-400 hover:text-green-300 mr-4">
                    <i class="fas fa-arrow-left mr-2"></i> ABORT
                </button>
                <div class="flex items-center">
                    <div id="selectedGameIcon" class="w-12 h-12 rounded-lg flex items-center justify-center mr-3 neon-border">
                        <i class="fas fa-fire text-2xl text-orange-500"></i>
                    </div>
                    <div>
                        <h3 id="selectedGameName" class="text-2xl font-bold neon-text">FREE FIRE</h3>
                        <p class="text-green-400 text-sm">TARGET LOCKED</p>
                    </div>
                </div>
            </div>

            <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
                <!-- Left Column - Form -->
                <div class="lg:col-span-2">
                    <div class="terminal">
                        <div class="terminal-header">
                            <div class="terminal-dot red"></div>
                            <div class="terminal-dot yellow"></div>
                            <div class="terminal-dot green"></div>
                            <span class="ml-4 text-sm">root@tokogame:~$ ./topup_system</span>
                        </div>
                        
                        <!-- Membership Benefits -->
                        <div id="membershipBenefits" class="mb-6 p-4 border-l-4 border-orange-500">
                            <h4 class="font-bold mb-2 text-orange-400 flex items-center">
                                <i class="fas fa-shield-alt mr-2"></i> SYSTEM PRIVILEGES:
                            </h4>
                            <ul class="list-disc list-inside text-sm text-green-400">
                                <li>WEEKLY ACCESS: +10% BONUS</li>
                                <li>MONTHLY ACCESS: +15% BONUS + EXCLUSIVE ITEMS</li>
                                <li>EVENT ACCESS: UNLOCKED</li>
                            </ul>
                        </div>

                        <!-- User Input Section -->
                        <div class="mb-6">
                            <label class="block text-green-400 mb-2 font-bold">TARGET ID <span class="text-red-500">*</span></label>
                            <input type="text" id="userId" placeholder="ENTER TARGET ID" class="w-full px-4 py-3 bg-black border border-green-500 rounded text-green-400 focus:outline-none focus:border-blue-400 font-mono">
                            <p id="idHelpText" class="text-xs text-green-600 mt-1">LOCATE ID IN GAME PROFILE</p>
                        </div>

                        <div class="mb-6">
                            <label class="block text-green-400 mb-2 font-bold">CONTACT NUMBER (OPTIONAL)</label>
                            <input type="tel" id="userPhone" placeholder="ENTER PHONE NUMBER" class="w-full px-4 py-3 bg-black border border-green-500 rounded text-green-400 focus:outline-none focus:border-blue-400 font-mono">
                            <p class="text-xs text-green-600 mt-1">FOR TRANSACTION CONFIRMATION</p>
                        </div>

                        <!-- Package Selection -->
                        <h4 class="font-bold mb-4 text-lg text-green-400">SELECT PACKAGE</h4>
                        <div id="packageGrid" class="grid grid-cols-2 md:grid-cols-3 gap-4 mb-6">
                            <!-- Packages will be dynamically inserted here -->
                        </div>

                        <!-- Selected Package Display -->
                        <div id="selectedPackage" class="hidden mb-6 p-4 border border-orange-500 rounded">
                            <div class="flex justify-between items-center">
                                <div>
                                    <span class="font-bold">PACKAGE SELECTED:</span>
                                    <span id="packageInfo" class="ml-2"></span>
                                </div>
                                <div class="font-bold text-lg" id="packagePrice"></div>
                            </div>
                        </div>

                        <!-- Payment Method Selection -->
                        <h4 class="font-bold mb-4 text-lg text-green-400">PAYMENT PROTOCOL</h4>
                        <div class="grid grid-cols-2 md:grid-cols-4 gap-3 mb-6">
                            <div class="cyber-card cursor-pointer text-center" onclick="selectPayment('BCA')">
                                <i class="fas fa-university text-2xl text-blue-500 mb-2"></i>
                                <div class="text-xs">BCA</div>
                            </div>
                            <div class="cyber-card cursor-pointer text-center" onclick="selectPayment('Mandiri')">
                                <i class="fas fa-university text-2xl text-blue-800 mb-2"></i>
                                <div class="text-xs">MANDIRI</div>
                            </div>
                            <div class="cyber-card cursor-pointer text-center" onclick="selectPayment('BNI')">
                                <i class="fas fa-university text-2xl text-green-600 mb-2"></i>
                                <div class="text-xs">BNI</div>
                            </div>
                            <div class="cyber-card cursor-pointer text-center" onclick="selectPayment('BRI')">
                                <i class="fas fa-university text-2xl text-blue-500 mb-2"></i>
                                <div class="text-xs">BRI</div>
                            </div>
                            <div class="cyber-card cursor-pointer text-center" onclick="selectPayment('Gopay')">
                                <i class="fas fa-wallet text-2xl text-blue-500 mb-2"></i>
                                <div class="text-xs">GOPAY</div>
                            </div>
                            <div class="cyber-card cursor-pointer text-center" onclick="selectPayment('OVO')">
                                <i class="fas fa-wallet text-2xl text-purple-600 mb-2"></i>
                                <div class="text-xs">OVO</div>
                            </div>
                            <div class="cyber-card cursor-pointer text-center" onclick="selectPayment('DANA')">
                                <i class="fas fa-wallet text-2xl text-blue-700 mb-2"></i>
                                <div class="text-xs">DANA</div>
                            </div>
                            <div class="cyber-card cursor-pointer text-center" onclick="selectPayment('ShopeePay')">
                                <i class="fas fa-wallet text-2xl text-orange-500 mb-2"></i>
                                <div class="text-xs">SHOPEEPAY</div>
                            </div>
                        </div>

                        <!-- Process Button -->
                        <button id="processBtn" onclick="processOrder()" class="w-full cyber-btn text-lg py-3" disabled>
                            INITIATE TRANSFER
                        </button>
                    </div>
                </div>

                <!-- Right Column - Info & Contact -->
                <div class="lg:col-span-1">
                    <!-- Game Info -->
                    <div class="terminal mb-6">
                        <div class="terminal-header">
                            <div class="terminal-dot red"></div>
                            <div class="terminal-dot yellow"></div>
                            <div class="terminal-dot green"></div>
                            <span class="ml-4 text-sm">root@tokogame:~$ ./target_info</span>
                        </div>
                        <h3 class="font-bold mb-4">TARGET: <span id="gameInfoName">FREE FIRE</span></h3>
                        <p id="gameDescription" class="text-sm text-green-400 mb-4">BATTLE ROYALE GAME DEVELOPED BY 111DOTS STUDIO</p>
                        <div id="gameDetails" class="space-y-2 text-sm">
                            <div class="flex items-center">
                                <i class="fas fa-code text-orange-500 mr-2"></i>
                                <span>DEVELOPER: 111DOTS STUDIO</span>
                            </div>
                            <div class="flex items-center">
                                <i class="fas fa-server text-orange-500 mr-2"></i>
                                <span>PUBLISHER: GARENA</span>
                            </div>
                            <div class="flex items-center">
                                <i class="fas fa-calendar text-orange-500 mr-2"></i>
                                <span>RELEASE: 2017</span>
                            </div>
                        </div>
                    </div>

                    <!-- How to Top Up -->
                    <div class="terminal mb-6">
                        <div class="terminal-header">
                            <div class="terminal-dot red"></div>
                            <div class="terminal-dot yellow"></div>
                            <div class="terminal-dot green"></div>
                            <span class="ml-4 text-sm">root@tokogame:~$ ./protocol</span>
                        </div>
                        <h3 class="font-bold mb-4">INFILTRATION PROTOCOL</h3>
                        <ol class="list-decimal list-inside space-y-2 text-sm text-green-400">
                            <li>ENTER TARGET ID</li>
                            <li>SELECT PACKAGE</li>
                            <li>CHOOSE PAYMENT</li>
                            <li>INITIATE TRANSFER</li>
                            <li>COMPLETE TRANSACTION</li>
                            <li>RESOURCES DELIVERED</li>
                        </ol>
                    </div>

                    <!-- Contact Information -->
                    <div class="terminal">
                        <div class="terminal-header">
                            <div class="terminal-dot red"></div>
                            <div class="terminal-dot yellow"></div>
                            <div class="terminal-dot green"></div>
                            <span class="ml-4 text-sm">root@tokogame:~$ ./support</span>
                        </div>
                        <h3 class="font-bold mb-4">SUPPORT CHANNEL</h3>
                        <div class="space-y-3">
                            <a href="#" class="flex items-center text-green-400 hover:text-green-300 transition">
                                <i class="fab fa-whatsapp text-xl mr-3"></i>
                                <span>WHATSAPP</span>
                            </a>
                            <a href="#" class="flex items-center text-green-400 hover:text-green-300 transition">
                                <i class="fab fa-instagram text-xl mr-3"></i>
                                <span>INSTAGRAM</span>
                            </a>
                            <a href="#" class="flex items-center text-green-400 hover:text-green-300 transition">
                                <i class="fab fa-facebook-messenger text-xl mr-3"></i>
                                <span>MESSENGER</span>
                            </a>
                            <a href="#" class="flex items-center text-green-400 hover:text-green-300 transition">
                                <i class="fas fa-envelope text-xl mr-3"></i>
                                <span>EMAIL</span>
                            </a>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </main>

    <!-- Custom Tawk.to Chat Widget -->
    <div class="fixed bottom-6 right-6 z-50">
        <!-- Custom Tawk.to Container -->
        <div id="tawkCustomContainer" class="tawk-custom">
            <div class="tawk-custom-header">
                <span>SUPPORT TERMINAL</span>
                <button onclick="toggleTawkChat()" class="text-black hover:text-gray-700">
                    <i class="fas fa-times"></i>
                </button>
            </div>
            <div class="tawk-custom-body">
                <!-- Tawk.to akan dimuat di sini -->
            </div>
        </div>
        
        <!-- Custom Chat Button -->
        <button onclick="toggleTawkChat()" class="bg-green-500 text-black rounded-full w-14 h-14 flex items-center justify-center shadow-lg hover:bg-green-400 transition font-bold">
            <i class="fas fa-terminal"></i>
        </button>
    </div>

    <!--Start of Custom Tawk.to Script-->
    <script type="text/javascript">
    var Tawk_API = Tawk_API || {},
        Tawk_LoadStart = new Date();

    // Custom functions untuk Tawk.to
    Tawk_API.onLoad = function() {
        console.log("Tawk.to loaded");
        // Sembunyikan widget default
        if (document.querySelector('iframe[title="chat widget"]')) {
            document.querySelector('iframe[title="chat widget"]').style.display = 'none';
        }
    };

    Tawk_API.onChatMaximized = function() {
        console.log("Chat maximized");
        // Sembunyikan custom container saat Tawk.to terbuka
        document.getElementById('tawkCustomContainer').style.display = 'none';
    };

    Tawk_API.onChatMinimized = function() {
        console.log("Chat minimized");
        // Tampilkan custom container saat Tawk.to diminimalkan
        document.getElementById('tawkCustomContainer').style.display = 'block';
    };

    Tawk_API.onChatHidden = function() {
        console.log("Chat hidden");
        // Sembunyikan custom container saat Tawk.to disembunyikan
        document.getElementById('tawkCustomContainer').style.display = 'none';
    };

    // Fungsi untuk toggle chat
    function toggleTawkChat() {
        if (typeof Tawk_API !== 'undefined') {
            Tawk_API.toggle();
            
            // Tampilkan custom container jika chat sedang terbuka
            setTimeout(function() {
                if (Tawk_API.isChatMaximized()) {
                    document.getElementById('tawkCustomContainer').style.display = 'block';
                    // Pindahkan iframe Tawk.to ke custom container
                    var tawkIframe = document.querySelector('iframe[title="chat widget"]');
                    if (tawkIframe) {
                        document.querySelector('.tawk-custom-body').appendChild(tawkIframe);
                        tawkIframe.style.display = 'block';
                    }
                }
            }, 500);
        }
    }

    // Load Tawk.to script
    (function() {
        var s1 = document.createElement("script"),
            s0 = document.getElementsByTagName("script")[0];
        s1.async = true;
        s1.src = 'https://embed.tawk.to/68fc0a02511129194ce141e5/1j8c8e6m5';
        s1.charset = 'UTF-8';
        s1.setAttribute('crossorigin', '*');
        s0.parentNode.insertBefore(s1, s0);
    })();
    </script>
    <!--End of Custom Tawk.to Script-->

    <script>
        // Matrix Rain Effect
        const canvas = document.getElementById('matrix-rain');
        const ctx = canvas.getContext('2d');
        
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
        
        const matrix = "ABCDEFGHIJKLMNOPQRSTUVWXYZ123456789@#$%^&*()*&^%+-/~{[|`]}";
        const matrixArray = matrix.split("");
        
        const fontSize = 10;
        const columns = canvas.width / fontSize;
        
        const drops = [];
        for(let x = 0; x < columns; x++) {
            drops[x] = 1;
        }
        
        function draw() {
            ctx.fillStyle = 'rgba(0, 0, 0, 0.04)';
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            
            ctx.fillStyle = '#00ff41';
            ctx.font = fontSize + 'px monospace';
            
            for(let i = 0; i < drops.length; i++) {
                const text = matrixArray[Math.floor(Math.random() * matrixArray.length)];
                ctx.fillText(text, i * fontSize, drops[i] * fontSize);
                
                if(drops[i] * fontSize > canvas.height && Math.random() > 0.975) {
                    drops[i] = 0;
                }
                drops[i]++;
            }
        }
        
        setInterval(draw, 35);
        
        // Resize canvas on window resize
        window.addEventListener('resize', () => {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        });
        
        // Game selection functionality
        let selectedGame = '';
        let selectedGameColor = '';
        let selectedGameIcon = '';
        let selectedDiamonds = 0;
        let selectedPrice = 0;
        let selectedPayment = '';

        // Game data
        const gameData = {
            'Free Fire': {
                color: 'orange',
                icon: 'fa-fire',
                description: 'BATTLE ROYALE GAME DEVELOPED BY 111DOTS STUDIO',
                developer: '111DOTS STUDIO',
                publisher: 'GARENA',
                release: '2017',
                currency: 'DIAMONDS',
                packages: [
                    { amount: 12, price: 2000 },
                    { amount: 50, price: 8000 },
                    { amount: 100, price: 15000 },
                    { amount: 200, price: 28000 },
                    { amount: 310, price: 42000 },
                    { amount: 425, price: 55000 },
                    { amount: 570, price: 70000 },
                    { amount: 720, price: 85000 },
                    { amount: 1000, price: 115000 }
                ]
            },
            'Mobile Legends': {
                color: 'blue',
                icon: 'fa-mobile-alt',
                description: 'MOBA GAME DEVELOPED BY MOONTON',
                developer: 'MOONTON',
                publisher: 'MOONTON',
                release: '2016',
                currency: 'DIAMONDS',
                packages: [
                    { amount: 86, price: 20000 },
                    { amount: 172, price: 40000 },
                    { amount: 257, price: 60000 },
                    { amount: 344, price: 80000 },
                    { amount: 429, price: 100000 },
                    { amount: 514, price: 120000 },
                    { amount: 600, price: 140000 },
                    { amount: 708, price: 165000 },
                    { amount: 880, price: 200000 }
                ]
            },
            'PUBG Mobile': {
                color: 'red',
                icon: 'fa-crosshairs',
                description: 'BATTLE ROYALE GAME DEVELOPED BY LIGHTSPEED & QUANTUM',
                developer: 'LIGHTSPEED & QUANTUM STUDIO',
                publisher: 'TENCENT GAMES',
                release: '2018',
                currency: 'UC',
                packages: [
                    { amount: 60, price: 15000 },
                    { amount: 300, price: 75000 },
                    { amount: 600, price: 150000 },
                    { amount: 1200, price: 300000 },
                    { amount: 1800, price: 450000 },
                    { amount: 2400, price: 600000 },
                    { amount: 3000, price: 750000 },
                    { amount: 3600, price: 900000 },
                    { amount: 6000, price: 1500000 }
                ]
            },
            'Garena Shell': {
                color: 'yellow',
                icon: 'fa-coins',
                description: 'VIRTUAL CURRENCY FOR GARENA GAMES',
                developer: 'GARENA',
                publisher: 'GARENA',
                release: '2010',
                currency: 'SHELLS',
                packages: [
                    { amount: 12, price: 15000 },
                    { amount: 23, price: 30000 },
                    { amount: 46, price: 60000 },
                    { amount: 92, price: 120000 },
                    { amount: 184, price: 240000 },
                    { amount: 276, price: 360000 },
                    { amount: 368, price: 480000 },
                    { amount: 460, price: 600000 },
                    { amount: 920, price: 1200000 }
                ]
            },
            'Steam Wallet': {
                color: 'gray',
                icon: 'fa-steam',
                description: 'DIGITAL WALLET FOR STEAM PLATFORM',
                developer: 'VALVE',
                publisher: 'VALVE',
                release: '2003',
                currency: 'WALLET',
                packages: [
                    { amount: 12000, price: 150000 },
                    { amount: 25000, price: 300000 },
                    { amount: 50000, price: 600000 },
                    { amount: 100000, price: 1200000 },
                    { amount: 200000, price: 2400000 },
                    { amount: 300000, price: 3600000 },
                    { amount: 400000, price: 4800000 },
                    { amount: 500000, price: 6000000 },
                    { amount: 1000000, price: 12000000 }
                ]
            },
            'Google Play': {
                color: 'green',
                icon: 'fa-google-play',
                description: 'DIGITAL CONTENT FOR ANDROID',
                developer: 'GOOGLE',
                publisher: 'GOOGLE',
                release: '2008',
                currency: 'SALDO',
                packages: [
                    { amount: 15000, price: 20000 },
                    { amount: 50000, price: 65000 },
                    { amount: 100000, price: 130000 },
                    { amount: 200000, price: 260000 },
                    { amount: 300000, price: 390000 },
                    { amount: 400000, price: 520000 },
                    { amount: 500000, price: 650000 },
                    { amount: 1000000, price: 1300000 },
                    { amount: 2000000, price: 2600000 }
                ]
            },
            'Call of Duty': {
                color: 'indigo',
                icon: 'fa-fighter-jet',
                description: 'FPS GAME DEVELOPED BY TIMI STUDIO',
                developer: 'TIMI STUDIO GROUP',
                publisher: 'ACTIVISION',
                release: '2019',
                currency: 'CP',
                packages: [
                    { amount: 50, price: 12000 },
                    { amount: 120, price: 28000 },
                    { amount: 240, price: 56000 },
                    { amount: 360, price: 84000 },
                    { amount: 600, price: 140000 },
                    { amount: 960, price: 224000 },
                    { amount: 1320, price: 308000 },
                    { amount: 1920, price: 448000 },
                    { amount: 3840, price: 896000 }
                ]
            },
            'Arena of Valor': {
                color: 'purple',
                icon: 'fa-hat-wizard',
                description: 'MOBA GAME DEVELOPED BY TIMI STUDIO',
                developer: 'TIMI STUDIO GROUP',
                publisher: 'GARENA',
                release: '2016',
                currency: 'VOUCHER',
                packages: [
                    { amount: 76, price: 15000 },
                    { amount: 152, price: 30000 },
                    { amount: 228, price: 45000 },
                    { amount: 304, price: 60000 },
                    { amount: 380, price: 75000 },
                    { amount: 456, price: 90000 },
                    { amount: 608, price: 120000 },
                    { amount: 760, price: 150000 },
                    { amount: 1520, price: 300000 }
                ]
            }
        };

        function selectGame(gameName, color, icon) {
            selectedGame = gameName;
            selectedGameColor = color;
            selectedGameIcon = icon;
            
            // Hide game selection and show top up form
            document.getElementById('gameSelection').classList.add('hidden');
            document.getElementById('topUpForm').classList.remove('hidden');
            document.getElementById('topUpForm').classList.add('fade-in');
            
            // Update game info
            const game = gameData[gameName];
            document.getElementById('selectedGameName').textContent = gameName.toUpperCase();
            document.getElementById('selectedGameIcon').innerHTML = `<i class="fas ${icon} text-2xl text-${color}-500"></i>`;
            document.getElementById('gameInfoName').textContent = gameName.toUpperCase();
            document.getElementById('gameDescription').textContent = game.description.toUpperCase();
            
            // Update game details
            const detailsHtml = `
                <div class="flex items-center text-sm">
                    <i class="fas fa-code text-${color}-500 mr-2"></i>
                    <span>DEVELOPER: ${game.developer}</span>
                </div>
                <div class="flex items-center text-sm">
                    <i class="fas fa-server text-${color}-500 mr-2"></i>
                    <span>PUBLISHER: ${game.publisher}</span>
                </div>
                <div class="flex items-center text-sm">
                    <i class="fas fa-calendar text-${color}-500 mr-2"></i>
                    <span>RELEASE: ${game.release}</span>
                </div>
            `;
            document.getElementById('gameDetails').innerHTML = detailsHtml;
            
            // Update membership benefits color
            const membershipDiv = document.getElementById('membershipBenefits');
            membershipDiv.className = `mb-6 p-4 border-l-4 border-${color}-500`;
            membershipDiv.querySelector('h4').className = `font-bold mb-2 text-${color}-400 flex items-center`;
            
            // Update ID help text
            document.getElementById('idHelpText').textContent = `LOCATE ID IN ${gameName.toUpperCase()} PROFILE`;
            
            // Generate package cards
            generatePackageCards(game);
            
            // Reset selections
            selectedDiamonds = 0;
            selectedPrice = 0;
            selectedPayment = '';
            document.getElementById('selectedPackage').classList.add('hidden');
            document.getElementById('processBtn').disabled = true;
        }

        function generatePackageCards(game) {
            const packageGrid = document.getElementById('packageGrid');
            packageGrid.innerHTML = '';
            
            game.packages.forEach(pkg => {
                const card = document.createElement('div');
                card.className = 'cyber-card cursor-pointer text-center';
                card.onclick = () => selectPackage(pkg.amount, pkg.price);
                
                card.innerHTML = `
                    <div class="text-3xl font-bold text-${game.color}-500 mb-1">${pkg.amount}</div>
                    <div class="text-sm text-green-400">${game.currency}</div>
                    <div class="font-bold mt-1">Rp ${pkg.price.toLocaleString('id-ID')}</div>
                `;
                
                packageGrid.appendChild(card);
            });
        }

        function backToGameSelection() {
            // Show game selection and hide top up form
            document.getElementById('topUpForm').classList.add('hidden');
            document.getElementById('gameSelection').classList.remove('hidden');
            document.getElementById('gameSelection').classList.add('fade-in');
        }

        function selectPackage(amount, price) {
            selectedDiamonds = amount;
            selectedPrice = price;
            
            // Update UI to show selected package
            const packageCards = document.querySelectorAll('#packageGrid .cyber-card');
            packageCards.forEach(card => {
                card.style.background = 'rgba(0, 0, 0, 0.7)';
            });
            
            event.currentTarget.style.background = 'rgba(0, 255, 65, 0.1)';
            
            // Show selected package info
            const selectedPackageDiv = document.getElementById('selectedPackage');
            selectedPackageDiv.classList.remove('hidden');
            document.getElementById('packageInfo').textContent = `${amount} ${gameData[selectedGame].currency}`;
            document.getElementById('packagePrice').textContent = `Rp ${price.toLocaleString('id-ID')}`;
            
            // Enable process button if all required fields are filled
            checkFormValidity();
        }

        function selectPayment(payment) {
            selectedPayment = payment;
            
            // Update UI to show selected payment
            const paymentMethods = document.querySelectorAll('.cyber-card');
            paymentMethods.forEach(method => {
                if (method.onclick && method.onclick.toString().includes('selectPayment')) {
                    method.style.background = 'rgba(0, 0, 0, 0.7)';
                }
            });
            
            event.currentTarget.style.background = 'rgba(0, 255, 65, 0.1)';
            
            // Enable process button if all required fields are filled
            checkFormValidity();
        }

        function checkFormValidity() {
            const userId = document.getElementById('userId').value;
            const processBtn = document.getElementById('processBtn');
            
            if (userId && selectedDiamonds > 0 && selectedPayment) {
                processBtn.disabled = false;
            } else {
                processBtn.disabled = true;
            }
        }

        function processOrder() {
            const userId = document.getElementById('userId').value;
            const userPhone = document.getElementById('userPhone').value;
            
            if (!userId) {
                alert(`PLEASE ENTER ${selectedGame.toUpperCase()} ID`);
                return;
            }
            
            if (selectedDiamonds === 0) {
                alert('PLEASE SELECT PACKAGE');
                return;
            }
            
            if (!selectedPayment) {
                alert('PLEASE SELECT PAYMENT METHOD');
                return;
            }
            
            // Simulate processing
            const processBtn = document.getElementById('processBtn');
            processBtn.innerHTML = '<div class="loading mr-2"></div>PROCESSING...';
            processBtn.disabled = true;
            
            setTimeout(() => {
                alert(`TRANSFER SUCCESSFUL!\n\nTARGET: ${selectedGame.toUpperCase()}\nID: ${userId}\nPACKAGE: ${selectedDiamonds} ${gameData[selectedGame].currency}\nAMOUNT: Rp ${selectedPrice.toLocaleString('id-ID')}\nPAYMENT: ${selectedPayment}\n\nRESOURCES WILL BE DELIVERED IN 5 MINUTES.`);
                
                // Reset form
                document.getElementById('userId').value = '';
                document.getElementById('userPhone').value = '';
                document.getElementById('selectedPackage').classList.add('hidden');
                
                const packageCards = document.querySelectorAll('#packageGrid .cyber-card');
                packageCards.forEach(card => {
                    card.style.background = 'rgba(0, 0, 0, 0.7)';
                });
                
                const paymentMethods = document.querySelectorAll('.cyber-card');
                paymentMethods.forEach(method => {
                    if (method.onclick && method.onclick.toString().includes('selectPayment')) {
                        method.style.background = 'rgba(0, 0, 0, 0.7)';
                    }
                });
                
                selectedDiamonds = 0;
                selectedPrice = 0;
                selectedPayment = '';
                
                processBtn.innerHTML = 'INITIATE TRANSFER';
                processBtn.disabled = true;
            }, 2000);
        }

        // Check form validity on input change
        document.getElementById('userId').addEventListener('input', checkFormValidity);
    </script>
</body>
</html>
