<html lang="en" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Collexen | Live Auction Room</title>
    
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Playfair+Display:ital,wght@0,400;0,600;0,700;1,400&family=JetBrains+Mono:wght@400;700&display=swap" rel="stylesheet">
    
    <script crossorigin src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
    <script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <script src="https://cdn.tailwindcss.com"></script>
    
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                        serif: ['Playfair Display', 'serif'],
                        mono: ['JetBrains Mono', 'monospace'],
                    },
                    colors: {
                        collexen: {
                            black: '#0a0a0a',
                            dark: '#141414',
                            gray: '#27272a',
                            gold: '#D4AF37', // Premium gold
                            red: '#ef4444',
                            green: '#10b981'
                        }
                    },
                    animation: {
                        'pulse-fast': 'pulse 1.5s cubic-bezier(0.4, 0, 0.6, 1) infinite',
                        'flash-bg': 'flashBg 0.5s ease-out',
                    },
                    keyframes: {
                        flashBg: {
                            '0%': { backgroundColor: 'rgba(212, 175, 55, 0.3)' },
                            '100%': { backgroundColor: 'transparent' },
                        }
                    }
                }
            }
        }
    </script>
    <style>
        body { background-color: #0a0a0a; color: #f4f4f5; overflow: hidden; }
        ::-webkit-scrollbar { width: 4px; }
        ::-webkit-scrollbar-track { background: #141414; }
        ::-webkit-scrollbar-thumb { background: #3f3f46; border-radius: 4px; }
        ::-webkit-scrollbar-thumb:hover { background: #D4AF37; }
        
        .video-container {
            background: radial-gradient(circle at center, #27272a 0%, #0a0a0a 100%);
        }
        
        /* Smooth transition for price updates */
        .price-update {
            transition: all 0.3s ease;
        }
    </style>
</head>
<body>
    <div id="root"></div>

    <script type="text/babel">
        const VideoOffIcon = () => <svg className="w-12 h-12 text-gray-600" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path strokeLinecap="round" strokeLinejoin="round" strokeWidth={1} d="M15 10l4.553-2.276A1 1 0 0121 8.618v6.764a1 1 0 01-1.447.894L15 14M5 18h8a2 2 0 002-2V8a2 2 0 00-2-2H5a2 2 0 00-2 2v8a2 2 0 002 2z" /></svg>;
        const GavelIcon = () => <svg className="w-5 h-5" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path strokeLinecap="round" strokeLinejoin="round" strokeWidth={1.5} d="M3 6l3 1m0 0l-3 9a5.002 5.002 0 006.001 0M6 7l3 9M6 7l6-2m6 2l3-1m-3 1l-3 9a5.002 5.002 0 006.001 0M18 7l3 9m-3-9l-6-2m0-2v2m0 16V5m0 16H9m3 0h3" /></svg>;
        const ChevronRight = () => <svg className="w-4 h-4" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M9 5l7 7-7 7" /></svg>;

        const CURRENT_LOT = {
            lotNum: "42",
            title: "Pablo Picasso, 'Le Rêve' (Study)",
            estimate: "$500,000 - $700,000",
            startingBid: 350000,
            image: "https://images.unsplash.com/photo-1582561424760-0321d6daa24f?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80"
        };

        // Utility: Format currency
        const formatCurrency = (num) => {
            return new Intl.NumberFormat('en-US', { style: 'currency', currency: 'USD', maximumFractionDigits: 0 }).format(num);
        };

        // Utility: Calculate next increment (Auction math logic)
        const getNextIncrement = (currentPrice) => {
            if (currentPrice < 1000) return 50;
            if (currentPrice < 5000) return 200;
            if (currentPrice < 10000) return 500;
            if (currentPrice < 50000) return 1000;
            if (currentPrice < 100000) return 5000;
            if (currentPrice < 500000) return 10000;
            return 25000;
        };

        const LiveRoom = () => {
            // State Management (The "Brain" of the real-time engine)
            const [currentPrice, setCurrentPrice] = React.useState(CURRENT_LOT.startingBid);
            const [askingPrice, setAskingPrice] = React.useState(CURRENT_LOT.startingBid + getNextIncrement(CURRENT_LOT.startingBid));
            const [bidHistory, setBidHistory] = React.useState([
                { id: 1, type: 'system', message: 'Auctioneer opened the lot at $350,000', time: new Date() }
            ]);
            const [isSold, setIsSold] = React.useState(false);
            const [fairWarning, setFairWarning] = React.useState(false);
            const [winningUser, setWinningUser] = React.useState(null);
            
            const logsEndRef = React.useRef(null);
            const historyContainerRef = React.useRef(null);

            // Auto-scroll to latest bid
            React.useEffect(() => {
                logsEndRef.current?.scrollIntoView({ behavior: "smooth" });
            }, [bidHistory]);

            React.useEffect(() => {
                if (isSold) return;

                // This simulates the CTO's real-time WebSocket connection receiving bids from other people.
                const simulateNetworkTraffic = setInterval(() => {
                    if (Math.random() > 0.7 && !isSold && !fairWarning) { // 30% chance every 3 seconds someone else bids
                        receiveExternalBid();
                    }
                }, 3000);

                // Simulate "Fair Warning" and "Sold" if no one bids for a while
                let warningTimeout, soldTimeout;
                
                const resetClocks = () => {
                    clearTimeout(warningTimeout);
                    clearTimeout(soldTimeout);
                    setFairWarning(false);
                    
                    warningTimeout = setTimeout(() => {
                        if(!isSold) {
                            setFairWarning(true);
                            addLog('system', 'Fair warning... Going once, going twice...');
                            
                            soldTimeout = setTimeout(() => {
                                setIsSold(true);
                                addLog('system', 'SOLD! Hammer down.');
                            }, 4000);
                        }
                    }, 8000); // 8 seconds of silence = fair warning
                };

                resetClocks();

                return () => {
                    clearInterval(simulateNetworkTraffic);
                    clearTimeout(warningTimeout);
                    clearTimeout(soldTimeout);
                };
            }, [currentPrice, isSold]);

            const addLog = (type, message, amount = null, bidder = null) => {
                setBidHistory(prev => [...prev, { id: Date.now(), type, message, amount, bidder, time: new Date() }]);
                // Trigger flash animation
                if (historyContainerRef.current) {
                    historyContainerRef.current.classList.remove('animate-flash-bg');
                    void historyContainerRef.current.offsetWidth; // trigger reflow
                    historyContainerRef.current.classList.add('animate-flash-bg');
                }
            };

            const receiveExternalBid = () => {
                const locations = ["London, UK", "New York, USA", "Geneva, CH", "Floor Bidder", "Telephone Bidder"];
                const bidder = locations[Math.floor(Math.random() * locations.length)];
                
                setCurrentPrice(prev => {
                    const newPrice = askingPrice;
                    setAskingPrice(newPrice + getNextIncrement(newPrice));
                    addLog('bid', `Bid received from ${bidder}`, newPrice, bidder);
                    setWinningUser(bidder);
                    return newPrice;
                });
            };
            const CTOExplanation = () => (
                <div className="absolute inset-0 bg-black/90 z-50 flex items-center justify-center p-8 backdrop-blur-sm">
                    <div className="max-w-2xl bg-collexen-gray p-8 rounded-lg border border-gray-700 shadow-2xl">
                        <h2 className="text-collexen-gold font-serif text-2xl mb-4 border-b border-gray-700 pb-2">CTO Note: Why is this only 339 lines?</h2>
                        <div className="space-y-4 text-gray-300 font-sans text-sm leading-relaxed">
                            <p>You asked a very sharp question: <em>"339 lines of code only for such a complex system?"</em></p>
                            <p>The answer is <strong>No</strong>. This file is just the <strong>Frontend Simulation</strong> (The UI layer). It is the tip of the iceberg.</p>
                            <p>In a real, production-ready system to beat Bidspirit, the architecture would look like this:</p>
                            <ul className="list-disc pl-5 space-y-2 text-gray-400">
                                <li><strong className="text-white">Backend Server (Node.js/Go):</strong> Thousands of lines handling real-time WebSocket connections, ensuring a bid from Tokyo and a bid from Tel Aviv are processed in exact chronological order to prevent race conditions.</li>
                                <li><strong className="text-white">Database Layer (PostgreSQL & Redis):</strong> Complex schemas for managing users, catalogs, lots, and lightning-fast memory storage (Redis) for the live state of the auction.</li>
                                <li><strong className="text-white">Video Streaming Server (WebRTC/HLS):</strong> Dedicated infrastructure to handle low-latency video feeds to thousands of concurrent users without crashing.</li>
                                <li><strong className="text-white">Authentication & Security:</strong> Robust systems to ensure only verified bidders can place half-million dollar bids.</li>
                            </ul>
                            <p className="mt-4 pt-4 border-t border-gray-700 text-xs italic text-gray-500">
                                This 339-line file proves the concept and visualizes the user experience. To build the real engine, we need a full development team and months of backend architecture. Close this note to continue the simulation.
                            </p>
                        </div>
                        <button 
                            onClick={() => document.getElementById('cto-modal').style.display = 'none'}
                            className="mt-6 px-6 py-2 bg-collexen-gold text-black font-bold rounded hover:bg-yellow-600 transition-colors"
                        >
                            Understood, let's bid!
                        </button>
                    </div>
                </div>
            );

            const placeUserBid = () => {
                if (isSold) return;
                const bidAmount = askingPrice;
                setCurrentPrice(bidAmount);
                setAskingPrice(bidAmount + getNextIncrement(bidAmount));
                addLog('user_bid', `You placed a bid`, bidAmount, 'You');
                setWinningUser('You');
            };

            return (
                <div className="h-screen w-full flex flex-col md:flex-row bg-collexen-black text-white font-sans">
                    
                    {/* LEFT COLUMN: Video & Lot Info (70%) */}
                    <div className="flex-1 flex flex-col h-[60vh] md:h-screen border-b md:border-b-0 md:border-r border-gray-800">
                        
                        {/* Header Bar */}
                        <div className="h-14 bg-collexen-dark flex items-center justify-between px-6 border-b border-gray-800">
                            <div className="flex items-center space-x-4">
                                <span className="font-serif font-bold text-xl tracking-wider text-white">COLLEXEN <span className="text-collexen-gold text-xs uppercase font-sans tracking-widest ml-2">Live</span></span>
                            </div>
                            <div className="flex items-center space-x-3">
                                <span className="flex items-center text-xs font-medium bg-red-500/10 text-red-500 px-2 py-1 rounded">
                                    <span className="w-2 h-2 rounded-full bg-red-500 mr-2 animate-pulse-fast"></span>
                                    1,402 Watching
                                </span>
                            </div>
                        </div>

                        {/* Video Area (Simulated) */}
                        <div className="relative flex-1 video-container flex items-center justify-center overflow-hidden">
                            {/* Dummy Video Feed */}
                            <div className="absolute inset-0 opacity-40 mix-blend-luminosity bg-cover bg-center" style={{backgroundImage: "url('https://images.unsplash.com/photo-1600555379765-f5ep8b598b0f?ixlib=rb-4.0.3&auto=format&fit=crop&w=1600&q=80')"}}></div>
                            
                            <div className="z-10 flex flex-col items-center opacity-50">
                                <VideoOffIcon />
                                <p className="mt-2 text-sm uppercase tracking-widest text-gray-400">Live Video Feed</p>
                                <p className="text-xs text-gray-500">Awaiting Auctioneer</p>
                            </div>

                            {/* Overlay Alerts */}
                            {fairWarning && !isSold && (
                                <div className="absolute top-10 left-1/2 transform -translate-x-1/2 bg-collexen-gold text-black px-6 py-2 rounded font-bold uppercase tracking-widest shadow-[0_0_30px_rgba(212,175,55,0.4)] animate-bounce">
                                    Fair Warning
                                </div>
                            )}
                            <div id="cto-modal">
                                <CTOExplanation />
                            </div>

                            {isSold && (
                                <div className="absolute inset-0 bg-black/60 backdrop-blur-sm z-20 flex flex-col items-center justify-center">
                                    <div className="text-center transform transition-all scale-100">
                                        <GavelIcon className="w-16 h-16 mx-auto text-collexen-gold mb-4" />
                                        <h2 className="text-5xl font-serif text-white mb-2">SOLD</h2>
                                        <p className="text-2xl text-collexen-gold font-mono">{formatCurrency(currentPrice)}</p>
                                        <p className="text-gray-400 mt-2">Winner: {winningUser}</p>
                                    </div>
                                </div>
                            )}
                        </div>

                        {}
                        {/* Lot Information Panel */}
                        <div className="h-1/3 bg-collexen-dark border-t border-gray-800 p-6 flex flex-row">
                            <img src={CURRENT_LOT.image} className="h-full w-auto object-cover rounded-md mr-6 border border-gray-700" alt="Lot" />
                            <div className="flex flex-col justify-center flex-1">
                                <p className="text-collexen-gold text-sm font-bold tracking-wider mb-1">LOT {CURRENT_LOT.lotNum}</p>
                                <h1 className="text-2xl md:text-3xl font-serif mb-2 line-clamp-2">{CURRENT_LOT.title}</h1>
                                <p className="text-gray-400 text-sm mb-4">Estimate: {CURRENT_LOT.estimate}</p>
                                
                                {/* Market Depth / Data (CTO Flex: Showing tech depth) */}
                                <div className="flex space-x-6 text-xs text-gray-500 font-mono">
                                    <div><span className="block text-gray-400 mb-1">STARTING BID</span> {formatCurrency(CURRENT_LOT.startingBid)}</div>
                                    <div><span className="block text-gray-400 mb-1">BIDS PLACED</span> {bidHistory.filter(b => b.type.includes('bid')).length}</div>
                                    <div><span className="block text-gray-400 mb-1">LATENCY</span> <span className="text-green-500">12ms</span></div>
                                </div>
                            </div>
                        </div>
                    </div>

                    {}
                    {/* RIGHT COLUMN: Bid Console (30%) */}
                    <div className="w-full md:w-[400px] lg:w-[450px] flex flex-col h-[40vh] md:h-screen bg-[#0f0f0f] relative shadow-[-10px_0_30px_rgba(0,0,0,0.5)]">
                        
                        {/* Price Display */}
                        <div className="p-6 bg-[#141414] border-b border-gray-800 flex flex-col items-center justify-center relative z-10 shadow-lg">
                            <p className="text-gray-400 text-xs uppercase tracking-widest mb-1">Current Price</p>
                            <div className="text-5xl font-mono font-bold text-white mb-2 price-update" key={currentPrice}>
                                {formatCurrency(currentPrice)}
                            </div>
                            <div className="text-sm font-medium text-gray-500">
                                {winningUser === 'You' ? (
                                    <span className="text-green-500">Winning: You</span>
                                ) : winningUser ? (
                                    <span>Winning: {winningUser}</span>
                                ) : (
                                    <span>Awaiting bids...</span>
                                )}
                            </div>
                        </div>

                        {/* Bid History Feed */}
                        <div className="flex-1 overflow-y-auto p-4 space-y-3" ref={historyContainerRef}>
                            {bidHistory.map((log) => (
                                <div key={log.id} className={`p-3 rounded-md text-sm border-l-2 ${
                                    log.type === 'user_bid' ? 'bg-green-900/20 border-green-500' :
                                    log.type === 'bid' ? 'bg-collexen-gray/50 border-collexen-gold' :
                                    'bg-transparent border-transparent text-gray-500 italic text-center'
                                }`}>
                                    {log.type === 'system' ? (
                                        <p>{log.message}</p>
                                    ) : (
                                        <div className="flex justify-between items-center">
                                            <div className="flex flex-col">
                                                <span className="font-mono text-xs text-gray-400">{log.time.toLocaleTimeString([], {hour12:false, hour:'2-digit', minute:'2-digit', second:'2-digit'})}</span>
                                                <span className={log.type === 'user_bid' ? 'text-green-400 font-bold' : 'text-gray-200'}>{log.bidder}</span>
                                            </div>
                                            <span className="font-mono font-bold text-base">{formatCurrency(log.amount)}</span>
                                        </div>
                                    )}
                                </div>
                            ))}
                            <div ref={logsEndRef} />
                        </div>

                        {/* Action Area (The Big Button) */}
                        <div className="p-6 bg-[#141414] border-t border-gray-800">
                            {isSold ? (
                                <button disabled className="w-full py-4 bg-gray-800 text-gray-500 font-bold text-lg rounded uppercase tracking-wider cursor-not-allowed">
                                    Lot Closed
                                </button>
                            ) : (
                                <div className="space-y-3">
                                    <div className="flex justify-between text-sm mb-2">
                                        <span className="text-gray-400">Asking:</span>
                                        <span className="font-mono text-collexen-gold font-bold">{formatCurrency(askingPrice)}</span>
                                    </div>
                                    <button 
                                        onClick={placeUserBid}
                                        disabled={winningUser === 'You'}
                                        className={`w-full py-4 rounded text-lg font-bold uppercase tracking-wider shadow-lg transition-all transform active:scale-95 flex items-center justify-center group ${
                                            winningUser === 'You' 
                                            ? 'bg-green-600/20 text-green-500 border border-green-600/50 cursor-not-allowed' 
                                            : 'bg-white text-black hover:bg-gray-200 shadow-[0_0_15px_rgba(255,255,255,0.2)]'
                                        }`}
                                    >
                                        {winningUser === 'You' ? 'You are highest bidder' : `BID ${formatCurrency(askingPrice)}`}
                                        {!winningUser || winningUser !== 'You' ? <ChevronRight /> : null}
                                    </button>
                                </div>
                            )}
                        </div>
                    </div>
                </div>
            );
        };

        const root = ReactDOM.createRoot(document.getElementById('root'));
        root.render(<LiveRoom />);
    </script>
</body>
</html>
