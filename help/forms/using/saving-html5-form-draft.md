---
title: 將HTML5窗體另存為草稿
seo-title: Saving an HTML5 form as a draft
description: 將HTML5窗體另存為草稿，並在稍後階段繼續填寫窗體。
seo-description: Save an HTML5 form as a draft and resume filling the form at a later stage.
uuid: 70cd5f6f-f125-470c-8cee-ee14d2127713
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 445e24af-cd1a-414d-bd01-9feb6631bbef
feature: Mobile Forms
exl-id: a9879445-d626-4279-8a95-a9009294b483
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 5%

---

# 將HTML5窗體另存為草稿 {#saving-an-html-form-as-a-draft}

您可以將HTML5表單另存為草稿，然後在稍後階段繼續填充表單。 Forms門戶允許任何用戶保存和恢復HTML5窗體。 要啟用「另存為草稿」功能，請將以下配置添加到配置檔案節點：

## 允許「另存為拔模」特徵的自定義配置檔案 {#custom-profile-to-allow-save-as-draft-feature}

現在，AEM Forms **另存為草稿** 檔案。 可以使用「另存為拔模」(Save as Draft)配置檔案來渲染表單，以啟用HTML5表單的拔模功能。 可以為中的表單指定HTML呈現配置檔案 [Forms經理](/help/forms/using/introduction-managing-forms.md)。

為現有檔案啟用「另存為草稿」功能 [自定義配置檔案](/help/forms/using/custom-profile.md)，將以下屬性添加到自定義配置檔案節點：

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
   <td><p>啟用另存為拔模特徵</p> <p>的下一頁。</p> </td>
  </tr>
  <tr>
   <td>mfAllow附件</td>
   <td>字串</td>
   <td>true</td>
   <td><p>允許上載附件</p> <p>和此配置檔案。</p> </td>
  </tr>
 </tbody>
</table>

## 草稿儲存和清單 {#drafts-storage-and-listing}

為表單啟用「另存為草稿」功能後；保存表單時，它列在 [草稿和提交元件](/help/forms/using/draft-submission-component.md)。 可以從「草稿」和「提交」元件中檢索並開始填充已保存的表單。

要為「草稿」和「提交」元件啟用表單清單，請將以下屬性添加到配置檔案節點：

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
   <td>啟用草稿和表單以在中列出<br /> Forms門戶提交後草稿和提交元件</td>
  </tr>
 </tbody>
</table>

預設情況下，AEM Forms將與表單草稿和提交相關聯的用戶資料儲存在發佈實例的/content/forms/fp節點中。 您可以添加自定義儲存提供程式，有關詳細資訊，請參閱 [「草稿和提交」元件的自定義儲存](/help/forms/using/adding-custom-storage-provider-forms.md)。
