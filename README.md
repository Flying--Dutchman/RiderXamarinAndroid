# Rider Xamarin.Android
This is a step-by-step guide on how to install Xamarin.Android on any Linux distro, using [DistroBox](https://github.com/89luca89/distrobox).

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
sudo pacman -Sy chaotic-aur/yay community/mono-msbuild libxtst chaotic-aur/android-studio fakeroot extra/jdk11-openjdk community/dotnet-sdk-6.0 chaotic-aur/rider --noconfirm && yay -S xamarin-android --noconfirm
```

5. Within Rider, download the Android SDK and set the correct paths (Android SDK+NDK and Java)

# How to start Rider
Simply start Rider, from your local shell, with the following command:

```
distrobox enter archriderbox -- rider
```


# Bonus (Gnome)
You can use [alacarte](https://gitlab.gnome.org/GNOME/alacarte) to easily add Rider to your system menu in Gnome

![image](https://user-images.githubusercontent.com/56829222/226169688-d0f696fc-2272-45d0-aa9e-66df4981dafe.png)

# Troubleshooting
## Crashing while debugging
1. `fast deployment` is turned off or log contains `fpctx->head.magic == FPSIMD_MAGIC' not met` <br>
1.1 Add or replace the following line in your Android.csproj file:\
`<AndroidSupportedAbis>x86;x86_64;armeabi-v7a;arm64-v8a</AndroidSupportedAbis>`
