---
title: 疑難排解
seo-title: 疑難排解
description: 疑難排解社群（包括已知問題）
seo-description: 疑難排解社群（包括已知問題）
uuid: 99225430-fa2a-4393-ae5a-18b19541c358
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: cdb2d80a-2fbf-4ee6-b89b-b5d74e6d3bfc
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# 疑難排解 {#troubleshooting}

本節包含共同關切和已知問題。

## 已知問題 {#known-issues}

### Dispatcher Refetch失敗 {#dispatcher-refetch-fails}

當將Dispatcher 4.1.5與較新版本的Jetty一起使用時，重新讀取可能會在等待請求超時後導致「無法從遠程伺服器接收響應」。

使用Dispatcher 4.1.6或更新版本將解決此問題。

### 從CQ 5.4升級後無法存取論壇貼文 {#cannot-access-forum-post-after-upgrading-from-cq}

如果論壇是在CQ 5.4上建立並張貼主題，然後網站已升級至AEM 5.6.1或更新版本，嘗試檢視現有貼文可能會在頁面上造成錯誤：

非法模式字元&#39;a無法在此伺服器上將要求傳送至/content/demoforums/forum-test.html

而記錄檔包含下列內容：

```xml
20.03.2014 22:49:35.805 ERROR [10.177.45.32 [1395380975744] GET /content/demoforums/forum-test.html HTTP/1.1] com.day.cq.wcm.tags.IncludeTag Error while executing script content.jsp
org.apache.sling.api.scripting.ScriptEvaluationException:
at org.apache.sling.scripting.core.impl.DefaultSlingScript.call(DefaultSlingScript.java:388)
at org.apache.sling.scripting.core.impl.DefaultSlingScript.eval(DefaultSlingScript.java:171)
```

問題是com.day.cq.commons.date.RelativeTimeFormat的格式字串在5.4和5.5之間變更，因此不再接受&quot;ago&quot;的&quot;a&quot;。

因此，使用RelativeTimeFormat()API的任何程式碼都需要變更

* 從: `final RelativeTimeFormat fmt = new RelativeTimeFormat("r a", resourceBundle);`
* 至: `final RelativeTimeFormat fmt = new RelativeTimeFormat("r", resourceBundle);`

作者和發佈上的失敗不同。 在作者上，它會無訊息地失敗，而且不會顯示論壇主題。 在發佈時，會在頁面上引發錯誤。

如需詳 [細資訊，請參閱com.day.cq.commons.date.RelativeTimeFormat](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/date/RelativeTimeFormat.html) API。

## 常見問題 {#common-concerns}

### 記錄檔警告：已過時的車把 {#warning-in-logs-handlebars-deprecated}

在啟動期間（不是第1次——但之後的每次），記錄檔中可能會出現下列警告：

* 11.04.2014 08:38:07.223 **WARN**[]FelixStartLevelcom.github.jkank.handlebars.Handlebars Helper &#39;i18n&#39;已由&#39;com.adobe.cq.social.handlebars.I18nHelper@15bac645&#39;取代

此警告可以安全地忽略，因為 [SCF](scf.md#handlebarsjavascripttemplatinglanguage)，使用jkanc.handlebars。Handlebars隨附其i18n輔助工具。 啟動時，會以AEM專用的 [i18n協助程式取代它](handlebars-helpers.md#i-n)。 此警告由協力廠商程式庫產生，以確認覆寫現有協助程式。

### 記錄檔警告：OakResourceListener processOsgiEventQueue {#warning-in-logs-oakresourcelistener-processosgieventqueue}

張貼許多Social Communities論壇主題可能會產生大量來自OakResourceListener processOsgiEventQueue的警告和資訊記錄檔。

這些警告可以安全地忽略。

```xml
23.04.2014 14:21:18.900 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/search-collections/ugc-sc/_m.frq/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.908 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/search-collections/ugc-sc/_m.prx/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.909 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/67/67699ab5-9d57-4c79-a755-2727ba9e6452/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.909 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/67/67699ab5-9d57-4c79-a755-2727ba9e6452/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.990 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/b9/b91f1690-87e8-41d8-a78e-cd2259f837c8/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.990 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/b9/b91f1690-87e8-41d8-a78e-cd2259f837c8/jcr:content not found, which is not expected for an added or modified node
```

### 日誌中出錯：IndexElementFactory的NoClassDefFoundError {#error-in-logs-noclassdeffounderror-for-indexelementfactory}

將AEM 5.6.1 GA升級至最新cq-socialcommunities-pkg-1.4.x或AEM 6.0會在啟動期間導致記錄檔發生錯誤，因為條件會自行解決，重新啟動時未看到錯誤就是明證。

```xml
14.11.2013 20:52:39.453 ERROR [Apache Sling JCR Resource Event Queue Processor for path '/'] com.adobe.cq.social.storage.index.impl.IndexService Error occurred while processing event java.util.ConcurrentModificationException
14.11.2013 20:52:40.716 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory) java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory
14.11.2013 20:52:40.717 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Failed creating the component instance; see log for reason
```
