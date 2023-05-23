---
title: 將自定義操作添加到「資產清單」視圖
seo-title: Add custom action to the Asset Listing view
description: 本文教授如何將自定義操作添加到「資產清單」視圖
seo-description: This article teaches how to add custom action to the Asset Listing view
uuid: 45f25cfb-f08f-42c6-99c5-01900dd8cdee
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 6378ae30-a351-49f7-8e9a-f0bd4287b9d3
docset: aem65
feature: Correspondence Management
exl-id: bf6d3edb-6bf7-4d3e-b042-d75cb8e39e3f
source-git-commit: 4fa868f3ae4778d3a637e90b91f7c5909fe5f8aa
workflow-type: tm+mt
source-wordcount: '1355'
ht-degree: 3%

---

# 將自定義操作添加到「資產清單」視圖{#add-custom-action-to-the-asset-listing-view}

## 概觀 {#overview}

Tergement Management解決方案允許您將自定義操作添加到Manage Assets用戶介面。

您可以將自定義操作添加到「資產清單」視圖中，用於：

* 一個或多個資產類型或字母
* 在選擇單個、多個資產/字母或不選擇時執行（操作/命令變為活動）

此自定義通過向字母的「資產清單」視圖添加命令「下載平面PDF」的方案來演示。 此自定義方案允許用戶下載單個選定字母的平面PDF。

### 必備條件 {#prerequisites}

要完成以下或類似的方案，您需要瞭解：

* CRX
* JavaScript
* Java™

## 方案：向字母清單用戶介面添加命令以下載字母的平面PDF版本 {#addcommandtoletters}

以下步驟將命令「下載平面PDF」添加到字母的「資產清單」視圖中，並允許用戶下載所選字母的平面PDF。 使用這些步驟和相應的代碼和參數，您可以為不同的資產添加一些其他功能，如資料字典或文本。

要自定義「通信管理」以允許用戶下載扁平的PDF信函，請完成以下步驟：

1. 轉到 `https://'[server]:[port]'/[ContextPath]/crx/de` 並以管理員身份登錄。

1. 在apps資料夾中，使用以下步驟建立一個名為items的資料夾，其路徑/結構與所選資料夾中的items資料夾類似：

   1. 按一下右鍵 **項目** 資料夾，然後選擇 **覆蓋節點**:

      `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/body/content/header/items/selection/items`

      >[!NOTE]
      >
      >此路徑專用於建立與選擇多個資產/字母之一相配合的操作。 如果要建立不進行選擇而起作用的操作，請為以下路徑建立覆蓋節點，並相應完成其餘步驟：
      >
      >
      >`/libs/fd/cm/ma/gui/content/cmassets/jcr:content/body/content/header/items/default/items`

      ![建立節點](assets/1_itemscreatenode.png)

   1. 確保「覆蓋節點」對話框具有以下值：

      **路徑：** /libs/fd/cm/ma/gui/content/cmassets/jcr：內容/正文/內容/標題/項目/選擇/項目

      **位置：** /apps/

      **匹配節點類型：** 已選擇

      ![覆蓋節點](assets/2_createnodedownloadflatpdf.png)

   1. 按一下&#x200B;**「確定」**。資料夾結構是在apps資料夾中建立的。

      按一下 **全部保存**。

