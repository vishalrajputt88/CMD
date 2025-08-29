<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Essential Command Collection</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --bg-primary: #0d1117;
            --bg-secondary: #161b22;
            --bg-tertiary: #21262d;
            --text-primary: #f0f6fc;
            --text-secondary: #8b949e;
            --accent: #58a6ff;
            --accent-hover: #1f6feb;
            --border: #30363d;
            --success: #3fb950;
            --warning: #d29922;
            --danger: #f85149;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Noto Sans', Helvetica, Arial, sans-serif;
            background: var(--bg-primary);
            color: var(--text-primary);
            line-height: 1.6;
            min-height: 100vh;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 2rem;
        }

        header {
            text-align: center;
            margin-bottom: 3rem;
            padding: 2rem 0;
            background: linear-gradient(135deg, var(--bg-secondary), var(--bg-tertiary));
            border-radius: 12px;
            border: 1px solid var(--border);
        }

        h1 {
            font-size: 3rem;
            font-weight: 700;
            margin-bottom: 1rem;
            background: linear-gradient(135deg, var(--accent), #bb6bd9);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .subtitle {
            font-size: 1.2rem;
            color: var(--text-secondary);
            margin-bottom: 2rem;
        }

        .search-container {
            position: relative;
            margin-bottom: 2rem;
            max-width: 500px;
            margin-left: auto;
            margin-right: auto;
        }

        .search-input {
            width: 100%;
            padding: 1rem 1rem 1rem 3rem;
            background: var(--bg-secondary);
            border: 2px solid var(--border);
            border-radius: 8px;
            color: var(--text-primary);
            font-size: 1rem;
            transition: all 0.3s ease;
        }

        .search-input:focus {
            outline: none;
            border-color: var(--accent);
            box-shadow: 0 0 0 3px rgba(88, 166, 255, 0.1);
        }

        .search-icon {
            position: absolute;
            left: 1rem;
            top: 50%;
            transform: translateY(-50%);
            color: var(--text-secondary);
        }

        .add-cmd-btn {
            background: linear-gradient(135deg, var(--accent), #bb6bd9);
            color: white;
            border: none;
            padding: 1rem 2rem;
            border-radius: 8px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            margin: 1rem 0;
        }

        .add-cmd-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 25px rgba(88, 166, 255, 0.3);
        }

        .categories {
            display: flex;
            flex-wrap: wrap;
            gap: 1rem;
            justify-content: center;
            margin-bottom: 2rem;
        }

        .category-btn {
            background: var(--bg-secondary);
            color: var(--text-secondary);
            border: 1px solid var(--border);
            padding: 0.5rem 1rem;
            border-radius: 6px;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .category-btn.active,
        .category-btn:hover {
            background: var(--accent);
            color: white;
            border-color: var(--accent);
        }

        .commands-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(400px, 1fr));
            gap: 1.5rem;
            margin-top: 2rem;
        }

        .command-card {
            background: var(--bg-secondary);
            border: 1px solid var(--border);
            border-radius: 12px;
            padding: 1.5rem;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .command-card:hover {
            transform: translateY(-4px);
            box-shadow: 0 12px 30px rgba(0, 0, 0, 0.3);
            border-color: var(--accent);
        }

        .command-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1rem;
        }

        .command-title {
            font-size: 1.2rem;
            font-weight: 600;
            color: var(--text-primary);
        }

        .command-category {
            background: var(--accent);
            color: white;
            padding: 0.25rem 0.75rem;
            border-radius: 12px;
            font-size: 0.8rem;
            font-weight: 500;
        }

        .command-code {
            background: var(--bg-primary);
            border: 1px solid var(--border);
            border-radius: 6px;
            padding: 1rem;
            margin: 1rem 0;
            font-family: 'SFMono-Regular', Consolas, 'Liberation Mono', Menlo, monospace;
            font-size: 0.9rem;
            position: relative;
            overflow-x: auto;
        }

        .copy-btn {
            position: absolute;
            top: 0.5rem;
            right: 0.5rem;
            background: var(--bg-tertiary);
            border: 1px solid var(--border);
            color: var(--text-secondary);
            padding: 0.5rem;
            border-radius: 4px;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .copy-btn:hover {
            background: var(--accent);
            color: white;
        }

        .command-description {
            color: var(--text-secondary);
            margin-bottom: 1rem;
            line-height: 1.5;
        }

        .command-url {
            display: flex;
            align-items: center;
            gap: 0.5rem;
            color: var(--accent);
            text-decoration: none;
            font-size: 0.9rem;
            transition: color 0.3s ease;
        }

        .command-url:hover {
            color: var(--accent-hover);
        }

        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            z-index: 1000;
            backdrop-filter: blur(4px);
        }

        .modal-content {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: var(--bg-secondary);
            border: 1px solid var(--border);
            border-radius: 12px;
            padding: 2rem;
            max-width: 500px;
            width: 90%;
        }

        .form-group {
            margin-bottom: 1.5rem;
        }

        .form-label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: 600;
            color: var(--text-primary);
        }

        .form-input,
        .form-textarea,
        .form-select {
            width: 100%;
            padding: 0.75rem;
            background: var(--bg-primary);
            border: 1px solid var(--border);
            border-radius: 6px;
            color: var(--text-primary);
            font-size: 1rem;
            transition: border-color 0.3s ease;
        }

        .form-input:focus,
        .form-textarea:focus,
        .form-select:focus {
            outline: none;
            border-color: var(--accent);
        }

        .form-textarea {
            min-height: 100px;
            resize: vertical;
        }

        .modal-buttons {
            display: flex;
            gap: 1rem;
            justify-content: flex-end;
        }

        .btn-secondary {
            background: var(--bg-tertiary);
            color: var(--text-primary);
            border: 1px solid var(--border);
            padding: 0.75rem 1.5rem;
            border-radius: 6px;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .btn-secondary:hover {
            background: var(--border);
        }

        .stats {
            display: flex;
            justify-content: center;
            gap: 2rem;
            margin-bottom: 2rem;
            flex-wrap: wrap;
        }

        .stat-item {
            text-align: center;
            background: var(--bg-secondary);
            padding: 1rem 2rem;
            border-radius: 8px;
            border: 1px solid var(--border);
        }

        .stat-number {
            font-size: 2rem;
            font-weight: 700;
            color: var(--accent);
            display: block;
        }

        .stat-label {
            color: var(--text-secondary);
            font-size: 0.9rem;
        }

        @media (max-width: 768px) {
            .container {
                padding: 1rem;
            }

            h1 {
                font-size: 2rem;
            }

            .commands-grid {
                grid-template-columns: 1fr;
            }

            .stats {
                flex-direction: column;
                gap: 1rem;
            }

            .categories {
               
                align-items: center;
            }
        }

        .fade-in {
            animation: fadeIn 0.5s ease-in;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>⚡ Essential Commands</h1>
            <p class="subtitle">Your curated collection of important command-line tools and utilities</p>
            
            <div class="stats">
                <div class="stat-item">
                    <span class="stat-number" id="total-commands">0</span>
                    <span class="stat-label">Total Commands</span>
                </div>
                <div class="stat-item">
                    <span class="stat-number" id="total-categories">0</span>
                    <span class="stat-label">Categories</span>
                </div>
            </div>

            <div class="search-container">
                <input type="text" class="search-input" id="searchInput" placeholder="Search commands...">
                <span class="search-icon">🔍</span>
            </div>

            <button class="add-cmd-btn" onclick="openModal()">+ Add New Command</button>
        </header>

        <div class="categories" id="categories">
            <button class="category-btn active" data-category="all">All</button>
        </div>

        <div class="commands-grid" id="commandsGrid">
            <!-- Commands will be dynamically added here -->
        </div>
    </div>

    <!-- Modal for adding new commands -->
    <div class="modal" id="addModal">
        <div class="modal-content">
            <h2 style="margin-bottom: 1.5rem; color: var(--text-primary);">Add New Command</h2>
            <form id="addCommandForm">
                <div class="form-group">
                    <label class="form-label" for="cmdTitle">Command Title</label>
                    <input type="text" class="form-input" id="cmdTitle" placeholder="e.g., Git Clone Repository" required>
                </div>
                
                <div class="form-group">
                    <label class="form-label" for="cmdCode">Command</label>
                    <textarea class="form-textarea" id="cmdCode" placeholder="git clone https://github.com/user/repo.git" required></textarea>
                </div>
                
                <div class="form-group">
                    <label class="form-label" for="cmdDescription">Description</label>
                    <textarea class="form-textarea" id="cmdDescription" placeholder="Clones a Git repository to your local machine"></textarea>
                </div>
                
                <div class="form-group">
                    <label class="form-label" for="cmdCategory">Category</label>
                    <select class="form-select" id="cmdCategory" required>
                        <option value="git">Git</option>
                        <option value="docker">Docker</option>
                        <option value="linux">Linux</option>
                        <option value="npm">NPM</option>
                        <option value="ssh">SSH</option>
                        <option value="database">Database</option>
                        <option value="network">Network</option>
                        <option value="other">Other</option>
                    </select>
                </div>
                
                <div class="form-group">
                    <label class="form-label" for="cmdUrl">Reference URL (optional)</label>
                    <input type="url" class="form-input" id="cmdUrl" placeholder="https://docs.example.com">
                </div>
                
                <div class="modal-buttons">
                    <button type="button" class="btn-secondary" onclick="closeModal()">Cancel</button>
                    <button type="submit" class="add-cmd-btn">Add Command</button>
                </div>
            </form>
        </div>
    </div>

    <script>
        // Sample initial data
        let commands = [
            {
                id: 1,
                title: "Clone Git Repository",
                command: "git clone https://github.com/username/repository.git",
                description: "Creates a local copy of a remote Git repository",
                category: "git",
                url: "https://git-scm.com/docs/git-clone"
            },
            {
                id: 2,
                title: "Docker Container List",
                command: "docker ps -a",
                description: "Shows all Docker containers (running and stopped)",
                category: "docker",
                url: "https://docs.docker.com/engine/reference/commandline/ps/"
            },
            {
                id: 3,
                title: "Check System Resources",
                command: "htop",
                description: "Interactive process viewer and system monitor",
                category: "linux",
                url: "https://htop.dev/"
            },
            {
                id: 4,
                title: "Install NPM Package",
                command: "npm install --save package-name",
                description: "Installs an NPM package and adds it to dependencies",
                category: "npm",
                url: "https://docs.npmjs.com/cli/v7/commands/npm-install"
            }
        ];

        let currentFilter = 'all';

        function renderCommands() {
            const grid = document.getElementById('commandsGrid');
            const filteredCommands = currentFilter === 'all' 
                ? commands 
                : commands.filter(cmd => cmd.category === currentFilter);
            
            const searchTerm = document.getElementById('searchInput').value.toLowerCase();
            const searchedCommands = filteredCommands.filter(cmd => 
                cmd.title.toLowerCase().includes(searchTerm) ||
                cmd.command.toLowerCase().includes(searchTerm) ||
                cmd.description.toLowerCase().includes(searchTerm)
            );

            grid.innerHTML = searchedCommands.map(cmd => `
                <div class="command-card fade-in">
                    <div class="command-header">
                        <h3 class="command-title">${cmd.title}</h3>
                        <span class="command-category">${cmd.category.toUpperCase()}</span>
                    </div>
                    
                    <div class="command-code">
                        <code>${cmd.command}</code>
                        <button class="copy-btn" onclick="copyCommand('${cmd.command.replace(/'/g, "\\'")}')">📋</button>
                    </div>
                    
                    <p class="command-description">${cmd.description}</p>
                    
                    ${cmd.url ? `
                        <a href="${cmd.url}" target="_blank" class="command-url">
                            🔗 Documentation
                        </a>
                    ` : ''}
                </div>
            `).join('');

            updateStats();
        }

        function renderCategories() {
            const categories = ['all', ...new Set(commands.map(cmd => cmd.category))];
            const categoryContainer = document.getElementById('categories');
            
            categoryContainer.innerHTML = categories.map(category => `
                <button class="category-btn ${category === currentFilter ? 'active' : ''}" 
                        data-category="${category}" 
                        onclick="filterByCategory('${category}')">
                    ${category === 'all' ? 'All' : category.toUpperCase()}
                </button>
            `).join('');
        }

        function filterByCategory(category) {
            currentFilter = category;
            document.querySelectorAll('.category-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            document.querySelector(`[data-category="${category}"]`).classList.add('active');
            renderCommands();
        }

        function copyCommand(command) {
            navigator.clipboard.writeText(command).then(() => {
                // Visual feedback
                const btn = event.target;
                const originalText = btn.textContent;
                btn.textContent = '✅';
                setTimeout(() => {
                    btn.textContent = originalText;
                }, 1000);
            });
        }

        function openModal() {
            document.getElementById('addModal').style.display = 'block';
        }

        function closeModal() {
            document.getElementById('addModal').style.display = 'none';
            document.getElementById('addCommandForm').reset();
        }

        function updateStats() {
            document.getElementById('total-commands').textContent = commands.length;
            document.getElementById('total-categories').textContent = new Set(commands.map(cmd => cmd.category)).size;
        }

        // Event listeners
        document.getElementById('searchInput').addEventListener('input', renderCommands);

        document.getElementById('addCommandForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const newCommand = {
                id: Date.now(),
                title: document.getElementById('cmdTitle').value,
                command: document.getElementById('cmdCode').value,
                description: document.getElementById('cmdDescription').value,
                category: document.getElementById('cmdCategory').value,
                url: document.getElementById('cmdUrl').value
            };
            
            commands.push(newCommand);
            closeModal();
            renderCategories();
            renderCommands();
        });

        // Close modal when clicking outside
        document.getElementById('addModal').addEventListener('click', function(e) {
            if (e.target === this) {
                closeModal();
            }
        });

        // Initialize the page
        renderCategories();
        renderCommands();
    </script>
</body>
</html>
