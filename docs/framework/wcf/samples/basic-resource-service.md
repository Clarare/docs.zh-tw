---
title: "基本資源服務 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4360063e-cc8c-4648-846e-c05a5af51a7a
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 基本資源服務
此範例示範如何使用 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] REST 程式設計模型實作 HTTP 的服務，此模型會公開一組支援擷取、加入、刪除和取代作業的客戶。此範例由兩個元件所組成：自我裝載的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] HTTP 服務 \(Service.cs\)，以及建立服務並呼叫該服務的主控台應用程式 \(program.cs\)。  
  
## 範例詳細資料  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服務會以資源導向\/REST 的方式公開客戶的集合。簡單地說，這牽涉到客戶集合和集合中的每個客戶都擁有唯一的 URI。此服務支援傳送集合 URI 的 HTTP `GET` 以擷取整個集合，也支援傳送集合 URI 的 HTTP `POST` 以便將新的客戶加入至集合。此外，在個別客戶的 URI 上，它也支援 HTTP `GET` 取得客戶詳細資料、支援 HTTP `PUT` 取代客戶的詳細資料，以及支援 HTTP `DELETE` 從集合移除客戶。當新客戶加入至集合時，服務會指派一個唯一的 URI 給它，並將 URI 儲存為客戶詳細資料的一部分。此外，它會使用回應的 Location HTTP 標頭，與用戶端的 URI 進行通訊。  
  
 App.config 檔案會以預設的 <xref:System.ServiceModel.Description.WebHttpEndpoint> 設定 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服務，且 <xref:System.ServiceModel.Description.WebHttpEndpoint.HelpEnabled%2A> 屬性設定為 `true`。因此，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 會在 `http://localhost:8000/Customers/help` 中建立自動 HTML 說明頁，這個頁面會提供如何對服務建構 HTTP 要求以及如何存取服務之 HTTP 回應的相關資訊，例如，如何以 XML 和 JSON 表示客戶詳細資料的範例。  
  
 以此方式公開客戶集合 \(以及更普遍的任何資源\) 可讓用戶端以統一的方式，使用 URI 和 HTTP `GET`、`PUT`、`DELETE` 以及 `POST` 與其互動。Program.cs 會示範如何使用 <xref:System.Net.HttpWebRequest> 授權此種用戶端。請注意，這只是存取 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] REST 服務的其中一種方式。您也可以使用其他 .NET Framework 類別 \(例如 <xref:System.ServiceModel.ChannelFactory> 和 <xref:System.Net.WebClient>\) 來存取服務。SDK 中的其他範例 \(例如[基本 HTTP 服務](../../../../docs/framework/wcf/samples/basic-http-service.md)範例和[自動格式選取](../../../../docs/framework/wcf/samples/automatic-format-selection.md)範例\) 會示範如何使用這些類別與 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服務進行通訊。  
  
 此範例包含同時在主控台應用程式中執行的自我裝載服務和用戶端。當主控台應用程式執行時，用戶端會對服務發出要求，然後將相關的資訊從回應寫入至主控台視窗。  
  
#### 若要使用這個範例  
  
1.  開啟基本資源服務範例的方案。啟動 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 時，您必須以系統管理員身分執行，才能讓範例成功執行。方法是，以滑鼠右鍵按一下 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 圖示，然後選取內容功能表中的 \[**以系統管理員身分執行**\]。  
  
2.  按下 CTRL\+SHIFT\+B 建置方案，然後按下 Ctrl\+F5 執行主控台應用程式。主控台視窗隨即出現，並提供執行中服務的 URI，以及執行中服務之 HTML 說明頁的 URI。您可以隨時在瀏覽器中輸入說明頁的 URI 來檢視 HTML 說明頁。當範例執行時，用戶端會寫入目前活動的狀態。  
  
3.  按下任何按鍵可終止此範例。  
  
> [!IMPORTANT]
>  這些範例可能已安裝在您的電腦上。請先檢查下列 \(預設\) 目錄，然後再繼續。  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  如果此目錄不存在，請移至[用於 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 與 Windows Workflow Foundation \(WF\) 範例](http://go.microsoft.com/fwlink/?LinkId=150780)，以下載所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。此範例位於下列目錄。  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Web\BasicResourceService`  
  
## 請參閱  
 [基本 HTTP 服務](../../../../docs/framework/wcf/samples/basic-http-service.md)   
 [自動格式選取](../../../../docs/framework/wcf/samples/automatic-format-selection.md)