---
title: 指定輸出的檔案位置
seo-title: Specify file locations for Output
description: 了解如何指定輸出的檔案位置。
seo-description: Learn how to specify file locations for Output.
uuid: 3287274f-85b5-4811-8abb-d347a9b80947
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 460bbb31-8187-469c-8102-b310093b6c03
exl-id: 620c69d6-4fe1-46d6-b5d4-3b562142e547
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 1%

---

# 指定輸出的檔案位置 {#specify-file-locations-for-output}

您可以指定「輸出」在哪些位置查找它所需的特定類型檔案。

1. 在管理控制台中，按一下「服務>輸出」。
1. 在「位置」下，指定適當的選項。
1. 按一下「儲存」。

## 位置設定 {#locations-settings}

**內容根URI:** 從中檢索表單的儲存庫的URI或絕對位置。 此值會與透過API指定的sForm參數結合，以建構擷取之表單的絕對路徑。 此值可參考使用HTTP存取的目錄或Web位置。

預設值為空字串。

**XCI配置檔案：** 輸出服務用於呈現的XCI配置檔案的相對或絕對位置。 對於相對值，假設XCI檔案位於AEM表單可部署EAR檔案中。

預設值為 `com/adobe/formServer/PA/pa_output.xci`。

**快取位置：** 指定輸出磁碟快取的位置。 更改此設定時，當前位置的所有現有快取資訊都會重置，並在新位置建立新快取。 選取下列其中一個選項：

**預設位置：** 這是預設選取項目。 選中此選項時，快取將建立在與所使用的應用程式伺服器相關的位置：

* **JBoss:** `[JBoss Home]\server\[install type]\svcdata\Output\Cache`
* **WebLogic:** `[WebLogic Home]\user_projects\domains\[aem-forms domain Name]\adobe\[forms server name]\Output\Cache`
* **WebSphere:** `[IBM Home]\WebSphere\AppServer\installedApps\adobe\server1\Output\Cache`

**LC臨時目錄：** 快取建立在AEM Forms臨時目錄的子目錄中，該子目錄在管理控制台的「設定>核心繫統設定>配置>臨時目錄的位置」下指定。 子目錄已命名 `adobeoutput_[servername]`.

>[!NOTE]
>
>如果您使用臨時清除實用程式，請注意，刪除這些目錄不會影響功能，但在建立新快取之前，這會在短時間內對效能造成重大影響。 要避免此問題，清除AEM表單臨時目錄時，請勿刪除這些目錄。
