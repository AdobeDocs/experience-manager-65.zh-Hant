---
title: 追蹤已跳回的電子郵件
seo-title: 追蹤已跳回的電子郵件
description: 當您傳送電子報給許多使用者時，清單中通常會有一些無效的電子郵件地址。 傳送電子報給這些地址，會反彈回來。 AEM可管理這些彈回數，並可在超過設定的彈回數後，停止傳送電子報至這些位址。
seo-description: 當您傳送電子報給許多使用者時，清單中通常會有一些無效的電子郵件地址。 傳送電子報給這些地址，會反彈回來。 AEM可管理這些彈回數，並可在超過設定的彈回數後，停止傳送電子報至這些位址。
uuid: 749959f2-e6f8-465f-9675-132464c65f11
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: fde9027b-9057-48c3-ae34-3f3258c5b371
translation-type: tm+mt
source-git-commit: 016c705230dffec052c200b058a36cdbe0520fc4

---


# 追蹤已跳回的電子郵件{#tracking-bounced-emails}

>[!NOTE]
>
>Adobe不打算進一步加強追蹤AEM SMTP服務傳送的已開啟／已拒絕電子郵件。
>
>建議您運用 [Adobe Campaign及其AEM整合](/help/sites-administering/campaign.md)。

當您傳送電子報給許多使用者時，清單中通常會有一些無效的電子郵件地址。 傳送電子報給這些地址，會反彈回來。 AEM可管理這些彈回數，並可在超過設定的彈回數後，停止傳送電子報至這些位址。 依預設，反彈率設定為3，但是可設定。

若要將AEM設為追蹤已退回的電子郵件，您必須設定AEM來投票問答收到已退回電子郵件的現有郵箱（通常是您指定傳送電子報的「寄件者」電子郵件地址）。 AEM會輪詢此收件匣，並匯入所有位於輪詢設定中指定路徑下方的電子郵件。 然後觸發工作流程，以搜尋使用者內遭拒的電子郵件地址，並據以更新使用者的bounceCounter屬性值。 超過設定的最大彈回數後，會從電子報清單中移除使用者。

## 設定動態消息匯入工具 {#configuring-the-feed-importer}

動態消息匯入工具可讓您從外部來源重複匯入內容至您的儲存庫。 使用此動態消息匯入工具的設定，AEM會檢查傳送者的郵箱是否有遭拒的電子郵件。

若要設定動態消息匯入工具以追蹤已跳回的電子郵件：

1. 在「工 **具**」中，選取「動態消息匯入工具」。

1. 按一 **下「新增** 」以建立新設定。

   ![chlimage_1](assets/chlimage_1a.png)

1. 選擇類型並將資訊添加到輪詢URL以配置主機和埠，以添加新配置。 此外，您還需要新增一些郵件和通訊協定特定參數至URL查詢。 將配置設定為每天至少輪詢一次。

   所有配置都需要輪詢URL中的以下資訊：

   `username`:用於連接的用戶名

   `password`:用於連接的口令

   此外，您還可以根據通訊協定來設定特定設定。

   **POP3配置屬性：**

   `pop3.leave.on.server`:定義是否在伺服器上保留消息。 設定為true可將消息留在伺服器上，否則為false。 預設為true。

   **POP3示例：**

   | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret | 使用pop3 over SSL連線至連接埠995的GMail（使用者／機密），預設會將訊息留在伺服器上 |
   |---|---|
   | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret&amp;pop3.leave.on.server=false | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret&amp;pop3.leave.on.server=false |

   **IMAP配置屬性：**

   允許您設定要搜索的標誌。

   `imap.flag.SEEN`：為新消息／未顯示消息設定false，為已讀取消息設定true

   請參 [閱](https://java.sun.com/products/javamail/javadocs/javax/mail/Flags.Flag.html) https://java.sun.com/products/javamail/javadocs/javax/mail/Flags.Flag.html以取得標幟的完整清單。

   **IMAP示例：**

   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret | 使用IMAP over SSL，以用戶／密碼連接到埠993上的GMail。 預設情況下，僅獲取新消息。 |
   |---|---|
   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret&amp;imap.flag.SEEN=true | 使用IMAP over SSL連線至GMail 993並使用使用者／機密，只會收到已看到的訊息。 |
   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret&amp;imap.flag.SEEN=true&amp;imap.flag.SEEN=false | 使用IMAP over SSL連接GMail 993和用戶／密碼，即可讀取或獲得新消息。 |

1. 保存配置。

## 設定電子報服務元件 {#configuring-the-newsletter-service-component}

設定動態消息匯入工具後，您必須設定「寄件者」位址和彈回數。

若要設定電子報服務：

1. 在OSGi主控台中，導 `<host>:<port>/system/console/configMgr` 覽至 **MCM電子報**。

1. 設定服務，並在完成時儲存變更。

   ![chlimage_1-1](assets/chlimage_1-1a.png)

   可以設定以下配置來調整行為：

   | 反彈計數器最大值(max.bounce.count) | 定義在傳送電子報時，使用者會被省略之前的彈回數。 將此值設為0會完全停用彈回數檢查。 |
   |---|---|
   | 活動無快取(sent.activity.nocache) | 定義快取設定，以用於電子報傳送的活動 |

   儲存後，電子報MCM服務會執行下列動作：

   * 在成功傳送電子報時，將活動寫入隱藏的串流給使用者。
   * 如果偵測到彈回數且使用者彈回數變更，則寫入活動。
