# pg-contrib-card

Generate a shareable contributor card from a PostgreSQL contributor's
[Commitfest](https://commitfest.postgresql.org) history, patches submitted,
committed, active, commitfests participated in, and focus areas.

## Focus areas

Open [https://curiousone.in/pg-contrib-card/](https://curiousone.in/pg-contrib-card/) in a browser, type a Commitfest handle or name, and it builds the contrib card. You can then download a high-resolution PNG, copy a shareable link, or share to LinkedIn.

You can also link straight to a result with a query parameter:

```
https://curiousone.in/pg-contrib-card/?q=<handle>          # auto-runs the search
https://curiousone.in/pg-contrib-card/?q=<handle>&quick=1  # quick scan (current commitfest only)
```

### A note on CORS

`commitfest.postgresql.org` does not send CORS headers, so a browser cannot read
it directly. The page attempts a direct fetch first, then automatically falls
back to a public CORS proxy. This works, but depends on the proxy being up.

## How it works

1. Resolve the handle to a numeric id via
   `/lookups/user/?cf=<cf>&query=<handle>`.
2. Fetch each commitfest filtered by that author: `/<cf>/?author=<id>`.
3. Parse the patch rows, dedupe patches that span multiple commitfests
   (a committed status wins), and aggregate the totals and top tags.

## Attribution

Data comes from `commitfest.postgresql.org`. Slonik (the elephant) is a
trademark of the PostgreSQL Community Association; the mark drawn in the card is
an original stylized silhouette, not the official logo file.
