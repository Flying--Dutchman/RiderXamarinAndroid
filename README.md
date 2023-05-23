# Rider Xamarin.Android
This is a step-by-step guide on how to install Xamarin.Android on any Linux distro, using [DistroBox](https://github.com/89luca89/distrobox).
Note: The 'rider' package has been removed in Chaotic-AUR, therefore we will be installing the 'JetBrains Toolbox' for easier update management. Be sure to quit any local installation of JetBrains Toolbox before following this guide.

# QuickStart

1. Install `DistroBox` and `Podman`/`Docker` using your package manager

2. Create and enter an Arch Linux Box
```
distrobox create -n archriderbox -i archlinux:latest && distrobox enter archriderbox
```

3. Add Chaotic AUR
```
sudo -- sh -c "sudo pacman-key --init && sudo pacman-key --recv-key FBA220DFC880C036 --keyserver keyserver.ubuntu.com && sudo pacman-key --lsign-key FBA220DFC880C036 && sudo pacman --noconfirm -U 'https://cdn-mirror.chaotic.cx/chaotic-aur/chaotic-keyring.pkg.tar.zst' 'https://cdn-mirror.chaotic.cx/chaotic-aur/chaotic-mirrorlist.pkg.tar.zst' && { sudo echo '[chaotic-aur]' ; sudo echo 'Include = /etc/pacman.d/chaotic-mirrorlist'; } >>/etc/pacman.conf"
```

4. Install packages
```
sudo pacman -Sy chaotic-aur/yay extra/mono-msbuild libxtst fakeroot extra/jdk11-openjdk extra/libxcursor extra/libxcomposite extra/flac extra/lame extra/libasyncns extra/libogg extra/libsndfile extra/libvorbis extra/mpg123 extra/opus extra/libpulse extra/dotnet-sdk-6.0 chaotic-aur/jetbrains-toolbox --noconfirm && yay -S xamarin-android --noconfirm
```

5. Start JetBrains Toolbox and install Rider. The toobox may display locally installed IDE's, this is normal.
```
jetbrains-toolbox
```

6. Start Rider
```
rider
```

7. Within Rider, download the Android SDK and set the correct paths (Android SDK+NDK and Java)

# How to start Rider
Simply start Rider, from your local shell, with the following command:

```
distrobox enter archriderbox -- rider
```


# Bonus (Gnome)
You can use [alacarte](https://gitlab.gnome.org/GNOME/alacarte) to easily add Rider to your system menu in Gnome

![image](https://user-images.githubusercontent.com/56829222/226169688-d0f696fc-2272-45d0-aa9e-66df4981dafe.png)

# Troubleshooting
## Emulator won't start
Make sure to start your emulator using software rendering. 
Edit your emulator, and set "Graphics" under "Emulated Performance" to "Software - GLES 2.0"
 
## Crashing while debugging
1. `fast deployment` is turned off or log contains `fpctx->head.magic == FPSIMD_MAGIC' not met` <br>
1.1 Add or replace the following line in your Android.csproj file:\
`<AndroidSupportedAbis>x86;x86_64;armeabi-v7a;arm64-v8a</AndroidSupportedAbis>`
