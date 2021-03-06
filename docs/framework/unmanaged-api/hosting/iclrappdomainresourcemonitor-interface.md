---
title: ICLRAppDomainResourceMonitor-Schnittstelle
ms.date: 03/30/2017
api_name:
- ICLRAppDomainResourceMonitor
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRAppDomainResourceMonitor
helpviewer_keywords:
- ICLRAppDomainResourceMonitor interface [.NET Framework hosting]
ms.assetid: 72fa83a1-8997-41d7-b355-ab177a24a303
topic_type:
- apiref
ms.openlocfilehash: 208d567aa5c19ddcf8bf9b13b452cb4fc48c976f
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2019
ms.locfileid: "73126764"
---
# <a name="iclrappdomainresourcemonitor-interface"></a>ICLRAppDomainResourceMonitor-Schnittstelle
Stellt Methoden bereit, die den Arbeitsspeicher und die CPU-Auslastung einer Anwendungsdomäne überprüfen.  
  
## <a name="methods"></a>Methoden  
  
|Methode|Beschreibung|  
|------------|-----------------|  
|[GetCurrentAllocated-Methode](../../../../docs/framework/unmanaged-api/hosting/iclrappdomainresourcemonitor-getcurrentallocated-method.md)|Ruft die Gesamtgröße (in Bytes) aller Speicher Belegungen ab, die von der Anwendungsdomäne seit der Erstellung vorgenommen wurden, ohne Subtraktion von Speicher, der in die Garbage Collection aufgenommen wurde.|  
|[GetCurrentSurvived-Methode](../../../../docs/framework/unmanaged-api/hosting/iclrappdomainresourcemonitor-getcurrentsurvived-method.md)|Ruft die Anzahl der Bytes ab, die die letzte vollständige Blockierung Garbage Collection und auf die von der aktuellen Anwendungsdomäne verwiesen wird.|  
|[GetCurrentCpuTime-Methode](../../../../docs/framework/unmanaged-api/hosting/iclrappdomainresourcemonitor-getcurrentcputime-method.md)|Ruft die gesamte Prozessorzeit ab, die während der Ausführung in der aktuellen Anwendungsdomäne von allen Threads verwendet wurde, seit die Anwendungsdomäne erstellt wurde.|  
  
## <a name="remarks"></a>Hinweise  
 Die `ICLRAppDomainResourceMonitor`-Schnittstelle bietet ähnliche Funktionen wie die folgenden verwalteten Eigenschaften:  
  
- <xref:System.AppDomain.MonitoringIsEnabled%2A?displayProperty=nameWithType>  
  
- <xref:System.AppDomain.MonitoringTotalProcessorTime%2A?displayProperty=nameWithType>  
  
- <xref:System.AppDomain.MonitoringTotalAllocatedMemorySize%2A?displayProperty=nameWithType>  
  
- <xref:System.AppDomain.MonitoringSurvivedProcessMemorySize%2A?displayProperty=nameWithType>  
  
- <xref:System.AppDomain.MonitoringSurvivedMemorySize%2A?displayProperty=nameWithType>  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** Informationen finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** MetaHost. h  
  
 **Bibliothek:** Als Ressource in Mscoree. dll enthalten  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Siehe auch

- [\<appdomainresourcemonitoring > Element](../../../../docs/framework/configure-apps/file-schema/runtime/appdomainresourcemonitoring-element.md)
- [Überwachung von Anwendungsdomänenressourcen](../../../standard/garbage-collection/app-domain-resource-monitoring.md)
- [Hosten von Schnittstellen](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
- [Hosting](../../../../docs/framework/unmanaged-api/hosting/index.md)
