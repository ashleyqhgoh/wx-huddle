# WX Huddle — Halloween Edition

A hybrid huddle for approximately 14 colleagues, supporting 2–16 players. Participants enter a name and choose one of 30 original monster avatars. No player account is required. The host has a normal player seat.

## The game

The programme lasts about 60 minutes. Every player chooses from three different welcome questions. The welcome can finish earlier when everyone is ready. The app chooses players, runs answer timers and moves between rounds automatically.

1. **Share your perspective:** choose one of three questions about team experiences, strengths, support and working together. Tell a short story, then respond to a related situation and a colleague’s follow-up.
2. **What would you do?:** two discussion sets. In each set, choose one of three questions about team connection or everyday collaboration to answer. The selected question appears on the card of the colleague assigned to ask it. Everyone asks once and receives one question. Each reply becomes that player’s complete answer, shown with their question at the reveal.
3. **Bad idea, better idea:** choose one of three situations, give a deliberately terrible suggestion, then turn it into something you would actually try.

All three options are reserved for one player: no other player receives those questions. The 240 primary questions cover sixteen players, three options each, across the welcome, round one, both discussion sets and round three. Picks save with the room and survive reconnects. They lock when the answer turn starts, or after the welcome answer is shared. The first option is selected by default so automatic play can continue.

The live cloud keeps each player's latest written answer in one complete tile. Identical answers and clear short synonyms or typos group together, with the most shared answers highlighted. Longer or unfamiliar phrases stay whole. Tap a tile to see all original answers and names. There is no response-history section. Grouping uses a conservative local vocabulary, without an external AI service.

Players use one submission button with an optional answer box, without selecting or displaying a response type. An answer without text records participation and earns the same contribution credits. Spoken contributions take place in the shared room or existing video call; the game does not record, transcribe or carry voice audio.

During the discussion, a participant can finish a typed reply while later question turns run, until the final response window closes. Private preparation notes stay private. Replies to a colleague are shared when submitted; a final answer saved separately is shared at the reveal. Private cards, unshared takeaways and recognition votes remain private.

[Read all 240 question choices](QUESTION_BANK.md), plus their related situations, follow-ups and sixteen closing reflections.

## Deploy on Streamlit Community Cloud

1. Create an app from this repository and the `main` branch.
2. Set the main file path to `WX_Huddle_Halloween.py`.
3. Use Python 3.12 or 3.13 and deploy.
4. Enable public app sharing so participants do not need Streamlit accounts.
5. Open `https://wx-huddle.streamlit.app/?host=1`, create a room, and share its room QR or joining link.
6. Participants use the normal site or room QR link. The host can start after one other person joins.

The public hosting origin is used for invitation links. An optional Streamlit secret `PUBLIC_APP_URL` can specify the final HTTPS address.

## Host permissions

Only the room’s actual owner in host entry can start, pause, resume, skip, restart, end, reorder players or correct credits. Opening a host URL does not give a guest those permissions. Both the server and the interface enforce the restrictions. Host and participant browser sessions are saved separately, so a participant link does not reopen a cached host seat.

The host can switch between My cards and Host controls. Clear records & restart removes responses, credits, votes, readiness and the word cloud while retaining joined names, avatars and private recovery credentials.

## Mobile joining and effects

A scanned room QR opens joining with its code entered. Participant entry and waiting rooms do not show invitation QR panels. The form appears first on phones, with ten avatar choices and a See all 30 characters control. The page grows and shrinks with its content; dialogs use the visible browser viewport.

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

The host lobby shows its room code, joining link and QR above the player list on laptops and phones. The main participant link opens the join form; saved seats remain available through Resume. Remove clears one saved seat, and Clear saved seats clears the list for that browser role after confirmation. These controls forget local access shortcuts without deleting rooms, answers or other players. Keep a private recovery key if you need to return later.

Soft minor-key background music begins after the host creates or starts a room, unless muted. The visible Music toggle also enables it manually after a reload. Players opt in on their own devices. Music becomes quieter during answers and stops when the game is paused or finished. Browser audio still requires a user gesture.

## Validation

The source passed 75 JavaScript checks and ten Python service integration checks. Coverage includes all 240 distinct options, three private choices per player at 2, 14 and 16 seats, selection persistence, turn locking, round-two handoff to the assigned asker, keyword grouping and counts, complete named answer details, full-game credits and timers, host permissions, all thirty avatars, mobile entry, concurrent joins and credential recovery.

The Python service tests exercise the production transaction layer against the exact bundled engine in Node. The generated Streamlit file is also checked against a fresh deterministic build. Browser verification checks the deployed Streamlit component separately.

Existing rooms keep the question bank they started with. New rooms and rooms restarted by their host use the team-bonding question bank. The duplicate response-history section is removed for every room.
