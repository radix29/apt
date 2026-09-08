# radix29 apt repository

A signed APT repository for [radix29](https://github.com/radix29)'s tools,
served over GitHub Pages at **https://radix29.github.io/apt**.

## Install goSSMS

```sh
sudo install -d -m 0755 /etc/apt/keyrings
curl -fsSL https://radix29.github.io/apt/gossms.asc \
  | sudo tee /etc/apt/keyrings/gossms.asc > /dev/null
echo "deb [signed-by=/etc/apt/keyrings/gossms.asc] https://radix29.github.io/apt stable main" \
  | sudo tee /etc/apt/sources.list.d/gossms.list > /dev/null
sudo apt-get update
sudo apt-get install gossms
```

`amd64` and `arm64`. The packages hold a statically linked binary with no
dependencies, so any Debian- or Ubuntu-derived distribution still receiving
security updates should work.

[goSSMS](https://github.com/radix29/gossms) is a portable, cross-platform
terminal reimplementation of SQL Server Management Studio.

## How this repository is maintained

Everything below the root — `pool/`, `dists/` and `gossms.asc` — is
**generated**. The release workflow in `radix29/gossms` builds the `.deb`s from
each tagged release, regenerates the package indices from the whole pool, signs
`Release`, and pushes the result here. Editing those files by hand is pointless;
the next release overwrites them. Change
`.github/workflows/release.yml` in the gossms repo instead.

`.nojekyll` is present because GitHub Pages' Jekyll step would otherwise skip
directories apt needs.
