---
title: 對應管理中的自訂特殊字元
seo-title: 對應管理中的自訂特殊字元
description: 瞭解如何在「對應管理」中新增自訂特殊字元。
seo-description: 瞭解如何在「對應管理」中新增自訂特殊字元。
uuid: a1890f6d-8e0c-471f-a9bd-861acf1f17e6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9f26565c-a7ba-4e9e-bf77-a95eb8e351f2
docset: aem65
translation-type: tm+mt
source-git-commit: 08e53eec26e29c2403cdfc3239da3ea23da3f321

---


# 對應管理中的自訂特殊字元{#custom-special-characters-in-correspondence-management}

## 概覽 {#overview}

Correponce Management已內建210個特殊字元的預設支援，您可輕鬆將這些字元插入字母中。

例如，您可以插入下列特殊字元：

* 貨幣符號，例如€、¥和英鎊
* 數學符號，如∑、√、÷和^
* 標點符號‟as and&quot;

可以在字母中插入特殊字元：

* 在文字編 [輯器中](/help/forms/using/document-fragments.md#createtext)
* 在可編 [輯的內嵌模組中，](../../forms/using/create-correspondence.md#managecontent)

![特殊字元線模組](assets/specialcharactersinlinemodule.png)

管理員可透過自訂方式新增更多／自訂特殊字元的支援。 本文提供如何新增對其他自訂特殊字元支援的指示。

## 在「對應管理」中新增或修改自訂特殊字元的支援 {#creatingfolderstructure}

使用下列步驟新增自訂特殊字元的支援：

1. 前往並 `https://[server]:[port]/[ContextPath]/crx/de` 以管理員身分登入。
1. 在應用程式檔案夾中，建立名為 **[!UICONTROL specialcharacters]** （路徑／結構類似於specialcharacters檔案夾）的檔案夾（位於libs下的textEditorConfig檔案夾）:

   1. 在下列路徑上 **按一下特定字元** ，然後選取「覆 **蓋節點」**:

      `/libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters`

   1. 請確定「覆蓋節點」對話框具有下列值：

      **** 路徑：/libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters

      **** 覆蓋位置：/apps/

      **** 匹配節點類型：已勾選

      >[!NOTE]
      >
      >請勿在/libs分支中進行更改。 您所做的任何變更都可能會遺失，因為此分支在您執行下列動作時都會面臨變更：
      >
      >
      >
      >    * 在您的實例上升級
      >    * 套用Hot Fix
      >    * 安裝功能套件


   1. 按一 **下「確定** 」，然後按一 **下「全部儲存」**。 指定字元資料夾是在指定路徑中建立的。

      建立覆蓋後，請驗證節點結構標籤。 使用覆蓋在/apps中建立的每個節點都應具有與該節點在/libs中定義的相同類別和屬性。 如果/apps位置下的節點結構中缺少任何屬性或標籤，請將其標籤與/libs中的對應節點同步。



1. 確保textEditorConfig **[!UICONTROL 節點具有]** 以下屬性和值：

   | 名稱 | 類型 | 值 |
   |---|---|---|
   | cmConfigurationType | 字串 | cmTextEditorConfiguration |
   | cssPath | 字串 | /libs/fd/cm/ma/gui/components/admin/createasset/textcontrol/clientlibs/textcontrol |

1. 按一下右鍵以下路 **[!UICONTROL 徑中的指定字元]** ，然後選擇「 **建立」>「子節點」** ，然後按一下「全 **部保存**:

   /apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters/&lt;YourChildNode>

1. 刷新文本編輯器\建立對應UI頁。 您新增的節點是UI中「特殊」字元清單中的最後一個節點。
1. 按一下「 **全部儲存**」。
1. 視需要變更特殊字元：

<table>
 <tbody>
  <tr>
   <td><strong>至...</strong></td>
   <td><strong>完成下列步驟</strong></td>
  </tr>
  <tr>
   <td>新增自訂特殊字元</td>
   <td>
    <ol>
     <li>在"/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters"下添加子節點，其中包含強制屬性。</li>
     <li>按一下「全部儲存」</li>
     <li>刷新文本編輯器\建立對應UI以查看更改。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>更新現有特殊字元的屬性</td>
   <td>
    <ol>
     <li>覆蓋要如上所述更新的節點，並驗證標籤和類。</li>
     <li>變更任何值，例如標題、值、endValue和multipleCaption。 </li>
     <li>按一下「全部儲存」。 </li>
     <li>刷新文本編輯器\建立對應UI以查看更改。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>隱藏特殊字元</td>
   <td>
    <ol>
     <li>將要隱藏的節點覆蓋在"/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters"下</li>
     <li>將sling:hideResource(Boolean)屬性新增至要隱藏的節點（在應用程式下）。 </li>
     <li>按一下「全部儲存」。 </li>
     <li>刷新文本編輯器\建立對應UI以查看更改。<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>隱藏多個特殊字元</td>
   <td>
    <ol>
     <li>將屬性"sling:hideChildren（String或String[]）"新增至"/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters"。 </li>
     <li>將節點名稱（要隱藏的特殊字元）新增為"sling:hideChildren"屬性的值。 </li>
     <li>按一下「全部儲存」。 </li>
     <li>刷新文本編輯器\建立對應UI以查看更改。<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>為特殊字元排序</td>
   <td>
    <ol>
     <li>在"/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters"下添加子節點，其中包含強制屬性。 </li>
     <li>將"sling:orderBefore(String)"屬性新增至新建立的子節點。 </li>
     <li>將節點名稱添加為值，新添加的特殊字元將在該值之前顯示。 </li>
     <li>按一下「全部儲存」。 </li>
     <li>刷新文本編輯器\建立對應UI以查看更改。<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

