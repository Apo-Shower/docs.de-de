---
ms.openlocfilehash: 806722ea9aec1c828786525e3155b7f624159ac1
ms.sourcegitcommit: 4f4a32a5c16a75724920fa9627c59985c41e173c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72522661"
---
### <a name="identity-adddefaultui-method-overload-removed"></a>Identität: AddDefaultUI-Methodenüberladung wurde entfernt.

Ab ASP.NET Core 3.0 ist die <xref:Microsoft.AspNetCore.Identity.IdentityBuilderUIExtensions.AddDefaultUI(Microsoft.AspNetCore.Identity.IdentityBuilder,Microsoft.AspNetCore.Identity.UI.UIFramework)?displayProperty=nameWithType>-Methodenüberladung nicht mehr vorhanden.

#### <a name="version-introduced"></a>Eingeführt in Version

3.0

#### <a name="reason-for-change"></a>Grund für die Änderung

Diese Änderung wurde aufgrund der Einführung der Funktion für statische Webressourcen notwendig.

#### <a name="recommended-action"></a>Empfohlene Maßnahme

Rufen Sie anstelle der Überladung <xref:Microsoft.AspNetCore.Identity.IdentityBuilderUIExtensions.AddDefaultUI(Microsoft.AspNetCore.Identity.IdentityBuilder)?displayProperty=nameWithType> auf. Wenn Sie Bootstrap 3 verwenden, fügen Sie außerdem die folgende Zeile in einem `<PropertyGroup>`-Element in Ihrer Projektdatei hinzu:

```xml
<IdentityUIFrameworkVersion>Bootstrap3</IdentityUIFrameworkVersion>
```

#### <a name="category"></a>Kategorie

ASP.NET Core

#### <a name="affected-apis"></a>Betroffene APIs

<xref:Microsoft.AspNetCore.Identity.IdentityBuilderUIExtensions.AddDefaultUI(Microsoft.AspNetCore.Identity.IdentityBuilder,Microsoft.AspNetCore.Identity.UI.UIFramework)?displayProperty=fullName>

<!--

#### Affected APIs

`M:Microsoft.AspNetCore.Identity.IdentityBuilderUIExtensions.AddDefaultUI(Microsoft.AspNetCore.Identity.IdentityBuilder,Microsoft.AspNetCore.Identity.UI.UIFramework)`

-->
