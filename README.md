# watch-party-python
Watch Party is a real-time web application that allows users to create or join virtual rooms and enjoy videos together. Users can communicate through chat, react to messages, share playlists, and participate in polls while watching videos.
A real-time watch-party starter project where users can create or join rooms and coordinate video playback while chatting, reacting, sharing a playlist, and voting in polls.

Important: This is a learning/starter project. The included app has not been independently load-tested against the stated targets of 10+ concurrent users, P95 event propagation under 250 ms, or playback drift under 500 ms. Run the test plan below and document your measured results before claiming those targets are met.

Features
Create a watch room or join one with a room code
Share a room by sending its URL
Synchronize play, pause, seek, and video loading through Socket.IO events
Display a movie/video catalogue with categories and search
In-room text chat and emoji reactions
Shared playlist
Poll creation and voting
Host transfer and basic host reassignment when the host disconnects
Health endpoint at /api/health
Tech stack
Backend: Python, Flask, Flask-SocketIO
Frontend: HTML, CSS, JavaScript
Real-time events: Socket.IO
Runtime: Local development server
The server is Python, but the browser interface still uses HTML, CSS, and JavaScript. This is a web app, so those frontend files are needed to render and control the page.

Project structure
watch-party-python/
├── app.py
├── requirements.txt
├── README.md
├── templates/
│   └── index.html
└── static/
    ├── app.js
    └── styles.css
Requirements
Python 3.11 or newer recommended
Visual Studio Code
A modern browser (Chrome, Edge, or Firefox)
Git, if you want to publish the project to GitHub
Run locally using VS Code (Windows, Command Prompt — no PowerShell)
1. Open the project
Download and extract the project ZIP.
Open VS Code.
Select File → Open Folder and choose the extracted watch-party-python folder.
In VS Code, choose Terminal → New Terminal.
If the terminal is PowerShell, use the terminal dropdown to select Command Prompt.
2. Check Python
Run:

python --version
If Python is not installed, install it from python.org and enable Add Python to PATH during installation.

3. Create and activate a virtual environment
Run these commands in the VS Code Command Prompt terminal:

python -m venv .venv
.venv\Scripts\activate.bat
If activation is blocked or fails, you can continue without activating the environment by using the alternative install/run commands below.

4. Install dependencies
With the virtual environment activated:

python -m pip install -r requirements.txt
If you skipped activation, use:

.venv\Scripts\python.exe -m pip install -r requirements.txt
5. Start the app
With the environment activated:

python app.py
If you skipped activation:

.venv\Scripts\python.exe app.py
Open http://127.0.0.1:5000 in your browser.

Keep the terminal running while you use the app. Press Ctrl+C in that terminal to stop the development server.

Try the app
Open the local URL in a browser.
Enter your display name and create a room.
Open another browser window or an incognito window and join the same room using its code.
Test playback controls, chat, reactions, playlist actions, polls, and host transfer.
For synchronized playback testing, use a video URL supported by the browser and accessible to every participant. Some sites block embedding; a URL being playable on the original website does not guarantee it can be embedded in this app.
Test on another device on the same Wi-Fi network
Find your computer's local IPv4 address in Windows network settings.
Start the server so it listens on the network interface. In app.py, configure the development server host as 0.0.0.0 if it is not already configured.
On the second device, open http://YOUR-COMPUTER-IP:5000.
Allow access through Windows Firewall only on a trusted private network if prompted.
Do not expose the Flask development server directly to the public internet. For public deployment, use a production-ready server and appropriate security configuration.

API endpoint
GET /api/health — basic server health check
GET /api/movies — returns the movie/video catalogue used by the app
GitHub upload using VS Code
Option A: VS Code interface
Create a new empty repository on GitHub. For example, name it watch-party-python.
In VS Code, open Source Control.
Select Initialize Repository if prompted.
Review the changed files and stage the files you want to upload.
Enter a commit message such as Initial Python Watch Party and commit.
Select Publish to GitHub and follow the prompts.
Do not commit .venv/, passwords, API keys, or other secrets. If you created a virtual environment, add .venv/ to .gitignore before publishing.

Option B: VS Code Command Prompt terminal
Create an empty repository on GitHub first, then run the following commands from the project folder. Replace YOUR-USERNAME with your GitHub username and use your actual repository URL.

git init
git add .
git commit -m "Initial Python Watch Party"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/watch-party-python.git
git push -u origin main
If Git asks you to identify yourself, configure your Git name and email. GitHub authentication may open a browser or ask you to use Git Credential Manager.

Performance and reliability test plan
Do not claim performance targets are met until you have recorded measurements. Test and document at least:

Concurrency: 10 or more browser clients in the same room
Event propagation: measure time from host action to client receipt; report P50, P95, and maximum
Playback drift: compare the current playback time across clients after play, pause, and seek; report maximum observed difference
Late join: join while a video is already playing and check whether the new participant reaches the expected state
Reconnect: disconnect and reconnect a client; check whether it rejoins the room and receives current state
Host disconnect: disconnect the host and verify the expected new host
Rapid controls: issue multiple seeks and play/pause events quickly and check for stale state
Invalid input: try malformed room codes, empty messages, and unsupported video URLs
Suggested results table for your report:

Test	Target / expected behavior	Actual result
Concurrent clients	10+ clients in one room	Not measured yet
Event propagation P95	≤ 250 ms on LAN	Not measured yet
Playback drift	≤ 500 ms	Not measured yet
Late join	Client receives current room state	Verify
Reconnection	Client rejoins and resynchronizes	Verify
Host disconnect	Host is reassigned when possible	Verify
Current limitations
Room and playlist state are stored in server memory and are lost when the server restarts.
This starter is not configured for multi-process or multi-server deployment.
Reconnection and late-join behavior should be tested and improved before a production/demo claim.
Video playback depends on the media URL, browser support, CORS/embedding rules, and network conditions.
There is no production authentication, database persistence, rate limiting, or hardened deployment configuration.
The Flask development server is intended for local development, not public production traffic.
Troubleshooting
python is not recognized
Reinstall Python from python.org with Add Python to PATH enabled, then restart VS Code.

No module named flask or another dependency error
Make sure the VS Code terminal is in the project directory and run:

python -m pip install -r requirements.txt
The page does not open
Confirm that python app.py is still running and that the terminal shows the local address. Open http://127.0.0.1:5000.

Another process is using port 5000
Stop the other local app using that port or change the port setting in app.py, then open the matching URL.

Video does not load
Try a direct media URL that the browser can play and that permits embedding. Some streaming services prevent their videos from being embedded in third-party pages.

License
No license has been added. If you plan to publish or accept contributions, choose and add a license file that matches how you want others to use the project.
