<html lang="en" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Collexen | Premium Auctions</title>
    
    <!-- Fonts: Playfair Display for Serifs (Luxury), Inter for Sans (Readability) -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600&family=Playfair+Display:ital,wght@0,400;0,600;0,700;1,400&display=swap" rel="stylesheet">
    
    <!-- React & Tailwind -->
    <script crossorigin src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
    <script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Tailwind Configuration -->
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                        serif: ['Playfair Display', 'serif'],
                    },
                    colors: {
                        collexen: {
                            black: '#0a0a0a',
                            dark: '#141414',
                            gray: '#27272a',
                            gold: '#D4AF37', // Premium gold
                            lightGold: '#F3E5AB'
                        }
                    }
                }
            }
        }
    </script>
    <style>
        body { background-color: #0a0a0a; color: #f4f4f5; }
        /* Smooth scrolling for anchor links */
        html { scroll-behavior: smooth; }
        /* Hide scrollbar for category filter but keep functionality */
        .no-scrollbar::-webkit-scrollbar { display: none; }
        .no-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }
        /* Glassmorphism for sticky headers */
        .glass { background: rgba(10, 10, 10, 0.8); backdrop-filter: blur(12px); -webkit-backdrop-filter: blur(12px); }
    </style>
</head>
<body>
    <div id="root"></div>

    <script type="text/babel">
        // --- Icons (Lucide via SVG) ---
        const SearchIcon = () => <svg className="w-5 h-5" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path strokeLinecap="round" strokeLinejoin="round" strokeWidth={1.5} d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" /></svg>;
        const FilterIcon = () => <svg className="w-5 h-5" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path strokeLinecap="round" strokeLinejoin="round" strokeWidth={1.5} d="M3 4a1 1 0 011-1h16a1 1 0 011 1v2.586a1 1 0 01-.293.707l-6.414 6.414a1 1 0 00-.293.707V17l-4 4v-6.586a1 1 0 00-.293-.707L3.293 7.293A1 1 0 013 6.586V4z" /></svg>;
        const UserIcon = () => <svg className="w-5 h-5" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path strokeLinecap="round" strokeLinejoin="round" strokeWidth={1.5} d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" /></svg>;
        const ClockIcon = () => <svg className="w-4 h-4" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path strokeLinecap="round" strokeLinejoin="round" strokeWidth={1.5} d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" /></svg>;

        // --- Mock Data ---
        const AUCTION_HOUSES = ["Tiroche", "Matsart", "Sotheby's Tel Aviv", "Zilbershlag Collection", "Kedem"];
        
        const LOTS = [
            { id: 1, house: "Zilbershlag Collection", title: "Antique Silver Menorah, Warsaw 19th Century", estimate: "$15,000 - $20,000", currentBid: 12500, status: "live", category: "Judaica", image: "https://images.unsplash.com/photo-1601058268499-e52658b8ebf8?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80" },
            { id: 2, house: "Tiroche", title: "Reuven Rubin, Olive Trees in Galilee, Oil on Canvas", estimate: "$80,000 - $120,000", currentBid: 75000, status: "upcoming", date: "Oct 15", category: "Fine Art", image: "https://images.unsplash.com/photo-1577720580479-7d839d829c73?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80" },
            { id: 3, house: "Matsart", title: "Rare Rolex Daytona 'Paul Newman' Ref. 6239", estimate: "$200,000 - $300,000", currentBid: 180000, status: "live", category: "Watches", image: "https://images.unsplash.com/photo-1523170335258-f5ed11844a49?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80" },
            { id: 4, house: "Kedem", title: "First Edition Book of Zohar, Mantua 1558", estimate: "$40,000 - $60,000", currentBid: null, status: "upcoming", date: "Nov 2", category: "Rare Books", image: "https://images.unsplash.com/photo-1544396821-4dd40b938ad3?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80" },
            { id: 5, house: "Sotheby's Tel Aviv", title: "Marc Chagall, Les Amoureux, Lithograph", estimate: "$5,000 - $7,000", currentBid: 4200, status: "live", category: "Fine Art", image: "https://images.unsplash.com/photo-1569171206894-01962da42d54?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80" },
            { id: 6, house: "Zilbershlag Collection", title: "Persian Silk Qum Rug, Signed, Mid 20th C.", estimate: "$8,000 - $12,000", currentBid: 6000, status: "upcoming", date: "Oct 20", category: "Carpets", image: "https://images.unsplash.com/photo-1600166898405-da9535204843?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80" }
        ];

        const CATEGORIES = ["All", "Fine Art", "Judaica", "Watches", "Jewelry", "Rare Books", "Carpets", "Asian Art"];

        // --- Components ---

        const Navbar = () => (
            <nav className="fixed top-0 w-full z-50 glass border-b border-gray-800 transition-all duration-300">
                <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                    <div className="flex justify-between items-center h-20">
                        {/* Logo */}
                        <div className="flex-shrink-0 flex items-center cursor-pointer">
                            <span className="font-serif font-bold text-2xl tracking-widest text-white">COLLEXEN</span>
                        </div>
                        
                        {/* Desktop Menu */}
                        <div className="hidden md:flex space-x-8 items-center">
                            <a href="#" className="text-sm font-medium text-gray-300 hover:text-white transition-colors">Auctions</a>
                            <a href="#" className="text-sm font-medium text-gray-300 hover:text-white transition-colors">Auction Houses</a>
                            <a href="#" className="text-sm font-medium text-gray-300 hover:text-white transition-colors">Sell</a>
                        </div>

                        {/* Search & Profile */}
                        <div className="flex items-center space-x-6">
                            <button className="text-gray-300 hover:text-white transition-colors"><SearchIcon /></button>
                            <div className="h-6 w-px bg-gray-700"></div>
                            <button className="text-gray-300 hover:text-white transition-colors flex items-center space-x-2">
                                <UserIcon />
                                <span className="text-sm hidden sm:block">Sign In</span>
                            </button>
                        </div>
                    </div>
                </div>
            </nav>
        );

        const Hero = () => (
            <div className="relative pt-20 pb-32 flex content-center items-center justify-center min-h-[60vh]">
                <div className="absolute top-0 w-full h-full bg-center bg-cover opacity-30" 
                     style={{backgroundImage: "url('https://images.unsplash.com/photo-1582561424760-0321d6daa24f?ixlib=rb-4.0.3&auto=format&fit=crop&w=2000&q=80')"}}>
                    <span id="blackOverlay" className="w-full h-full absolute opacity-70 bg-gradient-to-b from-transparent to-collexen-black"></span>
                </div>
                <div className="container relative mx-auto px-4 z-10 text-center">
                    <h1 className="text-5xl md:text-7xl font-serif font-bold text-white mb-6 tracking-wide">
                        Discover the <span className="italic text-collexen-gold">Extraordinary</span>
                    </h1>
                    <p className="mt-4 text-lg md:text-xl text-gray-300 max-w-2xl mx-auto font-light">
                        The premier platform connecting collectors with the world's most prestigious auction houses.
                    </p>
                    <div className="mt-10 flex justify-center gap-4">
                        <button className="bg-white text-collexen-black px-8 py-3 font-semibold hover:bg-gray-200 transition-colors">
                            Browse Live Auctions
                        </button>
                    </div>
                </div>
            </div>
        );

        const LotCard = ({ lot }) => (
            <div className="group cursor-pointer flex flex-col h-full bg-collexen-dark border border-gray-800 hover:border-gray-600 transition-all duration-300">
                {/* Image Container */}
                <div className="relative aspect-[4/3] overflow-hidden bg-gray-900">
                    <img src={lot.image} alt={lot.title} className="object-cover w-full h-full group-hover:scale-105 transition-transform duration-700 ease-out opacity-90 group-hover:opacity-100" />
                    
                    {/* Status Badge */}
                    <div className="absolute top-3 left-3 flex gap-2">
                        {lot.status === 'live' ? (
                            <span className="bg-red-600 text-white text-[10px] font-bold px-2 py-1 uppercase tracking-widest flex items-center gap-1 shadow-lg">
                                <span className="w-1.5 h-1.5 rounded-full bg-white animate-pulse"></span>
                                Live Now
                            </span>
                        ) : (
                            <span className="bg-collexen-black text-white border border-gray-600 text-[10px] font-bold px-2 py-1 uppercase tracking-widest shadow-lg">
                                {lot.date}
                            </span>
                        )}
                    </div>
                </div>

                {/* Content */}
                <div className="p-5 flex flex-col flex-grow">
                    <p className="text-collexen-gold text-xs font-semibold uppercase tracking-wider mb-2">{lot.house}</p>
                    <h3 className="text-white font-serif text-lg mb-3 leading-snug flex-grow">{lot.title}</h3>
                    
                    <div className="mt-auto pt-4 border-t border-gray-800">
                        <div className="flex justify-between items-end mb-4">
                            <div>
                                <p className="text-gray-500 text-xs mb-1">Estimate</p>
                                <p className="text-gray-300 text-sm">{lot.estimate}</p>
                            </div>
                            <div className="text-right">
                                <p className="text-gray-500 text-xs mb-1">{lot.status === 'live' ? 'Current Bid' : 'Starting Bid'}</p>
                                <p className="text-white font-medium">{lot.currentBid ? `$${lot.currentBid.toLocaleString()}` : '--'}</p>
                            </div>
                        </div>
                        
                        {/* Action Button */}
                        <button className={`w-full py-2.5 text-sm font-medium transition-colors border ${lot.status === 'live' ? 'bg-white text-black border-white hover:bg-gray-200' : 'bg-transparent text-white border-gray-600 hover:border-white'}`}>
                            {lot.status === 'live' ? 'Join Live Auction' : 'Register to Bid'}
                        </button>
                    </div>
                </div>
            </div>
        );

        const Catalog = () => {
            const [activeCategory, setActiveCategory] = React.useState("All");

            return (
                <section className="py-12 px-4 sm:px-6 lg:px-8 max-w-7xl mx-auto">
                    
                    {/* Filter/Search Bar (The alternative to Bidspirit's clunky search) */}
                    <div className="sticky top-20 z-40 bg-collexen-black/95 py-4 mb-8 border-b border-gray-800">
                        <div className="flex flex-col md:flex-row justify-between items-center gap-4">
                            
                            {/* Categories Scroll */}
                            <div className="w-full md:w-auto overflow-x-auto no-scrollbar pb-2 md:pb-0">
                                <div className="flex space-x-6">
                                    {CATEGORIES.map(cat => (
                                        <button 
                                            key={cat}
                                            onClick={() => setActiveCategory(cat)}
                                            className={`whitespace-nowrap text-sm pb-1 transition-colors ${activeCategory === cat ? 'text-collexen-gold border-b border-collexen-gold font-medium' : 'text-gray-400 hover:text-white'}`}
                                        >
                                            {cat}
                                        </button>
                                    ))}
                                </div>
                            </div>

                            {/* Advanced Filters Button */}
                            <button className="flex items-center space-x-2 text-sm text-gray-300 hover:text-white border border-gray-700 px-4 py-2 rounded-sm w-full md:w-auto justify-center">
                                <FilterIcon />
                                <span>Filter & Sort</span>
                            </button>
                        </div>
                    </div>

                    {/* Section Title */}
                    <div className="mb-8 flex justify-between items-end">
                        <h2 className="text-3xl font-serif text-white">Curated Lots</h2>
                        <a href="#" className="text-collexen-gold text-sm hover:underline">View All Upcoming</a>
                    </div>

                    {/* Grid */}
                    <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6 md:gap-8">
                        {LOTS.filter(lot => activeCategory === "All" || lot.category === activeCategory).map(lot => (
                            <LotCard key={lot.id} lot={lot} />
                        ))}
                    </div>
                    
                    {/* Load More */}
                    <div className="mt-16 text-center">
                        <button className="border border-gray-600 text-white px-8 py-3 text-sm font-medium hover:bg-gray-800 transition-colors">
                            Load More Lots
                        </button>
                    </div>
                </section>
            );
        };

        const Footer = () => (
            <footer className="bg-collexen-dark border-t border-gray-800 pt-16 pb-8 mt-20">
                <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                    <div className="grid grid-cols-1 md:grid-cols-4 gap-12 mb-12">
                        <div className="col-span-1 md:col-span-2">
                            <span className="font-serif font-bold text-2xl tracking-widest text-white mb-4 block">COLLEXEN</span>
                            <p className="text-gray-400 text-sm max-w-sm mb-6">
                                The next generation auction platform. Discover, bid, and acquire extraordinary items from the world's leading auction houses with unparalleled elegance and security.
                            </p>
                        </div>
                        <div>
                            <h4 className="text-white font-medium mb-4 uppercase tracking-wider text-sm">Platform</h4>
                            <ul className="space-y-2 text-sm text-gray-400">
                                <li><a href="#" className="hover:text-collexen-gold transition-colors">Live Auctions</a></li>
                                <li><a href="#" className="hover:text-collexen-gold transition-colors">Auction Houses</a></li>
                                <li><a href="#" className="hover:text-collexen-gold transition-colors">Private Sales</a></li>
                                <li><a href="#" className="hover:text-collexen-gold transition-colors">Sell with Us</a></li>
                            </ul>
                        </div>
                        <div>
                            <h4 className="text-white font-medium mb-4 uppercase tracking-wider text-sm">Support</h4>
                            <ul className="space-y-2 text-sm text-gray-400">
                                <li><a href="#" className="hover:text-collexen-gold transition-colors">How to Bid</a></li>
                                <li><a href="#" className="hover:text-collexen-gold transition-colors">FAQ</a></li>
                                <li><a href="#" className="hover:text-collexen-gold transition-colors">Contact</a></li>
                                <li><a href="#" className="hover:text-collexen-gold transition-colors">Terms of Service</a></li>
                            </ul>
                        </div>
                    </div>
                    <div className="border-t border-gray-800 pt-8 flex flex-col md:flex-row justify-between items-center">
                        <p className="text-gray-500 text-xs">© 2024 Collexen. All rights reserved.</p>
                        <div className="flex space-x-4 mt-4 md:mt-0 text-gray-500 text-xs">
                            <span>Powered by next-gen auction technology.</span>
                        </div>
                    </div>
                </div>
            </footer>
        );

        const App = () => (
            <div className="min-h-screen">
                <Navbar />
                <Hero />
                <Catalog />
                <Footer />
            </div>
        );

        const root = ReactDOM.createRoot(document.getElementById('root'));
        root.render(<App />);
    </script>
</body>
</html>
