---
title: 建立自定義工具欄佈局
seo-title: Creating custom toolbar layout
description: 可以為表單指定工具欄佈局。 工具欄佈局定義窗體上工具欄的命令和佈局。
seo-description: You can specify a toolbar layout for the form. The toolbar layout defines the commands and the layout of the toolbar on the form.
uuid: 389a715a-4c91-4a63-895d-bb2d0f1054eb
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 0d817a7e-2758-4308-abda-6194716c2d97
docset: aem65
exl-id: 44516956-00aa-41d5-a7e9-746c7618e5db
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---

# 建立自定義工具欄佈局{#creating-custom-toolbar-layout}

## 工具欄佈局 {#layout}

建立自適應表單時，可以為表單指定工具欄佈局。 工具欄佈局定義窗體上工具欄的命令和佈局。

工具欄佈局使用嚴重依賴由複雜JavaScript和CSS代碼驅動的客戶端處理。 組織和優化此代碼的服務可能是一個複雜的問題。 為幫助解決此問題，AEM提供了客戶端庫資料夾，允許您將客戶端代碼儲存在儲存庫中，將其組織成類別，並定義將每類代碼提供給客戶端的時間和方式。 然後，客戶端庫系統會注意在最終網頁中生成正確的連結以載入正確的代碼。 有關詳細資訊，請參見 [客戶端庫在中的工作方AEM式。](/help/sites-developing/clientlibs.md)

![工具欄的示例佈局](assets/default_toolbar_layout.png)

工具欄的示例佈局

自適應表單提供一組現成佈局：

![工具欄佈局可用 ](assets/toolbar1.png)

工具欄佈局可用

此外，還可以建立自定義工具欄佈局。

以下過程詳細介紹了建立自定義工具欄的步驟，該工具欄在工具欄中顯示三個操作，在工具欄的下拉清單中顯示其他操作。

附加的內容包包含下面描述的整個代碼。 安裝內容包後，開啟 `/content/forms/af/CustomLayoutDemo.html` 來查看自定義工具欄佈局演示。

CustomToolbarLayoutDemo.zip

[獲取檔案](assets/customtoolbarlayoutdemo.zip)
演示自定義工具欄佈局

## 建立自定義工具欄佈局 {#layout-1}

1. 建立資料夾以維護自定義工具欄佈局。 例如：

   `/apps/customlayout/toolbar`。

   要建立自定義佈局，可以使用（和自定義）以下資料夾中提供的一個預置工具欄佈局：

   `/libs/fd/af/layouts/toolbar`

   例如，複製 `mobileFixedToolbarLayout` 節點 `/libs/fd/af/layouts/toolbar` 資料夾 `/apps/customlayout/toolbar` 的子菜單。

   另外，將工具欄Common.jsp複製到 `/apps/customlayout/toolbar` 的子菜單。

   >[!NOTE]
   >
   >為維護自定義佈局而建立的資料夾 `apps` 的子菜單。

1. 更名複製的節點， `mobileFixedToolbarLayout`。 `customToolbarLayout.`

   另外，請提供節點的相關說明。 例如，將節點的jcr:description更改為 **工具欄的自定義佈局**。

   的 `guideComponentType` 節點的屬性決定佈局類型。 在這種情況下，佈局類型為工具欄，因此它會顯示在工具欄佈局選擇下拉清單中。

   ![具有相關描述的節點](assets/toolbar3.png)

   具有相關描述的節點

   新的自定義工具欄佈局顯示在 **自適應表單工具欄** 對話框配置。

   ![可用工具欄佈局清單](assets/toolbar4.png)

   可用工具欄佈局清單

   >[!NOTE]
   >
   >在上一步中更新的說明將顯示在「佈局」(Layout)下拉清單中。

