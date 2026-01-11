# Stickman Fighter

A 2-player local multiplayer fighting game built with HTML5 Canvas. Two stick figure characters battle on floating platforms using swords and collectible weapons.

**Play now:** https://pwmckenna.github.io/stickman/

## Game Overview

- **Genre:** 2D Platform Fighter
- **Players:** 2 (local, shared keyboard or touch controls)
- **Tech:** Single HTML file with embedded CSS and JavaScript
- **Canvas:** 1400x500 pixels

## Controls

### Keyboard (Desktop)

| Action | Player 1 | Player 2 |
|--------|----------|----------|
| Move Left | A | ← Arrow |
| Move Right | D | → Arrow |
| Jump | W | ↑ Arrow |
| Crouch | S | ↓ Arrow |
| Roll | S + A/D | ↓ + ←/→ |
| Attack | F | L |
| Smash | G | K |

### Touch Controls (iPad/Mobile)

- **Player 1:** Left side of screen - D-pad + Jump/Attack/Smash buttons
- **Player 2:** Right side of screen - D-pad + Jump/Attack/Smash buttons
- Touch controls auto-display on touch devices
- Tap screen to restart after game over

## Game Mechanics

### Movement
- **Walk:** Constant speed (5 units/frame)
- **Jump:** Single jump, height calibrated to reach one platform level
- **Crouch:** Press down to duck; running into a crouching player launches you over them
- **Roll:** Press down + direction for a quick dodge roll (same speed as walking)

### Combat
- **Attack:** Quick sword swing, lower damage, faster cooldown
- **Smash:** Heavy swing with high knockback but low damage (5 HP)
- **Hit Detection:** Entire blade does damage (sampled at 10 points along the blade)
- **Knockback:** Horizontal knockback with minimal vertical (won't knock to higher platforms)
- **Invincibility:** Brief invincibility frames after being hit

### Weapons
Default weapon is sword. Collectible power-ups grant temporary weapons (5 seconds):

| Weapon | Damage | Knockback | Range | Special |
|--------|--------|-----------|-------|---------|
| Sword | 10 | 8 | 45 | Default weapon |
| Hammer | 8 | 20 | 35 | High knockback |
| Spear | 15 | 5 | 65 | Long range |
| Axe | 20 | 12 | 40 | High damage |
| Bow | 12 | 6 | 30 | Ranged (shoots projectiles) |

### Power-ups
- Spawn every 5 seconds (max 3 on screen)
- Bounce around the screen off walls and ceiling
- Collected on contact
- Grant weapon for 300 frames (5 seconds at 60fps)

### Projectiles (Bow)
- Fire by pressing Attack while holding Bow
- Affected by gravity
- Stop when hitting platforms
- Deal damage on contact with opponent

## Stage Design

### Platforms
5 levels of floating platforms:
- **Level 1 (y=420):** 4 large platforms (200-350px wide)
- **Level 2 (y=340):** 4 large platforms (200-250px wide)
- **Level 3 (y=260):** 5 medium platforms (180px wide)
- **Level 4 (y=180):** 5 small platforms (140px wide)
- **Level 5 (y=100):** 5 smallest platforms (100px wide)

Platforms are one-way - you can jump through from below but land on top.

### Spike Pit
- Visual metal spikes line the bottom of the screen
- Deals 0.5 damage per frame (30 HP/second) when touching
- Players can stand on spikes and jump out
- No instant death - gives time to escape

### Background
- Minecraft-style blocky aesthetic
- Pre-rendered for performance (no flickering)
- Blue sky blocks with variation
- White block clouds
- Yellow block sun
- Dirt and stone blocks at bottom
- Grass-topped dirt platforms

## Win Conditions

- Reduce opponent's health to 0
- Winner performs a victory dab animation
- Press SPACE (keyboard) or tap screen (touch) to restart

## Visual Style

### Characters
- Classic stick figure design
- Circle head (outline only)
- Line body/torso
- Thin line arms and legs
- Player 1: Blue (#4a9eff)
- Player 2: Red (#ff4a4a)

### Animations
- Walking leg movement
- Attack/Smash sword swings
- Roll tumble animation
- Victory dab pose
- Hit flash effect
- Invincibility flicker

### Effects
- Screen shake on hits (stronger for smash)
- Weapon glow during attacks
- Health bar UI at top of screen

## Technical Details

### Constants
```javascript
GRAVITY = 0.6
MOVE_SPEED = 5
JUMP_FORCE = -10.5
ROLL_SPEED = 5
ROLL_DURATION = 20 frames
POWERUP_DURATION = 300 frames
ATTACK_DAMAGE = 10
SMASH_DAMAGE = 5
ATTACK_KNOCKBACK = 8
SMASH_KNOCKBACK = 25
```

### Player Properties
- Position (x, y), Velocity (vx, vy)
- Health (100 max), Facing direction
- Attack/Smash timers and cooldowns
- Roll state and timer
- Crouch state
- Current weapon and timer
- Invincibility frames

### Performance
- Background pre-rendered to off-screen canvas
- Single requestAnimationFrame game loop
- Touch events use passive: false for responsiveness

## File Structure
```
stickman/
├── index.html    # Complete game (HTML + CSS + JS)
└── README.md     # This documentation
```

## Deployment

Hosted on GitHub Pages:
- Repository: https://github.com/pwmckenna/stickman
- Live game: https://pwmckenna.github.io/stickman/

## Future Ideas

- Sound effects
- More weapon types
- Character selection
- Online multiplayer
- Additional stages
- Mobile-optimized layout
