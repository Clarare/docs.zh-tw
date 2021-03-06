---
title: "無法發出組件︰&lt;錯誤訊息&gt;|Microsoft 文件"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc30145
- bc30145
dev_langs:
- VB
helpviewer_keywords:
- BC30145
ms.assetid: 2e7eb2b9-eda6-4bdb-95cc-72c7f0be7528
caps.latest.revision: 11
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: dac4b133882c043f9c84e936bad2e36f35fc4c33
ms.lasthandoff: 03/13/2017

---
# <a name="unable-to-emit-assembly-lterror-messagegt"></a>無法發出組件︰&lt;錯誤訊息&gt;
[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 編譯器呼叫組件連結器 (Al.exe，也稱為 Alink) 使用資訊清單產生組件，連結器在建立組件的發出階段回報錯誤。  
  
 **錯誤識別碼︰** BC30145  
  
## <a name="to-correct-this-error"></a>更正這個錯誤  
  
1.  檢查引用的錯誤訊息，並參考主題[Al.exe 工具錯誤和警告](http://msdn.microsoft.com/en-us/7f125d49-0a03-47a6-9ba9-d61a679a7d4b)的進一步說明和建議。  
  
2.  請嘗試 簽署組件以手動方式，使用[Al.exe （組件連結器）](https://msdn.microsoft.com/library/c405shex)或[Sn.exe （強式名稱工具）](https://msdn.microsoft.com/library/k5b5tt23)。  
  
3.  如果錯誤持續發生，請收集情況的相關資訊，並通知 Microsoft 產品支援服務。  
  
### <a name="to-sign-the-assembly-manually"></a>手動簽署組件  
  
1.  使用[Sn.exe （強式名稱工具）](https://msdn.microsoft.com/library/k5b5tt23)建立公開/私密金鑰組檔案。  
  
     這個檔案的副檔名為 .snk。  
  
2.  從專案刪除產生錯誤的 COM 參考。  
  
3.  從 Windows**啟動**功能表上，指向**程式**，指向  **Microsoft Visual Studio 2008**，指向  **Visual Studio Tools**，然後按一下  **Visual Studio 2008 命令提示字元**。  
  
4.  移到您要放置組件包裝函式的目錄。  
  
5.  輸入下列程式碼。  
  
    ```  
    tlbimp <path to COM reference file> /out:<output assembly name> /keyfile:<path to .snk file>  
    ```  
  
     您可能輸入的程式碼範例如下。  
  
    ```  
    tlbimp c:\windows\system32\msi.dll /out:Interop.WindowsInstaller.dll /keyfile:"c:\documents and settings\mykey.snk"  
    ```  
  
     如果路徑或檔案包含空格，請使用雙引號 (")。  
  
6.  在 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] 中，加入您剛建立之檔案的 .NET Assembly 參考。  
  
## <a name="see-also"></a>另請參閱  
 [Al.exe （組件連結器）](https://msdn.microsoft.com/library/c405shex)   
 [Al.exe 工具錯誤和警告](http://msdn.microsoft.com/en-us/7f125d49-0a03-47a6-9ba9-d61a679a7d4b)   
 [Sn.exe （強式名稱工具）](https://msdn.microsoft.com/library/k5b5tt23)   
 [如何：建立公開/私密金鑰組](http://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114)   
 [告訴我們](https://docs.microsoft.com/visualstudio/ide/talk-to-us)
