---
title: < Crst_DisableSpinWait >-element
ms.date: 04/18/2019
f1_keywords:
- Crst_DisableSpinWait
helpviewer_keywords:
- Crst_DisableSpinWait element
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6cde26250db0b3d11c51a18b7ebd378953ae0958
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/22/2019
ms.locfileid: "59981254"
---
# <a name="crstdisablespinwait-element"></a><span data-ttu-id="8806f-102">\<Crst_DisableSpinWait >-Element</span><span class="sxs-lookup"><span data-stu-id="8806f-102">\<Crst_DisableSpinWait> element</span></span>

<span data-ttu-id="8806f-103">Gibt an, ob die Spin-warten auf einen kritischen Abschnitt bei Konflikten deaktiviert.</span><span class="sxs-lookup"><span data-stu-id="8806f-103">Specifies whether to disable spin-waiting for a critical section when contended.</span></span> \ 
  
 <span data-ttu-id="8806f-104">\<configuration></span><span class="sxs-lookup"><span data-stu-id="8806f-104">\<configuration></span></span>  
<span data-ttu-id="8806f-105">\<runtime></span><span class="sxs-lookup"><span data-stu-id="8806f-105">\<runtime></span></span>  
<span data-ttu-id="8806f-106">\<Crst_DisableSpinWait></span><span class="sxs-lookup"><span data-stu-id="8806f-106">\<Crst_DisableSpinWait></span></span>  
  
## <a name="syntax"></a><span data-ttu-id="8806f-107">Syntax</span><span class="sxs-lookup"><span data-stu-id="8806f-107">Syntax</span></span>  
  
```xml  
<Crst_DisableSpinWait enabled="true | false"/>  
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="8806f-108">Attribute und Elemente</span><span class="sxs-lookup"><span data-stu-id="8806f-108">Attributes and Elements</span></span>

<span data-ttu-id="8806f-109">In den folgenden Abschnitten werden Attribute sowie untergeordnete und übergeordnete Elemente beschrieben.</span><span class="sxs-lookup"><span data-stu-id="8806f-109">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="8806f-110">Attribute</span><span class="sxs-lookup"><span data-stu-id="8806f-110">Attributes</span></span>  
  
|<span data-ttu-id="8806f-111">Attribut</span><span class="sxs-lookup"><span data-stu-id="8806f-111">Attribute</span></span>|<span data-ttu-id="8806f-112">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="8806f-112">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="8806f-113">**enabled**</span><span class="sxs-lookup"><span data-stu-id="8806f-113">**enabled**</span></span>|<span data-ttu-id="8806f-114">Gibt an, ob Spin-warten auf kritische Abschnitte aktiviert ist, wenn diese Anzahl von Konflikten vorliegt.</span><span class="sxs-lookup"><span data-stu-id="8806f-114">Specifies whether spin-waiting for critical sections is enabled when they are contended.</span></span>|  
  
## <a name="enabled-attribute"></a><span data-ttu-id="8806f-115">Enabled-Attribut</span><span class="sxs-lookup"><span data-stu-id="8806f-115">enabled Attribute</span></span>  
  
|<span data-ttu-id="8806f-116">Wert</span><span class="sxs-lookup"><span data-stu-id="8806f-116">Value</span></span>|<span data-ttu-id="8806f-117">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="8806f-117">Description</span></span>|  
|-----------|-----------------|  
|<span data-ttu-id="8806f-118">1</span><span class="sxs-lookup"><span data-stu-id="8806f-118">1</span></span>|<span data-ttu-id="8806f-119">Drehfeld-Waiting ist aktiviert.</span><span class="sxs-lookup"><span data-stu-id="8806f-119">Spin-waiting is enabled.</span></span>|  
|<span data-ttu-id="8806f-120">0</span><span class="sxs-lookup"><span data-stu-id="8806f-120">0</span></span>|<span data-ttu-id="8806f-121">Drehfeld-Waiting ist deaktiviert.</span><span class="sxs-lookup"><span data-stu-id="8806f-121">Spin-waiting is disabled.</span></span> <span data-ttu-id="8806f-122">Dies ist der Standardwert</span><span class="sxs-lookup"><span data-stu-id="8806f-122">This is the default</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="8806f-123">Untergeordnete Elemente</span><span class="sxs-lookup"><span data-stu-id="8806f-123">Child Elements</span></span>  
 <span data-ttu-id="8806f-124">Keine</span><span class="sxs-lookup"><span data-stu-id="8806f-124">None.</span></span>  
  
### <a name="parent-elements"></a><span data-ttu-id="8806f-125">Übergeordnete Elemente</span><span class="sxs-lookup"><span data-stu-id="8806f-125">Parent Elements</span></span>  
  
|<span data-ttu-id="8806f-126">Element</span><span class="sxs-lookup"><span data-stu-id="8806f-126">Element</span></span>|<span data-ttu-id="8806f-127">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="8806f-127">Description</span></span>|  
|-------------|-----------------|  
|`configuration`|<span data-ttu-id="8806f-128">Das Stammelement in jeder von den Common Language Runtime- und .NET Framework-Anwendungen verwendeten Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="8806f-128">The root element in every configuration file used by the common language runtime and .NET Framework applications.</span></span>|  
|`runtime`|<span data-ttu-id="8806f-129">Enthält Informationen über verschiedene Konfigurationseinstellungen für die Common Language Runtime.</span><span class="sxs-lookup"><span data-stu-id="8806f-129">Contains information about various runtime configuration settings.</span></span>|  
  
## <a name="example"></a><span data-ttu-id="8806f-130">Beispiel</span><span class="sxs-lookup"><span data-stu-id="8806f-130">Example</span></span>  

<span data-ttu-id="8806f-131">Das folgende Beispiel deaktiviert die Spin-Waiting in kritischen Abschnitten bei Konflikten.</span><span class="sxs-lookup"><span data-stu-id="8806f-131">The following example disables spin-waiting in critical sections when contended.</span></span>  
  
```xml  
<configuration>  
   <runtime>  
      <Crst_DisableSpinWait enabled="1"/>  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a><span data-ttu-id="8806f-132">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="8806f-132">See also</span></span>

- [<span data-ttu-id="8806f-133">Schema für Laufzeiteinstellungen</span><span class="sxs-lookup"><span data-stu-id="8806f-133">Runtime Settings Schema</span></span>](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)
- [<span data-ttu-id="8806f-134">Konfigurationsdateischema</span><span class="sxs-lookup"><span data-stu-id="8806f-134">Configuration File Schema</span></span>](../../../../../docs/framework/configure-apps/file-schema/index.md)