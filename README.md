## Welcome to My page

I hope you have visited my [YouTube channel](https://www.youtube.com/channel/UCSF-smuInDWE6HJGr5JTgwQ?view_as=subscriber). Support me on [Twitter](https://twitter.com/NaffyDharni)

I have developed a game using HTML, CSS and JS.
It is open source. The score is also displayed on the screen. Moreover, there is a feature for level selection which decides the speed of the game.

### This is the code for my project
```markdown
<!DOCTYPE html>
<html>

<head>

  <title>snake game</title>
  <style>

    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      background: black;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      text-align: center;
    }

    canvas {
      border: 1px solid white;
      margin: 0;
    }

    #heading {
      font-size: 7em;
      font-family: Arial;
      color: rgba(0, 0, 0, 0);
      background: url(http://cdn30.us1.fansshare.com/image/wallpaperbackground/nature-wallpapers-nature-wallpapers-wallpapers-html-wallpaper-nature-465289872.jpg);
      -webkit-background-clip: text;
      background-clip: text;
      text-transform: uppercase;
      font-family: 'Courier New', Courier, monospace;
    }

    #score {
      color: #ffffff;
      font-size: 3rem;
      font-family: 'Courier New', Courier, monospace;
    }

  </style>

</head>

<body>

  <h1 id="heading">Snake Game</h1>
  <canvas width="400" height="400" id="game"></canvas>
  <h1 id="score">Score : 0</h1>

  <!-- Main Javascipt Part -->
  <script>
    // Level input
    var level = prompt('We have 8 levels in this game. Choose a level from 1 to 8. Level 5 is recommended.');

    // Deciding the speed according to the level
    if (level == '1') {
      speed = 8
    }
    else if (level == '2'){
      speed = 7
    }
    else if (level == '3'){
      speed = 6
    }
    else if (level == '4'){
      speed = 5
    }
    else if (level == '5'){
      speed = 4
    }
    else if (level == '6'){
      speed = 3
    }
    else if (level == '7'){
      speed = 2
    }
    else if (level == '8'){
      speed = 1
    }
    else {
      speed = 4
    }
 
    var canvas = document.getElementById('game');
    var context = canvas.getContext('2d');
    var scor = document.getElementById('score');
    var score = 0;

    var grid = 16;
    var count = 0;

    // Snake
    var snake = {
      x: 160,
      y: 160,

      // Snake velocity
      dx: grid,
      dy: 0,

      // Keep track of all cells of the snake
      cells: [],

      // Snake length
      maxCells: 4
    };

    // Apple's position
    var apple = {
      x: 320,
      y: 320
    };

    // Creating a random integer
    function getRandomInt(min, max) {
      return Math.floor(Math.random() * (max - min)) + min;
    }

    // Main game loop
    function loop() {
      requestAnimationFrame(loop);

      // Speed of our game
      if (++count < speed) {
        return;
      }

      count = 0;
      context.clearRect(0, 0, canvas.width, canvas.height);

      // Moveing our snake by it's velocity
      snake.x += snake.dx;
      snake.y += snake.dy;

      // Wrapping snake's position horizontally on edge of screen
      if (snake.x < 0) {
        snake.x = canvas.width - grid;
      }
      else if (snake.x >= canvas.width) {
        snake.x = 0;
      }

      // Wrapping snake's position vertically on edge of screen
      if (snake.y < 0) {
        snake.y = canvas.height - grid;
      }
      else if (snake.y >= canvas.height) {
        snake.y = 0;
      }

      // Keeping track of where snake has been
      snake.cells.unshift({ x: snake.x, y: snake.y });

      // Clearing the previous cells
      if (snake.cells.length > snake.maxCells) {
        snake.cells.pop();
      }

      // Drawing an apple for our snake
      context.fillStyle = 'red';
      context.fillRect(apple.x, apple.y, grid - 1, grid - 1);

      // Drawing snake one cell at a time
      context.fillStyle = 'green';
      snake.cells.forEach(function (cell, index) {

        // Drawing boundary of each cell
        context.fillRect(cell.x, cell.y, grid - 1, grid - 1);

        // If the snakee eats the apple
        if (cell.x === apple.x && cell.y === apple.y) {
          snake.maxCells++;
          score++;
          console.log(`The score is : ${score}`);
          scor.innerText = `Score : ${score}`;

          // Deciding new place for our apple
          apple.x = getRandomInt(0, 25) * grid;
          apple.y = getRandomInt(0, 25) * grid;
        }

        // Checking collision with all cells after this one
        for (var i = index + 1; i < snake.cells.length; i++) {

          // Game reset
          if (cell.x === snake.cells[i].x && cell.y === snake.cells[i].y) {
            snake.x = 160;
            snake.y = 160;
            snake.cells = [];
            snake.maxCells = 4;
            snake.dx = grid;
            snake.dy = 0;

            apple.x = getRandomInt(0, 25) * grid;
            apple.y = getRandomInt(0, 25) * grid;

            score = 0;
            console.log(`The score is : ${score}`);
            scor.innerText = `Score : ${score}`;
          }
        }
      });
    }

    // Adding keyboard events to move our snake
    document.addEventListener('keydown', function (e) {

      // Left arrow key
      if (e.which === 37 && snake.dx === 0) {
        snake.dx = -grid;
        snake.dy = 0;
      }
      // Up arrow key
      else if (e.which === 38 && snake.dy === 0) {
        snake.dy = -grid;
        snake.dx = 0;
      }
      // Right arrow key
      else if (e.which === 39 && snake.dx === 0) {
        snake.dx = grid;
        snake.dy = 0;
      }
      // Down arrow key
      else if (e.which === 40 && snake.dy === 0) {
        snake.dy = grid;
        snake.dx = 0;
      }
      
    });

    // Start the game
    requestAnimationFrame(loop);
  </script>
</body>

</html>
```

