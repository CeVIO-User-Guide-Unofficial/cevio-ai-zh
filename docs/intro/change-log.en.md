---
title: 更新日志
author: 夜輪風超絶技巧変奏曲
date: 2022-02-04
category: Change Log
layout: post
---

------------------------------------------------------
Jun.29,2022 Version 8.3 Official Release (8.3.2.0～8.3.3.0)
------------------------------------------------------
Version 8.3 is even easier to use with many improvements, including support for exporting 24bit / 32bit float WAV files, implementation of new Song functions, improved operability, and improved Talk phonographs.

▼Common to Songs and Talks
・WAV export format was added to "Environment" under "Options.
　Supports 24 bit / 32 bit float output (except for mixdown WAV export).

▼Song related changes
・Updated to Song Engine 6.1.3. No change in sound quality.

・Supported Accent and Staccato settings.

・Supported the dynamics setting of "ffff", "fff", "ppp", "ppppp".

・The "Merge Notes" function has been implemented.

・The right-click menu changes depending on the situation, making it easier to set notes, etc.
　・When a single note is selected, the attributes (Accent/Staccato/Breath/Slur/Falsetto) can be set and auditioned.
　・With multiple notes selected, slurs can be set, notes can be combined, and auditioning can be performed.

・When moving notes other than with the "Collectively Select" tool, the parameters will automatically follow if they have already been adjusted.

・The following processes have been speeded up to improve response time.
　・Loading a project.
　・Undo/Redo.
　・Paste after copying a collectively selection, and drag/cut/delete after collectively selection.
　・Insert/delete measures.
　・Add, change, and delete tempo and time signatures.
　・Move notes with the up/down cursor keys (when "Auto Play" is on).

・Improved eraser behavior for phoneme/note timing.
　*The State Line is not necessarily initialized, but interpolated based on the ratio of the previous/next phoneme/note.

・The "Enter Lyrics Collectively" can now be completed by pressing the [Enter] key.

・The following shortcut keys have been added.
　[Ctrl+Arrow Left/Right]...Switch Editing Tools.
　[Ctrl+Tab]...Display the next adjustment screen.
　[Ctrl+Shift+Tab]...Display the previous adjustment screen.
　[Shift+Q]...Next quantize value.
　[Shift+W]...Previous quantize value.
　[Shift+T]...Triplet on/off.
　[Ctrl+U]...Merge notes (when multiple notes are selected).

・The menu name "Remove Fine Spaces" was changed to "Remove Rests".
　The gap between one note and the next note can now be filled even when only one note is selected.

・The MIDI Import Window now supports "*.midi" extensions.

・Fixed a bug that the eraser could not erase the adjustment timing in the Score editing screen.

・Fixed a bug that the mouse cursor did not return to the pen, etc., when the mouse cursor was moved out of the adjustment screen and then returned.

・Fixed a bug in which the tempo, time signature, key signature, and dynamics were not pasted correctly under certain circumstances after copying a measure by measure with the "Collectively Select" tool.

▼Talk related changes
・Updated to Talk Engine 6.0.18. No change in sound quality.

・Updated to Japanese Talk Dictionary 3.0.14.

・Improved phoneme graph.
　・The bar graph of the mouse cursor position in PIT and VOL is surrounded by a vertical line to make it easier to understand the operation target.
　・Phoneme names are now displayed at the top of the PIT and VOL bar graphs. It is easier to adjust while looking at the top of the graph.

・The following shortcut keys have been added.
　[Ctrl+Tab]...Display the next adjustment screen.
　[Ctrl+Shift+Tab]...Display the previous adjustment screen.

▼Other changes
・The default horizontal zoom setting has been reduced to make it easier to see the timeline.

・All supported file extensions are now initially displayed in the import window.

・The maximum number of "Recent Project" in the "File" menu has been increased to 10 files.

・Other minor improvements and bug fixes.
      