---
title: "存取控制機制 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "存取控制 [WCF]"
  - "WCF 安全性"
ms.assetid: 9d576122-3f55-4425-9acf-b23d0781e966
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# 存取控制機制
您可以用 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 以多種方式控制存取。本主題將扼要討論各種機制，並提供每一種機制的建議使用時機，本主題目的在於協助您選擇使用正確的機制。下面將依複雜性的順序列出存取技術。最簡單的是 <xref:System.Security.Permissions.PrincipalPermissionAttribute>，最複雜的則是「身分識別模型」。  
  
 除了這些機制以外，在[委派和模擬](../../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md)中也有說明使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 進行模擬與委派的詳細資訊。  
  
## PrincipalPermissionAttribute  
 <xref:System.Security.Permissions.PrincipalPermissionAttribute> 是用來限制對於服務方法的存取。當套用到方法時，這個屬性即可用來要求 Windows 群組或 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 角色中的特定呼叫者身分識別或成員資格。如果是使用 X.509 憑證進行驗證，用戶端便會獲得由主體名稱加憑證指紋所組成的主要身分識別。  
  
 請用 <xref:System.Security.Permissions.PrincipalPermissionAttribute> 控制服務執行所在電腦上資源的存取，如果服務的使用者永遠屬於服務執行所在之相同 Windows 網域，也用此種做法。您可以輕易建立具有指定之存取層級 \(例如無、唯讀或讀取和寫入\) 的 Windows 群組。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]使用屬性的詳細資訊，請參閱 [HOW TO：使用 PrincipalPermissionAttribute 類別來限制存取](../../../../docs/framework/wcf/how-to-restrict-access-with-the-principalpermissionattribute-class.md)。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]身分識別的詳細資訊，請參閱[服務身分識別和驗證](../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)。  
  
## ASP.NET 成員資格提供者  
 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 的一項功能是成員資格提供者。儘管從技術角度來說，成員資格提供者並不屬於存取控制機制，但其可透過限制能夠存取服務端點的一組可能識別來控制對於服務的存取。成員資格功能包括可以填入 \(Populate\) 使用者名稱\/密碼組合的資料庫，而該名稱\/密碼組合可讓網站的使用者配合該網站來建立帳戶。為了存取使用成員資格提供者的服務，使用者必須以自己的使用者名稱和密碼登入。  
  
> [!NOTE]
>  您必須先使用 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 功能填入資料庫，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服務才能使用該資料進行授權。  
  
 如果已經從現有 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 網站建立了成員資格資料庫，而且要讓相同的使用者使用您的服務 \(即透過相同的使用者名稱和密碼進行授權\)，您也可以使用成員資格功能。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服務中成員資格功能的詳細資訊，請參閱 [HOW TO：使用 ASP.NET 成員資格提供者](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-membership-provider.md)。  
  
## ASP.NET 角色提供者  
 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 的另一項功能便是使用角色管理授權的能力。[!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 角色提供者可以讓開發人員建立使用者的角色，並指派每名使用者為一個或多個角色。就像使用成員資格提供者，角色和指派會儲存在資料庫中，而且可以使用 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 角色提供者之特定實作 \(Implementation\) 所提供的工具進行填入。就像使用成員資格功能，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 開發人員可以使用資料庫中的資訊，依據個別角色來授權服務使用者。例如，他們可以結合使用角色提供者與前述的 `PrincipalPermissionAttribute` 存取控制機制。  
  
 如果已經建立現有的 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 角色提供者資料庫，而且要使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服務中的相同規則集和使用者指派，您也可以使用 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 角色提供者。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]使用角色提供者功能的詳細資訊，請參閱 [HOW TO：使用 ASP.NET 角色提供者搭配服務](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-role-provider-with-a-service.md)。  
  
## 授權管理員  
 另一項功能會結合授權管理員 \(AzMan\) 與 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 角色提供者來授權用戶端。當 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 裝載 Web 服務時，AzMan 即可整合到應用程式中，如此一來，服務的授權便能透過 AzMan 完成。[!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 角色管理員會提供特定應用程式開發介面來讓您管理應用程式角色、從角色新增和移除使用者，以及檢查角色成員資格，但是您無法使用它來查詢某位使用者是否已獲授權為可執行具名的工作或作業。AzMan 可讓您定義個別的作業，並將它們結合於工作中。使用 AZMan 時，除了角色檢查以外，您也可以檢查使用者是否能夠執行某項工作。角色指派和工作授權可以設定在應用程式外部，或是以程式設計方式執行於應用程式內部。AzMan 管理 Microsoft 管理主控台 \(MMC\) 嵌入式管理單元可讓系統管理員能夠變更角色可在執行階段執行的工作，以及管理每位使用者的角色成員資格。  
  
 如果已經能夠存取現有的 AzMan 安裝，而且要使用 AzMan\/角色提供者組合的功能來授權您的服務使用者，您也可以使用 AzMan 和 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 角色提供者。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] AzMan 和 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 角色提供者的詳細資訊，請參閱 [How To：搭配 ASP.NET 2.0 使用授權管理員 \(AzMan\)](http://go.microsoft.com/fwlink/?LinkId=88951) \(英文\)。[!INCLUDE[crabout](../../../../includes/crabout-md.md)] 使用 AzMan 和 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服務之角色提供者的詳細資訊，請參閱 [HOW TO：使用 ASP.NET 授權管理員角色提供者搭配服務](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-authorization-manager-role-provider-with-a-service.md)。  
  
## 識別模型  
 身分識別模型是一組 API，這組 API 可讓您管理宣告和原則來授權用戶端。使用身分識別模型時，您可以檢查呼叫者向服務驗證本身時所使用認證中所包含的每一個宣告、比較宣告與服務的原則集，並根據比較結果來授與或拒絕存取權。  
  
 如果您需要精密控制能力，以及在授與存取權之前設定特定準則的能力，請使用身分識別模型。例如，當使用 <xref:System.Security.Permissions.PrincipalPermissionAttribute> 時，準則只是已通過驗證且屬於特定角色之使用者的身分識別。相較之下，若是使用身分識別模型，您就可以建立原則，表示使用者必須超過 18 歲並擁有有效的駕照，才允許該使用者檢視某份文件。  
  
 有一個可以充分發揮身分識別模型宣告架構存取控制的範例，就是在發行權杖情節中使用同盟認證的情況下。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]同盟與發行權杖的詳細資訊，請參閱[聯合與發行的權杖](../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]身分識別模型的詳細資訊，請參閱[使用身分識別模型來管理宣告與授權](../../../../docs/framework/wcf/feature-details/managing-claims-and-authorization-with-the-identity-model.md)。  
  
## 請參閱  
 <xref:System.Security.Permissions.PrincipalPermissionAttribute>   
 [HOW TO：使用 PrincipalPermissionAttribute 類別來限制存取](../../../../docs/framework/wcf/how-to-restrict-access-with-the-principalpermissionattribute-class.md)   
 [HOW TO：使用 ASP.NET 角色提供者搭配服務](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-role-provider-with-a-service.md)   
 [HOW TO：使用 ASP.NET 授權管理員角色提供者搭配服務](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-authorization-manager-role-provider-with-a-service.md)   
 [使用身分識別模型來管理宣告與授權](../../../../docs/framework/wcf/feature-details/managing-claims-and-authorization-with-the-identity-model.md)   
 [委派和模擬](../../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md)