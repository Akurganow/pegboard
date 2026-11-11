# Catalogues

An entry is listed only if it is public without key or account. Each entry cites the pages that state its access terms or data licence, the date each was read, and what they state. An entry with no such page is dropped. The plugin holds no key and reads none.

## What a lookup sends

1. Send a catalogue a public site hostname, a DOI or a repository path (`owner/repo`) and nothing else. Never send text from the user's question, a local file path or file contents, because catalogues are third-party services and the question and the local files may be private.
2. Send only an identifier that is already public: a DOI printed on a public page, or a repository path on a public host. A path taken from a private remote or an unpublished identifier would tell a third party that the repository or paper exists.
3. Give a host that is private, internal, intranet or IP-literal the status `not looked up`, and look nothing up, because its name would tell a third party that the host exists.
4. Look up one DOI or repository per call. A rating needs one record, so never load a whole list or a bulk file.

## Hostname lookup

### Wikipedia Perennial Sources

Host `en.wikipedia.org`. It is the only catalogue with a hostname route. Search with the host written without `www.`: `https://en.wikipedia.org/w/api.php?action=query&list=search&srsearch="<host>" prefix:"Wikipedia:Reliable sources/Perennial sources"&srlimit=2&format=json`, then read the subpage whose text lists the hostname with `https://en.wikipedia.org/w/index.php?title=<subpage>&action=raw`. With no such subpage the status is `no-record`: the search found no subpage naming the host, which is no proof that the list holds none.

Terms: [robot policy](https://wikitech.wikimedia.org/wiki/Robot_policy), read 2026-11-05; see also [Terms of Use](https://foundation.wikimedia.org/wiki/Policy:Terms_of_Use) section 12. The robot policy asks a bot to identify itself in its User-Agent header. Use the harness's own client and never invent a personal contact, because a made-up contact misleads whoever reads the header.

### Lateral-reading search

Reading a source from outside is called lateral reading. For each source, run one web search, worded by step 3 of `briefs/vetter.md`, and add nothing from the user's question, because a search goes to a third party. Put in one line, in the `reason` of the row, what others say about the source. A source with no outside mention reads "no mention found".

## Statuses

| Status | Meaning |
| :-- | :-- |
| `listed` | The catalogue returned a record. Show it as found, with the catalogue name. |
| `no-record` | The catalogue answered and holds no record. |
| `error(code)` | The call failed with this code, such as 400 or 403. |
| `skipped` | The harness refused the call, or no tool was available. |
| `not looked up` | The host is private, internal, intranet or IP-literal. |

Neither `no-record` nor `error(code)` says anything about safety. A source no listed catalogue covers reads "not checked". A negative record is a `listed` entry that rates the host unreliable, deprecated or blacklisted. A source on such a host is named in the reply with its record and gives no support to a point, because the record already rates it. A `no-record` from Crossref or OpenAlex does not prove a paper is not retracted: Crossref omits a Retraction Watch record that has no notice DOI.

## DOI and repository lookups

| Catalogue | Host | Route (DOI or repository path) | Terms read |
| :-- | :-- | :-- | :-- |
| Crossref REST API, with Retraction Watch data | `api.crossref.org` | `https://api.crossref.org/v1/works?filter=updates:<doi>&rows=20&cursor=*`; read each next page with the returned `next-cursor` until a page holds fewer than 20 records ([pagination](https://www.crossref.org/documentation/retrieve-metadata/rest-api/tips-for-using-the-crossref-rest-api/), read 2026-11-06); the filter `updates` means "Is an update to the given DOI", and `update-type` names a correction or retraction ([filter table](https://www.crossref.org/documentation/retrieve-metadata/rest-api/rest-api-filters/), read 2026-11-05). A returned record is an update notice. A record from the Retraction Watch database has `"source":"retraction-watch"` ([documentation](https://www.crossref.org/documentation/retrieve-metadata/retraction-watch/), read 2026-11-05) | [access terms](https://www.crossref.org/documentation/retrieve-metadata/rest-api/access-and-authentication/), read 2026-11-05; [Retraction Watch in Crossref](https://www.crossref.org/documentation/retrieve-metadata/retraction-watch/), read 2026-11-05, describes the data and states no usage terms |
| OpenAlex | `api.openalex.org` | `https://api.openalex.org/works/doi:<doi>?select=id,is_retracted,open_access`; `is_retracted` true counts as a retraction notice. Write `open_access.oa_url` in `record` as `oa_url: <url>`. It may be a landing page, a PDF or null (field seen in a returned work record, 2026-11-05) | [authentication](https://help.openalex.org/api/authentication/), read 2026-11-05: basic queries need no key, at 10 requests per second; [About](https://openalex.org/about), read 2026-11-05: the data is CC0. Neither page states terms of use for the API |
| OpenSSF Scorecard | `api.scorecard.dev` | `https://api.scorecard.dev/projects/github.com/<owner>/<repo>`; for `github.com` repositories only. Any other host reads "not checked" | [README, section "Scorecard REST API"](https://github.com/ossf/scorecard/blob/e73dbc5037aa4940d567e4878d50a7f524f30f08/README.md), read 2026-11-05: the data licence is CDLA Permissive 2.0; the section states no access terms and no authentication rule. The MCP section says a server that reads the REST API "needs no credentials" |

Entries by topic type: Wikipedia Perennial Sources for every source, Crossref and OpenAlex for every source with a DOI, and OpenSSF Scorecard added for practice/technology.

## Lookup rules

- Read the Crossref route to its last page.
- Never turn an error into `no-record`, because a failed call says nothing about the source.
- A refusal by the harness sets `skipped`. Do not retry through another route, because the refusal is a decision of the user or the harness.
- Do not work around a bot check or a 403 on a catalogue route. Mark it `error(403)` and move on, because the catalogue refused the call.
- When the user names hosts to avoid or to prefer, honour the list and never request an avoided host. If a redirect reaches one, discard that page.
