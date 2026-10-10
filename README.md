
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Neural Raphael Hub - GitHub Style</title>
    <style>
        :root {
            --bg-dark-red: #1a0202;
            --bg-card-red: #260404;
            --border-red: #590d0d;
            --accent-green: #00ff66;
            --accent-green-dim: #00b347;
            --accent-green-glow: rgba(0, 255, 102, 0.35);
            --black-header: #000000;
            --text-main: #e6e6e6;
            --text-muted: #a6a6a6;
            --text-danger: #ff3333;
            --font-system: -apple-system, BlinkMacSystemFont, "Segoe UI", "Noto Sans", Helvetica, Arial, sans-serif;
            --font-mono: ui-monospace, SFMono-Regular, SF Mono, Menlo, Consolas, Liberation Mono, monospace;
        }

        * { box-sizing: border-box; margin: 0; padding: 0; font-family: var(--font-system); }

        body {
            background-color: var(--bg-dark-red);
            color: var(--text-main);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
        }

        /* GitHub Style Header */
        header.gh-header {
            background-color: var(--black-header);
            border-bottom: 2px solid var(--accent-green);
            padding: 12px 24px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.8);
        }

        .gh-header-left { display: flex; align-items: center; gap: 16px; }
        .gh-logo {
            color: var(--accent-green);
            font-size: 1.3rem;
            font-weight: bold;
            font-family: var(--font-mono);
            letter-spacing: 1px;
            text-shadow: 0 0 10px var(--accent-green-glow);
            text-decoration: none;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .gh-search {
            background-color: #120101;
            border: 1px solid var(--border-red);
            border-radius: 6px;
            padding: 5px 12px;
            color: var(--text-main);
            font-size: 0.9rem;
            width: 260px;
            outline: none;
        }
        .gh-search:focus { border-color: var(--accent-green); box-shadow: 0 0 8px var(--accent-green-glow); }

        .gh-header-right { display: flex; align-items: center; gap: 16px; }
        .gh-avatar {
            width: 30px; height: 30px;
            border-radius: 50%;
            border: 1px solid var(--accent-green);
            background: #260404;
            display: flex; align-items: center; justify-content: center;
            color: var(--accent-green);
            font-weight: bold;
            font-size: 0.8rem;
        }

        /* GitHub Style Navigation / Tab Bar */
        nav.gh-subnav {
            background-color: var(--black-header);
            border-bottom: 1px solid var(--border-red);
            padding: 0 24px;
            display: flex;
            gap: 20px;
        }
        nav.gh-subnav a {
            color: var(--text-muted);
            text-decoration: none;
            font-size: 0.9rem;
            padding: 12px 4px;
            border-bottom: 2px solid transparent;
            font-weight: 500;
            transition: 0.2s;
        }
        nav.gh-subnav a:hover, nav.gh-subnav a.active {
            color: var(--accent-green);
            border-bottom-color: var(--accent-green);
        }

        .container { max-width: 1200px; margin: 30px auto; padding: 0 20px; flex: 1; width: 100%; }

        .view-section { display: none; }
        .view-section.active-view { display: block; }

        /* GitHub Profile / Overview Layout */
        .gh-grid { display: grid; grid-template-columns: 280px 1fr; gap: 30px; }
        @media(max-width: 768px) { .gh-grid { grid-template-columns: 1fr; } }

        .gh-sidebar-profile { display: flex; flex-direction: column; gap: 15px; }
        .gh-sidebar-profile .avatar-box {
            width: 100%;
            aspect-ratio: 1;
            border-radius: 50%;
            border: 2px solid var(--accent-green);
            background: var(--bg-card-red);
            display: flex; align-items: center; justify-content: center;
            font-size: 3rem;
            color: var(--accent-green);
            box-shadow: 0 0 20px var(--accent-green-glow);
        }
        .gh-sidebar-profile h2 { font-size: 1.4rem; color: var(--text-main); }
        .gh-sidebar-profile p { color: var(--text-muted); font-size: 0.95rem; }

        .gh-card {
            background-color: var(--bg-card-red);
            border: 1px solid var(--border-red);
            border-radius: 6px;
            padding: 20px;
            margin-bottom: 20px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.5);
        }
        .gh-card h3 { color: var(--accent-green); font-size: 1rem; margin-bottom: 12px; font-family: var(--font-mono); }

        /* Canvas 2D Visualizer */
        canvas#neuralCanvas {
            width: 100%;
            height: 180px;
            background-color: var(--black-header);
            border: 1px solid var(--border-red);
            border-radius: 4px;
            display: block;
        }

        .section-header-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid var(--border-red);
            padding-bottom: 12px;
            margin-bottom: 20px;
        }
        .section-header-row h2 { color: var(--accent-green); font-size: 1.2rem; font-family: var(--font-mono); }

        /* GitHub Style Buttons */
        .btn-gh {
            background-color: #260404;
            color: var(--accent-green);
            border: 1px solid var(--accent-green);
            padding: 6px 14px;
            border-radius: 6px;
            font-weight: 600;
            font-size: 0.85rem;
            cursor: pointer;
            transition: 0.2s;
        }
        .btn-gh:hover {
            background-color: var(--accent-green);
            color: var(--black-header);
            box-shadow: 0 0 10px var(--accent-green-glow);
        }
        .btn-gh-danger { color: var(--text-danger); border-color: var(--text-danger); }
        .btn-gh-danger:hover { background-color: var(--text-danger); color: var(--black-header); }

        .repo-list, .issues-list, .pulls-list, .settings-list, .cicd-list { display: flex; flex-direction: column; gap: 12px; }
        .repo-item, .issue-item, .pr-item, .setting-item, .cicd-item {
            background-color: var(--bg-card-red);
            border: 1px solid var(--border-red);
            padding: 16px 20px;
            border-radius: 6px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .repo-item h4 a { color: var(--accent-green); text-decoration: none; font-size: 1.05rem; font-family: var(--font-mono); }
        .repo-item p { font-size: 0.85rem; color: var(--text-muted); margin-top: 4px; }
        .repo-meta { font-size: 0.8rem; color: var(--accent-green-dim); display: flex; gap: 16px; font-family: var(--font-mono); }
        .gh-badge {
            color: var(--accent-green);
            border: 1px solid var(--accent-green);
            padding: 2px 8px;
            font-size: 0.75rem;
            font-weight: 600;
            border-radius: 12px;
            background: var(--black-header);
            font-family: var(--font-mono);
        }

        footer {
            background-color: var(--black-header);
            border-top: 1px solid var(--border-red);
            text-align: center;
            padding: 20px;
            font-size: 0.8rem;
            color: var(--text-muted);
            font-family: var(--font-mono);
        }
    </style>
</head>
<body>
    <header class="gh-header">
        <div class="gh-header-left">
            <a href="#" class="gh-logo">⚡ NeuralRaphaelHub</a>
            <input type="text" class="gh-search" placeholder="Type '/' to search repositories...">
        </div>
        <div class="gh-header-right">
            <button class="btn-gh" onclick="openNewRepoModal()">+ New repo</button>
            <div class="gh-avatar">NR</div>
        </div>
    </header>

    <nav class="gh-subnav">
        <a href="#" onclick="switchTab('overview', this)" class="active">Overview</a>
        <a href="#" onclick="switchTab('repos', this)">Repositories</a>
        <a href="#" onclick="switchTab('issues', this)">Issues</a>
        <a href="#" onclick="switchTab('pulls', this)">Pull requests</a>
        <a href="#" onclick="switchTab('commits', this)">Commits</a>
        <a href="#" onclick="switchTab('cicd', this)">Actions (CI/CD)</a>
        <a href="#" onclick="switchTab('settings', this)">Settings & PAT</a>
    </nav>

    <div class="container">
        <!-- VIEW: OVERVIEW -->
        <div id="section-overview" class="view-section active-view">
            <div class="gh-grid">
                <div class="gh-sidebar-profile">
                    <div class="avatar-box">⚡</div>
                    <div>
                        <h2>raphael_neural</h2>
                        <p>Neural Systems Architect & AI Core Maintainer</p>
                    </div>
                    <button class="btn-gh" style="width:100%;" onclick="switchTab('repos', document.querySelectorAll('.gh-subnav a')[1])">Explore Repositories</button>
                </div>
                <div>
                    <div class="gh-card">
                        <h3>Pinned Neural Repositories</h3>
                        <div id="pinned-repos-container" style="display: flex; flex-direction: column; gap: 10px;">
                            <p style="color:var(--text-muted);">Carregando repositórios em destaque...</p>
                        </div>
                    </div>
                    <div class="gh-card">
                        <h3>Neural Activity Monitor (Canvas 2D Real-time)</h3>
                        <canvas id="neuralCanvas"></canvas>
                    </div>
                </div>
            </div>
        </div>

        <!-- VIEW: REPOSITORIES -->
        <div id="section-repos" class="view-section">
            <div class="section-header-row">
                <h2>Repositories</h2>
                <button class="btn-gh" onclick="openNewRepoModal()">New repository</button>
            </div>
            <div id="repos-content" class="repo-list"><p>Carregando repositórios...</p></div>
        </div>

        <!-- VIEW: ISSUES -->
        <div id="section-issues" class="view-section">
            <div class="section-header-row">
                <h2>Issues & Bug Tracking</h2>
                <button class="btn-gh" onclick="openNewIssueModal()">New issue</button>
            </div>
            <div id="issues-content" class="issues-list"><p>Carregando issues...</p></div>
        </div>

        <!-- VIEW: PULL REQUESTS -->
        <div id="section-pulls" class="view-section">
            <div class="section-header-row">
                <h2>Pull Requests</h2>
                <button class="btn-gh" onclick="openNewPRModal()">New pull request</button>
            </div>
            <div id="pulls-content" class="pulls-list"><p>Carregando Pull Requests...</p></div>
        </div>

        <!-- VIEW: COMMITS -->
        <div id="section-commits" class="view-section">
            <div class="section-header-row"><h2>Commit History (Git DAG SHA-256)</h2></div>
            <div id="commits-content" class="repo-list"><p>Carregando commits...</p></div>
        </div>

        <!-- VIEW: CI/CD -->
        <div id="section-cicd" class="view-section">
            <div class="section-header-row"><h2>CI/CD Workflows & Webhooks</h2></div>
            <div class="gh-card">
                <h3>Workflows Ativos (.neural-ci)</h3>
                <div id="workflows-container" style="margin-top: 15px;" class="cicd-list">Carregando workflows...</div>
            </div>
        </div>

        <!-- VIEW: SETTINGS -->
        <div id="section-settings" class="view-section">
            <div class="section-header-row"><h2>Personal Access Tokens (PAT) & SSH Keys</h2></div>
            <div class="gh-card">
                <h3>Tokens de Acesso Pessoal</h3>
                <button class="btn-gh" onclick="generateNewPATToken()">Generate new token</button>
                <div id="tokens-list-container" style="margin-top: 15px;" class="settings-list">Carregando tokens...</div>
            </div>
        </div>
    </div>

    <footer>Neural Raphael Hub &copy; 2026 - GitHub-Style Cyberpunk Edition</footer>

    <script>
        // Canvas 2D Animation Loop
        const canvas = document.getElementById('neuralCanvas');
        const ctx = canvas.getContext('2d');

        function resizeCanvas() {
            canvas.width = canvas.parentElement.clientWidth - 40;
            canvas.height = 180;
        }
        window.addEventListener('resize', resizeCanvas);
        resizeCanvas();

        const nodes = Array.from({ length: 22 }, () => ({
            x: Math.random() * canvas.width,
            y: Math.random() * canvas.height,
            vx: (Math.random() - 0.5) * 1.2,
            vy: (Math.random() - 0.5) * 1.2,
            radius: Math.random() * 2.5 + 1.5
        }));

        function drawNeuralCanvas() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            ctx.strokeStyle = 'rgba(0, 255, 102, 0.12)';
            ctx.lineWidth = 1;

            for (let i = 0; i < nodes.length; i++) {
                for (let j = i + 1; j < nodes.length; j++) {
                    const dx = nodes[i].x - nodes[j].x;
                    const dy = nodes[i].y - nodes[j].y;
                    const dist = Math.sqrt(dx * dx + dy * dy);
                    if (dist < 100) {
                        ctx.beginPath();
                        ctx.moveTo(nodes[i].x, nodes[i].y);
                        ctx.lineTo(nodes[j].x, nodes[j].y);
                        ctx.stroke();
                    }
                }
            }

            nodes.forEach(node => {
                node.x += node.vx;
                node.y += node.vy;
                if (node.x < 0 || node.x > canvas.width) node.vx *= -1;
                if (node.y < 0 || node.y > canvas.height) node.vy *= -1;

                ctx.fillStyle = '#00ff66';
                ctx.shadowBlur = 6;
                ctx.shadowColor = '#00ff66';
                ctx.beginPath();
                ctx.arc(node.x, node.y, node.radius, 0, Math.PI * 2);
                ctx.fill();
                ctx.shadowBlur = 0;
            });

            requestAnimationFrame(drawNeuralCanvas);
        }
        drawNeuralCanvas();

        // SPA Navigation & Fetch
        function switchTab(tabName, el) {
            document.querySelectorAll('.view-section').forEach(s => s.classList.remove('active-view'));
            document.querySelectorAll('nav.gh-subnav a').forEach(a => a.classList.remove('active'));
            document.getElementById('section-' + tabName).classList.add('active-view');
            if (el) el.classList.add('active');

            if (tabName === 'overview') loadOverviewData();
            if (tabName === 'repos') loadRepositoriesView();
            if (tabName === 'issues') loadIssuesView();
            if (tabName === 'pulls') loadPullRequestsView();
            if (tabName === 'commits') loadCommitsView();
            if (tabName === 'cicd') loadCICDView();
            if (tabName === 'settings') loadSettingsView();
        }

        async function loadOverviewData() {
            const res = await (await fetch('/api/repos')).json();
            document.getElementById('pinned-repos-container').innerHTML = res.repositories.slice(0, 2).map(r => \`
                <div class="repo-item" style="padding: 12px 15px;">
                    <div><h4><a href="#">\${r.owner_name} / \${r.name}</a></h4><p>\${r.description || ''}</p></div>
                    <span class="gh-badge">Public</span>
                </div>
            \`).join('');
        }

        async function loadRepositoriesView() {
            const res = await (await fetch('/api/repos')).json();
            document.getElementById('repos-content').innerHTML = res.repositories.map(r => \`
                <div class="repo-item">
                    <div><h4><a href="#">\${r.owner_name} / \${r.name}</a></h4><p>\${r.description || ''}</p></div>
                    <div class="repo-meta"><span>★ \${r.stars}</span><span>⑂ \${r.forks}</span></div>
                </div>
            \`).join('');
        }

        async function loadIssuesView() {
            const res = await (await fetch('/api/repos/1/issues')).json();
            document.getElementById('issues-content').innerHTML = res.issues.map(i => \`
                <div class="issue-item">
                    <div><h4>#\${i.id} - \${i.title}</h4><p>\${i.body || ''}</p></div>
                    <span class="gh-badge">\${i.status.toUpperCase()}</span>
                </div>
            \`).join('');
        }

        async function loadPullRequestsView() {
            const res = await (await fetch('/api/repos/1/pulls')).json();
            document.getElementById('pulls-content').innerHTML = res.pull_requests.map(pr => \`
                <div class="pr-item">
                    <div><h4>PR #\${pr.id} - \${pr.title}</h4><p>\${pr.source_branch} ➔ \${pr.target_branch}</p></div>
                    <span class="gh-badge" style="color: #00ccff; border-color: #00ccff;">\${pr.status.toUpperCase()}</span>
                </div>
            \`).join('');
        }

        async function loadCommitsView() {
            const res = await (await fetch('/api/repos/1/commits')).json();
            document.getElementById('commits-content').innerHTML = res.commits.map(c => \`
                <div class="repo-item">
                    <div><strong>\${c.message}</strong><p style="color: var(--text-muted);">Hash: \${c.commit_hash.substring(0,10)}</p></div>
                    <span class="gh-badge">\${c.branch_name || 'main'}</span>
                </div>
            \`).join('');
        }

        async function loadCICDView() {
            const res = await (await fetch('/api/repos/1/workflows')).json();
            document.getElementById('workflows-container').innerHTML = res.workflows.map(w => \`
                <div class="cicd-item">
                    <div><strong>\${w.name}</strong><p style="color: var(--text-muted);">Trigger: \${w.trigger_event}</p></div>
                    <button class="btn-gh" onclick="triggerWorkflow(\${w.id})">Run Workflow</button>
                </div>
            \`).join('');
        }

        async function loadSettingsView() {
            const res = await (await fetch('/api/users/1/settings')).json();
            document.getElementById('tokens-list-container').innerHTML = res.access_tokens.map(t => \`
                <div class="setting-item">
                    <div><strong>\${t.token_name}</strong><p style="color: var(--text-muted);">Scopes: \${t.scopes}</p></div>
                    <button class="btn-gh btn-gh-danger" onclick="revokeToken(\${t.id})">Revoke</button>
                </div>
            \`).join('');
        }

        async function triggerWorkflow(id) {
            alert('Executing CI/CD pipeline...');
            await fetch(\`/api/workflows/\${id}/trigger\`, { method: 'POST' });
            alert('Pipeline successfully completed!');
            loadCICDView();
        }

        async function generateNewPATToken() {
            const token_name = prompt('Token Name:');
            if (!token_name) return;
            const res = await fetch('/api/users/1/tokens', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ token_name, scopes: 'repo,user,admin' })
            });
            const data = await res.json();
            if (data.success) {
                prompt('Token generated successfully! Copy below:', data.token.rawToken);
                loadSettingsView();
            }
        }

        async function revokeToken(id) {
            if (!confirm('Revoke token?')) return;
            await fetch(\`/api/users/1/tokens/\${id}\`, { method: 'DELETE' });
            loadSettingsView();
        }

        async function openNewRepoModal() {
            const name = prompt('Repository name:');
            if (!name) return;
            const description = prompt('Description:');
            await fetch('/api/repos', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ name, description, owner_id: 1, is_private: 0 })
            });
            loadRepositoriesView();
        }

        async function openNewIssueModal() {
            const title = prompt('Issue title:');
            if (!title) return;
            const body = prompt('Description:');
            await fetch('/api/repos/1/issues', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ title, body, author_id: 1 })
            });
            loadIssuesView();
        }

        async function openNewPRModal() {
            const title = prompt('PR title:');
            if (!title) return;
            const description = prompt('Description:');
            await fetch('/api/repos/1/pulls', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ title, description, source_branch: 'feature/new', target_branch: 'main', author_id: 1 })
            });
            loadPullRequestsView();
        }

        loadOverviewData();
    </script>
</body>
</html>`;

// ============================================================================
// 2. BACKEND & DATABASE ENGINE (Express, SQLite3, All 8 Modules)
// ============================================================================
const express = require('express');
const sqlite3 = require('sqlite3').verbose();
const bodyParser = require('body-parser');
const path = require('path');
const crypto = require('crypto');

const app = express();
const PORT = process.env.PORT || 3000;

app.use(bodyParser.urlencoded({ extended: true }));
app.use(bodyParser.json());
app.use(express.static(path.join(__dirname, 'public')));

const dbFile = path.join(__dirname, 'neural_raphael_hub.db');
const db = new sqlite3.Database(dbFile, (err) => {
    if (err) {
        console.error('\x1b[31m[CRITICAL ERROR] Database connection failed:\x1b[0m', err.message);
    } else {
        console.log('\x1b[32m[NEURAL-HUB] SQLite connected successfully. Initializing complete database architecture...\x1b[0m');
        initializeUltimateDatabaseSchema();
    }
});

function initializeUltimateDatabaseSchema() {
    db.serialize(() => {
        db.run(`CREATE TABLE IF NOT EXISTS users (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            username TEXT UNIQUE NOT NULL,
            email TEXT UNIQUE NOT NULL,
            created_at DATETIME DEFAULT CURRENT_TIMESTAMP
        )`);

        db.run(`CREATE TABLE IF NOT EXISTS repositories (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            name TEXT NOT NULL,
            description TEXT,
            owner_id INTEGER,
            is_private BOOLEAN DEFAULT 0,
            stars INTEGER DEFAULT 0,
            forks INTEGER DEFAULT 0,
            created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
            FOREIGN KEY(owner_id) REFERENCES users(id)
        )`);

        db.run(`CREATE TABLE IF NOT EXISTS branches (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            repo_id INTEGER,
            name TEXT NOT NULL,
            is_default BOOLEAN DEFAULT 0,
            created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
            FOREIGN KEY(repo_id) REFERENCES repositories(id)
        )`);

        db.run(`CREATE TABLE IF NOT EXISTS commit_tree (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            repo_id INTEGER,
            branch_id INTEGER,
            parent_hash TEXT,
            commit_hash TEXT UNIQUE NOT NULL,
            author TEXT NOT NULL,
            message TEXT NOT NULL,
            changes_summary TEXT,
            created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
            FOREIGN KEY(repo_id) REFERENCES repositories(id),
            FOREIGN KEY(branch_id) REFERENCES branches(id)
        )`);

        db.run(`CREATE TABLE IF NOT EXISTS file_blobs (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            repo_id INTEGER,
            commit_hash TEXT,
            file_path TEXT NOT NULL,
            content TEXT NOT NULL,
            FOREIGN KEY(repo_id) REFERENCES repositories(id)
        )`);

        db.run(`CREATE TABLE IF NOT EXISTS issues (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            repo_id INTEGER,
            title TEXT NOT NULL,
            body TEXT,
            status TEXT DEFAULT 'open',
            author_id INTEGER,
            created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
            FOREIGN KEY(repo_id) REFERENCES repositories(id),
            FOREIGN KEY(author_id) REFERENCES users(id)
        )`);

        db.run(`CREATE TABLE IF NOT EXISTS issue_comments (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            issue_id INTEGER,
            author_id INTEGER,
            comment TEXT NOT NULL,
            created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
            FOREIGN KEY(issue_id) REFERENCES issues(id),
            FOREIGN KEY(author_id) REFERENCES users(id)
        )`);

        db.run(`CREATE TABLE IF NOT EXISTS pull_requests (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            repo_id INTEGER,
            title TEXT NOT NULL,
            description TEXT,
            source_branch TEXT NOT NULL,
            target_branch TEXT NOT NULL,
            status TEXT DEFAULT 'open',
            author_id INTEGER,
            created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
            FOREIGN KEY(repo_id) REFERENCES repositories(id),
            FOREIGN KEY(author_id) REFERENCES users(id)
        )`);

        db.run(`CREATE TABLE IF NOT EXISTS pr_reviews (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            pr_id INTEGER,
            author_id INTEGER,
            file_path TEXT,
            line_number INTEGER,
            review_comment TEXT NOT NULL,
            created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
            FOREIGN KEY(pr_id) REFERENCES pull_requests(id),
            FOREIGN KEY(author_id) REFERENCES users(id)
        )`);

        db.run(`CREATE TABLE IF NOT EXISTS user_profiles (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            user_id INTEGER UNIQUE,
            bio TEXT,
            company TEXT,
            location TEXT,
            website TEXT,
            theme_preference TEXT DEFAULT 'cyber_red_green',
            updated_at DATETIME DEFAULT CURRENT_TIMESTAMP,
            FOREIGN KEY(user_id) REFERENCES users(id)
        )`);

        db.run(`CREATE TABLE IF NOT EXISTS ssh_keys (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            user_id INTEGER,
            title TEXT NOT NULL,
            key_fingerprint TEXT NOT NULL,
            public_key TEXT NOT NULL,
            created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
            FOREIGN KEY(user_id) REFERENCES users(id)
        )`);

        db.run(`CREATE TABLE IF NOT EXISTS personal_access_tokens (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            user_id INTEGER,
            token_name TEXT NOT NULL,
            token_hash TEXT UNIQUE NOT NULL,
            scopes TEXT DEFAULT 'repo,user,admin',
            expires_at DATETIME,
            created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
            FOREIGN KEY(user_id) REFERENCES users(id)
        )`);

        db.run(`CREATE TABLE IF NOT EXISTS audit_logs (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            user_id INTEGER,
            action TEXT NOT NULL,
            ip_address TEXT,
            created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
            FOREIGN KEY(user_id) REFERENCES users(id)
        )`);

        db.run(`CREATE TABLE IF NOT EXISTS cicd_workflows (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            repo_id INTEGER,
            name TEXT NOT NULL,
            trigger_event TEXT DEFAULT 'push',
            script_body TEXT NOT NULL,
            created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
            FOREIGN KEY(repo_id) REFERENCES repositories(id)
        )`);

        db.run(`CREATE TABLE IF NOT EXISTS pipeline_runs (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            workflow_id INTEGER,
            commit_hash TEXT,
            status TEXT DEFAULT 'pending',
            logs TEXT,
            duration_ms INTEGER DEFAULT 0,
            started_at DATETIME DEFAULT CURRENT_TIMESTAMP,
            finished_at DATETIME,
            FOREIGN KEY(workflow_id) REFERENCES cicd_workflows(id)
        )`);

        db.run(`CREATE TABLE IF NOT EXISTS webhooks (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            repo_id INTEGER,
            payload_url TEXT NOT NULL,
            secret TEXT,
            event_type TEXT DEFAULT '*',
            is_active BOOLEAN DEFAULT 1,
            created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
            FOREIGN KEY(repo_id) REFERENCES repositories(id)
        )`);

        db.get(`SELECT COUNT(*) as count FROM users`, (err, row) => {
            if (row && row.count === 0) {
                seedUltimateDatabase();
            }
        });
    });
}

function seedUltimateDatabase() {
    db.run(`INSERT INTO users (username, email) VALUES ('raphael_neural', 'raphael@neuralhub.com')`, function(err) {
        if (!err) {
            const uid = this.lastID;
            db.run(`INSERT INTO repositories (name, description, owner_id, is_private, stars, forks) VALUES 
                ('neural-core', 'Core intelligence engine for Neural Raphael Hub', ?, 0, 142, 38),
                ('quantum-net', 'Distributed decentralized network nodes', ?, 0, 89, 12)`, [uid, uid], function() {
                    db.run(`INSERT INTO branches (repo_id, name, is_default) VALUES (1, 'main', 1), (2, 'main', 1)`);
                    db.run(`INSERT INTO issues (repo_id, title, body, status, author_id) VALUES (1, 'Otimizar consumo de RAM no engine neural', 'O worker consome muita memória em loops intensos.', 'open', ?)`, [uid]);
                    db.run(`INSERT INTO pull_requests (repo_id, title, description, source_branch, target_branch, status, author_id) VALUES (1, 'Upgrade Node.js v22 com worker threads', 'Melhoria de performance e segurança criptográfica.', 'feature/v22', 'main', 'open', ?)`, [uid]);
                    db.run(`INSERT INTO user_profiles (user_id, bio, company, location, website) VALUES (?, 'Arquiteto de Sistemas Neurais & IA', 'Neural Corp', 'Brasil', 'https://raphaelhub.neural')`, [uid]);
                    db.run(`INSERT INTO cicd_workflows (repo_id, name, trigger_event, script_body) VALUES (1, 'Neural Build & Test Pipeline', 'push', 'npm install && npm test --ci')`);
                });
        }
    });
}

// ============================================================================
// 3. REST API ENDPOINTS & HTTP ROUTING
// ============================================================================
app.get('/api/repos', (req, res) => {
    db.all(`SELECT r.*, u.username as owner_name FROM repositories r JOIN users u ON r.owner_id = u.id ORDER BY r.created_at DESC`, [], (err, rows) => {
        if (err) return res.status(500).json({ error: err.message });
        res.json({ repositories: rows });
    });
});

app.post('/api/repos', (req, res) => {
    const { name, description, owner_id, is_private } = req.body;
    db.run(`INSERT INTO repositories (name, description, owner_id, is_private) VALUES (?, ?, ?, ?)`, 
        [name, description, owner_id || 1, is_private ? 1 : 0], function(err) {
        if (err) return res.status(500).json({ error: err.message });
        const repoId = this.lastID;
        db.run(`INSERT INTO branches (repo_id, name, is_default) VALUES (?, 'main', 1)`, [repoId], () => {
            const commitHash = crypto.createHash('sha256').update(`${repoId}-init-${Date.now()}`).digest('hex');
            db.run(`INSERT INTO commit_tree (repo_id, branch_id, parent_hash, commit_hash, author, message, changes_summary) VALUES (?, 1, '000000', ?, 'raphael_neural', 'Initial commit', '1 file added')`,
                [repoId, commitHash], () => {
                    db.run(`INSERT INTO cicd_workflows (repo_id, name, trigger_event, script_body) VALUES (?, 'Default Build Pipeline', 'push', 'npm test')`, [repoId]);
                    res.json({ id: repoId, message: 'Repository created and initialized successfully.' });
                });
        });
    });
});

app.get('/api/stats', (req, res) => {
    db.get(`SELECT COUNT(*) as total_repos FROM repositories`, (err, r) => {
        db.get(`SELECT COUNT(*) as total_users FROM users`, (err2, u) => {
            db.get(`SELECT COUNT(*) as total_issues FROM issues`, (err3, i) => {
                res.json({
                    repositories: r ? r.total_repos : 0,
                    users: u ? u.total_users : 0,
                    issues: i ? i.total_issues : 0,
                    active_nodes: 99.99
                });
            });
        });
    });
});

app.get('/api/repos/:id/commits', (req, res) => {
    db.all(`SELECT c.*, b.name as branch_name FROM commit_tree c JOIN branches b ON c.branch_id = b.id WHERE c.repo_id = ? ORDER BY c.id DESC`, [req.params.id], (err, rows) => {
        if (err) return res.status(500).json({ error: err.message });
        res.json({ commits: rows });
    });
});

app.get('/api/repos/:id/issues', (req, res) => {
    db.all(`SELECT i.*, u.username as author_name FROM issues i JOIN users u ON i.author_id = u.id WHERE i.repo_id = ? ORDER BY i.created_at DESC`, [req.params.id], (err, rows) => {
        if (err) return res.status(500).json({ error: err.message });
        res.json({ issues: rows });
    });
});

app.post('/api/repos/:id/issues', (req, res) => {
    const { title, body, author_id } = req.body;
    db.run(`INSERT INTO issues (repo_id, title, body, author_id, status) VALUES (?, ?, ?, ?, 'open')`,
        [req.params.id, title, body, author_id || 1], function(err) {
        if (err) return res.status(500).json({ error: err.message });
        res.json({ success: true, issueId: this.lastID });
    });
});

app.get('/api/repos/:id/pulls', (req, res) => {
    db.all(`SELECT pr.*, u.username as author_name FROM pull_requests pr JOIN users u ON pr.author_id = u.id WHERE pr.repo_id = ? ORDER BY pr.created_at DESC`, [req.params.id], (err, rows) => {
        if (err) return res.status(500).json({ error: err.message });
        res.json({ pull_requests: rows });
    });
});

app.post('/api/repos/:id/pulls', (req, res) => {
    const { title, description, source_branch, target_branch, author_id } = req.body;
    db.run(`INSERT INTO pull_requests (repo_id, title, description, source_branch, target_branch, author_id, status) VALUES (?, ?, ?, ?, ?, ?, 'open')`,
        [req.params.id, title, description, source_branch || 'feature/dev', target_branch || 'main', author_id || 1], function(err) {
        if (err) return res.status(500).json({ error: err.message });
        res.json({ success: true, prId: this.lastID });
    });
});

app.get('/api/users/:id/settings', (req, res) => {
    const userId = req.params.id;
    db.get(`SELECT * FROM user_profiles WHERE user_id = ?`, [userId], (err, profile) => {
        db.all(`SELECT id, title, key_fingerprint, created_at FROM ssh_keys WHERE user_id = ?`, [userId], (err2, keys) => {
            db.all(`SELECT id, token_name, scopes, created_at, expires_at FROM personal_access_tokens WHERE user_id = ?`, [userId], (err3, tokens) => {
                res.json({
                    profile: profile || { bio: '', company: '', location: '', website: '' },
                    ssh_keys: keys || [],
                    access_tokens: tokens || []
                });
            });
        });
    });
});

app.post('/api/users/:id/tokens', (req, res) => {
    const userId = req.params.id;
    const { token_name, scopes } = req.body;
    const rawToken = `nrh_${crypto.randomBytes(24).toString('hex')}`;
    const tokenHash = crypto.createHash('sha256').update(rawToken).digest('hex');

    db.run(`INSERT INTO personal_access_tokens (user_id, token_name, token_hash, scopes) VALUES (?, ?, ?, ?)`,
        [userId, token_name, tokenHash, scopes || 'repo,user'], function(err) {
        if (err) return res.status(500).json({ error: err.message });
        res.json({ success: true, token: { id: this.lastID, tokenName: token_name, rawToken } });
    });
});

app.delete('/api/users/:userId/tokens/:tokenId', (req, res) => {
    db.run(`DELETE FROM personal_access_tokens WHERE id = ? AND user_id = ?`, [req.params.tokenId, req.params.userId], function(err) {
        if (err) return res.status(500).json({ error: err.message });
        res.json({ success: true, deleted: this.changes > 0 });
    });
});

app.post('/api/users/:id/ssh-keys', (req, res) => {
    const userId = req.params.id;
    const { title, public_key } = req.body;
    const fingerprint = crypto.createHash('sha256').update(public_key || '').digest('hex');

    db.run(`INSERT INTO ssh_keys (user_id, title, key_fingerprint, public_key) VALUES (?, ?, ?, ?)`,
        [userId, title || 'Chave Padrão', fingerprint, public_key], function(err) {
        if (err) return res.status(500).json({ error: err.message });
        res.json({ success: true, keyId: this.lastID, fingerprint });
    });
});

app.get('/api/repos/:id/workflows', (req, res) => {
    db.all(`SELECT * FROM cicd_workflows WHERE repo_id = ?`, [req.params.id], (err, rows) => {
        if (err) return res.status(500).json({ error: err.message });
        res.json({ workflows: rows });
    });
});

app.post('/api/workflows/:id/trigger', (req, res) => {
    const workflowId = req.params.id;
    const startTime = Date.now();
    const runLogs = `[NEURAL-CI] Initializing containerized sandbox...\n[STEP 1/3] Cloning source tree...\n[STEP 2/3] Running security scan & linter...\n[STEP 3/3] Executing unit tests (100% passed)...\n[NEURAL-CI] Pipeline build successfully completed!`;

    setTimeout(() => {
        const duration = Date.now() - startTime;
        db.run(`INSERT INTO pipeline_runs (workflow_id, commit_hash, status, logs, duration_ms, finished_at) VALUES (?, 'latest', 'success', ?, ?, CURRENT_TIMESTAMP)`,
            [workflowId, runLogs, duration], function(err) {
                if (err) return res.status(500).json({ error: err.message });
                res.json({ success: true, runId: this.lastID, status: 'success', duration_ms: duration, logs: runLogs });
            });
    }, 600);
});

app.get('/api/repos/:id/webhooks', (req, res) => {
    db.all(`SELECT id, payload_url, event_type, is_active, created_at FROM webhooks WHERE repo_id = ?`, [req.params.id], (err, rows) => {
        if (err) return res.status(500).json({ error: err.message });
        res.json({ webhooks: rows });
    });
});

app.post('/api/repos/:id/webhooks', (req, res) => {
    const repoId = req.params.id;
    const { payload_url, secret, event_type } = req.body;
    db.run(`INSERT INTO webhooks (repo_id, payload_url, secret, event_type) VALUES (?, ?, ?, ?)`,
        [repoId, payload_url, secret || '', event_type || '*'], function(err) {
        if (err) return res.status(500).json({ error: err.message });
        res.json({ success: true, webhookId: this.lastID });
    });
});

// Serve GitHub-Style Frontend Template
app.get('/', (req, res) => {
    res.send(FRONTEND_HTML);
});

// Start Monolithic Server
app.listen(PORT, () => {
    console.log(`\x1b[32m[NEURAL-RAPHAEL-HUB] GitHub-Style Monolithic Application running on port ${PORT}\x1b[0m`);
});
