---
title: 設定電子郵件通知
seo-title: 設定電子郵件通知
description: 瞭解如何在AEM中設定「電子郵件通知」。
seo-description: 瞭解如何在AEM中設定「電子郵件通知」。
uuid: 6cbdc312-860b-4a69-8bbe-2feb32204a27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6466d7b8-e308-43c5-acdc-dec15f796f64
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 1%

---


# 設定電子郵件通知{#configuring-email-notification}

AEM會傳送電子郵件通知給下列使用者：

* 已訂閱頁面事件，例如修改或複製。 [通知收件箱](/help/sites-classic-ui-authoring/author-env-inbox.md#subscribing-to-notifications)部分介紹如何訂閱此類事件。

* 已訂閱論壇活動。
* 必須在工作流程中執行步驟。 [參與者步驟](/help/sites-developing/workflows-step-ref.md#participant-step)區段說明如何在工作流程中觸發電子郵件通知。

先決條件：

* 使用者必須在其個人檔案中定義有效的電子郵件地址。
* **Day CQ Mail Service**&#x200B;需要正確配置。

當使用者收到通知時，他會收到電子郵件，其語言為其個人檔案中定義。 每種語言都有自己的範本可自訂。 新的電子郵件範本可以針對新語言新增。

>[!NOTE]
>
>使用AEM時，有幾種方法可管理此類服務的組態設定；如需詳細資訊和建議的實務，請參閱[設定OSGi](/help/sites-deploying/configuring-osgi.md)。

## 配置郵件服務{#configuring-the-mail-service}

AEM若要能夠傳送電子郵件，**Day CQ Mail Service**&#x200B;必須正確設定。 您可以在Web控制台中查看配置。 使用AEM時，有幾種方法可管理此類服務的組態設定；如需詳細資訊和建議的實務，請參閱[設定OSGi](/help/sites-deploying/configuring-osgi.md)。

適用下列限制：

* **SMTP伺服器埠**&#x200B;必須為25或更高。

* **SMTP伺服器主機名**&#x200B;不能為空。
* **&quot;From&quot;地址**&#x200B;不能為空。

要幫助您調試&#x200B;**Day CQ Mail Service**&#x200B;的問題，您可以查看服務的日誌：

`com.day.cq.mailer.DefaultMailService`

配置在Web控制台中的外觀如下：

![chlimage_1-276](assets/chlimage_1-276.png)

## 配置電子郵件通知渠道{#configuring-the-email-notification-channel}

當您訂閱頁面或論壇事件通知時，預設的寄件者電子郵件地址會設為`no-reply@acme.com`。 您可以在Web控制台中配置&#x200B;**通知電子郵件通道**&#x200B;服務來更改此值。

要配置寄件者電子郵件地址，請向儲存庫添加`sling:OsgiConfig`節點。 使用以下過程直接使用CRXDE Lite添加節點：

1. 在CRXDE Lite中，在應用程式資料夾下方新增名為`config`的資料夾。
1. 在config資料夾中，添加名為：

   `com.day.cq.wcm.notification.email.impl.EmailChannel` 類型  `sling:OsgiConfig`

1. 將`String`屬性添加到名為`email.from`的節點。 請為值指定您要使用的電子郵件地址。

1. 按一下&#x200B;**保存全部**。

請按下列步驟在內容包源資料夾中定義節點：

1. 在`jcr_root/apps/*app_name*/config folder`中，建立名為`com.day.cq.wcm.notification.email.impl.EmailChannel.xml`的檔案

1. 添加以下XML以表示節點：

   `<?xml version="1.0" encoding="UTF-8"?> <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig" email.from="name@server.com"/>`
1. 將`email.from`屬性(`name@server.com`)的值取代為您的電子郵件位址。

1. 儲存檔案。

## 配置工作流電子郵件通知服務{#configuring-the-workflow-email-notification-service}

當您收到工作流程電子郵件通知時，寄件者電子郵件地址和主機URL首碼都會設為預設值。 您可以在Web控制台中配置&#x200B;**Day CQ Workflow Email Notification Service**&#x200B;來更改這些值。 如果您這樣做，建議將更改保存在儲存庫中。

預設配置在Web控制台中的外觀如下：

![chlimage_1-277](assets/chlimage_1-277.png)

### 頁面通知的電子郵件範本{#email-templates-for-page-notification}

頁面通知的電子郵件範本位於以下：

`/etc/notification/email/default/com.day.cq.wcm.core.page`

預設英文模板(`en.txt`)定義如下：

```xml
subject=[CQ Page Event Notification]: Page Event

header=-------------------------------------------------------------------------------------\n \
Time: ${time}\n \
User: ${userFullName} (${userId})\n \
-------------------------------------------------------------------------------------\n\n

message=The following pages were affected by the event: \n \
 \n \
${modifications} \n \
 \n\n
footer=\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### 自訂頁面通知的電子郵件範本{#customizing-email-templates-for-page-notification}

若要自訂頁面通知的英文電子郵件範本：

1. 在CRXDE中，開啟檔案：

   `/etc/notification/email/default/com.day.cq.wcm.core.page/en.txt`

1. 根據您的需求修改檔案。
1. 儲存變更。

範本必須具備下列格式：

```
 subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

其中，&lt;text_x>可混合使用靜態文字和動態字串變數。 以下變數可用於電子郵件範本中的頁面通知：

* `${time}`，事件日期和時間。

* `${userFullName}`，則觸發事件之使用者的完整名稱。

* `${userId}`，則觸發事件之使用者的ID。
* `${modifications}`，以下列格式說明頁面事件和頁面路徑的類型：

   &lt;page event=&quot;&quot; type=&quot;&quot;> =>  &lt;page path=&quot;&quot;>

   例如：

   PageModified => /content/geometrixx/tw/products

### 論壇通知的電子郵件範本{#email-templates-for-forum-notification}

論壇通知的電子郵件範本位於：

`/etc/notification/email/default/com.day.cq.collab.forum`

預設英文模板(`en.txt`)定義如下：

```xml
subject=[CQ Forum Notification]

header=-------------------------------------------------------------------------------------\n \
Time: Time: ${time}\n \
Forum Page Path: ${forum.path}\n \
-------------------------------------------------------------------------------------\n\n

message=Page: ${host.prefix}${forum.path}.html\n

footer=\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### 自定義論壇通知的電子郵件模板{#customizing-email-templates-for-forum-notification}

若要自訂論壇通知的英文電子郵件範本：

1. 在CRXDE中，開啟檔案：

   `/etc/notification/email/default/com.day.cq.collab.forum/en.txt`

1. 根據您的需求修改檔案。
1. 儲存變更。

範本必須具備下列格式：

```
 subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

其中`<text_x>`可混合使用靜態文字和動態字串變數。

在論壇通知的電子郵件範本中可使用下列變數：

* `${time}`，事件日期和時間。

* `${forum.path}`，則為論壇頁面的路徑。

### 工作流程通知的電子郵件範本{#email-templates-for-workflow-notification}

工作流程通知的電子郵件範本（英文）位於：

`/etc/workflow/notification/email/default/en.txt`

定義如下：

```xml
subject=Workflow notification: ${event.EventType}

header=-------------------------------------------------------------------------------------\n \
Time: ${event.TimeStamp}\n \
Step: ${item.node.title}\n \
User: ${participant.name} (${participant.id})\n \
Workflow: ${model.title}\n \
-------------------------------------------------------------------------------------\n\n

message=Content: ${host.prefix}${payload.path.open}\n

footer=\n \
-------------------------------------------------------------------------------------\n \
View the overview in your ${host.prefix}/aem/inbox\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### 自定義工作流通知的電子郵件模板{#customizing-email-templates-for-workflow-notification}

要為工作流事件通知自定義英文電子郵件模板：

1. 在CRXDE中，開啟檔案：

   `/etc/workflow/notification/email/default/en.txt`

1. 根據您的需求修改檔案。
1. 儲存變更。

範本必須具備下列格式：

```
subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

>[!NOTE]
>
>其中`<text_x>`可混合使用靜態文字和動態字串變數。 `<text_x>`項目的每一行都需要以反斜線(`\`)結尾，但最後一個例項除外，因為沒有反斜線表示`<text_x>`字串變數的結尾。
>
>有關模板格式的詳細資訊，請參閱Properties.load()](https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html#load-java.io.InputStream-)方法的[javadoc。

方法`${payload.path.open}`會顯示工作項目的有效負荷路徑。 例如，若是Sites中的頁面，則`payload.path.open`會類似於`/bin/wcmcommand?cmd=open&path=…`。;這沒有伺服器名，因此模板會以`${host.prefix}`為前置詞。

下列變數可用於電子郵件範本中：

* `${event.EventType}`，事件類型
* `${event.TimeStamp}`、事件的日期和時間
* `${event.User}`，觸發事件的使用者
* `${initiator.home}`，啟動器節點路徑

* `${initiator.name}`，啟動器名稱

* `${initiator.email}`，啟動器的電子郵件地址
* `${item.id}`，工作項目的ID
* `${item.node.id}`，與此工作項目關聯的工作流模型中節點的ID
* `${item.node.title}`，工作項目標題
* `${participant.email}`、參與者的電子郵件地址
* `${participant.name}`，參與者名稱
* `${participant.familyName}`，參與者的姓氏
* `${participant.id}`，參與者的id
* `${participant.language}`，參與者語言
* `${instance.id}`, the workflow id
* `${instance.state}`，則工作流狀態
* `${model.title}`，工作流模型的標題
* `${model.id}`，工作流模型的ID

* `${model.version}`，工作流模型的版本
* `${payload.data}`、裝載

* `${payload.type}`、裝載類型
* `${payload.path}`，裝載路徑
* `${host.prefix}`，主機首碼，例如：http://localhost:4502

### 為新語言添加電子郵件模板{#adding-an-email-template-for-a-new-language}

要添加新語言的模板，請執行以下操作：

1. 在CRXDE中，添加以下檔案`<language-code>.txt`:

   * `/etc/notification/email/default/com.day.cq.wcm.core.page` :頁面通知
   * `/etc/notification/email/default/com.day.cq.collab.forum` :論壇通知
   * `/etc/workflow/notification/email/default` :工作流通知

1. 根據語言調整檔案。
1. 儲存變更。

>[!NOTE]
>
>`<language-code>`用作電子郵件範本的檔案名稱，必須是由AEM識別的雙字母小寫語言代碼。 對於語言代碼，AEM需仰賴ISO-639-1。

## 設定AEM Assets電子郵件通知{#assetsconfig}

當「AEM資產」中的「系列」是共用或取消共用時，使用者可以從AEM接收電子郵件通知。 若要設定電子郵件通知，請依照下列步驟進行。

1. 按照[配置郵件服務](/help/sites-administering/notification.md#configuring-the-mail-service)中所述配置電子郵件服務。
1. 以管理員身分登入AEM。 按一下&#x200B;**工具** > **操作** > **Web控制台**&#x200B;以開啟Web控制台配置。
1. 編輯&#x200B;**Day CQ DAM Resource Collection Servlet**。 選擇&#x200B;**傳送電子郵件**。 按一下&#x200B;**「儲存」**。

