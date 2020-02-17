---
title: AEM Repo工具
seo-title: AEM Repo工具
description: AEM Repo tool是一套簡單的解決方案，可讓您透過類似FTP的命令列，在本機檔案系統與AEM伺服器之間傳輸JCR內容。 AEM Repo tool類似Jackrabbit FileVault工具，但速度更快、相依性最小，而且是簡單的bash指令碼。
seo-description: AEM Repo tool是一套簡單的解決方案，可讓您透過類似FTP的命令列，在本機檔案系統與AEM伺服器之間傳輸JCR內容。 AEM Repo tool類似Jackrabbit FileVault工具，但速度更快、相依性最小，而且是簡單的bash指令碼。
uuid: 6c4a3504-e8e8-46c0-83cb-c18d9791f93e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 7de7b2f9-770e-4af3-8a31-c7b4de64fd43
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# AEM Repo工具{#aem-repo-tool}

AEM Repo tool是一套簡單的解決方案，可讓您透過類似FTP的命令列，在本機檔案系統與AEM伺服器之間傳輸JCR內容。 AEM Repo tool類似 [Jackrabbit FileVault工具](/help/sites-developing/ht-vlttool.md)，但速度更快、相依性最小，而且是簡單的bash指令碼。

此工具可簡化開發人員檔案的傳輸作業，也可整合至IntelliJ和Eclipse，讓開發工作更有效率。

## 概覽 {#overview}

對於檔案系統上檔案預設結構內的指定路徑，AEM Repo Tool會針對整個子樹建立包含單一篩選器的套件，並將其推送至伺服器(類似於FTP `jcr_root` )、從伺服器擷取( `put`)或比較差異( `get`and `status``diff`)。

此工具不支援多個篩選路徑或FileVault的篩選路徑 `filter.xml`。

>[!CAUTION]
>
>請注意，AEM Repo Tool一律會覆寫指定的整個檔案或目錄。

## 下載和檔案 {#download-and-documentation}

AEM Repo Tool [可透過此連結](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) ，以及詳細的安裝與使用指示，在GitHub上提供。

如果您想要下載AEM Repo Tool的來源，請參閱下方連結的GitHub專案。

GITHUB代碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟工具專案](https://github.com/Adobe-Marketing-Cloud/tools)
* 將專案下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)

