---
title: AEM Repo Tool
seo-title: AEM Repo Tool
description: AEM Repo Tool是一個簡單的解決方案，可透過與FTP相仿的命令列，在本機檔案系統與AEM伺服器之間傳輸JCR內容。 AEM Repo Tool與Jackrabbit FileVault工具類似，但速度較快、相依性最低，且是簡單的bash指令碼。
seo-description: AEM Repo Tool是一個簡單的解決方案，可透過與FTP相仿的命令列，在本機檔案系統與AEM伺服器之間傳輸JCR內容。 AEM Repo Tool與Jackrabbit FileVault工具類似，但速度較快、相依性最低，且是簡單的bash指令碼。
uuid: 6c4a3504-e8e8-46c0-83cb-c18d9791f93e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 7de7b2f9-770e-4af3-8a31-c7b4de64fd43
exl-id: c46c9f0c-b0d2-4f2f-b95c-90fd3ced32a9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 2%

---

# AEM Repo Tool{#aem-repo-tool}

AEM Repo Tool是一個簡單的解決方案，可透過與FTP相仿的命令列，在本機檔案系統與AEM伺服器之間傳輸JCR內容。 AEM Repo Tool與[Jackrabbit FileVault工具](/help/sites-developing/ht-vlttool.md)類似，但速度較快、相依性最小，且是簡單的bash指令碼。

此工具可簡化開發人員的檔案傳輸，也可整合至IntelliJ和Eclipse，讓開發更有效率。

## 概覽 {#overview}

對於檔案系統上`jcr_root`檔案預設結構內的給定路徑，AEM Repo Tool會為整個子樹建立一個包，並將其推送到伺服器（類似於FTP `put`）、從伺服器中提取該路徑(`get`)或比較差異（`status`和`diff`）。

該工具不支援多個篩選路徑或FileVault的`filter.xml`。

>[!CAUTION]
>
>請注意，AEM Repo Tool一律會覆寫指定的整個檔案或目錄。

## 下載和文檔{#download-and-documentation}

[AEM Repo Tool可透過此連結](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo)在GitHub上取得，並附上詳細的安裝與使用指示。

如果您想要下載AEM Repo Tool的來源，請參閱下方連結的GitHub專案。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟工具專案](https://github.com/Adobe-Marketing-Cloud/tools)
* 將專案下載為[a ZIP檔案](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)
