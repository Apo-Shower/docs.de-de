---
title: IHostTaskManager::SetLocale-Methode
ms.date: 03/30/2017
api_name:
- IHostTaskManager.SetLocale
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostTaskManager::SetLocale
helpviewer_keywords:
- SetLocale method, IHostTaskManager interface [.NET Framework hosting]
- IHostTaskManager::SetLocale method [.NET Framework hosting]
ms.assetid: 747ee407-ee8c-484d-9583-25089236d2d1
topic_type:
- apiref
ms.openlocfilehash: e560d08d3e10db1b5978d1bd7be53dfed9ca3268
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2019
ms.locfileid: "73132986"
---
# <a name="ihosttaskmanagersetlocale-method"></a>IHostTaskManager::SetLocale-Methode
Benachrichtigt den Host, dass die Common Language Runtime (CLR) das Gebiets Schema oder die Kultur für den aktuell ausgeführten Task geändert hat.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT SetLocale (  
    [in] LCID lcid  
);  
```  
  
## <a name="parameters"></a>Parameter  
 `lcid`  
 in Der Wert für den Gebiets Schema Bezeichner, der der neu zugewiesenen geografischen Kultur und Sprache zugeordnet wird.  
  
## <a name="return-value"></a>Rückgabewert  
  
|HRESULT|Beschreibung|  
|-------------|-----------------|  
|S_OK|`SetLocale` erfolgreich zurückgegeben.|  
|HOST_E_CLRNOTAVAILABLE|Die CLR wurde nicht in einen Prozess geladen, oder die CLR befindet sich in einem Zustand, in dem Sie verwalteten Code nicht ausführen oder den-Befehl nicht erfolgreich verarbeiten kann.|  
|HOST_E_TIMEOUT|Timeout des Aufrufes.|  
|HOST_E_NOT_OWNER|Der Aufrufer ist nicht Besitzer der Sperre.|  
|HOST_E_ABANDONED|Ein Ereignis wurde abgebrochen, während ein blockierter Thread oder eine Fiber darauf wartete.|  
|E_FAIL|Ein unbekannter schwerwiegender Fehler ist aufgetreten. Wenn eine Methode E_FAIL zurückgibt, kann die CLR innerhalb des Prozesses nicht mehr verwendet werden. Nachfolgende Aufrufe von Hostingmethoden geben HOST_E_CLRNOTAVAILABLE zurück.|  
|E_NOTIMPL|Der Host lässt nicht zu, dass das Gebiets Schema von verwaltetem Benutzercode geändert wird.|  
  
## <a name="remarks"></a>Hinweise  
 Die Laufzeit ruft `SetLocale` auf, wenn der Wert der <xref:System.Threading.Thread.CurrentCulture%2A?displayProperty=nameWithType>-Eigenschaft von verwaltetem Code geändert wird. Diese Methode bietet dem Host die Möglichkeit, alle Mechanismen auszuführen, die möglicherweise für die Synchronisierung von Gebiets Schemas erforderlich sind. Wenn ein Host nicht zulässt, dass das Gebiets Schema aus verwaltetem Code geändert wird, oder keinen Mechanismus zum Synchronisieren von Gebiets Schemas implementiert, sollte er E_NOTIMPL von dieser Methode zurückgeben.  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** Informationen finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** Mscoree. h  
  
 **Bibliothek:** Als Ressource in Mscoree. dll enthalten  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Siehe auch

- [ICLRTask-Schnittstelle](../../../../docs/framework/unmanaged-api/hosting/iclrtask-interface.md)
- [ICLRTaskManager-Schnittstelle](../../../../docs/framework/unmanaged-api/hosting/iclrtaskmanager-interface.md)
- [IHostTask-Schnittstelle](../../../../docs/framework/unmanaged-api/hosting/ihosttask-interface.md)
- [IHostTaskManager-Schnittstelle](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-interface.md)
- [SetUILocale-Methode](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-setuilocale-method.md)
