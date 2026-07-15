\# PR Response Doc — CineLog Watchlist Feature



\## AI Usage

<!-- Fill in at the end — how you used AI tools during this project -->



\## Comment 1 — Rename

\*\*What I did:\*\* I changed the function name from save\_to\_watchlist() to add\_to\_watchlist() in the services/watchlist\_service.py file and updated any calls found in routes/watchlist/watchlist.py. 

\*\*How I verified:\*\* I did a project-wide search for any more instances of the old function name and then ran the `pytest tests/ -v` and all tests passed.



\## Comment 2 — Deduplication

\*\*What I did:\*\* Added deduplication logic to add\_to\_watchlist() function in services/watchlist\_service.py. Did so by adding a check to see if the film already existed in the watchlist and added a class AlreadyInWatchlistError(Exception) for handling the exception.

\*\*How I verified:\*\* I ran the `pytest tests/ -v` and all tests passed.



\## Comment 3 — Missing test

\*\*What I did:\*\*

\*\*How I verified:\*\*



\## Comment 4 — Default visibility

\*\*My position:\*\*

\*\*Reasoning:\*\*

\*\*Tradeoff acknowledged:\*\*



\## Comment 5 — Sort order

\*\*My position:\*\*

\*\*Reasoning:\*\*

\*\*Engagement with reviewer's point:\*\*



\## Comment 6 — Rebase

\*\*What conflicted:\*\*

\*\*How I resolved it:\*\*

\*\*How I verified no conflict remains:\*\*



\## PR Description

<!-- Written at the end — feature overview, design decisions, manual testing steps -->

