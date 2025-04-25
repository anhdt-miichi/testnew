 検討したソリューション:
1. AWS DocumentDB または AWS Backup を使用
バックアップ方法: クラスターのスナップショットを作成

自動化:

AWS Backup サービスを利用可能

DocumentDB の デイリーバックアップ 機能を利用可能

手動:

クラスターのスナップショットを手動で作成

2. MongoDB ツールを使用: mongodump, mongorestore
自動化:

スクリプトの作成が必要

手動:

mongodump や mongorestore のコマンドラインツールを使用

✅ 結論:
AWS DocumentDB に備わっているバックアップおよびリストア機能だけで、ほとんどのケースに対応できると考えています。統合されており、設定も簡単です。
