---
title: 設定與Acrobat Reader DC擴充功能搭配使用的逾時值
description: 瞭解如何設定逾時值以與Acrobat Reader DC擴充功能搭配使用。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0a55aab3-14a3-41ad-8533-dc2cd116a848
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# 設定與Acrobat Reader DC擴充功能搭配使用的逾時值  {#setting-timeout-values-for-use-with-acrobat-reader-dc-extensions}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

在Acrobat Reader DC擴充功能中處理許多PDF檔案時，請確定已適當設定下列逾時值，以防止工作逾時及失敗：

**檔案處置逾時**

此值可在管理主控台中設定。 按一下「設定」>「核心系統設定」>「設定」，並指定「預設檔案處置逾時」的值。

**使用者管理員AEM表單逾時：**&#x200B;此值可透過編輯config.xml檔案來設定。 在管理控制檯中，按一下「設定」>「使用者管理」>「組態」>「匯入及匯出組態檔」，然後按一下「匯出」。 開啟匯出的config.xml檔案並編輯下列行：

&lt;entry key=&quot;assertionValidityInMinutes&quot; value=&quot;600&quot;/>

&lt;entry key=&quot;SessionTimeout&quot; value=&quot;600&quot;/>

儲存並將config.xml檔案匯入回管理主控台。

**應用程式伺服器工作階段逾時：**&#x200B;這個值可以在應用程式伺服器上設定。 如需詳細資訊，請參閱應用程式伺服器隨附的檔案。
