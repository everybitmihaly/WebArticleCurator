# Portal configs: review and update report

Date of the review: 2026-10-11. Branch: `update/portals_202610_review`.

All 56 portal configs in `configs/` except `p444` (fixed earlier) were tested against the live sites. **21** were updated and work again, **24** work without any change, and **11** could not be made to work and were left untouched.

## How the portals were tested

Each config was run through the real crawler classes (`NewsArchiveCrawler`, `WarcCachingDownloader`) with its own schema and extractor functions, at one request per two seconds:

- up to three columns per portal (first, middle, last), two archive pages each: the extracted article URLs and the next-page URL were checked;
- four of the extracted articles were downloaded, and the multi-page function was run on them where the schema has one;
- for date-based archives the last three days of the column's date range were used;
- for most multi-column portals (hvg, hirado, nepszava, p888, maszol, feol, lelato_transindex, index, p24_roboraptor and the other p24 configs) the first archive page of every column was also checked; for `p24_istentudja` the first 14 of its 208 columns, for `forum_index` only the three sampled ones of its 254.

This is a light test: it shows that a config extracts article URLs, pages through the archive and downloads articles, but it is not a full crawl. Changes were limited to the YAML schemas and the extractor functions; the old selectors were kept as a fallback, so WARC files cached before the redesigns still work and the self-tests of the extractor files still pass.

## Overview

| Portal | Updateable | State now | Test result |
|---|---|---|---|
| `abcug` | No | Site gone | - |
| `alfahir` | Yes, updated | Works after update | 2/2 pages, 20 URLs, 4/4 articles |
| `atlatszo_ro` | Yes, updated | Works after update | 6/6 pages, 90 URLs, 4/4 articles |
| `bbeacon` | No | Site gone | - |
| `blikk` | Yes, updated | Works after update | 2/2 pages, 60 URLs, 4/4 articles |
| `epiteszforum` | Yes, updated | Works with `--user-agent` | 2/2 pages, 64 URLs, 4/4 articles |
| `feol` | Yes, updated | Works after update | 6/6 pages, 60 URLs, 4/4 articles |
| `forum_index` | Not needed, works | Works | 3/4 pages, 240 URLs, 4/4 articles |
| `foter` | Yes, updated | Works after update | 2/2 pages, 32 URLs, 4/4 articles |
| `gov_koronavirus` | No | Section removed | - |
| `hang` | Yes, updated | Works after update | 6/6 pages, 90 URLs, 4/4 articles |
| `hataratkelo` | Not needed, works | Works | 2/2 pages, 10 URLs, 4/4 articles |
| `hirado` | Not needed, works | Works | 4/5 pages, 40 URLs, 4/4 articles |
| `hvg` | Yes, updated | Works after update | 5/5 pages, 116 URLs, 4/4 articles |
| `index` | Yes, updated | Works after update | 4/4 pages, 113 URLs, 4/4 articles |
| `index_koronavirus` | Not needed, works | Works | 1/4 pages, 13 URLs, 4/4 articles |
| `jogtar` | Yes, updated | Works after update | 1/1 pages, 107 URLs, 4/4 articles |
| `kremmania_forum` | Not needed, works | Works | 2/2 pages, 60 URLs, 4/4 articles |
| `kronikaonline` | Yes, updated | Works after update | 2/2 pages, 32 URLs, 4/4 articles |
| `kurucinfo` | No | Blocked | - |
| `lelato_transindex` | Not needed, works | Works | 5/5 pages, 86 URLs, 4/4 articles |
| `magyaridok` | No | Archive behind subscription | - |
| `magyarnarancs` | Not needed, works | Works | 2/2 pages, 24 URLs, 4/4 articles |
| `maszol` | Yes, updated | Works after update | 6/6 pages, 307 URLs, 4/4 articles |
| `merce` | Yes, updated | Works after update | 4/5 pages, 25 URLs, 4/4 articles |
| `mno` | Yes, updated | Works after update | 6/6 pages, 191 URLs, 4/4 articles |
| `mosthallottam` | Yes, updated | Works after update | 2/2 pages, 18 URLs, 4/4 articles |
| `nepszava` | Not needed, works | Works | 6/6 pages, 180 URLs, 4/4 articles |
| `nol` | No | Archive behind subscription | - |
| `origo` | Yes, updated | Works after update, with a limit | 2/2 pages, 118 URLs, 4/4 articles |
| `p24_belfold1` | Not needed, works | Works | 4/4 pages, 64 URLs, 4/4 articles |
| `p24_belfold2` | Not needed, works | Works | 6/6 pages, 144 URLs, 4/4 articles |
| `p24_gazdasag` | Not needed, works | Works | 6/6 pages, 94 URLs, 4/4 articles |
| `p24_istentudja` | Yes, updated | Works after update | 3/3 pages, 10 URLs, 4/4 articles |
| `p24_kulfold` | Not needed, works | Works | 4/4 pages, 56 URLs, 4/4 articles |
| `p24_rangado` | Not needed, works | Works | 6/6 pages, 130 URLs, 4/4 articles |
| `p24_rest1` | Not needed, works | Works | 4/4 pages, 50 URLs, 4/4 articles |
| `p24_rest2` | Not needed, works | Works | 6/6 pages, 85 URLs, 4/4 articles |
| `p24_rest3` | Not needed, works | Works | 5/5 pages, 108 URLs, 4/4 articles |
| `p24_roboraptor` | Yes, updated | Works after update | 6/6 pages, 59 URLs, 4/4 articles |
| `p24_sokszinuvidek` | Not needed, works | Works | 6/6 pages, 144 URLs, 4/4 articles |
| `p888` | Not needed, works | Works | 6/6 pages, 105 URLs, 4/4 articles |
| `penzcsinalok_transindex` | No | Portal discontinued | - |
| `plakatmagany_transindex` | Not needed, works | Works | 2/2 pages, 10 URLs, 4/4 articles |
| `semmelweis` | Not needed, works | Works | 2/2 pages, 48 URLs, 4/4 articles |
| `szekelyhon` | Not needed, works | Works | 4/4 pages, 64 URLs, 4/4 articles |
| `telex` | Yes, updated | Works after update | 2/2 pages, 21 URLs, 4/4 articles |
| `telex_koronavirus` | Yes, updated | Works after update | 2/2 pages, 20 URLs, 4/4 articles |
| `termvil` | Not needed, works | Works | 2/2 pages, 20 URLs, 4/4 articles |
| `think_transindex` | Not needed, works | Works | 2/2 pages, 40 URLs, 4/4 articles |
| `transindex` | No | Site gone | - |
| `tv_transindex` | No | Site gone | - |
| `utazomajom` | Not needed, works | Works | 3/3 pages, 30 URLs, 4/4 articles |
| `vadhajtasok` | Yes, updated | Works after update | 6/6 pages, 73 URLs, 4/4 articles |
| `valasz` | No | Site gone | - |
| `vs` | No | Site gone | - |

