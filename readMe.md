# 藥品國際應用

## 應用概述
由於民眾通常不太熟悉藥品知識，很需要發展應用系統，輔助民眾居家用藥。 FHIR 當中用藥相關的 resources 包含Medication 藥品、MedicationRequest 藥物處方、MedicationDispense 配藥結果、MedicationAdministration 實際用藥紀錄、MedicationKnowledge 藥物相關的知識等。 
用藥所需資訊眾多，可能用到的藥品種類繁多，居家用藥紀錄或可以基於 MedicationRequest 藥物處方，進行用藥提醒，再以 MedicationAdministration 為主，紀錄服藥的時間、劑量、路徑（例如口服、注射）等資訊。
MedicationRequest 藥物處方、MedicationDispense 配藥結果，以及其參考的資訊是由醫療端產生，可記錄在 FHIR EMR 伺服器，並授權民眾端調閱。若民眾對於用藥有不清楚狀況，或相關問題狀況，可再將其 EMR  及 PHR 資訊提供給其家庭醫師、個管師、甚至 AI 系統，透過 FHIR commmunicatiuon, 進行線上資訊。
上述情境，醫療服務人員及系統並不限於在同一個國家. 另外, 若可跨國收集 PHR 端民眾用藥的資訊, 對於其後續分析及精確用藥管理非常有幫助. 但這不僅需基於 FHIR 記錄用藥相關資訊,也需要有國際統一的編碼!
關於 FHIR 用藥，許多國家公告的 implementation guide, 但其 medication、route、timing 的代碼不一. 這或可進一步建置跨國統一的規範, 也可從民眾端開始, 建置統一的代碼, 再基於醫資標準 code  system，發展支援各國語言及當地藥品相關資訊。如下:



### 各國藥品名稱對應
- 基於 RxNorm
- Task 1. 整理 範例 json 之各國語言對照表 



## Task 
1. 整理 範例 json 之各國語言對照表 
2. 癌病用藥，chatGPT 回應結果，不確定其內容( RxNorm 碼及藥品名)是否正確
https://chatgpt.com/share/675a570b-03a4-8006-91b1-57feacd6f695
3. 請提供 RxNorm codesystem、藥品代碼:1721560、英文藥物名稱：Osimertinib 之 JSON 範例，請分別提供英文、中文、印尼文之 JSON 範例，不確定其各國語言翻譯是否正確，需進一步確認
4. chatGPT 產生 RxNorm API  debug
https://chatgpt.com/share/675a5c6c-d794-8006-86ce-af2f6b9da9e7




## 民眾居家常見的給藥途徑有哪些?
- https://chatgpt.com/share/675a5fe1-6588-8006-9ff3-09a86031e9ac
- 這也需各國語言對應

## 進一步考量事項
參考 FHIR MedicationRequest 及 MedicationAdministration，民眾居家用藥過程， PHR 端應用軟體應紀錄及呈現那些資訊
若藥品使用國際統一之 RxNorm 碼，但同一種藥品可能在不同國家製造、包裝、及印製藥品仿單及說明文件。藥品銷售、收費、保險給付方式也可能有差異。同一種藥品在全球各地應用還有哪些差異? 若要基於 FHIR ，發展一全球支援之用藥資訊系統，有哪些建議及處理事項?
ChatGPT 說：
ChatGPT
全球用藥應用的差異
即使使用國際統一的 RxNorm 代碼，藥物在全球各地的應用仍可能因以下原因產生差異：

製造與包裝

不同國家的藥廠可能會生產相同活性成分但不同劑型（例如片劑、膠囊）或濃度。
包裝設計需符合當地法規，可能包含本地語言的標籤和用法說明。
仿單與說明文件

仿單需依據當地的藥品監管規定，描述藥物用途、禁忌症、副作用等資訊。
可能因文化差異而有不同的表述，甚至針對特定國家或族群的數據補充。
藥物定價與保險給付

每個國家的藥品價格與支付方式不同，與當地的醫療政策、保險體系、和藥品稅費有關。
例如，有些國家提供政府補助或全額支付，而另一些國家可能採用部分自費模式。
藥物適應症與用法

根據不同地區的臨床試驗結果與藥物監管機構的批準，適應症可能有所差異。
劑量建議可能因當地族群特性（如代謝差異）或醫療習慣而異。
藥品可及性與分銷

某些藥物可能僅在特定國家獲得批准或銷售，甚至受到出口限制。
藥物的分銷途徑和供應鏈在不同地區可能有顯著差異。
基於 FHIR 的全球支援用藥資訊系統建議
要開發一個支持全球化的用藥資訊系統，需考慮以下建議與處理事項：

