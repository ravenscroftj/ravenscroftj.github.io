---
id: eqs6w1shat0vy43cvftohxx
title: Rockstar Launcher
desc: ''
updated: 1673805181919
created: 1673805096847
---

The following instructions for running Rockstar Launcher on SteamDeck/Proton are taken from [this post](https://www.reddit.com/r/SteamDeck/comments/xhoy9l/red_dead_redemption_2_rockstar_launcher_version/):

-   Download the Rockstar Launcher exe from the official website.
-   Add the exe as a non-steam game, change compatability to GE-Proton7-33.
-   Run the exe through Steam, it should install.
-   Now go into the file explorer on your deck, and navigate to your Steam compatdata folder: `/home/deck/.local/share/Steam/steamapps/compatdata`
-   Find the folder that has been modified most recently, it will be a random number. You need to find the **launcher.exe** that has jsut been installed. For reference, mine was in: `/home/deck/.local/share/Steam/steamapps/compatdata/4155815133/pfx/drive_c/Program Files/Rockstar Games/Launcher/launcher.exe`
-   Once you find the launcher.exe, you need to go into Steam, and change the non-steam shortcut that you previously made for the installer, to the new launcher.exe. **DO NOT ADD A NEW SHORTCUT!** Right click on the existing shortcut, go to properties and click browse....then navigate to the **launcher.exe** you have just found and select it.
-   Now run the shortcut through Steam, and wait a few seconds. It may seem like nothing is happening but the Rockstar Launcher should load eventually.
-   Login, and then install RDR2 through the launcher. Don't change any settings, keep everything in the installer default.
-   Once downloaded and installed, run the game. You'll get an Error 18 message so exit out of the game.
-   Go back to your compatdata folder, and there should be an RDR2 folder with the Rockstar Launcher folder.
-   ~Now in the RDR2 folder, you need to find~ **~VulkanRT-1.1.108.0-Installer.exe~** ~in the Redistributables folder: /home/deck/.local/share/Steam/steamapps/compatdata/4155815133/pfx/drive\_c/Program Files/Rockstar Games/Red Dead Redemption 2/Redistributables~
-   ~Once again, go into Steam and~ **~CHANGE~** ~the shortcut to~ **~VulkanRT-1.1.108.0-Installer.exe.~**
-   ~Run the shortcut again, install the program with the default settings.~
-   Once installed, you **CHANGE** the Steam shortcut for the final time to **RDR2.exe:** `/home/deck/.local/share/Steam/steamapps/compatdata/4155815133/pfx/drive_c/Program Files/Rockstar Games/Red Dead Redemption 2/RDR2.exe`
-   To fix the Error 18 message, add the following command to the launch options for the shortcut: `WINEDLLOVERRIDES=vulkan-1=n,b %command%`
-   Finally, navigate back into your compatdata folder, and find **system.xml (**you have to run the game at least once to generate this file)**:** `/home/deck/.local/share/Steam/steamapps/compatdata/4155815133/pfx/drive_c/users/steamuser/Documents/Rockstar Games/Red Dead Redemption 2/Settings/system.xml`
-   Open it with KWrite and change the line `<API>kSettingAPI_DX12</API>` to `<API>kSettingAPI_Vulkan</API>`
-   DONE. You should now have a fully working RDR2 installation. I didn't need to change many graphics settings in-game, just disable vsync and enable FSR 2.0 and you should be good to go. Enjoy!