1. 在新建立的項目資料夾下，為特定資產中的自定義按鈕/操作添加一個節點(示例：downloadFlatPDF)，執行以下步驟：

   1. 按一下右鍵 **項目** 資料夾和 **建立** > **建立節點**。

   1. 確保「建立節點」對話框具有以下值，然後按一下 **確定**:

      **名稱：** downloadFlatPDF（或您要為此屬性指定的名稱）

      **類型：** nt：非結構化

   1. 按一下您建立的新節點（此處下載FlatPDF）。 CRX顯示節點的屬性。

   1. 將以下屬性添加到節點（此處為downloadFlatPDF），然後按一下 **全部保存**:

      <table>
        <tbody>
        <tr>
        <td><strong>名稱</strong></td>
        <td><strong>類型</strong></td>
        <td><strong>值 和說明</strong></td>
        </tr>
        <tr>
        <td>類別</td>
        <td>字串</td>
        <td>基礎收集 — 操作</td>
        </tr>
        <tr>
        <td>基礎收集 — 操作</td>
        <td>字串</td>
        <td><p>{「目標」："。cq-manageasset-admin-childpages", "activeSelectionCount":"single","type":"字母"}<br /> <br /> <br /> <strong>activeSelectionCount</strong> 可以是單個或多個，以允許選擇執行自定義操作的單個或多個資產。</p> <p><strong>類型</strong> 可以是下列項中的一個或多個（逗號分隔多個項）:字母、文本、清單、條件、自動詞</p> </td>
        </tr>
        <tr>
        <td>圖示</td>
        <td>字串</td>
        <td>表徵圖下載<br /> <br /> 「通信管理」(Tergement Management)在命令/菜單的左側顯示的表徵圖。 有關可用的不同表徵圖和設定，請參見 <a href="https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html" target="_blank">CoralUI表徵圖文檔</a>。<br /> </td>
        </tr>
        <tr>
        <td>jcr:primaryType</td>
        <td>名稱</td>
        <td>nt:unstructured</td>
        </tr>
        <tr>
        <td>裸</td>
        <td>字串</td>
        <td>下載 — 平面 — pdf — 按鈕</td>
        </tr>
        <tr>
        <td>sling:resourceType</td>
        <td>字串</td>
        <td>花崗岩/ui/元件/端或/操作欄/按鈕</td>
        </tr>
        <tr>
        <td>text</td>
        <td>字串</td>
        <td>下載平面PDF（或任何其他標籤）<br /> <br /> 顯示在「資產清單」介面中的命令</td>
        </tr>
        <tr>
        <td>標題</td>
        <td>字串</td>
        <td>下載所選字母的平PDF（或任何其他標籤/Alt文本）<br /> <br /> 標題是當用戶在自定義命令上移動時Tergement Management顯示的備用文本。</td>
        </tr>
        </tbody>
       </table>

1. 在apps資料夾中，使用以下步驟建立一個名為js的資料夾，其路徑/結構類似於管理資料夾中的items資料夾：

   1. 按一下右鍵 **j** 資料夾，然後選擇 **覆蓋節點**:

      `/libs/fd/cm/ma/gui/components/admin/clientlibs/admin/js`

   1. 確保「覆蓋節點」對話框具有以下值：

      **路徑：** /libs/fd/cm/ma/gui/components/admin/clientlibs/admin/js

      **位置：** /apps/

      **匹配節點類型：** 已選擇

   1. 按一下&#x200B;**「確定」**。資料夾結構是在apps資料夾中建立的。 按一下 **全部保存**。

1. 在js資料夾中，使用以下步驟建立名為formaction.js的檔案，該檔案包含用於按鈕操作處理的代碼：

   1. 按一下右鍵 **j** 資料夾，然後選擇 **建立>建立檔案**:

      `/apps/fd/cm/ma/gui/components/admin/clientlibs/admin/js`

      將檔案命名為formaction.js。

   1. 按兩下檔案以在CRX中開啟它。
   1. 在formaction.js檔案（在/apps分支下）中，將代碼從formaction.js檔案複製到以下位置：

      `/libs/fd/cm/ma/gui/components/admin/clientlibs/admin/js/formaction.js`

      然後，在formaction.js檔案（在/apps分支下）的末尾添加以下代碼，然後按一下 **全部保存**:

      ```javascript
      /* Action url for xml file to be added.*/
      var ACTION_URL = "/apps/fd/cm/ma/gui/content/commons/actionhandlers/items/letterpdfdownloader.html";
      
      /* File upload handling*/
      var fileSelectedHandler = function(e){
          if(e && e.target && e.target.value)
              $(".downloadLetterPDFBtn").removeAttr('disabled');
          else
              $(".downloadLetterPDFBtn").attr('disabled','disabled');
      }
      
      /*Handing of Download button in pop up.*/
      var downloadClickHandler = function(){
          $('#downloadLetterPDFDilaog').modal("hide");
          var element = $('.foundation-selections-item');
          var path = $(element).data("path");
          $("#fileUploadForm").attr('action', ACTION_URL + "?letterId="+path).submit();
      }
      
      /*Click handling on action button.*/
      $(document).on("click",'.download-flat-pdf-button',function(e){
          $("#uploadSamepledata").val("");
           if($('#downloadLetterPDFDilaog').length == 0){
              $(document).on("click",".downloadLetterPDFBtn",downloadClickHandler);
              $(document).on("change","#uploadSamepledata",fileSelectedHandler);
              $("body").append(downloadLetterPDFDilaog);
          }
            $('#downloadLetterPDFDilaog').modal("show");
      });
      
      /*Download popup.*/
      var downloadLetterPDFDilaog = '<div id="downloadLetterPDFDilaog" class="coral-Modal notice " role="dialog"  aria-hidden="true">'+
          '<form id="fileUploadForm" method="POST" enctype="multipart/form-data">'+
              '<div class="coral-Modal-header">'+
                  '<h2 class="coral-Modal-title coral-Heading coral-Heading--2" id="modal-header1443020790107-label" tabindex="0">Download Letter as PDF.</h2>'+
                  '<button type="button" class="coral-MinimalButton coral-Modal-closeButton" data-dismiss="modal">×</button>'+
              '</div>'+
              '<div class="coral-Modal-body" id="modal-header1443020790107-message" role="document" tabindex="0">'+
                  '<div class="coral-Modal-message">'+
                      '<p></p>'+
                  '</div>'+
                  '<div class="coral-Modal-uploader">'+
                      '<p>Select sample data for letter.</p>'+
                      '<input type="file" id="uploadSamepledata" name="file" accept=".xml" size="70px">'+
                  '</div>'+
              '</div>'+
           '</form>'+
              '<div class="coral-Modal-footer">'+
                  '<button type="button" class="coral-Button" data-dismiss="modal">Cancel</button>'+
                  '<button type="button" class="coral-Button coral-Button--primary downloadLetterPDFBtn" disabled="disabled">Download</button>'+
              '</div>'+
      '</div>';
      ```

      在此步驟中添加的代碼將覆蓋libs資料夾下的代碼，因此將上一個代碼複製到/apps分支中的formaction.js檔案。 將代碼從/libs分支複製到/apps分支可確保以前的功能也能正常工作。

      上述代碼用於對在此過程中建立的命令執行字母特定的操作處理。 要處理其他資產的操作，請修改JavaScript代碼。

