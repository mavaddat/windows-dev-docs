---
description: The materials Windows uses to create app hierarchy
title: Materials used in Windows apps
ms.assetid: 912C88C8-2382-465C-B4AB-902BCFAED48D
ms.date: 09/16/2024
ms.topic: article
keywords: windows 11, design, ui, uiux, materials, acrylic, mica, smoke
ms.localizationpriority: medium
---

# Materials in Windows

Materials are visual effects applied to UX surfaces that resemble real life artifacts. Windows uses two primary types of materials: occluding and transparent. Occluding materials, like _acrylic_ and _mica_, are used as base layers beneath interactive UI controls. Transparent materials such as _smoke_ are used to highlight immersive surfaces.

Mica, Acrylic, and Smoke each have a specific purpose in how they are used throughout Windows.

> [!TIP]
> This article describes how the [Fluent Design language](https://fluent2.microsoft.design/) is applied to Windows apps. For more information, see [**Fluent Design - Material**](https://fluent2.microsoft.design/material).

## Acrylic

![A semi-transparent UI surface made of acrylic](images/materials_acrylic_hero_1880.png)

[Acrylic](../style/acrylic.md) is a semi-transparent material that replicates the effect of frosted glass. In Windows 11, acrylic has been updated to be brighter and more translucent, allowing for a stronger contextual relationship with the visuals behind it. Acrylic is used only for transient, light-dismiss surfaces such as flyouts and context menus.

Acrylic is mode aware; it supports both light and dark mode.

## Mica

![Several UI surfaces made of Mica demonstrating how Mica is subtly tinted based on the user's desktop color](images/materials_mica_hero_1880.png)

[Mica](../style/mica.md) is a new opaque material introduced in Windows 11. Mica surfaces are subtly tinted with the user's desktop background color.

Mica is mode aware; it supports both light and dark modes. Mica also indicates window focus with active and inactive states as a built in feature.

## Smoke

![A modal dialog hovering above a window dimmed by smoke](images/materials_smoke_hero_1880.png)

Smoke emphasizes an important UI surface by dimming the surfaces beneath so that they recede into the background. Smoke is used to signal blocking interaction below a modal UI such as a dialog.

Smoke is not mode aware; it is always translucent black in both light and dark mode.
