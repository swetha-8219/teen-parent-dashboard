# Teen Parent Dashboard

A weekly dashboard for parents of teenagers — and for teenagers themselves — built from Reddit discussions.

**Parents section:** what teenagers are going through this week, and the solutions other parents and teens offered.
**Teens section:** what their peers are going through, and how they can help themselves.

## Status: live data — weekly snapshot

This version runs on **real Reddit data from the week of November 11–18, 2026** (fetched November 18, 2026): 45 top posts and 116 top comments from r/Parenting, r/parentingteenagers, r/teenagers, r/LGBTeens and r/ADHD (r/TeenParenting returned nothing that week). The header shows a LIVE DATA banner with the week and fetch date.

It is a snapshot, not a live feed: the page does not fetch Reddit when it is opened. Refresh it weekly by re-running the pull described below and rebuilding the page.

## Use it

- Open `index.html` in any browser — no build step, no server needed.
- Or turn on GitHub Pages (Settings → Pages → Deploy from a branch) and share the link.

## How the live data works

Scraping Reddit's public pages does not work — Reddit blocks unauthenticated access (both `.json` endpoints return a network-security block page, and the RSS feed is empty). The working route is a permitted API:

1. **RedditAPIs** (https://www.redditapis.com) — pay-as-you-go Reddit API. Reads cost $0.0015 per call, and signup includes $0.50 in free credits (no card). Base URL: `https://api.redditapis.com`, bearer-token auth.
   - Weekly top posts: `GET /api/reddit/posts?subreddit=Parenting&sort=top&t=week&limit=10`
   - Top comments for solutions: `GET /api/reddit/comments?permalink=<permalink>`
   - A weekly refresh (6 subreddits, top comments on the top 5 posts each) is about 30 calls — roughly $0.05 a week. Pricing is per call, not per post, so fetching 100 posts costs the same as 25.
2. Keep your API key secret — as an environment variable on your host, never committed to the repo. The dashboard is served by a scheduled job that fetches the data and rebuilds the page, so the key never appears in the page itself.
3. Suggested subreddits: parents — r/Parenting, r/parentingteenagers, r/TeenParenting; teens — r/teenagers, r/LGBTeens, r/ADHD.
4. Stay read-only: never vote, post, or DM through the API.

Alternatives: Reddit's official Data API (OAuth, approval required; free tier is 100 queries/min for approved non-commercial use) or a public dataset.

## Make it your own

- Change the subreddit list and topic filters (screens, school, anxiety, sleep, friends, independence).
- Fork it, adapt the sections, and share your version.

## A note on the content

Reddit is skewed — mostly US, English-speaking, self-selected — and the advice in threads is anecdotal, never medical advice. Usernames are never shown, removed and deleted comments are left out, and threads about a teenager in crisis are pointed to alongside the crisis resources below rather than summarised.

If a teenager is in crisis: **call or text 988** (Suicide and Crisis Lifeline, US) or **text HOME to 741741** (Crisis Text Line). This dashboard never gives automated advice.

## License

MIT — see LICENSE.
