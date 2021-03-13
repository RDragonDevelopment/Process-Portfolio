# **DGL104 Process Portfolio**
## Ryan Dragon - N0180886
---
---
## **Activity 0101:**

<details>
<summary>Click to expand answer</summary>

During the first semester of my Web and Mobile Application Development Diploma program, I struggled to work out what loops to use in specific situations. After learning and experiencing multiple coding languages, I learned the difference between loops such as for, for-in, while, etc. Once I started to become more comfortable with the code, I was able to confidently browse W3Schools and past assignments if I ever had issues come up again. With this deeper understanding I was able to effectively find solutions to a wide array of issues I have encountered over the last year and a half.

</details>

---

## **Activity 0102:**

<details>
<summary>Click to expand answer</summary>

<details>
<summary>Example Code</summary>

```javascript
"use strict";

// Canvas references
const canvas = document.querySelector("canvas");
const ctx = canvas.getContext("2d");

// UI references
const restartButton = document.querySelector("#restart");
const undoButton = document.querySelector("#undo");
const colorSelectButtons = document.querySelectorAll(".color-select");

// Constants
const CELL_COLORS = {
    red: [255, 0, 0],
    blue: [0, 0, 255],
    white: [255, 255, 255],
};
const CELLS_PER_AXIS = 3;
const CELL_WIDTH = canvas.width / CELLS_PER_AXIS;
const CELL_HEIGHT = canvas.height / CELLS_PER_AXIS;

// Game objects
let replacementColor = CELL_COLORS.red;
let grids;

// Game Logic

function startGame(startingGrid = []) {
    if (startingGrid.length === 0) {
        startingGrid = initializeGrid();
    }
    initializeHistory(startingGrid);
    updateBoard();
    undoButton.disabled = true;
}

function initializeGrid() {
    const newGrid = [];
    for (let i = 0; i < CELLS_PER_AXIS * CELLS_PER_AXIS; i++) {
        newGrid.push(CELL_COLORS.white);
    }
    return newGrid;
}

function initializeHistory(startingGrid) {
    grids = [];
    grids.push(startingGrid);
}

function rollBackHistory() {
    if (grids.length > 0) {
        grids = grids.slice(0, grids.length - 1);
    }
    if (grids.length == 1) {
        undoButton.disabled = true;
    }
}

function renderCells(grid) {
    for (let i = 0; i < grid.length; i++) {
        ctx.fillStyle = `rgb(${grid[i][0]}, ${grid[i][1]}, ${grid[i][2]})`;
        ctx.fillRect(
            (i % CELLS_PER_AXIS) * CELL_WIDTH,
            Math.floor(i / CELLS_PER_AXIS) * CELL_HEIGHT,
            CELL_WIDTH,
            CELL_HEIGHT
        );
    }
}

function updateGridAt(mousePositionX, mousePositionY) {
    const gridCoordinates = convertCartesiansToGrid(
        mousePositionX,
        mousePositionY
    );
    const newGrid = grids[grids.length - 1].slice();
    squareFill(
        newGrid,
        gridCoordinates,
        newGrid[gridCoordinates.row * CELLS_PER_AXIS + gridCoordinates.column]
    );
    grids.push(newGrid);
    undoButton.disabled = false;
}

function squareFill(grid, gridCoordinate, colorToChange) {
    if (arraysAreEqual(colorToChange, replacementColor)) {
        return;
    } else {
        grid[
            gridCoordinate.row * CELLS_PER_AXIS + gridCoordinate.column
        ] = replacementColor;
    }
    return;
}

function renderLines() {
    ctx.beginPath();
    ctx.moveTo(200, 0);
    ctx.lineTo(200, 600);
    ctx.lineWidth = 5;
    ctx.stroke();
    ctx.beginPath();
    ctx.moveTo(400, 0);
    ctx.lineTo(400, 600);
    ctx.lineWidth = 5;
    ctx.stroke();
    ctx.beginPath();
    ctx.moveTo(0, 200);
    ctx.lineTo(600, 200);
    ctx.lineWidth = 5;
    ctx.stroke();
    ctx.beginPath();
    ctx.moveTo(0, 400);
    ctx.lineTo(600, 400);
    ctx.lineWidth = 5;
    ctx.stroke();
}

function restart() {
    startGame(grids[0]);
}

function updateBoard() {
    renderCells(grids[grids.length - 1]);
    renderLines();
}

// Event Listeners

canvas.addEventListener("mousedown", gridClickHandler);
function gridClickHandler(event) {
    updateGridAt(event.offsetX, event.offsetY);
    updateBoard();
}

restartButton.addEventListener("mousedown", restartClickHandler);
function restartClickHandler() {
    restart();
}

undoButton.addEventListener("mousedown", undoLastMove);
function undoLastMove() {
    rollBackHistory();
    updateBoard();
}

colorSelectButtons.forEach((button) => {
    button.addEventListener(
        "mousedown",
        () => (replacementColor = CELL_COLORS[button.name])
    );
});

// Helper Functions

// To convert canvas coordinates to grid coordinates
function convertCartesiansToGrid(xPos, yPos) {
    return {
        column: Math.floor(xPos / CELL_WIDTH),
        row: Math.floor(yPos / CELL_HEIGHT),
    };
}

// To compare two arrays
function arraysAreEqual(arr1, arr2) {
    if (arr1.length != arr2.length) {
        return false;
    } else {
        for (let i = 0; i < arr1.length; i++) {
            if (arr1[i] != arr2[i]) {
                return false;
            }
        }
        return true;
    }
}

//Start game
startGame();
```
</details>


