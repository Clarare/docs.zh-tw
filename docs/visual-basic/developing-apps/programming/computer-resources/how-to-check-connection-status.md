---
title: "如何：在 Visual Basic 中檢查連線狀態 | Microsoft Docs"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Web connections
- IsAvailable property, about IsAvailable
- connections, checking status
- connection status
ms.assetid: 4d9ee8ab-9a6f-4279-ace4-b75afc976a74
caps.latest.revision: 26
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 81386ee1f8c8cefbcd34a05d594277b9de772b8d
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-check-connection-status-in-visual-basic"></a>如何：在 Visual Basic 中檢查連接狀態
<xref:Microsoft.VisualBasic.Devices.Network.IsAvailable%2A> 屬性可用來判斷電腦具有工作中的網路或網際網路連線。  
  
[!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
### <a name="to-check-whether-a-computer-has-a-working-connection"></a>檢查電腦是否有工作中的連線  
  
-   判斷 `IsAvailable` 屬性是 `True` 或 `False`。 下列程式碼會檢查並報告屬性的狀態︰  
  
     [!code-vb[VbResourceTasks#3](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-check-connection-status_1.vb)]  
  
     這個程式碼範例也可用為 IntelliSense 程式碼片段。 在程式碼片段選擇器中，該程式碼片段會位於 [連接和網路]**** 中。 如需詳細資訊，請參閱[程式碼片段](https://docs.microsoft.com/visualstudio/ide/code-snippets)。  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.VisualBasic.Devices.Network?displayProperty=fullName>   
 <xref:Microsoft.VisualBasic.Devices.Network.IsAvailable%2A>

