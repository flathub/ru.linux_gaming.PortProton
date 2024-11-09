<div align="center">
  <img src="https://raw.githubusercontent.com/Castro-Fidel/PortWINE/master/data_from_portwine/img/gui/portproton.svg" width="64">
  <h1 align="center">PortProton on Flatpak</h1>
  <p align="center">Project designed to make it easy and convenient to run Windows games on Linux for both beginners and advanced users.
The project strives to make launching games (and other software) as simple as possible, but at the same time provides flexible settings for advanced users.</p>
</div>

## 💻 Installation

   ```sh
   flatpak install flathub ru.linux_gaming.PortProton
   ```

## ⏰ Running
Launch PortProton from your desktop menu, or via command line:
```
flatpak run ru.linux_gaming.PortProton
```

## 🔨 Building

To compile PortProton as a Flatpak, you'll need both [Flatpak](https://flatpak.org/) and [Flatpak Builder](http://docs.flatpak.org/en/latest/flatpak-builder.html) installed. Once you manage that, do the following...

0. Clone this repository and `cd` into it
1. Add the git submodules
   ```sh
   git submodule init
   git submodule update
   ```
2. Compile the flatpak
   ```sh
   flatpak-builder --repo=portproton --force-clean --install-deps-from=flathub build-dir ru.linux_gaming.PortProton.yml
   ```
3. Add the local repo and install the flatpak
   ```sh
   flatpak remote-add portproton portproton --no-gpg-verify
   flatpak install portproton ru.linux_gaming.PortProton
   ```

## 📋 FAQ

- PortProton cannot detect my MangoHud config if I used MANGOHUD_USER_CONF

   Add the adequate filesystem override
   ``` sh
   flatpak override --user --filesystem=xdg-config/MangoHud:ro ru.linux_gaming.PortProton
   ```

- What tarball downloaded in startup

   During the first run of PortProton the file PortWINE-master.tar.gz is downloaded, these are just scripts that are downloaded from gitlab or github, more details in [upstream](https://github.com/Castro-Fidel/PortProton_ALT/blob/main/portproton).

- Building custom wine version used in PortProton from source code

   All sources as well as tools for building custom versions of Wine (Wine LG) and Proton (Proton LG) used in PortProton can be found in the [wine buillds](https://github.com/Castro-Fidel/wine_builds) repository.

- What to do if PortProton does not follow the system theme

  ```sh
  flatpak override --user --filesystem=xdg-config/gtk-3.0 ru.linux_gaming.PortProton
  flatpak override --user --env=GTK_THEME=$(gsettings get org.gnome.desktop.interface gtk-theme | tr -d "'") ru.linux_gaming.PortProton
  ```
