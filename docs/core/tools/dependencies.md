---
title: 管理 .NET Core 中的相依性
description: 說明如何管理 .NET Core 應用程式的專案相依性。
no-loc:
- dotnet add package
- dotnet remove package
- dotnet list package
ms.date: 02/25/2020
ms.openlocfilehash: 367be7eb04d58bffc0846de1d035a5801e8d9376
ms.sourcegitcommit: 00aa62e2f469c2272a457b04e66b4cc3c97a800b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/28/2020
ms.locfileid: "78157241"
---
# <a name="manage-dependencies-in-net-core-applications"></a>管理 .NET Core 應用程式中的相依性

本文說明如何藉由編輯專案檔或使用 CLI 來新增和移除相依性。

## <a name="the-packagereference-element"></a>\<PackageReference > 元素

`<PackageReference>` 專案檔案元素具有下列結構：

```xml
<PackageReference Include="PACKAGE_ID" Version="PACKAGE_VERSION" />
```

`Include` 屬性會指定要加入至專案的封裝識別碼。 `Version` 屬性會指定要取得的版本。 版本是根據[NuGet 版本規則](/nuget/create-packages/dependency-versions#version-ranges)來指定。

> [!NOTE]
> 如果您不熟悉專案檔語法，請參閱[MSBuild 專案參考](/visualstudio/msbuild/msbuild-project-file-schema-reference)檔以取得詳細資訊。

使用條件來新增只能在特定目標中使用的相依性，如下列範例所示：

```xml
<PackageReference Include="PACKAGE_ID" Version="PACKAGE_VERSION" Condition="'$(TargetFramework)' == 'netcoreapp2.1'" />
```

上述範例中的相依性只有在該指定目標的組建發生時才有效。 條件中的 `$(TargetFramework)` 是在專案中設定的 MSBuild 屬性。 對於最常見的 .NET Core 應用程式，您不需要這麼做。

## <a name="add-a-dependency-by-editing-the-project-file"></a>藉由編輯專案檔來新增相依性

若要加入相依性，請在 `<ItemGroup>` 元素內加入 `<PackageReference>` 專案。 您可以將加入至現有的 `<ItemGroup>`，或建立一個新的。 下列範例會使用 `dotnet new console`所建立的預設主控台應用程式專案：

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>netcoreapp3.1</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.EntityFrameworkCore" Version="3.1.2" />
  </ItemGroup>

</Project>
```

## <a name="add-a-dependency-by-using-the-cli"></a>使用 CLI 新增相依性

若要新增相依性，請執行[dotnet add package](dotnet-add-package.md)命令，如下列範例所示：

```dotnetcli
dotnet add package Microsoft.EntityFrameworkCore
```

## <a name="remove-a-dependency-by-editing-the-project-file"></a>藉由編輯專案檔來移除相關性

若要移除相依性，請從專案檔中移除它的 `<PackageReference>` 元素。

## <a name="remove-a-dependency-by-using-the-cli"></a>使用 CLI 移除相依性

若要移除相依性，請執行[dotnet remove package](dotnet-remove-package.md)命令，如下列範例所示：

```dotnetcli
dotnet remove package Microsoft.EntityFrameworkCore
```

## <a name="see-also"></a>另請參閱

* [專案檔中的 NuGet 套件](../project-sdk/msbuild-props.md#nuget-packages)
* [dotnet list package 命令](dotnet-remove-package.md)
