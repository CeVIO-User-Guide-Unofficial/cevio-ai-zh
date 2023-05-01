---
title: Change Log (This Website)
author: 夜輪風超絶技巧変奏曲
date: 2022-11-16
category: Change Log
layout: post
---

## May 1, 2023

- Material for MkDocs has been updated to 9.1.8。
- mkdocs-static-i18n plugin has been updated to 0.56。
<!-- - As the bug in mkdocs-static-i18n has been fixed, the document structure has been changed back to version June 7th 2022.
    - > [Is folder based docs structure incompatible with static navigation? #168](https://github.com/ultrabug/mkdocs-static-i18n/issues/168) -->

## November 21, 2022

- English translation has been added.
- Language switching has been enabled to switch between the English pages and Chinese pages.
    - Added mkdocs-static-i18n plugin.
    - Language switcher is now disabled as it is not compatible with `navigation.instant`.
        - > mkdocs-material language switcher contextual link is not compatible with theme.features = navigation.instant
- Due to a change in the folder structure, the creation dates of all pages have been changed.
- Added image zoom function.
    - Added mkdocs-glightbox plugin.
- Material for MkDocs has been updated to 9.0.0b3.

## 2022.11.16

- Material for MkDocs has been updated to 8.5.10.
    - Style change of annotation took place in version 8.5.6.
- Each page will now display the date it was created at the bottom of it.
    - Applied the following setting to git-revision-date-localized plugin: `enable_creation_date: true`.

## 2022.6.7

The first version.
