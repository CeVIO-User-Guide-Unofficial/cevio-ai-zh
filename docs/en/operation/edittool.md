---
title: Editing Tool (Song)
author: 夜輪風超絶技巧変奏曲
category: operation
layout: post
---
Original article: [CeVIO AI ユーザーズガイド ┃ 編集ツール（ソング）](https://cevio.jp/guide/cevio_ai/operation/edittool/)

---

![edit tool](images/edittool_1.png#only-light)
![edit tool](images/edittool_1_dark.png#only-dark)

Switch the edit mode of the Song Track.

(Cannot be used in Talk Track or Audio Track.)

### Selection Tool

Score editing screen: Select notes, tempo, etc. Drag to select a range of notes.

Adjustment screen: Drag to copy or delete notes.

\* When ++lctrl++ is held down, it changes to the Draw Tool.

### Collectively Selection Tool

Select all the notes in the range and all the adjustment values at once, without quantization while pressing Alt.

\* When ++lctrl++ is held down, it changes to the Draw Tool.

### Draw Tool

Score editing screen: Select notes, tempo, etc. Drag to enter or move notes.

Adjustment screen: Drag to adjust values. Change to connection adjustment mode when ++alt++ is pressed.

\* When ++lctrl++ is held down, it changes to the Eraser Tool.

!!! info "Connection Adjustment Mode"

    ![connection adjustment mode](images/edittool_2.png)
    
    * When you hold down ++alt++ and drag the mouse, the draw tool will draw a red line. When ++alt++ is released, the red line drawn and the original line will be automatically connected and used as the new value.
    * When ++alt++ is held down, a single line reflecting the adjusted value will be displayed. You can use it to check the current status easily.

        \* If you release ++alt++ without dragging, the focus will shift to the menu[^1], but you can check it again by holding down ++alt++.
    
    * The connection between the default value and the adjusted value on the screen may look a little off due to the internal data resolution of the horizontal axis (time).

### Line Tool

Score editing screen: Same as the Draw Tool.

Adjustment screen: (except for Timing editing screen) Drag to draw a straight line. Hold down ++shift++ at the same time to draw a horizontal line.

\* When ++lctrl++ is held down, it changes to the Eraser Tool.

### Eraser Tool

Score editing screen: Delete notes, tempo, etc.

Adjustment screen: Delete the adjusted value. (Pitch/Vibrato editing screen) Hold down ++shift++ at the same time to delete the original value.[^2]

\* When ++lctrl++ is held down, it changes to the Selection Tool.

[^1]: Translator's note: Actually this is a shortcut for Windows to use the keyboard to invoke the menus, and the letters that follow in the text of the menus are the keys that invoke them. For example, try pressing ++alt++ in CeVIO and then pressing ++f++ (
[^2]: Translator's note: A trick: deleting the original pitch value with eraser tool can make a death growl.
