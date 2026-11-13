# Records

A record is an outside account of a source: who stands behind it, whether it was withdrawn or corrected, how others assess it. Choose the records for each source yourself, because no fixed list covers every kind of source, place and language.

## Choose the records for a source

1. Name the source's kind and its place, when it has one: the country or region that publishes it. State what a record must answer about it. The table gives the question for common kinds.
2. Search the web for records that answer it, in the source's language and the user's. Word the search with the kind, the place and that question, and nothing from the user's question. Reuse the choice for every source of that kind and place.
3. Test each candidate by the next section, and look the source up in the records that pass.

| Kind of source | Question a record answers |
| :-- | :-- |
| Paper | Was it retracted, corrected or flagged with a concern? |
| News outlet or site | Who owns, funds and edits it, and how do independent assessors rate it? |
| Repository or package | Is it maintained, and by whom? |
| Statistic or standard | Who issued it, by what method and coverage, and was it revised? |

## What makes a record fit to rely on

A record fits only when it meets all five tests.

- **Open:** it is public without key or account, and its terms allow automated reading.
- **Independent:** to rate how good a source is, the record's keeper does not own, fund, sell or publish it. A record of a fact, such as a retraction, a release history or an owner, may come from the publisher or registry, and `reason` says so.
- **Method and coverage stated:** it says what it includes, how an entry gets in and who judges.
- **Current:** it shows its last update, recent enough for the topic.
- **Covering:** it covers this kind of source in this place.

## What a lookup sends

1. Send a record only a public identifier of the source: its hostname, published name, DOI, repository path or package name. Never send text of the question, a local path or file content, because records are third-party services and these may be private.
2. Send no path from a private remote and no unpublished identifier, because it would tell a third party that it exists.
3. Look nothing up for a host that is private, internal, intranet or IP-literal, because its name would tell a third party that the host exists.
4. Look up one identifier per call. A rating needs one entry, so never load a whole list or a bulk file. Read all pages of notices for that identifier.
5. A service that asks clients to identify themselves gets the harness's own client, never an invented contact, because a made-up contact misleads its readers.

## Statuses

| Status | Meaning |
| :-- | :-- |
| `listed` | A fitting record returned an entry. Show it as found. |
| `no-record` | A fitting record answered and holds no entry. |
| `error(code)` | The call failed with this code, such as 403. |
| `skipped` | The harness refused the call, or no tool was available. |
| `not looked up` | The host is private, internal, intranet or IP-literal. |
| `not checked` | No fitting record was found for this kind and place. Say which kinds you searched for. |

## Rules

- Only `listed` says anything about a source.
- A negative record is a `listed` entry that rates the source unreliable or blacklists it. Name the source with its record. It gives no support to a point, because the record already rates it.
- A retraction record can omit a notice, so `no-record` does not prove a paper stands. Read the paper's own page for a notice too.
- Never turn an error into `no-record`, because a failed call says nothing about the source.
- Do not retry a refused call through another route, because the refusal is a decision of the user or the harness.
- Do not work around a bot check or a 403. Mark `error(403)` and move on, because the record refused the call.
- Honour the user's list of hosts to avoid or prefer. If a redirect reaches an avoided host, discard that page.
