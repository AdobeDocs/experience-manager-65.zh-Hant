---
title: 追蹤跳出的電子郵件
seo-title: Tracking Bounced Emails
description: 當您傳送電子報給許多使用者時，清單中通常會有一些無效的電子郵件地址。 將電子報傳送到這些地址退回。 AEM能夠管理這些退信，而且在超出設定的退信計數器後，可以停止傳送電子報至這些地址。
seo-description: When you send a newsletter to many users, there are usually some invalid emails addresses in the list. Sending newsletters to those addresses bounce back. AEM is capable of managing those bounces and can stop sending newsletters to those addresses after the configured bounce counter is exceeded.
uuid: 749959f2-e6f8-465f-9675-132464c65f11
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: fde9027b-9057-48c3-ae34-3f3258c5b371
exl-id: 6cda0a68-0df9-44e7-ae4f-9951411af6dd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 0%

---

# 追蹤跳出的電子郵件{#tracking-bounced-emails}

>[!NOTE]
>
>Adobe沒有計畫進一步增強對AEM SMTP服務所傳送已開啟/退信電子郵件的追蹤。
>
>建議是 [運用Adobe Campaign及其AEM整合](/help/sites-administering/campaign.md).

當您傳送電子報給許多使用者時，清單中通常會有一些無效的電子郵件地址。 將電子報傳送到這些地址退回。 AEM能夠管理這些退信，而且在超出設定的退信計數器後，可以停止傳送電子報至這些地址。 預設情況下，跳出率會設為3，但可設定。

若要設定AEM以追蹤退信電子郵件，您必須設定AEM以輪詢收到退信電子郵件的現有信箱（通常是您指定傳送電子報的「寄件者」電子郵件地址）。 AEM會輪詢此收件匣，並匯入所有位於輪詢設定中指定之路徑下的電子郵件。 接著會觸發工作流程，以搜尋使用者內退回的電子郵件地址，並據此更新使用者的bounceCounter屬性值。 超過設定的最大跳出數後，會從電子報清單中移除該使用者。

## 設定摘要匯入工具 {#configuring-the-feed-importer}

摘要匯入工具可讓您重複從外部來源將內容匯入存放庫。 使用此摘要匯入工具的設定，AEM會檢查寄件者的信箱中是否有退信的電子郵件。

若要設定摘要匯入工具以追蹤退回的電子郵件：

1. 在 **工具**，選取摘要匯入工具。

1. 按一下 **新增** 來建立新配置。

   ![chlimage_1](assets/chlimage_1a.png)

1. 選取類型，並將資訊新增至輪詢URL以設定主機和連接埠，以新增設定。 此外，您需要將一些郵件和通訊協定專用參數新增至URL查詢。 設定每天至少輪詢一次。

   所有設定都需要輪詢URL中下列項目的相關資訊：

   `username`:用於連接的用戶名

   `password`:用於連接的密碼

   此外，您可以根據通訊協定來設定特定設定。

   **POP3配置屬性：**

   `pop3.leave.on.server`:定義是否在伺服器上保留消息。 設為true可將郵件保留在伺服器上，否則為false。 預設為true。

   **POP3示例：**

   | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret | 使用pop3 over SSL連接埠995上的GMail，使用用戶/密碼，預設情況下將消息保留在伺服器上 |
   |---|---|
   | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret&amp;pop3.leave.on.server=false | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret&amp;pop3.leave.on.server=false |

   **IMAP配置屬性：**

   可讓您設定要搜尋的標幟。

   `imap.flag.SEEN`：為新消息/未顯示的消息設定false，為已讀取的消息設定true

   請參閱 [https://java.sun.com/products/javamail/javadocs/javax/mail/Flags.Flag.html](https://java.sun.com/products/javamail/javadocs/javax/mail/Flags.Flag.html) 標幟的完整清單。

   **IMAP示例：**

   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret | 使用IMAP over SSL連接埠993上的GMail，使用用戶/密碼。 預設情況下僅獲取新消息。 |
   |---|---|
   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret&amp;imap.flag.SEEN=true | 使用IMAP over SSL連接到具有用戶/密碼的GMail 993，但只獲得已被看到的消息。 |
   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret&amp;imap.flag.SEEN=true&amp;imap.flag.SEEN=false | 使用IMAP over SSL連接到GMail 993，使用用戶/密碼，已讀取或新消息。 |

1. 儲存設定。

## 設定新聞稿服務元件 {#configuring-the-newsletter-service-component}

設定摘要匯入工具後，您需要設定寄件者地址和退信計數器。

若要設定電子報服務：

1. 在OSGi主控台中， `<host>:<port>/system/console/configMgr` 並導覽至 **MCM電子報**.

1. 設定服務並在完成時儲存變更。

   ![chlimage_1-1](assets/chlimage_1-1a.png)

   可設定下列設定來調整行為：

   | 跳出計數器上限(max.bounce.count) | 定義退信數，直到在傳送電子報時忽略使用者為止。 將此值設定為0將完全禁用退信檢查。 |
   |---|---|
   | 活動無快取(sent.activity.nocache) | 定義用於電子報傳送活動的快取設定 |

   電子報MCM服務儲存後會執行下列作業：

   * 成功傳送電子報時，將活動寫入隱藏的資料流給使用者。
   * 在偵測到跳出且使用者跳出計數器變更時寫入活動。
