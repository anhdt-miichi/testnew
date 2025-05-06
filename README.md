
## 🔍 調査方法

### 1. AWS Tag Editorを使用

- **手順：**
  - [AWS Tag Editor](https://console.aws.amazon.com/resource-groups/tag-editor)でリージョン内のすべてのリソースを一覧表示。
  - サービスごとに分類（例：EC2、RDS、EKSなど）。
  - [AWS Service Quotas](https://console.aws.amazon.com/servicequotas/)で定義されたクォータと照合。

- **メリット：**
  - **実際に使用中のリソース**を確認可能。
  - EKSなど**Service Quotasで使用量を表示できないサービス**に対応。

- **デメリット：**
  - **クォータとの対応付けは手動**。
  - 大規模な環境では時間がかかる。

---

### 2. AWS Service Quotasを使用

- **手順：**
  - [AWS Service Quotas](https://console.aws.amazon.com/servicequotas/)で各サービスの**クォータと使用量**（対応している場合）を確認。

- **メリット：**
  - クォータ情報の**一元管理**。
  - EC2やLambdaなど**使用量を可視化**できるサービスに便利。

- **デメリット：**
  - EKSなど**使用量が確認できないサービス**がある。
  - 実際のリソース詳細は確認できない。

---

## 📊 要約と今後の対応

- 両方法の結果をまとめて、以下をレポート：
  - **現在の使用状況**
  - **サービスごとのクォータ上限**
  - **使用量が見えないサービスの特定**
  - **必要に応じたクォータ引き上げの検討**
