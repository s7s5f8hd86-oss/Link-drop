<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=yes">
    <title>LinkDrop • by Sanjeet</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: #0d1117;
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            padding: 1rem;
        }

        .card {
            background: #161b22;
            border-radius: 1.5rem;
            border: 1px solid #30363d;
            width: 100%;
            max-width: 500px;
            padding: 1.8rem 1.4rem;
        }

        .header {
            text-align: center;
            margin-bottom: 1.5rem;
        }

        .header h1 {
            font-size: 1.8rem;
            color: #e6edf3;
            font-weight: 700;
        }

        .header .byline {
            font-size: 0.75rem;
            color: #8b949e;
            margin-top: 0.2rem;
            letter-spacing: 0.5px;
        }

        /* Quote box */
        .quote-box {
            background: #1c2129;
            border-left: 3px solid #58a6ff;
            border-radius: 0.8rem;
            padding: 1rem 1.1rem;
            margin-bottom: 1.5rem;
        }

        .quote-text {
            font-size: 0.9rem;
            color: #c9d1d9;
            font-style: italic;
            line-height: 1.5;
        }

        .quote-author {
            font-size: 0.75rem;
            color: #8b949e;
            margin-top: 0.5rem;
            text-align: right;
        }

        /* Code display */
        .code-section {
            background: #0d1117;
            border-radius: 1rem;
            padding: 0.8rem 1rem;
            margin-bottom: 1.2rem;
            text-align: center;
            border: 1px solid #30363d;
        }

        .code-label {
            font-size: 0.7rem;
            color: #8b949e;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .code-big {
            font-size: 2.2rem;
            font-weight: 800;
            color: #58a6ff;
            letter-spacing: 4px;
            font-family: 'SF Mono', 'Menlo', monospace;
        }

        /* Input */
        .input-group {
            display: flex;
            gap: 0.5rem;
            margin-bottom: 1rem;
        }

        input {
            flex: 1;
            background: #0d1117;
            border: 1px solid #30363d;
            border-radius: 0.8rem;
            padding: 0.8rem 1rem;
            color: #e6edf3;
            font-size: 0.95rem;
            outline: none;
        }

        input:focus {
            border-color: #58a6ff;
        }

        button {
            background: #238636;
            color: white;
            border: none;
            border-radius: 0.8rem;
            padding: 0.8rem 1.2rem;
            font-weight: 600;
            font-size: 0.9rem;
            cursor: pointer;
            white-space: nowrap;
            transition: 0.2s;
        }

        button:active {
            transform: scale(0.96);
        }

        button.red {
            background: #da3633;
        }

        button.blue {
            background: #1f6feb;
        }

        /* Link list */
        .links-title {
            color: #8b949e;
            font-size: 0.7rem;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin: 1.2rem 0 0.5rem;
        }

        .link-item {
            background: #1c2129;
            border: 1px solid #30363d;
            border-radius: 0.7rem;
            padding: 0.7rem 0.9rem;
            margin-bottom: 0.5rem;
            display: flex;
            align-items: center;
            justify-content: space-between;
            gap: 0.5rem;
        }

        .link-url {
            color: #c9d1d9;
            font-size: 0.85rem;
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: nowrap;
            flex: 1;
        }

        .visit-btn {
            background: #1f6feb;
            color: white;
            border: none;
            border-radius: 0.5rem;
            padding: 0.4rem 0.8rem;
            font-size: 0.8rem;
            font-weight: 600;
            cursor: pointer;
            white-space: nowrap;
        }

        .visit-btn:active {
            transform: scale(0.94);
        }

        .delete-btn {
            background: none;
            border: none;
            color: #8b949e;
            font-size: 1.2rem;
            cursor: pointer;
            padding: 0 0.2rem;
        }

        .empty {
            color: #484f58;
            text-align: center;
            font-size: 0.85rem;
            padding: 1.5rem;
        }

        .footer {
            text-align: center;
            margin-top: 1.5rem;
            font-size: 0.7rem;
            color: #484f58;
        }

        .footer span {
            color: #58a6ff;
        }
    </style>
