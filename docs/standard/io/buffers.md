---
title: System.Buffers – .NET
ms.date: 12/05/2019
ms.technology: dotnet-standard
helpviewer_keywords:
- buffers [.NET]
- I/O [.NET], buffers
author: rick-anderson
ms.author: riande
ms.openlocfilehash: e42f165bfedec3b1fa54615ee7e2a2028f40aadb
ms.sourcegitcommit: 42ed59871db1f29a32b3d8e7abeb20e6eceeda7c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/10/2019
ms.locfileid: "74960474"
---
# <a name="work-with-buffers-in-net"></a><span data-ttu-id="a57e7-102">Arbeiten mit Puffern in .NET</span><span class="sxs-lookup"><span data-stu-id="a57e7-102">Work with Buffers in .NET</span></span>

<span data-ttu-id="a57e7-103">Dieser Artikel bietet eine Übersicht über die Typen, die das Lesen von Daten unterstützen, die über mehrere Puffer hinweg ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="a57e7-103">This article provides an overview of types that help read data that runs across multiple buffers.</span></span> <span data-ttu-id="a57e7-104">Sie werden hauptsächlich zur Unterstützung von <xref:System.IO.Pipelines.PipeReader>-Objekten verwendet.</span><span class="sxs-lookup"><span data-stu-id="a57e7-104">They're primarily used to support <xref:System.IO.Pipelines.PipeReader> objects.</span></span>

## <a name="ibufferwritert"></a><span data-ttu-id="a57e7-105">IBufferWriter\<T\></span><span class="sxs-lookup"><span data-stu-id="a57e7-105">IBufferWriter\<T\></span></span>

<span data-ttu-id="a57e7-106"><xref:System.Buffers.IBufferWriter%601?displayProperty=fullName> ist ein Vertrag für synchrone gepufferte Schreibvorgänge.</span><span class="sxs-lookup"><span data-stu-id="a57e7-106"><xref:System.Buffers.IBufferWriter%601?displayProperty=fullName> is a contract for synchronous buffered writing.</span></span> <span data-ttu-id="a57e7-107">Auf niedrigster Ebene gilt Folgendes für die Schnittstelle:</span><span class="sxs-lookup"><span data-stu-id="a57e7-107">At the lowest level, the interface:</span></span>

- <span data-ttu-id="a57e7-108">Sie ist einfach zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="a57e7-108">Is basic and not difficult to use.</span></span>
- <span data-ttu-id="a57e7-109">Sie bietet Zugriff auf <xref:System.Memory%601>- oder <xref:System.Span%601>-Elemente.</span><span class="sxs-lookup"><span data-stu-id="a57e7-109">Allows access to a <xref:System.Memory%601> or <xref:System.Span%601>.</span></span> <span data-ttu-id="a57e7-110">`Memory<T>` und `Span<T>` erlauben Schreibvorgänge, und Sie können ermitteln, wie viele `T`-Elemente geschrieben wurden.</span><span class="sxs-lookup"><span data-stu-id="a57e7-110">The `Memory<T>` or `Span<T>` can be written to and you can determine how many `T` items were written.</span></span>

[!code-csharp[](~/samples/snippets/csharp/buffers/MyClass.cs?name=snippet)]

<span data-ttu-id="a57e7-111">Für die oben genannte Methode gilt:</span><span class="sxs-lookup"><span data-stu-id="a57e7-111">The preceding method:</span></span>

- <span data-ttu-id="a57e7-112">Fordert einen Puffer mit mindestens 5 Bytes von `IBufferWriter<byte>` unter Verwendung von `GetSpan(5)` an.</span><span class="sxs-lookup"><span data-stu-id="a57e7-112">Requests a buffer of at least 5 bytes from the `IBufferWriter<byte>` using `GetSpan(5)`.</span></span>
- <span data-ttu-id="a57e7-113">Sie schreibt Bytes für die ASCII-Zeichenfolge „Hello“ in das zurückgegebene `Span<byte>`-Element.</span><span class="sxs-lookup"><span data-stu-id="a57e7-113">Writes bytes for the ASCII string "Hello" to the returned `Span<byte>`.</span></span>
- <span data-ttu-id="a57e7-114">Sie ruft <xref:System.Buffers.IBufferWriter%601> auf, um anzugeben, wie viele Bytes in den Puffer geschrieben wurden.</span><span class="sxs-lookup"><span data-stu-id="a57e7-114">Calls  <xref:System.Buffers.IBufferWriter%601> to indicate how many bytes were written to the buffer.</span></span>

