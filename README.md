# seafoam &nbsp; [![bluebuild build badge](https://github.com/bit-of-a-git/seafoam/actions/workflows/build.yml/badge.svg)](https://github.com/bit-of-a-git/seafoam/actions/workflows/build.yml)

Seafoam is an experimental Linux distro which uses BlueBuild to create a custom image based on Universal Blue.

## Why

I tried out several distros before landing on Aurora, a general-purpose uBlue distro. I can do almost everything I want with the tools provided in Aurora, but occasionally encounter things I cannot do - or at least would require a lot of time investigating, which I don't always have. I currently intend to use Seafoam to experiment with things like:
- Nix and Nix Home Manager
- KDE extensions
- Packages that are not easily available through Flatpaks, Brew, or Distrobox

## Installation

> [!WARNING]  
> [This is an experimental feature](https://www.fedoraproject.org/wiki/Changes/OstreeNativeContainerStable), try at your own discretion.

To rebase an existing atomic Fedora installation to the latest build:

- First rebase to the unsigned image, to get the proper signing keys and policies installed:
  ```
  rpm-ostree rebase ostree-unverified-registry:ghcr.io/bit-of-a-git/seafoam:latest
  ```
- Reboot to complete the rebase:
  ```
  systemctl reboot
  ```
- Then rebase to the signed image, like so:
  ```
  rpm-ostree rebase ostree-image-signed:docker://ghcr.io/bit-of-a-git/seafoam:latest
  ```
- Reboot again to complete the installation
  ```
  systemctl reboot
  ```

The `latest` tag will automatically point to the latest build. That build will still always use the Fedora version specified in `recipe.yml`, so you won't get accidentally updated to the next major version.

## ISO

If build on Fedora Atomic, you can generate an offline ISO with the instructions available [here](https://blue-build.org/how-to/generate-iso/#_top). These ISOs cannot unfortunately be distributed on GitHub for free due to large sizes, so for public projects something else has to be used for hosting.

## Verification

These images are signed with [Sigstore](https://www.sigstore.dev/)'s [cosign](https://github.com/sigstore/cosign). You can verify the signature by downloading the `cosign.pub` file from this repo and running the following command:

```bash
cosign verify --key cosign.pub ghcr.io/bit-of-a-git/seafoam
```
