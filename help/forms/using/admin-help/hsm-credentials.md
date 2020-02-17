---
title: 管理HSM憑據
seo-title: 管理HSM憑據
description: 瞭解如何管理HSM憑證。
seo-description: 瞭解如何管理HSM憑證。
uuid: 30ddcd4a-f771-44d5-bdef-4826adcd0c44
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e5f17ba8-8aab-4449-811a-20ad33de1c6f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 管理HSM憑據 {#managing-hsm-credentials}

在「信任儲存管理」頁中，您可以管理硬體安全模組(HSM)憑據。 HSM是第三方PKCS#11設備，可用於安全地生成和儲存私鑰。 HSM在物理上保護對私有密鑰的訪問和使用。

需要客戶端軟體才能與HSM通信。 HSM用戶端軟體必須與AEM表單安裝在相同的電腦上並加以設定。

AEM表單數位簽章可使用儲存在HSM上的認證來套用伺服器端數位簽名。 請依照本節中的說明，為數位簽章將使用的每個HSM憑證建立別名。 別名包含HSM所需的所有參數。

>[!NOTE]
>
>變更HSM設定後，請重新啟動AEM表單伺服器。

## 在HSM設備聯機時為HSM憑證建立別名 {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-online}

1. 在管理控制台中，按一下「設定>信任商店管理> HSM憑證」，然後按一下「新增」。
1. 在「描述檔名稱」方塊中，輸入用來識別別名的字串。 此值用作某些數位簽章作業的屬性，例如「簽章欄位」作業。
1. 在「PKCS11庫」框中，鍵入伺服器上HSM客戶端庫的完全限定路徑。 例如， `c:\Program Files\LunaSA\cryptoki.dll`。 在群集環境中，此路徑對於群集中的所有伺服器必須相同。
1. 按一下「Test HSM Connectivity（測試HSM連接性）」。 如果AEM表單能夠連線至HSM裝置，會顯示訊息，指出HSM可用。 按一下「下一步」。
1. 使用Token名稱、Slot ID或Slot List Index來識別憑證儲存在HSM上的位置。

   * **** 代號名稱：與要使用的HSM分區的名稱（例如HSMPART1）相對應。
   * **** 插槽ID:插槽ID是類型為long的資料類型的插槽標識符。
   * **** 插槽清單索引：如果選擇「插槽清單索引」，請將「插槽資訊」設定為與插槽對應的整數。 這是一個基於0的索引，這意味著如果客戶機首先在HSMPART1分區中註冊，則HSMPART1將使用SlotListIndex值0。

1. 在「Token Pin」（標籤釘選）框中，鍵入訪問HSM密鑰所需的密碼，然後按一下「Next」（下一步）。
1. 在「憑據」框中，選擇憑據。 按一下「儲存」。

## 在HSM設備離線時為HSM憑證建立別名 {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-offline}

1. 在管理控制台中，按一下「設定>信任商店管理> HSM憑證」，然後按一下「新增」。
1. 在「描述檔名稱」方塊中，輸入用來識別別名的字串。 此值用作某些數位簽章作業的屬性，例如「簽章欄位」作業。
1. 在「PKCS11庫」框中，鍵入伺服器上HSM客戶端庫的完全限定路徑。 例如， `c:\Program Files\LunaSA\cryptoki.dll`。 在群集環境中，此路徑對於群集中的所有伺服器必須相同。
1. 選中「離線建立配置檔案」複選框。 按一下「下一步」。
1. 在「HSM設備」清單中，選擇儲存憑據的HSM設備的製造商。
1. 在「插槽類型」清單中，選擇「插槽ID」、「插槽索引」或「標籤名稱」，並在「插槽資訊」框中指定值。 AEM表格會使用這些設定來判斷憑證儲存在HSM上的位置。

   * **** 代號名稱：與分區名稱（例如HSMPART1）相對應。
   * **** 插槽ID:插槽ID是與插槽對應的整數，插槽又與分區相對應。 例如，首先在HSMPART1分區中註冊的客戶端（表單伺服器）。 這會將此客戶機的插槽1映射到HSMPART1分區。 由於HSMPART1是註冊的第一個分區，因此插槽ID為1，您可將插槽資訊設定為1。

      插槽ID是逐個客戶機設定的。 如果將第二台電腦註冊到不同的分區（例如，在同一HSM設備上的HSMPART2），則插槽1將與該客戶機的HSMPART2分區相關聯。

   * **** 插槽索引：如果選擇「插槽索引」，請將「插槽資訊」設定為與插槽對應的整數。 這是一個基於0的索引，這意味著如果客戶機首先向HSMPART1分區註冊，則插槽1將映射到此客戶機的HSMPART1。 由於HSMPART1是註冊的第一個分區，因此插槽索引為0。

1. 選擇下列選項之一併提供路徑：

   * **憑證**:（使用SHA1時不需要）按一下瀏覽並找到您使用的憑據的公鑰路徑。
   * **** 證書SHA1:（若使用實體憑證，則不需要）為您使用之憑證鍵入公開金鑰(.cer)檔案的SHA1值（指紋）。 請確定SHA1值中沒有使用空格。

1. 在「密碼」框中，鍵入訪問給定插槽資訊的HSM密鑰所需的密碼，然後按一下「保存」。

## 查看HSM憑據別名屬性 {#view-hsm-credential-alias-properties}

1. 在管理控制台中，按一下「設定>信任商店管理> HSM憑證」。
1. 按一下憑據別名的別名以查看屬性，然後按一下確定。

## 檢查HSM憑據的狀態 {#check-the-status-of-an-hsm-credential}

1. 在管理控制台中，按一下「設定>信任商店管理> HSM憑證」。
1. 按一下要檢查的憑據旁的複選框，然後按一下「檢查狀態」。

「狀態」列反映憑據的當前狀態。 如果失敗，「狀態」欄會顯示紅色X。 將滑鼠指標暫留在X上，以顯示包含失敗原因的工具提示。

## 更新HSM憑據別名屬性 {#update-hsm-credential-alias-properties}

1. 在管理控制台中，按一下「設定>信任商店管理> HSM憑證」。
1. 按一下憑據別名的別名。
1. 按一下「更新憑證」，並視需要更新設定。

## 重置所有HSM連接 {#reset-all-hsm-connections}

在表單伺服器與HSM設備之間的網路會話中斷後，重置到HSM設備的開啟連接。 例如，網路中斷或HSM設備離線進行軟體更新可能會造成中斷。 中斷後，現有的連線已過時，對這些連線的任何簽署要求都會失敗。 使用「重置所有HSM連接」選項可清除舊連接。

1. 在管理控制台中，按一下「設定>信任商店管理> HSM憑證」。
1. 按一下「重置所有HSM連接」。

## 刪除HSM憑據別名 {#delete-an-hsm-credential-alias}

1. 在管理控制台中，按一下「設定>信任商店管理> HSM憑證」。
1. 選擇要刪除的HSM憑據的複選框，按一下刪除，然後按一下確定。

## 配置遠程HSM支援 {#configure-remote-hsm-support}

AEM表單使用以Web services為基礎的IPC/RPC機制。 此機制可讓AEM表單使用安裝在遠端電腦上的HSM。 要使用此功能，請在安裝HSM的遠程電腦上安裝Web服務。 如需詳 [細資訊，請參閱在Windows 64位元平台上使用Sun JDK設定AEM表單ES](https://kb2.adobe.com/cps/808/cpsid_80835.html)的HSM支援。

此機制不支援線上建立HSM配置檔案或狀態檢查。 但是，建立HSM配置檔案和執行狀態檢查有兩種方法：

* 將AEM表單用戶端憑證傳遞給簽署者的憑證，以建立此憑證。 請依照在Windows 64位元平 [台上使用Sun JDK，設定AEM Forms ES的HSM支援中的步驟進行](https://kb2.adobe.com/cps/808/cpsid_80835.html)。 Web服務位置作為憑據屬性傳入。 也支援使用憑證碼或憑證SHA-1十六進位建立的離線HSM設定檔。 不過，如果您已從舊版AEM表單升級至AEM表單，請變更用戶端，因為憑證包含憑證和網站服務資訊。
* Web服務位置是在簽名服務的管理控制台中指定的。 (請參閱 [簽名服務設定](/help/forms/using/admin-help/configure-service-settings.md#signature-service-settings)。)在此，客戶機僅在信任儲存中攜帶HSM配置檔案的別名。 即使您已從舊版AEM表單升級至AEM表單，您也可以順暢地使用此選項，不需要任何用戶端變更。 此選項不支援使用證書SHA-1的HSM配置檔案。

