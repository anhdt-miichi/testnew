✅ 検討した方法の概要
オンラインマイグレーション（AWS ElastiCache 機能）

説明: オンプレミスの Redis OSS から AWS ElastiCache への移行機能。

制限: ❌ AWS ElastiCache 間の移行には未対応。

REPLICAOF コマンド

説明: Redis 間でデータをレプリケートするための標準コマンド。

制限: ❌ AWS Redis OSS ではサポートされていない。

サードパーティツール（例：redis-dump / redis-load、RedisShake）

説明: Redis データのエクスポート・インポートを行うツール。

制限: ⚠️ 信頼性や互換性の懸念あり（特に機密データや大規模環境で）。

redis-cli によるキーごとのコピー

説明: Redis の全キーをスキャンして、ターゲットに一つずつコピーするスクリプトを作成。

利点: ✅ スクリプトにより柔軟に対応可能。
