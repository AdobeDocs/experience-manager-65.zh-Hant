---
title: 指定輸出的檔案位置
description: 瞭解如何為特定型別的檔案指定輸出的檔案位置，例如，內容根URI、XCI設定檔案、快取和預設。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 620c69d6-4fe1-46d6-b5d4-3b562142e547
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 1%

---

# 指定輸出的檔案位置 {#specify-file-locations-for-output}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

您可以指定Output尋找所需特定檔案型別的位置。

1. 在Administration Console中，按一下「服務>輸出」。
1. 在「位置」下，指定適當的選項。
1. 按一下「儲存」。

## 位置設定 {#locations-settings}

**內容根URI：**&#x200B;從中擷取表單之存放庫的URI或絕對位置。 此值會與sForm引數（透過API指定）結合，以建構擷取之表單的絕對路徑。 此值可參考可使用HTTP存取的目錄或Web位置。

預設值為空字串。

**XCI組態檔：**&#x200B;輸出服務用於轉譯之XCI組態檔的相對或絕對位置。 若為相對值，則假設XCI檔案位在AEM表單可部署EAR檔案中。

預設值為 `com/adobe/formServer/PA/pa_output.xci`。

**快取位置：**&#x200B;指定輸出磁碟快取的位置。 當您變更此設定時，會重設目前位置的所有現有快取資訊，並在新位置建立新的快取。 選取下列其中一個選項：

**預設位置：**&#x200B;這是預設選取範圍。 選取此選項時，會在從屬於您正在使用的應用程式伺服器的位置建立快取：

* **JBoss：** `[JBoss Home]\server\[install type]\svcdata\Output\Cache`
* **WebLogic：** `[WebLogic Home]\user_projects\domains\[aem-forms domain Name]\adobe\[Forms Server name]\Output\Cache`
* **WebSphere：** `[IBM Home]\WebSphere\AppServer\installedApps\adobe\server1\Output\Cache`

**LC Temp Directory：**&#x200B;快取是在AEM Forms暫存目錄的子目錄中建立的，該目錄是在管理主控台的[設定] > [核心系統設定] > [設定] > [暫存目錄位置]下指定的。 子目錄名為`adobeoutput_[servername]`。

>[!NOTE]
>
>如果您使用暫時清除公用程式，雖然刪除這些目錄不會影響功能，但可能會短暫地大幅影響效能，直到建立新快取為止。 為避免此問題，在清除AEM表單臨時目錄時，請勿刪除這些目錄。