"Not needed, works" means that the config passed the test as it was. The test result column shows: archive pages that yielded article URLs / archive pages requested, the number of distinct article URLs extracted, and articles downloaded / tried. Where not every page yielded URLs, the reason is in the portal's summary below. For `epiteszforum` the result is the one with `--user-agent` set.

## State of each portal

### abcug

**Site gone.** The domain `abcug.hu` does not resolve anymore (DNS error), so there is nothing to crawl.

### alfahir

**Works after update.** The date-range search archive (`/kereso?...`) answers 404 since the redesign. The schema now uses the paginated list of all articles (`/hirek/oldalak/N`, about 23,500 pages) in a single column instead of the three date-based columns, and the next-page extractor follows the new `<link rel="next">`. The portal answered 403 for a few minutes after a quick burst of requests, so it should be crawled slowly (noted in the schema).

### atlatszo_ro

**Works after update.** The search-based archive is still there, but the list items and the next-page link changed with the new theme. Both extractors were updated; all three language columns (hu, ro, en) work.

### bbeacon

**Site gone.** The TLS certificate of `budapestbeacon.com` has expired and the server answers "503 Site Currently Unavailable" even when the certificate is ignored.

### blikk

**Works after update.** The date-based archive still exists, but the article list and the "Következő oldal" link are in a new container, which made the old extractor crash. Both extractors were updated; a whole day (4 archive pages, 109 articles) was paged through correctly.

### epiteszforum

**Works with `--user-agent`.** The extractors still work, but the portal answers 403 to requests without a User-Agent header, which is the default of the crawler. With `--user-agent` set, the test passed unchanged. Only a note was added to the schema.

### feol

**Works after update.** The column pages moved from `/NAME/` (404 now) to `/rovat/NAME?page=N` with new list and pager markup. Schema columns and both extractors were updated; all six columns work. (The site sends a Cloudflare challenge to `curl`, but not to the crawler.)

