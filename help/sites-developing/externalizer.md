---
title: 外部化URL
seo-title: 外部化URL
description: Externalizer是OSGI服務，可讓您以程式設計方式將資源路徑轉換為外部和絕對URL
seo-description: Externalizer是OSGI服務，可讓您以程式設計方式將資源路徑轉換為外部和絕對URL
uuid: 65bcc352-fc8c-4aa0-82fb-1321a035602d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 938469ad-f466-42f4-8b6f-bfc060ae2785
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# 外部化URL{#externalizing-urls}

在AEM中， **Externalizer** 是OSGI服務，可讓您以程式設計方式轉換資源路徑(例如 `/path/to/my/page`)加入外部和絕對URL(例如 `https://www.mycompany.com/path/to/my/page`)，方法是使用預先設定的DNS來預先固定路徑。

由於例項在Web層後面執行時無法知道其外部可見的URL，而且有時必須在請求範圍外建立連結，因此此服務提供一個集中位置來設定這些外部URL並建立它們。

本頁說明如何設定 **Externalizer** service，以及如何使用它。 如需詳細資訊，請參閱 [Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html)。

## 配置Externalizer服務 {#configuring-the-externalizer-service}

Externalizer **** service可讓您集中定義多個網域，可用來以程式設計方式為資源路徑加上前置詞。 每個網域都由唯一名稱來識別，該名稱用於以程式設計方式參考網域。

要定義 **Externalizer服務的域映射** :

1. 通過工具依次導航至配 **置管理器**, **然後輸入**:

   `https://<host>:<port>/system/console/configMgr`

1. 按一 **下「日CQ連結外部化** 」以開啟設定對話方塊。

   >[!NOTE]
   >
   >配置的直接連結是 `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

   ![aem-externalizer-01](assets/aem-externalizer-01.png)

1. 定義網 **域** 映射：映射由唯一名稱組成，可用於代碼中以引用域、空間和域：

   `<unique-name> [scheme://]server[:port][/contextpath]`

   其中：

   * **scheme** 通常為http或https，但也可以是ftp等。

      * 視需要使用https來強制https連結
      * 當用戶端程式碼要求將URL外部化時，不會覆寫配置時，就會使用它。
   * **server** 是主機名（可以是域名或IP地址）。
   * **port** （可選）是埠號。
   * **contextpath** （選用）只有在AEM安裝為位於不同內容路徑下的網頁應用程式時才會設定。
   例如： `production https://my.production.instance`

   下列對應名稱是預先定義的，必須一律設定，因為AEM需仰賴這些名稱：

   * `local` -本機例項
   * `author` -編寫系統DNS
   * `publish` -公眾對應網站DNS
   >[!NOTE]
   >
   >自訂設定可讓您新增類別，例如 `production`, `staging` 甚至外部非AEM系統，例如 `my-internal-webservice`。 避免在專案程式碼基底的不同位置硬式編碼此類URL，會很有用。

1. 按一 **下「儲存** 」以儲存變更。

>[!NOTE]
>
>Adobe建議您將 [設定新增至儲存庫](/help/sites-deploying/configuring.md#addinganewconfigurationtotherepository)。

### 使用Externalizer服務 {#using-the-externalizer-service}

本節說明如何使用 **Externalizer** service的幾個範例：

1. **要在JSP中獲取Externalizer服務，請執行以下操作：**

   ```java
   Externalizer externalizer = resourceResolver.adaptTo(Externalizer.class);
   ```

1. **若要將路徑外部化為具有「發佈」網域：**

   ```java
   String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
   ```

   假設域映射：

   * `publish https://www.website.com`
   `myExternalizedUrl` 最後是值：

   * `https://www.website.com/contextpath/my/page.html`


1. **要將具有「author」域的路徑外部化：**

   ```java
   String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
   ```

   假設域映射：

   * `author https://author.website.com`
   `myExternalizedUrl` 最後是值：

   * `https://author.website.com/contextpath/my/page.html`


1. **要將具有「本地」域的路徑外部化：**

   ```java
   String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
   ```

   假設域映射：

   * `local https://publish-3.internal`
   `myExternalizedUrl` 最後是值：

   * `https://publish-3.internal/contextpath/my/page.html`


1. 您可以在 [Javadocs中找到更多範例](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html)。