<span data-ttu-id="a57e7-115">Diese Methode zum Schreiben verwendet die Puffer `Memory<T>`/`Span<T>`, die von `IBufferWriter<T>` bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="a57e7-115">This method of writing uses the `Memory<T>`/`Span<T>` buffer provided by the `IBufferWriter<T>`.</span></span> <span data-ttu-id="a57e7-116">Alternativ dazu kann die Erweiterungsmethode <xref:System.Buffers.BuffersExtensions.Write%2A> verwendet werden, um einen vorhandenen Puffer in das `IBufferWriter<T>`-Element zu kopieren.</span><span class="sxs-lookup"><span data-stu-id="a57e7-116">Alternatively, the <xref:System.Buffers.BuffersExtensions.Write%2A> extension method can be used to copy an existing buffer to the `IBufferWriter<T>`.</span></span> <span data-ttu-id="a57e7-117">`Write` ruft `GetSpan`/`Advance` je nach Bedarf auf, daher muss nach dem Schreiben `Advance` nicht aufgerufen werden:</span><span class="sxs-lookup"><span data-stu-id="a57e7-117">`Write` does the work of calling `GetSpan`/`Advance` as appropriate, so there's no need to call `Advance` after writing:</span></span>

[!code-csharp[](~/samples/snippets/csharp/buffers/MyClass.cs?name=snippet2)]

<span data-ttu-id="a57e7-118"><xref:System.Buffers.ArrayBufferWriter%601> ist eine Implementierung des `IBufferWriter<T>`-Elements, dessen Sicherungsspeicher ein einzelnes zusammenhängendes Array ist.</span><span class="sxs-lookup"><span data-stu-id="a57e7-118"><xref:System.Buffers.ArrayBufferWriter%601> is an implementation of `IBufferWriter<T>` whose backing store is a single contiguous array.</span></span>

### <a name="ibufferwriter-common-problems"></a><span data-ttu-id="a57e7-119">Häufige IBufferWriter-Probleme</span><span class="sxs-lookup"><span data-stu-id="a57e7-119">IBufferWriter common problems</span></span>

- <span data-ttu-id="a57e7-120">`GetSpan` und `GetMemory` geben einen Puffer mit mindestens der angeforderten Menge an Arbeitsspeicher zurück.</span><span class="sxs-lookup"><span data-stu-id="a57e7-120">`GetSpan` and `GetMemory` return a buffer with at least the requested amount of memory.</span></span> <span data-ttu-id="a57e7-121">Gehen Sie nicht von genauen Puffergrößen aus.</span><span class="sxs-lookup"><span data-stu-id="a57e7-121">Don't assume exact buffer sizes.</span></span>
- <span data-ttu-id="a57e7-122">Es gibt keine Garantie, dass aufeinanderfolgende Aufrufe denselben Puffer oder dieselbe Puffergröße zurückgeben.</span><span class="sxs-lookup"><span data-stu-id="a57e7-122">There's no guarantee that successive calls will return the same buffer or the same-sized buffer.</span></span>
- <span data-ttu-id="a57e7-123">Nach dem Aufrufen von `Advance` muss ein neuer Puffer angefordert werden, um das Schreiben weiterer Daten fortzusetzen.</span><span class="sxs-lookup"><span data-stu-id="a57e7-123">A new buffer must be requested after calling `Advance` to continue writing more data.</span></span> <span data-ttu-id="a57e7-124">In einen zuvor abgerufenen Puffer kann erst nach dem Aufruf von `Advance` geschrieben werden.</span><span class="sxs-lookup"><span data-stu-id="a57e7-124">A previously acquired buffer cannot be written to after `Advance` has been called.</span></span>

## <a name="readonlysequencet"></a><span data-ttu-id="a57e7-125">ReadOnlySequence\<T\></span><span class="sxs-lookup"><span data-stu-id="a57e7-125">ReadOnlySequence\<T\></span></span>

![ReadOnlySequence mit Arbeitsspeicher in der Pipe, darunter die Sequenzposition des schreibgeschützten Arbeitsspeichers](media/buffers/ro-sequence.png)

<span data-ttu-id="a57e7-127"><xref:System.Buffers.ReadOnlySequence%601> ist eine Struktur, die eine zusammenhängende oder eine nicht zusammenhängende Sequenz von `T` darstellen kann.</span><span class="sxs-lookup"><span data-stu-id="a57e7-127"><xref:System.Buffers.ReadOnlySequence%601> is a struct that can represent a contiguous or noncontiguous sequence of `T`.</span></span> <span data-ttu-id="a57e7-128">Sie kann aus Folgendem erstellt werden:</span><span class="sxs-lookup"><span data-stu-id="a57e7-128">It can be constructed from:</span></span>

1. <span data-ttu-id="a57e7-129">Eine `T[]`</span><span class="sxs-lookup"><span data-stu-id="a57e7-129">A `T[]`</span></span>
1. <span data-ttu-id="a57e7-130">Eine `ReadOnlyMemory<T>`</span><span class="sxs-lookup"><span data-stu-id="a57e7-130">A `ReadOnlyMemory<T>`</span></span>
1. <span data-ttu-id="a57e7-131">Ein Paar aus einem verknüpften Listenknoten <xref:System.Buffers.ReadOnlySequenceSegment%601> und einem Index zum Darstellen der Start- und Endposition der Sequenz.</span><span class="sxs-lookup"><span data-stu-id="a57e7-131">A pair of linked list node <xref:System.Buffers.ReadOnlySequenceSegment%601> and index to represent the start and end position of the sequence.</span></span>

