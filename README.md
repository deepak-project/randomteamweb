  <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Team Generator with Constraints</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
      * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background: #0e021a; /* pure black background */
    color: #cbd5e1; /* cool light blue-gray text */
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 1rem;
}

header {
    text-align: center;
    margin: 1.5rem 0;
}

header h1 {
    font-size: 2.8rem;
    margin-bottom: 0.5rem;
    font-weight: 700;
    color: #7dd3fc; /* bright cyan */
    text-shadow: 0 0 8px #38bdf8;
}

header p {
    font-size: 1.2rem;
    color: #94a3b8; /* muted blue-gray */
    max-width: 600px;
}

.container {
    background: rgba(15, 23, 42, 0.85); /* dark navy with opacity */
    backdrop-filter: blur(12px);
    border-radius: 16px;
    padding: 2rem;
    width: 90%;
    max-width: 800px;
    box-shadow: 0 0 20px #0ea5e9; /* subtle cyan glow */
    margin-bottom: 2rem;
}

.section {
    margin-bottom: 2rem;
}

h2 {
    font-size: 1.5rem;
    margin-bottom: 1rem;
    color: #38bdf8; /* bright blue */
    display: flex;
    align-items: center;
    gap: 0.5rem;
}

h2 i {
    font-size: 1.3rem;
}

label {
    display: block;
    margin-top: 1rem;
    font-weight: 600;
    color: #94a3b8;
}

input[type="number"],
input[type="text"],
textarea {
    width: 100%;
    padding: 0.8rem;
    margin-top: 0.5rem;
    border-radius: 10px;
    border: 2px solid #334155; /* dark slate */
    font-size: 1rem;
    resize: vertical;
    background: #1e293b; /* dark slate blue */
    color: #cbd5e1;
    transition: border-color 0.3s;
}

input:focus,
textarea:focus {
    outline: none;
    border-color: #0ea5e9; /* bright cyan */
    background: #334155; /* lighter slate */
}

input::placeholder,
textarea::placeholder {
    color: #64748b; /* medium slate */
}

#members-list {
    margin-top: 0.5rem;
    max-height: 150px;
    overflow-y: auto;
    background: #1e293b; /* dark slate blue */
    border-radius: 10px;
    padding: 0.8rem;
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem;
}

.member-tag {
    display: inline-flex;
    align-items: center;
    background: #0ea5e9; /* bright cyan */
    padding: 0.4rem 0.8rem;
    border-radius: 20px;
    font-size: 0.9rem;
    cursor: pointer;
    user-select: none;
    transition: background 0.3s ease;
    color: #000000;
    font-weight: 600;
}

.member-tag:hover {
    background: #0284c7; /* darker cyan */
}

.member-tag .remove-btn {
    margin-left: 0.5rem;
    font-weight: bold;
    cursor: pointer;
    color: #1e293b;
}

.constraints-example {
    display: block;
    margin-top: 0.25rem;
    margin-bottom: 1rem;
    color: #64748b;
    font-size: 0.85rem;
}

.buttons {
    display: flex;
    justify-content: center;
    margin-top: 1.5rem;
}

button {
    background: #0ea5e9; /* bright cyan */
    border: none;
    padding: 1rem 2rem;
    font-size: 1.1rem;
    color: #000000;
    border-radius: 10px;
    cursor: pointer;
    transition: background 0.3s ease;
    font-weight: 700;
    display: flex;
    align-items: center;
    gap: 0.5rem;
    box-shadow: 0 0 10px #0ea5e9;
}

button:hover {
    background: #0284c7; /* darker cyan */
    box-shadow: 0 0 15px #0284c7;
    transform: translateY(-2px);
}

button:active {
    transform: translateY(0);
}

#teams-output {
    margin-top: 2rem;
}

.team {
    background: #334155; /* dark slate */
    margin-bottom: 1.5rem;
    padding: 1.5rem;
    border-radius: 12px;
    box-shadow: 0 0 10px #0ea5e9;
}

.team h3 {
    margin: 0 0 1rem 0;
    color: #7dd3fc; /* cyan */
    font-size: 1.3rem;
    display: flex;
    align-items: center;
    gap: 0.5rem;
}