### **3 Areas of Improvement:**
1. Comments aren't completely sufficient throughout the code. While there were comments, it would have been much more beneficial to explain each section of the code to further explain how it all works together.</br></br>
2. Loops located in rollBackHistory should be reformatted to a single if-esle loop, rather than two seperate if statements, this would be a much cleaner control flow.</br></br>
3. Indentation used to clean up some of the Functions/Arrays have irregular indentation. Many CONST elements and nested loops were not indented correctly, and correct indentation is absolutely essential when writing code.

</details>


---
---

## **Activity 0201:**
<details>
<summary>Click to expand answer</summary>

## **App Chosen:** *TikTok*
> The values inherent to TikTok helped me identify the target user base as those who are "Generation Z". Younger individuals have a high attachment to social media, and being able to post and share content with others has always been a great way to captivate a young audience. By entertaining, educating (in some ways), it earns people money, it informs, and it also serves as a distraction and is a way to pass time. All of those values make TikTok much more attractive.

</details>

---

## **Activity 0202:**
<details>
<summary>Click to expand answer</summary>

<details>
<summary>Example Code</summary>

```javascript
"use strict";

// Canvas references
const canvas = document.querySelector("canvas");
const ctx = canvas.getContext("2d");

// UI references
const restartButton = document.querySelector("#restart");
const undoButton = document.querySelector("#undo");
const colorSelectButtons = document.querySelectorAll(".color-select");

// Constants
const CELL_COLORS = {
    red: [255, 0, 0],
    blue: [0, 0, 255],
    white: [255, 255, 255],
};
const CELLS_PER_AXIS = 3;
const CELL_WIDTH = canvas.width / CELLS_PER_AXIS;
const CELL_HEIGHT = canvas.height / CELLS_PER_AXIS;

// Game objects
let replacementColor = CELL_COLORS.red;
let grids;

// Game Logic

function startGame(startingGrid = []) {
    if (startingGrid.length === 0) {
        startingGrid = initializeGrid();
    }
    initializeHistory(startingGrid);
    updateBoard();
    undoButton.disabled = true;
}

function initializeGrid() {
    const newGrid = [];
    for (let i = 0; i < CELLS_PER_AXIS * CELLS_PER_AXIS; i++) {
        newGrid.push(CELL_COLORS.white);
    }
    return newGrid;
}

function initializeHistory(startingGrid) {
    grids = [];
    grids.push(startingGrid);
}

function rollBackHistory() {
    if (grids.length > 0) {
        grids = grids.slice(0, grids.length - 1);
    }
    if (grids.length == 1) {
        undoButton.disabled = true;
    }
}

function renderCells(grid) {
    for (let i = 0; i < grid.length; i++) {
        ctx.fillStyle = `rgb(${grid[i][0]}, ${grid[i][1]}, ${grid[i][2]})`;
        ctx.fillRect(
            (i % CELLS_PER_AXIS) * CELL_WIDTH,
            Math.floor(i / CELLS_PER_AXIS) * CELL_HEIGHT,
            CELL_WIDTH,
            CELL_HEIGHT
        );
    }
}

function updateGridAt(mousePositionX, mousePositionY) {
    const gridCoordinates = convertCartesiansToGrid(
        mousePositionX,
        mousePositionY
    );
    const newGrid = grids[grids.length - 1].slice();
    squareFill(
        newGrid,
        gridCoordinates,
        newGrid[gridCoordinates.row * CELLS_PER_AXIS + gridCoordinates.column]
    );
    grids.push(newGrid);
    undoButton.disabled = false;
}

function squareFill(grid, gridCoordinate, colorToChange) {
    if (arraysAreEqual(colorToChange, replacementColor)) {
        return;
    } else {
        grid[
            gridCoordinate.row * CELLS_PER_AXIS + gridCoordinate.column
        ] = replacementColor;
    }
    return;
}

function renderLines() {
    ctx.beginPath();
    ctx.moveTo(200, 0);
    ctx.lineTo(200, 600);
    ctx.lineWidth = 5;
    ctx.stroke();
    ctx.beginPath();
    ctx.moveTo(400, 0);
    ctx.lineTo(400, 600);
    ctx.lineWidth = 5;
    ctx.stroke();
    ctx.beginPath();
    ctx.moveTo(0, 200);
    ctx.lineTo(600, 200);
    ctx.lineWidth = 5;
    ctx.stroke();
    ctx.beginPath();
    ctx.moveTo(0, 400);
    ctx.lineTo(600, 400);
    ctx.lineWidth = 5;
    ctx.stroke();
}

function restart() {
    startGame(grids[0]);
}

function updateBoard() {
    renderCells(grids[grids.length - 1]);
    renderLines();
}

// Event Listeners

canvas.addEventListener("mousedown", gridClickHandler);
function gridClickHandler(event) {
    updateGridAt(event.offsetX, event.offsetY);
    updateBoard();
}

restartButton.addEventListener("mousedown", restartClickHandler);
function restartClickHandler() {
    restart();
}

undoButton.addEventListener("mousedown", undoLastMove);
function undoLastMove() {
    rollBackHistory();
    updateBoard();
}

colorSelectButtons.forEach((button) => {
    button.addEventListener(
        "mousedown",
        () => (replacementColor = CELL_COLORS[button.name])
    );
});

// Helper Functions

// To convert canvas coordinates to grid coordinates
function convertCartesiansToGrid(xPos, yPos) {
    return {
        column: Math.floor(xPos / CELL_WIDTH),
        row: Math.floor(yPos / CELL_HEIGHT),
    };
}

// To compare two arrays
function arraysAreEqual(arr1, arr2) {
    if (arr1.length != arr2.length) {
        return false;
    } else {
        for (let i = 0; i < arr1.length; i++) {
            if (arr1[i] != arr2[i]) {
                return false;
            }
        }
        return true;
    }
}

//Start game
startGame();
```
</details>

