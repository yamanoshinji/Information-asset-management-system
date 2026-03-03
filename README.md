# Information-asset-management-system
情報資産管理システムの構築

## フォルダ構成
```
├── frontend/
│   └──
├── backend/
│   └──
└── docs/
    ├── 01_requirements/                  # 【要件定義】
    │    ├── 01_business_requirements.md  # 解決したい課題、MVPスコープ、業務フロー
    │    └── 02_non_functional.md         # 非機能要件（パフォーマンス、セキュリティ、動作環境など）
    │
    ├── 02_architecture/                  # 【システムアーキテクチャ】
    │    ├── 01_system_design.md          # 全体構成図（インフラ構成、利用技術スタック）
    │    └── adrs/                        # Architecture Decision Records (技術選定の理由・履歴)
    │         ├── 0001-use-nestjs.md
    │         └── 0002-use-jsonb-for-specific-details.md
    │
    ├── 03_database/                      # 【データベース設計】
    │    ├── 01_schema_overview.md        # テーブル一覧、ER図（Mermaid）、Prismaのベースモデル
    │    └── 02_jsonb_structures.md       # ※重要：6カテゴリごとの個別項目(JSONB)の詳細な型定義
    │
    ├── 04_api/                           # 【API設計】
    │    ├── 01_endpoints.md              # REST APIのエンドポイント一覧
    │    └── 02_interfaces.md             # リクエスト/レスポンスのデータ構造
    │
    ├── 05_frontend/                      # 【フロントエンド設計】
    │    ├── 01_routing.md                # 画面一覧とURL設計
    │    └── 02_components.md             # 共通UIコンポーネントや状態管理ルール
    │
    ├── 06_management/                    # 【プロジェクト管理】
    │    ├── 01_wbs_and_tasks.md          # 開発タスク（WBS）と進捗トラッキング
    │    └── 02_prompts_templates.md      # Copilotに指示を出すときのプロンプトのテンプレート集
    │
    └── 99_manuals/                       # 【運用・ユーザーマニュアル】
        ├── admin_manual.md
        └── user_manual.md
```