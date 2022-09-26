# Rider Xamarin.Android
This is a step-by-step guide on how to install Xamarin.Android on your Linux system.

<br><br>
This guide has initially been written for Manjaro Linux, as I am now moving to Fedora I noticed missing, incomplete or outdated mono packages.
I will update this README accordingly.

@Fedora users: 
- Do not use the standard packages from Gnome-Software or dnf
- Use the official steps from the mono project and stick to the preview package: https://www.mono-project.com/download/preview/#download-lin-fedora
- Not tested, but you should be able to install the .deb package (step 2) using dpkg


# 1. Prerequisites
Install following packages with your package manager:

1. mono
2. dotnet SDK (Probably .NET Core 3.1)
3. Java SDK
4. Android Studio

# 2. Xamarin.Android package

1. Download the current release of Xamarin.Android from the build server: 
https://dev.azure.com/xamarin/public/_build?definitionId=48&_a=summary
2. Pick one where both stages were successfull and click on it.
3. In the "Summary" box, check for "Related" and click on "n published" below it.
4. Download the "installers-unsigned - Linux" (Using the 3 dots menu on the far right)
5. Unzip the downloaded file.
6. If possible install using your package manager. <br>
6.1 **Arch Linux users**: You can install the .deb package using "debtap"<br>
6.2 debtap -U < deb_file ><br>
6.3 When asked to edit the .PGKINFO file, do so with your favourite editor and remove any invalid, or not needed dependency. (In my case I removed c, c0 and java8-sdk)<br>
6.4 Install the created *.zst file
7. **If no package manager is available** (not recommended):<br>
7.1 Unzip the .deb file and unzip the containing data file. <br>
7.2 Copy all the files to their respective folder on your drive.

# 3. Android Studio
1. Open Android Studio
2. Click on "More actions" --> SDK Manager
3. Under "SDK Platforms" install the desired API-levels.
4. Under "SDK Tools" make sure that the following are installed:<br>
4.1 Android SDK Build-Tools<br>
4.2 NDK (Side by side)<br>
4.3 Android SDK Command-line Tools<br>
4.4 CMake<br>
4.5 Android Emulator<br>
4.6 Android SDK Platform-Tools

# 4. Rider
1. In your Rider settings, search for "Android" and set the following fields (should be under "Build, Execution, Deployment" --> "Android"):<br>
1.1 Android SDK Location (e.g. /home/user/Android/Sdk)<br>
1.2 Android NDK Location (e.g. /home/user/Android/Sdk/ndk/< version >)<br>
1.3 Java Development Kit Location (e.g. /usr/lib/jvm/java-11-adoptopenjdk)
2. Also check your mono and dotnet settings, search for "Mono" (should be under "Build, Execution, Deployment" --> "Toolset and Build".

# Troubleshooting
## Crashing while debugging
1. `fast deployment` is turned off or log contains `fpctx->head.magic == FPSIMD_MAGIC' not met` <br>
1.1 Add or replace the following line in your Android.csproj file:\
`<AndroidSupportedAbis>x86;x86_64;armeabi-v7a;arm64-v8a</AndroidSupportedAbis>`
