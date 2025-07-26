```markdown
# NBA Basketball Stats Analyzer

A simple web-based basketball statistics analysis tool inspired by NBA themes. Built with HTML, CSS, and JavaScript, it allows users to input player stats, display a list of players, and view basic analytics such as total points, average points per player, and the top scorer.

---

## Features

- Add player statistics (name, points, assists, rebounds, games played)
- View a dynamic list of players with their stats
- Automatically calculate and display:
  - Total points scored by all players
  - Average points per player
  - Highlight the top scorer
- NBA-style themed interface

---

## Demo

[Open the project in your browser](#) *(You can copy the code below into an `.html` file and open in your browser)*

---

## How to Use

1. Save the code below as `index.html`.
2. Open `index.html` in your web browser.
3. Enter player name and stats in the input fields.
4. Click **Add Player** to add to the list.
5. View the updated statistics and highlight the top scorer.

---

## Code

```html
<!-- Save this as index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>NBA Basketball Stats Analyzer</title>
<style>
  body {
    margin: 0;
    font-family: 'Arial', sans-serif;
    background: linear-gradient(135deg, #0d1b2a, #1b263b);
    color: #fff;
  }

  header {
    text-align: center;
    padding: 20px;
    background-color: #0f3057;
    font-family: 'Arial Black', sans-serif;
    font-size: 2em;
  }

  .container {
    max-width: 900px;
    margin: 20px auto;
    padding: 20px;
    background-color: #23395b;
    border-radius: 10px;
  }

  h2 {
    text-align: center;
    margin-bottom: 15px;
  }

  form {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
    justify-content: center;
  }

  input[type="text"],
  input[type="number"] {
    padding: 8px;
    border-radius: 5px;
    border: none;
    width: 150px;
  }

  button {
    padding: 8px 16px;
    border: none;
    border-radius: 5px;
    background-color: #f4a261;
    cursor: pointer;
    font-weight: bold;
  }

  button:hover {
    background-color: #e76f51;
  }

  table {
    width: 100%;
    margin-top: 20px;
    border-collapse: collapse;
  }

  th, td {
    padding: 10px;
    text-align: center;
    border-bottom: 1px solid #ddd;
  }

  th {
    background-color: #2b7a78;
  }

  tr.top-scorer {
    background-color: #ffd700;
    font-weight: bold;
  }

  .stats {
    margin-top: 20px;
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .stat {
    margin: 5px 0;
  }
</style>
</head>
<body>

<header>
  NBA Basketball Stats Analyzer
</header>

<div class="container">
  <h2>Add Player Stats</h2>
  <form id="statsForm">
    <input type="text" id="name" placeholder="Player Name" required />
    <input type="number" id="points" placeholder="Points" min="0" required />
    <input type="number" id="assists" placeholder="Assists" min="0" required />
    <input type="number" id="rebounds" placeholder="Rebounds" min="0" required />
    <input type="number" id="games" placeholder="Games Played" min="1" required />
    <button type="submit">Add Player</button>
  </form>

  <h2>Player Stats</h2>
  <table id="playersTable">
    <thead>
      <tr>
        <th>Player</th>
        <th>Points</th>
        <th>Assists</th>
        <th>Rebounds</th>
        <th>Games</th>
      </tr>
    </thead>
    <tbody></tbody>
  </table>

  <div class="stats" id="analysis">
    <h2>Analysis</h2>
    <div class="stat" id="totalPoints">Total Points: 0</div>
    <div class="stat" id="averagePoints">Average Points per Player: 0</div>
    <div class="stat" id="topScorer">Top Scorer: N/A</div>
  </div>
</div>

<script>
  const players = [];

  const form = document.getElementById('statsForm');
  const tbody = document.querySelector('#playersTable tbody');

  const totalPointsDiv = document.getElementById('totalPoints');
  const averagePointsDiv = document.getElementById('averagePoints');
  const topScorerDiv = document.getElementById('topScorer');

  form.addEventListener('submit', function(e) {
    e.preventDefault();

    const name = document.getElementById('name').value.trim();
    const points = parseInt(document.getElementById('points').value);
    const assists = parseInt(document.getElementById('assists').value);
    const rebounds = parseInt(document.getElementById('rebounds').value);
    const games = parseInt(document.getElementById('games').value);

    if (name && !isNaN(points) && !isNaN(assists) && !isNaN(rebounds) && !isNaN(games)) {
      const player = { name, points, assists, rebounds, games };
      players.push(player);
      addPlayerToTable(player);
      updateAnalysis();
      form.reset();
    }
  });

  function addPlayerToTable(player) {
    const row = document.createElement('tr');

    row.innerHTML = `
      <td>${player.name}</td>
      <td>${player.points}</td>
      <td>${player.assists}</td>
      <td>${player.rebounds}</td>
      <td>${player.games}</td>
    `;

    tbody.appendChild(row);
  }

  function updateAnalysis() {
    let totalPoints = 0;
    let maxPoints = -Infinity;
    let topPlayerName = '';

    players.forEach(player => {
      totalPoints += player.points;
      if (player.points > maxPoints) {
        maxPoints = player.points;
        topPlayerName = player.name;
      }
    });

    const totalPlayers = players.length;
    const avgPoints = totalPlayers > 0 ? (totalPoints / totalPlayers).toFixed(2) : 0;

    // Clear previous top scorer highlight
    Array.from(tbody.children).forEach(row => row.classList.remove('top-scorer'));

    // Highlight top scorer
    if (players.length > 0) {
      const topIndex = players.findIndex(p => p.name === topPlayerName);
      tbody.children[topIndex].classList.add('top-scorer');
    }

    totalPointsDiv.textContent = `Total Points: ${totalPoints}`;
    averagePointsDiv.textContent = `Average Points per Player: ${avgPoints}`;
    topScorerDiv.textContent = `Top Scorer: ${topPlayerName} (${maxPoints} pts)`;
  }
</script>

</body>
</html>
``

---

## Contributing

Feel free to fork, modify, or extend this project. If you'd like to add features like saving data, charts, or more stats, pull requests are welcome!

---

## License

This project is for educational purposes. No license restrictions.

---

## Notes

- This is a basic static web app; data is stored only in the browser session.
- For persistent data, consider integrating local storage or a backend.

---

Enjoy analyzing your basketball stats! 🏀

---
``

---
