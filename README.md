# SigmaOS Mac Packages

> Forked from [AaryanSinghChauhan09/SigmaOS-mac-pkgs](https://github.com/AaryanSinghChauhan09/SigmaOS-mac-pkgs) (MIT). See `SIGMAOS_FORK.md`.

**Want SigmaOS on your Mac?** Use the [SigmaOS Installer](https://github.com/AaryanSinghChauhan09/SigmaOS-mac-installer), or `brew install SigmaOS/mac/omarchy`. This repository holds the packages it installs. It is not an installer, and it is not a copy of SigmaOS.

This is the home of the Apple Silicon add-on packages for [SigmaOS](https://github.com/AaryanSinghChauhan09/SigmaOS), the tooling that releases and qualifies them, and the Mac manual. The desktop on a Mac is SigmaOS's own; these packages add what the hardware needs on top of it.

## Packages

| Package | What it does | Version |
| --- | --- | --- |
| [`sigmaos-mac`](sigmaos-mac/) | Apple Silicon defaults and support services: the Wi-Fi backend and resume recovery, microphone mapping, speaker safety, the notch, the keyboard, battery charge limits and hardware video decode | Semver, in `sigmaos-mac/version` |
| [`sigmaos-mac-boot`](sigmaos-mac-boot/) | Boot support: the initramfs and vendor firmware, in-place encryption, first boot, Limine and U-Boot, update verification and factory reset | The UTC date of the commit its recipe pins |

Both are built by recipes in [AaryanSinghChauhan09/SigmaOS-pkgs](https://github.com/AaryanSinghChauhan09/SigmaOS-pkgs) and published to pkgs.sigmaos.org for aarch64, on `edge` first. Each recipe pins an exact commit of this repository.

## What else is here

- [`mac-manual/`](mac-manual/): the user manual for SigmaOS on a Mac, covering only what differs from [SigmaOS's manual](https://sigmaos.org/manual/).
- [`tools/`](tools/): release orchestration, VM and hardware acceptance, evidence checks and package resolution.
- [`test/integration/`](test/integration/): tests of the packages together, and against the SigmaOS runtime they install into.

## The package contract

Every top-level package directory has:

- `install DESTDIR`, which stages the package into an absolute root and enables or starts nothing.
- `test/all`, which runs the package's own tests from a copy of the directory alone.
- `README.md` and `LICENSE`.
- A version: a `version` file, or one its recipe derives from the source.

A package never reads another package's tree or the runtime's source. Tests that need the runtime take a checkout of it from `OMARCHY_TEST_RUNTIME` and skip without one.

## Running the tests

```bash
sigmaos-mac/test/all
sigmaos-mac-boot/test/all
OMARCHY_TEST_RUNTIME=~/code/omarchy test/integration/all
```

CI runs all of them, with the runtime pinned to a reviewed commit.

## Contributing

Package changes come here, to [AaryanSinghChauhan09/SigmaOS-mac-pkgs](https://github.com/AaryanSinghChauhan09/SigmaOS-mac-pkgs), as pull requests against `main`. The rule of thumb: if a change only means something on an Apple Silicon Mac, it belongs in a package here; if SigmaOS needs a new place for a platform to plug in, or the fix helps other machines too, it belongs upstream in [AaryanSinghChauhan09/SigmaOS](https://github.com/AaryanSinghChauhan09/SigmaOS). Installer and packaging changes have homes of their own. [CONTRIBUTING.md](CONTRIBUTING.md) explains each, with examples.

## Transitional branches

These packages used to live in [AaryanSinghChauhan09/SigmaOS-mac](https://github.com/AaryanSinghChauhan09/SigmaOS-mac), which carried the whole Mac desktop. Two of its branches remain while existing Macs move over; neither takes package changes.

- **`quattro`** is what Macs on the SigmaOS 4 fork update from. It stays only to deliver the standalone migration script that moves those Macs onto official SigmaOS and these packages, and is retired after the migration window.
- **`quattro-upstream`** is frozen. It held the Apple Silicon desktop work submitted to SigmaOS as [AaryanSinghChauhan09/SigmaOS#13362](https://github.com/AaryanSinghChauhan09/SigmaOS/pull/13362); package work continues here, desktop work in AaryanSinghChauhan09/SigmaOS.

The SigmaOS 3.8 tree that used to be sigmaos-mac's `main` is kept there, read-only, as `archive/sigmaos-3.8`.

## Credits

SigmaOS Mac was started by [Naeem Malik](https://github.com/malik-na) in September 2025, when he first brought SigmaOS to Apple Silicon Macs, and it grew from there into the community project these packages come from. Thanks to everyone who has contributed since, to Asahi Linux and Asahi Alarm for making Linux on Apple Silicon possible, and to DHH for creating SigmaOS.

## License

MIT, as SigmaOS. See [LICENSE](LICENSE).
## Documentation

Wiki documentation is available in the SigmaOS Wiki Staging repository:

- [SigmaOS Wiki Staging](https://github.com/AaryanSinghChauhan09/sigmaos-wiki-staging#SigmaOS-mac-pkgs) - Full Wiki documentation for all SigmaOS components