1. 在apps資料夾中，使用以下步驟建立名為items的資料夾，其路徑/結構與actionhandlers資料夾中的items資料夾類似：

   1. 按一下右鍵 **項目** 資料夾，然後選擇 **覆蓋節點**:

      `/libs/fd/cm/ma/gui/content/commons/actionhandlers/items/`

   1. 確保「覆蓋節點」對話框具有以下值：

      **路徑：** /libs/fd/cm/ma/gui/content/commons/actionhlers/items/

      **位置：** /apps/

      **匹配節點類型：** 已選擇

   1. 按一下&#x200B;**「確定」**。資料夾結構是在apps資料夾中建立的。

   1. 按一下 **全部保存**。

1. 在新建立的項節點下，為特定資產中的自定義按鈕/操作添加一個節點(示例：letterpdfdownloader)，執行以下步驟：

   1. 按一下右鍵項目資料夾並選擇 **「建立」>「建立節點」**。

   1. 確保「建立節點」對話框具有以下值，然後按一下 **確定**:

      **名稱：** letterpdfdownloader（或要為此屬性指定的名稱）必須唯一。 如果在此處使用不同的名稱，也可在formaction.js檔案的ACTION_URL變數中指定相同的名稱。)

      **類型：** nt：非結構化

   1. 按一下您建立的新節點（此處下載FlatPDF）。 CRX顯示節點的屬性。

   1. 將以下屬性添加到節點（此處為letterpdfdownloader），然後按一下 **全部保存**:

      | **名稱** | **類型** | **值** |
      |---|---|---|
      | sling:resourceType | 字串 | fd/cm/ma/gui/元件/admin/clientlibs/admin |

