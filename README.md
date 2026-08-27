# driverctl-gui

A small GTK front-end for [`driverctl`](https://gitlab.com/driverctl/driverctl).
It lists PCI devices with their current driver, shows which have an override
set, and lets you set or clear a driver override. Privileged actions run
through `pkexec`, so the application itself does not run as root.

It lets you choose which driver binds to a device, persistently across
reboots, without editing configuration files by hand.

## Usage

Launch **driverctl GUI** from the applications menu, or run `driverctl-gui`.

- Select a device in the list.
- To bind it to a driver, type the driver name and click **Set Override**.
  You will be prompted for authentication.
- To restore the default driver, select the device and click **Unset
  Override**.
- **Refresh** re-reads the device list.

An override set here is persistent across reboots (this is `driverctl`'s
own behaviour).

## Dependencies

Installed automatically by `apt`:

- `python3`, `python3-gi`, `gir1.2-gtk-3.0` — the GTK 3 runtime.
- `driverctl` — the underlying utility.
- `pciutils` — provides `lspci` for PCI device descriptions.
- `usbutils` — provides `lsusb` for USB device descriptions.
- `pkexec` — for privileged actions.

## Build

Install the build dependencies, then build:

```sh
sudo apt build-dep ./
dpkg-buildpackage -us -uc -b
```

This produces `../driverctl-gui_<version>_all.deb`.

## Install

Install the built package with `apt` so its dependencies are resolved:

```sh
sudo apt install ./driverctl-gui_0.1.0-1_all.deb
```

## License

MIT. See `debian/copyright`.
