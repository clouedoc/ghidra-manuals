# ghidra-manuals
A way to download Ghidra processor manuals that should be future proof. When future versions of Ghidra add support for new processors and have new processor manuals, this program will be able to add those new manuals to its config to download later.

Currently updated for **11.2**

# How to Use

The quickest way to run this is with [`uvx`](https://docs.astral.sh/uv/),
which fetches and runs the tool straight from this fork without you having
to clone anything:

```
uvx --from git+https://github.com/clouedoc/ghidra-manuals ghidra-manuals ~/ghidra_11.2
```

A `config.json` listing all known processor manuals is bundled with the
package, so the command above works as-is. If you want to use your own
edited config (for example to add backup URLs), point at it with
`--config`:

```
uvx --from git+https://github.com/clouedoc/ghidra-manuals ghidra-manuals \
    ~/ghidra_11.2 --config ./my-config.json
```

The PDFs will be downloaded automatically and placed in the correct
folders. If already downloaded, the cached PDFs are reused.

# Usage

```
usage: ghidra-manuals [-h] [--config PATH] [--get-manual-idxs] [--overwrite-config] [--no-cache] ~/ghidra_xx.xx

Get ghidra manuals from the internet and put into your ghidra installation

positional arguments:
  ~/ghidra_xx.xx      Path to ghidra installation

options:
  -h, --help          show this help message and exit
  --config PATH       Path to a config.json to use. Defaults to ./config.json
                      if it exists, otherwise the config.json bundled with
                      this package.
  --get-manual-idxs   Update config.json to include manuals from current ghidra installation
  --overwrite-config  Overwrite config.json with the new manual indexes. This is not typically what you want to do. Will clear current URLs from config.json
  --no-cache          Force download of PDFs. Do not use cached PDFs.
```

## Working on the project locally

If you've cloned the repo and want to hack on it, use `uv` directly:

```
uv run ghidra-manuals ~/ghidra_11.2
```

uv will create the virtualenv and install dependencies for you the first time.

# Notes and Updating config with new manuals

This whole repo is meant to be futureproof. If you initially used this script for a previous version of ghidra, and now want to use it for a newer version, you can simply run:

```
uvx --from git+https://github.com/clouedoc/ghidra-manuals ghidra-manuals \
    <path_to_new_ghidra_dir> --get-manual-idxs
```

This writes a `config.json` into your current working directory (seeded
from the bundled config), which you can then edit and PR back. Use
`--config PATH` if you want to read/write a config at a specific location.

Which should give you one of the following outputs:

```shell
# There was a new processor manual added:
 > ghidra-manuals ~/ghidra_11.2.1 --get-manual-idxs
Updated config with 1 configs.
Manuals info dumped to config.json

Done updating config.json.
```

or

```shell
# No new processor manuals were added:
 > ghidra-manuals ~/ghidra_11.2.1 --get-manual-idxs
Did not update config.json as there were no missing manuals...

Done updating config.json.
```

# Missing Manuals

Currently there are missing manuals for:
 - M16C
  - M16C_60
  - M16C_80

For some reason they are hard to find. If anyone has these please let me know.

Please feel free to open a pull request to add more backup URLs to this project.

## Notes

This project was originally created against ghidra 10.1.2 which had the 6805 processor folder which apparently no longer exists. If you get a warning about missing the 6805 folder, that's why.

