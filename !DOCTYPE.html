<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Doodle Jump Clone</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            overflow: hidden;
            touch-action: none;
            background-color: #87CEEB;
            font-family: Arial, sans-serif;
        }
        #gameCanvas {
            display: block;
            width: 100%;
            height: 100%;
            touch-action: none;
        }
        #ui {
            position: absolute;
            top: 10px;
            left: 10px;
            color: white;
            font-size: 18px;
            text-shadow: 1px 1px 2px black;
        }
        #restartBtn {
            position: absolute;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            padding: 10px 20px;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 16px;
            display: none;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div id="ui">
        Score: <span id="score">0</span> | 
        High: <span id="highScore">0</span> | 
        Coins: <span id="coins">0</span>
    </div>
    <button id="restartBtn">Restart</button>
    <canvas id="gameCanvas"></canvas>

    <script>
        // Game variables
        const canvas = document.getElementById('gameCanvas');
        const ctx = canvas.getContext('2d');
        const scoreElement = document.getElementById('score');
        const highScoreElement = document.getElementById('highScore');
        const coinsElement = document.getElementById('coins');
        const restartBtn = document.getElementById('restartBtn');
        
        // Set canvas size
        function resizeCanvas() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        }
        resizeCanvas();
        window.addEventListener('resize', resizeCanvas);
        
        // Game settings
        const GRAVITY = 0.2;
        const JUMP_FORCE = 12;
        const BOOST_JUMP_FORCE = 18;
        const PLATFORM_COUNT = 8;
        const COIN_SPAWN_RATE = 0.3;
        const BLACK_HOLE_SPAWN_RATE = 0.1;
        const TRAP_SPAWN_RATE = 0.15;
        const BOOST_SPAWN_RATE = 0.1;
        
        // Game state
        let score = 0;
        let coins = 0;
        let highScore = localStorage.getItem('highScore') || 0;
        let gameOver = false;
        let platforms = [];
        let coinsList = [];
        let blackHoles = [];
        let traps = [];
        let boosts = [];
        
        // Player
        const player = {
            x: canvas.width / 2,
            y: canvas.height / 2,
            width: 40,
            height: 40,
            velX: 0,
            velY: 0,
            isJumping: false,
            texture: null,
            
            reset: function() {
                this.x = canvas.width / 2;
                this.y = canvas.height / 2;
                this.velX = 0;
                this.velY = 0;
                this.isJumping = false;
            },
            
            update: function() {
                // Apply gravity
                this.velY += GRAVITY;
                
                // Update position
                this.x += this.velX;
                this.y += this.velY;
                
                // Horizontal boundaries
                if (this.x < 0) this.x = canvas.width;
                if (this.x > canvas.width) this.x = 0;
                
                // Check if player fell off the bottom
                if (this.y > canvas.height + 100) {
                    gameOver = true;
                    restartBtn.style.display = 'block';
                    
                    // Update high score
                    if (score > highScore) {
                        highScore = score;
                        localStorage.setItem('highScore', highScore);
                        highScoreElement.textContent = highScore;
                    }
                }
            },
            
            draw: function() {
                if (this.texture) {
                    ctx.drawImage(this.texture, this.x - this.width/2, this.y - this.height, this.width, this.height);
                } else {
                    // Default player (simple circle)
                    ctx.fillStyle = '#FF5733';
                    ctx.beginPath();
                    ctx.arc(this.x, this.y - this.height/2, this.width/2, 0, Math.PI * 2);
                    ctx.fill();
                    
                    // Eyes
                    ctx.fillStyle = 'white';
                    ctx.beginPath();
                    ctx.arc(this.x - 8, this.y - this.height/2 - 5, 5, 0, Math.PI * 2);
                    ctx.arc(this.x + 8, this.y - this.height/2 - 5, 5, 0, Math.PI * 2);
                    ctx.fill();
                    
                    ctx.fillStyle = 'black';
                    ctx.beginPath();
                    ctx.arc(this.x - 8, this.y - this.height/2 - 5, 2, 0, Math.PI * 2);
                    ctx.arc(this.x + 8, this.y - this.height/2 - 5, 2, 0, Math.PI * 2);
                    ctx.fill();
                }
            },
            
            jump: function(force = JUMP_FORCE) {
                this.velY = -force;
                this.isJumping = true;
            }
        };
        
        // Platform types
        const PLATFORM_TYPES = {
            NORMAL: { color: '#4CAF50', width: 70, height: 15, isBreakable: false, isMoving: false },
            BREAKABLE: { color: '#9E9E9E', width: 70, height: 15, isBreakable: true, isMoving: false },
            MOVING: { color: '#2196F3', width: 70, height: 15, isBreakable: false, isMoving: true }
        };
        
        // Platform class
        function Platform(x, y, type) {
            this.x = x;
            this.y = y;
            this.width = type.width;
            this.height = type.height;
            this.color = type.color;
            this.isBreakable = type.isBreakable;
            this.isMoving = type.isMoving;
            this.velX = this.isMoving ? (Math.random() * 2 - 1) * 1.5 : 0;
            this.type = type;
            
            this.update = function() {
                if (this.isMoving) {
                    this.x += this.velX;
                    if (this.x < 0 || this.x + this.width > canvas.width) {
                        this.velX *= -1;
                    }
                }
            };
            
            this.draw = function() {
                ctx.fillStyle = this.color;
                ctx.fillRect(this.x, this.y, this.width, this.height);
            };
        }
        
        // Coin class
        function Coin(x, y) {
            this.x = x;
            this.y = y;
            this.radius = 10;
            this.collected = false;
            this.texture = null;
            
            this.draw = function() {
                if (this.texture) {
                    ctx.drawImage(this.texture, this.x - this.radius, this.y - this.radius, this.radius * 2, this.radius * 2);
                } else {
                    ctx.fillStyle = '#FFD700';
                    ctx.beginPath();
                    ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2);
                    ctx.fill();
                    
                    ctx.fillStyle = '#FFC600';
                    ctx.beginPath();
                    ctx.arc(this.x, this.y, this.radius - 3, 0, Math.PI * 2);
                    ctx.fill();
                }
            };
        }
        
        // Black Hole class
        function BlackHole(x, y) {
            this.x = x;
            this.y = y;
            this.radius = 25;
            this.pullRadius = 60;
            this.pullForce = 0.5;
            
            this.draw = function() {
                // Outer ring
                ctx.fillStyle = 'rgba(0, 0, 0, 0.7)';
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.pullRadius, 0, Math.PI * 2);
                ctx.fill();
                
                // Black hole
                ctx.fillStyle = 'black';
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2);
                ctx.fill();
                
                // Swirling effect
                ctx.strokeStyle = 'rgba(255, 255, 255, 0.3)';
                ctx.lineWidth = 2;
                for (let i = 0; i < 3; i++) {
                    ctx.beginPath();
                    ctx.arc(this.x, this.y, this.radius + 5 + i * 5, 0, Math.PI * (i % 2 === 0 ? 1.5 : 0.5));
                    ctx.stroke();
                }
            };
            
            this.update = function() {
                // Check if player is in pull radius
                const dx = player.x - this.x;
                const dy = (player.y - player.height) - this.y;
                const distance = Math.sqrt(dx * dx + dy * dy);
                
                if (distance < this.pullRadius) {
                    // Calculate pull force
                    const angle = Math.atan2(dy, dx);
                    const force = this.pullForce * (1 - distance / this.pullRadius);
                    
                    player.velX -= Math.cos(angle) * force;
                    player.velY -= Math.sin(angle) * force;
                    
                    // If player gets too close, game over
                    if (distance < this.radius) {
                        gameOver = true;
                        restartBtn.style.display = 'block';
                    }
                }
            };
        }
        
        // Trap class (spikes)
        function Trap(x, y) {
            this.x = x;
            this.y = y;
            this.width = 30;
            this.height = 20;
            
            this.draw = function() {
                ctx.fillStyle = '#FF5252';
                
                // Draw spikes
                const spikeCount = 5;
                const spikeWidth = this.width / spikeCount;
                
                for (let i = 0; i < spikeCount; i++) {
                    ctx.beginPath();
                    ctx.moveTo(this.x + i * spikeWidth, this.y + this.height);
                    ctx.lineTo(this.x + (i + 0.5) * spikeWidth, this.y);
                    ctx.lineTo(this.x + (i + 1) * spikeWidth, this.y + this.height);
                    ctx.closePath();
                    ctx.fill();
                }
            };
            
            this.checkCollision = function() {
                return (
                    player.x + player.width/2 > this.x &&
                    player.x - player.width/2 < this.x + this.width &&
                    player.y > this.y &&
                    player.y - player.height < this.y + this.height
                );
            };
        }
        
        // Jump Boost class
        function JumpBoost(x, y) {
            this.x = x;
            this.y = y;
            this.radius = 15;
            this.collected = false;
            
            this.draw = function() {
                ctx.fillStyle = '#FF9800';
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2);
                ctx.fill();
                
                ctx.fillStyle = '#FFC107';
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.radius - 5, 0, Math.PI * 2);
                ctx.fill();
                
                // Arrow up symbol
                ctx.fillStyle = '#FF5722';
                ctx.beginPath();
                ctx.moveTo(this.x, this.y - this.radius + 5);
                ctx.lineTo(this.x - 5, this.y - this.radius + 10);
                ctx.lineTo(this.x + 5, this.y - this.radius + 10);
                ctx.closePath();
                ctx.fill();
            };
        }
        
        // Initialize game
        function initGame() {
            platforms = [];
            coinsList = [];
            blackHoles = [];
            traps = [];
            boosts = [];
            score = 0;
            coins = 0;
            gameOver = false;
            scoreElement.textContent = score;
            coinsElement.textContent = coins;
            highScoreElement.textContent = highScore;
            restartBtn.style.display = 'none';
            
            player.reset();
            
            // Create initial platforms
            for (let i = 0; i < PLATFORM_COUNT; i++) {
                createPlatform(canvas.height - i * (canvas.height / PLATFORM_COUNT));
            }
        }
        
        // Create a new platform
        function createPlatform(yPos) {
            const types = Object.values(PLATFORM_TYPES);
            let type;
            
            // Randomly select platform type with different probabilities
            const rand = Math.random();
            if (rand < 0.6) {
                type = PLATFORM_TYPES.NORMAL; // 60% chance
            } else if (rand < 0.85) {
                type = PLATFORM_TYPES.BREAKABLE; // 25% chance
            } else {
                type = PLATFORM_TYPES.MOVING; // 15% chance
            }
            
            const x = Math.random() * (canvas.width - type.width);
            const platform = new Platform(x, yPos, type);
            platforms.push(platform);
            
            // Sometimes add a coin on the platform
            if (Math.random() < COIN_SPAWN_RATE && type !== PLATFORM_TYPES.BREAKABLE) {
                const coinX = platform.x + platform.width / 2;
                const coinY = platform.y - 20;
                coinsList.push(new Coin(coinX, coinY));
            }
            
            // Sometimes add a black hole near the platform
            if (Math.random() < BLACK_HOLE_SPAWN_RATE) {
                const holeX = Math.random() * canvas.width;
                const holeY = platform.y - 100 - Math.random() * 50;
                blackHoles.push(new BlackHole(holeX, holeY));
            }
            
            // Sometimes add a trap near the platform
            if (Math.random() < TRAP_SPAWN_RATE) {
                const trapX = Math.random() * (canvas.width - 30);
                const trapY = platform.y - 50 - Math.random() * 30;
                traps.push(new Trap(trapX, trapY));
            }
            
            // Sometimes add a jump boost near the platform
            if (Math.random() < BOOST_SPAWN_RATE) {
                const boostX = Math.random() * (canvas.width - 30);
                const boostY = platform.y - 50 - Math.random() * 30;
                boosts.push(new JumpBoost(boostX, boostY));
            }
        }
        
        // Check collision between player and platforms
        function checkPlatformCollision() {
            for (let i = 0; i < platforms.length; i++) {
                const platform = platforms[i];
                
                if (
                    player.velY > 0 &&
                    player.x + player.width/2 > platform.x &&
                    player.x - player.width/2 < platform.x + platform.width &&
                    player.y + player.velY > platform.y &&
                    player.y < platform.y
                ) {
                    // Player landed on a platform
                    player.jump(platform.type === PLATFORM_TYPES.BREAKABLE ? JUMP_FORCE * 0.8 : JUMP_FORCE);
                    
                    // Break breakable platforms
                    if (platform.isBreakable) {
                        platforms.splice(i, 1);
                        i--;
                    }
                    
                    // Add score when jumping on a platform
                    if (player.y < canvas.height / 2) {
                        const scoreAdd = Math.floor(10 + (canvas.height / 2 - player.y) / 10);
                        score += scoreAdd;
                        scoreElement.textContent = score;
                        
                        // Move everything down
                        const moveY = canvas.height / 2 - player.y;
                        player.y += moveY;
                        
                        for (let p of platforms) p.y += moveY;
                        for (let c of coinsList) c.y += moveY;
                        for (let h of blackHoles) h.y += moveY;
                        for (let t of traps) t.y += moveY;
                        for (let b of boosts) b.y += moveY;
                    }
                    
                    // Create new platforms when needed
                    if (platforms[platforms.length - 1].y > canvas.height) {
                        createPlatform(platforms[platforms.length - 1].y - canvas.height / PLATFORM_COUNT);
                    }
                    
                    break;
                }
            }
        }
        
        // Check coin collection
        function checkCoinCollection() {
            for (let i = 0; i < coinsList.length; i++) {
                const coin = coinsList[i];
                
                if (!coin.collected) {
                    const dx = player.x - coin.x;
                    const dy = player.y - coin.y;
                    const distance = Math.sqrt(dx * dx + dy * dy);
                    
                    if (distance < player.width/2 + coin.radius) {
                        coin.collected = true;
                        coins++;
                        coinsElement.textContent = coins;
                        coinsList.splice(i, 1);
                        i--;
                    }
                }
            }
        }
        
        // Check jump boost collection
        function checkBoostCollection() {
            for (let i = 0; i < boosts.length; i++) {
                const boost = boosts[i];
                
                if (!boost.collected) {
                    const dx = player.x - boost.x;
                    const dy = player.y - boost.y;
                    const distance = Math.sqrt(dx * dx + dy * dy);
                    
                    if (distance < player.width/2 + boost.radius) {
                        boost.collected = true;
                        player.jump(BOOST_JUMP_FORCE);
                        boosts.splice(i, 1);
                        i--;
                    }
                }
            }
        }
        
        // Check trap collision
        function checkTrapCollision() {
            for (let i = 0; i < traps.length; i++) {
                if (traps[i].checkCollision()) {
                    gameOver = true;
                    restartBtn.style.display = 'block';
                    
                    // Update high score
                    if (score > highScore) {
                        highScore = score;
                        localStorage.setItem('highScore', highScore);
                        highScoreElement.textContent = highScore;
                    }
                    break;
                }
            }
        }
        
        // Touch controls
        let touchStartX = 0;
        
        canvas.addEventListener('touchstart', function(e) {
            e.preventDefault();
            touchStartX = e.touches[0].clientX;
        }, false);
        
        canvas.addEventListener('touchmove', function(e) {
            e.preventDefault();
            const touchX = e.touches[0].clientX;
            player.velX = (touchX - touchStartX) * 0.1;
            touchStartX = touchX;
        }, false);
        
        canvas.addEventListener('touchend', function(e) {
            e.preventDefault();
            player.velX = 0;
        }, false);
        
        // Mouse controls (for testing on desktop)
        let mouseDown = false;
        let mouseStartX = 0;
        
        canvas.addEventListener('mousedown', function(e) {
            mouseDown = true;
            mouseStartX = e.clientX;
        });
        
        canvas.addEventListener('mousemove', function(e) {
            if (mouseDown) {
                player.velX = (e.clientX - mouseStartX) * 0.1;
                mouseStartX = e.clientX;
            }
        });
        
        canvas.addEventListener('mouseup', function() {
            mouseDown = false;
            player.velX = 0;
        });
        
        // Restart button
        restartBtn.addEventListener('click', initGame);
        
        // Game loop
        function gameLoop() {
            if (!gameOver) {
                // Clear canvas
                ctx.clearRect(0, 0, canvas.width, canvas.height);
                
                // Draw background (can be replaced with an image)
                ctx.fillStyle = '#87CEEB';
                ctx.fillRect(0, 0, canvas.width, canvas.height);
                
                // Update and draw platforms
                for (let platform of platforms) {
                    platform.update();
                    platform.draw();
                }
                
                // Update and draw coins
                for (let coin of coinsList) {
                    coin.draw();
                }
                
                // Update and draw black holes
                for (let hole of blackHoles) {
                    hole.update();
                    hole.draw();
                }
                
                // Draw traps
                for (let trap of traps) {
                    trap.draw();
                }
                
                // Draw boosts
                for (let boost of boosts) {
                    boost.draw();
                }
                
                // Update player
                player.update();
                
                // Check collisions
                checkPlatformCollision();
                checkCoinCollection();
                checkBoostCollection();
                checkTrapCollision();
                
                // Draw player
                player.draw();
            }
            
            requestAnimationFrame(gameLoop);
        }
        
        // Load custom textures (if provided)
        function loadCustomTextures() {
            // This is where you can load custom textures
            // For example:
            // player.texture = new Image();
            // player.texture.src = 'path/to/player.png';
            
            // For coins:
            // for (let coin of coinsList) {
            //     coin.texture = new Image();
            //     coin.texture.src = 'path/to/coin.png';
            // }
        }
        
        // Start the game
        initGame();
        loadCustomTextures();
        gameLoop();
    </script>
</body>
</html>