# WX Huddle — Halloween Edition

A hybrid huddle for approximately 14 colleagues, supporting 2–16 players. Participants enter a name and choose one of 30 original monster avatars. No player account is required. The host has a normal player seat.

## The game

The programme allows about 60 minutes. From the welcome onward, each player sees three question choices only when their turn begins. Everyone sees the current player’s avatar, name and chosen question. Shuffle to next player saves their complete answer and selects someone who has not had a turn in that round. The timer advances if needed, and the final player moves the group to the next round.

1. **Share your perspective:** choose one of three questions and tell a work story.
2. **What would you do?:** choose one question and share how you would handle it.
3. **Wild ideas:** choose one question and give your most ridiculous idea.

Each player answers once per round. There are no extra rules, follow-up questions or second discussion set. All three options are reserved for one player, so another player cannot receive the same question. The current programme uses 192 distinct choices: sixteen players, three options each, across the welcome and three rounds. Picks save with the room and can change until the answer is submitted. No question is chosen automatically. Future questions stay absent from other players’ views and private hands until the relevant turn.

The live cloud keeps each player's latest written answer in one complete tile. Identical answers and clear short synonyms or typos group together, with the most shared answers highlighted. Longer or unfamiliar phrases stay whole. Tap a tile to see all original answers and names. There is no response-history section. Grouping uses a conservative local vocabulary, without an external AI service.

Players use one Shuffle to next player button with an optional answer box, without selecting or displaying a response type. An answer without text records participation and earns the same contribution credits. Spoken contributions take place in the shared room or existing video call; the game does not record, transcribe or carry voice audio.

One complete answer earns 30 contribution credits per round. A closing reflection earns 10, giving 100 base credits, plus peer recognition. Unselected questions, unshared takeaways and recognition votes remain private.

[Read the current question choices](QUESTION_BANK.md), plus sixteen closing reflections.

## Deploy on Streamlit Community Cloud

1. Create an app from this repository and the `main` branch.
2. Set the main file path to `WX_Huddle_Halloween.py`.
3. Use Python 3.12 or 3.13 and deploy.
4. Enable public app sharing so participants do not need Streamlit accounts.
5. Open `https://wx-huddle.streamlit.app/?host=1`, create a room, and share its room QR or joining link.
6. Participants use the normal site or room QR link. The host can start after one other person joins.

The public hosting origin is used for invitation links. An optional Streamlit secret `PUBLIC_APP_URL` can specify the final HTTPS address.

## Host permissions

Only the room’s actual owner in host entry can start, pause, resume, skip, restart, end, reorder players or correct credits. Opening a host URL does not give a guest those permissions. Both the server and the interface enforce the restrictions. The current player can save their own answer and shuffle to the next unplayed seat; other players cannot advance that turn. Repeated requests cannot create duplicate answers or skip extra turns. Host and participant browser sessions are saved separately, so a participant link does not reopen a cached host seat.

Creating a room opens My cards: the host is already a player. The room code, direct joining link and QR appear above the player list. The host can switch between My cards and Host controls. Clear records & restart removes responses, credits, votes, readiness and the word cloud while retaining joined names, avatars and private recovery credentials.

## Mobile joining and effects

A scanned room QR opens joining with its code entered. After joining, hosts and participants both see the room code, direct joining link and QR. During play, Invite players opens them again. The form appears first on phones, with ten avatar choices and a See all 30 characters control. The page grows and shrinks with its content; dialogs use the visible browser viewport.

A ghost animation reveals the selected player. Soft synthesized music accompanies the draw, with short tones for the final answer countdown. Sound is controlled by the speaker button and begins through a user gesture. Reduced-motion settings are respected.

## Run locally

```bash
python -m pip install -r requirements.txt
streamlit run WX_Huddle_Halloween.py
```

The Python file contains the frontend, avatars, server game engine and shared room service. Streamlit does not need separate asset folders or a Node build.

## Session storage

Rooms expire after 24 hours. SQLite shares state across browser sessions in one running app instance. Streamlit Community Cloud local storage is ephemeral; restarting or redeploying the app can reset rooms. Infrastructure with durable storage can set `WX_DATA_DIR` to that location.

Private session and recovery keys are hashed on the server. A successful recovery rotates the key and invalidates the previous device’s credential.

Every joined player’s lobby shows its room code, joining link and QR above the player list on laptops and phones. The main participant link opens the join form; saved seats remain available through Resume. Remove clears one saved seat, and Clear saved seats clears the list for that browser role after confirmation. These controls forget local access shortcuts without deleting rooms, answers or other players. Keep a private recovery key if you need to return later.

Soft minor-key background music begins after creating, joining or starting a room, unless muted. The visible Music toggle also enables it manually after a reload. Each player controls music on their own device; a saved mute choice is respected. Music becomes quieter during answers and stops when the game is paused or finished. Browser audio still requires a user gesture.

## Validation

The source passed 91 JavaScript checks and twelve Python service integration checks. Coverage includes three unique private options at 2, 14 and 16 seats, exactly one answer per player per round, hidden future questions, shared current-player avatars and prompts, participant shuffle without repeats, atomic concurrent retries, complete automatic progression, choice persistence and locking, whole-answer grouping, credits, host permissions, all thirty avatars, host creation into player view, participant QR, mobile entry, concurrent joins and credential recovery. Legacy-flow checks preserve existing games.

The Python service tests exercise the production transaction layer against the exact bundled engine in Node. The generated Streamlit file is also checked against a fresh deterministic build. Browser verification checks the deployed Streamlit component separately.

Existing active rooms keep the programme and question bank they started with. New rooms and rooms restarted by their host use the turn-time question selection and participant shuffle programme. The duplicate response-history section is removed for every room.