1. 選擇此自定義工具欄佈局，然後按一下「確定」。

   在 `/etc/customlayout` 並在 `customToolbarLayout.jsp`。

   ![customToolbarLayout.css檔案的路徑](assets/toolbar_3.png)

   customToolbarLayout.css檔案的路徑

   範例 `customToolbarLayout.jsp`:

   ```jsp
   <%@include file="/libs/fd/af/components/guidesglobal.jsp" %>
   <cq:includeClientLib categories="customtoolbarlayout" />
   <c:if test="${isEditMode}">
           <cq:includeClientLib categories="customtoolbarlayoutauthor" />
   </c:if>
   <div class="guidetoolbar mobileToolbar mobilecustomToolbar" data-guide-position-class="guide-element-hide">
       <div data-guide-scroll-indicator="true"></div>
       <%@include file="../toolbarCommon.jsp" %>
   </div>
   ```

   >[!NOTE]
   >
   >為佈局添加指導工具欄類。 工具欄的出廠設定樣式是針對導向工具欄類定義的。

   範例 `toolBarCommon.jsp`:

   ```jsp
   <%@taglib prefix="fn" uri="https://java.sun.com/jsp/jstl/functions"%>
   <%--------------------
   This code iterates over all the tool bar items using the guideToolbar bean.
   If the number of toolbar items are more than 3, then we create a dropdown menu using bootstrap for other actions present in the toolbar.
   In both desktop and mobile devices, the layout is different.
   ---------------------------------%>
   
   <c:forEach items="${guideToolbar.items}" var="toolbarItem" varStatus="loop">
       <c:choose>
         <c:when test="${loop.index gt 2}">
      <c:choose>
       <c:when test="${loop.index eq 3}">
                     <div class="btn-group dropdown">
                       <button type="button" class="btn btn-primary dropdown-toggle label" data-toggle="dropdown">Actions <span class="caret"></code></button>
                       <button type="button" class="btn btn-primary dropdown-toggle icon" data-toggle="dropdown"><span class="glyphicon glyphicon-th-list"></code></button>
             <ul class="dropdown-menu" role="menu">
                           <li>
                               <div id="${toolbarItem.id}_guide-item">
                                 <sling:include path="${toolbarItem.path}" resourceType="${toolbarItem.resourceType}"/>
                              </div>
                           </li>
                           <c:if test="${loop.index eq (fn:length(guideToolbar.items)-1)}">
                                </ul>
                                </div>
                           </c:if>
       </c:when>
       <c:when test="${loop.index eq (fn:length(guideToolbar.items)-1)}">
                          <li>
                                     <div id="${toolbarItem.id}_guide-item">
                                         <sling:include path="${toolbarItem.path}" resourceType="${toolbarItem.resourceType}"/>
                                     </div>
                           </li>
                       </ul>
                     </div>
   
       </c:when>
       <c:otherwise>
         <li>
          <div id="${toolbarItem.id}_guide-item">
           <sling:include path="${toolbarItem.path}" resourceType="${toolbarItem.resourceType}"/>
          </div>
         </li>
       </c:otherwise>
      </c:choose>
         </c:when>
         <c:otherwise>
     <div id="${toolbarItem.id}_guide-item">
           <sling:include path="${toolbarItem.path}" resourceType="${toolbarItem.resourceType}"/>
        </div>
         </c:otherwise>
    </c:choose>
   </c:forEach>
   ```

   客戶端庫節點記憶體在的CSS:

   ```css
   .mobilecustomToolbar .dropdown {
       display: inline-block;
   }
   
   .mobilecustomToolbar .dropdown {
       float: right;
   }
   
   .mobilecustomToolbar .dropdown > button {
      padding: 6px 12px;
   }
   
   .mobilecustomToolbar .dropdown .guideFieldWidget, .mobilecustomToolbar .dropdown .guideFieldWidget button {
       width: 100%;
   }
   
   .mobilecustomToolbar .dropdown .caret{
       border-bottom: 6px solid;
       border-right: 6px solid transparent;
       border-left: 6px solid transparent;
    border-top: transparent;
   }
   
   .mobilecustomToolbar .dropdown-menu{
    top: auto;
    bottom: 100%;
   }
   
   .mobilecustomToolbar .btn-group {
    vertical-align: super;
   }
   
   .mobilecustomToolbar .glyphicon {
    font-size: 24px;
   }
   
   @media (max-width: 767px){
   
    .mobilecustomToolbar .dropdown .guideButton .iconButton-icon {
      display: none;
       }
   
       .mobilecustomToolbar .dropdown .guideButton .iconButton-label {
      display: inline-block;
       }
   
       .mobilecustomToolbar .dropdown .guideButton button {
      background-color: #013853;
       }
   
    .mobilecustomToolbar .btn-group {
     vertical-align: top;
    }
   
   }
   ```

>[!NOTE]
>
>在上一步中更新的說明將顯示在「佈局」(Layout)下拉清單中。

![自定義佈局工具欄的案頭視圖](assets/toolbar_1.png)

自定義佈局工具欄的案頭視圖
