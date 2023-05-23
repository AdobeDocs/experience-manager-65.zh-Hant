---
title: 如何審核用戶管理操AEM作
seo-title: How to Audit User Management Operations in AEM
description: 瞭解如何在中審核用戶管理操AEM作。
seo-description: Learn how to audit User Management Operations in AEM.
uuid: 9d177afb-172c-4858-a678-254c97cfa472
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: ba6a56e5-b91c-4779-9154-d4300b2827f8
docset: aem65
exl-id: 7a4406c9-2f98-4bf8-b32c-1ec1e7ff36f0
feature: Operations
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 1%

---

# 如何審核用戶管理操AEM作{#how-to-audit-user-management-operations-in-aem}

## 簡介 {#introduction}

已AEM引入了記錄權限更改的功能，以便以後可以審核這些更改。

該增強允許對用戶的權限和組分配執行審計CRUD（建立、讀取、更新、刪除）操作。 更具體地說，它將記錄：

* 正在建立新用戶
* 正在添加到組中的用戶
* 現有用戶或組的權限更改

預設情況下，這些條目將寫入 `error.log` 的子菜單。 為了使監控更輕鬆，建議將它們重定向到單獨的日誌檔案。 有關如何執行此操作的詳細資訊，請參見下段。

## 將輸出重定向到單獨的日誌檔案 {#redirecting-the-output-to-a-separate-log-file}

為了將日誌輸出重定向到單獨的日誌檔案，您需要建立新的日誌 **Apache Sling日誌記錄程式** 配置。 我們用 `useraudit.log` 作為下例中單獨檔案的名稱。

1. 通過瀏覽到 *https://serveraddress:serverport/system/console/configMgr*
1. 搜索 **Apache Sling日誌記錄器配置**。 然後，按條目右側的「+」以建立新的工廠配置。
1. 建立以下配置：

   * **日誌級別：** 資訊
   * **日誌檔案：** logs/useraudit.log
   * **消息模式：** 級別預設
   * **記錄器：** com.adobe.granite.security.user.internal.audit, com.adobe.granite.security.user.internal.servlet.可授權的Servlet

   為了將兩個伐木工同時輸入 **記錄器** 欄位，您需要輸入第一個記錄器的名稱，然後按「+」按鈕並輸入第二個記錄器的名稱來建立另一個欄位。

## 示例輸出 {#example-output}

如果配置正確，輸出應如下所示：

```xml
19.05.2017 15:15:08.933 *INFO* [0:0:0:0:0:0:0:1 [1495196108932] POST /libs/granite/security/post/authorizables.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Create Group 'group1' operation initiated by User 'admin' (administrator)
19.05.2017 15:15:08.934 *INFO* [0:0:0:0:0:0:0:1 [1495196108932] POST /libs/granite/security/post/authorizables.html HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditAuthorizableAction Group 'group1' was created

19.05.2017 15:16:25.698 *INFO* [0:0:0:0:0:0:0:1 [1495196185696] POST /libs/granite/security/post/authorizables.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Create User 'user1' operation initiated by User 'admin' (administrator)
19.05.2017 15:16:25.700 *INFO* [0:0:0:0:0:0:0:1 [1495196185696] POST /libs/granite/security/post/authorizables.html HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditAuthorizableAction User 'user1' was created

19.05.2017 15:16:25.728 *INFO* [0:0:0:0:0:0:0:1 [1495196185726] POST /home/groups/d/dGf7f7vGrZRLs6HS3AK-.rw.userprops.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Edit Membership for Group 'group1' operation initiated by User 'admin' (administrator)
19.05.2017 15:16:25.729 *INFO* [0:0:0:0:0:0:0:1 [1495196185726] POST /home/groups/d/dGf7f7vGrZRLs6HS3AK-.rw.userprops.html HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditGroupAction User 'user1' was added to the group 'group1'

19.05.2017 15:17:29.830 *INFO* [0:0:0:0:0:0:0:1 [1495196249828] POST /home/users/5/5dI6iK4HkZmrfTjcLBoI.rw.userprops.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Password Change for User 'user2' operation initiated by User 'admin' (administrator)
19.05.2017 15:17:29.832 *INFO* [0:0:0:0:0:0:0:1 [1495196249828] POST /home/users/5/5dI6iK4HkZmrfTjcLBoI.rw.userprops.html HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditAuthorizableAction Password for User 'user2' was changed

19.05.2017 15:17:54.906 *INFO* [0:0:0:0:0:0:0:1 [1495196274904] POST /home/users/5/5dI6iK4HkZmrfTjcLBoI.rw.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Delete User 'user2' operation initiated by User 'admin' (administrator)
19.05.2017 15:17:54.906 *INFO* [0:0:0:0:0:0:0:1 [1495196274904] POST /home/users/5/5dI6iK4HkZmrfTjcLBoI.rw.html HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditAuthorizableAction User 'user2' was removed

19.05.2017 15:19:11.050 *INFO* [0:0:0:0:0:0:0:1 [1495196351049] POST /libs/granite/security/post/authorizables.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Create User 'user3' operation initiated by User 'admin' (administrator)
19.05.2017 15:19:11.052 *INFO* [0:0:0:0:0:0:0:1 [1495196351049] POST /libs/granite/security/post/authorizables.html HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditAuthorizableAction User 'user3' was created
19.05.2017 15:19:36.899 *INFO* [0:0:0:0:0:0:0:1 [1495196376898] POST /home/groups/d/dGf7f7vGrZRLs6HS3AK-.rw.userprops.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Edit Membership for Group 'group1' operation initiated by User 'admin' (administrator)

19.05.2017 15:19:36.916 *INFO* [0:0:0:0:0:0:0:1 [1495196376915] POST /home/groups/d/dGf7f7vGrZRLs6HS3AK-.rw.userprops.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Edit Membership for Group 'group1' operation initiated by User 'admin' (administrator)
19.05.2017 15:19:36.917 *INFO* [0:0:0:0:0:0:0:1 [1495196376915] POST /home/groups/d/dGf7f7vGrZRLs6HS3AK-.rw.userprops.html HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditGroupAction User 'user1' was removed from the group 'group1'

19.05.2017 15:21:34.419 *INFO* [0:0:0:0:0:0:0:1 [1495196494417] POST /home/groups/d/dGf7f7vGrZRLs6HS3AK-.rw.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Delete Group 'group1' operation initiated by User 'admin' (administrator)
19.05.2017 15:21:34.419 *INFO* [0:0:0:0:0:0:0:1 [1495196494417] POST /home/groups/d/dGf7f7vGrZRLs6HS3AK-.rw.html HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditAuthorizableAction Group 'group1' was removed

19.05.2017 15:44:10.404 *INFO* [0:0:0:0:0:0:0:1 [1495197850401] POST /home/users/3/35XVpVtLRx4a5J9gKrVG.rw.userprops.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Password Change for User 'john' operation initiated by User 'john' (not administrator)
19.05.2017 15:44:10.405 *INFO* [0:0:0:0:0:0:0:1 [1495197850401] POST /home/users/3/35XVpVtLRx4a5J9gKrVG.rw.userprops.html HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditAuthorizableAction Password for User 'john' was changed
```

## 傳統 UI {#classic-ui}

在經典UI中，與添加和刪除用戶有關的審計日誌中記錄的有關CRUD操作的資訊僅限於受影響用戶的ID以及更改發生的時間。

例如：

```
10.05.2019 18:01:09.123 INFO [0:0:0:0:0:0:0:1 [1557491469096] POST /libs/cq/security/authorizables/POST HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditAuthorizableAction User 'test' was created
```
