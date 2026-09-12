# Planet Simulation 🪐

A 2D gravitational simulation of the inner Solar System, built with **Python** and **Pygame**. It models the Sun, Mercury, Venus, Earth, and Mars using Newtonian gravity, and renders their orbits in real time.

![Python](https://img.shields.io/badge/python-3.8%2B-blue)
![Pygame](https://img.shields.io/badge/pygame-2.x-green)
![License](https://img.shields.io/badge/license-MIT-lightgrey)

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Demo](#demo)
- [Project Structure](#project-structure)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
- [How It Works](#how-it-works)
- [Customization](#customization)
- [Roadmap](#roadmap)
- [License](#license)

---

## Overview

This project simulates planetary motion using **Newton's Law of Universal Gravitation**:

```
F = G * (M * m) / r²
```

Each planet's position is updated every frame based on the gravitational force exerted on it by every other body in the system (including the Sun). The result is an approximation of real orbital mechanics, with each planet tracing an elliptical/circular path around the Sun.

## Features

- Real-time physics simulation using actual astronomical constants (AU, gravitational constant, planetary masses, and orbital velocities)
- Visual orbit trails for each planet
- Live distance-to-Sun readout displayed next to each planet (in km)
- Simple, dependency-light codebase (just Pygame + the standard library)
- Easily extendable to add more planets, moons, or comets

## Demo

When run, the simulation opens an 800x800 window on a dark blue "space" background showing:

- ☀️ The Sun (yellow, stationary at the center)
- 🔵 Earth (blue)
- 🔴 Mars (red)
- ⚪ Mercury (grey)
- 🟡 Venus (tan/khaki)

Each planet orbits the Sun while leaving a trailing path behind it.

## Project Structure

Suggested layout if you want to expand this into a full project:

```
planet-simulation/
│
├── README.md                 # Project documentation (this file)
├── requirements.txt          # Python dependencies
├── LICENSE                   # License file
├── .gitignore                # Git ignore rules
│
├── src/
│   ├── main.py                # Entry point — runs the simulation loop
│   ├── planet.py               # Planet class (physics + rendering logic)
│   └── constants.py            # Colors, screen size, physical constants
│
└── assets/
    └── screenshots/           # Screenshots / demo GIFs for the README
```

## Requirements

- Python 3.8 or higher
- [Pygame](https://www.pygame.org/) 2.x

## Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/<your-username>/planet-simulation.git
   cd planet-simulation
   ```

2. **(Optional) Create a virtual environment**
   ```bash
   python -m venv venv
   source venv/bin/activate      # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install pygame
   ```

   Or, if using a `requirements.txt`:
   ```bash
   pip install -r requirements.txt
   ```

## Usage

Run the simulation from the project root:

```bash
python src/main.py
```

A window will open showing the simulation. Close the window or press the quit button to exit.

## How It Works

### 1. The `Planet` Class

Each planet is represented as an instance of the `Planet` class, storing:

| Attribute | Description |
|---|---|
| `x`, `y` | Position in meters |
| `x_vel`, `y_vel` | Velocity in m/s |
| `mass` | Mass in kilograms |
| `radius` | Display radius in pixels |
| `color` | RGB tuple for rendering |
| `sun` | Boolean flag marking the central star |
| `orbit` | List of past `(x, y)` positions for drawing the trail |

### 2. Gravitational Attraction

The `attraction()` method calculates the gravitational force between the current planet and another body using Newton's law, then resolves that force into `x` and `y` components using trigonometry (`atan2`, `cos`, `sin`).

### 3. Updating Positions

The `update_position()` method sums the gravitational forces from every other planet, converts force into acceleration (`F / mass`), updates velocity, and then updates position — all scaled by the simulation's `TIMESTEP` (1 simulated day per update).

### 4. Scaling for Display

Since real distances are measured in meters (with 1 AU ≈ 149.6 million km), the `SCALE` constant converts these massive real-world distances into pixel coordinates that fit inside the 800x800 window.

### 5. The Main Loop

The `main()` function initializes the Sun and planets with their starting positions and orbital velocities, then runs a loop that:
1. Clears the screen
2. Updates each planet's position based on gravity
3. Draws each planet and its orbit trail
4. Refreshes the display at 60 FPS

## Customization

You can easily tweak the simulation:

- **Add a new planet:**
  ```python
  jupiter = Planet(5.2 * Planet.AU, 0, 20, (255, 165, 0), 1.898 * 10**27)
  jupiter.y_vel = -13.07 * 1000
  planets.append(jupiter)
  ```
- **Change simulation speed:** Adjust `TIMESTEP` (currently `3600 * 24`, i.e., 1 day per frame)
- **Change zoom level:** Adjust the `SCALE` constant
- **Change window size:** Modify `WIDTH` and `HEIGHT`

## Roadmap

- [ ] Add outer planets (Jupiter, Saturn, Uranus, Neptune)
- [ ] Add a UI slider to control simulation speed
- [ ] Add pause/resume and reset controls
- [ ] Export orbit data to CSV for analysis
- [ ] Add unit tests for physics calculations

## License

This project is open source and available under the [MIT License](LICENSE).

---

*Inspired by classical Newtonian orbital mechanics — from Copernicus's early trigonometric estimates of planetary distances to modern real-time simulation.*
