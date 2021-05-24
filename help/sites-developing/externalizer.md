---
title: 將URL外部化
seo-title: 將URL外部化
description: Externalizer是OSGI服務，可讓您以程式設計方式將資源路徑轉換為外部和絕對URL
seo-description: Externalizer是OSGI服務，可讓您以程式設計方式將資源路徑轉換為外部和絕對URL
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
source-wordcount: '523'
ht-degree: 0%

---

# 將URL外部化{#externalizing-urls}

在AEM中，**Externalizer**&#x200B;是OSGI服務，可讓您以程式設計方式轉換資源路徑(例如`/path/to/my/page`)填入外部和絕對URL（例如`https://www.mycompany.com/path/to/my/page`），方法是使用預先設定的DNS來預先修正路徑。

由於執行個體在Web層後面執行時無法知道其外部可見的URL，且由於有時必須在請求範圍之外建立連結，因此此服務提供一個集中位置來設定這些外部URL並建置它們。

本頁說明如何配置&#x200B;**Externalizer**&#x200B;服務以及如何使用它。 有關更多詳細資訊，請參閱[Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html)。

## 配置Externalizer服務{#configuring-the-externalizer-service}

**Externalizer**&#x200B;服務允許您集中定義多個域，這些域可用於以寫程式方式為資源路徑加上前置詞。 每個網域都以唯一名稱識別，該名稱用於以程式設計方式參考網域。

要定義&#x200B;**Externalizer**&#x200B;服務的域映射：

1. 透過&#x200B;**Tools**，然後導覽至&#x200B;**Web Console**，或輸入：

   `https://<host>:<port>/system/console/configMgr`

1. 按一下&#x200B;**Day CQ Link Externalizer**&#x200B;以開啟設定對話方塊。

   >[!NOTE]
   >
   >配置的直接連結為`https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

   ![aem-externalizer-01](assets/aem-externalizer-01.png)

1. 定義&#x200B;**Domains**&#x200B;對應：映射由唯一名稱組成，該名稱可在代碼中用於引用域、空格和域：

   `<unique-name> [scheme://]server[:port][/contextpath]`

   其中：

   * **** 架構通常為http或https，但也可以是ftp等。

      * 視需要使用https強制https連結
      * 若要求將URL外部化時用戶端代碼未覆寫配置，則會使用此URL。
   * **** server是主機名（可以是域名或ip地址）。
   * **port** （可選）是埠號。
   * **只有當AEM安裝為位於不同內容路徑下的網頁應用程式時，才會設定contextpath** （選用）。

   例如：`production https://my.production.instance`

   下列對應名稱是預先定義的，且必須一律設定，因為AEM需仰賴這些名稱：

   * `local`  — 本機執行個體
   * `author`  — 編寫系統DNS
   * `publish`  — 公開對應的網站DNS

   >[!NOTE]
   >
   >自訂設定可讓您新增新類別，例如`production`、`staging`或甚至外部非AEM系統，例如`my-internal-webservice`。 建議您避免在專案的程式碼基底中不同位置以硬式編碼撰寫此類URL。

1. 按一下&#x200B;**儲存**&#x200B;以儲存變更。

>[!NOTE]
>
>Adobe建議您[將配置添加到儲存庫](/help/sites-deploying/configuring.md#addinganewconfigurationtotherepository)。

### 使用Externalizer服務{#using-the-externalizer-service}

本節顯示如何使用&#x200B;**Externalizer**&#x200B;服務的一些示例：

1. **要在JSP中獲取Externalizer服務，請執行以下操作：**

   ```java
   Externalizer externalizer = resourceResolver.adaptTo(Externalizer.class);
   ```

1. **若要將具有&#39;publish&#39;網域的路徑外部化：**

   ```java
   String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
   ```

   假設網域對應：

   * `publish https://www.website.com`

   `myExternalizedUrl` 結尾為值：

   * `https://www.website.com/contextpath/my/page.html`


1. **若要將具有「作者」網域的路徑外部化：**

   ```java
   String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
   ```

   假設網域對應：

   * `author https://author.website.com`

   `myExternalizedUrl` 結尾為值：

   * `https://author.website.com/contextpath/my/page.html`


1. **要將具有&#39;local&#39;域的路徑外部化：**

   ```java
   String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
   ```

   假設網域對應：

   * `local https://publish-3.internal`

   `myExternalizedUrl` 結尾為值：

   * `https://publish-3.internal/contextpath/my/page.html`


1. 您可以在[Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html)中找到更多範例。
