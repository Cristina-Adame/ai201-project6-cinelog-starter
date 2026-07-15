# PR Response Doc — CineLog Watchlist Feature



## AI Usage

<!-- Fill in at the end — how you used AI tools during this project -->
Asked Claude to pull up and explain the PR review comments in order to understand fully what each one was asking. Claude helped me understand what each changed wanted and I verified by reading the code and seeing the reasoning for the changes proposed. For Comments 4 and 5, I made my own arguments first anf then asked Claude to see if my tradeoffs made sense. Claude helped me understand the issues going on with the rebase and I made the changes and tested them with the appropriate file.


## Comment 1 — Rename

**What I did:** I changed the function name from save\_to\_watchlist() to add\_to\_watchlist() in the services/watchlist\_service.py file and updated any calls found in routes/watchlist/watchlist.py. 

**How I verified:** I did a project-wide search for any more instances of the old function name and then ran `pytest tests/ -v` and all tests passed.



## Comment 2 — Deduplication

**What I did:** Added deduplication logic to add\_to\_watchlist() function in services/watchlist\_service.py. Did so by adding a check to see if the film already existed in the watchlist and added a class AlreadyInWatchlistError(Exception) for handling the exception.

**How I verified:** I ran `pytest tests/ -v` and all tests passed.



## Comment 3 — Missing test

**What I did:** Created a new file tests/test\_watchlist.py. Used test\_add\_to\_collection\_nonexistent\_film\_raises() from tests/test\_collection.py to wrote an equivalently structured function. Adjusted the imports, copied the pytest fixtures and added the nonexistent film handling function.

**How I verified:** I ran `pytest tests/test\_watchlist.py -v` along with `pytest tests/ -v` and all tests passed.



## Comment 4 — Default visibility

**My position:** Agree that public=True should be the default.

**Reasoning:** CineLog is a community film tracking app, as such it can be reasoned that these watchlists should default to being public and then later the user may toggle the option to make it private. A watchlist is not sensitive information that puts a user at risk and will not offend users.

**Tradeoff acknowledged:** The tradeoff would be that some users may have films that contain sensitive subjects and having that be instantly public may be problematic for them. Users also may not be aware that the default is public which may them lead them to add movies with interests they would rather keep private.



## Comment 5 — Sort order

**My position:** Order by Date

**Reasoning:** A watchlist, containing films a user would like to one day watch, can be useful in more than just its' content. If the list were sorted by date added, the user may be able to more easily choose which film to watch next. Also, get\_collection() already sorts by date added, choosing by date will keep consistency.

**Engagement with reviewer's point:** I agree. Dates associated with movies may also help a user recall which movie they wanted to choose (e.g. "what was that movie I wanted to watch two months ago? I recall I added it to my watchlist"). Alphabetical order is not exactly a useful feature in the use of a watchlist.



## Comment 6 — Rebase

**What conflicted:** The .gitignore file had an add/add conflict since main added one during the refactor and models.py didn't have the WatchlistEntry after the refactor.

**How I resolved it:** Merged the .gitignore conflict by keeping what both versions had in it. Added the WatchlistEntry back to models.py.

**How I verified no conflict remains:** Ran `pytest tests/ -v` — all tests passed.

**Screenshot of Commits:**
<img width="1237" height="352" alt="image" src="https://github.com/user-attachments/assets/8ad0f0de-cbf1-4a60-baea-167f6d0c7f3d" />


## PR Description

<!-- Written at the end — feature overview, design decisions, manual testing steps -->
## What it does
Adds watchlist feature to CineLog so users may save films they want to see

## Design decisions
**Default visibility (public=True):** Watchlists default to public because CineLog is a community film tracking app, as such it can be reasoned that these watchlists should default to being public and then later the user may toggle the option to make it private.

**Sort order (date added):** Watchlists are sorted by date added descending. Dates associated with movies may also help a user recall which movie they wanted to choose (e.g. "what was that movie I wanted to watch two months ago? I recall I added it to my watchlist").

## How to manually test
1. Start the app: `python app.py`
2. Add a film to a watchlist:
   `curl -X POST http://127.0.0.1:5000/watchlist/<user_id>/add -H "Content-Type: application/json" -d '{"film_id": "<film_uuid>"}'`
3. View the watchlist:
   `curl http://127.0.0.1:5000/watchlist/<user_id>`
4. Verify duplicate prevention by adding the same film twice — should return an error.
5. Run the test suite: `pytest tests/ -v`
