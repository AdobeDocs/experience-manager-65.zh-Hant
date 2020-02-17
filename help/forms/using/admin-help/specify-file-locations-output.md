---
title: 指定輸出的檔案位置
seo-title: 指定輸出的檔案位置
description: 瞭解如何指定「輸出」的檔案位置。
seo-description: 瞭解如何指定「輸出」的檔案位置。
uuid: 3287274f-85b5-4811-8abb-d347a9b80947
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 460bbb31-8187-469c-8102-b310093b6c03
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 指定輸出的檔案位置 {#specify-file-locations-for-output}

您可以指定「輸出」在何處查找所需的特定類型檔案。

1. 在管理控制台中，按一下「服務>輸出」。
1. 在「位置」下，指定適當的選項。
1. 按一下「儲存」。

## 位置設定 {#locations-settings}

**** 內容根URI:從中檢索表單的儲存庫的URI或絕對位置。 此值會與sForm參數（透過API指定）結合，以建構擷取之表單的絕對路徑。 此值可以引用可使用HTTP訪問的目錄或Web位置。

預設值為空字串。

**** XCI配置檔案：輸出服務用於渲染的XCI配置檔案的相對或絕對位置。 對於相對值，會假設XCI檔案位於AEM表單可部署的EAR檔案中。

預設值為 `com/adobe/formServer/PA/pa_output.xci`。

**** 快取位置：指定輸出磁碟快取的位置。 更改此設定時，將重置當前位置的所有現有快取資訊，並在新位置建立新快取。 選擇下列選項之一：

**** 預設位置：這是預設選擇。 選取此選項時，快取會建立在與您所使用之應用程式伺服器相關的位置：

* **** JBoss: `[JBoss Home]\server\[install type]\svcdata\Output\Cache`
* **** WebLogic: `[WebLogic Home]\user_projects\domains\[aem-forms domain Name]\adobe\[forms server name]\Output\Cache`
* **** WebSphere: `[IBM Home]\WebSphere\AppServer\installedApps\adobe\server1\Output\Cache`

**** LC臨時目錄：快取會建立在AEM forms temp目錄的子目錄中，此目錄會在管理控制台中的「設定>核心繫統設定>組態>臨時目錄位置」下指定。 子目錄名為 `adobeoutput_[servername]`。

>[!NOTE]
>
>如果您使用臨時清除實用程式，請注意，刪除這些目錄不會影響功能，但在建立新快取之前，它可能會在短時間內顯著影響效能。 若要避免此問題，請勿在清除AEM表單temp目錄時刪除這些目錄。

