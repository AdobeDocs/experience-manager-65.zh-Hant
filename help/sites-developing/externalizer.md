---
title: 外部化URL
description: Externalizer是一種OSGI服務，可讓您以程式設計方式將資源路徑轉換為外部和絕對URL
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
exl-id: 971d6c25-1fbe-4c07-944e-be6b97a59922
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# 外部化URL{#externalizing-urls}

在Adobe Experience Manager (AEM)中，**外部化程式**&#x200B;是OSGI服務，可讓您以程式設計方式將資源路徑（例如`/path/to/my/page`）轉換為外部和絕對URL （例如`https://www.mycompany.com/path/to/my/page`），方法是以預先設定的DNS為路徑加上前置詞。

由於執行個體在網頁層後面執行時無法知道其外部可見的URL，而且有時必須在請求範圍之外建立連結，因此此服務會提供中央位置來設定這些外部URL並建置它們。

此頁面說明如何設定&#x200B;**Externalizer**&#x200B;服務以及如何使用它。 如需詳細資訊，請參閱[Javadocs](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/Externalizer.html)。

## 設定Externalizer服務 {#configuring-the-externalizer-service}

**Externalizer**&#x200B;服務可讓您集中定義多個網域，以便以程式設計方式為資源路徑加上前置詞。 每個網域都由唯一名稱識別，該名稱以程式設計方式參考該網域。

若要定義&#x200B;**Externalizer**&#x200B;服務的網域對應：

1. 透過&#x200B;**工具**，然後透過&#x200B;**網頁主控台**&#x200B;瀏覽至組態管理員，或輸入：

   `https://<host>:<port>/system/console/configMgr`

1. 按一下&#x200B;**Day CQ Link Externalizer**&#x200B;以開啟設定對話方塊。

   >[!NOTE]
   >
   >設定的直接連結是`https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

   ![aem-externalizer-01](assets/aem-externalizer-01.png)

1. 定義&#x200B;**網域**&#x200B;對應：對應包含唯一的名稱，可在程式碼中用來參考網域、空格和網域：

   `<unique-name> [scheme://]server[:port][/contextpath]`

   其中：

   * **配置**&#x200B;是http或https，但也可以是ftp等等。

      * 必要時使用https強制執行https連結
      * 若使用者端代碼在要求外部化URL時未覆寫配置，則會使用它。

   * **server**&#x200B;是主機名稱（可以是網域名稱或ip位址）。
   * **連線埠** （選擇性）是連線埠號碼。
   * **contextpath** （選擇性）只有在將AEM安裝為webapp時，才會設定在不同的內容路徑下。

   例如：`production https://my.production.instance`

   下列對應名稱為預先定義，且必須設定，因為AEM仰賴這些名稱：

   * `local` — 本機執行個體
   * `author` — 編寫系統DNS
   * `publish` — 面向公眾的網站DNS

   >[!NOTE]
   >
   >自訂組態可讓您新增類別，例如`production`、`staging`，或甚至外部非AEM系統，例如`my-internal-webservice`。 避免在專案的程式碼基底中跨不同位置以硬式編碼撰寫這類URL，會很有用。

1. 按一下[儲存]儲存變更。****

>[!NOTE]
>
>Adobe建議您[將組態新增到存放庫](/help/sites-deploying/configuring.md#addinganewconfigurationtotherepository)。

### 使用Externalizer服務 {#using-the-externalizer-service}

本節說明如何使用&#x200B;**Externalizer**&#x200B;服務的幾個範例：

1. **若要取得JSP中的Externalizer服務：**

   ```java
   Externalizer externalizer = resourceResolver.adaptTo(Externalizer.class);
   ```

1. **若要外部化具有&#39;publish&#39;網域的路徑：**

   ```java
   String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
   ```

   假設網域對應：

   * `publish https://www.website.com`

   `myExternalizedUrl`結尾是值：

   * `https://www.website.com/contextpath/my/page.html`

1. **若要外部化具有&#39;author&#39;網域的路徑：**

   ```java
   String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
   ```

   假設網域對應：

   * `author https://author.website.com`

   `myExternalizedUrl`結尾是值：

   * `https://author.website.com/contextpath/my/page.html`

1. **若要外部化具有&#39;local&#39;網域的路徑：**

   ```java
   String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
   ```

   假設網域對應：

   * `local https://publish-3.internal`

   `myExternalizedUrl`結尾是值：

   * `https://publish-3.internal/contextpath/my/page.html`

1. 您可以在[Javadocs](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/Externalizer.html)中找到更多範例。
