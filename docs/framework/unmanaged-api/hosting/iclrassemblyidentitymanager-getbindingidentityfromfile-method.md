---
title: ICLRAssemblyIdentityManager::GetBindingIdentityFromFile-Methode
ms.date: 03/30/2017
api_name:
- ICLRAssemblyIdentityManager.GetBindingIdentityFromFile
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRAssemblyIdentityManager::GetBindingIdentityFromFile
helpviewer_keywords:
- GetBindingIdentityFromFile method [.NET Framework hosting]
- ICLRAssemblyIdentityManager::GetBindingIdentifyFromFile method [.NET Framework hosting]
ms.assetid: 7797562d-7b4c-4bd9-8b93-f35e0e2869e4
topic_type:
- apiref
ms.openlocfilehash: 19d6a76d62680be91a7b9721912ca528edde7511
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2019
ms.locfileid: "73126754"
---
# <a name="iclrassemblyidentitymanagergetbindingidentityfromfile-method"></a>ICLRAssemblyIdentityManager::GetBindingIdentityFromFile-Methode
Ruft die assemblyidentitäts-Bindungs Daten für die Assembly am angegebenen Dateipfad ab.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT GetBindingIdentityFromFile(  
    [in] LPCWSTR     pwzFilePath,  
    [in] DWORD       dwFlags,  
    [out, size_is(*pcchBufferSize)] LPWSTR pwzBuffer,  
    [in, out] DWORD *pcchBufferSize  
);  
```  
  
## <a name="parameters"></a>Parameter  
 `pwzFilePath`  
 in Der Pfad zu der Datei, die ausgewertet werden soll.  
  
 `dwFlags`  
 in Ein Wert der [ECLRAssemblyIdentityFlags](../../../../docs/framework/unmanaged-api/hosting/eclrassemblyidentityflags-enumeration.md) -Enumeration, der den Identitätstyp einer Assembly angibt. Wird für zukünftige Erweiterbarkeit bereitgestellt. CLR_ASSEMBLY_IDENTITY_FLAGS_DEFAULT ist der einzige Wert, den die Common Language Runtime (CLR)-Version 2,0 unterstützt.  
  
 `pwzBuffer`  
 vorgenommen Ein Puffer, der die nicht transparenten Assembly-Identitätsdaten enthält.  
  
 `pcchBufferSize`  
 [in, out] Ein Zeiger auf die Größe der `pwzBuffer`.  
  
## <a name="return-value"></a>Rückgabewert  
  
|HRESULT|Beschreibung|  
|-------------|-----------------|  
|S_OK|Die Methode wurde erfolgreich zurückgegeben.|  
|E_INVALIDARG|Der angegebene `pwzFilePath` ist NULL.|  
|ERROR_INSUFFICIENT_BUFFER|Die Größe der `pwzBuffer` ist zu klein.|  
|HOST_E_CLRNOTAVAILABLE|Die CLR wurde nicht in einen Prozess geladen, oder die CLR befindet sich in einem Zustand, in dem Sie verwalteten Code nicht ausführen oder den-Befehl nicht erfolgreich verarbeiten kann.|  
|HOST_E_TIMEOUT|Timeout des Aufrufes.|  
|HOST_E_NOT_OWNER|Der Aufrufer ist nicht Besitzer der Sperre.|  
|HOST_E_ABANDONED|Ein Ereignis wurde abgebrochen, während ein blockierter Thread oder eine Fiber darauf wartete.|  
|E_FAIL|Ein unbekannter schwerwiegender Fehler ist aufgetreten. Wenn eine Methode E_FAIL zurückgibt, kann die CLR innerhalb des Prozesses nicht mehr verwendet werden. Nachfolgende Aufrufe von Hostingmethoden geben HOST_E_CLRNOTAVAILABLE zurück.|  
  
## <a name="remarks"></a>Hinweise  
 `GetBindingIdentityFromFile` wird in der Regel zweimal aufgerufen. Der erste-Befehl liefert einen NULL-Wert für `pwzBuffer`, und die-Methode gibt die entsprechende Größe in `pcchBufferSize`zurück. Der zweite-Befehl stellt einen entsprechend zugewiesenen Puffer bereit, und die-Methode gibt nach Abschluss des Vorgangs mit den eigentlichen Puffer Daten zurück.  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** Informationen finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** Mscoree. h  
  
 **Bibliothek:** Als Ressource in Mscoree. dll enthalten  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Siehe auch

- [ICLRAssemblyIdentityManager-Schnittstelle](../../../../docs/framework/unmanaged-api/hosting/iclrassemblyidentitymanager-interface.md)
- [ICLRAssemblyReferenceList-Schnittstelle](../../../../docs/framework/unmanaged-api/hosting/iclrassemblyreferencelist-interface.md)
- [ICLRHostBindingPolicyManager-Schnittstelle](../../../../docs/framework/unmanaged-api/hosting/iclrhostbindingpolicymanager-interface.md)