<span data-ttu-id="a57e7-132">Die dritte Darstellung ist die interessanteste, da sie sich auf die Leistung verschiedener Vorgänge in `ReadOnlySequence<T>` auswirkt:</span><span class="sxs-lookup"><span data-stu-id="a57e7-132">The third representation is the most interesting one as it has performance implications on various operations on the `ReadOnlySequence<T>`:</span></span>

|<span data-ttu-id="a57e7-133">Darstellung</span><span class="sxs-lookup"><span data-stu-id="a57e7-133">Representation</span></span>|<span data-ttu-id="a57e7-134">Vorgang</span><span class="sxs-lookup"><span data-stu-id="a57e7-134">Operation</span></span>|<span data-ttu-id="a57e7-135">Komplexität</span><span class="sxs-lookup"><span data-stu-id="a57e7-135">Complexity</span></span>|
---|---|---|
|`T[]`/`ReadOnlyMemory<T>`|`Length`|`O(1)`|
|`T[]`/`ReadOnlyMemory<T>`|`GetPosition(long)`|`O(1)`|
|`T[]`/`ReadOnlyMemory<T>`|`Slice(int, int)`|`O(1)`|
|`T[]`/`ReadOnlyMemory<T>`|`Slice(SequencePostion,  SequencePostion)`|`O(1)`|
|`ReadOnlySequenceSegment<T>`|`Length`|`O(1)`|
|`ReadOnlySequenceSegment<T>`|`GetPosition(long)`|`O(number of segments)`|
|`ReadOnlySequenceSegment<T>`|`Slice(int, int)`|`O(number of segments)`|
|`ReadOnlySequenceSegment<T>`|`Slice(SequencePostion, SequencePostion)`|`O(1)`|

<span data-ttu-id="a57e7-136">Aufgrund dieser gemischten Darstellung macht `ReadOnlySequence<T>` Indizes als `SequencePosition` anstelle einer Ganzzahl verfügbar.</span><span class="sxs-lookup"><span data-stu-id="a57e7-136">Because of this mixed representation, the `ReadOnlySequence<T>` exposes indexes as `SequencePosition` instead of an integer.</span></span> <span data-ttu-id="a57e7-137">Für eine `SequencePosition` gilt:</span><span class="sxs-lookup"><span data-stu-id="a57e7-137">A `SequencePosition`:</span></span>

- <span data-ttu-id="a57e7-138">Es handelt sich um einen nicht transparenten Wert, der einen Index für das `ReadOnlySequence<T>`-Element darstellt, aus dem der Wert stammt.</span><span class="sxs-lookup"><span data-stu-id="a57e7-138">Is an opaque value that represents an index into the `ReadOnlySequence<T>` where it originated.</span></span>
- <span data-ttu-id="a57e7-139">Sie besteht aus zwei Teilen: einer Ganzzahl und einem Objekt.</span><span class="sxs-lookup"><span data-stu-id="a57e7-139">Consists of two parts, an integer and an object.</span></span> <span data-ttu-id="a57e7-140">Die Darstellung dieser beiden Werte ist an die Implementierung von `ReadOnlySequence<T>` gebunden.</span><span class="sxs-lookup"><span data-stu-id="a57e7-140">What these two values represent are tied to the implementation of `ReadOnlySequence<T>`.</span></span>

### <a name="access-data"></a><span data-ttu-id="a57e7-141">Zugriff auf Daten</span><span class="sxs-lookup"><span data-stu-id="a57e7-141">Access data</span></span>

<span data-ttu-id="a57e7-142">`ReadOnlySequence<T>` macht Daten als aufzählbares Element von `ReadOnlyMemory<T>` verfügbar.</span><span class="sxs-lookup"><span data-stu-id="a57e7-142">The `ReadOnlySequence<T>` exposes data as an enumerable of `ReadOnlyMemory<T>`.</span></span> <span data-ttu-id="a57e7-143">Die Aufzählung jedes der Segmente kann mithilfe eines einfachen foreach-Vorgangs durchgeführt werden:</span><span class="sxs-lookup"><span data-stu-id="a57e7-143">Enumerating each of the segments can be done using a basic foreach:</span></span>

[!code-csharp[](~/samples/snippets/csharp/buffers/MyClass.cs?name=snippet3)]

<span data-ttu-id="a57e7-144">Die oben genannte Methode durchsucht jedes Segment nach einem bestimmten Byte.</span><span class="sxs-lookup"><span data-stu-id="a57e7-144">The preceding method searches each segment for a specific byte.</span></span> <span data-ttu-id="a57e7-145">Wenn Sie die `SequencePosition` jedes Segments nachverfolgen müssen, ist <xref:System.Buffers.ReadOnlySequence%601.TryGet%2A?displayProperty=nameWithType> besser geeignet.</span><span class="sxs-lookup"><span data-stu-id="a57e7-145">If you need to keep track of each segment's `SequencePosition`, <xref:System.Buffers.ReadOnlySequence%601.TryGet%2A?displayProperty=nameWithType> is more appropriate.</span></span> <span data-ttu-id="a57e7-146">Das nächste Beispiel ändert den oben stehenden Code so, dass anstelle einer Ganzzahl eine `SequencePosition` zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="a57e7-146">The next sample changes the preceding code to return a `SequencePosition` instead of an integer.</span></span> <span data-ttu-id="a57e7-147">Die Rückgabe einer `SequencePosition` bietet den Vorteil, dass die aufrufende Funktion keine zweite Überprüfung durchführen muss, um die Daten an einer bestimmten Indexposition abzurufen.</span><span class="sxs-lookup"><span data-stu-id="a57e7-147">Returning a `SequencePosition` has the benefit of allowing the caller to avoid a second scan to get the data at a specific index.</span></span>

