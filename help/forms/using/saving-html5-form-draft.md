---
title: 將HTML5表單儲存為草稿
seo-title: 將HTML5表單儲存為草稿
description: 將HTML5表單儲存為草稿，然後在稍後階段繼續填寫表單。
seo-description: 將HTML5表單儲存為草稿，然後在稍後階段繼續填寫表單。
uuid: 70cd5f6f-f125-470c-8cee-ee14d2127713
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 445e24af-cd1a-414d-bd01-9feb6631bbef
feature: 行動表單
exl-id: a9879445-d626-4279-8a95-a9009294b483
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 5%

---

# 將HTML5表單儲存為草稿{#saving-an-html-form-as-a-draft}

您可以將HTML5表單儲存為草稿，並在稍後階段繼續填寫表單。 Forms Portal可讓任何使用者儲存及還原HTML5表單。 若要啟用「另存為草稿」功能，請將下列設定新增至設定檔節點：

## 允許另存為草稿功能的自定義配置檔案{#custom-profile-to-allow-save-as-draft-feature}

AEM Forms可立即提供&#x200B;**另存為草稿**&#x200B;設定檔。 您可以使用「另存為草稿」設定檔來轉譯表單，以啟用HTML5表單的草稿功能。 您可以在[Forms Manager](/help/forms/using/introduction-managing-forms.md)中指定表單的HTML呈現設定檔。

若要為現有[自訂設定檔](/help/forms/using/custom-profile.md)啟用「另存為草稿」功能，請將下列屬性新增至自訂設定檔節點：

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
   <td><p>啟用另存為拔模特徵</p> <p>此設定檔。</p> </td>
  </tr>
  <tr>
   <td>mfAllowAttachments</td>
   <td>字串</td>
   <td>true</td>
   <td><p>允許上傳附件</p> <p>和此設定檔。</p> </td>
  </tr>
 </tbody>
</table>

## 草稿儲存和清單{#drafts-storage-and-listing}

啟用表單的「另存為草稿」功能後；保存表單時，表單會列在[草稿和提交元件](/help/forms/using/draft-submission-component.md)中。 您可以從草稿和提交元件擷取並開始填寫已儲存的表單。

若要啟用草稿和提交元件的表單清單，請將下列屬性新增至設定檔節點：

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
   <td>在提交後，啟用草稿和表單以列在<br /> Forms Portal Drafts &amp; Submissions元件中</td>
  </tr>
 </tbody>
</table>

依預設，AEM Forms會將與表單草稿和提交相關的使用者資料儲存在Publish執行個體的/content/forms/fp節點中。 如需詳細資訊，您可以新增自訂儲存提供者，請參閱[草稿和提交元件的自訂儲存](/help/forms/using/adding-custom-storage-provider-forms.md)。
