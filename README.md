# Saaj Research: recipes from metadata

**A research spike for [Saaj](https://github.com/Abdullah-Albariqi/saaj): can a recipe be extracted from a TikTok or Instagram post's caption and transcript alone, without downloading and analysing the video?**

## The question

Analysing video is slow and expensive. If most recipe posts already carry the recipe in their caption or subtitles, Saaj could import them instantly and cheaply, and fall back to video only when it has to.

## The method

- 15 real public recipe posts: 10 from TikTok and 5 from Instagram.
- Fetched each post's metadata, captions and subtitle tracks with yt-dlp, retrying failures.
- Gave each post a verdict: `CAPTION_OK`, `TRANSCRIPT_OK`, `WEAK`, `NEEDS_VIDEO` or `FAILED`.

## Key results

| Verdict | Posts |
|---|---|
| Caption alone is enough (`CAPTION_OK`) | 10 |
| Transcript is enough (`TRANSCRIPT_OK`) | 2 |
| Weak signal (`WEAK`) | 1 |
| Video analysis needed (`NEEDS_VIDEO`) | 2 |
| Failed | 0 |

- **12 of 15 posts (80%)** could be imported from metadata alone.
- All 15 fetched successfully, and Instagram needed no login cookies.
- Only 4 of 15 had an Arabic transcript track, so captions matter more than subtitles for this audience.

**Outcome:** Saaj's import chain goes metadata first, then a transcript, then video only as a last resort.

## How it works

```
urls.txt ──▶ fetch.py (yt-dlp metadata + subtitles, with retries)
                 │
                 ▼
         extract.py (caption / transcript text)
                 │
                 ▼
         verdicts.py (classify each post) ──▶ report.md
```

## Tech stack

Python · yt-dlp

## Status

✅ **Completed research spike.** Its findings shaped Saaj's import design.

---

Source code is private and available on request. More about me: [Abdullah-Albariqi](https://github.com/Abdullah-Albariqi)