> Some identifiers I would have changed would be the variable names used for the buttons. (restartButton, undoButton, colorSelectButtons). Rather than using camelCase for these, it would make more sense to me to start the variable name with "button_" followed by their specific use. This would make it easier to point to the button inside of a function by typing "button_" and seeing all the options I have created. camelCase is nice, but having the variable names saved as camelCase will not allow me to see if the value is a variable or a constant.

</details>

---
---

## **Activity 0301:**
<details>
<summary>Click to expand answer</summary>

## **App Chosen:** *Instagram*
### \**I do not have access to an android device, so I've opted to using the progressive web version vs. the iOS version.*\*

| Web Version  | iOS Version |
| --- | --- |
|![Web Version](https://github.com/n0180886/Process-Portfolio/blob/main/images/webApp.PNG?raw=true)|![iOS Version](https://github.com/n0180886/Process-Portfolio/blob/main/images/iOS.PNG?raw=true)|

## Differences:
- iOS utilizes space on the screen.
- webApp does not utilize dark mode through phone settings. I believe 
- webApp includes app name in header
- no need to have app downloaded and updates on webApp, latest updates will automatically be loaded when page loads.
- pages and content loaded much faster on native app.

</details>

---

## **Activity 0302:**
<details>
<summary>Click to expand answer</summary>

## **Developer Document chosen:** [Apple Developer Technologies](https://developer.apple.com/documentation/technologies)

> The section I decided to look at is the [Apple Pay on the Web](https://developer.apple.com/documentation/apple_pay_on_the_web) section. It was laid out very clearly, with lots of whitespace and it make each step of the process obvious to the reader. It provided insight into each aspect of implementing apple pay using a javascript-based API. Throughout the documentation, there are countless threads of information to thoroughly introduce you to different API's, concepts, and their functionality.

</details>

---
---

## **Activity 0401:**
<details>
<summary>Click to expand answer</summary>

## **Pattern Chosen:** [Bond Personal Security](https://pttrns.com/applications/763#8950)

> I believe this pattern is effective not only for its use of intelligence and also one-handed use. The most important functions on screen are in an easy to access part of the screen making it much easier for the user to manage and navigate.


</details>

---

## **Activity 0402:**
<details>
<summary>Click to expand answer</summary>

## **Pseudo Class Chosen:** *Split2*

### **Why?**

> because split1 relies on opening a file for reading, while split2 uses a given line. A main benefit of coding orthgonol is to produce code that promotes reuse. Using a given line vs. a file would be much easier to use in the future, and can be easilly reconfigurable and reengineered.

</details>

---
---

## **Activity 0501:**
<details>
<summary>Click to expand answer</summary>

**MVC:**
> Model, View, and Controller.
> - Model acts as a model for the data within the app.
> - View deals with what can be seen in the UI by a user.
> - Controller controls the interaction between the Model and the View. The view and the model have no direct connection to eachother, but they both connect to the controller.

**MVP:**
> Very similar to the MVC architecture, but the controller is replaced with the presenter. The presenter is responsible for changing the view, as the view very rarely calls on the presenter. 

**MVVM:**
> The MVVM (Model, View, View-Model) architecture is where data binding really holds strong. Data Binding is when UI components located in thje layout/view are binded to data sources within the model of the app. For example, if a slider present on the page is changed, not only would the model be updated, but if the data was displayed as a text on the view, that value would update as well.

</details>

---

## **Activity 0503:**
<details>
<summary>Click to expand answer</summary>

| Kata #1 | Kata #2 |
| --- | --- |
|![Kata #1](https://github.com/n0180886/Process-Portfolio/blob/main/images/Kata_1.JPG?raw=true)|![Kata #2](https://github.com/n0180886/Process-Portfolio/blob/main/images/Kata_1.JPG?raw=true)|

</details>

---
---

## **Activity 0801:**
<details>
<summary>Click to expand answer</summary>

> MVI is a uni-diurectional flow, example: View -> ViewModel -> Model -> View...

> MVI is Different than MVC as MVC has a high level of coupling between it's components, while MVI does not.

> All in all, each architechture has it's benefits. MVI would be best for scalability, MVC would be good for smaller projects as it requires less code, MVP would be much more reusable and easier to test, and MVVM is similar to MVP but without the coupling between the ViewModel and the View.

</details>

---

## **Activity 0802:**
<details>
<summary>Click to expand answer</summary>

## **App Chosen:** *Snapchat*
- The resources critical to the functionality of the Snapchat app in my opinion would be primarily disk space, while still requiring ample power, processing and sensor usage. 

- The sensors on the phone would be used to determine speed, height, temperature etc that are available to be shown on different 'filters' offered inside the app. 

- The app also keeps a local copy of all 'stories' and snapchats(when told) on the app, this can accumulate very fast meaning you would need ample storage.

</details>

---
---

## **Activity 0901:**
<details>
<summary>Click to expand answer</summary>

## **Apps Chosen:** *8Ball Pool* & *Domino's*
---
### **8Ball Pool:**
<p>
Use of notifications:
</p>

- Notifies user to use 'Loot Crate' system in the app, only after app is closed.
- Notifies user of friends active on game, again only after app is closed.
- Passage of time during loading screen shows the user a loading percentage, and a button that offers to play offline in the event that loading online data fails.

<p>
Offline Usage:
</p>

- Gives player two options: 1, play the game with a friend on the same device by passing the phone back and forth. 2, 

---

### **Domino's:**
<p>
Use of notifications:
</p>

- Passage of time is shown in the loading screen with a small loading icon, no show of percentage or time loading.
- Notifications are sent when new deals are presented, usually as a CTA to drive sales.
- Notifications are also sent when pizza order status has been updated.

<p>
Offline Usage:
</p>

- App is unable to be used offline.

</details>

---

## **Activity 0903:**
<details>
<summary>Click to expand answer</summary>

### **Which of the 4 steps have I used before?**
<p>I have used all of the steps before. Studying the data, hypothesizing, experimenting, and repeating those 3 steps.</p>

### **Is there one step that you feel you've done particularly well?**
> I believe I am strongest with experimenting. When something doesn't work as I intended, I tend to try multiple different things before I proceed. Finding different ways to achieve the same outcome is very rewarding, sometimes you can find much more efficient methods.

### **Is there one step that you feel you could improve on?**
> Hypothesizing. I have problems with this because I cannot visualize it in my mind on how it could work exactly, without writing the code down. Having the code in front of me and testing different methods is the only way I can bug-fix.

### **Might there be situations where this four step process won't work?**
> In the event there are no code errors, compiles correctly, but still doesn't work, I don't think this method would work as intended. When there is absolutely no clue where the error exists, you would not be able to hypothesize the answer, and you would not know where to start experimenting with the code.

</details>

---
---