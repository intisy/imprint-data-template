## What is here

- `setups/`: one TOML file per setup, named `<purpose>[-<variant>]` after what the system is for.
  `example.toml` is Arch with i3 and a few apps.
- `catalog/`: your own catalog entries, which replace the catalog's entry with the same `id`.
- `tags/`: your own tags.
- `dotfiles/<window manager>/`: the configuration copied into the user's home.

A setup may `extends` another setup of this repo. Secrets never go here: Wi-Fi passwords and
Tailscale keys stay in the stick's `personal/` folder.
