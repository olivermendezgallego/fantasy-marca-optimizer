# Fantasy Marca Optimizer

Scrapes data from the Fantasy Marca web app and optimizes your team to maximize
profit, based on the previous day's price changes.

## What it does

- Extracts your squad, the transfer market, your balance, and per-player value
  history from fantasy.marca.com (unofficial endpoints, session-based auth).
- Computes the best combination of players to hold (from your current squad +
  the market) to maximize expected value gain, given your available budget and
  league rules (max 25 players, max 3 per real-life team).
- Compares two approaches: a fast greedy heuristic (ratio-based) and an exact
  solution using integer linear programming (PuLP/CBC).

## Example output

[Resultado del optimizador](examples/resultado.png)


## Setup

1. Clone the repo and install dependencies:
pip install -r requirements.txt

2. Get your session credentials from fantasy.marca.com (see "How authentication
   works" below) and set them as environment variables in a `.env` file:

MARCA_X_AUTH=...
MARCA_COOKIE=...
MARCA_COMMUNITY_ID=...

(If running from Google Colab, use Colab Secrets instead — see `notebooks/demo.ipynb`.)

## How authentication works

This project reuses your existing browser session with fantasy.marca.com — it
does not implement its own login. You need to extract your `X-Auth` token and
session cookie from your browser's DevTools (Network tab) after logging in
normally. *(opcional: enlaza aquí a una pequeña guía o explica los pasos brevemente)*

## Known limitations

- Uses undocumented endpoints that may change or break if Marca updates their
  frontend.
- `price_change` reflects the previous day's movement, not a real prediction of
  future value — it's used here as a simple proxy.
- The session token expires periodically and must be refreshed manually.
- This is a personal/educational project, not affiliated with MARCA.

## Roadmap

- [ ] Predictive model for price changes (instead of using yesterday's value)
- [ ] Matchday lineup optimizer (position minimums, opponent difficulty,
      starting probability)