### forum_index

**Works.** Topic lists, topics and multi-page topics download correctly. One of the three sampled columns (`trollitika`) answers 403 because that forum now requires a login; only 3 of the 254 columns were sampled.

### foter

**Works after update.** The category archives (`/cikk/category/NAME/`) were renamed and restructured. The schema now uses the portal's paginated article feed (`/mod/open24h.php?p=N`, the same mechanism as szekelyhon) in a single column, and the extractor handles its markup. The feed currently goes back 100-200 pages (16 articles each), so the 11 category columns are no longer separate.

### gov_koronavirus

**Section removed.** The coronavirus information section of `nnk.gov.hu` answers 404; the institution was reorganised and the 2020 article list has no successor on the site.

### hang

**Works after update.** New list markup, and `/COLUMN/?page=N` is now redirected to `/COLUMN` without the page number, which would have returned the first page forever. The extractor was updated and the trailing slash removed from the seven affected column URLs.

### hataratkelo

**Works.** Archive paging and article download work unchanged.

### hirado

**Works.** The AJAX list endpoint and the articles work unchanged. Three of the 12 columns (`koronavirus`, `video-no-comment`, `kultura-eletmod`) return an empty list now.

### hvg

**Works after update.** Article cards and pagination changed. Both extractors were updated (including the photo column `nagyitas`). 16 of the 19 columns list articles under their own URL; `hvgmuerto` answers 404, `velemeny_nyuzsog` and `w` are redirected to `velemeny`, and `pszichologiamagazin` is redirected to `pulzus.hvg.hu` (and works).

### index

**Works after update.** The `index` column worked. The `velvet` column produced invalid relative URLs (e.g. `celeb/`) because the velvet.hu archive has a new card markup; the extractor now picks the article link. Note that the velvet archive lists the same index.hu articles as the `index` column now.

### index_koronavirus

**Works.** Works unchanged; the tag has no recent articles, the older period lists and downloads correctly.

### jogtar

**Works after update.** The schema pointed to the extractor of index, which finds nothing on `net.jogtar.hu`. New extractors were added for the result list (document links) and for the next-page link (200 results per page). During the review the host refused or timed out every connection from the test machine for a while (at least 15 minutes) and then answered again; whether that was an outage or a temporary block after the test requests is not known, so crawl it slowly.

### kremmania_forum

**Works.** Topic list, topics and multi-page topics work unchanged.

### kronikaonline

**Works after update.** The portal moved to `kronika.ro` and its search-based archive lists nothing anymore. The schema now uses the paginated article feed (`kronika.ro/mod/open24h.php?p=N`, 2,000-3,000 pages), which the existing extractor already handles.

### kurucinfo

**Blocked.** `kuruc.info` answers every request with a Cloudflare JavaScript challenge (403), with or without a browser User-Agent. It cannot be crawled without a browser.

### lelato_transindex

**Works.** All seven columns work through a redirect to `lelato.transindex.adatbank.ro` (archived site).

### magyaridok

**Archive behind subscription.** The site only shows a notice that the archive can be subscribed to at Lapcentrum; no article lists are available.

### magyarnarancs

**Works.** The search-based archive, paging and articles work unchanged.

### maszol

**Works after update.** Article extraction worked, but the next-page link was not found (class renamed), so only the first page of each column was crawled. Fixed; all eight columns page correctly.

### merce

**Works after update.** The main column works unchanged. The `balraat` blog has no articles after 2022-04 and its empty months answer 404, so `date_last_article` was set for that column. (The one failed page in the test is the last month of the closed `avm` column, 2021-07, which also answers 404.)

### mno

**Works after update.** magyarnemzet.hu was redesigned: the column pages moved to `/rovat/NAME?page=N` with new list and pager markup. Schema and both extractors were updated for the seven columns. The former `archivum` column (all articles) was dropped because it has no successor (`/friss-hirek` only lists recent articles).

### mosthallottam

**Works after update.** New theme: the list items and the next-page link changed. The portal got its own article extractor (it shared one with magyaridok) and the shared next-page extractor handles the new link; semmelweis, which uses the same function, still works.

### nepszava

**Works.** The JSON list and article endpoints work unchanged for all 15 columns.

### nol

**Archive behind subscription.** The site only shows a notice that the archive can be subscribed to at Lapcentrum; no article lists are available.

### origo

