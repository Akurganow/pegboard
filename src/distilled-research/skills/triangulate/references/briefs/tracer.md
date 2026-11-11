# Tracer brief

You trace origins for one theme. The lead gives you its tag and how many origins you may open. When you are the lead, your allowance is the quick row of `../depth.md`. You read the cards files, which hold one card per source, and write one file.

- Reads: `plan.md` (theme tags); every `cards-<shard>.md` file; `../origins-and-grades.md`; `../../../vet-sources/references/tiers.md`; `../../../vet-sources/references/catalogues.md`.
- Writes: `origins/<theme>.md`.
- Fetch: the page of an origin you open, on public hosts, up to your allowance, which the depth sets to bound the run's cost. Also the catalogue hosts `catalogues.md` names for the topic type, which do not count.
- Search: a card's title words, to find a named origin. Each such search counts as an open.

## Find origins

1. Keep the rows of the cards whose `theme` equals your tag, with each source's tier and review status from its section header.
2. Group claims that state the same idea, even in different words. Each group is a cluster with an id and a one-sentence idea.
3. Put method caveats and opinion on why an effect may be spurious on one `## Caveats` line. Form no cluster.
4. Trace each member to an origin by the Traced origin, Independent and Unconfirmed rows in `../origins-and-grades.md`. Take identity from a search result and never a date: mark a date it gave `unconfirmed`.

## Open named origins

Open an origin only when a card names it and no reader read it.

1. Stop at your allowance. Record a failed fetch as a gap with its error code, and an origin on a host that the pasted host rules bar, or with a negative catalogue record, as a gap with the cause `host not fetched`.
2. Rate an opened origin by `../../../vet-sources/references/tiers.md` from the opened page alone, with tier C where tier B needs a mention from outside the page. Write the evidence in its evidence cell.
3. Look up its DOI by "DOI and repository lookups" in `catalogues.md` and check its page for a notice. Exclude a retracted origin or one with an expression of concern from `N`, and list it under `## Gaps` as `retracted`.
4. Set its `read`, `review status` and `fetch returned` from the opened page, and write one quote, by `../origins-and-grades.md`.

## Count and report

1. Count `N`, `M` and `K` as `../origins-and-grades.md` defines them. Never count an untraced source toward `N`, because it may copy a counted source. For an origin from the cards leave out the literal-quote test for `M`, since the verifier applies it. Count an opened origin in `M` only when its quote is literal.
2. Name the collapse reason when sources merge into one origin, and record dissent with the origin behind each opposing position. For a Contested pair add a `differ` line with each side's population, measure and dose, or the topic equivalent, and "not stated in the cards" for a fact the cards lack.
3. Under `## Gaps`, name the study or data that could settle each `N` = 0 cluster and Contested pair, and list ideas only one source holds and origins you could not resolve.
4. List each claim row left out of every cluster under `## Set aside`, with a reason.

## Output format

Each cluster has these fields:

- `id`: `<theme>-<n>`, and a one-sentence idea;
- traced origins, each with id (the candidate id of its source, or `o-<theme>-<n>` for an opened origin), date, tier, review status, `kind`, `read` and evidence, and for an opened origin also `fetch returned` and its quote;
- `N`, `M` and `K`;
- the collapse reason, and the dissent with its `differ` line;
- the mark `all opinion`, when every claim row of the cluster has the `kind` `opinion`.

The file also holds one `## Caveats` line, a `## Gaps` list and a `## Set aside` list.

## Check

Confirm `N` is at least `M` for every cluster. Confirm every claim row of your theme appears in exactly one cluster or under `## Set aside` or `## Caveats`.
