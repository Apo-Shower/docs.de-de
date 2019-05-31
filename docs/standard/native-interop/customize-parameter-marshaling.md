---
title: Anpassen des Marshallings für Parameter – .NET
description: Erfahren Sie, wie Sie anpassen können, wie .NET Ihre Parameter in eine native Darstellung marshallt.
author: jkoritzinsky
ms.author: jekoritz
ms.date: 01/18/2019
ms.openlocfilehash: 877eb00c18c9108fe6bcfb50104ff5ed813e85f3
ms.sourcegitcommit: ca2ca60e6f5ea327f164be7ce26d9599e0f85fe4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/06/2019
ms.locfileid: "65065973"
---
# <a name="customizing-parameter-marshaling"></a><span data-ttu-id="bb1cf-103">Anpassen des Marshallings für Parameter</span><span class="sxs-lookup"><span data-stu-id="bb1cf-103">Customizing parameter marshaling</span></span>

<span data-ttu-id="bb1cf-104">Wenn das standardmäßige Verhalten der .NET-Runtime beim Parametermarshalling nicht Ihren Vorstellungen entspricht, können Sie mithilfe des Attributs <xref:System.Runtime.InteropServices.MarshalAsAttribute?displayProperty=nameWithType> anpassen, wie Ihre Parameter gemarshallt werden.</span><span class="sxs-lookup"><span data-stu-id="bb1cf-104">When the .NET runtime's default parameter marshaling behavior doesn't do what you want, use can use the <xref:System.Runtime.InteropServices.MarshalAsAttribute?displayProperty=nameWithType> attribute to customize how your parameters are marshaled.</span></span>

## <a name="customizing-string-parameters"></a><span data-ttu-id="bb1cf-105">Anpassen von Zeichenfolgenparametern</span><span class="sxs-lookup"><span data-stu-id="bb1cf-105">Customizing string parameters</span></span>

<span data-ttu-id="bb1cf-106">.NET bietet eine Vielzahl von Formaten zum Marshalling von Zeichenfolgen.</span><span class="sxs-lookup"><span data-stu-id="bb1cf-106">.NET has a variety of formats for marshaling strings.</span></span> <span data-ttu-id="bb1cf-107">Diese Methoden werden in unterschiedliche Abschnitte für Zeichenfolgen im C-Stil und für Windows-orientierte Zeichenfolgenformate aufgeteilt.</span><span class="sxs-lookup"><span data-stu-id="bb1cf-107">These methods are split into distinct sections on C-style strings and Windows-centric string formats.</span></span>

### <a name="c-style-strings"></a><span data-ttu-id="bb1cf-108">Zeichenfolgen im C-Stil</span><span class="sxs-lookup"><span data-stu-id="bb1cf-108">C-Style strings</span></span>

<span data-ttu-id="bb1cf-109">Jedes dieser Formate übergibt eine null-terminierte Zeichenkette an den nativen Code.</span><span class="sxs-lookup"><span data-stu-id="bb1cf-109">Each of these formats passes a null-terminated string to native code.</span></span> <span data-ttu-id="bb1cf-110">Sie unterscheiden sich hinsichtlich der Codierung der nativen Zeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="bb1cf-110">They differ by the encoding of the native string.</span></span>

| <span data-ttu-id="bb1cf-111">`System.Runtime.InteropServices.UnmanagedType`-Wert</span><span class="sxs-lookup"><span data-stu-id="bb1cf-111">`System.Runtime.InteropServices.UnmanagedType` value</span></span> | <span data-ttu-id="bb1cf-112">Codierung</span><span class="sxs-lookup"><span data-stu-id="bb1cf-112">Encoding</span></span> |
|------------------------------------------------------|----------|
| <span data-ttu-id="bb1cf-113">LPStr</span><span class="sxs-lookup"><span data-stu-id="bb1cf-113">LPStr</span></span> | <span data-ttu-id="bb1cf-114">ANSI</span><span class="sxs-lookup"><span data-stu-id="bb1cf-114">ANSI</span></span> |
| <span data-ttu-id="bb1cf-115">LPUTF8Str</span><span class="sxs-lookup"><span data-stu-id="bb1cf-115">LPUTF8Str</span></span> | <span data-ttu-id="bb1cf-116">UTF-8</span><span class="sxs-lookup"><span data-stu-id="bb1cf-116">UTF-8</span></span> | 
| <span data-ttu-id="bb1cf-117">LPWStr</span><span class="sxs-lookup"><span data-stu-id="bb1cf-117">LPWStr</span></span> | <span data-ttu-id="bb1cf-118">UTF-16</span><span class="sxs-lookup"><span data-stu-id="bb1cf-118">UTF-16</span></span> |
| <span data-ttu-id="bb1cf-119">LPTStr</span><span class="sxs-lookup"><span data-stu-id="bb1cf-119">LPTStr</span></span> | <span data-ttu-id="bb1cf-120">UTF-16</span><span class="sxs-lookup"><span data-stu-id="bb1cf-120">UTF-16</span></span> |

