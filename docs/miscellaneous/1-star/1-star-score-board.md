# Score Board

## Why this challenge?
This challenge show we how to access the hidden path of the website although we haven't login yet.

## What i did?
### Step 1
- Using Developer Tool (F12) to see the source code of the website.
![Access Developer Tool](../../assets/miscellaneous/1-star/score-board/access-devtool.png)

### Step 2
- Go to the **Sources** tab, then find the file named "main.js".
![Find main.js file](../../assets/miscellaneous/1-star/score-board/source-tab.png)

### Step 3
- Analyze the code carefully, you see many path of the website.
![Analyze main.js file](../../assets/miscellaneous/1-star/score-board/website-path.png)

### Step 4
- Find the hidden path `/score-board`.
![Find hidden path](../../assets/miscellaneous/1-star/score-board/scoreboard-path.png)
### Step 5 
- Access it directly via URL: `http://IP:PORT/score-board`
![Access score-board](../../assets/miscellaneous/1-star/score-board/access-scoreboard-path.png)

## Completed challenge!
![Completed challenge](../../assets/miscellaneous/1-star/score-board/scoreboard-solved.png)

## What i learned?
- The hidden path is stored in the JavaScript files. So, analyzing the JavaScript files is very important in order to find hidden paths or vulnerabilities.
- Access control is very important to secure the web application; deny users who haven't logged in yet access to sensitive pages.

## How to prevent it?
- Implement proper access control mechanisms to restrict access to sensitive pages only to authenticated users.
- Minify and obfuscate JavaScript files to make it harder for attackers to analyze the code (UglifyJS, Terser).