[!code-csharp[](~/samples/snippets/csharp/buffers/MyClass.cs?name=snippet4)]

<span data-ttu-id="a57e7-148">Die Kombination aus `SequencePosition` und `TryGet` fungiert wie ein Enumerator.</span><span class="sxs-lookup"><span data-stu-id="a57e7-148">The combination of `SequencePosition` and `TryGet` acts like an enumerator.</span></span> <span data-ttu-id="a57e7-149">Das Positionsfeld wird beim Start jeder Iteration so geändert, dass es als Start jedes Segments innerhalb des `ReadOnlySequence<T>`-Elements dient.</span><span class="sxs-lookup"><span data-stu-id="a57e7-149">The position field is modified at the start of each iteration to be start of each segment within the `ReadOnlySequence<T>`.</span></span>

<span data-ttu-id="a57e7-150">Die oben beschriebene Methode ist als Erweiterungsmethode in `ReadOnlySequence<T>` vorhanden.</span><span class="sxs-lookup"><span data-stu-id="a57e7-150">The preceding method exists as an extension method on `ReadOnlySequence<T>`.</span></span> <span data-ttu-id="a57e7-151"><xref:System.Buffers.BuffersExtensions.PositionOf%2A> kann zur Vereinfachung des vorherigen Codes verwendet werden:</span><span class="sxs-lookup"><span data-stu-id="a57e7-151"><xref:System.Buffers.BuffersExtensions.PositionOf%2A> can be used to simplify the preceding code:</span></span>

```csharp
SequencePosition? FindIndexOf(in ReadOnlySequence<byte> buffer, byte data) => buffer.PositionOf(data);
```

#### <a name="process-a-readonlysequencet"></a><span data-ttu-id="a57e7-152">Verarbeiten eines ReadOnlySequence\<T\>-Elements</span><span class="sxs-lookup"><span data-stu-id="a57e7-152">Process a ReadOnlySequence\<T\></span></span>

<span data-ttu-id="a57e7-153">Die Verarbeitung eines `ReadOnlySequence<T>`-Elements kann schwierig sein, weil Daten möglicherweise auf mehrere Segmente innerhalb der Sequenz aufgeteilt sind.</span><span class="sxs-lookup"><span data-stu-id="a57e7-153">Processing a `ReadOnlySequence<T>` can be challenging since data may be split across multiple segments within the sequence.</span></span> <span data-ttu-id="a57e7-154">Um die bestmögliche Leistung zu erzielen, teilen Sie den Code in zwei Pfade auf:</span><span class="sxs-lookup"><span data-stu-id="a57e7-154">For the best performance, split code into two paths:</span></span>

- <span data-ttu-id="a57e7-155">Ein schneller Pfad, der den Fall eines einzelnen Segments verarbeitet.</span><span class="sxs-lookup"><span data-stu-id="a57e7-155">A fast path that deals with the single segment case.</span></span>
- <span data-ttu-id="a57e7-156">Ein langsamer Pfad, der auf Segmente aufgeteilte Daten verarbeitet.</span><span class="sxs-lookup"><span data-stu-id="a57e7-156">A slow path that deals with the data split across segments.</span></span>

<span data-ttu-id="a57e7-157">Zur Verarbeitung von Daten in Sequenzen mit mehreren Segmenten können verschiedene Ansätze verwendet werden:</span><span class="sxs-lookup"><span data-stu-id="a57e7-157">There are a few approaches that can be used to process data in multi-segmented sequences:</span></span>

