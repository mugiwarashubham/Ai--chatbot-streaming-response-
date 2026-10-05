🎮 SassBot Arena

A chatbot that roasts you. Politely. Mostly.

SassBot Arena is a small web app where you chat with a sarcastic AI inside a retro-gaming interface. Replies appear live as the AI writes them, you earn XP for every message, and you level up the more you talk. It runs on Google's free Gemini API, so you don't need a credit card to try it.

I built it to learn how streaming AI responses work, from the model all the way to the browser.

What you get
Live replies. Words show up as they're generated instead of after a long wait.
A gaming-style UI. Neon colors, pixel fonts, scanlines, an XP bar and "LEVEL UP!" pop-ups.
A stop button. The AI rambling on? Cancel it mid-sentence.
Memory. The bot remembers what you said earlier in the chat.
Phone friendly. The layout adapts to small screens.
What you need
Node.js version 20.6 or newer
A free Gemini API key. Get one in a minute at aistudio.google.com/apikey (no credit card)
Getting it running

1. Install the packages

bash
npm install

2. Add your API key

Make a copy of the example settings file:

bash
# Mac / Linux
cp .env.example .env

# Windows PowerShell
copy .env.example .env

Open the new .env file and paste in your key:

GEMINI_API_KEY=your_gemini_key_here
MODEL=gemini-3.8-flash
PORT=3000

Keep your key private. .env is already in .gitignore, so Git will skip it.

3. Start it

bash
npm start

Now open http://localhost:3000 and say hello. Expect sarcasm.

How it works (the short version)
You type a message and the browser sends it to the server.
The server asks Gemini for a reply and asks it to send the answer in small pieces.
Each piece is passed straight to your browser the moment it arrives.
The page types the pieces into the chat, so you see the reply being written.
What's in the folder
public/index.html     The whole frontend (looks + browser code)
server.js             Web server, serves the page and streams replies
ChatService.js        Talks to Gemini and hands back text piece by piece
ChatController.js     Passes messages to the service
index.js              Connects the controller and service
.env.example          Template for your settings
Settings
Setting	What it does	Default
GEMINI_API_KEY	Your Gemini API key (required)	none
MODEL	Which Gemini model to use	gemini-3.8-flash
PORT	Which port the app runs on	3000
When something goes wrong

"node: .env: not found" The settings file is missing or misnamed. It has to be called exactly .env (not .env.txt) and live in the project folder. Check with dir -Force on Windows or ls -a on Mac/Linux.

A 404 error mentioning the model Google renames and retires models from time to time. Set MODEL in .env to a current Gemini flash model and restart.

A 429 error You've hit the free-tier limit. Take a short break and try again in a minute.

The reply shows up all at once Check your terminal. The server prints a line for each chunk Gemini sends. If you only see one or two big chunks, the model itself is sending its answer in a burst. A lighter "flash-lite" model usually streams more smoothly.

The page looks old after an update Hard refresh with Ctrl + Shift + R.

"Port already in use" Another app is using port 3000. Close it, or change PORT in .env.

Good to know
The free Gemini tier may use your messages to improve Google's products, so don't share anything private.
Chat memory lives in the server's memory, so restarting the server resets the conversation.
Built with

Node.js, Express, the OpenAI JavaScript SDK (pointed at Gemini's compatible endpoint), and plain HTML, CSS and JavaScript. No build step, no frameworks.

License

MIT. Do whatever you like with it.
