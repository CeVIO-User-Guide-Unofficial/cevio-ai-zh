---
title: Description of the Song Track
author: 夜輪風超絶技巧変奏曲
category: songtrack
layout: post
---
原文：[CeVIO AI ユーザーズガイド ┃ ソングトラックの説明](https://cevio.jp/guide/cevio_ai/songtrack/)

---
Put the notes in the piano roll and enter lyrics, then fine-tune in the adjustment screen.

By selecting "Add Track" from "Track" menu or the right-clicking on a track, up to 32 song tracks can be added.

![songtrack](images/songtrack_1.png#only-light)
![songtrack](images/songtrack_1_dark.png#only-dark)

### Position Cursor

Click on the ruler to move the cursor to the position where you want playback to begin.

The piano roll is usually automatically position-corrected by quantize, but clicking when holding down ++alt++ will not correct it.

### Ruler

In the Measure Row, you can drag the mouse horizontally (hold down the left mouse button) to scroll.

Drag the mouse vertically to zoom in/out on any row.

You can add, edit, and delete tempo and other information in the middle of the song in the Tempo, Time Signature, Key Signature, and Dynamics Mark Rows.

\* The Tempo and Time Signature Rows are hidden by default, but can be displayed from the ruler header or the right-click menu in the piano roll.[^1]

### Listening

Play a simple interval of the selected note. In the adjustment screen, play the selected area as a interval.

You can also use the shortcut key ++shift+space++ to listen.

### Automatic Listening

Toggle whether or not the notes are automatically played after they are entered or moved.

### Piano Keyboard

Click on the scale and character assigned to this track will sing this key.

### Scrollbar

When the scrollbar is at the right end, you can add measures by pressing the right scroll button or press ++shift++ with mouse scroll down.

### Zoom Slider

Drag to change the scaling rate of the piano roll.

## Right-click Menu

Right-click (or hold down on the touchscreen) on the Piano Roll to open the menu.

![right-click menu](images/songtrack_2.png)

### Selection / Collectively Selection / Draw / Line / Eraser Tool

Toggle between the edit tools.

[Editing Tool](../edittool)

### Quantize

Change quantize.

[Quantize is](../infopanel#Quantize)

### Edit Mode {#edit-mode-song}

Toggle between the Score editing mode for entering notes and lyrics, and the modes for adjusting timing, volume, pitch and vibrato.

You can also disable the vibrato of the selected track.

### Cut

Cut the selected note(s).

### Copy

Copy the selected note(s).

### Paste

Paste the copied/cut note(s) to the position of the position cursor.

### Delete

Delete the selected note(s).

### Select All

Select all the notes on the current track.

### Enter Lyrics Collectively

Input the lyrics at a time from the currently selected note (or from the beginning if it is not selected).

### Other Operations

#### Insert Measures

Insert measures at the specified position and length for the currently selected track or all song tracks.

You can also append measures to the end by pressing the right scroll button on the scroll bar at the right end of the piano roll; or by pressing ++shift++ + scroll the mouse wheel down.

#### Delete Measures

Delete measures at the specified position and length for the currently selected track or all song tracks.

#### Remove Rests

Removes tiny gaps (rests) caused by MIDI import, etc.

### Enter Lyrics with Phoneme

Enter lyrics with phonemic symbol.

When this option is on, the input mode switches to phoneme input mode, and the background of the lyrics input field changes to blue-grey.

!!! new

    ### Auto Split English Lyrics

    Automatically divide into one syllable per note when entering English lyrics.

    \* The division position in the notation may be incorrect due to automatic estimation.

### View

### Other Track Notes

Select whether or not to display notes from other song tracks in the Score editing screen.

(Notes in muted track will not be displayed.)

### Tempo Row / Time Signature Row / Key Signature Row / Dynamics Mark Row

Select whether or not to display Tempo / Time Signature / Key Signature / Dynamics Mark on the ruler.

### Beat Line / Quantize Line / Line Display on Adjustment Screen

Select whether or not to display Beat / Quantize Lines in the piano roll.

When "Line Display on Adjustment Screen" is turned on, the Beat and Quantize Lines will be also displayed on the Adjustment screen.

!!! new

    ### Timing Status Line

    Select whether or not to display state change lines within phonemes on the Timing editing screen.

    They will be automatically adjusted when hidden.

### Guide Cursor

Select whether or not to display the Quantize guide cursor.

\* It will be also displayed on the Score editing screen when using Collectively Selection / Draw / Line Tool.

[^1]:Translator's note: The original is Dynamics Mark Rows, but since version 8.2.5.0, Dynamics Mark Rows are shown by default along with the Key Signature Row, and Tempo and Time Signature Rows are hidden by default.
