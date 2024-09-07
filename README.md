# json-log-filter

Filter JSON log records with exact field matching and a bounded result count.

## Run

Python 3.8 or later; no third-party packages or cloud credentials are required.

```sh
python3 tool.py examples/input.json
cat examples/input.json | python3 tool.py -
python3 -m unittest -v
```

## Example

Input:

```json
{
  "match": {
    "level": "error"
  },
  "records": [
    {
      "level": "info",
      "message": "ok"
    },
    {
      "level": "error",
      "message": "failed"
    }
  ]
}
```

Result:

```json
{
  "records": [
    {
      "level": "error",
      "message": "failed"
    }
  ],
  "total_matches": 1,
  "truncated": false
}
```

The command writes JSON to standard output. Exit 0 means evaluation completed;
a finding in the output may still require attention. Invalid input returns exit 2,
with an error on standard error and no result on standard output.

## Operational scope

In-memory exact matching only; input and output logs may contain sensitive information.

The tool evaluates supplied data locally. It does not change hosts, deploy
resources, or establish production compliance. Example identifiers and observations
are test fixtures. Keep credentials and private inventory out of Git.

## Design and verification

See [NOTES.md](NOTES.md) for the input contract, verification, and integration notes.
Related utilities: [url-health-manifest](https://github.com/sal-s-root/url-health-manifest), [http-status-budget](https://github.com/sal-s-root/http-status-budget).
