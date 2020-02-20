---
title: Messaging Essentials
seo-title: Messaging Essentials
description: 訊息元件概觀
seo-description: 訊息元件概觀
uuid: e0dad45e-d84d-4b28-b357-aded1c5d2605
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 98f70093-e786-4555-8aaa-d0df4c977dc0
docset: aem65
translation-type: tm+mt
source-git-commit: a3ccb1ffe2b2e24c453afac8cf3efc098f393030

---


# Messaging Essentials{#messaging-essentials}

本頁記錄了使用消息傳遞元件在網站上包含消息傳遞功能的詳細資訊。

## 用戶端基本功能 {#essentials-for-client-side}

**撰寫訊息**

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td><p>social/messaging/components/hbs/composemessage</p> </td>
  </tr>
  <tr>
   <td> <a href="/help/communities/client-customize.md#clientlibs-for-scf" target="_blank"><strong>clientlibs</strong></a></td>
   <td><p>cq.social.hbs.messaging</p> </td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td>/libs/social/messaging/components/hbs/composemessage/composemessage.hbs</td>
  </tr>
  <tr>
   <td><strong>css</strong></td>
   <td>/libs/social/messaging/components/hbs/composemessage/clientlibs/composemessage.css</td>
  </tr>
  <tr>
   <td><strong>屬性</strong></td>
   <td>請參 <a href="/help/communities/configure-messaging.md" target="_blank">閱配置消息</a></td>
  </tr>
  <tr>
   <td><strong>管理員設定</strong></td>
   <td><a href="/help/communities/messaging.md">配置消息</a></td>
  </tr>
 </tbody>
</table>

**消息清單**

（用於收件箱、已發送和垃圾筒）

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td><p>social/messaging/components/hbs/messagebox</p> </td>
  </tr>
  <tr>
   <td> <a href="/help/communities/client-customize.md#clientlibs-for-scf" target="_blank"><strong>clientlibs</strong></a></td>
   <td><p>cq.social.hbs.messaging</p> </td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td>/libs/social/messaging/components/hbs/messagebox/messagebox.hbs</td>
  </tr>
  <tr>
   <td><strong>css</strong></td>
   <td>/libs/social/messaging/components/hbs/messagebox/clientlibs/messagebox.css</td>
  </tr>
  <tr>
   <td><strong>屬性</strong></td>
   <td>請參 <a href="/help/communities/configure-messaging.md" target="_blank">閱配置消息</a></td>
  </tr>
  <tr>
   <td><strong>管理員設定</strong></td>
   <td><a href="/help/communities/messaging.md" target="_blank">配置消息</a></td>
  </tr>
 </tbody>
</table>

另請參閱 [用戶端自訂](/help/communities/client-customize.md)

## 伺服器端的基本功能 {#essentials-for-server-side}

* [配置消息](/help/communities/configure-messaging.md)
* [SCF元件的消息傳遞客戶端](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/client/api/package-summary.html) API
* [服務的訊息](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/api/package-summary.html) API
* [消息傳送端點](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/client/endpoints/package-summary.html)
* [伺服器端自訂](/help/communities/server-customize.md)

>[!CAUTION]
>
>String參數必須*not *包含下列MessageBuilder方法的尾隨斜線&quot;/&quot;:
>
>* `setInboxPath`()
>* `setSentItemsPath`()
>
>例如：
>
>```
>valid: mb.setInboxPath( "/mail/inbox" );
> not valid: mb.setInboxPath( "/mail/inbox/" );
>```

### 社群網站 {#community-site}

使用嚮導建立的社區站點結構在選定時包括消息傳遞功能。 請參 `User Management` 閱社群網 [站主控台的設定](/help/communities/sites-console.md#user-management)。

### 范常式式碼：收到的消息通知 {#sample-code-message-received-notification}

「社交訊息」功能會拋出操作的事件， `send`例如 `marking read`, `marking delete`。 可以捕獲這些事件並對事件中包含的資料採取操作。

下列範例是事件處理常式，其會監聽事件 `message sent` 並使用傳送電子郵件給所有訊息收件者 `Day CQ Mail Service`。

若要試用伺服器端範例指令碼，您需要開發環境和建立OSGi套件的能力：

1. 以管理員身分登入， ` [CRXDE|Lite](https://localhost:4502/crx/de).`
1. 使用任 `bundle node`意 `/apps/engage/install` 名稱建立，例如：

   * 符號名稱：com.engage.media.social.messaging.MessagingNotification
   * 名稱：快速入門教學課程訊息通知
   * 說明：在使用者收到訊息時傳送電子郵件通知的範例服務
   * 套件：com.engage.media.social.messaging.notification

1. 導覽至/apps/engage/install/com.engage.media.social.messaging.MessagingNotification/src/main/java/com/engage/media/social/messaging/notification，然後：

   1. 刪除自動建立的Activator.java類。
   1. 建立類MessageEventHandler.java。
   1. 將下面的代碼複製並貼上到MessageEventHandler.java中。

1. 按一下「 **全部儲存」。**
1. 導覽至/apps/engage/install/com.engage.media.social.messaging.MessagingNotification/com.engage.media.social.messaging.MessagingNotification.bnd，並新增MessageEventHandler.java程式碼中寫入的所有匯入陳述式。
1. 建立套件。
1. 確 `Day CQ Mail Service`保已配置OSGi服務。
1. 以示範使用者身分登入，並傳送電子郵件給其他使用者。
1. 收件者會收到有關新訊息的電子郵件。

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

