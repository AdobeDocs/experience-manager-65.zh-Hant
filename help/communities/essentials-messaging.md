---
title: 消息傳送軟體包
seo-title: Messaging Essentials
description: 消息元件概述
seo-description: Messaging component overview
uuid: e0dad45e-d84d-4b28-b357-aded1c5d2605
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 98f70093-e786-4555-8aaa-d0df4c977dc0
docset: aem65
exl-id: b941b5e0-f768-4393-9a9d-ded2cd7d10c4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 2%

---

# 消息傳送軟體包 {#messaging-essentials}

此頁記錄了使用消息元件在網站上包含消息功能的詳細資訊。

## 客戶端基本知識 {#essentials-for-client-side}

**撰寫郵件**

<table>
 <tbody>
  <tr>
   <td> <strong>資源類型</strong></td>
   <td><p>社交/消息/元件/hbs/組合消息</p> </td>
  </tr>
  <tr>
   <td> <a href="/help/communities/client-customize.md#clientlibs-for-scf" target="_blank"><strong>客戶端</strong></a></td>
   <td><p>cq.social.hbs.messaging</p> </td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td>/libs/social/messaging/components/hbs/composemessage/composemessage.hbs</td>
  </tr>
  <tr>
   <td><strong>cs</strong></td>
   <td>/libs/social/messaging/components/hbs/composemessage/clientlibs/composemessage.css</td>
  </tr>
  <tr>
   <td><strong>屬性</strong></td>
   <td>請參閱 <a href="/help/communities/configure-messaging.md" target="_blank">配置消息</a></td>
  </tr>
  <tr>
   <td><strong>管理員配置</strong></td>
   <td><a href="/help/communities/messaging.md">配置消息</a></td>
  </tr>
 </tbody>
</table>

**消息清單**

（用於收件箱、已發送和資源回收筒）

<table>
 <tbody>
  <tr>
   <td> <strong>資源類型</strong></td>
   <td><p>社交/消息/元件/hbs/消息框</p> </td>
  </tr>
  <tr>
   <td> <a href="/help/communities/client-customize.md#clientlibs-for-scf" target="_blank"><strong>客戶端</strong></a></td>
   <td><p>cq.social.hbs.messaging</p> </td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td>/libs/social/messaging/components/hbs/messagebox/messagebox/messagebox/hbs</td>
  </tr>
  <tr>
   <td><strong>cs</strong></td>
   <td>/libs/social/messaging/components/hbs/messagebox/clientlibs/messagebox/css</td>
  </tr>
  <tr>
   <td><strong>屬性</strong></td>
   <td>請參閱 <a href="/help/communities/configure-messaging.md" target="_blank">配置消息</a></td>
  </tr>
  <tr>
   <td><strong>管理員配置</strong></td>
   <td><a href="/help/communities/messaging.md" target="_blank">配置消息</a></td>
  </tr>
 </tbody>
</table>

另請參閱 [客戶端自定義](/help/communities/client-customize.md)

## 伺服器端軟體包 {#essentials-for-server-side}

* [配置消息](/help/communities/configure-messaging.md)
* [消息傳送客戶端API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/client/api/package-summary.html) 對於SCF元件
* [消息傳遞API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/api/package-summary.html) 服務
* [消息終結點](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/client/endpoints/package-summary.html)
* [伺服器端自定義](/help/communities/server-customize.md)

>[!CAUTION]
>
>String參數必須 *不* 包含以下MessageBuilder方法的尾斜槓「/」：
>
>* `setInboxPath`()
>* `setSentItemsPath`()
>
>例如：
>
>
```
>valid: mb.setInboxPath( "/mail/inbox" );
> not valid: mb.setInboxPath( "/mail/inbox/" );
>```

### 社群網站 {#community-site}

