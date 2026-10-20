# imprint-data-template

An example data repo for imprint. Fork it, or point imprint at your own with imprint data use owner/repo.

## What is here

- `setups/`: one TOML file per setup, named `<purpose>[-<variant>]` after what the system is for.
  `example.toml` is Arch with i3 and a few apps.
- `catalog/`: your own catalog entries, which replace the catalog's entry with the same `id`.
- `tags/`: your own tags.
- `dotfiles/<window manager>/`: the configuration copied into the user's home.
- `hooks/`: shell scripts a setup runs at one stage of building or installing a system.
  `example.sh` only prints what it was given; `example.toml` runs it at the first boot.

A setup may `extends` another setup of this repo. Secrets never go here: Wi-Fi passwords and
Tailscale keys stay in the stick's `personal/` folder.

## Hooks

A setup lists its hooks by stage, each a script path inside this repo:

    [[hooks]]
    stage  = "firstboot"   # build | install | firstboot | session
    script = "hooks/example.sh"

`build` runs while the image is built, `install` in the new system as root, `firstboot` once as
root after the network is up on the first boot (again on the next boot if a hook failed, so make
it safe to run twice), `session` at the user's first login. A setup's hooks run after those of
the setup it `extends`. Each script runs with `sh` and gets `IMPRINT_SETUP` (the resolved setup
as a JSON file), `IMPRINT_DATA` (this repo), `IMPRINT_PERSONAL` (the stick's `personal/` folder)
and `IMPRINT_STAGE`. Try one with `imprint hooks run firstboot example`.

Today `imprint hooks install-firstboot` sets up the firstboot stage in an installed system, and
`imprint hooks run` runs any stage by hand; the image build and the installer will run the other
stages themselves once they are ported to imprint.