1. 建立名為POST.jsp的檔案，該檔案的代碼用於在以下位置處理命令：

   /apps/fd/cm/ma/gui/components/admin/clientlibs/admin

   1. 按一下右鍵 **管理員** 資料夾，然後選擇 **建立>建立檔案**:

      /apps/fd/cm/ma/gui/components/admin/clientlibs/admin

      將檔案命名為POST.jsp。 (檔案名只需要為POST.jsp。)

   1. 按兩下 **POST.jsp** 的子菜單。
   1. 將以下代碼添加到POST.jsp檔案中，然後按一下 **全部保存**:

      此代碼特定於字母呈現服務。 對於任何其他資產，將該資產的Java™庫添加到此代碼中。 有關AEM FormsAPI的詳細資訊，請參見 [AEM FormsAPI](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html)。

      有關庫的詳細信AEM息，請參AEM閱 [元件](/help/sites-developing/components.md)。

      ```xml
      /*Import libraries. Here we are downloading letter flat pdf with input xml data so we require letterRender Api. For any other Module functionality we need to first import that library. */
      <%@include file="/libs/foundation/global.jsp"%>
      <!DOCTYPE html lang="en" PUBLIC "-//W3C//DTD XHTML 1.1//EN" "https://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">
      <%@page import="com.adobe.icc.ddg.api.*"%>
      <%@page import="com.adobe.icc.dbforms.obj.*"%>
      <%@page import="com.adobe.icc.render.obj.*" %>
      <%@page import="com.adobe.icc.services.api.*" %>
      <%@page import="org.apache.sling.api.resource.*" %>
      <%@page import="java.io.File" %>
      <%@page import="java.util.*" %>
      <%@page import="com.adobe.livecycle.content.appcontext.AppContextManager"%>
      <%@page import=" com.adobe.icc.dbforms.exceptions.ICCException"%>
      <%@page import="java.io.InputStream" %>
      <%@page import="java.io.FileInputStream" %>
      <%@page import="org.apache.commons.io.IOUtils" %>
      <%@page session="false" contentType="text/html; charset=utf-8"%>
      <%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0"%>
      <%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %>
       <%@page session="false" contentType="text/html; charset=utf-8"%>
      <%
         AppContextManager.setCurrentAppContext("/content/apps/cm");
         /*Get letter id sent in js file.*/
          String letterId = request.getParameter("letterId");
          if(letterId.lastIndexOf("?") != -1)
              letterId = letterId.substring(0, letterId.indexOf("?"));
          String fileName = null;
          String letterName = null;
          InputStream inputStream = null;
          /*Get xml file data*/
          if (slingRequest.getRequestParameter("file") != null)
              inputStream = slingRequest.getRequestParameter("file").getInputStream();
          if(letterId != null){
              String xmlData = null;
              try{
                  xmlData = IOUtils.toString(inputStream, "UTF-8");
              }
              catch (Exception e) {
                  log.error("Xml data does not exists.");
              }
              /*letter Name from letter letter id.*/
              letterName = letterId.substring(letterId.lastIndexOf("/")+1);
              /*Invoking letter render services API.*/
              LetterRenderService letterRenderService = sling.getService(LetterRenderService.class);
              /*using CM renderLetter api to get pdfbytes.*/
              PDFResponseType  pdfResponseType= letterRenderService.renderLetter(letterId,xmlData,true,false,false,false);
              byte[] bytes = null;
              /*Downloading pdf bytes as pdf.*/
              if(pdfResponseType != null && pdfResponseType.getFile() != null){
                  bytes = pdfResponseType.getFile().getDocument();
                  /*set the response header to enable download*/
                  response.setContentType("application/OCTET-STREAM");
                  response.setHeader("Content-Disposition", "attachment;filename=\"" + letterName + ".pdf\"");
                  response.setHeader("Pragma", "cache");
                  response.setHeader("Cache-Control", "private");
                  out.clear();
                  response.getOutputStream().write(bytes);
              }
          }
          else{
              log.error("Letter id does not exists.");
          }
      %>
      ```

## 使用自定義功能下載字母的平面PDF {#download-flat-pdf-of-a-letter-using-the-custom-functionality}

添加自定義功能以下載字母的平面PDF後，您可以使用以下步驟下載所選字母的平面PDF版本：

1. 轉到 `https://'[server]:[port]'/[ContextPath]/projects.html` 登錄。

1. 選擇 **Forms>字母**。 Tergement Management列出系統中可用的信函。
1. 按一下 **選擇** 然後按一下一個字母來選擇它。
1. 選擇 **更多** > **&lt;download flat=&quot;&quot; pdf=&quot;&quot;>** （使用本文說明建立的自定義功能）。 將顯示「以PDF形式下載信函」對話框。

   菜單項名稱、功能和Alt-text根據在 [方案：向字母清單用戶介面添加命令以下載字母的平面PDF版本。](#addcommandtoletters)

   ![自定義功能：下載平面PDF](assets/5_downloadflatpdf.png)

1. 在「作為PDF的下載信函」對話框中，選擇要從中填充PDF中資料的相關XML。

   >[!NOTE]
   >
   >在將字母下載為平面PDF之前，可以使用 **建立報告** 的雙曲餘切值。

   ![下載信件作為PDF](assets/6_downloadflatpdf.png)

   這封信作為平面PDF下載到你的電腦。
