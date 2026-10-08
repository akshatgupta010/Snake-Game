# Complete Snake Game Architecture & Logic Notes
*Source: [This JS Project will fix your logic problem | JS Game.](https://www.youtube.com/watch?v=SFLs1fYb5QA&list=PLfy1uVlOm1CU&index=4&t=7576s)*  
*Instructor: Ankur Prajapati ([Sheryians Coding School](https://www.youtube.com/@sheryians))*

---

## 1. Project Overview & Layout Architecture
* **Top Meta/Info Bar (`infos` container):**
  * **High Score:** Persisted across sessions via `localStorage`.
  * **Current Score:** Increases dynamically as food items are collected.
  * **Game Timer:** Tracks active session duration in minutes and seconds (`MM:SS`).
* **Game Canvas / Board (`board` container):**
  * Dedicated container displaying the grid, snake body blocks, and food item.

---

## 2. Discrete Grid & Coordinate Plane Setup
* **Grid Abstraction:** The board is not rendered using continuous raw pixels. Instead, it is partitioned into a discrete 2D matrix of coordinate cells $(X, Y)$:
  * `X`: Horizontal coordinate axis (columns).
  * `Y`: Vertical coordinate axis (rows).
* **Block Resolution Calculation:**
  $$\text{totalCols} = \frac{\text{boardWidth}}{\text{blockSize}}, \quad \text{totalRows} = \frac{\text{boardHeight}}{\text{blockSize}}$$
* **Unit Stepping:** All movement vectors operate strictly in whole integer increments ($1$ unit step per game tick), eliminating fractional alignment issues.

---

## 3. Data Structures & State Management
* **Snake Representation:** Managed as an array of coordinate objects arranged from head to tail:
  ```javascript
  let snake = [
    { x: 5, y: 5 }, // Index 0: Head (leading segment)
    { x: 4, y: 5 }, // Body segment
    { x: 3, y: 5 }  // Tail segment
  ];