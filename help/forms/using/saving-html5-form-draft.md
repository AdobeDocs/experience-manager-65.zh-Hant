---
title: 將HTML5表格儲存為草稿
seo-title: 將HTML5表格儲存為草稿
description: 將HTML5表格儲存為草稿，並在稍後階段繼續填寫表格。
seo-description: 將HTML5表格儲存為草稿，並在稍後階段繼續填寫表格。
uuid: 70cd5f6f-f125-470c-8cee-ee14d2127713
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 445e24af-cd1a-414d-bd01-9feb6631bbef
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 5%

---


# 將HTML5表單儲存為草稿{#saving-an-html-form-as-a-draft}

您可以將HTML5表格儲存為草稿，然後在稍後階段繼續填寫表格。 Forms入口網站可讓任何使用者儲存和還原HTML5表單。 要啟用「另存為草稿」功能，請將以下配置添加到配置檔案節點：

## 「自訂描述檔」可允許「另存為草稿」功能{#custom-profile-to-allow-save-as-draft-feature}

現成可用的AEM Forms提供&#x200B;**另存為草稿**&#x200B;描述檔。 您可以使用「另存為草稿」描述檔來轉換表單，以啟用HTML5表單的草稿功能。 您可以在[Forms管理員](/help/forms/using/introduction-managing-forms.md)中指定表單的HTML演算描述檔。

要為現有的[自定義配置檔案](/help/forms/using/custom-profile.md)啟用「另存為草稿」功能，請將以下屬性添加到自定義配置檔案節點：

<table>
 <tbody>
  <tr>
   <td><strong>屬性名稱</strong></td>
   <td><strong>類型</strong></td>
   <td><strong>值</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>mfAllowFPDraft</td>
   <td>字串</td>
   <td>true</td>
   <td><p>啟用另存為繪製特徵</p> <p>的URL。</p> </td>
  </tr>
  <tr>
   <td>mfAllowAttachments</td>
   <td>字串</td>
   <td>true</td>
   <td><p>允許上傳附件</p> <p>和此個人檔案。</p> </td>
  </tr>
 </tbody>
</table>

## 草稿儲存和清單{#drafts-storage-and-listing}

啟用表單的「另存為草稿」功能後；保存表單時，它會列在[草稿和提交元件](/help/forms/using/draft-submission-component.md)中。 您可以檢索並開始填寫「草稿和提交」元件中保存的表單。

要為「草稿」和「提交」元件啟用表單清單，請向配置檔案節點添加以下屬性：

<table>
 <tbody>
  <tr>
   <td><strong>屬性名稱</strong></td>
   <td><strong>類型</strong></td>
   <td><strong>值</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>fp.enablePortalSubmit</td>
   <td>字串</td>
   <td>true</td>
   <td>使草稿和表格在提交後列在<br />Forms門戶Portal Drafts &amp; Submissions元件中</td>
  </tr>
 </tbody>
</table>

依預設，AEM Forms會將與表單草稿和提交相關的使用者資料儲存在「發佈」例項的/content/forms/fp節點中。 您可以新增自訂儲存提供者，以取得詳細資訊，請參閱[草稿和提交的自訂儲存元件](/help/forms/using/adding-custom-storage-provider-forms.md)。