**Works after update, with a limit.** The old archive URLs are redirected to a new daily archive with different markup; the extractor was updated and old dates (1998-2021) work too. **Limitation:** the new archive lists at most 100 articles per day, so busy days are incomplete (noted in the schema). The site's search API, which could page further, returns empty responses to the crawler.

### p24_belfold1

**Works.** All seven columns work unchanged.

### p24_belfold2

**Works.** All nine columns work unchanged.

### p24_gazdasag

**Works.** All three columns work unchanged.

### p24_istentudja

**Works after update.** The tag pages use the same article widgets as 24.hu now, so the extractor found nothing. It now falls back to the 24.hu extractor; the 14 tag columns checked all list their articles.

### p24_kulfold

**Works.** All four columns work unchanged.

### p24_rangado

**Works.** All seven columns work unchanged.

### p24_rest1

**Works.** All three columns work unchanged.

### p24_rest2

**Works.** Nine of the ten columns list articles; `uzleti-tippek3` returned an empty page for the tested date.

### p24_rest3

**Works.** All twelve columns work unchanged.

### p24_roboraptor

**Works after update.** The portal left 24.hu and moved to `www.roboraptor.hu`; the old column URLs redirect to unrelated articles or 404. The schema points to the new category pages and new extractors were added; all seven columns work.

### p24_sokszinuvidek

**Works.** All nine columns work unchanged.

### p888

**Works.** All 20 columns work through a redirect to `archivum.888.hu`.

### penzcsinalok_transindex

**Portal discontinued.** The site redirects (via `penzcsinalok.ro`) to the "Pénzcsinálók" column of Transtelex, a different portal with a different structure; the old columns and their archive are not available.

### plakatmagany_transindex

**Works.** Works through a redirect to `plakatmagany.transindex.adatbank.ro` (archived site).

### semmelweis

**Works.** Tag archive, paging and articles work unchanged.

### szekelyhon

**Works.** Both columns (main and sport feed) work unchanged.

### telex

**Works after update.** The archive list items changed; the article URL extractor was updated. Paging and multi-page (live) articles still work.

### telex_koronavirus

**Works after update.** Same fix as telex (shared extractor); the column lists and downloads correctly.

### termvil

**Works.** Works unchanged (through a redirect to `www.termvil.hu`).

### think_transindex

**Works.** Works through a redirect to `think.transindex.adatbank.ro` (archived site).

### transindex

**Site gone.** `archivum.transindex.ro` redirects to `archivum.transindex.adatbank.ro`, which does not resolve (DNS error).

### tv_transindex

**Site gone.** `tv.transindex.ro` redirects to `tv.transindex.adatbank.ro`, which does not resolve (DNS error).

### utazomajom

**Works.** Category archive, paging and articles work unchanged.

### vadhajtasok

**Works after update.** New list markup; the extractor was updated. The columns are paged up to a fixed `max_pagenum`, which was far behind (e.g. 1,390 vs 4,187 pages for `0-24`); all eight values were updated to the current page counts.

### valasz

**Site gone.** `valasz.hu` answers with Cloudflare error 1001 (409): the site behind the domain no longer exists.

### vs

**Site gone.** `vs.hu` answers 403 with an empty body or drops the connection; the archive endpoint is not reachable.

## Things to know before crawling

- **origo:** at most 100 articles per day are listed by the new archive, so a crawl of busy days is incomplete.
- **alfahir:** crawl slowly (for example `--max-no-of-calls-in-period 1 --limit-period 4`); bursts are answered with 403 for minutes.
- **epiteszforum:** needs `--user-agent`.
- **jogtar:** the host was unreachable from the test machine for a while during the review; crawl it slowly.
- **foter, kronikaonline:** the article feed replaces the old archive; foter's feed only reaches 100-200 pages back.
- **mno:** there is no archive of all articles anymore, only the columns (the portal has more columns than the seven in the schema).
- **vadhajtasok:** `max_pagenum` values are a snapshot of 2026-10-11 and have to be raised again later.
- **Portals working through redirects** (`p888`, `lelato_transindex`, `plakatmagany_transindex`, `think_transindex`, `termvil`, some `hvg` columns): the schemas still contain the old host names, which keeps them compatible with previously crawled WARC files, but they depend on the redirects staying in place.
- **Multi-page article functions** were only re-verified for telex, forum_index and kremmania_forum; for the other updated portals (hvg, alfahir, origo, index) no paginated article was found in the samples.
- No new pages were added to the test fixtures in `tests/`; the existing self-tests only cover the old designs.