<span data-ttu-id="bb1cf-121">Das <xref:System.Runtime.InteropServices.UnmanagedType.VBByRefStr?displayProperty=nameWithType>-Format ist etwas anders.</span><span class="sxs-lookup"><span data-stu-id="bb1cf-121">The <xref:System.Runtime.InteropServices.UnmanagedType.VBByRefStr?displayProperty=nameWithType> format is slightly different.</span></span> <span data-ttu-id="bb1cf-122">Genauso wie `LPWStr` marshallt es die Zeichenfolge in eine native C-Stil-Zeichenfolge, die in UTF-16 codiert ist.</span><span class="sxs-lookup"><span data-stu-id="bb1cf-122">Like `LPWStr`, it marshals the string to a native C-style string encoded in UTF-16.</span></span> <span data-ttu-id="bb1cf-123">Die verwaltete Signatur lässt Sie jedoch die Zeichenfolge nach Referenz übergeben und die passende native Signatur übernimmt die Zeichenfolge nach Wert.</span><span class="sxs-lookup"><span data-stu-id="bb1cf-123">However, the managed signature has you pass in the string by reference and the matching native signature takes the string by value.</span></span> <span data-ttu-id="bb1cf-124">Diese Unterscheidung ermöglicht es Ihnen, eine native API zu verwenden, die eine Zeichenfolge nach Wert übernimmt und an Ort und Stelle ändert, ohne einen `StringBuilder` verwenden zu müssen.</span><span class="sxs-lookup"><span data-stu-id="bb1cf-124">This distinction allows you to use a native API that takes a string by value and modifies it in-place without having to use a `StringBuilder`.</span></span> <span data-ttu-id="bb1cf-125">Wir empfehlen, dieses Format nicht manuell zu verwenden, da es zu Verwechslungen mit den nicht übereinstimmenden nativen und verwalteten Signaturen führen kann.</span><span class="sxs-lookup"><span data-stu-id="bb1cf-125">We recommend against manually using this format since it's prone to cause confusion with the mismatching native and managed signatures.</span></span>

### <a name="windows-centric-string-formats"></a><span data-ttu-id="bb1cf-126">Windows-orientierte Zeichenfolgenformate</span><span class="sxs-lookup"><span data-stu-id="bb1cf-126">Windows-centric string formats</span></span>

<span data-ttu-id="bb1cf-127">Wenn Sie mit COM- oder OLE-Schnittstellen interagieren, werden Sie wahrscheinlich feststellen, dass die nativen Funktionen Zeichenfolgen als `BSTR`-Argumente verwenden.</span><span class="sxs-lookup"><span data-stu-id="bb1cf-127">When interacting with COM or OLE interfaces, you'll likely find that the native functions take strings as `BSTR` arguments.</span></span> <span data-ttu-id="bb1cf-128">Sie können den nicht verwalteten Typ <xref:System.Runtime.InteropServices.UnmanagedType.BStr?displayProperty=nameWithType> verwenden, um eine Zeichenfolge als `BSTR` zu marshallen.</span><span class="sxs-lookup"><span data-stu-id="bb1cf-128">You can use the <xref:System.Runtime.InteropServices.UnmanagedType.BStr?displayProperty=nameWithType> unmanaged type to marshal a string as a `BSTR`.</span></span>

<span data-ttu-id="bb1cf-129">Wenn Sie mit WinRT-APIs interagieren, können Sie das Format <xref:System.Runtime.InteropServices.UnmanagedType.HString?displayProperty=nameWithType> verwenden, um eine Zeichenfolge als `HSTRING` marshallen.</span><span class="sxs-lookup"><span data-stu-id="bb1cf-129">If you're interacting with WinRT APIs, you can use the <xref:System.Runtime.InteropServices.UnmanagedType.HString?displayProperty=nameWithType> format to marshal a string as an `HSTRING`.</span></span>

