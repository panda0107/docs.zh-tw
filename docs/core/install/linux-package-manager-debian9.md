---
title: 在 Debian 9 上安裝 .NET Core-套件管理員-.NET Core
description: 使用套件管理員，在 Debian 9 上安裝 .NET Core SDK 和執行時間。
author: thraka
ms.author: adegeo
ms.date: 12/04/2019
ms.openlocfilehash: 32b152ff9be5135cf0ca7f8914bc9ee4f78000be
ms.sourcegitcommit: cdf5084648bf5e77970cbfeaa23f1cab3e6e234e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "76920842"
---
# <a name="debian-9-package-manager---install-net-core"></a>Debian 9 套件管理員-安裝 .NET Core

[!INCLUDE [package-manager-switcher](./includes/package-manager-switcher.md)]

本文說明如何使用套件管理員，在 Debian 9 上安裝 .NET Core。 如果您要安裝執行階段，我們建議您安裝 [ASP.NET Core runtime](#install-the-aspnet-core-runtime)，因為它同時包含 .net Core 和 ASP.NET Core 執行階段。

## <a name="register-microsoft-key-and-feed"></a>註冊 Microsoft 金鑰和總結

安裝 .NET 之前，您必須：

- 註冊 Microsoft 金鑰。
- 註冊產品存放庫。
- 安裝必要的相依性。

每部電腦只需要執行這項作業一次。

開啟終端機並執行下列命令。

```bash
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.asc.gpg
sudo mv microsoft.asc.gpg /etc/apt/trusted.gpg.d/
wget -q https://packages.microsoft.com/config/debian/9/prod.list
sudo mv prod.list /etc/apt/sources.list.d/microsoft-prod.list
sudo chown root:root /etc/apt/trusted.gpg.d/microsoft.asc.gpg
sudo chown root:root /etc/apt/sources.list.d/microsoft-prod.list
```

## <a name="install-the-net-core-sdk"></a>安裝 .NET Core SDK

更新可供安裝的產品，然後安裝 .NET Core SDK。 在您的終端機中，執行下列命令。

```bash
sudo apt-get update
sudo apt-get install apt-transport-https
sudo apt-get update
sudo apt-get install dotnet-sdk-3.1
```

## <a name="install-the-aspnet-core-runtime"></a>安裝 ASP.NET Core 執行階段

更新可供安裝的產品，然後安裝 ASP.NET 執行時間。 在您的終端機中，執行下列命令。

```bash
sudo apt-get update
sudo apt-get install apt-transport-https
sudo apt-get update
sudo apt-get install aspnetcore-runtime-3.1
```

## <a name="install-the-net-core-runtime"></a>安裝 .NET Core 執行階段

更新可供安裝的產品，然後安裝 .NET Core 執行階段。 在您的終端機中，執行下列命令。

```bash
sudo apt-get update
sudo apt-get install apt-transport-https
sudo apt-get update
sudo apt-get install dotnet-runtime-3.1
```

## <a name="how-to-install-other-versions"></a>如何安裝其他版本

[!INCLUDE [package-manager-switcher](./includes/package-manager-heading-hack-pkgname.md)]

## <a name="troubleshoot-the-package-manager"></a>針對套件管理員進行疑難排解

本節提供使用封裝管理員安裝 .NET Core 時，可能會收到的常見錯誤資訊。

### <a name="failed-to-fetch"></a>無法提取

[!INCLUDE [package-manager-failed-to-fetch-deb](includes/package-manager-failed-to-fetch-deb.md)]
