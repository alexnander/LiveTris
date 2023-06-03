# Database for LiveTris

## Users Table
Users Table meta info:

`(integer primary key)gamer_id, (string)email, (string)password_hash, (string)gamer_tag`

---

`gamer_id` - unique primary key of player

`email` - needed for login

`password_hash` - password verification hash

`gamer_tag` - name that shows up on leader boards etc. 

## Games Table

Games Table meta info:

`(integer primary key)game_id, (integer foreign key)gamer_id, (datetime)time_start, (bool)live, (bool)save, (bool)archived, (integer)final_score`

---

`game_id` - unique primary key of game session

`gamer_id` - foreign key of gamer of the session

`time_start` - time game began

`live` - game is live (need routines for cleaning/removing stale games)

`save` - game will be saved

`archived` - game is saved to archive

`final_score` - score after game completed


## Recordings Table

Recordings Table meta info:

`(integer foreign key)game_id, (datetime)time, (integer)sequence, (integer)score, (string[10 char])event_type, (byteint)parameter,`

---

`game_id` - unique primary key of specific game session recording

`time` - time event was logged

`sequence` - integer incremented for each event recorded ensuring completeness of recording

`score` - score of game at specific event

`event_type` - type of event being recorded.

`parameter` - extra info needed to describe event. 

note:
`game_id`, `time`, `sequence` and `score` are recorded for each event entry

### One-Time Event Types:

| Event        | Parameter    | Note                                |
|--------------|--------------|-------------------------------------|
| `GAME_START` | no parameter | signifies that the game has started |
| `GAME_OVER`  | no parameter | signifies the game has ended        |

### Movement Event Type:

| Event  | Parameter                                                                   | Note                  |
|--------|-----------------------------------------------------------------------------|-----------------------|
| `MOVE` | (integer code for move type i.e. "left", "right", "down", "drop", "rotate") | records player inputs |
 
### Engine Event:

| Event        | Parameter                     | Note                                                |
|--------------|-------------------------------|-----------------------------------------------------|
| `NEXT_PIECE` | (integer code for piece type) | records which piece game engine chose as next piece |
