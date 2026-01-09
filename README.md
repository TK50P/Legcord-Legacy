
![Legcord](https://github.com/user-attachments/assets/f7b007d4-44fa-4c88-96e4-0a448b568b5d)

> [!CAUTION]
> Usage of unofficial or ported clients is not guaranteed to function as intended. Future updates may break certain features or cause unexpected behavior.
>
> **Don’t be stupid** — do **not** open issues or contact Legcord support. These clients are not supported or affiliated with **the official Legcord** in any way.
>
> **Use at your own risk.**

# Features

- **Standalone client**

   Legcord is built as a standalone client and doesn't rely on the original Discord client in any way.

- **Various mods built-in**

   Enjoy [Vencord](https://github.com/Vendicated/Vencord), [Equicord](https://github.com/Equicord/Equicord), [Shelter](https://github.com/uwu/shelter) and their many features, or have a more vanilla experience, it's your choice!

- **Themes**

   Legcord natively supports theming of the entire app, you can easily import BetterDiscord themes and manage them

- **Made for Privacy™**

   Legcord automatically blocks all of Discord's trackers; even without any client mods, you can feel safe and secure!

- **Supports Rich Presence**

   Unlike other clients, Legcord supports rich presence (game activity) out of the box thanks to [arRPC](https://arrpc.openasar.dev).

- **Mobile support**

   Legcord has **experimental** mobile support for phones running Linux such as the PinePhone. While this is still far from an ideal solution, we're slowly trying to improve it.

- **Much more stable**

   Legcord is using a newer build of Electron than the stock Discord app. This means you can have a much more stable and secure experience, along with slightly better performance.

- **Cross-platform support!**

   Legcord was originally created for AArch64 Linux devices since Discord doesn't support them. We soon decided to support every platform that [Electron supports](https://github.com/electron/electron#platform-support)!

- **_NT 6.x Support!!!_**

   Legcord-Legacy is designed to run on Legacy Windows Systems like 32Bit Windows or Windows NT 6.x (Vista _with [Extended Kernel](https://win32subsystem.live/extended-kernel/)_ Windows 7 and 8, 8.1) Support.

- **_macOS Catalina 10.15 Support!!!_**

   Legcord-Legacy is designed to run on Legacy macOS, currently supports macOS Catalina (10.15).
<img width="1920" height="1080" alt="Windows Vista-2025-11-22-12-12-01" src="https://github.com/user-attachments/assets/8c04c57f-fb05-4ed3-a0ef-1cb85a20795e" />
<img width="1920" height="1080" alt="Windows_7_Main-2025-11-01-19-28-27" src="https://github.com/user-attachments/assets/c4cf9e07-55b4-4497-b7c2-5765b46b2933" />
  
# How to run/install it?

### Windows
Get the .exe installer from Releases.

### macOS
Get the .dmg installer from Releases.

### Pre-built binaries

 Check the **[releases tab](https://github.com/TK50P/Legcord-Legacy/releases)** for precompiled packages for Windows, and macOS.

### Compiling

 Alternatively, you can run Legcord from source ([NodeJS](https://nodejs.dev) and [pnpm](https://pnpm.io/installation#using-npm)) are required:

### For Windows
You need to have the following dependencies installed:

You’ll also need the following this file:  
- [Modified Electron](https://github.com/e3kskoy7wqk/Electron-for-windows-7) (Thanks to [@e3kskoy7wqk](https://github.com/e3kskoy7wqk))

First, fork repository with `git clone https://github.com/Legcord/Legcord`

Place the unpacked `dist-(x86).zip` in `local_electron`, rename to `electron-v37.2.2-win32-x64` for 64-Bit, and `electron-v37.2.2-win32-ia32` for 32-Bit.

Inside this folder, you **must** include the files:  
- `electron-v37.2.2-win32-x64` (for 64-Bit)
- `electron-v37.2.2-win32-ia32` (for 32-Bit)

Now open `package.json`. Replace `pnpm build:plugins && pnpm run build && electron --trace-warnings --ozone-platform-hint=auto ./ts-out/main.js` with `pnpm build:plugins && pnpm run build && local_electron\\electron-v37.2.2-win32-x64\\electron --trace-warnings --ozone-platform-hint=auto ./ts-out/main.js`. <br>
In `"devDependencies"` section, replace `"electron"`'s version (e.g. `"^37.2.2"` with `"file:./local_electron"`). 

Now, add this section.
```js
    "build": {
      "electronDist": "./local_electron/electron-v37.2.2-win32-x64",
      "electronVersion": "37.2.2"
    },
```
> [!NOTE]
> You must change `x64` to `ia32` if you are targetting to 32Bit.

For Example, if code is like this,
```js
    "scripts": {
        "build:dev": "rollup -c --environment BUILD:dev && tsx scripts/copyVenmic.mts",
        "build:plugins": "lune ci --repoSubDir src/shelter --to ts-out/plugins",
        "build": "pnpm build:plugins && rolldown -c rolldown.config.js && tsx scripts/copyVenmic.mts",
        "start": "node scripts/electron.cjs .",
        "startThemeManager": "pnpm run build:dev && electron ./ts-out/main.js themes",
        "package": "pnpm run build && electron-builder",
        "packageQuick": "pnpm run build && electron-builder --dir",
        "lint": "biome check",
        "lint:fix": "biome check --write",
        "postinstall": "electron-builder install-app-deps",
        "CIbuild": "pnpm run build && electron-builder --linux zip && electron-builder --windows zip && electron-builder --macos zip",
        "updateMeta": "tsx scripts/utils/updateMeta.mts"
    },
    "repository": {
        "type": "git",
        "url": "git+https://github.com/Legcord/Legcord.git"
    },
```

Place like this.
```js
    "scripts": {
        "build:dev": "rollup -c --environment BUILD:dev && tsx scripts/copyVenmic.mts",
        "build:plugins": "lune ci --repoSubDir src/shelter --to ts-out/plugins",
        "build": "pnpm build:plugins && rolldown -c rolldown.config.js && tsx scripts/copyVenmic.mts",
        "start": "node scripts/electron.cjs .",
        "startThemeManager": "pnpm run build:dev && electron ./ts-out/main.js themes",
        "package": "pnpm run build && electron-builder",
        "packageQuick": "pnpm run build && electron-builder --dir",
        "lint": "biome check",
        "lint:fix": "biome check --write",
        "postinstall": "electron-builder install-app-deps",
        "CIbuild": "pnpm run build && electron-builder --linux zip && electron-builder --windows zip && electron-builder --macos zip",
        "updateMeta": "tsx scripts/utils/updateMeta.mts"
    },
    "build": {
      "electronDist": "./local_electron/electron-v37.2.2-win32-x64",
      "electronVersion": "37.2.2"
    },
    "repository": {
        "type": "git",
        "url": "git+https://github.com/Legcord/Legcord.git"
    },
```

Now, run this.

```sh
# Set architecture FIRST to build 32-bit (ia32) target
set npm_config_arch=ia32

# Install Dependencies
pnpm i

# Start the program
pnpm start

# Or package it for Windows
pnpm package

# For 32Bit Windows
pnpm exec electron-builder --win --ia32

```

## For macOS Catalina (10.15)  
> [!NOTE]  
> Since macOS Catalina only supports Intel Macs, so building with universal binary is pointless.
> 
> You can replace `universal` with `x64` to build Intel Macs (x64 binaries) only.

Open `package.json` and add this.
```js
"build": {
  "mac": {
    "minimumSystemVersion": "10.15.0",
    "target": [
      {
        "target": "dmg",
        "arch": ["x64"]
      }
    ]
  }
}
```
For Example, if code is like this,
```js
{
  "scripts": {
    "build:dev": "rollup -c --environment BUILD:dev && tsx scripts/copyVenmic.mts",
    "build:plugins": "lune ci --repoSubDir src/shelter --to ts-out/plugins",
    "build": "pnpm build:plugins && rolldown -c rolldown.config.js && tsx scripts/copyVenmic.mts",
    "start": "node scripts/electron.cjs .",
    "startThemeManager": "pnpm run build:dev && electron ./ts-out/main.js themes",
    "package": "pnpm run build && electron-builder",
    "packageQuick": "pnpm run build && electron-builder --dir",
    "lint": "biome check",
    "lint:fix": "biome check --write",
    "postinstall": "electron-builder install-app-deps",
    "CIbuild": "pnpm run build && electron-builder --linux zip && electron-builder --windows zip && electron-builder --macos zip",
    "updateMeta": "tsx scripts/utils/updateMeta.mts"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/Legcord/Legcord.git"
  }
}
```

Place like this.
```js
    "scripts": {
        "build:dev": "rollup -c --environment BUILD:dev && tsx scripts/copyVenmic.mts",
        "build:plugins": "lune ci --repoSubDir src/shelter --to ts-out/plugins",
        "build": "pnpm build:plugins && rolldown -c rolldown.config.js && tsx scripts/copyVenmic.mts",
        "start": "node scripts/electron.cjs .",
        "startThemeManager": "pnpm run build:dev && electron ./ts-out/main.js themes",
        "package": "pnpm run build && electron-builder",
        "packageQuick": "pnpm run build && electron-builder --dir",
        "lint": "biome check",
        "lint:fix": "biome check --write",
        "postinstall": "electron-builder install-app-deps",
        "CIbuild": "pnpm run build && electron-builder --linux zip && electron-builder --windows zip && electron-builder --macos zip",
        "updateMeta": "tsx scripts/utils/updateMeta.mts"
    },
    "build": {
      "mac": {
        "minimumSystemVersion": "10.15.0",
        "target": [
          {
            "target": "dmg",
            "arch": ["x64"]
          }
        ]
      }
    },
    "repository": {
        "type": "git",
        "url": "git+https://github.com/Legcord/Legcord.git"
    },
```

Simply downgrade the Electron version as follows:

```sh
# Install dependencies
pnpm i

# Downgrade Electron to v32 (last version supported on Catalina, based on Chromium 128)
pnpm i -f electron@32

# Package the app
pnpm package
```

# FAQ

## Do you have a support Discord?

- Since this is fork of Legcord, it's not guranteed to get supported using these legacy forks.

## Will I get banned for using this?

- You are breaking [Discord ToS](https://discord.com/terms#software-in-discord%E2%80%99s-services) by using Legcord, but no one has been banned from using it or any of the client mods included.

## How can I access the settings?

- Open Discord settings and there should be a button `Legcord Settings` button with a white Discord icon, you can also right click on the tray icon and click `Open Settings`

## How does this work?

- We utilize the official web app and package it within Electron. While this approach may seem familiar, our focus is on delivering a truly customized and enhanced experience. Unlike many others, we provide seamless integration for loading themes and mods without the need for installers or injectors. You can easily enable transparency effects and adopt Windows' Fluent Design, offering a modern and sleek interface. Though it's fundamentally a web wrapper, we have implemented numerous optimizations and patches to ensure a smooth and tailored experience for you.

## Does Legcord have a portable mode for windows?

- Yes it does! Simply add a folder called "legcord-data" in the folder where your legcord executable is located and start Legcord. Make sure to download the archive/zip file.

## Where can I find the source code?

- The source code is on [GitHub](https://github.com/Legcord/Legcord/).

## Where can I translate this?

- Translations are done using our [Weblate page](https://hosted.weblate.org/projects/Legcord/Legcord/).

# Credits

- [Legcord UI design, branding, and a few features](https://github.com/kckarnige)
- [OpenAsar](https://github.com/GooseMod/OpenAsar)
- [arRPC (for Rich Presence)](https://github.com/OpenAsar/arrpc)
- [electron-builder](https://electron.build)
  
Discord is trademark of Discord Inc. Legcord is not affiliated with or endorsed by Discord Inc.
Legcord is not affiliated with or endorsed by ARM Limited.
