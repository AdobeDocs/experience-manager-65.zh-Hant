---
title: 如何使用Apache Maven建置AEM專案
description: 本檔案說明如何根據Apache Maven設定AEM專案
exl-id: 451913bf-bb1e-4444-aee5-968ac30b5c9d
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
source-wordcount: '166'
ht-degree: 15%
---
# 如何使用Apache Maven建置AEM專案 {#how-to-build-aem-projects-using-apache-maven}

AEM 6.5遵循套件管理和專案結構的最新最佳做法，這些最佳做法由適用於內部部署和AMS實施的最新AEM專案原型實施。

>[!TIP]
>
>如需詳細資訊，請參閱：
>
>* AEM as a Cloud Service檔案中的[AEM專案結構](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)文章，說明如何結構現代AEM專案。
>* [AEM專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)檔案，說明如何使用原型啟動新的AEM專案。
>* AEM as a Cloud Service檔案中的[Adobe Content Package Maven外掛程式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developer-tools/maven-plugin.html#developer-tools)文章，說明如何部署AEM應用程式。
>
>全部三份檔案皆適用於AEM 6.5。
