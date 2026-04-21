# 🎙️ Siri Shortcut 語音記帳指南

## 方案說明

雖然 Siri 無法直接控制 Web App，但我們可以透過 **iPhone Shortcut + URL Scheme** 實現語音記帳流程。

---

## 📱 Siri Shortcut 設定方式

### 方法：使用「剪貼簿 + 網頁」流程

1. **喺 iPhone 開 Shortcuts App**
2. **創建新 Shortcut，命名為「記帳」**
3. **加入步驟：**
   - **「Ask for Input」** → 問題：「金額」
   - **「Ask for Input」** → 問題：「類別」
   - **「Text」** → 格式：`https://yayasasapig.github.io/family-accounting-app/add.html?amount=[金額]&category=[類別]`
   - **「Open URL」** → 打開上面嘅 URL

4. **對 Siri 說：**
   - 「Hey Siri，記帳」
   - 然後話「50 蚊」「茶餐廳」

### ⚠️ 限制
- 呢個方法會打開 Safari 並跳轉到 add.html，帶上預填參數
- Web App 需要支持 URL 參數自動填表（見下方）

---

## 🔧 Web App URL 參數支援（需要開發）

修改 add.html，支援以下 URL 格式：
```
add.html?amount=50&category=food&note=茶餐廳
```

JavaScript 解析：
```javascript
const params = new URLSearchParams(window.location.search);
const amount = params.get('amount');
const category = params.get('category');
const note = params.get('note');
// 自動填入表單
```

---

## 🎯 理想流程（需要真正後端）

如使用 Firebase 後端，可實現：
1. Siri Shortcut → 呼叫 Firebase Function
2. 語音轉文字 + 解析
3. 自動寫入資料庫
4. Web App 即時更新

---

## 📋 總結

| 方案 | 效果 | 難度 |
|------|------|------|
| Web Speech API（App內🎤）| ✅ 即時語音轉文字 | ⭐ 簡單 |
| Shortcut URL Scheme | ⚠️ 需手動填一半 | ⭐⭐ 中等 |
| Firebase + Shortcut API | ✅ 完美語音記帳 | ⭐⭐⭐ 複雜 |

---

## 🚀 下一步建議

1. 先完成 Web Speech API（已派 Developer）
2. 再加入 URL 參數支援
3. 最後視乎需要加入 Firebase 後端
