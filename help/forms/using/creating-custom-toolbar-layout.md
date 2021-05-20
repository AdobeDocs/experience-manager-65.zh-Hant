---
title: 建立自訂工具列版面
seo-title: 建立自訂工具列版面
description: 您可以指定表單的工具列版面。 工具欄佈局定義命令和窗體上工具欄的佈局。
seo-description: 您可以指定表單的工具列版面。 工具欄佈局定義命令和窗體上工具欄的佈局。
uuid: 389a715a-4c91-4a63-895d-bb2d0f1054eb
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 0d817a7e-2758-4308-abda-6194716c2d97
docset: aem65
exl-id: 44516956-00aa-41d5-a7e9-746c7618e5db
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 0%

---

# 建立自定義工具欄佈局{#creating-custom-toolbar-layout}

## 工具列配置 {#layout}

建立最適化表單時，您可以指定表單的工具列版面。 工具欄佈局定義命令和窗體上工具欄的佈局。

工具列配置使用時，主要依賴由複雜JavaScript和CSS程式碼驅動的用戶端處理。 組織並最佳化此程式碼的服務可能是個複雜的問題。 為協助處理此問題，AEM提供用戶端程式庫資料夾，可讓您將用戶端程式碼儲存在存放庫中、將其組織為類別，以及定義將各類別的程式碼提供給用戶端的時間和方式。 然後，用戶端資料庫系統會負責在您的最終網頁中產生正確的連結，以載入正確的程式碼。 如需詳細資訊，請參閱[用戶端程式庫在AEM中的運作方式。](/help/sites-developing/clientlibs.md)

![工具列的範例版面](assets/default_toolbar_layout.png)

工具列的範例版面

適用性表單提供一組現成的配置：

![可用的工具列配置  ](assets/toolbar1.png)

可用的工具列配置

此外，您還可以建立自訂工具列版面。

以下過程詳細說明了建立自定義工具欄的步驟，該工具欄在工具欄中顯示三個操作，在工具欄的下拉清單中顯示其他操作。

附加的內容套件包含下列說明的整個程式碼。 安裝內容套件後，請開啟`/content/forms/af/CustomLayoutDemo.html`以檢視自訂工具列版面示範。

CustomToolbarLayoutDemo.zip

[獲取檔](assets/customtoolbarlayoutdemo.zip)
案演示自定義工具欄佈局

## 建立自定義工具欄佈局{#layout-1}

1. 建立資料夾以維護自訂工具列配置。 例如：

   `/apps/customlayout/toolbar`。

   若要建立自訂版面，您可以使用（和自訂）下列資料夾中可用的其中一個現成工具列版面：

   `/libs/fd/af/layouts/toolbar`

   例如，將`mobileFixedToolbarLayout`節點從`/libs/fd/af/layouts/toolbar`資料夾複製到`/apps/customlayout/toolbar`資料夾。

   同時，將toolbarCommon.jsp複製到`/apps/customlayout/toolbar`資料夾。

   >[!NOTE]
   >
   >您為維護自定義佈局而建立的資料夾很多都是使用`apps`資料夾建立的。

1. 將複製的節點`mobileFixedToolbarLayout`更名為`customToolbarLayout.`

   此外，請提供節點的相關說明。 例如，將節點的jcr:description更改為工具欄&#x200B;**自定義佈局**。

   節點的`guideComponentType`屬性決定佈局類型。 在這種情況下，版面類型是工具欄，因此它會顯示在工具欄版面選擇下拉清單中。

   ![具有相關說明的節點](assets/toolbar3.png)

   具有相關說明的節點

   新的自定義工具欄佈局顯示在&#x200B;**適用性表單工具欄**&#x200B;對話框配置中。

   ![可用工具欄佈局清單](assets/toolbar4.png)

   可用工具欄佈局清單

   >[!NOTE]
   >
   >在上一步驟中更新的說明會顯示在「配置」下拉式清單中。

1. 選取此自訂工具列版面，然後按一下「確定」。

   在`/etc/customlayout`節點中新增clientlib（javascript和css），並在`customToolbarLayout.jsp`中包含clientlib的參考。

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
   >為版面添加指導工具欄類。 工具列的現成樣式是針對引導工具列類別而定義的。

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

   clientlib節點內部存在的CSS:

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
>在上一步驟中更新的說明會顯示在「配置」下拉式清單中。

![自定義佈局工具欄的案頭視圖](assets/toolbar_1.png)

自定義佈局工具欄的案頭視圖
