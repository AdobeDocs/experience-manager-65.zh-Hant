---
title: AEM Repo Tool
description: AEM Repo Tool是簡單的解決方案，可透過類似FTP的命令列，在本機檔案系統與AEM伺服器之間傳輸JCR內容。 AEM Repo工具類似於Jackrabbit FileVault工具，但速度更快、相依性最低，而且是簡單的bash指令碼。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: c46c9f0c-b0d2-4f2f-b95c-90fd3ced32a9
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: f2d27a5f-0d67-4d85-8a24-86a8d8a3574b
    internal-label: Developer tools
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 2%
---
# AEM Repo Tool{#aem-repo-tool}

AEM Repo Tool是簡單的解決方案，可透過類似FTP的命令列，在本機檔案系統與AEM伺服器之間傳輸JCR內容。 AEM Repo Tool類似於[Jackrabbit FileVault tool](/help/sites-developing/ht-vlttool.md)，但速度更快、相依性最少，而且是簡單的bash指令碼。

此工具可為開發人員簡化檔案傳輸，也可整合至IntelliJ和Eclipse，讓開發更有效率。

## 概觀 {#overview}

針對檔案系統上`jcr_root`檔案檔案檔案檔案結構內的指定路徑，AEM Repo Tool會建立包含整個子樹狀結構單一篩選器的套件，並將其推送到伺服器（類似FTP `put`）、從伺服器( `get`)擷取它，或比較差異（`status`和`diff`）。

工具不支援多個篩選路徑或FileVault的`filter.xml`。

>[!CAUTION]
>
>AEM Repo工具一律會覆寫指定的整個檔案或目錄。

## 下載和檔案 {#download-and-documentation}

[AEM Repo Tool可透過此連結](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo)在GitHub上取得，並附上詳細的安裝和使用指示。

如果您想要下載AEM Repo工具的來源，請參閱下方連結的GitHub專案。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟工具專案](https://github.com/Adobe-Marketing-Cloud/tools)
* 將專案下載為[ZIP檔](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)
