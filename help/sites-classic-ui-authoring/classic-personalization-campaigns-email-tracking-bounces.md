---
title: 追蹤退信電子郵件
description: 當您傳送電子報給許多使用者時，清單中通常會有一些無效的電子郵件地址。 傳送電子報到這些地址會退回。 AEM可以管理這些跳出，並可在超出設定的跳出計數器後停止傳送電子報至這些地址。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: 6cda0a68-0df9-44e7-ae4f-9951411af6dd
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 0%

---

# 追蹤退信電子郵件{#tracking-bounced-emails}

>[!NOTE]
>
>Adobe不打算進一步增強對AEM SMTP服務傳送的已開啟/已退回電子郵件的追蹤。
>
>建議為 [使用Adobe Campaign及其AEM整合](/help/sites-administering/campaign.md).

當您傳送電子報給許多使用者時，清單中通常會有一些無效的電子郵件地址。 傳送電子報到這些地址會退回。 AEM可以管理這些跳出，並可在超出設定的跳出計數器後停止傳送電子報至這些地址。 依預設，跳出率設為3，但可設定。

若要設定AEM以追蹤退信電子郵件，請設定AEM以輪詢接收退信電子郵件的現有信箱。 通常，此位置是您指定傳送Newsletter的來源電子郵件地址。 AEM會輪詢此收件匣，並匯入輪詢設定中所指定路徑下的所有電子郵件。 然後會觸發工作流程以搜尋使用者內退信的電子郵件地址，並相應地更新使用者的bounceCounter屬性值。 超過設定的最大跳出數後，使用者會從Newsletter清單中移除。

## 設定摘要匯入工具 {#configuring-the-feed-importer}

摘要匯入工具可讓您重複地將外部來源的內容匯入存放庫。 透過此摘要匯入工具的設定，AEM會檢查寄件者的信箱是否有退回的電子郵件。

若要設定摘要匯入工具來追蹤跳出的電子郵件，請執行下列動作：

1. 在 **工具**，選取摘要匯入工具。

1. 按一下 **新增** 以建立組態。

   ![chlimage_1](assets/chlimage_1a.png)

1. 選取型別，並將資訊新增至輪詢URL，以便您設定主機和連線埠，以新增設定。 此外，將一些郵件和通訊協定特定的引數新增到URL查詢中。 設定為每天至少輪詢一次。

   所有設定都需要輪詢URL中下列專案的相關資訊：

   `username`：用來連線的使用者名稱

   `password`：用來連線的密碼

   此外，您也可以根據通訊協定來設定某些設定。

   **POP3設定屬性：**

   `pop3.leave.on.server`：定義是否要將訊息留在伺服器上。 設為true會在伺服器上留下訊息，否則則為false。 預設為true。

   **POP3範例：**

   | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret | 透過SSL使用pop3連線至連線埠995上的GMail （含使用者/密碼），依預設會在伺服器上留下訊息 |
   |---|---|
   | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret&amp;pop3.leave.on.server=false | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret&amp;pop3.leave.on.server=false |

   **IMAP設定屬性：**

   可讓您設定要搜尋的標幟。

   `imap.flag.SEEN`：設定新增/未檢視訊息為false，已讀取訊息為true

   另請參閱 [https://javaee.github.io/javamail/docs/api/index.html?javax/mail/Flags.Flag.html](https://javaee.github.io/javamail/docs/api/index.html?javax/mail/Flags.Flag.html) 以取得完整的旗標清單。

   **IMAP範例：**

   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret | 透過SSL使用IMAP連線到連線埠993上的GMail，並使用user/secret。 僅依預設取得新訊息。 |
   |---|---|
   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret&amp;imap.flag.SEEN=true | 透過SSL使用IMAP連線到具有使用者/密碼的GMail 993，只看到訊息。 |
   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret&amp;imap.flag.SEEN=true&amp;imap.flag.SEEN=false | 透過SSL使用IMAP連線到具有使用者/密碼的GMail 993，已讀取或收到新訊息。 |

1. 儲存設定。

## 設定Newsletter服務元件 {#configuring-the-newsletter-service-component}

在設定摘要匯入工具後，請設定「寄件者」位址和「跳出」計數器。

若要設定Newsletter服務：

1. 在OSGi主控台中，位於 `<host>:<port>/system/console/configMgr`，導覽至 **MCM電子報**.

1. 完成時設定服務並儲存變更。

   ![chlimage_1-1](assets/chlimage_1-1a.png)

   可設定下列設定來調整行為：

   | 彈回計數器上限(max.bounce.count) | 定義在傳送Newsletter時省略使用者之前的跳出次數。 將此值設定為0 ，會完全停用退信檢查。 |
   |---|---|
   | 活動無快取(sent.activity.nocache) | 定義用於電子報傳送活動的快取設定 |

   儲存後，Newsletter MCM服務會執行下列動作：

   * 在成功傳送電子報時將活動寫入使用者隱藏的資料流。
   * 在偵測到跳出且使用者跳出計數器變更時寫入活動。
