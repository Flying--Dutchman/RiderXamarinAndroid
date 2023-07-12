# Rider Xamarin.Android
This is a step-by-step guide on how to install Xamarin.Android on any Linux distro, using [DistroBox](https://github.com/89luca89/distrobox). <br> <br>
Note: The 'rider' package has been removed in Chaotic-AUR, also, there were some GPG/mirror issues with Chaotic-AUR in the past. Therefore I decided to remove Chaotic-AUR from this tutorial.

# QuickStart

1. Install `DistroBox` and `Podman`/`Docker` using your package manager

2. Create and enter an Arch Linux Box

    2.1. With a custom home folder (recommended)
    ```
    distrobox create -n archriderbox -i archlinux:latest --home ~/distrobox/archriderbox && distrobox enter -nw archriderbox
    ```

    2.2. Without a custom home folder
    ```
    distrobox create -n archriderbox -i archlinux:latest && distrobox enter archriderbox
    ```

3. Install packages (This should take a while... :coffee:)
```
sudo pacman -Sy --needed git base-devel extra/mono-msbuild libxtst fakeroot extra/jdk11-openjdk extra/libxcursor extra/libxcomposite extra/flac extra/lame extra/libasyncns extra/libogg extra/libsndfile extra/libvorbis extra/mpg123 extra/opus extra/libpulse extra/dotnet-sdk-6.0 --noconfirm && \
git clone https://aur.archlinux.org/yay.git && cd yay && makepkg -si --noconfirm && \
yay -S xamarin-android --noconfirm
```

4. Download and extract Rider (or the JetBrains Toolbox)

```
cd ~/ && wget -O rider.zip https://download.jetbrains.com/rider/JetBrains.Rider-2023.1.3.tar.gz && tar -xf rider.zip && rm rider.zip && ln -s JetBrains\ Rider-2023.1.3/ Rider
```

5. Start Rider
```
~/Rider/bin/rider.sh
```

6. Within Rider, download the Android SDK and set the correct paths (Android SDK+NDK and Java)

# How to start Rider
Simply start Rider, from your local shell, with the following command:

```
distrobox enter -nw archriderbox -- Rider/bin/rider.sh
```


# Bonus (Gnome)
You can use [alacarte](https://gitlab.gnome.org/GNOME/alacarte) to easily add Rider to your system menu in Gnome

![image](https://github.com/Flying--Dutchman/RiderXamarinAndroid/assets/9158539/7ff42eca-d74f-4629-90b1-05f6fb56cb08)


# Troubleshooting
## Emulator won't start
Make sure to start your emulator using software rendering. 
Edit your emulator, and set "Graphics" under "Emulated Performance" to "Software - GLES 2.0"
 
## Crashing while debugging
1. `fast deployment` is turned off or log contains `fpctx->head.magic == FPSIMD_MAGIC' not met` <br>
1.1 Add or replace the following line in your Android.csproj file:\
`<AndroidSupportedAbis>x86;x86_64;armeabi-v7a;arm64-v8a</AndroidSupportedAbis>`
