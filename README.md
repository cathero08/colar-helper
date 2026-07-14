# 色弱救星（Color Helper）

手機優先的色彩辨識與色覺輔助工具。使用者可以用手機相機取色，查看中文色名、HEX/RGB/HSL、ISCC-NBS 相近色、色盲模擬、A/B 色差比較與文字對比建議。

這是一個純前端靜態網站，可直接部署到 GitHub Pages，並支援 PWA：可安裝到手機主畫面、以獨立 App 形式開啟、離線使用。

## 功能

- 手機相機即時取色
- 點選畫面任意位置取色
- 凍結畫面後慢慢取樣
- 開啟 / 關閉相機，方便省電與保護隱私
- 手動選色備援
- 顯示 HEX、RGB、HSL 與明暗判斷
- 使用 ISCC-NBS Level 3 267 類色名做中文色名判定
- 使用 CIE Lab 與 CIEDE2000 / Delta E 2000 找最接近色名
- 顯示前 3 名相近色與色差值
- 最近 8 筆取色歷史
- A/B 色差比較
- Protanopia、Deuteranopia、Tritanopia 色覺模擬
- 色覺混淆提示
- WCAG 黑字 / 白字對比建議

## 使用方式

1. 用手機開啟網站。
2. 按下「啟動相機」並允許相機權限。
3. 把要辨識的顏色放在畫面中央，或直接點選畫面上的顏色位置。
4. 查看目前顏色名稱、色碼、相近色排名與輔助建議。
5. 若畫面晃動，可按「凍結畫面」後再點選取色。

## 部署到 GitHub Pages

1. 將此專案推到 GitHub repository。
2. 到 repository 的 `Settings > Pages`。
3. Source 選擇要部署的 branch，例如 `master` 或 `main`。
4. Folder 選擇 `/root`。
5. 儲存後等待 GitHub Pages 產生網址。

相機 API 需要 HTTPS 才能使用，GitHub Pages 預設提供 HTTPS。

## 安裝為 App（PWA）

- **Android（Chrome）**：開啟網站後，點選網址列旁的「安裝」提示，或選單中的「加入主畫面 / 安裝應用程式」。
- **iOS（Safari）**：開啟網站後，點「分享」按鈕 → 「加入主畫面」。

安裝後會以獨立 App 形式全螢幕開啟，且支援離線使用（相機取色所有運算都在本機進行，不需要網路）。

更新機制：App 開啟時若有網路，會自動抓取最新版頁面；若修改了 `index.html` 等被快取的檔案，記得同步調高 `sw.js` 裡的 `CACHE_VERSION`，離線快取才會更新。

## 技術說明

顏色命名流程：

```text
相機 / 手動選色
-> RGB
-> CIE Lab
-> 與 ISCC-NBS 267 色票計算 CIEDE2000
-> 取 Delta E 最小的中文色名
```

此工具使用的 ISCC-NBS 色票是 Level 3 的 267 個命名色塊。每個色名代表一個色彩範圍，不是單一絕對顏色，因此畫面會顯示 Delta E 數值作為接近程度參考。

## 隱私

相機畫面只在使用者瀏覽器本機處理，不會上傳到任何伺服器。此專案沒有後端，也沒有資料庫。

## 限制

- 手機相機會受環境光、白平衡、螢幕亮度與陰影影響。
- ISCC-NBS 色名判定是以 sRGB 代表色與 CIEDE2000 近似比對，不等於專業儀器量測。
- 色盲模擬是前端矩陣近似，適合輔助理解，不應視為醫療診斷。

## 資料來源

- ISCC-NBS Level 3 color centroids: <https://people.csail.mit.edu/jaffer/Color/NBS-ISCC-rgb.txt>
- ISCC-NBS 色名系統：Inter-Society Color Council 與 National Bureau of Standards 的色名分類方法。
