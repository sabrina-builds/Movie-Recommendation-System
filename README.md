# CineSearch: Movie Recommendation System & Product Design

Data-driven product case study: building and testing a movie recommendation engine on MovieLens data, then designing a Figma app around it so people spend less time deciding what to watch.

**[View the interactive prototype →](https://www.figma.com/proto/IMu0c0kO9QS72pHSpojwTs/CineSearch?node-id=1-2&t=DvnzeUAWBS148fxB-1&scaling=scale-down&content-scaling=fixed&page-id=0%3A1)**

## Overview

I watch movies and shows across several streaming services and log them on Letterboxd, but I still spend 30-60 minutes deciding what to watch. CineSearch is a button-based app concept that fixes that: for each movie card, the user taps **Seen** (then rates it) or **Not seen yet** (straight to the next movie), and every choice feeds back into future recommendations.

Users can also search for movies by title or describe what they want in plain language (for example, "comedy, no romance"). Any movie found through search or the prompt can be added to a want to watch list.

**Key finding:** In an offline A/B test on 1.1M MovieLens ratings, collaborative filtering had a 5.9% top-10 hit rate vs. 0.4% for genre-based recommendations (n = 4,998 users, p < 0.001). That is about 15x better, and roughly 55x better than random guessing (about 0.1%). So the app recommends based on what similar users liked, not just matching genres.

## What's in this repo

- `CineSearch.ipynb` — full analysis: data filtering, the two recommendation models, search and prompt functions, A/B test, and conclusion
- Figma mock-up (linked above) — the app screens and flow
- The MovieLens data is not included because the files are too large for GitHub (see "Run it yourself")

## Tools

Python (pandas, NumPy, SciPy, scikit-learn), Figma

## Process

1. Filtered MovieLens to 9,322 movies with 200+ ratings and a random sample of 5,000 users with 50+ ratings (1.1M ratings)
2. Counted a rating of 4+ as "liked"
3. Hid each user's most recent liked movie, so the models never see the answer
4. Built two recommenders: genre-based (genre similarity) and collaborative filtering (similar users' likes)
5. Compared hit rates with a chi-square test
6. Built the search bar, prompt filter, and want to watch list into the engine, and designed the app flow in Figma

## Results

| Approach | Top-10 hit rate |
|---|---|
| Genre-based | 0.4% |
| Collaborative filtering | 5.9% |

n = 4,998 users, p < 0.001.

## Limitations

- The data has no "Not seen yet" clicks, so the test only uses seen-and-liked movies.
- The prompt is a simple keyword parser that understands five genres, not a language model.
- The test is offline (past ratings), not with real users.

## Next steps

- Run a live A/B test in the app
- Track how often recommendations are added to the want to watch list
- Replace the keyword parser with a language model

## Run it yourself

1. Download the MovieLens ratings dataset from [grouplens.org/datasets/movielens](https://grouplens.org/datasets/movielens/) and put `movies.csv` and `ratings.csv` in a `data/` folder.
2. Install the packages: `pip install pandas numpy scipy scikit-learn jupyter`
3. Open `CineSearch.ipynb` and run all cells.
