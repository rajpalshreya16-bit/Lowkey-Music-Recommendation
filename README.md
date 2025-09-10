<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chill Vibes - Music Discovery for Teens</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, sans-serif;
            background: linear-gradient(135deg, #d4a574 0%, #8b6244 100%);
            min-height: 100vh;
            color: #3e2723;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        header {
            text-align: center;
            padding: 40px 0;
            color: #f5e6d3;
        }

        h1 {
            font-size: 3em;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(62, 39, 35, 0.3);
            animation: fadeInDown 0.8s ease;
            font-weight: 800;
            letter-spacing: -1px;
        }

        .subtitle {
            font-size: 1.2em;
            opacity: 0.95;
            animation: fadeInUp 0.8s ease;
            color: #fdf6ec;
        }

        .controls {
            background: #f5e6d3;
            border-radius: 20px;
            padding: 30px;
            margin-bottom: 30px;
            box-shadow: 0 10px 40px rgba(62, 39, 35, 0.2);
            animation: slideIn 0.6s ease;
            border: 1px solid rgba(139, 98, 68, 0.1);
        }

        .search-container {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
        }

        input[type="text"] {
            flex: 1;
            padding: 12px 20px;
            border: 2px solid #d4a574;
            border-radius: 50px;
            font-size: 16px;
            transition: all 0.3s ease;
            background: #fdf6ec;
            color: #3e2723;
        }

        input[type="text"]::placeholder {
            color: #8b6244;
            opacity: 0.6;
        }

        input[type="text"]:focus {
            outline: none;
            border-color: #8b6244;
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(139, 98, 68, 0.2);
            background: white;
        }

        .genre-filters {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin-bottom: 20px;
        }

        .genre-btn {
            padding: 8px 20px;
            border: 2px solid #8b6244;
            background: #fdf6ec;
            color: #5d4037;
            border-radius: 25px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 14px;
            font-weight: 600;
        }

        .genre-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(139, 98, 68, 0.3);
            background: #8b6244;
            color: #f5e6d3;
        }

        .genre-btn.active {
            background: linear-gradient(135deg, #6f4e37 0%, #3e2723 100%);
            color: #f5e6d3;
            transform: scale(1.05);
            border-color: #3e2723;
        }

        .view-toggle {
            display: flex;
            gap: 10px;
            justify-content: center;
            margin-bottom: 20px;
        }

        .view-btn {
            padding: 10px 25px;
            background: linear-gradient(135deg, #8b6244 0%, #5d4037 100%);
            color: #f5e6d3;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: 600;
            transition: all 0.3s ease;
        }

        .view-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(93, 64, 55, 0.4);
        }

        .view-btn.inactive {
            background: #c8b09a;
            color: #8b6244;
        }

        .music-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 25px;
            margin-bottom: 30px;
        }

        .music-card {
            background: #f5e6d3;
            border-radius: 15px;
            overflow: hidden;
            box-shadow: 0 5px 20px rgba(62, 39, 35, 0.15);
            transition: all 0.3s ease;
            animation: fadeIn 0.5s ease;
            position: relative;
            border: 1px solid rgba(139, 98, 68, 0.1);
        }

        .music-card:hover {
            transform: translateY(-5px) scale(1.02);
            box-shadow: 0 15px 40px rgba(62, 39, 35, 0.25);
        }

        .album-cover {
            height: 200px;
            background: linear-gradient(135deg, #8b6244 0%, #5d4037 100%);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 60px;
            position: relative;
            overflow: hidden;
        }

        .album-cover img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .album-cover-placeholder {
            font-size: 48px;
            filter: grayscale(20%);
        }

        .album-cover::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: linear-gradient(45deg, transparent, rgba(245, 230, 211, 0.1), transparent);
            transform: rotate(45deg);
            animation: shimmer 3s infinite;
        }

        .music-info {
            padding: 20px;
            background: #fdf6ec;
        }

        .song-title {
            font-size: 18px;
            font-weight: 700;
            color: #3e2723;
            margin-bottom: 5px;
        }

        .artist {
            color: #6f4e37;
            font-size: 14px;
            margin-bottom: 8px;
        }

        .genre-tag {
            display: inline-block;
            padding: 4px 12px;
            background: linear-gradient(135deg, #d4a574 0%, #c8b09a 100%);
            color: #3e2723;
            border-radius: 15px;
            font-size: 12px;
            font-weight: 600;
            margin-bottom: 15px;
        }

        .card-actions {
            display: flex;
            justify-content: space-between;
            align-items: center;
            gap: 10px;
        }

        .like-btn {
            background: none;
            border: none;
            cursor: pointer;
            font-size: 24px;
            transition: all 0.3s ease;
            padding: 5px;
        }

        .like-btn:hover {
            transform: scale(1.2);
        }

        .like-btn.liked {
            animation: heartBeat 0.6s ease;
        }

        .spotify-btn {
            padding: 8px 16px;
            background: #1DB954;
            color: white;
            border: none;
            border-radius: 20px;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.3s ease;
            text-decoration: none;
            display: inline-flex;
            align-items: center;
            gap: 6px;
            font-size: 14px;
        }

        .spotify-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(29, 185, 84, 0.4);
            background: #1ed760;
        }

        .play-btn {
            padding: 8px 20px;
            background: linear-gradient(135deg, #8b6244 0%, #5d4037 100%);
            color: #f5e6d3;
            border: none;
            border-radius: 20px;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.3s ease;
        }

        .play-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(139, 98, 68, 0.4);
        }

        .vibe-meter {
            position: absolute;
            top: 10px;
            right: 10px;
            background: rgba(253, 246, 236, 0.95);
            padding: 5px 10px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: 700;
            color: #6f4e37;
            box-shadow: 0 2px 10px rgba(62, 39, 35, 0.1);
        }

        .stats {
            background: #f5e6d3;
            border-radius: 20px;
            padding: 30px;
            margin-bottom: 30px;
            box-shadow: 0 10px 40px rgba(62, 39, 35, 0.2);
            text-align: center;
            border: 1px solid rgba(139, 98, 68, 0.1);
        }

        .stats h2 {
            color: #3e2723;
            margin-bottom: 20px;
            font-weight: 700;
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 20px;
        }

        .stat-item {
            padding: 15px;
            background: linear-gradient(135deg, #8b6244 0%, #5d4037 100%);
            border-radius: 15px;
            color: #f5e6d3;
        }

        .stat-number {
            font-size: 28px;
            font-weight: 700;
            margin-bottom: 5px;
        }

        .stat-label {
            font-size: 14px;
            opacity: 0.95;
        }

        .empty-state {
            text-align: center;
            padding: 60px 20px;
            color: #f5e6d3;
        }

        .empty-state h3 {
            font-size: 24px;
            margin-bottom: 10px;
        }

        @keyframes fadeInDown {
            from {
                opacity: 0;
                transform: translateY(-20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateX(-20px);
            }
            to {
                opacity: 1;
                transform: translateX(0);
            }
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
            }
            to {
                opacity: 1;
            }
        }

        @keyframes heartBeat {
            0%, 100% {
                transform: scale(1);
            }
            50% {
                transform: scale(1.3);
            }
        }

        @keyframes shimmer {
            0% {
                transform: translateX(-100%) rotate(45deg);
            }
            100% {
                transform: translateX(100%) rotate(45deg);
            }
        }

        @media (max-width: 768px) {
            h1 {
                font-size: 2em;
            }
            
            .music-grid {
                grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
                gap: 15px;
            }
            
            .genre-filters {
                justify-content: center;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>☕ Chill Vibes</h1>
            <p class="subtitle">Discover lowkey gems that hit different</p>
        </header>

        <div class="controls">
            <div class="search-container">
                <input type="text" id="searchInput" placeholder="Search for songs, artists, or vibes...">
            </div>
            
            <div class="genre-filters" id="genreFilters">
                <button class="genre-btn active" data-genre="all">All Vibes</button>
                <button class="genre-btn" data-genre="indie">Indie</button>
                <button class="genre-btn" data-genre="bedroom-pop">Bedroom Pop</button>
                <button class="genre-btn" data-genre="lofi">Lo-Fi</button>
                <button class="genre-btn" data-genre="alt-rnb">Alt R&B</button>
                <button class="genre-btn" data-genre="dream-pop">Dream Pop</button>
                <button class="genre-btn" data-genre="soft-rock">Soft Rock</button>
                <button class="genre-btn" data-genre="chill-rap">Chill Rap</button>
            </div>

            <div class="view-toggle">
                <button class="view-btn" id="allSongsBtn">All Songs</button>
                <button class="view-btn inactive" id="recommendedBtn">For You</button>
                <button class="view-btn inactive" id="favoritesBtn">Your Library</button>
            </div>
        </div>

        <div class="stats">
            <h2>Your Vibe Check</h2>
            <div class="stats-grid">
                <div class="stat-item">
                    <div class="stat-number" id="totalSongs">45</div>
                    <div class="stat-label">Hidden Gems</div>
                </div>
                <div class="stat-item">
                    <div class="stat-number" id="likedSongs">0</div>
                    <div class="stat-label">Saved Songs</div>
                </div>
                <div class="stat-item">
                    <div class="stat-number" id="topGenre">Indie</div>
                    <div class="stat-label">Your Vibe</div>
                </div>
                <div class="stat-item">
                    <div class="stat-number" id="vibeScore">0</div>
                    <div class="stat-label">Vibe Score</div>
                </div>
            </div>
        </div>

        <div class="music-grid" id="musicGrid">
            <!-- Music cards will be dynamically inserted here -->
        </div>

        <div class="empty-state" id="emptyState" style="display: none;">
            <h3>No songs found</h3>
            <p>Try adjusting your filters or search terms</p>
        </div>
    </div>

    <script>
        // Lowkey teenage-focused music database with Spotify links
        const musicDatabase = [
            { id: 1, title: "Apocalypse", artist: "Cigarettes After Sex", genre: "dream-pop", emoji: "🌙", vibe: 95, spotify: "https://open.spotify.com/track/0yc6Gst2xkRu0eMLeRMGCX" },
            { id: 2, title: "Lover", artist: "Taylor Swift", genre: "indie", emoji: "💝", vibe: 88, spotify: "https://open.spotify.com/track/1dGr1c8CrMLDpV6mPbImSI" },
            { id: 3, title: "We Fell in Love in October", artist: "Girl in Red", genre: "bedroom-pop", emoji: "🍂", vibe: 92, spotify: "https://open.spotify.com/track/0W4Kpfp1w2xNY5iCcP2JJ" },
            { id: 4, title: "Sweater Weather", artist: "The Neighbourhood", genre: "alt-rnb", emoji: "🧥", vibe: 94, spotify: "https://open.spotify.com/track/2QjOHCTQ1Jl3zawyYOpxh6" },
            { id: 5, title: "Space Song", artist: "Beach House", genre: "dream-pop", emoji: "🌌", vibe: 90, spotify: "https://open.spotify.com/track/7H0ya83CMmgFcOhw0UB6ow" },
            { id: 6, title: "Flightless Bird, American Mouth", artist: "Iron & Wine", genre: "indie", emoji: "🕊️", vibe: 87, spotify: "https://open.spotify.com/track/2GiJYvgVaD2HtM8GqD9EgQ" },
            { id: 7, title: "Coffee", artist: "Beabadoobee", genre: "bedroom-pop", emoji: "☕", vibe: 89, spotify: "https://open.spotify.com/track/4HBZA5flZLE435QTztThqH" },
            { id: 8, title: "Death Bed", artist: "Powfu ft. Beabadoobee", genre: "lofi", emoji: "🛏️", vibe: 91, spotify: "https://open.spotify.com/track/7eJMfftS33KTjuF7lTsMCx" },
            { id: 9, title: "Heather", artist: "Conan Gray", genre: "bedroom-pop", emoji: "💔", vibe: 93, spotify: "https://open.spotify.com/track/4xqrdfXkTW4T0RauPLv3WA" },
            { id: 10, title: "Are You Bored Yet?", artist: "Wallows ft. Clairo", genre: "indie", emoji: "🎮", vibe: 88, spotify: "https://open.spotify.com/track/7FNnA9vBm5EKtRhlNhh3S" },
            { id: 11, title: "Sofia", artist: "Clairo", genre: "bedroom-pop", emoji: "💕", vibe: 90, spotify: "https://open.spotify.com/track/7B3z0ySL9Rr0XvZEAjWZzM" },
            { id: 12, title: "Good Days", artist: "SZA", genre: "alt-rnb", emoji: "☀️", vibe: 89, spotify: "https://open.spotify.com/track/3YJJjQPAbDT7mGpX3WtQ9A" },
            { id: 13, title: "Telephones", artist: "Vacations", genre: "dream-pop", emoji: "📞", vibe: 86, spotify: "https://open.spotify.com/track/1IJxbEXY3CYfW0Cp1pBwPp" },
            { id: 14, title: "Chamber of Reflection", artist: "Mac DeMarco", genre: "indie", emoji: "🪞", vibe: 91, spotify: "https://open.spotify.com/track/7H7NyZ3G075GqPx2evsfeb" },
            { id: 15, title: "Bags", artist: "Clairo", genre: "bedroom-pop", emoji: "👜", vibe: 87, spotify: "https://open.spotify.com/track/5SWnsxjhdcEDc7LJjq" },
            { id: 16, title: "Line Without a Hook", artist: "Ricky Montgomery", genre: "indie", emoji: "🎣", vibe: 92, spotify: "https://open.spotify.com/track/1UHS8Rf6h5Ar3CDWRd3wjF" },
            { id: 17, title: "Falling Behind", artist: "Laufey", genre: "soft-rock", emoji: "🎹", vibe: 85, spotify: "https://open.spotify.com/track/4aI9aW6HvARKJ2rzu0L4v" },
            { id: 18, title: "From the Start", artist: "Laufey", genre: "soft-rock", emoji: "💌", vibe: 88, spotify: "https://open.spotify.com/track/3VF68KZqC7SlYg5Tqv0Wu" },
            { id: 19, title: "Bubble Gum", artist: "Clairo", genre: "bedroom-pop", emoji: "🫧", vibe: 84, spotify: "https://open.spotify.com/track/3mRLHiSHYtC8Hk7bzZdUs1" },
            { id: 20, title: "Golden", artist: "Harry Styles", genre: "indie", emoji: "✨", vibe: 86, spotify: "https://open.spotify.com/track/7LVHVU3tWfcxj5aiPFEW4Q" },
            { id: 21, title: "Heat Waves", artist: "Glass Animals", genre: "alt-rnb", emoji: "🌊", vibe: 90, spotify: "https://open.spotify.com/track/02MWAffLxlfxAUY7c5dvx" },
            { id: 22, title: "Pluto Projector", artist: "Rex Orange County", genre: "bedroom-pop", emoji: "🪐", vibe: 89, spotify: "https://open.spotify.com/track/3LgWsmilsrWXiPYQFRD0T" },
            { id: 23, title: "See You Again", artist: "Tyler, The Creator ft. Kali Uchis", genre: "chill-rap", emoji: "🌻", vibe: 87, spotify: "https://open.spotify.com/track/7KA4W4McWYRpgf0fWsJZWB" },
            { id: 24, title: "Lost in the Light", artist: "Bahamas", genre: "soft-rock", emoji: "💡", vibe: 83, spotify: "https://open.spotify.com/track/5M4yti0QxgqJieUYfExnE" },
            { id: 25, title: "Freaks", artist: "Surf Curse", genre: "indie", emoji: "👻", vibe: 91, spotify: "https://open.spotify.com/track/1Dwfg5K0vVYU6KUPRqS4J" },
            { id: 26, title: "Mr. Brightside", artist: "The Killers", genre: "soft-rock", emoji: "🌟", vibe: 85, spotify: "https://open.spotify.com/track/7oK9VyNzrYvRFo7nQEYkWN" },
            { id: 27, title: "Electric Feel", artist: "MGMT", genre: "indie", emoji: "⚡", vibe: 88, spotify: "https://open.spotify.com/track/3FtYbEfBqAlGO46NUDQSAt" },
            { id: 28, title: "Pretty Boy", artist: "The Neighbourhood", genre: "alt-rnb", emoji: "🖤", vibe: 86, spotify: "https://open.spotify.com/track/0PE0u6lXrcI0S2BFUBkwKq" },
            { id: 29, title: "Television / So Far So Good", artist: "Rex Orange County", genre: "bedroom-pop", emoji: "📺", vibe: 84, spotify: "https://open.spotify.com/track/5GUYJTQap5F3RDQiCOJhrS" },
            { id: 30, title: "Borderline", artist: "Tame Impala", genre: "dream-pop", emoji: "🌈", vibe: 89, spotify: "https://open.spotify.com/track/2g1EakEaW7jVkMrLvpeP3j" },
            { id: 31, title: "ivy", artist: "Frank Ocean", genre: "alt-rnb", emoji: "🌿", vibe: 93, spotify: "https://open.spotify.com/track/2ZWlPOoWh0626oTaHrnl2a" },
            { id: 32, title: "Dreams Tonite", artist: "Alvvays", genre: "dream-pop", emoji: "💭", vibe: 87, spotify: "https://open.spotify.com/track/3NhhyodlOuLvmj9Uu1Ac0C" },
            { id: 33, title: "Nights", artist: "Frank Ocean", genre: "alt-rnb", emoji: "🌃", vibe: 92, spotify: "https://open.spotify.com/track/7eqoqGkKwgOaWNNHx90uEZ" },
            { id: 34, title: "Loving Is Easy", artist: "Rex Orange County", genre: "bedroom-pop", emoji: "💚", vibe: 85, spotify: "https://open.spotify.com/track/1pKLBKgFnfeMkUC7gEZ8yC" },
            { id: 35, title: "Sunflower", artist: "Rex Orange County", genre: "bedroom-pop", emoji: "🌻", vibe: 88, spotify: "https://open.spotify.com/track/4jFwi7pUXrKQkdKKw2kL91" },
            { id: 36, title: "Best Friend", artist: "Rex Orange County", genre: "bedroom-pop", emoji: "👯", vibe: 86, spotify: "https://open.spotify.com/track/5rbagdVPfSdpxpRJpCVFl3" },
            { id: 37, title: "Moonlight", artist: "Kali Uchis", genre: "alt-rnb", emoji: "🌙", vibe: 90, spotify: "https://open.spotify.com/track/0J7U24vlOOIeMpuaO6Q85A" },
            { id: 38, title: "After the Storm", artist: "Kali Uchis ft. Tyler, The Creator", genre: "alt-rnb", emoji: "⛈️", vibe: 89, spotify: "https://open.spotify.com/track/0NwKP1PY3uCQJFQWKf51aE" },
            { id: 39, title: "Lover Is a Day", artist: "Cuco", genre: "lofi", emoji: "💖", vibe: 84, spotify: "https://open.spotify.com/track/5k6RM5WXyW0jxJJMkQAHr0" },
            { id: 40, title: "Lo Que Siento", artist: "Cuco", genre: "lofi", emoji: "💫", vibe: 87, spotify: "https://open.spotify.com/track/6dMw79lJO0vPz8PvJ5cBIH" },
            { id: 41, title: "Melting", artist: "Kali Uchis", genre: "alt-rnb", emoji: "🍯", vibe: 86, spotify: "https://open.spotify.com/track/1MsxVZu86qRssH5sJbQcg" },
            { id: 42, title: "Pretty Girl", artist: "Clairo", genre: "bedroom-pop", emoji: "🎀", vibe: 88, spotify: "https://open.spotify.com/track/2RDyg00OREjcJbYMVsQPQ" },
            { id: 43, title: "4EVER", artist: "Clairo", genre: "bedroom-pop", emoji: "♾️", vibe: 85, spotify: "https://open.spotify.com/track/0VF7YLIxSQKyNiFL1Cj0J" },
            { id: 44, title: "Amoeba", artist: "Clairo", genre: "bedroom-pop", emoji: "🦠", vibe: 83, spotify: "https://open.spotify.com/track/17Iy1lDaFVE0B0vniYgaZY" },
            { id: 45, title: "Softly", artist: "Clairo", genre: "bedroom-pop", emoji: "🌸", vibe: 90, spotify: "https://open.spotify.com/track/7HhuBDCeiQWDOixtNxSRuN" }
        ];

        // User preferences and state
        let userPreferences = {
            likedSongs: new Set(),
            genrePreferences: {},
            currentView: 'all',
            selectedGenre: 'all'
        };

        // Initialize the app
        function init() {
            renderMusicGrid(musicDatabase);
            setupEventListeners();
            updateStats();
        }

        // Setup event listeners
        function setupEventListeners() {
            // Search functionality
            document.getElementById('searchInput').addEventListener('input', (e) => {
                const query = e.target.value.toLowerCase();
                const filtered = musicDatabase.filter(song => 
                    song.title.toLowerCase().includes(query) ||
                    song.artist.toLowerCase().includes(query) ||
                    song.genre.toLowerCase().includes(query)
                );
                renderMusicGrid(filtered);
            });

            // Genre filter buttons
            document.querySelectorAll('.genre-btn').forEach(btn => {
                btn.addEventListener('click', (e) => {
                    document.querySelectorAll('.genre-btn').forEach(b => b.classList.remove('active'));
                    e.target.classList.add('active');
                    
                    const genre = e.target.dataset.genre;