使用嚮導建立的社區站點結構在選中時包括消息傳遞功能。 請參閱 `User Management` 設定 [社區站點控制台](/help/communities/sites-console.md#user-management)。

### 示例代碼：收到的消息通知 {#sample-code-message-received-notification}

「社交消息」功能可引發操作事件，例如 `send`。 `marking read`。 `marking delete`。 可以捕獲這些事件並對事件中包含的資料執行的操作。

以下示例是偵聽的 `message sent` 事件，並使用 `Day CQ Mail Service`。

要嘗試伺服器端示例指令碼，您需要開發環境和構建OSGi捆綁包的能力：

1. 以管理員身份登錄到 ` [CRXDE|Lite](https://localhost:4502/crx/de)`。
1. 建立 `bundle node`在 `/apps/engage/install` 具有任意名稱，如：

   * 符號名稱: `com.engage.media.social.messaging.MessagingNotification`
   * 名稱：入門教程消息通知
   * 描述：用於在用戶收到消息時向其發送電子郵件通知的示例服務
   * 封裝: `com.engage.media.social.messaging.notification`

1. 導航到 `/apps/engage/install/com.engage.media.social.messaging.MessagingNotification/src/main/java/com/engage/media/social/messaging/notification`，然後：

   1. 刪除 `Activator.java` 類自動建立。
   1. 建立類 `MessageEventHandler.java`。
   1. 將下面的代碼複製並貼上到 `MessageEventHandler.java`。

1. 按一下 **全部保存**。
1. 導航到 `/apps/engage/install/com.engage.media.social.messaging.MessagingNotification/com.engage.media.social.messaging.MessagingNotification.bnd`，並添加在 `MessageEventHandler.java` 代碼。
1. 生成捆綁包。
1. 確保 `Day CQ Mail Service`已配置OSGi服務。
1. 以演示用戶身份登錄，向另一用戶發送電子郵件。
1. 收件人接收有關新消息的電子郵件。

#### MessageEventHandler.java {#messageeventhandler-java}

```java
package com.engage.media.social.messaging.notification;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Properties;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.apache.felix.scr.annotations.Reference;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.api.resource.ResourceResolverFactory;
import org.apache.sling.api.resource.Resource;
import org.apache.commons.mail.Email;
import org.apache.commons.mail.EmailException;
import org.apache.commons.mail.SimpleEmail;
import org.apache.commons.mail.HtmlEmail;
import java.util.List;
import org.osgi.service.event.Event;
import org.osgi.service.event.EventHandler;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import com.adobe.cq.social.messaging.api.Message;
import com.adobe.cq.social.messaging.api.MessagingEvent;
import com.day.cq.mailer.MessageGatewayService;
import com.day.cq.mailer.MessageGateway;

@Component(immediate=true)
@Service(EventHandler.class)
@Properties({
        @Property(name = "event.topics", value = "com/adobe/cq/social/message")
})
public class MessagingEventHandler implements EventHandler {
    private Logger logger = LoggerFactory.getLogger(MessagingEventHandler.class);

    @Reference
    ResourceResolverFactory resourceResolverFactory;

    @Reference
    private MessageGatewayService messageGatewayService;

    ResourceResolver resourceResolver=null;
    MessageGateway messageGateway=null;

    public void sendMail(String from, String to,String subject, String content){
        Email email = new SimpleEmail();
        messageGateway = messageGatewayService.getGateway(SimpleEmail.class);
        try {
         email.addTo(to);
            email.addReplyTo(from);
            email.setFrom(from);
            email.setMsg(content);
            email.setSubject(subject);
         messageGateway.send(email);
        } catch(EmailException ex) {
            logger.error("MessageNotificaiton : Error sending email : "+ex.getMessage());
        }
        logger.info("**** MessageNotification **** Mail sent to " + to);
    }

    public void handleEvent(Event event) {
        //Get Message Path and originator User's ID from event
        String messagePath = (String) event.getProperty("path");
        String senderId = (String) event.getProperty("userId");
        MessagingEvent.MessagingActions action = (MessagingEvent.MessagingActions) event.getProperty("action");
        try{
            if(MessagingEvent.MessagingActions.MessageSent.equals(action)){
                resourceResolver = resourceResolverFactory.getAdministrativeResourceResolver(null);

                //Read message
                Resource resource = resourceResolver.getResource(messagePath);
                Message msg = resource.adaptTo(Message.class);

                //Get list of recipient Ids from message
                //For Getting Started Tutorial, Id is same as email. If that is not the case in your site,
                //an additional step is needed to retrieve the email for the Id
                List<String> reclist = msg.getRecipientIdList();
                for(int i=0;i<reclist.size();i++){
                    //Send Email using Mailing Service
                    sendMail("admin@cqadmin.qqq",reclist.get(i),"New message on Getting Started Tutorial", "Hi\nYou have received a new message from  " +  senderId + ". To read it, sign in to Getting Started Tutorial.\n\n-Engage Admin");
                }
            }
        } catch(Exception ex){
            logger.error("Error getting message info : " + ex.getMessage());
        } finally {
            resourceResolver.close();
        }

    }
}
```
