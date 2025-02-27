---
title: Security and identity
description: This article provides an index of development features that are related to security and identity scenarios in Windows apps.
ms.topic: overview
ms.date: 09/09/2024
#customer intent: As a Windows developer, I want to learn to use security and identity features available to Windows apps so that I can build more secure apps.
---

# Security and identity

This article provides an index of development features that are related to scenarios involving security and identity in Windows apps.

## Windows OS features

Windows provides a wide variety of APIs related to security and identity scenarios for apps. These features are available via a combination of Windows App SDK, Windows Runtime (WinRT), and Win32 (C++ and COM) APIs provided by the [Windows SDK](https://developer.microsoft.com/windows/downloads/windows-sdk).

### Windows App SDK APIs

The [Windows App SDK](../../windows-app-sdk/index.md) currently does not provide APIs related to security and identity scenarios other than a few helper APIs in the [Microsoft.Windows.Security.AccessControl](/windows/windows-app-sdk/api/winrt/microsoft.windows.security.accesscontrol) namespace. These APIs are related to named object sharing between packaged apps and Win32 applications.

### WinRT APIs

The following articles provide information about features available via WinRT APIs provided by the Windows SDK.

| Article | Description |
|---------|-------------|
| [Security](/windows/uwp/security) | Learn about the breadth of security features for Windows apps.  |
| [Authentication and user identity](/windows/uwp/security/authentication-and-user-identity) | Windows apps have several options for user authentication, ranging from simple single sign-on (SSO) using Web authentication broker to highly secure two-factor authentication. |
| [Credential locker](credential-locker.md) | This article describes how Windows apps can use the Credential Locker to securely store and retrieve user credentials, and roam them between devices with the user's Microsoft account. |
| [Cryptography](/windows/uwp/security/cryptography) | Learn about cryptography features available to Windows apps. |
| [Fingerprint biometrics](fingerprint-biometrics.md) | This article explains how to add fingerprint biometrics to your Windows app, including a request for fingerprint authentication when the user must consent to a particular action increases the security of your app. |
| [Share certificates between apps](share-certificates.md) | This article shows how you can authenticate multiple Windows apps using the same certificate, and how you can provide a method for users to import a certificate that was provided for access to secured web services. |
| [Smart cards](smart-cards.md) | This topic explains how packaged Windows apps can use smart cards to connect users to secure network services. |
| [Windows Hello](windows-hello.md) | This article describes the Windows Hello technology and discusses how developers can implement this technology to protect their apps and backend services. It highlights specific capabilities of Windows Hello that help mitigate threats from conventional credentials and provides guidance about designing and deploying these technologies as part of your packaged Windows apps. |
| [Create a Windows Hello login app](windows-hello-login.md) | Part 1 of a complete walkthrough on how to create a packaged Windows app that uses Windows Hello as an alternative to traditional username and password authentication systems. |
| [Create a Microsoft Passport login service](windows-hello-auth-service.md) | Part 2 of a complete walkthrough on how to use Windows Hello as an alternative to traditional username and password authentication systems in packaged Windows apps. |

### Win32 (C++ and COM) APIs

The following articles provide information about features available via Win32 (C++ and COM) APIs provided by the Windows SDK.

| Article | Description |
|---------|-------------|
| [Security and identity](/windows/win32/security) | Learn about the breadth of security features available to Windows apps via Win32 APIs. |
| [Authentication](/windows/win32/secauthn/authentication-portal) | Learn about authentication features available via Win32 APIs. |
| [Cryptography](/windows/win32/seccng/cng-portal) | Learn about cryptography features available via Win32 APIs. |

## .NET features

The .NET SDK also provides APIs related to security and identity scenarios for WPF and Windows Forms apps. The security and cryptography APIs in .NET can also be used in C# WinUI apps.

| Article | Description |
|---------|-------------|
| [Security in .NET](/dotnet/standard/security/)  | Learn about security concepts and features for all .NET apps.  |
| [Security (WPF)](/dotnet/desktop/wpf/security-wpf) | Learn about security concepts and features for WPF apps. |
| [Windows Forms Security](/dotnet/desktop/winforms/windows-forms-security) | Learn about security concepts and features for Windows Forms apps. |

## Other features

| Topic | Description |
|---------|-------------|
| [Intro to passkeys](./intro.md) | Passkeys are simpler, stronger, passwordless sign-ins. |
| [Implement passkeys](./implement.md) | Describes how to implement passkey sign-ins across online, enterprise, and government applications, and for payments. |
| [Design guidelines for passkeys](./design.md) | There are 14 design patterns for passkeys. You can get started with two essential patterns, and then add optional patterns to your passkeys deployment based on your unique business needs. |
| [Use cases for passkeys](./use-cases.md) | This topic describes some use cases for passkeys. |
| [Tools and libraries for passkeys](./tools-libraries.md) | This topic contains info about tools and libraries to help you implement passkeys. |
| [Reference for passkeys](./reference.md) | This topic offers some reference info, demos, and examples. |

## Related content

- [App lifecycle and system services](../app-lifecycle-and-system-services.md)
- [Develop Windows desktop apps](../index.md)
