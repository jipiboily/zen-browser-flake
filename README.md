# Zen Browser

This is a flake for the Zen browser.

Just add it to your NixOS `flake.nix` or home-manager:

```nix
inputs = {
  zen-browser.url = "github:MarceColl/zen-browser-flake";
  ...
}
```

## Packages

This flake exposes only one package, corresponding to the `specific` zen versions.
The `specific` one targets newer CPUs and kernels but it may not work in your case.

The `default` package is the `specific` one for backwards compatibility with older versions of the flake.

Then in the `configuration.nix` in the `environment.systemPackages` add one of:

```nix
inputs.zen-browser.packages."${system}".specific
```

Depending on which version you want

```shell
$ sudo nixos-rebuild switch
$ zen
```

## 1Password

Zen has to be manually added to the list of browsers that 1Password will communicate with. See [this wiki article](https://nixos.wiki/wiki/1Password) for more information. To enable 1Password integration, you need to add the line `.zen-wrapped` to the file `/etc/1password/custom_allowed_browsers`.

## Maintenance

To update the Zen version of this flake, do the following:

- go to the releases -> https://github.com/zen-browser/desktop/releases
- download the linux specific version
- extract the archive
- run this: `nix-hash --type sha256 --base32 ~/Downloads/zen.linux-specific/zen/`
- take the sha and update it in `flake.nix`
- update the browser version in the `flake.nix`
- you're done!

To test locally, use this as the input: `zen-browser.url = "path:/path-to-this-repo-on-your-computer";`