- <span data-ttu-id="a57e7-158">Verwenden Sie das [`SequenceReader<T>`](#sequencereadert)-Element.</span><span class="sxs-lookup"><span data-stu-id="a57e7-158">Use the [`SequenceReader<T>`](#sequencereadert).</span></span>
- <span data-ttu-id="a57e7-159">Analysieren Sie Daten segmentweise, und verfolgen Sie die `SequencePosition` und den Index innerhalb des analysierten Segments nach.</span><span class="sxs-lookup"><span data-stu-id="a57e7-159">Parse data segment by segment, keeping track of the `SequencePosition` and index within the segment parsed.</span></span> <span data-ttu-id="a57e7-160">Dieses Vorgehen vermeidet unnötige Zuteilungen, ist aber insbesondere für kleine Puffer möglicherweise ineffizient.</span><span class="sxs-lookup"><span data-stu-id="a57e7-160">This avoids unnecessary allocations but may be inefficient, especially for small buffers.</span></span>
- <span data-ttu-id="a57e7-161">Kopieren Sie das `ReadOnlySequence<T>`-Element in ein zusammenhängendes Array, und behandeln Sie es wie einen einzelnen Puffer:</span><span class="sxs-lookup"><span data-stu-id="a57e7-161">Copy the `ReadOnlySequence<T>` to a contiguous array and treat it like a single buffer:</span></span>
  - <span data-ttu-id="a57e7-162">Wenn das `ReadOnlySequence<T>`-Element klein ist, kann es sinnvoll sein, die Daten mithilfe des [stackalloc](../../csharp/language-reference/operators/stackalloc.md)-Operators in einen Puffer mit Stapelzuordnung zu kopieren.</span><span class="sxs-lookup"><span data-stu-id="a57e7-162">If the size of the `ReadOnlySequence<T>` is small, it may be reasonable to copy the data into a stack-allocated buffer using the [stackalloc](../../csharp/language-reference/operators/stackalloc.md) operator.</span></span>
  - <span data-ttu-id="a57e7-163">Kopieren Sie das `ReadOnlySequence<T>`-Element mithilfe von <xref:System.Buffers.ArrayPool%601.Shared%2A?displayProperty=nameWithType> in ein in einem Pool zusammengefasstes Array.</span><span class="sxs-lookup"><span data-stu-id="a57e7-163">Copy the `ReadOnlySequence<T>` into a pooled array using <xref:System.Buffers.ArrayPool%601.Shared%2A?displayProperty=nameWithType>.</span></span>
  - <span data-ttu-id="a57e7-164">Verwenden Sie [`ReadOnlySequence<T>.ToArray()`](xref:System.Buffers.BuffersExtensions.ToArray%2A).</span><span class="sxs-lookup"><span data-stu-id="a57e7-164">Use [`ReadOnlySequence<T>.ToArray()`](xref:System.Buffers.BuffersExtensions.ToArray%2A).</span></span> <span data-ttu-id="a57e7-165">Dies ist im langsamsten Pfad nicht empfehlenswert, da dadurch ein neues `T[]`-Element im Heap zugewiesen wird.</span><span class="sxs-lookup"><span data-stu-id="a57e7-165">This isn't recommended in hot paths as it allocates a new `T[]` on the heap.</span></span>

<span data-ttu-id="a57e7-166">Die folgenden Beispiele veranschaulichen einige gängige Fälle für die Verarbeitung von `ReadOnlySequence<byte>`:</span><span class="sxs-lookup"><span data-stu-id="a57e7-166">The following examples demonstrate some common cases for processing `ReadOnlySequence<byte>`:</span></span>

##### <a name="process-binary-data"></a><span data-ttu-id="a57e7-167">Verarbeiten von Binärdaten</span><span class="sxs-lookup"><span data-stu-id="a57e7-167">Process binary data</span></span>

<span data-ttu-id="a57e7-168">Das folgende Beispiel analysiert eine 4 Byte lange Big-Endian-Ganzzahl ab dem Start des `ReadOnlySequence<byte>`-Elements.</span><span class="sxs-lookup"><span data-stu-id="a57e7-168">The following example parses a 4-byte big-endian integer length from the start of the `ReadOnlySequence<byte>`.</span></span>

[!code-csharp[](~/samples/snippets/csharp/buffers/MyClass.cs?name=snippet5)]

##### <a name="process-text-data"></a><span data-ttu-id="a57e7-169">Verarbeiten von Textdaten</span><span class="sxs-lookup"><span data-stu-id="a57e7-169">Process text data</span></span>

<span data-ttu-id="a57e7-170">Im Beispiel unten geschieht Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a57e7-170">The following example:</span></span>

- <span data-ttu-id="a57e7-171">Die erste neue Zeile (`\r\n`) in `ReadOnlySequence<byte>` wird gefunden und über den Ausgabeparameter „line“ zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="a57e7-171">Finds the first newline (`\r\n`) in the `ReadOnlySequence<byte>` and returns it via the out 'line' parameter.</span></span>
- <span data-ttu-id="a57e7-172">Diese Zeile wird abgeschnitten, dabei wird die Zeichenfolge `\r\n` aus dem Eingabepuffer ausgeschlossen.</span><span class="sxs-lookup"><span data-stu-id="a57e7-172">Trims that line, excluding the `\r\n` from the input buffer.</span></span>

[!code-csharp[](~/samples/snippets/csharp/buffers/MyClass.cs?name=snippet6)]

##### <a name="empty-segments"></a><span data-ttu-id="a57e7-173">Leere Segmente</span><span class="sxs-lookup"><span data-stu-id="a57e7-173">Empty segments</span></span>

<span data-ttu-id="a57e7-174">Es ist möglich, leere Segmente in einem `ReadOnlySequence<T>`-Element zu speichern.</span><span class="sxs-lookup"><span data-stu-id="a57e7-174">It's valid to store empty segments inside of a `ReadOnlySequence<T>`.</span></span> <span data-ttu-id="a57e7-175">Leere Segmente können beim expliziten Aufzählen von Segmenten auftreten:</span><span class="sxs-lookup"><span data-stu-id="a57e7-175">Empty segments may occur while enumerating segments explicitly:</span></span>

[!code-csharp[](~/samples/snippets/csharp/buffers/MyClass.cs?name=snippet7)]

<span data-ttu-id="a57e7-176">Der oben stehende Code erstellt ein `ReadOnlySequence<byte>`-Element mit leeren Segmenten und zeigt, wie sich diese leeren Segmente auf die verschiedenen APIs auswirken:</span><span class="sxs-lookup"><span data-stu-id="a57e7-176">The preceding code creates a `ReadOnlySequence<byte>` with empty segments and shows how those empty segments affect the various APIs:</span></span>

- <span data-ttu-id="a57e7-177">`ReadOnlySequence<T>.Slice` mit einer `SequencePosition`, die auf ein leeres Segment zeigt, behält dieses Segment bei.</span><span class="sxs-lookup"><span data-stu-id="a57e7-177">`ReadOnlySequence<T>.Slice` with a `SequencePosition` pointing to an empty segment preserves that segment.</span></span>
- <span data-ttu-id="a57e7-178">`ReadOnlySequence<T>.Slice` mit einem int-Wert überspringt die leeren Segmente.</span><span class="sxs-lookup"><span data-stu-id="a57e7-178">`ReadOnlySequence<T>.Slice` with an int skips over the empty segments.</span></span>
- <span data-ttu-id="a57e7-179">Beim Aufzählen des `ReadOnlySequence<T>`-Elements werden die leeren Segmente aufgezählt.</span><span class="sxs-lookup"><span data-stu-id="a57e7-179">Enumerating the `ReadOnlySequence<T>` enumerates the empty segments.</span></span>

### <a name="potential-problems-with-readonlysequencet-and-sequenceposition"></a><span data-ttu-id="a57e7-180">Potenzielle Probleme mit ReadOnlySequence\<T> und SequencePosition</span><span class="sxs-lookup"><span data-stu-id="a57e7-180">Potential problems with ReadOnlySequence\<T> and SequencePosition</span></span>

<span data-ttu-id="a57e7-181">Beim Verarbeiten von `ReadOnlySequence<T>`/`SequencePosition` gibt es im Vergleich zu einer normalen `ReadOnlySpan<T>`/`ReadOnlyMemory<T>`/`T[]`/`int`-Verarbeitung verschiedene ungewöhnliche Ergebnisse:</span><span class="sxs-lookup"><span data-stu-id="a57e7-181">There are several unusual outcomes when dealing with a `ReadOnlySequence<T>`/`SequencePosition` vs. a normal `ReadOnlySpan<T>`/`ReadOnlyMemory<T>`/`T[]`/`int`:</span></span>

- <span data-ttu-id="a57e7-182">`SequencePosition` ist eine Positionsmarkierung für ein bestimmtes `ReadOnlySequence<T>`-Element, keine absolute Position.</span><span class="sxs-lookup"><span data-stu-id="a57e7-182">`SequencePosition` is a position marker for a specific `ReadOnlySequence<T>`, not an absolute position.</span></span> <span data-ttu-id="a57e7-183">Da diese Markierung relativ zu einem bestimmten `ReadOnlySequence<T>`-Element ist, hat sie außerhalb des `ReadOnlySequence<T>`-Elements, aus dem sie stammt, keine Bedeutung.</span><span class="sxs-lookup"><span data-stu-id="a57e7-183">Because it's relative to a specific `ReadOnlySequence<T>`, it doesn't have meaning if used outside of the `ReadOnlySequence<T>` where it originated.</span></span>
- <span data-ttu-id="a57e7-184">In der `SequencePosition` können ohne das `ReadOnlySequence<T>`-Element keine arithmetischen Berechnungen ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="a57e7-184">Arithmetic can't be performed on `SequencePosition` without the `ReadOnlySequence<T>`.</span></span> <span data-ttu-id="a57e7-185">Das bedeutet, dass einfache Vorgänge wie `position++` als `ReadOnlySequence<T>.GetPosition(position, 1)` geschrieben werden.</span><span class="sxs-lookup"><span data-stu-id="a57e7-185">That means doing basic things like `position++` is written `ReadOnlySequence<T>.GetPosition(position, 1)`.</span></span>
- <span data-ttu-id="a57e7-186">`GetPosition(long)` unterstützt **keine** negativen Indizes.</span><span class="sxs-lookup"><span data-stu-id="a57e7-186">`GetPosition(long)` does **not** support negative indexes.</span></span> <span data-ttu-id="a57e7-187">Das bedeutet, dass es unmöglich ist, das vorletzte Zeichen abzurufen, ohne alle Segmente zu durchlaufen.</span><span class="sxs-lookup"><span data-stu-id="a57e7-187">That means it's impossible to get the second to last character without walking all segments.</span></span>
- <span data-ttu-id="a57e7-188">Zwei `SequencePosition`-Elemente können nicht miteinander verglichen werden, sodass folgende Vorgänge schwierig sind:</span><span class="sxs-lookup"><span data-stu-id="a57e7-188">Two `SequencePosition` can't be compared, making it difficult to:</span></span>
  - <span data-ttu-id="a57e7-189">Ermitteln, ob eine Position größer oder kleiner ist als eine andere Position.</span><span class="sxs-lookup"><span data-stu-id="a57e7-189">Know if one position is greater than or less than another position.</span></span>
  - <span data-ttu-id="a57e7-190">Schreiben einiger Analysealgorithmen.</span><span class="sxs-lookup"><span data-stu-id="a57e7-190">Write some parsing algorithms.</span></span>
- <span data-ttu-id="a57e7-191">`ReadOnlySequence<T>` ist größer als ein Objektverweis und sollte nach Möglichkeit durch [in](../../csharp/language-reference/keywords/in-parameter-modifier.md) oder [ref](../../csharp/language-reference/keywords/ref.md) übergeben werden.</span><span class="sxs-lookup"><span data-stu-id="a57e7-191">`ReadOnlySequence<T>` is bigger than an object reference and should be passed by [in](../../csharp/language-reference/keywords/in-parameter-modifier.md) or [ref](../../csharp/language-reference/keywords/ref.md) where possible.</span></span> <span data-ttu-id="a57e7-192">Durch Übergeben von `ReadOnlySequence<T>` durch `in` oder `ref` werden weniger Kopien der [Struktur](../../csharp/language-reference/keywords/struct.md) erstellt.</span><span class="sxs-lookup"><span data-stu-id="a57e7-192">Passing `ReadOnlySequence<T>` by `in` or `ref` reduces copies of the [struct](../../csharp/language-reference/keywords/struct.md).</span></span>
- <span data-ttu-id="a57e7-193">Für leere Segmente gilt:</span><span class="sxs-lookup"><span data-stu-id="a57e7-193">Empty segments:</span></span>
  - <span data-ttu-id="a57e7-194">Sie sind innerhalb eines `ReadOnlySequence<T>`-Elements gültig.</span><span class="sxs-lookup"><span data-stu-id="a57e7-194">Are valid within a `ReadOnlySequence<T>`.</span></span>
  - <span data-ttu-id="a57e7-195">Sie können beim Durchlaufen mithilfe der `ReadOnlySequence<T>.TryGet`-Methode angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="a57e7-195">Can appear when iterating using the `ReadOnlySequence<T>.TryGet` method.</span></span>
  - <span data-ttu-id="a57e7-196">Sie können beim Aufteilen der Sequenz in Slices mithilfe der `ReadOnlySequence<T>.Slice()`-Methode mit `SequencePosition`-Objekten angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="a57e7-196">Can appear slicing the sequence using the `ReadOnlySequence<T>.Slice()` method with `SequencePosition` objects.</span></span>

## <a name="sequencereadert"></a><span data-ttu-id="a57e7-197">SequenceReader\<T\></span><span class="sxs-lookup"><span data-stu-id="a57e7-197">SequenceReader\<T\></span></span>

<span data-ttu-id="a57e7-198"><xref:System.Buffers.SequenceReader%601>:</span><span class="sxs-lookup"><span data-stu-id="a57e7-198"><xref:System.Buffers.SequenceReader%601>:</span></span>

- <span data-ttu-id="a57e7-199">Es handelt sich um einen neuen Typ, der in .NET Core 3.0 eingeführt wurde, um die Verarbeitung eines `ReadOnlySequence<T>`-Elements zu vereinfachen.</span><span class="sxs-lookup"><span data-stu-id="a57e7-199">Is a new type that was introduced in .NET Core 3.0 to simplify the processing of a `ReadOnlySequence<T>`.</span></span>
- <span data-ttu-id="a57e7-200">Durch den Typ entfallen die Unterschiede zwischen einem `ReadOnlySequence<T>`-Element mit einem Segment und einem `ReadOnlySequence<T>`-Element mit mehreren Segmenten.</span><span class="sxs-lookup"><span data-stu-id="a57e7-200">Unifies the differences between a single segment `ReadOnlySequence<T>` and multi-segment `ReadOnlySequence<T>`.</span></span>
- <span data-ttu-id="a57e7-201">Der Typ stellt Hilfsfunktionen für das Lesen von Binär- und Textdaten bereit (`byte` und `char`), die möglicherweise auf mehrere Segmente aufgeteilt sind.</span><span class="sxs-lookup"><span data-stu-id="a57e7-201">Provides helpers for reading binary and text data (`byte` and `char`) that may or may not be split across segments.</span></span>

<span data-ttu-id="a57e7-202">Es gibt integrierte Methoden für die Verarbeitung sowohl von binären Daten als auch von Daten mit Trennzeichen.</span><span class="sxs-lookup"><span data-stu-id="a57e7-202">There are built-in methods for dealing with processing both binary and delimited data.</span></span> <span data-ttu-id="a57e7-203">Der folgende Abschnitt veranschaulicht, wie diese Methoden mit dem `SequenceReader<T>`-Element aussehen:</span><span class="sxs-lookup"><span data-stu-id="a57e7-203">The following section demonstrates what those same methods look like with the `SequenceReader<T>`:</span></span>

### <a name="access-data"></a><span data-ttu-id="a57e7-204">Zugriff auf Daten</span><span class="sxs-lookup"><span data-stu-id="a57e7-204">Access data</span></span>

<span data-ttu-id="a57e7-205">`SequenceReader<T>` verfügt über Methoden zum Aufzählen von Daten direkt im `ReadOnlySequence<T>`-Element.</span><span class="sxs-lookup"><span data-stu-id="a57e7-205">`SequenceReader<T>` has methods for enumerating data inside of the `ReadOnlySequence<T>` directly.</span></span> <span data-ttu-id="a57e7-206">Der folgende Code ist ein Beispiel für die Verarbeitung jeweils eines `ReadOnlySequence<byte>`-Elements pro `byte`:</span><span class="sxs-lookup"><span data-stu-id="a57e7-206">The following code is an example of processing a `ReadOnlySequence<byte>` a `byte` at a time:</span></span>

[!code-csharp[](~/samples/snippets/csharp/buffers/MyClass.cs?name=snippet8)]

<span data-ttu-id="a57e7-207">`CurrentSpan` macht das `Span`-Element des aktuellen Segments verfügbar – dies entspricht der manuellen Ausführung des Vorgangs in der Methode.</span><span class="sxs-lookup"><span data-stu-id="a57e7-207">The `CurrentSpan` exposes the current segment's `Span`, which is similar to what was done in the method manually.</span></span>

### <a name="use-position"></a><span data-ttu-id="a57e7-208">Verwenden der Position</span><span class="sxs-lookup"><span data-stu-id="a57e7-208">Use position</span></span>

<span data-ttu-id="a57e7-209">Der folgende Code ist eine Beispielimplementierung von `FindIndexOf` unter Verwendung des `SequenceReader<T>`-Elements:</span><span class="sxs-lookup"><span data-stu-id="a57e7-209">The following code is an example implementation of `FindIndexOf` using the `SequenceReader<T>`:</span></span>

[!code-csharp[](~/samples/snippets/csharp/buffers/MyClass.cs?name=snippet9)]

### <a name="process-binary-data"></a><span data-ttu-id="a57e7-210">Verarbeiten von Binärdaten</span><span class="sxs-lookup"><span data-stu-id="a57e7-210">Process binary data</span></span>

<span data-ttu-id="a57e7-211">Das folgende Beispiel analysiert eine 4 Byte lange Big-Endian-Ganzzahl ab dem Start des `ReadOnlySequence<byte>`-Elements.</span><span class="sxs-lookup"><span data-stu-id="a57e7-211">The following example parses a 4-byte big-endian integer length from the start of the `ReadOnlySequence<byte>`.</span></span>

[!code-csharp[](~/samples/snippets/csharp/buffers/MyClass.cs?name=snippet11)]

### <a name="process-text-data"></a><span data-ttu-id="a57e7-212">Verarbeiten von Textdaten</span><span class="sxs-lookup"><span data-stu-id="a57e7-212">Process text data</span></span>

[!code-csharp[](~/samples/snippets/csharp/buffers/MyClass.cs?name=snippet10)]

### <a name="sequencereadert-common-problems"></a><span data-ttu-id="a57e7-213">Häufige SequenceReader\<T\>-Probleme</span><span class="sxs-lookup"><span data-stu-id="a57e7-213">SequenceReader\<T\> common problems</span></span>

- <span data-ttu-id="a57e7-214">Da `SequenceReader<T>` eine änderbare Struktur ist, sollte das Element immer durch [Verweis](../../csharp/language-reference/keywords/ref.md) übergeben werden.</span><span class="sxs-lookup"><span data-stu-id="a57e7-214">Because `SequenceReader<T>` is a mutable struct, it should always be passed by [reference](../../csharp/language-reference/keywords/ref.md).</span></span>
- <span data-ttu-id="a57e7-215">`SequenceReader<T>` ist eine [ref-Struktur](../../csharp/language-reference/keywords/ref.md#ref-struct-types) und kann daher nur in synchronen Methoden verwendet und nicht in Feldern gespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="a57e7-215">`SequenceReader<T>` is a [ref struct](../../csharp/language-reference/keywords/ref.md#ref-struct-types) so it can only be used in synchronous methods and can't be stored in fields.</span></span> <span data-ttu-id="a57e7-216">Weitere Informationen finden Sie unter [Schreiben von sicherem und effizientem C#-Code](../../csharp/write-safe-efficient-code.md).</span><span class="sxs-lookup"><span data-stu-id="a57e7-216">For more information, see [Write safe and efficient C# code](../../csharp/write-safe-efficient-code.md).</span></span>
- <span data-ttu-id="a57e7-217">`SequenceReader<T>` ist für die Verwendung als Vorwärtslesefunktion optimiert.</span><span class="sxs-lookup"><span data-stu-id="a57e7-217">`SequenceReader<T>` is optimized for use as a forward-only reader.</span></span> <span data-ttu-id="a57e7-218">`Rewind` ist für Sicherungen mit geringem Umfang vorgesehen, die nicht über andere `Read`-, `Peek`- oder `IsNext`-APIs verarbeitet werden können.</span><span class="sxs-lookup"><span data-stu-id="a57e7-218">`Rewind` is intended for small backups that can't be addressed utilizing other `Read`, `Peek`, and `IsNext` APIs.</span></span>