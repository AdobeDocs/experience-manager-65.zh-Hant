---
title: 疑難排解社群
description: 瞭解社群的疑難排解，包括已知問題和顧慮。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: ef4f4108-c485-4e2e-a58f-ff64eee9937e
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---

# 疑難排解社群 {#troubleshooting}

本節包含疑難排解Community時的常見問題和已知問題。

## 已知問題 {#known-issues}

### Dispatcher重新擷取失敗 {#dispatcher-refetch-fails}

將Dispatcher 4.1.5與較新版本的Jetty搭配使用時，重新擷取可能會在等候請求逾時後導致「無法從遠端伺服器接收回應」。

使用Dispatcher 4.1.6或更新版本可解決此問題。

### 從CQ 5.4升級後無法存取論壇貼文 {#cannot-access-forum-post-after-upgrading-from-cq}

如果在CQ 5.4上建立了論壇並張貼了主題，然後網站升級為AEM 5.6.1或更新版本，則嘗試檢視現有文章可能會導致頁面上的錯誤：

不合法的模式字元&#39;a&#39;無法將請求提供給 `/content/demoforums/forum-test.html` 此伺服器的記錄檔包含下列專案：

```xml
20.03.2014 22:49:35.805 ERROR [10.177.45.32 [1395380975744] GET /content/demoforums/forum-test.html HTTP/1.1] com.day.cq.wcm.tags.IncludeTag Error while executing script content.jsp
org.apache.sling.api.scripting.ScriptEvaluationException:
at org.apache.sling.scripting.core.impl.DefaultSlingScript.call(DefaultSlingScript.java:388)
at org.apache.sling.scripting.core.impl.DefaultSlingScript.eval(DefaultSlingScript.java:171)
```

問題是com.day.cq.commons.date.RelativeTimeFormat的格式字串在5.4和5.5之間已變更，使得「ago」的「a」不再被接受。

因此，使用RelativeTimeFormat() API的任何程式碼都必須變更：

* 從： `final RelativeTimeFormat fmt = new RelativeTimeFormat("r a", resourceBundle);`
* 至： `final RelativeTimeFormat fmt = new RelativeTimeFormat("r", resourceBundle);`

「作者」和「發佈」上的失敗不同。 在作者上，它只會無訊息地失敗，不會顯示論壇主題。 發佈時，會在頁面上擲回錯誤。

請參閱 [com.day.cq.commons.date.RelativeTimeFormat](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/date/RelativeTimeFormat.html) API以取得詳細資訊。

## 常見問題 {#common-concerns}

### 記錄檔中的警告：已棄用Handlebars {#warning-in-logs-handlebars-deprecated}

在啟動期間（不是第一個，但之後的每一個），可能會在紀錄中看到以下警告：

* `11.04.2014 08:38:07.223 WARN [FelixStartLevel]com.github.jknack.handlebars.Handlebars Helper 'i18n'` 已取代為 `com.adobe.cq.social.handlebars.I18nHelper@15bac645`

此警告可以安全地忽略，因為 `jknack.handlebars.Handlebars`，使用者： [SCF](scf.md#handlebarsjavascripttemplatinglanguage)，隨附自己的i18n協助程式公用程式。 啟動時，此變數會被AEM專屬的變數取代 [i18n協助程式](handlebars-helpers.md#i-n). 此警告由協力廠商程式庫產生，以確認覆寫現有的協助程式。

### 記錄檔中有警告： OakResourceListener processOsgiEventQueue {#warning-in-logs-oakresourcelistener-processosgieventqueue}

張貼多個Social Communities論壇主題可能會導致OakResourceListener processOsgiEventQueue產生大量警告和資訊記錄。

這些警告可以安全地忽略。

```xml
23.04.2014 14:21:18.900 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/search-collections/ugc-sc/_m.frq/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.908 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/search-collections/ugc-sc/_m.prx/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.909 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/67/67699ab5-9d57-4c79-a755-2727ba9e6452/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.909 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/67/67699ab5-9d57-4c79-a755-2727ba9e6452/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.990 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/b9/b91f1690-87e8-41d8-a78e-cd2259f837c8/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.990 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/b9/b91f1690-87e8-41d8-a78e-cd2259f837c8/jcr:content not found, which is not expected for an added or modified node
```

### 記錄檔錯誤：IndexElementFactory的NoClassDefFoundError {#error-in-logs-noclassdeffounderror-for-indexelementfactory}

將AEM 5.6.1升級至最新的cq-socialcommunities-pkg-1.4.x或AEM 6.0，會導致記錄檔出現錯誤。 此問題會在條件啟動期間發生，而條件會自我解析，以重新啟動時未看到錯誤為證據。

```xml
14.11.2013 20:52:39.453 ERROR [Apache Sling JCR Resource Event Queue Processor for path '/'] com.adobe.cq.social.storage.index.impl.IndexService Error occurred while processing event java.util.ConcurrentModificationException
14.11.2013 20:52:40.716 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory) java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory
14.11.2013 20:52:40.717 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Failed creating the component instance; see log for reason
```
