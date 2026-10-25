# WX Huddle — Halloween Edition

A 60-minute hybrid huddle for individual players, designed for approximately 14 colleagues. Participants choose one of 30 original cute-scary monster avatars and join using a name and room code. The owner also has a player seat.

The rounds are Answer, then change it, Solve the mystery, and Bad idea, better idea. Everyone receives private virtual cards, takes individual turns, and can speak in the shared call or type a response. The owner can share a QR joining link, pause the timer, manage the lobby, and export results.

## Deploy on Streamlit Community Cloud

1. Create an app from this repository and the `main` branch.
2. Set the main file path to `WX_Huddle_Halloween.py`.
3. Use Python 3.12 or 3.13 and select Deploy.
4. Enable public app sharing so participants do not need Streamlit accounts.
5. Open `https://wx-huddle.streamlit.app/?host=1`, choose your name and avatar, create a room, and share its room QR code or joining link.
6. Participants use the normal site or the room QR link. They see Join only. The host can start after one participant joins.
7. The host-only Clear records & restart control clears answers, credits, votes and notes while keeping the joined players connected.

The app automatically uses the public hosting origin for joining links. If needed, set the optional Streamlit secret `PUBLIC_APP_URL` to the final HTTPS app address.

## Run locally

```bash
python -m pip install -r requirements.txt
streamlit run WX_Huddle_Halloween.py
```

The Python file contains the interface, avatars, private game engine, and shared room service. No separate asset folder, Node installation, or build step is required on Streamlit.

## Session storage

Rooms are shared across browser sessions in one running Streamlit app instance and expire after 24 hours. State is stored in SQLite in the app's temporary directory. Streamlit Community Cloud local storage is ephemeral: a hosting restart or redeployment can reset active rooms. Keep the app running during the huddle. Hosts deploying on infrastructure with durable storage may set `WX_DATA_DIR` to that storage directory.

Private session and recovery keys are stored as hashes on the server. Each browser receives its own permitted card view. Recognition votes and unshared takeaways stay private.

## Validation

The source game passed 44 engine, invitation, participant-entry, participation and component-sizing checks and seven Python service integration checks, including 14 concurrent joins, access control, recovery, and SQLite persistence. The Python service was tested using the same bundled engine in Node because the optional Python V8 wheel was unavailable in the build environment. End-to-end Streamlit browser testing remains to be completed after deployment.

Each room deals different questions, twists, clues and reflections to up to 16 players. The decks are shuffled again after restarting. The participant entry rejects room creation and every administrative game action. Host entry is selected with `?host=1`; controlling an existing room also requires that room’s actual owner session key. A host URL alone does not grant a participant control of that room. Host and participant browser sessions are stored separately, so a scanned participant link does not reopen a cached host seat. Existing saved seats are migrated by role. There are no player accounts or passwords.

## Automatic hosting and sound

After the host taps Start, the app shuffles the roster, deals unique cards, randomises each round’s turns, runs the answer timers, and moves between rounds automatically. The host has a normal player seat. Pause, reset, and manual step controls remain available when needed.

A ghost animation reveals the selected player. Soft synthesized music accompanies the draw; short tones mark the final answer countdown. Audio starts through the host’s Start/Shuffle tap or the speaker button, as browsers require a user gesture. Other players can enable or mute sound using the speaker button. Reduced-motion settings are respected.

During question turns, the selected questioner can use their card or enter a different question. The selected player can answer aloud or type on their own device.

## Mobile joining

A scanned room QR opens Join with the room code already entered. Participant entry and waiting rooms do not display invitation QR codes. Host invitations remain available through Invite players; on phones the lobby invitation panel starts collapsed.

The phone entry form appears first, with ten character choices and a See all 30 characters control. The layout uses one column, readable inputs, wrapping controls, and safe-area spacing. Streamlit iframe sizing follows the current content so it can grow or shrink after character expansion or joining. Dialogs use the visible browser viewport.

## Participant interaction and word cloud

The welcome has an answer field, separate typed and spoken-answer buttons, a named response board and a live word cloud. Each participant taps Ready after contributing. The app moves on when everyone is ready, or when the five-minute welcome timer ends. Completing the welcome early can shorten the overall game.

During challenge turns, selected players have explicit Share typed answer and I answered aloud controls. Other participants can post a question or thought without taking over the speaker’s turn. Spoken answers are given in the shared room or existing video call; the game records the participant’s confirmation and optional typed summary. It does not record, transcribe or carry voice audio.

Publicly shared answers, questions and comments feed the word cloud. A word’s size reflects how many responses mention it; the response cards show each author’s name and avatar. Spoken confirmations without a typed summary do not create invented words. Private cards, unshared takeaways and voting choices are excluded. The board is visible on player, host and shared screens. Clearing records also clears the cloud, responses and readiness.

Only the actual host using host entry can start, pause, resume, skip, restart, end, reorder players or correct credits. These restrictions are enforced server-side as well as in the interface, and are tested with forged role fields and participant routes carrying cached owner credentials.

## Clearer question cards

Round one has sixteen distinct questions about everyday choices, useful skills, recommendations and small experiences. Each has a relevant new condition and a different colleague’s follow-up. The instruction screen shows a complete example instead of referring to an unexplained brief.

Round three has sixteen distinct situations. Its bad-suggestion and useful-change steps display their own instruction, one at a time. The welcome asks which small daily annoyance participants would remove. The mystery text consistently refers to treat boxes and playlist names.
