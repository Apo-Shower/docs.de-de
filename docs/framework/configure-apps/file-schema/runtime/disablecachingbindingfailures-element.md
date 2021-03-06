---
title: <disableCachingBindingFailures>-Element
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#disableCachingBindingFailures
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/disableCachingBindingFailures
helpviewer_keywords:
- assemblies [.NET Framework],caching binding failures
- caching assembly binding failures
- <disableCachingBindingFailures> element
- disableCachingBindingFailures element
ms.assetid: bf598873-83b7-48de-8955-00b0504fbad0
ms.openlocfilehash: 23633cb282b8e59b4df4bcc2cd38717d805a207e
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2019
ms.locfileid: "73117497"
---
# <a name="disablecachingbindingfailures-element"></a>\<disablecachingbindingfailure >-Element
Gibt an, ob das Zwischenspeichern von Bindungs Fehlern deaktiviert werden soll, die auftreten, da die Assembly nicht durchsuchen gefunden wurde.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp; &nbsp;[ **\<runtime >** ](runtime-element.md) \
&nbsp;&nbsp;&nbsp;&nbsp; **\<disablecachingbindingfailure >**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<disableCachingBindingFailures enabled="0|1"/>  
```  
  
## <a name="attributes-and-elements"></a>Attribute und Elemente  
 In den folgenden Abschnitten werden Attribute sowie untergeordnete und übergeordnete Elemente beschrieben.  
  
### <a name="attributes"></a>Attribute  
  
|Attribut|Beschreibung|  
|---------------|-----------------|  
|enabled|Erforderliches Attribut.<br /><br /> Gibt an, ob das Zwischenspeichern von Bindungs Fehlern deaktiviert werden soll, die auftreten, da die Assembly nicht durchsuchen gefunden wurde.|  
  
## <a name="enabled-attribute"></a>Enabled-Attribut  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|0|Deaktivieren Sie nicht das Zwischenspeichern von Bindungs Fehlern, die auftreten, da die Assembly nicht durchsuchen gefunden wurde. Dies ist das Standard Bindungsverhalten, beginnend mit dem .NET Framework-Version 2,0.|  
|1|Hiermit deaktivieren Sie das Zwischenspeichern von Bindungs Fehlern, die auftreten, da die Assembly nicht durch Tests gefunden wurde. Diese Einstellung kehrt zum Bindungsverhalten der .NET Framework Version 1,1 zurück.|  
  
### <a name="child-elements"></a>Untergeordnete Elemente  
 Keine  
  
### <a name="parent-elements"></a>Übergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|-----------------|  
|`configuration`|Das Stammelement in jeder von den Common Language Runtime- und .NET Framework-Anwendungen verwendeten Konfigurationsdatei.|  
|`runtime`|Enthält Informationen über die Assemblybindung und die Garbage Collection.|  
  
## <a name="remarks"></a>Hinweise  
 Beginnend mit der .NET Framework Version 2,0 besteht das Standardverhalten beim Laden von Assemblys darin, alle Bindungs-und Ladefehler zwischenzuspeichern. Das heißt, wenn ein Versuch, eine Assembly zu laden, fehlschlägt, schlagen nachfolgende Anforderungen zum Laden derselben Assembly sofort fehl, ohne dass versucht wird, die Assembly zu finden. Dieses Element deaktiviert dieses Standardverhalten bei Bindungs Fehlern, die auftreten, da die Assembly nicht im Überprüfungs Pfad gefunden werden konnte. Diese Fehler lösen <xref:System.IO.FileNotFoundException>aus.  
  
 Einige Bindungs-und Ladefehler sind von diesem Element nicht betroffen und werden immer zwischengespeichert. Diese Fehler treten auf, weil die Assembly gefunden wurde, aber nicht geladen werden konnte. Sie lösen <xref:System.BadImageFormatException> oder <xref:System.IO.FileLoadException>aus. In der folgenden Liste sind einige Beispiele für derartige Fehler enthalten.  
  
- Wenn Sie versuchen, eine Datei zu laden, ist keine gültige Assembly. nachfolgende Versuche, die Assembly zu laden, schlagen auch dann fehl, wenn die ungültige Datei durch die richtige Assembly ersetzt wird.  
  
- Wenn Sie versuchen, eine Assembly zu laden, die vom Dateisystem gesperrt ist, schlagen nachfolgende Versuche, die Assembly zu laden, auch dann fehl, wenn die Assembly vom Dateisystem freigegeben wurde.  
  
- Wenn sich eine oder mehrere Versionen der Assembly, die Sie laden möchten, im Überprüfungs Pfad befinden, die von Ihnen angeforderte Version jedoch nicht zu Ihnen gehört, schlagen nachfolgende Versuche, diese Version zu laden, auch dann fehl, wenn die richtige Version in den Überprüfungs Pfad verschoben wird.  
  
## <a name="example"></a>Beispiel  
 Das folgende Beispiel zeigt, wie Sie das Zwischenspeichern von Assemblybindungsfehlern deaktivieren, die auftreten, da die Assembly nicht durchsucht wurde.  
  
```xml  
<configuration>  
   <runtime>  
      <disableCachingBindingFailures enabled="1" />  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>Siehe auch

- [Schema für Laufzeiteinstellungen](index.md)
- [Konfigurationsdateischema](../index.md)
- [So sucht Common Language Runtime nach Assemblys](../../../deployment/how-the-runtime-locates-assemblies.md)
