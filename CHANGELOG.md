# Setup record

All entries describe the same configuration session on **2026-09-30**.

## 1. Playback baseline

- Checked the existing macOS installation: shell 5.1.28, web UI 6.0.4, server 4.21.2, native arm64 executable. Code signing and notarization were checked; no application update or custom build was installed.
- Kept hardware-accelerated decoding on.
- Changed cache from **2 GiB to 10 GiB**.
- Changed torrent profile from **Default to Fast**.
- Verified the persisted Fast profile values shown in `preset.json`; they are observations of this server version, not a separate custom tuning patch.
- Played and sought within the official Blender Sintel 1080p trailer.
- Installed the TMDB add-on with its default English catalogs.

## 2. Source and subtitle cleanup

- Initially kept Torrentio's quality-then-seeders ordering, excluded REMUX/3D/Screener/Cam, and limited each quality to five results.
- Replaced the original unconfigured Torrentio installation to avoid duplicate source results.
- Removed legacy OpenSubtitles v0.24.0; retained OpenSubtitles v3.
- Kept English subtitles, normal size, white text, transparent background, and black outline.
- Enabled Style ASS subtitles.

The intermediate Torrentio preset in this step was superseded by step 3.

## 3. Measured failures and final playback preset

- The original TMDB BeamUp deployment failed search/catalog requests. Independent probes included 504 timeouts after roughly 12–14 seconds and a separate 403 response.
- Replaced it with the working ElfHosted deployment. Search probes returned matching results in roughly **0.57–0.89 seconds**, and matching results were verified inside Stremio. These were endpoint spot checks, not a controlled performance benchmark.
- Changed Torrentio to **By seeders**, **20 total results**, with 1080p/4K retained and REMUX, 3D, Screener, Cam, 720p, 480p, Other, and Unknown excluded.
- In the public-domain test title, the first Torrentio option changed from a reported 3-seeder 4K HDR source to a reported 100-seeder 1080p source; a 4K option with 51 reported seeders remained available.
- Selected the 4K option for a short playback check. Playback visibly reached 1:42. Sampled speeds were 2.79, 3.38, and 4.01 MB/s with six or seven connected peers. These are download-rate samples, not a source bitrate or a sustained benchmark.
- Stopped the test and returned to browsing.
- No paid caching/debrid service was installed or connected.

## 4. Discovery refinement

- The requested discovery preference was a **varied mix of highly rated movies and shows**.
- Enabled TMDB's **Digital Release Filter** and **Use TMDB prefix**.
- Left Strict Region Filtering off.
- Hid Year Movie, Year Series, Language Movie, and Language Series from Home while retaining them in Discover.
- Kept Latest Releases, Trending, and Popular movie/series rows on Home.
- Installed the new TMDB configuration, verified it, and removed the superseded duplicate.
- Tried IMDb Catalogs from the Community directory; removed it after its default list proved to be another generic Popular catalog.
- Added Rotten Tomatoes from the Community directory and verified the **RT: Certified Fresh** and **RT: Fresh TV Shows** rows with titles and posters.
- The Community listing showed Rotten Tomatoes **1.0.7**; a separate live backend manifest reported **1.0.9**. The session did not establish that the installed listing metadata had updated to 1.0.9.
- Backend spot checks returned 60 movie entries and 58 series entries. Counts are observations, not fixed catalog sizes. Individual review scores were not audited.

## Remaining limits

- YouTube search produced HTTP 500 errors; its normal browsing catalog loaded. No YouTube fix is claimed.
- 1080p/4K filtering intentionally removes lower-resolution fallbacks.
- English preferences cannot supply an audio track or subtitle that a source does not contain.
- Seed counts and metadata can be stale; add-on hosts can fail or change.
- TMDB's digital-release filter does not apply to other add-ons or guarantee regional/source availability.
- No long-duration playback, HDR color accuracy, surround-sound, subtitle synchronization, or all-codec compatibility test was performed.
- No app source code, operating-system network settings, account permissions, library contents, or subscription purchases were changed as part of the documented setup.
