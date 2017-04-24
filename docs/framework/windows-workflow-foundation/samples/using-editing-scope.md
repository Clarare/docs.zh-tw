---
title: "使用編輯範圍 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 79306f9e-318b-4687-9863-8b93d1841716
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# 使用編輯範圍
此範例示範如何批次處理一組變更，以便在單一不可部分完成的單位中恢復這些變更。根據預設，活動設計工具作者所執行的動作會自動整合至恢復\/重做系統。  
  
## 示範  
 編輯範圍以及恢復與重做。  
  
## 討論  
 這個範例示範如何在單一工作單位中批次處理對 <xref:System.Activities.Presentation.Model.ModelItem> 樹狀結構的一組變更。請注意，從 WPF 設計工具直接繫結至 <xref:System.Activities.Presentation.Model.ModelItem> 值時，系統會自動套用變更。這個範例示範當透過命令式程式碼進行多個要批次處理的變更 \(而不是單一變更\) 時，所必須完成的工作。  
  
 在這個範例中，會加入三個活動。當編輯開始時，會呼叫 <xref:System.Activities.Presentation.Model.ModelItem> 執行個體上的 <xref:System.Activities.Presentation.Model.ModelItem.BeginEdit%2A>。在此編輯範圍內，對 <xref:System.Activities.Presentation.Model.ModelItem> 樹狀結構的變更會批次處理。<xref:System.Activities.Presentation.Model.ModelItem.BeginEdit%2A> 命令會傳回可用於控制此執行個體的 <xref:System.Activities.Presentation.Model.EditingScope>。可呼叫 <xref:System.Activities.Presentation.Model.EditingScope.OnComplete%2A> 或 <xref:System.Activities.Presentation.Model.EditingScope.OnRevert%2A>，以認可或還原編輯範圍。  
  
 您也可以巢狀處理 <xref:System.Activities.Presentation.Model.EditingScope> 物件，允許在更大的編輯範圍內追蹤多組變更，以及個別控制這些變更。可能使用此功能的狀況是當來自多個對話方塊的變更必須分別認可或還原，而所有變更是以單一不可部分完成作業的方式來處理。在這個範例中，編輯範圍是使用 <xref:System.Activities.Presentation.Model.ModelEditingScope> 類型的 <xref:System.Collections.ObjectModel.ObservableCollection%601> 進行追蹤。使用了 <xref:System.Collections.ObjectModel.ObservableCollection%601>，如此，可以在設計介面上觀察巢狀深度。  
  
## 若要安裝、建立及執行範例  
  
1.  建置及執行範例，然後使用左側按鈕修改工作流程。  
  
2.  按一下 \[**開啟編輯範圍**\]。  
  
    1.  這個命令會呼叫 <xref:System.Activities.Presentation.Model.ModelItem.BeginEdit%2A>，用於建立編輯範圍並將其發送至編輯堆疊上。  
  
    2.  三個活動接著會加入至選取的 <xref:System.Activities.Presentation.Model.ModelItem>。請注意，如果編輯範圍尚未使用 <xref:System.Activities.Presentation.Model.ModelItem.BeginEdit%2A> 開啟，三個新活動會出現在設計工具畫布上。因為這項作業在 <xref:System.Activities.Presentation.Model.EditingScope> 中仍為暫止，所以設計工具尚未更新。  
  
3.  按 \[**關閉編輯範圍**\] 認可編輯範圍。三個活動隨即出現在設計工具中。  
  
> [!IMPORTANT]
>  這些範例可能已安裝在您的電腦上。請先檢查下列 \(預設\) 目錄，然後再繼續。  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  如果此目錄不存在，請移至[用於 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 與 Windows Workflow Foundation \(WF\) 範例](http://go.microsoft.com/fwlink/?LinkId=150780)，以下載所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。此範例位於下列目錄。  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Basic\CustomActivities\CustomActivityDesigners\UsingEditingScope`