1. 多語言與多文化支持
使用 FHIR 的多語言功能（extension 或 translation）以記錄藥物資訊（如說明文件、標籤）。
提供基於國家或語言的本地化 UI，確保資訊清晰易懂。
2. 國家特定規範與法規
定義每個國家的藥物資料規範，例如使用 MedicationKnowledge 中的 regulatory 和 cost。
引入適應症、禁忌症等規範，讓系統動態適應不同國家的規定。
3. 藥物流通與供應鏈管理
使用 MedicationDispense 和 MedicationRequest 追踪用藥分發與使用情況。
建立與全球供應鏈系統（如 GS1 標準）的接口，以同步製造和物流資訊。
4. 藥物價格與支付模式
在 MedicationKnowledge 中記錄多國藥品價格（cost 模組）與支付模式。
與當地的醫療支付或保險系統整合，例如記錄保險覆蓋範圍和支付比例。
5. 藥品辨識與標準化
結合 RxNorm、ATC（Anatomical Therapeutic Chemical Classification）、以及其他標準代碼系統，確保全球識別一致。
使用 FHIR CodeSystem 和 ValueSet 建立不同標準之間的對應關係。
6. 法律合規與隱私保護
遵守各國的隱私保護法規（如 GDPR、HIPAA），確保病患用藥資訊安全。
透過 FHIR 的安全性模組（如 OAuth 2.0 和 SMART on FHIR）實現安全訪問。
7. 資料可擴展性
支持地區特有的擴展屬性（extension），以容納不同國家的獨特需求，例如特定警示資訊。
使用 FHIR 的 StructureDefinition 定義靈活的資料結構。
8. 臨床決策支援
與 CDSS（臨床決策支持系統）集成，為醫療人員提供動態建議，根據當地標準與患者情況量身定制治療方案。
9. 持續更新與監管機構接口
實現與監管機構（如 FDA、EMA、PMDA）的自動化數據同步。
確保藥物資訊（如新適應症、副作用）及時更新。
總結
基於 FHIR 開發全球用藥資訊系統，需要整合標準化與本地化需求，並確保數據的準確性、安全性和可用性。這樣的系統可以促進全球藥物資訊共享與協作，改善患者的用藥安全與治療效果。




你說：
若病人(如癌病病人) 要跨國就醫治療，則病人或其照護者使用之 PHR APP 可能介皆不同國家之 FHIR EMR 系統，取得藥物處方。但不同國家之 FHIR EMR 系統規格可能有差異，在民眾 PHR APP 要如何處裡?
ChatGPT 說：
ChatGPT
當病人（例如癌症患者）跨國就醫時，其個人健康記錄（PHR）應用程式（APP）需要處理不同國家 FHIR EMR 系統規格的差異。以下是處理這一挑戰的策略：

1. 採用標準化的核心模型
解決方案：
FHIR 基礎結構：PHR APP 應設計為基於 FHIR 的通用數據結構（如 Medication、MedicationRequest 等），以適應各國的不同擴展和實現方式。
國際標準支持：使用 FHIR 定義的 Profile 和 Extension，支持特定國家或地區的特殊需求，同時保留核心標準。
處理：
例如，某些國家可能會在 MedicationRequest 中包含額外的數據字段（如費用分類），PHR APP 應能夠通過 FHIR 的 StructureDefinition 處理這些擴展。
2. 多語言與本地化支持
解決方案：
語言切換：PHR APP 應支持多語言顯示（如英文、中文、日文等），確保患者和護理人員能理解資訊。
本地化規範匹配：根據不同國家的用藥法規，自動適配當地的藥物說明與適應症。
處理：
藥物名稱可通過 RxNorm 或 ATC 編碼獲取國際化的標籤和翻譯。
3. 跨國標準映射
解決方案：
CodeSystem 映射：建立 RxNorm、ATC、以及當地藥品編碼系統之間的對應關係，讓不同國家的藥物資訊能互相轉換。
ValueSet 管理：對於處方的劑量單位、頻率等，使用標準化的 ValueSet，以處理不同地區的格式。
處理：
例如，一個國家的處方頻率為 "BID"（每日兩次），在其他國家可能表示為 "Twice Daily"，需進行自動轉換。
4. 動態適配與擴展性
解決方案：
模組化設計：PHR APP 應動態讀取不同國家的 FHIR CapabilityStatement，以了解每個系統支持的資源和操作。
擴展支持：PHR APP 可透過擴展字段來記錄額外的本地需求，而不影響核心數據。
處理：
比如，如果某 FHIR 系統在 Medication 資源中引入額外字段來描述藥物包裝類型，PHR APP 可通過擴展動態支持。
5. 資料完整性與安全性
解決方案：
SMART on FHIR：採用安全的身份驗證和授權框架，確保患者能安全地訪問不同國家的 FHIR EMR 系統。
資料同步與備份：設計機制以便於本地存儲與雲端同步，確保數據完整性與連續性。
處理：
支持患者在網絡不穩定或訪問受限時，離線訪問用藥記錄，並在網絡恢復後同步。
6. 互操作性與數據轉換
解決方案：
數據標準化服務：集成一個數據中介服務，實時轉換不同地區的 FHIR 規範到通用格式。
FHIR Mapping Tool：使用工具如 FHIR Mapping Language，自動進行資源映射與轉換。
處理：
假如某國家使用非標準的劑量單位（如 "mg/kg"），中介服務可以將其轉換為國際標準單位（如 "mg"）。
7. 臨床決策支持
解決方案：
CDSS（臨床決策支持系統）集成：在患者查詢用藥時，提供基於國家或地區的用藥規範與建議。
提醒與警示：提示患者藥物禁忌症或可能的相互作用，特別是跨國用藥可能帶來的風險。
總結
在設計全球支持的 PHR APP 時，應將國際化、擴展性、標準化和數據安全性作為核心原則。同時，利用 FHIR 的標準資源與擴展功能來應對不同國家的規格差異，並確保患者能無縫訪問、管理和理解其用藥資訊。