## <a name="customizing-array-parameters"></a><span data-ttu-id="bb1cf-130">Anpassen von Arrayparametern</span><span class="sxs-lookup"><span data-stu-id="bb1cf-130">Customizing array parameters</span></span>

<span data-ttu-id="bb1cf-131">.NET bietet Ihnen außerdem mehrere Möglichkeiten zum Marshallen von Arrayparametern.</span><span class="sxs-lookup"><span data-stu-id="bb1cf-131">.NET also provides you multiple ways to marshal array parameters.</span></span> <span data-ttu-id="bb1cf-132">Wenn Sie eine API aufrufen, die ein Array im C-Stil verwendet, verwenden Sie den nicht verwalteten Typ <xref:System.Runtime.InteropServices.UnmanagedType.LPArray?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="bb1cf-132">If you're calling an API that takes a C-style array, use the <xref:System.Runtime.InteropServices.UnmanagedType.LPArray?displayProperty=nameWithType> unmanaged type.</span></span> <span data-ttu-id="bb1cf-133">Wenn die Werte im Array benutzerdefiniertes Marshalling benötigen, können Sie dafür das Feld <xref:System.Runtime.InteropServices.MarshalAsAttribute.ArraySubType> im Attribut `[MarshalAs]` verwenden.</span><span class="sxs-lookup"><span data-stu-id="bb1cf-133">If the values in the array need customized marshaling, you can use the <xref:System.Runtime.InteropServices.MarshalAsAttribute.ArraySubType> field on the `[MarshalAs]` attribute for that.</span></span>

