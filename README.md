# WX Huddle — Halloween Edition

A hybrid huddle for approximately 14 colleagues, supporting 2–16 players. Participants enter a name and choose one of 30 original monster avatars. No player account is required. The host has a normal player seat.

## The game

The programme lasts about 60 minutes. The welcome can finish earlier when everyone is ready. The app chooses players, runs answer timers and moves between rounds automatically.

1. **Share your perspective:** sixteen different cards about strengths, habits, interests and working preferences. Share an example, consider a related situation, and answer a colleague’s follow-up.
2. **What would you do?:** two familiar situations about an urgent request and raising a concern. Choose a first response, ask a colleague your unique question, then share your response and what you would actually say. Named results show different choices and changes of view. Choices are not graded.
3. **Bad idea, better idea:** sixteen different situations about communication, teamwork and useful working habits. Give a deliberately bad suggestion, replace it with a useful change, and answer a colleague’s question.

The welcome, response board and word cloud show participant names and avatars. Public typed responses and optional summaries of spoken answers feed the cloud. Spoken contributions take place in the shared room or existing video call; the game does not record, transcribe or carry voice audio.

During the discussion, a participant can finish a typed reply while later question turns run, until the final response window closes. First choices and final response text stay private until the reveal. Private cards, unshared takeaways and recognition votes remain private.

[Read the complete reviewed question bank](QUESTION_BANK.md). It includes the purpose of every question and improvement card, all 32 unique discussion questions, and the closing questions. The previous missing-treats and playlist puzzles are removed.

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

## Validation

The source passed 48 JavaScript checks and eight Python service integration checks. Coverage includes full-game credit totals, unique cards for sixteen players, role restrictions, private choices and public reveals, typed and spoken responses, replies across question turns, reset, concurrent joins, recovery and SQLite persistence.

The Python service uses the same bundled engine in Node during these checks because the optional Python V8 wheel is unavailable in the build environment. End-to-end testing in a live Streamlit browser remains to be completed after publication.
