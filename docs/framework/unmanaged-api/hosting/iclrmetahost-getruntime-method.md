---
title: ICLRMetaHost::GetRuntime-Methode
ms.date: 03/30/2017
api_name:
- ICLRMetaHost.GetRuntime
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRMetaHost::GetRuntime
helpviewer_keywords:
- GetRuntime method [.NET Framework hosting]
- ICLRMetaHost::GetRuntime method [.NET Framework hosting]
ms.assetid: a10749f1-ab91-47cf-982f-d8ccd2e81bd2
topic_type:
- apiref
ms.openlocfilehash: eb305aaa18fcb8dc63e3090297aabc8defc3a401
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2019
ms.locfileid: "73140932"
---
# <a name="iclrmetahostgetruntime-method"></a>ICLRMetaHost::GetRuntime-Methode
Ruft die [ICLRRuntimeInfo](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-interface.md) -Schnittstelle ab, die einer bestimmten Version des Common Language Runtime (CLR) entspricht. Diese Methode ersetzt die [CorBindToRuntimeEx](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md) -Funktion, die mit dem [STARTUP_LOADER_SAFEMODE](../../../../docs/framework/unmanaged-api/hosting/startup-flags-enumeration.md) -Flag verwendet wird.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT GetRuntime (  
    [in] LPCWSTR pwzVersion,  
    [in] REFIID riid,  
    [out,iid_is(riid), retval] LPVOID *ppRuntime  
);  
```  
  
## <a name="parameters"></a>Parameter  
 `pwzVersion`  
 in Die in den Metadaten gespeicherte .NET Framework Kompilierungs Version im Format "v*A*. *B*[. *X*] ". *A*, *B*und *X* sind Dezimalzahlen, die der Hauptversion, der neben Version und der Buildnummer entsprechen.  
  
> [!NOTE]
> Dieser Parameter muss dem Verzeichnisnamen für die .NET Framework Version entsprechen, wie er unter "c:\WINDOWS\Microsoft.NET\Framework" oder "c:\WINDOWS\Microsoft.NET\Framework64." angezeigt wird.  
  
 Beispiel Werte sind "v 1.0.3705", "v 1.1.4322", "v 2.0.50727" und "v 4.0". *X*", wobei *x* von der installierten Buildnummer abhängig ist. Das Präfix "v" ist erforderlich.  
  
 `riid`  
 in Der Bezeichner für die gewünschte Schnittstelle. Der einzige gültige Wert für diesen Parameter ist IID_ICLRRuntimeInfo.  
  
 `ppRuntime`  
 vorgenommen Ein Zeiger auf die [iclrruntimeingefo](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-interface.md) -Schnittstelle, die der angeforderten Laufzeit entspricht.  
  
## <a name="return-value"></a>Rückgabewert  
 Diese Methode gibt die folgenden spezifischen HRESULTs sowie HRESULT-Fehler zurück, die Methodenfehler anzeigen.  
  
|HRESULT|Beschreibung|  
|-------------|-----------------|  
|S_OK|Die Methode wurde erfolgreich abgeschlossen.|  
|E_POINTER|`pwzVersion` oder `ppRuntime` ist NULL.|  
  
## <a name="remarks"></a>Hinweise  
 Diese Methode interagiert konsistent mit Legacy Schnittstellen, wie z. b. der [ICorRuntimeHost](../../../../docs/framework/unmanaged-api/hosting/icorruntimehost-interface.md) -Schnittstelle, und Legacy Funktionen wie den veralteten `CorBindTo*` Funktionen (siehe [Veraltete CLR-Hostingfunktionen](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-functions.md) in der .NET Framework 2,0-Hosting-API). Das heißt, Laufzeiten, die mit der Legacy-API geladen werden, sind für die neue API sichtbar, und Laufzeiten, die mit der neuen API geladen werden, sind für die Legacy-API sichtbar.  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** Informationen finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** MetaHost. h  
  
 **Bibliothek:** Als Ressource in Mscoree. dll enthalten  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Siehe auch

- [ICLRMetaHost-Schnittstelle](../../../../docs/framework/unmanaged-api/hosting/iclrmetahost-interface.md)
- [Veraltete CLR-Hostingschnittstellen und Co-Klassen](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-interfaces-and-coclasses.md)
- [CLR-Hostingschnittstellen](../../../../docs/framework/unmanaged-api/hosting/clr-hosting-interfaces.md)
- [Veraltete CLR-Hostingfunktionen](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-functions.md)
- [Hosting](../../../../docs/framework/unmanaged-api/hosting/index.md)
