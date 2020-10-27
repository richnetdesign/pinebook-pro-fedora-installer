# pinebook-pro-fedora-installer

Scripts for installing Fedora aarch64 directly to SD/eMMC. The script will add copr repository for some extra packages needed on Pinebook Pro.<BR> copr: https://copr.fedorainfracloud.org/coprs/aptupdate/pinebook-pro/ source: https://github.com/bengtfredh/pinebook-pro-copr.git

Script will install kernel-pbp from copr which is a vanilla kernel patched for Pinebook Pro with Manjaro config merged on Fedora config. You can chose to switch to linux-manjaro from same copr which is a rpm packages Manjaro aarch64 kernel. Biggest difference is kernel-pbp have SELINUX and btrfs build in kernel, linux-manjaro have no SELINUX and have btrfs as module.

This script is "interactive". Meaning that it asks you questions when run to customize your install. Like username, password etc.

Runtime is approx 40-50 minutes for Fedora 33 Workstation depending on your bandwidth and SD card speed. Fedora update is what takes longest time.

## Dependencies:

* systemd-container (systemd-nspawn)
* bash
* wget
* rsync
* git
* systemd
* dialog
* libarchive
* qemu-user-static (archlinux: binfmt-qemu-static)
* openssl
* gawk
* dosfstools
* polkit
* btrfs-progs

## Installing and using from gitlab:

To use this script, please make sure that the following is correct:

* Some Fedora mirrors are slow. Add url to Fedora-Workstation-33-1.2.aarch64.raw.xz as parameter for different mirror, i.e:

  ```
  ./fedora-installer http://mirror.fedoraproject.org/pub/fedora/linux/releases/33/Workstation/aarch64/images/Fedora-Workstation-33-1.2.aarch64.raw.xz
  
  ```
* an **empty** SD/eMMC card with at least 16 GB storage is plugged in, but not mounted.
* Nothing is mounted on /dev/loop0
* that your user account has `sudo` rights.

Then use this to get it:

```
git clone https://github.com/bengtfredh/pinebook-pro-fedora-installer
cd pinebook-pro-fedora-installer
chmod +x fedora-installer
sudo bash ./fedora-installer
```

## Known Issues:

* Because `dialog` is weird, the script needs to be run in `bash`.
* First boot can take som time for SELINUX autorelabel to run.

## Things to do/improve

* [x] ~~Use Fedora kernel - default kernel will not boot - maybe build custom.~~ https://github.com/bengtfredh/pinebook-pro-copr/kernel-pbp/
* [x] ~~Get sound to work better, can only get low volume - change setting in overlay~~
* [x] ~~Change disk layout - I guess @daniel-thompson have a more sane layout~~
* [x] ~~Add support for update-uboot - need overlays for script~~
* [x] ~~Test update-uboot~~
* [x] ~~Create kernel upgrade script~~
* [ ] Add u-boot gfx - I have been testing this and it is too buggy by now. I like https://github.com/pcm720/u-boot-build-scripts/releases.
* [x] ~~Change disklayout and filesystem to btrfs.~~
* [ ] Change source to smaller image (container.tar.zx) and dnf an installation.
* [x] ~~Create copr repo and replace overlay and Manjaro part of the script~~ https://github.com/bengtfredh/pinebook-pro-copr

## Supported Devices:

* Pinebook Pro

## Supported Editions / Desktops:

* Fedora Workstation<BR>

  <BR> There is no reason why this script should not work with other editions of Fedora. Just change FEDORAURL and FEDORARAW. Script os only tested with Fedora Workstation.

## Other notes:

This script **should** be distro-agnostic, which means you can install *pinebook-pro-fedora-installer* from **any** distro, as long as the dependencies are met.

## Credits

Inspiration and code parts from:<BR> https://gitlab.manjaro.org/manjaro-arm/applications/manjaro-arm-installer<BR> https://github.com/nikhiljha/pp-fedora-sdsetup<BR> https://github.com/daniel-thompson/pinebook-pro-debian-installer.git
