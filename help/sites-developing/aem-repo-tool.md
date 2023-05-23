---
title: AEM Repo Tool
seo-title: AEM Repo Tool
description: 回購工AEM具是一種簡單的解決方案，可以通過與FTP類似的命令行在本地檔案系統AEM和伺服器之間傳輸JCR內容。 回購工AEM具與Jackrabbit FileVault工具類似，但速度更快，依賴性最小，而且是簡單的bash指令碼。
seo-description: The AEM Repo Tool is a simple solution to transfer JCR content between your local filesystem and the AEM server via the command line comparable to FTP. The AEM Repo Tool is similar to the Jackrabbit FileVault tool, but is faster, has minimal dependencies, and is a simple bash script.
uuid: 6c4a3504-e8e8-46c0-83cb-c18d9791f93e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 7de7b2f9-770e-4af3-8a31-c7b4de64fd43
exl-id: c46c9f0c-b0d2-4f2f-b95c-90fd3ced32a9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 2%

---

# AEM Repo Tool{#aem-repo-tool}

回購工AEM具是一種簡單的解決方案，可以通過與FTP類似的命令行在本地檔案系統AEM和伺服器之間傳輸JCR內容。 回AEM購工具與 [Jackrabbit FileVault工具](/help/sites-developing/ht-vlttool.md)，但速度較快，具有最小的依賴項，並且是一個簡單的bash指令碼。

此工具簡化了開發人員的檔案傳輸，還可以整合到IntelliJ和Eclipse中，使開發更加高效。

## 概觀 {#overview}

對於在 `jcr_root` 檔案系統上的filevault結AEM構，回購工具會為整個子樹建立一個包含單個篩選器的包，並將其推送到伺服器（類似於FTP） `put`)，從伺服器中讀取( `get`)或比較差異( `status` 和 `diff`)。

該工具不支援多個篩選器路徑或FileVault `filter.xml`。

>[!CAUTION]
>
>請注意，回AEM購工具將始終覆蓋指定的整個檔案或目錄。

## 下載和文檔 {#download-and-documentation}

的 [GitHubAEM上可通過此連結提供回購工具](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) 以及詳細的安裝和使用說明。

如果要下載回購工具的AEM源，請參閱下面連結的GitHub項目。

GITHUB代碼

可以在GitHub上找到此頁的代碼

* [在GitHub上開啟工具項目](https://github.com/Adobe-Marketing-Cloud/tools)
* 將項目下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)
