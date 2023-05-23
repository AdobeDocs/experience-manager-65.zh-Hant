---
title: 在HTML5窗體中使用Scribble簽名
seo-title: Using Scribble Signature in HTML5 forms
description: HTML5表格在觸摸設備上越來越被使用，一個常見要求是支援簽名。 在移動設備上簽名文檔正成為在移動設備上簽名表單的一種接受方式。
seo-description: HTML5 forms are increasingly used on touch devices, and one common requirement is to support signatures. Signing documents on mobile devices is becoming an accepted way of signing forms on mobile devices.
uuid: 163dd55a-971a-4dd4-93a7-a14e80184d9b
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
discoiquuid: ecd7f538-9c24-48e7-8450-596851e99cff
docset: aem65
feature: Designer
exl-id: 2025182f-195b-40d0-aee7-67669f55b964
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# 在HTML5窗體中使用Scribble簽名{#using-scribble-signature-in-html-forms}

HTML5表格在觸摸設備上越來越多地使用，一個常見要求是支援簽名。 划線（用手寫筆或手指書寫）正成為移動設備上簽名表格的一種接受方式。 HTML5表單和Forms設計師現在啟用了在表單上使用手寫簽名欄位的選項。 在瀏覽器中呈現表單時，可以使用手寫筆、滑鼠或觸摸在這些欄位上登錄。

## 如何使用Scribble簽名欄位設計表單 {#how-to-design-a-form-using-scribble-signature-field}

1. 在Forms設計器中開啟窗體。
1. 拖放頁面上的「簽名指令碼」欄位。

   ![設計器 — 指令碼](assets/designer_scribble.png)

   >[!NOTE]
   >
   >在「Forms設計器」中選擇的欄位的Dimension將在呈現該欄位時反映。 但是，渲染的簽名框的尺寸是根據欄位的長寬比計算的，而不是根據Forms設計器中指定的尺寸計算的。

1. 配置「簽名指令碼」欄位。

   預設情況下，「簽名指令碼」欄位將地理位置資訊標籤為在iPad的簽名過程中必需的（對於其他設備是可選的）。 通過更改 `geoLocMandatoryOnIpad` 屬性。 此屬性作為Signature Scribble Field中的額外內容公開。 修改步驟如下：

   1. 在表單上，選擇「簽名指令碼」欄位。
   1. 選擇 **XML源** 頁籤。

      >[!NOTE]
      >
      >要開啟「XML源」頁籤，請按一下 **視圖** > **XML源**。

   1. 查找 `<ui>` 標籤 `<field>` 標籤並修改原始碼，使其與以下內容類似：

      ```xml
      <extras name="x-scribble-add-on">
      <boolean name="geoLocMandatoryOnIpad">0</boolean>
      </extras>
      ```

   1. 選擇 **設計視圖** 頁籤。 在確認框中，按一下 **是**。
   1. 保存窗體。

1. 在支援的設備/案頭瀏覽器上呈現表單。

## 與Scribble簽名介面 {#interfacing-with-the-scribble-signatures}

### 簽名 {#signing}

將「簽名指令碼」欄位添加到表單並呈現後，按一下或點擊該欄位將開啟一個對話框。 用戶可以使用滑鼠、手指或手寫筆在由點線矩形指定的繪圖區中塗抹簽名。

![地理位置](assets/geolocation.png)

**答：** 畫筆 **B** 橡皮擦 **C.** 地理位置 **D** 地理位置資訊

### 地理標籤 {#geo-tagging}

在建立指令碼時按一下地理位置表徵圖會導致地理位置和時間資訊嵌入到欄位中。

>[!NOTE]
在iPad，預設情況下，必須嵌入地理位置資訊。

在iPad上，預設情況下不顯示地理位置表徵圖，並且當您按一下 **確定**。

對於iPad，可以通過修改 `geoLocManadatoryOnIpad` 參數 `0`，在欄位的init參數中。

* 當地理位置資訊是強制性的時候，向用戶呈現縮小的繪製區域。 當用戶按一下時添加地理位置文本 **確定** 表徵圖。
* 在其它情況下，向用戶呈現可完全拉長的區域。 如果用戶選擇嵌入地理位置資訊，則會調整此區域的大小以適應地理位置文本。

### 清除簽名 {#clearing-a-signature}

使用此功能時，用戶可以按一下 **橡皮擦** 表徵圖以清除該欄位，然後重新開始。 如果添加了地理位置資訊，則也會清除該資訊。

### 保存簽名 {#saving-a-signature}

按一下 **確定** 表徵圖將指令碼另存為欄位中的影像。 可以將影像和值提交到伺服器以進行進一步處理。 用戶按一下後 **確定**，「Scribble filed（塗寫檔案）」鎖定。 無法使用指令碼構件再次編輯簽名。

點擊或按一下「Scribble（指令碼）」欄位，將以只讀模式開啟對話框。

![3](assets/3.png)

### 選擇筆大小 {#selecting-pen-size}

按一下 **畫筆** 表徵圖，顯示可用筆大小的清單。 按一下或點擊筆大小以使用相應的筆。

### 從表單中刪除簽名 {#delete-signatures-from-the-form}

要從表單中刪除簽名：

* （移動設備）長時間按簽名欄位，在確認對話框上，點擊 **是**。
* （案頭）懸停在簽名欄位上，按一下 **取消** 表徵圖，在確認對話框上，按一下 **是**。
