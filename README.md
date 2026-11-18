**English** | [Français](README.fr.md)

# Chineur RSS

Static RSS feed of the **Chineur de Livres Photo** (a photobook deal finder).

Generated every Monday at 00:10 (Europe/Paris) by an n8n workflow that:
1. queries the Notion database `Ma bibliothèque` (my library),
2. selects 10 discounted books (discount ≥ 25%, visible in the Chineur),
3. rebuilds `feed.xml` and pushes it to the `main` branch.

The file is then served by GitHub Pages at:

```
https://thomashmd.github.io/ChineurRSS/feed.xml
```

This is the URL that Metricool consumes to schedule social media posts automatically.

## Why a static file?

The old system exposed an n8n webhook that Metricool polled in a loop (several times an hour). Each call triggered a full workflow run (Notion + code + response) and kept 4 Railway services running for nothing. Switching to a static file removes 100% of those useless runs.
