# PR Response Doc — CineLog Watchlist Feature



## AI Usage

<!-- Fill in at the end — how you used AI tools during this project -->



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

**What conflicted:**

**How I resolved it:**

**How I verified no conflict remains:**



## PR Description

<!-- Written at the end — feature overview, design decisions, manual testing steps -->

