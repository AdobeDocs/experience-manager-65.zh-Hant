---
title: 外部化URL
description: Externalizer是一種OSGI服務，可讓您以程式設計方式將資源路徑轉換為外部和絕對URL
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
exl-id: 971d6c25-1fbe-4c07-944e-be6b97a59922
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# 外部化URL{#externalizing-urls}

在Adobe Experience Manager (AEM)中， **Externalizer** 是OSGI服務，可讓您以程式設計方式轉換資源路徑(例如 `/path/to/my/page`)轉換成外部和絕對URL (例如， `https://www.mycompany.com/path/to/my/page`)，請在路徑前面加上預先設定的DNS。

由於執行個體在網頁層後面執行時無法知道其外部可見的URL，而且有時必須在請求範圍之外建立連結，因此此服務會提供中央位置來設定這些外部URL並建置它們。

本頁說明如何設定 **Externalizer** 服務以及如何加以使用。 如需詳細資訊，請參閱 [Javadocs](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/Externalizer.html).

## 設定Externalizer服務 {#configuring-the-externalizer-service}

此 **Externalizer** 服務可讓您集中定義多個網域，以便用於以程式設計方式為資源路徑加上前置詞。 每個網域都由唯一名稱識別，該名稱以程式設計方式參考該網域。

若要為定義領域對應 **Externalizer** 服務：

1. 透過以下方式瀏覽至設定管理員： **工具**，然後 **網頁主控台**，或輸入：

   `https://<host>:<port>/system/console/configMgr`

1. 按一下 **Day CQ連結外部化器** 以開啟組態對話方塊。

   >[!NOTE]
   >
   >設定的直接連結為 `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

   ![aem-externalizer-01](assets/aem-externalizer-01.png)

1. 定義 **網域** 對應：對應包含唯一名稱，可用於程式碼中參照網域、空格和網域：

   `<unique-name> [scheme://]server[:port][/contextpath]`

   其中：

   * **配置** 是http或https，但也可以是ftp等。

      * 必要時使用https強制執行https連結
      * 若使用者端代碼在要求外部化URL時未覆寫配置，則會使用它。

   * **伺服器** 是主機名稱（可以是網域名稱或ip位址）。
   * **連線埠** （選用）是連線埠號碼。
   * **contextpath** （選用）只有當AEM安裝為webapp且位於不同的內容路徑下時，才會設定。

   例如：`production https://my.production.instance`

   下列對應名稱為預先定義，且必須設定，因為AEM仰賴這些名稱：

   * `local`  — 本機執行個體
   * `author`  — 編寫系統DNS
   * `publish`  — 面向公眾的網站DNS

   >[!NOTE]
   >
   >自訂設定可讓您新增類別，例如 `production`， `staging`、或甚至外部非AEM系統(例如 `my-internal-webservice`. 避免在專案的程式碼基底中跨不同位置以硬式編碼撰寫這類URL，會很有用。

1. 按一下 **儲存** 以儲存變更。

>[!NOTE]
>
>Adobe建議您 [將設定新增到存放庫](/help/sites-deploying/configuring.md#addinganewconfigurationtotherepository).

### 使用Externalizer服務 {#using-the-externalizer-service}

本節將說明以下幾個範例： **Externalizer** 可以使用服務：

1. **若要在JSP中取得Externalizer服務：**

   ```java
   Externalizer externalizer = resourceResolver.adaptTo(Externalizer.class);
   ```

1. **若要外部化具有「發佈」網域的路徑：**

   ```java
   String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
   ```

   假設網域對應：

   * `publish https://www.website.com`

   `myExternalizedUrl` 最後會得到值：

   * `https://www.website.com/contextpath/my/page.html`

1. **若要外部化具有「作者」網域的路徑：**

   ```java
   String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
   ```

   假設網域對應：

   * `author https://author.website.com`

   `myExternalizedUrl` 最後會得到值：

   * `https://author.website.com/contextpath/my/page.html`

1. **若要外部化具有「本機」網域的路徑：**

   ```java
   String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
   ```

   假設網域對應：

   * `local https://publish-3.internal`

   `myExternalizedUrl` 最後會得到值：

   * `https://publish-3.internal/contextpath/my/page.html`

1. 如需更多範例，請參閱 [Javadocs](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/Externalizer.html).
