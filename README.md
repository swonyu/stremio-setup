# Stremio setup: fast playback and better discovery

A reproducible record of a Stremio setup tuned for responsive playback, 1080p/4K sources, English subtitles, and a varied mix of well-reviewed movies and shows.

**This is a settings and setup repository. No Stremio application code was modified.** The final configuration was checked on macOS with an Apple Silicon Mac on **30 September 2026**. Add-on availability and performance can change.

## Quick setup

1. Install or open [Stremio from its official site](https://www.stremio.com/downloads).
2. In **Settings → Player**, use the player settings below.
3. In **Settings → Streaming**, choose **10 GiB** cache and the **Fast** torrent profile.
4. In **Addons → Add addon**, paste the manifest links below. If an older configuration of the same add-on is installed, add the new configuration, verify it, and remove the superseded duplicate.
5. Open **Home** or **Discover** to browse the TMDB and Rotten Tomatoes rows. Keep **OpenSubtitles v3** and remove the legacy OpenSubtitles add-on if both are installed.

[preset.json](preset.json) contains the exact reference settings and final manifest URLs. It is **not** an account export or a file Stremio imports directly.

## Playback and subtitles

| Setting | Final value | Purpose |
|---|---|---|
| Hardware-accelerated decoding | On | Use the device's supported hardware decoding path |
| Torrent profile | Fast | Built-in peer/download preset |
| Disk cache | 10 GiB | Allow more downloaded video to remain cached |
| Default subtitle language | English | Prefer English subtitles |
| Subtitle size | 100% | Keep the normal size |
| Subtitle appearance | White, black outline, transparent background | Keep text readable |
| Style ASS subtitles | On | Enable ASS subtitle styling |
| Default audio track | English | Prefer an English track when present |
| Surround sound | Off | Retain the existing audio configuration |
| Auto-play next episode | On | Retain episode continuity |
| Next-video popup | 35 seconds | Retain the existing prompt timing |
| External player / transcode profile | Disabled | Retain the native playback path |

The working local streaming URL was `http://localhost:11470/`. It is a loopback address for the computer running Stremio, not a remote server to expose publicly. Leave an already working server URL alone.

The 10 GiB cache and Fast profile were changed during setup; hardware decoding and the audio/auto-play values were already set appropriately. Extra cache does not make a poorly seeded source fast. On a device with limited storage or a constrained connection, use a smaller cache or the Default torrent profile.

## Add-on configuration

### Torrentio: HD sources, ordered by seeders

[Open the configured manifest](https://torrentio.strem.fun/sort=seeders%7Cqualityfilter=brremux,threed,scr,cam,720p,480p,other,unknown%7Climit=20/manifest.json), or copy this URL into **Addons → Add addon**:

```text
https://torrentio.strem.fun/sort=seeders%7Cqualityfilter=brremux,threed,scr,cam,720p,480p,other,unknown%7Climit=20/manifest.json
```

- Sort: **By seeders**.
- Limit: **20 total results**, not 20 per quality.
- Keep 1080p and 4K options, including available HDR variants.
- Exclude BluRay REMUX, 3D, Screener, Cam, 720p, 480p, Other, and Unknown.
- No debrid account or paid service was connected.

This favors sources reporting more seeders within the retained quality categories. Reported seeders do not guarantee speed, and resolution labels do not guarantee a good encode. A highly seeded 1080p result may appear above 4K. Titles available only in the excluded categories may return no Torrentio results.

To customize or restore lower-resolution fallbacks, use [Torrentio's configurator](https://torrentio.strem.fun/configure). Stream only content you have permission to access.

### TMDB: released movies and clearer discovery rows

[Open the exact configured manifest](https://tmdb.elfhosted.com/N4IgTgDgJgRgsgUygSwIYBUCeEEGcQBcoEA9rgC4JiHlgCuCANCADYkDmJhAZqi7kxAxUAYwDWUMCQg8+AgL7Ny00hSq4xCTIRAglKspTC4AwiQB23ZO0LFDVLDh2qjAWigJedFuT0gKmCwIOgC2JB5g5n7kABZ0ITDmqMgsAEKoUOwIAApkyOTIFjrKEK5g1jG+SnEJSSnpmQgAysgAXsEE-iF8LNE1iclpLHTUBLz8CIog5CGw2WCeyAAexfTBzCyo5ux0qFk6COauAKpNfhQLqCHI24QA2gC6zCKo5Hwc+AR3oMhQxbMwAB0m0oFGi2A6IDCADdkOsQEkQpCADKvPDkAAEACUEEFUAJ8MxcDESAB3ACS5gAEiQkTQ1oofn9OjNYMC0WClBCdAJyng-IiURzMTi8QTziSKdTaR1aAxGSBfv82bRDihblynJ0YXCBVdIegFuZ1TYiZLKTS6QQ5ZNGEzlUDVcabqbptzOry4YSEfqdIa1S6JWSLTL6fK7YrmdMAYCSuCtVCSLD4YKdLkIN5UNQzcHpVabQqlSyY3HNZDPfzmKnOunM9n-Oa87KGRGi9G2ZgEFn45CdSnfZ0AJpd+vE3OWjrjBStqOsoGd7tlnlUL16q0gYeLhvj0NjOS2+3Ftmbba7fZL7VJ3VVgcgVGnvbwsdSieyCaF2cxk87R895d871qzvLYf3PbcX13KdJieEAXgoMw6HMXwCAAVhzUkAEEsixV4XUpABxQ4Fk+aY1j8Q5UBgIIsIQHCCluTooKDTDsNw7YAHV8hickATowNGP3c5aGQERyBxdhCnMAAxFIjB0JjmBQCS3hYUUuwEGSfCoMNJiAA/manifest.json) and paste its address into **Addons → Add addon**. The full URL is also in [preset.json](preset.json).

The configuration uses [TMDB on ElfHosted](https://tmdb.elfhosted.com/configure/):

- Language: **English (US)**; search enabled.
- **Digital Release Filter on**: filters movie catalogs against digital-release availability. This does not prove a playable source exists or that a title is available in every country.
- **Strict Region Filtering off**: English (US) is the metadata language choice, not a claim about the viewer's country.
- **Use TMDB prefix on**: clearly identifies these rows.
- Home: Latest Releases, Trending, and Popular for both movies and series.
- Discover only: Year and Language for both movies and series. These four catalogs are hidden from Home, not disabled.
- No TMDB, Trakt, MDBList, AI-search, or poster-rating account/key was connected.

For manual reconstruction, open the configurator, choose the settings above, and use **Copy URL** to get the manifest. In **Catalogs**, leave each catalog enabled but turn **Home** off for Year Movie, Year Series, Language Movie, and Language Series.

Digital-release filtering applies to TMDB movie rows, not Cinemeta, Rotten Tomatoes, or every catalog in the app. Latest Releases for series concerns new shows; it should not be treated as a complete list of new seasons or episodes.

### Rotten Tomatoes: two review-based rows

[Rotten Tomatoes manifest](https://7a82163c306e-rottentomatoes.baby-beamup.club/manifest.json):

```text
https://7a82163c306e-rottentomatoes.baby-beamup.club/manifest.json
```

Adds **RT: Certified Fresh** movies and **RT: Fresh TV Shows**. Both rows loaded in Stremio. The add-on was installed from Stremio's Community directory and needs no account for these catalogs. Its optional RPDB poster key was left blank.

This is a third-party catalog that draws on Rotten Tomatoes; this repository is not affiliated with Rotten Tomatoes. Catalog labels are supplied by the add-on; individual ratings were not independently audited.

### Subtitles and existing add-ons

[Official OpenSubtitles v3 manifest](https://opensubtitles-v3.strem.io/manifest.json):

```text
https://opensubtitles-v3.strem.io/manifest.json
```

Keep one **OpenSubtitles v3** installation. The legacy **OpenSubtitles v0.24.0** was removed during setup.

Existing Cinemeta, YouTube, WatchHub, Public Domain Movies, and Local Files were retained. A temporary IMDb Catalogs trial was removed because its default Popular list duplicated existing discovery rather than adding the desired highly rated selection.

## Verification and limits

The setup was observed with Stremio shell **5.1.28**, web UI **6.0.4**, and streaming server **4.21.2**. The installed macOS executable was native **arm64**. These are tested versions, not a promise that they are the newest releases.

- Persisted server settings confirmed **10 GiB** and the Fast profile's values.
- The Torrentio source list visibly used the configured seeders sort and exclusions.
- TMDB search returned matching results after replacing a failing deployment.
- Both Rotten Tomatoes rows displayed titles and posters in Stremio.
- A short 4K playback test reached **1 minute 42 seconds**; sampled download speeds included **2.79–4.01 MB/s**. Playback was stopped afterward.
- An official Blender 1080p trailer played and seeking worked.

These are functional spot checks, not controlled before/after benchmarks, sustained buffering tests, or guarantees for other titles/devices. Catalog changes improve discovery; they do not directly increase video bandwidth.

**Known remaining issue:** YouTube search rows returned HTTP 500 during the session. Regular YouTube browsing still loaded, so the add-on was retained. This issue was not fixed.

See [CHANGELOG.md](CHANGELOG.md) for the changes in order and the limits of the measurements.

## Reverting or adapting

All changes use normal Stremio settings or add-on installation:

- Restore cache to **2 GiB** and torrent profile to **Default** to return those two values to their starting state.
- Turn **Style ASS subtitles** off to restore its starting state.
- Use the Torrentio configurator to change ordering, result count, or quality exclusions.
- Use the TMDB configurator to restore Home rows or disable digital-release filtering.
- Remove Rotten Tomatoes if its two rows are not useful.
- Add-ons can normally be reinstalled from Stremio's directory; verify working replacements before removing an active configuration.

## Sources and privacy

- [Stremio downloads](https://www.stremio.com/downloads)
- [Stremio official add-ons registry](https://github.com/Stremio/stremio-official-addons)
- [Stremio add-on protocol](https://stremio.github.io/stremio-addon-sdk/protocol.html)
- [TMDB add-on source](https://github.com/mrcanelas/tmdb-addon)
- [Torrentio configurator](https://torrentio.strem.fun/configure)
- [Rotten Tomatoes add-on configurator](https://7a82163c306e-rottentomatoes.baby-beamup.club/configure)

The public files are hand-authored settings and documentation. They contain no Stremio account export, login token, API key, personal library, viewing history, private messages, app database, screenshot, or machine-specific home-directory path. No video files or Stremio application binaries are included.
