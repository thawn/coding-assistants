# Plugin configurations

## `continue.dev` with Blablador

1. Create an API key as described in [the Blablador documentation](https://sdlaml.pages.jsc.fz-juelich.de/ai/guides/blablador_api_access/)
2. Copy the example configuration file from `continue.dev_blablador/config.json` to:
   * Mac/Linux:  `~/.continue/config.json`
   * Windows: `%USERPROFILE%\.continue\config.json`
3. Replace `<insert API key here>` with the API key generated in step 1 (Note: it should start with `gplat-...`)

## `continue.dev` with HZDR AI

1. Copythe example configuration file from `continue.dev_hzdr/config.json` to:
   * Mac/Linux:  `~/.continue/config.json`
   * Windows: `%USERPROFILE%\.continue\config.json`

## `continue.dev` with LM Studio on your computer

This requires a powerful GPU with ~ 20 GB RAM (e.g. RTX 3090) or an Apple M CPU with ~24GB RAM.

1. Install LM Studio (https://lmstudio.ai/download)
2. Download the `qwen/qwen3-coder-30b` model (click on the purple looking glass and type `coder` into the search field)
3. Make sure the server is running (click on the green command line icon and make sure it says `Status: running` in the top)
4. Copy the example configuration file from `continue.dev_lmstudio/config.json` to:
   * Mac/Linux:  `~/.continue/config.json`
   * Windows: `%USERPROFILE%\.continue\config.json`
