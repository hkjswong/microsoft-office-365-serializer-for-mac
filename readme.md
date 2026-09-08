**前言**

隨著 **Office 2016 / Office 2019** 逐漸停止對新版 macOS 的支援，不少 MacBook 使用者開始轉向安裝較新的 **Microsoft Office 365**。

不過，在安裝 Office 365 的過程中，我之前一直遇到一個問題：

> **安裝完成後，Office 365 始終無法正常啟用。**

一開始我也嘗試排查過很多可能的原因，例如：

- 是否因為 **macOS 系統版本過高**？
- 是否下載到了不正確的 `vl_serializer.pkg`？
- 是否需要重新安裝 Office？
- 是否是授權元件沒有正確載入？

直到最近，我才找到真正影響啟用的核心問題。

## 解決方法

安裝完 `vl_serializer.pkg` 後，打開 **App Cleaner & Uninstall**，然後按照以下步驟操作：

1. 進入 **啟動程序（Startup Programs）**。
2. 找到以下服務：

   `com.microsoft.office.licensingV2.helper`

   ![image]([https://github.com/hkjswong/microsoft-office-365-serializer-for-mac/blob/main/%E8%9E%A2%E5%B9%95%E6%88%AA%E5%9C%96%202026-09-08%20%E4%B8%8B%E5%8D%882.05.00.png])


4. 將這項服務設定為 **啟用**。
5. 啟用後，重新打開 Office 365，檢查是否已經正常啟用。

如果完成以上操作後，Office 365 仍然無法啟用，可以再次安裝一次 `vl_serializer.pkg`，然後重新啟動 Office 應用程式。

在我的情況下，啟用 `com.microsoft.office.licensingV2.helper` 服務後，再次安裝 `vl_serializer.pkg`，Office 365 就可以正常識別授權並完成啟用。

> **重點：**  
> 問題未必出在 macOS 系統版本或 `vl_serializer.pkg` 本身，而有可能是 `com.microsoft.office.licensingV2.helper` 這項 Office Licensing Helper 服務被停用了。
```
