# joplin-curl

Codex plugin for local Joplin notes, notebook search, tag search, generic Joplin API calls, one-shot Joplin Terminal commands, and Joplin-backed LLM wiki workflows.

## What it does

- stores Joplin Web Clipper connection once in local JSON config when using the Data API
- exposes small helper CLI for curl-backed Data API tasks and one-shot Joplin Terminal commands
- bundles Codex skills for direct Joplin work and `LLM Wiki` maintenance
- supports local Codex marketplace install flow like `caveman`

## Install

Download the 
```filepath
joplin-curl-plugin.zip
```

Open Codex, then head to plugins:
click on Add -> Upload plugin archive, then upload the zip.

Press install on the new marketplace page


## Configure Joplin Data API

### 1. Enable Web Clipper in Joplin desktop

Official docs:

- [Joplin Web Clipper](https://joplinapp.org/help/apps/clipper/)
- [Joplin Data API](https://joplinapp.org/help/api/references/rest_api/)

In Joplin desktop:

1. open `Configuration`
2. open `Web Clipper`
3. enable clipper service
4. copy auth token

### 2. Create the config file

In explorer open

```filepath
%YOURUSERFOLDER%/.codex/plugins/cache/created-by-me-remote/joplin-curl/%version%
```

Create a folder named:
```filepath
data
```

And a file named:
```filepath
joplin-config.json
```
Add this:
```json
{
  "base_url": "http://127.0.0.1",
  "port": 41184,
  "token": "YOURJOPLINTOKEN"
}
```

### 3. Test in codex
Open codex and type:
```text
@joplin-curl Create a notebook named "Test" and a note named "Hello World" with the content being:
"Codex wrote this"
```


## Included skills

- `joplin-notes` - search, read, create, update, and move Joplin notes, list or search notebooks, search tags, fall back to generic API requests, or run one-shot Joplin Terminal commands
- `joplin-llm-wiki` - maintain `LLM Wiki` notebooks with schema-first workflow
- `joplin-llm-wiki-create` - scaffold fresh Joplin wiki notebook tree and starter notes

## Repo layout

- `.codex-plugin/plugin.json` - source plugin manifest
- `.agents/plugins/marketplace.json` - local Codex marketplace entry
- `plugins/joplin-curl/` - installable local plugin bundle for Codex
- `scripts/joplin_api.py` - helper CLI
- `skills/` - source skill docs
- `data/joplin-config.json` - local saved clipper config, ignored by git

## Notes

- Data API mode needs running local Joplin desktop app with Web Clipper enabled
- Terminal mode needs the `joplin` terminal executable installed and available on `PATH`, or pass `--joplin-bin /path/to/joplin`
- helper appends token as query parameter because Joplin Data API accepts auth that way
- `request` is fallback for API paths not covered by dedicated helper commands