.team p {
    margin: 0;
    font-size: 1.1rem;
    color: #cbd5e1;
}

.clap-container {
    margin-top: 2rem;
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 1rem;
}

.clap {
    font-size: 3rem;
    animation: clapAnim 1.5s ease-in-out infinite;
    color: #0ea5e9;
}

.clap:nth-child(2) {
    animation-delay: 0.3s;
}

@keyframes clapAnim {
    0%, 100% { transform: scale(1) rotate(0deg); }
    50% { transform: scale(1.3) rotate(15deg); }
}

footer {
    margin-top: 2rem;
    font-size: 0.9rem;
    color: #64748b;
    text-align: center;
}

/* Responsive Design */
@media (max-width: 600px) {
    header h1 {
        font-size: 2.2rem;
    }
    
    .container {
        padding: 1.5rem;
    }
    
    input[type="number"],
    input[type="text"],
    textarea {
        padding: 0.7rem;
    }
}
    </style>
</head>
<body>
    <header>
        <h1><i class="fas fa-users"></i> Team Generator</h1>
        <p>Create balanced teams with custom constraints for members</p>
    </header>

    <div class="container">
        <div class="section">
            <h2><i class="fas fa-list-ol"></i> Total Members</h2>
            <input type="number" id="total-members" min="1" placeholder="Enter total number of members">
        </div>

        <div class="section">
            <h2><i class="fas fa-user-plus"></i> Add Members</h2>
            <input type="text" id="member-name" placeholder="Type a name and press Enter" disabled>
            <div id="members-list"></div>
        </div>

        <div class="section">
            <h2><i class="fas fa-user-friends"></i> Team Size</h2>
            <input type="number" id="team-size" min="1" placeholder="Enter number of people per team" disabled>
        </div>

        <div class="section">
            <h2><i class="fas fa-ban"></i> Separation Constraints</h2>
            <label>Members that must NOT be in the same team:</label>
            <textarea id="not-same-team" rows="3" placeholder="Example: Alice,Bob&#10;Charlie,David" disabled></textarea>
            <span class="constraints-example">Enter one pair per line, separated by a comma (e.g., John, Jane)</span>
        </div>

        <div class="section">
            <h2><i class="fas fa-link"></i> Pairing Constraints</h2>
            <label>Members that must be in the same team:</label>
            <textarea id="same-team" rows="3" placeholder="Example: Eve,Frank&#10;Grace,Hank" disabled></textarea>
            <span class="constraints-example">Enter one pair per line, separated by a comma (e.g., Alex, Taylor)</span>
        </div>

        <div class="buttons">
            <button id="generate-btn" disabled><i class="fas fa-cogs"></i> Generate Teams</button>
        </div>

        <div id="teams-output"></div>
        
        <div class="clap-container" id="clap-container">
            <div class="clap">👏</div>
            <div class="clap">👏</div>
        </div>
    </div>

    <footer>
        <p>Made with ❤️ by Mr. Deepak Shah | Easy team generation with smart constraints</p>
    </footer>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const totalMembersInput = document.getElementById('total-members');
            const memberNameInput = document.getElementById('member-name');
            const membersListDiv = document.getElementById('members-list');
            const teamSizeInput = document.getElementById('team-size');
            const notSameTeamInput = document.getElementById('not-same-team');
            const sameTeamInput = document.getElementById('same-team');
            const generateBtn = document.getElementById('generate-btn');
            const teamsOutput = document.getElementById('teams-output');
            const clapContainer = document.getElementById('clap-container');

            let totalMembers = 0;
            let members = [];

            // Initially hide the clap container
            clapContainer.style.display = 'none';

            // Enable member name input after total members entered
            totalMembersInput.addEventListener('change', () => {
                totalMembers = parseInt(totalMembersInput.value);
                if (totalMembers > 0) {
                    memberNameInput.disabled = false;
                    members = [];
                    updateMembersList();
                    teamSizeInput.value = '';
                    teamSizeInput.disabled = true;
                    notSameTeamInput.value = '';
                    notSameTeamInput.disabled = true;
                    sameTeamInput.value = '';
                    sameTeamInput.disabled = true;
                    generateBtn.disabled = true;
                    teamsOutput.innerHTML = '';
                    clapContainer.style.display = 'none';
                    memberNameInput.focus();
                } else {
                    memberNameInput.disabled = true;
                    teamSizeInput.disabled = true;
                    notSameTeamInput.disabled = true;
                    sameTeamInput.disabled = true;
                    generateBtn.disabled = true;
                    members = [];
                    updateMembersList();
                    teamsOutput.innerHTML = '';
                    clapContainer.style.display = 'none';
                }
            });

            // Add member on Enter key
            memberNameInput.addEventListener('keydown', (e) => {
                if (e.key === 'Enter') {
                    e.preventDefault();
                    const name = memberNameInput.value.trim();
                    if (name && members.length < totalMembers) {
                        if (members.includes(name)) {
                            alert('This member is already added.');
                            memberNameInput.value = '';
                            return;
                        }
                        members.push(name);
                        updateMembersList();
                        memberNameInput.value = '';
                        if (members.length === totalMembers) {
                            memberNameInput.disabled = true;
                            teamSizeInput.disabled = false;
                            notSameTeamInput.disabled = false;
                            sameTeamInput.disabled = false;
                            generateBtn.disabled = false;
                            teamSizeInput.focus();
                        }
                    }
                }
            });

            // Trigger generate on Enter key in team size input
            teamSizeInput.addEventListener('keydown', (e) => {
                if (e.key === 'Enter') {
                    e.preventDefault();
                    if (!generateBtn.disabled) {
                        generateBtn.click();
                    }
                }
            });

            // Update members list display with remove buttons
            function updateMembersList() {
                membersListDiv.innerHTML = '';
                members.forEach((name, index) => {
                    const span = document.createElement('span');
                    span.className = 'member-tag';
                    span.textContent = name;

                    // Add remove button
                    const removeBtn = document.createElement('span');
                    removeBtn.textContent = '×';
                    removeBtn.className = 'remove-btn';
                    removeBtn.title = 'Remove member';
                    removeBtn.addEventListener('click', (e) => {
                        e.stopPropagation();
                        members.splice(index, 1);
                        updateMembersList();
                        // If members less than totalMembers, enable input again
                        if (members.length < totalMembers) {
                            memberNameInput.disabled = false;
                            generateBtn.disabled = true;
                            teamSizeInput.disabled = true;
                            notSameTeamInput.disabled = true;
                            sameTeamInput.disabled = true;
                            teamsOutput.innerHTML = '';
                            clapContainer.style.display = 'none';
                            memberNameInput.focus();
                        }
                    });

                    span.appendChild(removeBtn);
                    membersListDiv.appendChild(span);
                });
            }

            // Helper: parse pairs from textarea input
            function parsePairs(text) {
                const pairs = [];
                const lines = text.split('\n').map(l => l.trim()).filter(l => l.length > 0);
                for (const line of lines) {
                    const parts = line.split(',').map(p => p.trim());
                    if (parts.length !== 2) {
                        alert(`Invalid pair format: "${line}". Each line must have exactly two names separated by a comma.`);
                        return null;
                    }
                    pairs.push(parts);
                }
                return pairs;
            }

            // Union-Find (Disjoint Set) for grouping "must be together"
            class UnionFind {
                constructor(elements) {
                    this.parent = {};
                    elements.forEach(e => this.parent[e] = e);
                }
                find(x) {
                    if (this.parent[x] !== x) {
                        this.parent[x] = this.find(this.parent[x]);
                    }
                    return this.parent[x];
                }
                union(a, b) {
                    const rootA = this.find(a);
                    const rootB = this.find(b);
                    if (rootA !== rootB) {
                        this.parent[rootB] = rootA;
                    }
                }
                groups() {
                    const map = {};
                    for (const e in this.parent) {
                        const root = this.find(e);
                        if (!map[root]) map[root] = [];
                        map[root].push(e);
                    }
                    return Object.values(map);
                }
            }

            // Check if any "must not be together" pair is in the same cluster
            function checkMustNotTogether(clusters, notTogetherPairs) {
                for (const [a, b] of notTogetherPairs) {
                    for (const cluster of clusters) {
                        if (cluster.includes(a) && cluster.includes(b)) {
                            return false; // conflict
                        }
                    }
                }
                return true;
            }

            // Shuffle array in-place
            function shuffle(array) {
                for (let i = array.length -1; i > 0; i--) {
                    const j = Math.floor(Math.random() * (i+1));
                    [array[i], array[j]] = [array[j], array[i]];
                }
            }

            // Generate teams respecting constraints
            function generateTeams(members, teamSize, mustNotTogetherPairs, mustTogetherPairs) {
                // Step 1: Group members who must be together
                const uf = new UnionFind(members);
                for (const [a,b] of mustTogetherPairs) {
                    if (!members.includes(a) || !members.includes(b)) {
                        throw new Error(`Member in "must be together" pair not found: ${a}, ${b}`);
                    }
                    uf.union(a,b);
                }
                const clusters = uf.groups();

                // Step 2: Check if any cluster contains members who must NOT be together
                if (!checkMustNotTogether(clusters, mustNotTogetherPairs)) {
                    throw new Error('Conflict: Some members who must NOT be together are in the same cluster due to "must be together" constraints.');
                }

                // Step 3: Shuffle clusters for randomness
                shuffle(clusters);

                // Step 4: Assign clusters to teams trying to respect "must NOT be together"
                const teams = [];
                const maxTeams = Math.ceil(members.length / teamSize);

                for (let i=0; i<maxTeams; i++) {
                    teams.push([]);
                }

                for (const cluster of clusters) {
                    // Find a team where cluster can fit and no "must not together" conflict
                    let placed = false;
                    for (const team of teams) {
                        // Check size
                        if (team.length + cluster.length > teamSize) continue;

                        // Check conflicts with members in team
                        let conflict = false;
                        for (const memberInTeam of team) {
                            for (const [a,b] of mustNotTogetherPairs) {
                                if ((cluster.includes(a) && memberInTeam === b) || (cluster.includes(b) && memberInTeam === a)) {
                                    conflict = true;
                                    break;
                                }
                            }
                            if (conflict) break;
                        }
                        if (!conflict) {
                            team.push(...cluster);
                            placed = true;
                            break;
                        }
                    }
                    if (!placed) {
                        throw new Error('Cannot place all members respecting constraints with given team size.');
                    }
                }

                // Remove empty teams (if any)
                return teams.filter(t => t.length > 0);
            }

            generateBtn.addEventListener('click', () => {
                teamsOutput.innerHTML = '';
                clapContainer.style.display = 'none';

                const teamSize = parseInt(teamSizeInput.value);
                if (!teamSize || teamSize < 1) {
                    alert('Please enter a valid team size (at least 1).');
                    return;
                }
                if (teamSize > members.length) {
                    alert('Team size cannot be greater than total members.');
                    return;
                }

                // Parse constraints
                const notTogetherPairs = parsePairs(notSameTeamInput.value);
                if (notTogetherPairs === null) return; // parse error

                const mustTogetherPairs = parsePairs(sameTeamInput.value);
                if (mustTogetherPairs === null) return; // parse error

                // Validate all members in constraints exist
                for (const [a,b] of [...notTogetherPairs, ...mustTogetherPairs]) {
                    if (!members.includes(a) || !members.includes(b)) {
                        alert(`Member in constraints not found in members list: ${a}, ${b}`);
                        return;
                    }
                }

                try {
                    const teams = generateTeams(members, teamSize, notTogetherPairs, mustTogetherPairs);

                    // Display teams
                    teamsOutput.innerHTML = '';
                    teams.forEach((team, idx) => {
                        const div = document.createElement('div');
                        div.className = 'team';
                        const h3 = document.createElement('h3');
                        h3.innerHTML = `<i class="fas fa-user-friends"></i> Team ${idx + 1}`;
                        const p = document.createElement('p');
                        p.textContent = team.join(', ');
                        div.appendChild(h3);
                        div.appendChild(p);
                        teamsOutput.appendChild(div);
                    });

                    clapContainer.style.display = 'flex';
                } catch (err) {
                    alert(err.message);
                }
            });
        });
    </script>
</body>
</html>