<span data-ttu-id="bb1cf-134">Wenn Sie COM-APIs verwenden, müssen Sie Ihre Arrayparameter wahrscheinlich als `SAFEARRAY*` marshallen.</span><span class="sxs-lookup"><span data-stu-id="bb1cf-134">If you're using COM APIs, you'll likely have to marshal your array parameters as `SAFEARRAY*`s.</span></span> <span data-ttu-id="bb1cf-135">Dafür können Sie den nicht verwalteten Typ <xref:System.Runtime.InteropServices.UnmanagedType.SafeArray?displayProperty=nameWithType> verwenden.</span><span class="sxs-lookup"><span data-stu-id="bb1cf-135">To do so, you can use the <xref:System.Runtime.InteropServices.UnmanagedType.SafeArray?displayProperty=nameWithType> unmanaged type.</span></span> <span data-ttu-id="bb1cf-136">Der Standardtyp der Elemente von `SAFEARRAY` werden in der Tabelle in den Feldern [Anpassen`object` angezeigt](./customize-struct-marshaling.md#marshaling-systemobjects).</span><span class="sxs-lookup"><span data-stu-id="bb1cf-136">The default type of the elements of the `SAFEARRAY` can be seen in the table on [customizing `object` fields](./customize-struct-marshaling.md#marshaling-systemobjects).</span></span> <span data-ttu-id="bb1cf-137">Sie können die Felder <xref:System.Runtime.InteropServices.MarshalAsAttribute.SafeArraySubType?displayProperty=nameWithType> und <xref:System.Runtime.InteropServices.MarshalAsAttribute.SafeArrayUserDefinedSubType?displayProperty=nameWithType> verwenden, um den genauen Elementtyp von `SAFEARRAY` anzupassen.</span><span class="sxs-lookup"><span data-stu-id="bb1cf-137">You can use the <xref:System.Runtime.InteropServices.MarshalAsAttribute.SafeArraySubType?displayProperty=nameWithType> and <xref:System.Runtime.InteropServices.MarshalAsAttribute.SafeArrayUserDefinedSubType?displayProperty=nameWithType> fields to customize the exact element type of the `SAFEARRAY`.</span></span>

## <a name="customizing-boolean-or-decimal-parameters"></a><span data-ttu-id="bb1cf-138">Anpassen von booleschen oder dezimalen Parametern</span><span class="sxs-lookup"><span data-stu-id="bb1cf-138">Customizing boolean or decimal parameters</span></span>

<span data-ttu-id="bb1cf-139">Informationen zum Marshalling boolescher oder dezimaler Parameter finden Sie unter [Anpassen des Marshallings für Strukturen](customize-struct-marshaling.md).</span><span class="sxs-lookup"><span data-stu-id="bb1cf-139">For information on marshaling boolean or decimal parameters, see [Customizing structure marshaling](customize-struct-marshaling.md).</span></span>

## <a name="customizing-object-parameters-windows-only"></a><span data-ttu-id="bb1cf-140">Anpassen der Objektparameter (nur Windows)</span><span class="sxs-lookup"><span data-stu-id="bb1cf-140">Customizing object parameters (Windows-only)</span></span>

<span data-ttu-id="bb1cf-141">Unter Windows bietet die.NET-Runtime eine Reihe von verschiedenen Möglichkeiten zum Marshallen von Objektparametern in nativen Code.</span><span class="sxs-lookup"><span data-stu-id="bb1cf-141">On Windows, the .NET runtime provides a number of different ways to marshal object parameters to native code.</span></span>

### <a name="marshaling-as-specific-com-interfaces"></a><span data-ttu-id="bb1cf-142">Marshalling als bestimmte COM-Schnittstellen</span><span class="sxs-lookup"><span data-stu-id="bb1cf-142">Marshaling as specific COM interfaces</span></span>

<span data-ttu-id="bb1cf-143">Wenn Ihre API einen Zeiger auf ein COM-Objekt übernimmt, können Sie eines der folgenden `UnmanagedType`-Formate auf einem `object`-typisierten Parameter verwenden, damit .NET als diese spezifischen Schnittstellen marshallt.</span><span class="sxs-lookup"><span data-stu-id="bb1cf-143">If your API takes a pointer to a COM object, you can use any of the following `UnmanagedType` formats on an `object`-typed parameter to tell .NET to marshal as these specific interfaces:</span></span>

- `IUnknown`
- `IDispatch`
- `IInspectable`

<span data-ttu-id="bb1cf-144">Wenn Ihr Typ außerdem mit `[ComVisible(true)]` markiert ist oder Sie ein Marshalling des Typs `object` durchführen, können Sie das Format <xref:System.Runtime.InteropServices.UnmanagedType.Interface?displayProperty=nameWithType> verwenden, um Ihr Objekt als COM Callable Wrapper für die COM-Ansicht Ihres Typs darzustellen.</span><span class="sxs-lookup"><span data-stu-id="bb1cf-144">Additionally, if your type is marked `[ComVisible(true)]` or you're marshaling the `object` type, you can use the <xref:System.Runtime.InteropServices.UnmanagedType.Interface?displayProperty=nameWithType> format to marshal your object as a COM callable wrapper for the COM view of your type.</span></span>

### <a name="marshaling-to-a-variant"></a><span data-ttu-id="bb1cf-145">Marshalling zu einer `VARIANT`</span><span class="sxs-lookup"><span data-stu-id="bb1cf-145">Marshaling to a `VARIANT`</span></span>

<span data-ttu-id="bb1cf-146">Wenn Ihre native API eine Win32-`VARIANT` verwendet, können Sie das <xref:System.Runtime.InteropServices.UnmanagedType.Struct?displayProperty=nameWithType>-Format für Ihren `object`-Parameter verwenden, um Ihre Objekte als `VARIANT` zu marshallen.</span><span class="sxs-lookup"><span data-stu-id="bb1cf-146">If your native API takes a Win32 `VARIANT`, you can use the <xref:System.Runtime.InteropServices.UnmanagedType.Struct?displayProperty=nameWithType> format on your `object` parameter to marshal your objects as `VARIANT`s.</span></span> <span data-ttu-id="bb1cf-147">Informationen zur Zuordnung zwischen .NET-Typen und `VARIANT`-Typen finden Sie in der Dokumentation zum [Anpassen von `object`-Feldern](customize-struct-marshaling.md#marshaling-systemobjects).</span><span class="sxs-lookup"><span data-stu-id="bb1cf-147">See the documentation on [customizing `object` fields](customize-struct-marshaling.md#marshaling-systemobjects) for a mapping between .NET types and `VARIANT` types.</span></span>

### <a name="custom-marshalers"></a><span data-ttu-id="bb1cf-148">Benutzerdefinierte Marshaller</span><span class="sxs-lookup"><span data-stu-id="bb1cf-148">Custom marshalers</span></span>

<span data-ttu-id="bb1cf-149">Wenn Sie eine native COM-Schnittstelle in einen anderen verwalteten Typ projizieren möchten, können Sie das Format `UnmanagedType.CustomMarshaler` und eine Implementierung von <xref:System.Runtime.InteropServices.ICustomMarshaler> verwenden, um Ihren eigenen benutzerdefinierten Marshallingcode bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="bb1cf-149">If you want to project a native COM interface into a different managed type, you can use the `UnmanagedType.CustomMarshaler` format and an implementation of <xref:System.Runtime.InteropServices.ICustomMarshaler> to provide your own custom marshaling code.</span></span>