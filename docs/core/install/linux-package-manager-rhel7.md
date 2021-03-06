---
title: 在 Linux RHEL 7 套件管理員上安裝 .NET Core-.NET Core
description: 使用套件管理員，在 RHEL 7 上安裝 .NET Core SDK 和執行時間。
author: thraka
ms.author: adegeo
ms.date: 12/03/2019
ms.openlocfilehash: 4f85ed3da8a434fcd5b6ee88491daf623c3c8b31
ms.sourcegitcommit: 19014f9c081ca2ff19652ca12503828db8239d48
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/04/2020
ms.locfileid: "76980180"
---
# <a name="rhel-7-package-manager---install-net-core"></a>RHEL 7 套件管理員-安裝 .NET Core

[!INCLUDE [package-manager-switcher](includes/package-manager-switcher.md)]

本文說明如何使用套件管理員，在 RHEL 7 上安裝 .NET Core。

## <a name="register-your-red-hat-subscription"></a>註冊您的 Red Hat 訂用帳戶

若要從 RHEL 上的 Red Hat 安裝 .NET Core，您必須先使用 Red Hat 訂用帳戶管理員進行註冊。 如果未在您的系統上完成此動作，或您不確定，請參閱[.Net Core 的 Red Hat 產品檔](https://access.redhat.com/documentation/net_core/)。

## <a name="install-the-net-core-sdk"></a>安裝 .NET Core SDK

向訂閱管理員註冊之後，您就可以開始安裝和啟用 .NET Core SDK。 在您的終端機中，執行下列命令以啟用 RHEL 7 dotnet 通道並安裝。

```bash
subscription-manager repos --enable=rhel-7-server-dotnet-rpms
yum install rh-dotnet31 -y
scl enable rh-dotnet31 bash
```

## <a name="install-the-aspnet-core-runtime"></a>安裝 ASP.NET Core 執行時間

向訂閱管理員註冊之後，您就可以開始安裝和啟用 ASP.NET Core 執行時間。 在您的終端機中，執行下列命令。

```bash
subscription-manager repos --enable=rhel-7-server-dotnet-rpms
yum install rh-dotnet31-aspnetcore-runtime-3.1 -y
scl enable rh-dotnet31 bash
```

## <a name="install-the-net-core-runtime"></a>安裝 .NET Core 執行時間

向訂用帳戶管理員註冊之後，您就可以開始安裝和啟用 .NET Core 執行時間。 在您的終端機中，執行下列命令。

```bash
subscription-manager repos --enable=rhel-7-server-dotnet-rpms
yum install rh-dotnet31-dotnet-runtime-3.1 -y
scl enable rh-dotnet31 bash
```

## <a name="see-also"></a>請參閱

- [在 Red Hat Enterprise Linux 7 上使用 .NET Core 3。1](https://access.redhat.com/documentation/en-us/net_core/3.1/html/getting_started_guide/gs_install_dotnet)
