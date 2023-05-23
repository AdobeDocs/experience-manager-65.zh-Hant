---
title: 社區故障排除
description: 排除社區（包括已知問題）
uuid: 99225430-fa2a-4393-ae5a-18b19541c358
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: cdb2d80a-2fbf-4ee6-b89b-b5d74e6d3bfc
exl-id: ef4f4108-c485-4e2e-a58f-ff64eee9937e
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 1%

---

# 社區故障排除 {#troubleshooting}

本節包含排除社區故障時的常見問題和已知問題。

## 已知問題 {#known-issues}

### Dispatcher重取失敗 {#dispatcher-refetch-fails}

當將Dispatcher 4.1.5與較新版本的Jetty一起使用時，在等待請求超時後，重取可能會導致「無法從遠程伺服器接收響應」。

使用Dispatcher 4.1.6或更高版本將解決此問題。

### 從CQ 5.4升級後無法訪問論壇帖子 {#cannot-access-forum-post-after-upgrading-from-cq}

如果在CQ 5.4上建立論壇並發佈主題，然後將站點升級到AEM5.6.1或更高版本，則嘗試查看現有帖子可能會導致頁面上出現錯誤：

非法模式字元&#39;a&#39;無法將請求發送到 `/content/demoforums/forum-test.html` 和日誌中包含以下內容：

```xml
20.03.2014 22:49:35.805 ERROR [10.177.45.32 [1395380975744] GET /content/demoforums/forum-test.html HTTP/1.1] com.day.cq.wcm.tags.IncludeTag Error while executing script content.jsp
org.apache.sling.api.scripting.ScriptEvaluationException:
at org.apache.sling.scripting.core.impl.DefaultSlingScript.call(DefaultSlingScript.java:388)
at org.apache.sling.scripting.core.impl.DefaultSlingScript.eval(DefaultSlingScript.java:171)
```

問題是com.day.cq.commons.date.RelativeTimeFormat的格式字串在5.4和5.5之間更改，因此不再接受&quot;ago&quot;的&quot;a&quot;。

因此，使用RelativeTimeFormat()API的任何代碼都需要更改：

* 從: `final RelativeTimeFormat fmt = new RelativeTimeFormat("r a", resourceBundle);`
* 至: `final RelativeTimeFormat fmt = new RelativeTimeFormat("r", resourceBundle);`

在作者和發佈上，失敗不同。 在作者時，它會以靜默方式失敗，只是不顯示論壇主題。 在發佈時，它會在頁面上引發錯誤。

查看 [com.day.cq.commons.date.RelativeTimeFormat](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/date/RelativeTimeFormat.html) API（獲取詳細資訊）。

## 共同關注 {#common-concerns}

### 日誌中的警告：已棄用Handlebar {#warning-in-logs-handlebars-deprecated}

在啟動期間（不是第1次 — 但是之後的每次），日誌中可能會顯示以下警告：

* `11.04.2014 08:38:07.223 WARN [FelixStartLevel]com.github.jknack.handlebars.Handlebars Helper 'i18n'` 已替換為 `com.adobe.cq.social.handlebars.I18nHelper@15bac645`

此警告可安全忽略，因為 `jknack.handlebars.Handlebars`，使用 [SCF](scf.md#handlebarsjavascripttemplatinglanguage)，附帶i18n幫助程式。 啟動時，它被一個特定AEM的 [i18n助手](handlebars-helpers.md#i-n)。 此警告由第三方庫生成，以確認對現有幫助程式的覆蓋。

### 日誌中的警告：OakResourceListener進程OsgiEventQueue {#warning-in-logs-oakresourcelistener-processosgieventqueue}

過帳多個社區論壇主題可能會導致大量來自OakResourceListener processOsgiEventQueue的警告和資訊日誌。

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

將AEM5.6.1 GA升級到最新的cq-socialcommunities-pkg-1.4.x或升級到AEM6.0會導致在啟動期間日誌檔案出錯，這種情況將自行解決，重新啟動時未看到錯誤就是明證。

```xml
14.11.2013 20:52:39.453 ERROR [Apache Sling JCR Resource Event Queue Processor for path '/'] com.adobe.cq.social.storage.index.impl.IndexService Error occurred while processing event java.util.ConcurrentModificationException
14.11.2013 20:52:40.716 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory) java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory
14.11.2013 20:52:40.717 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Failed creating the component instance; see log for reason
```
