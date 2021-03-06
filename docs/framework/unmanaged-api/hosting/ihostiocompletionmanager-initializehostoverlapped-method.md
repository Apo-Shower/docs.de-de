---
title: IHostIoCompletionManager::InitializeHostOverlapped-Methode
ms.date: 03/30/2017
api_name:
- IHostIoCompletionManager.InitializeHostOverlapped
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostIoCompletionManager::InitializeHostOverlapped
helpviewer_keywords:
- IHostIoCompletionManager::InitializeHostOverlapped method [.NET Framework hosting]
- InitializeHostOverlapped method [.NET Framework hosting]
ms.assetid: c35199bf-bc47-4901-b467-4e8a37644bbb
topic_type:
- apiref
ms.openlocfilehash: 9fd299ad25166bcbcf0202da13a5b4cbdd20d7d7
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2019
ms.locfileid: "73133800"
---
# <a name="ihostiocompletionmanagerinitializehostoverlapped-method"></a>IHostIoCompletionManager::InitializeHostOverlapped-Methode
Bietet dem Host die Möglichkeit, benutzerdefinierte Daten zu initialisieren, um an eine Win32-`OVERLAPPED` Struktur anzufügen, die für asynchrone e/a-Anforderungen verwendet wird.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT InitializeHostOverlapped (  
    [in] void* pvOverlapped  
);  
```  
  
## <a name="parameters"></a>Parameter  
 `pvOverlapped`  
 in Ein Zeiger auf die Win32-`OVERLAPPED`-Struktur, die in der e/a-Anforderung enthalten sein soll.  
  
## <a name="return-value"></a>Rückgabewert  
  
|HRESULT|Beschreibung|  
|-------------|-----------------|  
|S_OK|`InitializeHostOverlapped` erfolgreich zurückgegeben.|  
|HOST_E_CLRNOTAVAILABLE|Der Common Language Runtime (CLR) wurde nicht in einen Prozess geladen, oder die CLR befindet sich in einem Zustand, in dem Sie verwalteten Code nicht ausführen oder den-Befehl nicht erfolgreich verarbeiten kann.|  
|HOST_E_TIMEOUT|Timeout des Aufrufes.|  
|HOST_E_NOT_OWNER|Der Aufrufer ist nicht Besitzer der Sperre.|  
|HOST_E_ABANDONED|Ein Ereignis wurde abgebrochen, während ein blockierter Thread oder eine Fiber darauf wartete.|  
|E_FAIL|Ein unbekannter schwerwiegender Fehler ist aufgetreten. Wenn eine Methode E_FAIL zurückgibt, kann die CLR innerhalb des Prozesses nicht mehr verwendet werden. Nachfolgende Aufrufe von Hostingmethoden geben HOST_E_CLRNOTAVAILABLE zurück.|  
|E_OUTOFMEMORY|Es war nicht genügend Arbeitsspeicher verfügbar, um die angeforderte Ressource zuzuordnen.|  
  
## <a name="remarks"></a>Hinweise  
 Die Funktionen der Windows-Plattform verwenden die `OVERLAPPED` Struktur zum Speichern des Zustands für asynchrone e/a-Anforderungen. Die CLR ruft die `InitializeHostOverlapped`-Methode auf, um dem Host die Möglichkeit zu geben, benutzerdefinierte Daten an eine `OVERLAPPED` Instanz anzufügen.  
  
> [!IMPORTANT]
> Um zum Anfang des benutzerdefinierten Datenblocks zu gelangen, muss der Offset auf die Größe der `OVERLAPPED` Struktur (`sizeof(OVERLAPPED)`) festgelegt werden.  
  
 Der Rückgabewert E_OUTOFMEMORY gibt an, dass der Host seine benutzerdefinierten Daten nicht initialisieren konnte. In diesem Fall meldet die CLR einen Fehler und schlägt den-Befehl fehl.  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** Informationen finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** Mscoree. h  
  
 **Bibliothek:** Als Ressource in Mscoree. dll enthalten  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Siehe auch

- [ICLRIoCompletionManager-Schnittstelle](../../../../docs/framework/unmanaged-api/hosting/iclriocompletionmanager-interface.md)
- [GetHostOverlappedSize-Methode](../../../../docs/framework/unmanaged-api/hosting/ihostiocompletionmanager-gethostoverlappedsize-method.md)
- [IHostIoCompletionManager-Schnittstelle](../../../../docs/framework/unmanaged-api/hosting/ihostiocompletionmanager-interface.md)
