---
title: 通訊管理中的自訂特殊字元
description: 瞭解如何在通訊管理中新增自訂特殊字元。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: 3e978c3e-12f2-4dc6-801d-8ab4c5df6700
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 1%

---

# 通訊管理中的自訂特殊字元{#custom-special-characters-in-correspondence-management}

## 概觀 {#overview}

「通訊管理」已內建預設支援210個特殊字元，您可以輕鬆插入信件。

例如，您可以插入下列特殊字元：

* 幣別符號，例如€、¥和£
* 數學符號，例如∑、√、∂和^
* 標點符號為&quot;和&quot;

您可以在字母中插入特殊字元：

* 在[文字編輯器](/help/forms/using/document-fragments.md#createtext)中
* 在[可編輯的通訊模組](../../forms/using/create-correspondence.md#managecontent)中

![specialcharactersinlinemodule](assets/specialcharactersinlinemodule.png)

管理員可透過自訂來新增對更多/自訂特殊字元的支援。 本文提供如何新增對其他自訂特殊字元的支援的說明。

## 在通訊管理中新增或修改對自訂特殊字元的支援 {#creatingfolderstructure}

使用下列步驟新增自訂特殊字元的支援：

1. 前往`https://'[server]:[port]'/[ContextPath]/crx/de`並以管理員身分登入。
1. 在apps資料夾中，建立名為&#x200B;**[!UICONTROL specialcharacters]**&#x200B;的資料夾，其路徑/結構類似於specialcharacters資料夾（在libs底下的textEditorConfig資料夾中）：

   1. 在下列路徑的&#x200B;**specialcharacters**&#x200B;資料夾上按一下滑鼠右鍵，然後選取&#x200B;**覆蓋節點**：

      `/libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters`

   1. 請確定「覆蓋節點」對話方塊是否具備下列值：

      **路徑：** /libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters

      **覆蓋位置：** /apps/

      **符合節點型別：**&#x200B;已核取

      >[!NOTE]
      >
      >請勿變更/libs分支。 您所做的任何變更都可能會遺失，因為每當您：
      >
      >
      >
      >    * 在您的執行個體上升級
      >    * 套用Hot Fix
      >    * 安裝Feature Pack
      >
      >

   1. 按一下[確定]&#x200B;**&#x200B;**，然後按一下[儲存全部]&#x200B;**&#x200B;**。 specialcharacters資料夾是在指定的路徑中建立的。

      建立覆蓋圖後，請驗證節點結構標籤。 使用覆蓋在/apps中建立的每個節點，都應與該節點的/libs中定義的類別和屬性相同。 如果/apps位置下方的節點結構中缺少任何屬性或標籤，請將其標籤與/libs中的對應節點同步。

1. 請確定&#x200B;**[!UICONTROL textEditorConfig]**&#x200B;節點具有下列屬性和值：

   | 名稱 | 類型 | 值 |
   |---|---|---|
   | cmConfigurationtype | 字串 | cmTextEditorConfiguration |
   | cssPath | 字串 | /libs/fd/cm/ma/gui/components/admin/createasset/textcontrol/clientlibs/textcontrol |

1. 在下列路徑的&#x200B;**[!UICONTROL specialcharacters]**&#x200B;資料夾上按一下滑鼠右鍵，並選取&#x200B;**建立>子節點**，然後按一下&#x200B;**儲存全部**：

   /apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters/&lt;YourChildNode>

1. 重新整理文字編輯器\建立通訊UI頁面。 您新增的節點是UI中特殊字元清單的最後一個節點。
1. 按一下&#x200B;**「儲存全部」**。
1. 視需要變更特殊字元：

<table>
 <tbody>
  <tr>
   <td><strong>至……</strong></td>
   <td><strong>完成下列步驟</strong></td>
  </tr>
  <tr>
   <td>新增自訂特殊字元</td>
   <td>
    <ol>
     <li>在「/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters」下新增具有強制屬性的子節點。</li>
     <li>按一下「儲存全部」</li>
     <li>重新整理文字編輯器\建立通訊UI，以便您檢視變更。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>更新現有的特殊字元屬性</td>
   <td>
    <ol>
     <li>覆蓋要更新的節點（如上所述），並驗證標籤和類別。</li>
     <li>變更任何值，例如caption、value、endValue和multipleCaption。 </li>
     <li>按一下「儲存全部」。 </li>
     <li>重新整理文字編輯器\建立通訊UI，以便您檢視變更。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>隱藏特殊字元</td>
   <td>
    <ol>
     <li>覆蓋要隱藏在「/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters」下的節點</li>
     <li>將sling：hideResource （布林值）屬性新增至要隱藏的節點（應用程式底下）。 </li>
     <li>按一下「儲存全部」。 </li>
     <li>重新整理文字編輯器\建立通訊UI，以便您檢視變更。<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>隱藏多個特殊字元</td>
   <td>
    <ol>
     <li>將屬性「sling：hideChildren （String或String[]）」新增至「/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters」。 </li>
     <li>新增節點名稱（要隱藏的特殊字元）作為「sling：hideChildren」屬性的值。 </li>
     <li>按一下「儲存全部」。 </li>
     <li>重新整理文字編輯器\建立通訊UI，以便您檢視變更。<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>排序特殊字元</td>
   <td>
    <ol>
     <li>在「/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters」下新增具有強制屬性的子節點。 </li>
     <li>將「sling：orderBefore (String)」屬性新增至新建立的子節點。 </li>
     <li>新增節點名稱作為要顯示新增之特殊字元的值。 </li>
     <li>按一下「儲存全部」。 </li>
     <li>重新整理文字編輯器\建立通訊UI，以便您檢視變更。<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>
