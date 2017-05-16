---
title: "C# 委派 | C# 語言教學課程"
description: "了解使用 C# 委派進行的晚期繫結"
keywords: ".NET, csharp, 委派, lambda, 晚期繫結"
author: BillWagner
ms.author: wiwagn
ms.date: 08/10/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 3cc27357-3ac2-43a1-aad0-86a77b88f884
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 5cb45d7ae09430c87872a12a0ceb451d5b2b5fda
ms.lasthandoff: 03/13/2017

---

# <a name="delegates"></a>委派

「委派型別」代表對方法的參考，其中含有特定參數清單與傳回型別。 委派讓您可將方法視為實體，而實體能指派給變數或當作參數來傳遞。 委派就類似其他程式設計語言中的函式指標，但與函式指標的不同之處是，委派是物件導向且為型別安全。

下列範例會宣告並使用名為 `Function` 的委派型別。

[!code-csharp[DelegateExample](../../../samples/snippets/csharp/tour/delegates/Program.cs#L3-L37)]

`Function` 委派型別的執行個體可以參考任何採用 `double` 引數並傳回 `double` 值的方法。 `Apply` 方法會將指定的函式套用到 `double[]` 的元素，其中會傳回含有結果的 `double[]`。 在 `Main` 方法中，是使用 `Apply` 將三個不同的函式套用到 `double[]`。

委派可以參考靜態方法 (例如上一個範例中的 `Square` 或 `Math.Sin`)，或是參考執行個體方法 (例如上一個範例中的 `m.Multiply`)。 參考執行個體方法的委派也會參考特定的物件，而且透過委派來叫用執行個體方法時，該物件就會變成叫用中的 this。

您也可以使用匿名函式來建立委派，這些函式是動態建立的「內嵌方法」。 匿名函式可以看見周圍方法的區域變數。 因此，可以更輕鬆地覆寫上面的乘數範例，而不需使用 Multiplier 類別：

[!code-csharp[LambdaExample](../../../samples/snippets/csharp/tour/delegates/Program.cs#L44-L44)]

委派有一個有趣且實用的屬性，就是它並不知道或並不在乎所參考方法的類別；唯一重要的是所參考的方法具有與委派相同的參數和傳回型別。

>[!div class="step-by-step"]
[上一頁](enums.md)
[下一頁](attributes.md)

