---
title: 信件和互動式通信的後處理
seo-title: Post Processing of Letters
description: 「信件後處理在信件管理中」允許您AEM建立和Forms郵件後處理流程，並將它們與信件整合。
seo-description: Post Processing of Letters in Correspondence Management lets you create AEM and Forms post processes, such as print and email, and integrate them with your letters.
uuid: 40cb349d-6ba2-4794-9ec6-dcab15c35b8d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9b06c394-8e26-429c-b78f-22afa271aeb3
docset: aem65
feature: Correspondence Management
exl-id: 91ee4422-99c1-4907-a507-5968c6984f28
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 0%

---

# 信件和互動式通信的後處理{#post-processing-of-letters-and-interactive-communications}

## 後處理 {#post-processing}

代理可以關聯並執行信件和交互通信的後處理工作流。 可以在Letter模板的「屬性」視圖中選擇要執行的後期進程。 您可以設定郵件處理，以電子郵件、打印、傳真或存檔您的最終信函。

![後處理](assets/ppoverview.png)

要將帖子進程與字母或互動式通信相關聯，您首先需要設定帖子進程。 可以對提交的信函執行兩種類型的工作流：

1. **Forms Workflow:** 這些是AEM FormsJEE流程管理工作流。 設定說明 [Forms Workflow](#formsworkflow)。

1. **工AEM作流：** 工AEM作流也可用作已提交信函的帖子流程。 設定說明 [工AEM作流](../../forms/using/aem-forms-workflow.md)。

## 表單工作流程 {#formsworkflow}

1. 在AEM中，使用以下URL開啟伺服器的Adobe Experience ManagerWeb控制台配置： `https://<server>:<port>/<contextpath>/system/console/configMgr`

   ![配置管理器](assets/2configmanager-1.png)

1. 在此頁上，找到「AEM Forms客戶端SDK配置」，然後按一下該配置展開。
1. 在伺服器URL中，在JEE伺服器上輸入AEM Forms的名稱、登錄詳細資訊，然後按一下 **保存**。

   ![輸入LiveCycle伺服器的名稱](assets/1cofigmanager.png)

1. 指定用戶名和密碼。
1. 確保將sun.util.calendar添加到反序列化防火牆配置中。

   轉到反序列化防火牆配置，在允許列出的包前置詞類下，添加sun.util.calendar。

1. 現在，您的伺服器已映射，在建立字母時，JEE上的AEM Forms的帖子進程AEM在用戶介面中可用。

   ![建立列出帖子進程的信件螢幕](assets/0configmanager.png)

1. 要驗證進程/服務，請複製進程名稱，然後返回Adobe Experience ManagerWeb控制台配置頁>AEM Forms客戶端SDK配置，並將進程作為新服務添加。

   例如，如果字母的「屬性」頁中的下拉清單將進程名稱顯示為Forms Workflow-> ValidCCPostProcess/SaveXML，請將服務名稱添加為 `ValidCCPostProcess/SaveXML`。

1. 要在JEE工作流上使用AEM Forms進行後處理，請設定必要的參數和輸出。 參數的預設值如下所示。

   轉到「Adobe Experience ManagerWeb控制台配置」頁> **[!UICONTROL 通信管理配置]** 並設定以下參數：

   1. **inPDFoc(PDF文檔參數):** 作為輸入的PDF文檔。 此輸入包含已呈現的字母作為輸入。 所指示的參數名稱是可配置的。 它們可以從配置中的「通信管理」配置中配置。
   1. **inXMLDoc（XML資料參數）:** 作為輸入的XML文檔。 此輸入包含用戶以XML形式輸入的資料。
   1. **inXDPDoc（XDP文檔參數）:** 作為輸入的XML文檔。 此輸入包含基礎佈局(XDP)。
   1. **inAttachmentDocs（Attachment Documents參數）:** 清單輸入參數。 此輸入包含作為輸入的所有附件。
   1. **重定向URL（重定向URL輸出）:** 指示要重定向到的URL的輸出類型。

   您的表單工作流必須具有PDF文檔參數或XML資料參數作為輸入，其名稱與中指定的名稱相同 **[!UICONTROL 通信管理配置]**。 在「後處理」(Post Process)下拉清單中列出該進程時，必須執行此操作。

## 發佈實例上的設定 {#settings-on-the-publish-instance}

1. 登錄 `https://localhost:publishport/aem/forms`。
1. 導航到 **[!UICONTROL 字母]** 查看發佈實例上可用的已發佈信函。
1. 配置AEMDS設定。 請參閱 [配置AEMDS設定](../../forms/using/configuring-the-processing-server-url-.md)。

>[!NOTE]
>
>在使用Forms或AEM工作流時，在從發佈伺服器提交任何資料之前，必須配置DS設定服務。 否則，報表不予受理。

## 字母實例檢索 {#letter-instances-retrieval}

通過使用LetterInstanceService中定義的以下API，可以進一步處理保存的字母實例，如檢索字母實例和刪除字母實例。

<table>
 <tbody>
  <tr>
   <td><strong>伺服器端API</strong></td>
   <td><strong>操作名稱</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td><p>公共LetterInstanceVO</p> <p>getLetterInstance(String letterInstanceId)</p> <p>拋出ICCException; </p> </td>
   <td>getLetterInstance</td>
   <td>提取指定的字母實例 </td>
  </tr>
  <tr>
   <td>Public void deleteLetterInstance(String letterInstanceId)拋出ICCException; </td>
   <td>deleteLetterInstance </td>
   <td>已刪除指定的信函實例 </td>
  </tr>
  <tr>
   <td>List getAllLetterInstances(Query)拋出ICCException; </td>
   <td>getAllLetterInstances </td>
   <td>此API基於輸入查詢參數提取字母實例。 要提取所有字母實例，查詢參數可以作為null傳遞。<br /> </td>
  </tr>
  <tr>
   <td>公共布爾型letterInstanceExists(String letterInstanceName)拋出ICCException; </td>
   <td>letterInstanceExists </td>
   <td>檢查給定名稱是否存在LetterInstance </td>
  </tr>
 </tbody>
</table>

## 將帖子流程與信件關聯 {#associating-a-post-process-with-a-letter}

在CCR用戶介面中，完成以下步驟以將後處理與字母關聯：

1. 懸停在字母上，點擊 **查看屬性**。
1. 選取&#x200B;**編輯**。
1. 在「基本屬性」中，使用「後置處理」下拉清單，選擇要與字母關聯的後置處理。 下拉列AEM出了與Forms有關的員額流程。
1. 點擊 **保存**。
1. 在使用「後置處理」配置信件後，發佈信件，並（可選）在發佈實例上指定AEMDS設定服務中的處理URL。 這可確保後處理在處理實例上運行。

## 重新載入草稿字母實例  {#reloaddraft}

可以使用以下url在用戶介面中重新載入草稿字母實例：

`https://<server>:<port>/aem/forms/`

`createcorrespondence.html?/random=$&cmLetterInstanceId=$<LetterInstanceId>`

LetterInstaceID:已提交信函實例的唯一ID。

有關保存草稿信的詳細資訊，請參閱 [保存草稿並提交信函實例](../../forms/using/create-correspondence.md#savingdrafts)。
