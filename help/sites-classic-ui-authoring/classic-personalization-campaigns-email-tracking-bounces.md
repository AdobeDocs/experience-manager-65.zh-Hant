---
title: 跟蹤已跳轉的電子郵件
seo-title: Tracking Bounced Emails
description: 當您向許多用戶發送新聞稿時，清單中通常包含一些無效的電子郵件地址。 向這些地址發送新聞稿後會回復。 可AEM以管理這些回報，並可以在超出配置的反彈計數器後停止向這些地址發送新聞稿。
seo-description: When you send a newsletter to many users, there are usually some invalid emails addresses in the list. Sending newsletters to those addresses bounce back. AEM is capable of managing those bounces and can stop sending newsletters to those addresses after the configured bounce counter is exceeded.
uuid: 749959f2-e6f8-465f-9675-132464c65f11
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: fde9027b-9057-48c3-ae34-3f3258c5b371
exl-id: 6cda0a68-0df9-44e7-ae4f-9951411af6dd
source-git-commit: e05f6cd7cf17f4420176cf76f28cb469bcee4a0a
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 0%

---

# 跟蹤已跳轉的電子郵件{#tracking-bounced-emails}

>[!NOTE]
>
>Adobe不打算進一步加強對SMTP服務發送的已開啟/已跳轉電子郵件AEM的跟蹤。
>
>建議是 [使用Adobe CampaignAEM及其整合](/help/sites-administering/campaign.md)。

當您向許多用戶發送新聞稿時，清單中通常包含一些無效的電子郵件地址。 向這些地址發送新聞稿後會回復。 可AEM以管理這些回報，並可以在超出配置的反彈計數器後停止向這些地址發送新聞稿。 預設情況下，彈跳率設定為3，但可配置。

要設定AEM跟蹤已跳轉電子郵件，請設定AEM以輪詢接收已跳轉電子郵件的現有郵箱。 通常，此位置是您指定的新聞稿發送位置的「發件人」電子郵件地址。 輪AEM詢此收件箱並導入輪詢配置中指定的路徑下的所有電子郵件。 然後觸發工作流以搜索用戶內被跳轉的電子郵件地址並相應地更新用戶的bounceCounter屬性值。 超出配置的最大退貨後，用戶將從新聞簡報清單中刪除。

## 配置源導入程式 {#configuring-the-feed-importer}

源導入程式允許您從外部源反複將內容導入儲存庫。 使用此源導入程式配置AEM，檢查發件人郵箱中是否有被拒發的電子郵件。

要配置源導入程式以跟蹤已跳轉的電子郵件，請執行以下操作：

1. 在 **工具**，選擇「Feed Importer（源導入程式）」。

1. 按一下 **添加** 建立配置。

   ![chlimage_1](assets/chlimage_1a.png)

1. 通過選擇類型和向輪詢URL添加資訊來添加配置，以便可以配置主機和埠。 此外，將某些特定於郵件和協定的參數添加到URL查詢。 將配置設定為每天至少輪詢一次。

   所有配置都需要輪詢URL中有關以下內容的資訊：

   `username`:用於連接的用戶名

   `password`:用於連接的密碼

   此外，根據協定，您可以配置某些設定。

   **POP3配置屬性：**

   `pop3.leave.on.server`:定義是否在伺服器上保留郵件。 設定為true可在伺服器上留下消息，否則為false。 預設為true。

   **POP3示例：**

   | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret | 使用pop3 over SSL以用戶/密鑰連接到埠995上的GMail，預設情況下將消息保留在伺服器上 |
   |---|---|
   | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret&amp;pop3.leave.on.server=false | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret&amp;pop3.leave.on.server=false |

   **IMAP配置屬性：**

   用於設定要搜索的標誌。

   `imap.flag.SEEN`：為新消息/不可見消息設定false，為已讀消息設定true

   請參閱 [https://javaee.github.io/javamail/docs/api/index.html?javax/mail/Flags.Flag.html](https://javaee.github.io/javamail/docs/api/index.html?javax/mail/Flags.Flag.html) 標誌的完整清單。

   **IMAP示例：**

   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret | 使用IMAP over SSL以用戶/密鑰連接到埠993上的GMail。 預設情況下，僅獲取新消息。 |
   |---|---|
   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret&amp;imap.flag.SEEN=true | 使用IMAP over SSL連接到GMail 993，並使用用戶/密鑰，只獲得已見的消息。 |
   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret&amp;imap.flag.SEEN=true&amp;imap.flag.SEEN=false | 使用IMAP over SSL連接到GMail 993，並使用用戶/密鑰，獲取已讀取或新郵件。 |

1. 儲存設定。

## 配置新聞簡報服務元件 {#configuring-the-newsletter-service-component}

配置源導入程式後，配置「發件人」地址和彈出計數器。

要配置新聞簡報服務，請執行以下操作：

1. 在OSGi控制台中， `<host>:<port>/system/console/configMgr`，導航 **MCM新聞稿**。

1. 配置服務並在完成後保存更改。

   ![chlimage_1-1](assets/chlimage_1-1a.png)

   可以設定以下配置來調整行為：

   | 反彈計數器最大值(max.bounce.count) | 定義回報數，直到用戶在發送新聞簡報時被省略。 將此值設定為0將完全禁用彈出檢查。 |
   |---|---|
   | 活動無快取(sent.activity.nocache) | 定義要用於新聞簡報發送活動的快取設定 |

   新聞稿MCM服務保存後，將執行以下操作：

   * 在成功發送新聞稿時，向用戶寫入隱藏的流。
   * 如果檢測到反彈並且用戶反彈計數器更改，則寫入活動。
