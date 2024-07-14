---
title: 觀察資料夾的備份策略
description: 本檔案說明不同的備份與復原案例如何影響watched資料夾、這些案例的限制與結果，以及如何將資料遺失降至最低。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0d36160a-29fa-4cc4-a0ff-fc681d3e040e
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '1080'
ht-degree: 0%

---

# 觀察資料夾的備份策略 {#backup-strategies-for-watched-folders}

本內容說明不同的備份與復原案例如何影響watched資料夾、這些案例的限制與結果，以及如何將資料遺失降至最低。

*Watched資料夾*&#x200B;是檔案系統型應用程式，可叫用已設定的服務作業，這些作業會在watched資料夾階層的下列其中一個資料夾中操作檔案：

* 輸入
* 測試
* 輸出
* 失敗
* 保留

使用者或使用者端應用程式會先將檔案或資料夾拖放到輸入資料夾中。 然後，服務作業會將檔案移至階段資料夾進行處理。 服務執行指定的操作後，會將修改的檔案儲存在輸出資料夾中。 成功處理的來源檔案會移至保留資料夾，而失敗的處理檔案則會移至失敗資料夾。 啟用watched資料夾的`Preserve On Failure`屬性時，失敗的已處理來源檔案會移至保留資料夾。 （請參閱[設定watched資料夾端點](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#configuring-watched-folder-endpoints)。）

您可以透過備份檔案系統來備份watched資料夾。

>[!NOTE]
>
>此備份與資料庫或檔案儲存的備份與復原程式無關。

## 觀察資料夾的運作方式 {#how-watched-folders-work}

此內容說明watched資料夾檔案操作程式。 在制定復原計畫之前，請務必瞭解此程式。 在此範例中，已啟用watched資料夾的`Preserve On Failure`屬性。 系統會依檔案到達的順序來處理這些檔案。

下表說明整個處理過程中五個範例檔案(file1、file2、file3、file4、file5)的檔案操作。 在表格中，x軸代表時間，例如Time 1或T1，而y軸代表在watched資料夾階層中的資料夾，例如Input。

<table>
 <thead>
  <tr>
   <th><p>資料夾</p></th>
   <th><p>T1</p></th>
   <th><p>T2</p></th>
   <th><p>T3</p></th>
   <th><p>T4</p></th>
   <th><p>T5</p></th>
   <th><p>T6</p></th>
   <th><p>T7</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>輸入</p></td>
   <td><p>檔案1，檔案2，檔案3，檔案4</p></td>
   <td><p>檔案2，檔案3，檔案4</p></td>
   <td><p>檔案3，檔案4</p></td>
   <td><p>檔案4</p></td>
   <td><p>空白</p></td>
   <td><p>檔案5</p></td>
   <td><p>空白</p></td>
  </tr>
  <tr>
   <td><p>測試</p></td>
   <td><p>空白</p></td>
   <td><p>檔案1</p></td>
   <td><p>file2</p></td>
   <td><p>檔案3</p></td>
   <td><p>檔案4</p></td>
   <td><p>空白</p></td>
   <td><p>檔案5</p></td>
  </tr>
  <tr>
   <td><p>輸出</p></td>
   <td><p>空白</p></td>
   <td><p>空白</p></td>
   <td><p>file1_out</p></td>
   <td><p>file1_out， file2_out</p></td>
   <td><p>file1_out， file2_out</p></td>
   <td><p>file1_out， file2_out， file4_out</p></td>
   <td><p>file1_out， file2_out， file4_out</p></td>
  </tr>
  <tr>
   <td><p>失敗</p></td>
   <td><p>空白</p></td>
   <td><p>空白</p></td>
   <td><p>空白</p></td>
   <td><p>空白</p></td>
   <td><p>file3_fail， file3 </p></td>
   <td><p>file3_fail， file3 </p></td>
   <td><p>file3_fail， file3 </p></td>
  </tr>
  <tr>
   <td><p>保留</p></td>
   <td><p>空白</p></td>
   <td><p>空白</p></td>
   <td><p>檔案1 </p></td>
   <td><p>檔案1，檔案2 </p></td>
   <td><p>檔案1，檔案2 </p></td>
   <td><p>檔案1，檔案2，檔案4 </p></td>
   <td><p>檔案1，檔案2，檔案4 </p></td>
  </tr>
 </tbody>
</table>

下列文字說明每次的檔案操作：

**T1：**&#x200B;四個範例檔案被放置在輸入資料夾中。

**T2：**&#x200B;服務作業會將file1移到stage資料夾中進行操作。

**T3：**&#x200B;服務作業會將file2移到Stage資料夾中進行操作。 它會將file1的結果放在輸出資料夾中，並將file1移動到保留資料夾。

**T4：**&#x200B;服務作業會將file3置於stage資料夾中以進行操作。 它會將file2的結果放置在輸出資料夾中，並將file2放置在保留資料夾中。

**T5：**&#x200B;服務作業會將file4置於Stage資料夾中以進行操作。 對file3的操作失敗，服務作業會將其置於失敗資料夾中。

**T6：**&#x200B;服務作業將file5放在輸入資料夾中。 它會將file4的結果放置在輸出資料夾中，將file4放置在保留資料夾中。

**T7：**&#x200B;服務作業會將file5放置在Stage資料夾中以進行操作。

## 備份watched資料夾 {#backing-up-watched-folders}

建議您將整個watched資料夾檔案系統備份到另一個檔案系統。

## 還原watched資料夾 {#restoring-watched-folders}

本節說明如何還原watched資料夾。 觀察資料夾通常會叫用在一分鐘內完成的短期程式。 在這種情況下，以每小時執行的備份還原watched資料夾無法防止資料遺失。

例如，如果在T1時間進行備份，而伺服器在T7失敗，則已處理file1、file2、file3和file4。 以T1取得的備份還原watched資料夾無法防止資料遺失。

如果進行較新的備份，您可以還原檔案。 還原檔案時，請考量目前檔案所在的監看資料夾階層資料夾：

**階段：**&#x200B;在還原watched資料夾後，會再次處理此資料夾中的檔案。

**輸入：**&#x200B;在還原watched資料夾後，會再次處理此資料夾中的檔案。

**結果：**&#x200B;未處理此資料夾中的檔案。

**輸出：**&#x200B;此資料夾中的檔案未處理。

**保留：**&#x200B;未處理此資料夾中的檔案。

## 將資料遺失減至最低的策略 {#strategies-to-minimize-data-loss}

還原watched資料夾時，下列策略可最小化輸出和輸入資料夾資料遺失：

* 經常備份輸出和失敗資料夾（例如每小時），以避免遺失結果和失敗檔案。
* 將輸入檔案備份至watched資料夾以外的資料夾。 這可確保復原後的檔案可用性，以防您在輸出或失敗資料夾中找不到檔案。 確保您的檔案命名配置一致。

  例如，如果您要以&#x200B;`%F.`*副檔名*&#x200B;儲存輸出，輸出檔案的名稱將與輸入檔案相同。 這可協助您決定要處理的輸入檔案以及必須重新提交哪些輸入檔案。 如果在結果資料夾中只看到file1_out檔案，而不是file2_out、file3_out和file4_out，則必須重新提交file2、file3和file4。

* 如果可用的watched資料夾備份時間早於處理工作所需的時間，您應該允許系統建立watched資料夾，並自動將檔案放入輸入資料夾中。
* 如果最新的可用備份不夠新，則備份時間會少於處理檔案所花的時間，而且會還原watched資料夾，因此會在下列不同階段之一中操作檔案：

   * 輸入資料夾中的&#x200B;**階段1：**
   * **階段2：**&#x200B;已複製到階段資料夾，但尚未叫用處理序
   * **階段3：**&#x200B;已複製到階段資料夾，而且已叫用處理序
   * **階段4：**&#x200B;操作進行中
   * **階段5：**&#x200B;傳回結果

  如果檔案位於「階段1」中，則會加以操作。 如果檔案在「舞台2」或「舞台3」中，請將它們放置在輸入資料夾中，以便再次進行操作。

  >[!NOTE]
  >
  >如果檔案操作發生多次，可避免資料遺失，但結果可能會重複。

## 結論 {#conclusion}

由於Watched資料夾的動態且不斷變更的性質，應使用在一天內備份的檔案來還原Watched資料夾。 最佳實務建議備份結果、將輸入資料夾儲存在伺服器上，以及追蹤輸入檔案，以便在發生失敗時可以重新提交工作。
