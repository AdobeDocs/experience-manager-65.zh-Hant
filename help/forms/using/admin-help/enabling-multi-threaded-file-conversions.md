---
title: 啟用多執行緒檔案轉換
description: 瞭解如何啟用多執行緒檔案轉換。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: 402c1fd4-c6c8-494e-b452-b56a91c4a397
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 4a55f87d3b8aa9944f0b32760aa645c42efd93e8
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%
---
# 啟用多執行緒檔案轉換 {#enabling-multi-threaded-file-conversions}

PDF Generator可同時執行多個檔案轉換，以提高轉換輸送量。 選擇適用的轉換模式：

| 轉換模式 | 支援同時轉換的應用程式 | 使用者帳戶模型 |
|---|---|---|
| 多使用者模式 | OpenOffice | 執行每個OpenOffice執行個體的使用者帳戶不同。 |
| 單一使用者模式 | ® Word和Microsoft® Excel | 一個使用者帳戶執行多個Word和Excel例項。 PowerPoint轉換仍維持序列化。 |

在啟用任一模式之前，請先為您使用的應用程式和作業系統完成[PDF Generator安裝前組態](/help/forms/using/install-configure-document-services.md#preinstallationconfigurations)。 如需支援的應用程式版本，請參閱[PDF Generator的軟體支援](/help/forms/using/aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator)。

## 多使用者模式 {#multi-user-mode}

在多使用者模式下，PDF Generator會在個別的使用者帳戶下啟動每個OpenOffice執行個體。 設定足夠的有效管理使用者帳戶，以符合您所需的並行轉換次數。 在叢集中，在每個節點上設定相同的帳戶。

在Windows上，請確定PDF Generator使用者具有[取代處理序層級權杖許可權](/help/forms/using/install-configure-document-services.md#grant-the-replace-a-process-level-token-privilege)，並完成[設定Document Services](/help/forms/using/install-configure-document-services.md#disable-user-account-control-uac)中說明的適用使用者帳戶控制設定。

### OpenOffice轉換 {#openoffice-conversions}

為可同時執行的每個OpenOffice執行個體設定一個PDF Generator使用者帳戶。 將OpenOffice安裝在每個設定使用者都可以存取的位置，並關閉每個使用者的初始OpenOffice啟用對話方塊。

針對UNIX系統，請在[設定Document Services](/help/forms/using/install-configure-document-services.md#preinstallationconfigurations)中完成OpenOffice安裝和使用者許可權需求。

## Windows上的單一使用者模式 {#single-user-mode-on-windows}

單一使用者模式可讓PDF Generator以一個已設定的使用者帳戶同時執行轉換。

在此模式中，® Word （DOC和DOCX）和Excel （XLS和XLSX）的多個執行個體會在同一個使用者下執行。 ® PowerPoint （PPT和PPTX）不支援單一使用者模式。 PDF Generator一次只會啟動一個PowerPoint例項，因此PowerPoint轉換會序列化。

若要啟用Word與Excel轉換的單一使用者模式：

1. 在管理主控台中，瀏覽至&#x200B;**首頁>服務>應用程式及服務>服務管理**。
1. 篩選&#x200B;**PDF Generator**&#x200B;並選取&#x200B;**GeneratePDFervice**。
1. 在&#x200B;**組態**&#x200B;索引標籤上，設定下列選項：

   * 將PDFMaker **的**&#x200B;啟用單一使用者模式設定為&#x200B;**true**。
   * 將&#x200B;**PDFMaker集區大小**&#x200B;設定為可同時執行轉換的Word執行個體數目上限。
   * 將Native2PDF **的**&#x200B;啟用單一使用者模式設定為&#x200B;**true**。
   * 將&#x200B;**Native2PDF集區大小**&#x200B;設定為可同時執行轉換的Excel執行個體數目上限。

1. 重新啟動AEM Forms伺服器。
