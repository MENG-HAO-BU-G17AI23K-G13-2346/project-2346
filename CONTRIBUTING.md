# 貢獻指南 (Contributing Guide)

感謝你對 Stripe CLI 的貢獻興趣！本指南將幫助你快速上手開發。

---

## 📋 目錄

- [開發環境設置](#開發環境設置)
- [常用命令](#常用命令)
- [代碼規範](#代碼規範)
- [測試](#測試)
- [版本發布](#版本發布)

---

## 🚀 開發環境設置

### 前置要求

- **Go 語言**：v1.16 或以上（推薦 1.18+）
  - 檢查版本：`go version`
- **Git**：用於版本控制
- **Make**：用於運行項目命令

### 第一步：克隆項目

```bash
git clone https://github.com/MENG-HAO-BU-G17AI23K-G13-2346/project-2346.git
cd project-2346
```

### 第二步：安裝依賴

**如果你使用 Go 1.18.x 或更高版本：**

```bash
go get ./...
```

**如果你使用 Go v1.16 或 v1.17（最低支持版本）：**

```bash
go get -v -u github.com/stripe/stripe-cli/...
cd go/src/github.com/stripe/stripe-cli
```

### 第三步：設置項目

安裝完依賴後，運行以下命令完成設置：

```bash
make setup
```

這個命令會準備所有必要的開發工具和配置。

---

## 🛠️ 常用命令

| 命令 | 說明 | 何時使用 |
|------|------|--------|
| `go run cmd/stripe/main.go` | 運行本地 CLI 版本 | 測試你的改動 |
| `make test` | 運行完整的測試套件 | 提交前驗證代碼 |
| `make lint` | 檢查代碼品質和風格 | 提交前進行檢查 |
| `make setup` | 初始化開發環境 | 第一次設置時 |
| `make release` | 發布新版本 | 完成所有修改後 |

### 快速運行別名設置（可選）

為了方便開發，你可以在 shell 配置文件中添加以下別名：

```bash
# 添加到 ~/.bashrc 或 ~/.zshrc
alias stripe-dev='go run cmd/stripe/main.go'
```

然後在 `project-2346` 目錄中，你可以直接運行：

```bash
stripe-dev  # 等同於 go run cmd/stripe/main.go
```

---

## 📐 代碼規範

### 代碼風格檢查

在提交代碼前，必須運行代碼檢查工具：

```bash
make lint
```

首次運行可能需要安裝 `golangci-lint`：

```bash
brew install golangci/tap/golangci-lint
```

### 錯誤處理

所有生產環境代碼在創建錯誤時，必須分配語義錯誤分類。

**使用 `errorcategory.New` 處理固定消息：**

```go
return errorcategory.New(errorcategory.UserInput, "an argument is required")
```

**使用 `errorcategory.Errorf` 處理格式化消息：**

```go
return errorcategory.Errorf(errorcategory.Auth, "profile %q has no API key", profile)
```

**添加上下文時，繼續使用 `%w` 包裝原始錯誤：**

```go
return fmt.Errorf("loading configuration: %w", err)
```

**特殊情況：**
- 測試文件和生成的代碼無需遵循此規則
- 如果無法分配錯誤分類，使用 `//nolint:errorcategory` 註釋並說明原因

---

## 🧪 測試

### 運行所有測試

```bash
make test
```

這個命令會運行完整的測試套件，確保你的修改不會破壞現有功能。

### 推薦流程

1. **修改代碼** → 2. **運行測試** → 3. **運行 lint** → 4. **提交 PR**

確保所有測試都通過後再提交你的代碼。

---

## 🎉 版本發布

### 發布新版本

當你完成所有修改並準備好發布時，運行：

```bash
make release
```

該命令會：
1. ✅ 提示你輸入新版本號
2. ✅ 自動創建新的 Git 標籤
3. ✅ 推送更新到倉庫

### 版本號規範

遵循 [語義版本控制](https://semver.org/)：
- **主版本號** (Major)：不兼容的 API 變更
- **次版本號** (Minor)：向下兼容的功能新增
- **修訂號** (Patch)：向下兼容的 bug 修復

例如：`v1.5.3`

---

## 💡 貢獻小技巧

### 開發流程建議

```bash
# 1. 創建新分支
git checkout -b feature/your-feature-name

# 2. 進行開發和測試
go run cmd/stripe/main.go  # 測試你的改動

# 3. 運行所有檢查
make test    # 運行測試
make lint    # 檢查代碼風格

# 4. 提交代碼
git add .
git commit -m "描述你的改動"

# 5. 推送並創建 PR
git push origin feature/your-feature-name
```

### 常見問題

**Q: 運行 `make test` 失敗了？**
- A: 確保 `make setup` 已成功運行，所有依賴已安裝

**Q: `golangci-lint` 安裝失敗？**
- A: 可能需要更新 Homebrew：`brew update && brew upgrade golangci-lint`

**Q: 如何測試特定功能？**
- A: 使用 `go test ./... -run TestName` 運行特定測試

---

## 📚 更多資源

- [Stripe CLI 官方文檔](https://docs.stripe.com/cli)
- [Go 官方指南](https://golang.org/doc/)
- [Git 工作流程](https://git-scm.com/book/zh/v2)

---

## 🤝 需要幫助？

如果你遇到問題，可以：
- 查看項目的 [Issues](https://github.com/MENG-HAO-BU-G17AI23K-G13-2346/project-2346/issues)
- 提出新的 Issue 描述你的問題
- 查閱相關的 Pull Requests

---

**謝謝你的貢獻！** 🎊
