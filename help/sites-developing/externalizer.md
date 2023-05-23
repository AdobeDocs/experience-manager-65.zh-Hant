---
title: 外部化URL
seo-title: Externalizing URLs
description: Externalizer是OSGI服務，它允許您以寫程式方式將資源路徑轉換為外部和絕對URL
seo-description: The Externalizer is an OSGI service that allows you to programmatically transform a resource path into an external and absolute URL
uuid: 65bcc352-fc8c-4aa0-82fb-1321a035602d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 938469ad-f466-42f4-8b6f-bfc060ae2785
docset: aem65
exl-id: 971d6c25-1fbe-4c07-944e-be6b97a59922
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---

# 外部化URL{#externalizing-urls}

在AEM中 **外部化器** 是一種OSGI服務，它允許您以寫程式方式轉換資源路徑(例如， `/path/to/my/page`)到外部和絕對URL(例如， `https://www.mycompany.com/path/to/my/page`)，方法是使用預配置的DNS預先固定路徑。

由於實例在Web層後面運行時無法知道其外部可見URL，並且由於有時必須在請求範圍之外建立連結，因此此服務提供了一個中心位置來配置這些外部URL並生成它們。

本頁說明如何配置 **外部化器** 服務和使用方法。 有關詳細資訊，請參閱 [賈瓦多克](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html)。

## 配置Externalizer服務 {#configuring-the-externalizer-service}

的 **外部化器** 服務允許您集中定義多個域，這些域可用於以寫程式方式為資源路徑添加前置詞。 每個域都由用於以寫程式方式引用域的唯一名稱標識。

定義域映射 **外部化器** 服務：

1. 通過導航到配置管理器 **工具**，則 **Web控制台**，或輸入：

   `https://<host>:<port>/system/console/configMgr`

1. 按一下 **第CQ天連結外部化程式** 的子菜單。

   >[!NOTE]
   >
   >到配置的直接連結是 `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

   ![aem-externalizer-01](assets/aem-externalizer-01.png)

1. 定義 **域** 映射：映射由唯一名稱組成，可在代碼中用於引用域、空間和域：

   `<unique-name> [scheme://]server[:port][/contextpath]`

   其中：

   * **方案** 通常是http或https，但也可以是ftp等。

      * 如果需要，使用https強制https連結
      * 如果客戶端代碼在請求將URL外部化時未覆蓋方案，則將使用它。
   * **伺服器** 是主機名（可以是域名或ip地址）。
   * **埠** （可選）是埠號。
   * **上下文路徑** （可選）僅當作為Webapp安裝AEM在其他上下文路徑下時才設定。

   例如：`production https://my.production.instance`

   以下映射名稱是預定義的，必須始終根據它們AEM進行設定：

   * `local`  — 本地實例
   * `author`  — 創作系統DNS
   * `publish`  — 面向公眾的網站DNS

   >[!NOTE]
   >
   >自定義配置允許您添加新類別，如 `production`。 `staging` 甚至外部非系AEM統，例如 `my-internal-webservice`。 避免在項目代碼庫的不同位置對此類URL進行硬編碼是有用的。

1. 按一下 **保存** 的子菜單。

>[!NOTE]
>
>Adobe建議您 [將配置添加到儲存庫](/help/sites-deploying/configuring.md#addinganewconfigurationtotherepository)。

### 使用Externalizer服務 {#using-the-externalizer-service}

本節顯示了以下幾個示例： **外部化器** 可以使用服務：

1. **要在JSP中獲取Externalizer服務：**

   ```java
   Externalizer externalizer = resourceResolver.adaptTo(Externalizer.class);
   ```

1. **要將路徑與「publish」域外部化：**

   ```java
   String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
   ```

   假定域映射：

   * `publish https://www.website.com`

   `myExternalizedUrl` 最後是值：

   * `https://www.website.com/contextpath/my/page.html`


1. **要將路徑與「author」域外部化：**

   ```java
   String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
   ```

   假定域映射：

   * `author https://author.website.com`

   `myExternalizedUrl` 最後是值：

   * `https://author.website.com/contextpath/my/page.html`


1. **要將路徑與「local」域外部化：**

   ```java
   String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
   ```

   假定域映射：

   * `local https://publish-3.internal`

   `myExternalizedUrl` 最後是值：

   * `https://publish-3.internal/contextpath/my/page.html`


1. 可以在 [賈瓦多克](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html)。