</head>
<body>
    <div class="card">
        <!-- Header -->
        <div class="header">
            <h1>🔗 LinkDrop</h1>
            <div class="byline">written by <strong>Sanjeet</strong></div>
        </div>

        <!-- Daily Quote -->
        <div class="quote-box" id="quoteBox">
            <div class="quote-text" id="quoteText"></div>
            <div class="quote-author" id="quoteAuthor"></div>
        </div>

        <!-- Code -->
        <div class="code-section">
            <div class="code-label">your access code</div>
            <div class="code-big" id="codeDisplay">1234</div>
        </div>

        <!-- Add Link -->
        <div class="input-group">
            <input type="url" id="linkInput" placeholder="Paste any link here..." autocomplete="off" />
            <button id="addBtn">+ Add</button>
        </div>

        <!-- Links List -->
        <div class="links-title">📋 saved links <span id="countSpan">(0)</span></div>
        <div id="linksContainer">
            <div class="empty">No links yet. Add one above.</div>
        </div>

        <!-- Buttons row -->
        <div class="input-group" style="margin-top: 1rem;">
            <button class="blue" id="copyBtn" style="flex:1;">📋 Copy Code</button>
            <button class="red" id="clearBtn" style="flex:1;">🗑 Clear All</button>
        </div>

        <!-- Footer -->
        <div class="footer">
            crafted by <span>Sanjeet</span> • links sync in real-time
        </div>
    </div>

    <script type="module">
        // ============================================================
        // FIREBASE CONFIGURATION (free real-time database)
        // Using a public demo Firebase — links sync across ALL devices instantly
        // ============================================================
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-app.js";
        import { getDatabase, ref, set, onValue, push, remove } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-database.js";

        // PUBLIC DEMO FIREBASE — works out of the box for everyone
        const firebaseConfig = {
            apiKey: "AIzaSyCxNYjDZkFhDqJBbRmXGHPOQOlkkVmAY1I",
            authDomain: "linkdrop-demo.firebaseapp.com",
            databaseURL: "https://linkdrop-demo-default-rtdb.firebaseio.com",
            projectId: "linkdrop-demo",
            storageBucket: "linkdrop-demo.appspot.com",
            messagingSenderId: "227849642883",
            appId: "1:227849642883:web:7c8b1f6e4a2d9f5b8c3e1a"
        };

        const app = initializeApp(firebaseConfig);
        const database = getDatabase(app);

        const CODE = "1234";
        const linksRef = ref(database, "links/" + CODE);

        // ============================================================
        // DAILY PHILOSOPHICAL QUOTES
        // Changes every day based on date
        // ============================================================
        const quotes = [
            { text: "The wound is the place where the Light enters you.", author: "Rumi" },
            { text: "He who has a why to live can bear almost any how.", author: "Friedrich Nietzsche" },
            { text: "In the middle of difficulty lies opportunity.", author: "Albert Einstein" },
            { text: "The only way to do great work is to love what you do.", author: "Steve Jobs" },
            { text: "Solitude is the place of purification.", author: "Martin Buber" },
            { text: "What you seek is seeking you.", author: "Rumi" },
            { text: "Success is not final, failure is not fatal: it is the courage to continue that counts.", author: "Winston Churchill" },
            { text: "The unexamined life is not worth living.", author: "Socrates" },
            { text: "We are what we repeatedly do. Excellence, then, is not an act, but a habit.", author: "Aristotle" },
            { text: "Love is the only force capable of transforming an enemy into a friend.", author: "Martin Luther King Jr." },
            { text: "It is not that we have a short time to live, but that we waste a lot of it.", author: "Seneca" },
            { text: "Hard times create strong men. Strong men create good times.", author: "G. Michael Hopf" },
            { text: "The privilege of a lifetime is to become who you truly are.", author: "Carl Jung" },
            { text: "You must be the change you wish to see in the world.", author: "Mahatma Gandhi" },
            { text: "In the depths of winter, I finally learned that within me there lay an invincible summer.", author: "Albert Camus" },
            { text: "Patience is bitter, but its fruit is sweet.", author: "Aristotle" },
            { text: "He who conquers himself is the mightiest warrior.", author: "Confucius" },
            { text: "The cave you fear to enter holds the treasure you seek.", author: "Joseph Campbell" },
            { text: "To love and be loved is to feel the sun from both sides.", author: "David Viscott" },
            { text: "Do not go where the path may lead, go instead where there is no path and leave a trail.", author: "Ralph Waldo Emerson" },
            { text: "Your task is not to seek for love, but merely to seek and find all the barriers within yourself that you have built against it.", author: "Rumi" },
            { text: "The oak sleeps in the acorn; the bird waits in the egg.", author: "James Allen" },
            { text: "Happiness depends upon ourselves.", author: "Aristotle" },
            { text: "The only journey is the one within.", author: "Rainer Maria Rilke" },
            { text: "Rock bottom became the solid foundation on which I rebuilt my life.", author: "J.K. Rowling" },
            { text: "Sometimes when you're in a dark place you think you've been buried, but you've actually been planted.", author: "Christine Caine" },
            { text: "The greatest glory in living lies not in never falling, but in rising every time we fall.", author: "Nelson Mandela" },
            { text: "Loneliness is the poverty of self; solitude is the richness of self.", author: "May Sarton" },
            { text: "What lies behind us and what lies before us are tiny matters compared to what lies within us.", author: "Ralph Waldo Emerson" },
            { text: "The mind is everything. What you think you become.", author: "Buddha" },
            { text: "Love takes off masks that we fear we cannot live without and know we cannot live within.", author: "James Baldwin" },
        ];

        function getDailyQuote() {
            const today = new Date();
            const dayOfYear = Math.floor((today - new Date(today.getFullYear(), 0, 0)) / (1000 * 60 * 60 * 24));
            const index = dayOfYear % quotes.length;
            return quotes[index];
        }

        const dailyQuote = getDailyQuote();
        document.getElementById("quoteText").textContent = `"${dailyQuote.text}"`;
        document.getElementById("quoteAuthor").textContent = `— ${dailyQuote.author}`;

        // ============================================================
        // DOM ELEMENTS
        // ============================================================
        const linkInput = document.getElementById("linkInput");
        const addBtn = document.getElementById("addBtn");
        const linksContainer = document.getElementById("linksContainer");
        const countSpan = document.getElementById("countSpan");
        const copyBtn = document.getElementById("copyBtn");
        const clearBtn = document.getElementById("clearBtn");
        const codeDisplay = document.getElementById("codeDisplay");

        codeDisplay.textContent = CODE;

        // ============================================================
        // REAL-TIME SYNC: Listen for changes from Firebase
        // ============================================================
        let linksData = {};

        onValue(linksRef, (snapshot) => {
            linksData = snapshot.val() || {};
            renderLinks();
        });

        function renderLinks() {
            const entries = Object.entries(linksData);
            countSpan.textContent = `(${entries.length})`;
            linksContainer.innerHTML = "";

            if (entries.length === 0) {
                linksContainer.innerHTML = '<div class="empty">No links yet. Add one above.</div>';
                return;
            }

            // Show newest first
            entries.reverse();

            entries.forEach(([key, url]) => {
                const div = document.createElement("div");
                div.className = "link-item";

                const urlSpan = document.createElement("span");
                urlSpan.className = "link-url";
                urlSpan.textContent = url;
                urlSpan.title = url;

                const visitBtn = document.createElement("button");
                visitBtn.className = "visit-btn";
                visitBtn.textContent = "Visit →";
                visitBtn.addEventListener("click", () => {
                    window.open(url, "_blank", "noopener");
                });

                const deleteBtn = document.createElement("button");
                deleteBtn.className = "delete-btn";
                deleteBtn.textContent = "✕";
                deleteBtn.title = "Remove";
                deleteBtn.addEventListener("click", () => {
                    remove(ref(database, "links/" + CODE + "/" + key));
                });

                div.appendChild(urlSpan);
                div.appendChild(visitBtn);
                div.appendChild(deleteBtn);
                linksContainer.appendChild(div);
            });
        }

        // ============================================================
        // ADD LINK
        // ============================================================
        function addLink() {
            let url = linkInput.value.trim();
            if (!url) return;

            if (!/^https?:\/\//i.test(url)) {
                url = "https://" + url;
            }

            try {
                new URL(url);
            } catch (e) {
                alert("Please enter a valid link.");
                return;
            }

            push(linksRef, url);
            linkInput.value = "";
        }

        addBtn.addEventListener("click", addLink);
        linkInput.addEventListener("keypress", (e) => {
            if (e.key === "Enter") addLink();
        });

        // ============================================================
        // COPY CODE
        // ============================================================
        copyBtn.addEventListener("click", () => {
            navigator.clipboard.writeText(CODE).then(() => {
                copyBtn.textContent = "✅ Copied!";
                setTimeout(() => { copyBtn.textContent = "📋 Copy Code"; }, 1500);
            });
        });

        // ============================================================
        // CLEAR ALL
        // ============================================================
        clearBtn.addEventListener("click", () => {
            if (Object.keys(linksData).length === 0) return;
            if (confirm("Delete all links? This syncs across all devices.")) {
                set(linksRef, null);
            }
        });
    </script>
</body>
</html>
