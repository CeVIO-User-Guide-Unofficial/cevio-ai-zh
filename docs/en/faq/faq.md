---
title: FAQ
author: 夜輪風超絶技巧変奏曲
category: faq
layout: post
---
Original article: [CeVIO AI ユーザーズガイド ┃ よくある質問](https://cevio.jp/guide/cevio_ai/faq/)

---

Q: I cannot install the software.

A: If the "User Account Control" window pops up during installation, click "Yes".

If the "Windows protected your PC" window pops up, click on "More info" and then click on the "Run anyway" button.

---

Q: I have installed the software, but I don't see "CeVIO AI".

A: To use the software, in addition to the Voice, you need to install and activate the "CeVIO AI" editor itself.

Please follow [the instructions on this page](../../firstguide/install) to install and activate the software.

---

Q: The software does not start.

A: If you get a message like "Could not load file or assembly CeVIO.Audio.dll or one of its dependencies" when starting the software, the required library (auxiliary program) is missing.

Please download and run "vc_redist.x64.exe" from [Microsoft support page](https://docs.microsoft.com/en-gb/cpp/windows/latest-supported-vc-redist?view=msvc-170).

If you are using "Windows Defender", please turn off "Controlled folder access" (set to Off by default) in "Manage Ransomware protection" under "Virus and threat protection".

Some PCs using the CPU, such as Pentium, Celeron or earlier Core i, may not start and occur errors.

Please update [Yuzuki Yukari Rei（結月ゆかり 麗）](https://cevio.jp/guide/cevio_ai/home/yukari_1_1_0), [Tohoku Kiritan（東北きりたん）](https://cevio.jp/guide/cevio_ai/home/kiritan_1_1_0), [Koharu Rikka（小春六花）](https://cevio.jp/guide/cevio_ai/home/rikka_1_1_1)and [可不(KAFU)](https://cevio.jp/guide/cevio_ai/home/kafu_update) via their pages respectively.

For other occasions where it does not start, please try a [Clean Install](https://cevio.jp/guide/cevio_ai/tool2).

---

Q: I have purchased the product but I don't know the serial number.

A: For physical / boxed edition, the Product Key for "KAFU" can be found on a manual, and the others are on the card encased in a silver bag or a plastic bag.

For digital edition purchased from Vector PC Shop, please access the received page from the link in "ライセンスキーのご案内" email, then click "ライセンスキーを表示" to check.

For digital edition purchased from DLsite, please see the download screen for this software in the Purchase History.

For digital edition purchased from Amazon, please use the link in the "Order Confirmation" email to display the product page, and check in "ゲーム&PCソフトダウンロードライブラリ".

---

Q: I can't save or export.

A: If you are using Windows Defender and enabled "Controlled folder access" (set to Off by default) in "Manage Ransomware protection" under "Virus and threat protection", you can add "CeVIO AI" to the allowed applications using "Allow an app through Controlled folder access".

!!! info "About Mac"

    For virtual environments built on a Mac with "Parallels Desktop 17" or earlier, it has been reported that turning off "Share Mac user folders with Windows" in "Sharing" under "Options" in "Configure" in Parallels solved the problem. (Parallels Desktop 18 seems to be fine with the default settings.)

    For other problems with virtualization software, please contact the provider of the virtualization software.

---

Q: No sound. I want to change the sound output device.

A: Please select the playback device from the Windows Sound setting.

You can also specify a different output device from the Windows settings in "Audio Device" in "Environment" in Options.

---

Q: Play/stop does not work with the ++space++ key. I cannot enter Japanese for track names.

A: The new MS IME will input text on screen when switching to the Japanese input method, and all shortcut keys will be invalid. A solution is to turn on Settings > General > Use previous version of Microsoft IME in the MS IME, then you can play/stop using the ++space++ key and input Japanese track names normally.

Google IME will input characters when Japanese input is on (except in combination with the ++ctrl++ key), so please turn Japanese input off and then press the ++space++ key, or use the playback button on the toolbar directly.

---

Q：++enter++ key does not confirm the input of lines or lyrics.

A: This seems to happen when Windows Update is running in the background, try restarting your PC.

---

Q: "(Import) Text File" failed.

A: Specify the character encoding of the file to be read in "Import" under "Text File Character Code" in the "Talk Settings" options.

Notepad and Google Spreadsheet are "UTF-8". Excel CSV is "Shift-JIS", but you can also select "CSV UTF-8".

---

Q: The exported text files and subtitle files are garbled when read with external software.

A: Specify the character encoding supported by your external software in "Export" under "Text File Character Code" in "Talk Settings" option.

\* For example, VideoStudio Pro 2019 (or 2018) uses "UTF-8 (with BOM)".

---

Q: The WAV export of the lines has a fixed filename.

A: The file name is specified in the File menu > Export > "File Naming Convention" in the "Details" section of Audio Files per Each Line. If you set the file name to `$Number$-$Cast Name$-$Text$`, the file name will revert to the default setting.

---

Q: I don't want silence at the end of the file for WAV export of lines.

A: If you select Option > Talk Settings, then turn off Affects on Export Audio File, the "Speech Interval" will not add silence to it.

---

Q: I can't overlap lines from another track.

A: Please turn on "Automatic Multi-track Alignment" from the right-click menu of an audio element or from "Talk Settings".

---

Q: I cannot connect to SAPI5. Cannot link to 'Word', 'Excel' or 'Acrobat Reader'.

A: As CeVIO AI is a 64-bit application, it cannot be linked directly with 32-bit external software (e.g. 棒読みちゃん, BouyomiChan). (There seems to be external softwares that can link "CeVIO AI" with "BouyomiChan", etc.)

Microsoft Office such as Word and Excel, and Acrobat Reader are not supported.

In extremely rare cases, registration of the linkage to the OS may fail during the installation process.

In this case, please try a [Clean Install](https://cevio.jp/guide/cevio_ai/tool2).

---

Q：There aren't 1/64 in Quantize.

A: For CeVIO AI, it is not recommended to use the tiny gaps between the notes to express the sokuon (っ, small tsu), or to use the position of the notes to express the timing of the vocalization.

Including the sokuon in the lyrics and adjusting the timing of the vocalization in the Timing adjustment screen will get a better song.

---

Q: The sound is intermittent during playback.

A: Real-time speech synthesis using the playback button requires CPU performance.

For laptops, first try connecting to a power source (deactivate the power-saving mode).

Alternatively, the following steps may improve the situation, please try them.

1. If a USB audio device is connected, disconnect it.
2. Select "High Performance" from "Plans shown on the battery meter" in "Power Options" in the control panel.
3. (From translator) For Windows 10, select the Battery icon on the taskbar, and then drag the slider to the "Best performance" mode. For Windows 11, select Start > Settings > System > Power & battery, then choose "Best performance" from "Power mode".

If the situation does not improve, please "Freeze Tracks" before playback.

\* The sound quality of the exported file is not affected by CPU performance.

---

Q: I want to use it offline.

A: You can use the system offline for 365 days after it was last started with an internet connection.

\* Not applicable to communication blocking by security software etc.

---

Q: I want to use it on another PC. I want to deactivate it.

A: Simply enter the Product Key after installing the software on a new PC.

\* This software does not require operations such as "Deactivate".

\* After activation, you must wait 24 hours before you can perform the activation again on another computer with the same Product Key.

---

Q: I want to back up my user dictionary and option settings and transfer them to another PC.

A: Please select File > Export > Settings File to export a file, then import it from File > Import > Settings File on another PC.

\* It is also possible to import the user dictionary of CeVIO CS7 into CeVIO AI.

---

Q: I would like to know the license regarding the use of character and sound data.

A: Non-commercial hobbies and secondary creations can use the audio and characters for free. Please make use of them.

Please refer to [this page](http://cevio.jp/commercial/) for the scope of other free use and commercial use.

---

Q: I want to report bugs or provide suggestions.

A: Please use [this form](https://docs.google.com/forms/d/1qGam3pOnz_XJ2dhxvGMPX8QeoBZPiaPrzMft6fOh-tY/viewform) to report.
