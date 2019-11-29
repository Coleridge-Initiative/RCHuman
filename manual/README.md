# Generating a public corpus for the leaderboard competition

This terminal step in the KG workflow includes two operations:

  1. Apply manually curated metadata to each publication as overrides (if any)
  2. Generate a public corpus for the ML leaderboard competition

This work depends on the following metadata components as input:

  - `partitions/*.json` - manually curated metadata for publications
  - `vocab.json` - vocabulary preamble for JSON-LD
  - `datasets.json` - dataset list from RCDatasets (TBD link as submodule)
  - `stream.json` - simulated stream from KG workflow (TBD replace by workflow)


## Metadata Format

We expect the following format for the stream of publication metadata,
with these fields as the minimum requirements for any entry in the
public corpus:

```
    {
        "doi": "10.1000/XYZ.0123456789",
        "publisher": "J Egreg Mansplain",
        "title": "Market share dominance among Samoan-owned coconut tree services in Oahu",
        "url": "https://example.com/article/5150",
        "pdf": "https://example.com/article/5150?render=pdf",
        "datasets": [
            "dataset-000",
            "dataset-123"
        ]
    },
```


## Running

This workflow step generates `uuid` values (late binding) for both
publications and datasets, then serializes the full output as TTL in
`tmp.ttl` and as JSON-LD in `tmp.jsonld` for a corpus update:

```
python gen_ttl.py
```

Afterwards, move/rename/test/commit the generated `tmp.*` files as a
new release for the corpus repo
<https://github.com/Coleridge-Initiative/rclc>


## Omissions

Note that publications get omitted from the corpus when:

  * the metadata has `"omit-corpus": true` flag
  * no open access PDF has been identified
  * the open access PDF has its format corrupted

