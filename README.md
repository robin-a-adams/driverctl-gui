# driverctl-gui

A small GTK front-end for [`driverctl`](https://gitlab.com/driverctl/driverctl).
It lists PCI and USB devices with their current driver, shows which have an
override set, and lets you set, clear, or load a driver override. Privileged
actions run through `pkexec`, so the application itself does not run as root.

It lets you choose which driver binds to a device, persistently across
reboots, without editing configuration files by hand. A common use is binding
a device to `vfio-pci` for virtual-machine passthrough.

## Usage

Launch **driverctl GUI** from the applications menu, or run `driverctl-gui`.

- **Bus** selects the device bus to manage (`pci` or `usb`).
- **Search** filters the device list across all columns.
- Select a device, choose a driver, and click **Set Override**. The driver
  field completes from the drivers available on the selected bus; click it to
  see the list, or tick **Show all drivers** to include every installed
  module.
- **Unset Override** removes an override; **Load Override** applies one that is
  saved but not yet active.
- **Apply now** rebinds immediately; leave it unchecked to save the override
  for the next boot instead. **Persistent** keeps the override across reboots.
- The **Override** column shows whether an override is `active`, `persisted`,
  or both.
- The toolbar terminal button reveals a panel with the exact commands run and
  their output.

Overrides are `driverctl`'s own persistent mechanism, so they survive reboots.

## Dependencies

Installed automatically by `apt`:

- `python3`, `python3-gi`, `gir1.2-gtk-3.0` — the GTK 3 runtime.
- `driverctl` — the underlying utility.
- `pciutils` — provides `lspci` for PCI device descriptions.
- `usbutils` — provides `lsusb` for USB device descriptions.
- `pkexec` — for privileged actions.

## Install

Download the `.deb` from the [latest release][releases] and install it with
`apt` so its dependencies are resolved:

```sh
sudo apt install ./driverctl-gui_*.deb
```

[releases]: https://github.com/robin-a-adams/driverctl-gui/releases/latest

## Build

Install the build dependencies, then build:

```sh
sudo apt build-dep ./
dpkg-buildpackage -us -uc -b
```

This produces `../driverctl-gui_<version>_all.deb`.

## License

MIT. See `debian/copyright`.
