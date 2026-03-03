# 命名規則 (Naming Conventions)

本プロジェクト（IAMS）における、ディレクトリ、ファイル、およびコードレベルでの命名規則を定義する。
AI（GitHub Copilot）による自動生成の精度を高めるため、原則としてこのルールから逸脱しないこと。

## 1. ドキュメント (docs/) の命名規則
- **ディレクトリ名・ファイル名**: すべて小文字の**スネークケース**（アンダーバーつなぎ）で統一する。
  - ⭕️ OK: `01_business_requirements.md`, `0001_use_nestjs.md`
  - ❌ NG: `01-business-requirements.md`, `UserManual.md`
- **プレフィックス**: 順序を明示するため、2桁（ADRの場合は4桁）の数字とアンダーバーを先頭に付ける。

## 2. フロントエンド (React/TypeScript) の命名規則
- **ディレクトリ名**: 小文字のケバブケース（ハイフンつなぎ）。 (例: `components/ui`, `pages/asset-list`)
- **ファイル名 (コンポーネント)**: **パスカルケース** (大文字始まり)。 (例: `AssetTable.tsx`, `Header.tsx`)
- **ファイル名 (ユーティリティ等)**: 小文字のキャメルケース または ケバブケース。 (例: `formatDate.ts`)
- **変数名 / 関数名**: キャメルケース (小文字始まり)。 (例: `assetList`, `fetchAssets()`)
- **インターフェース / 型名**: パスカルケース。 (例: `Asset`, `PhysicalAssetDetails`)

## 3. バックエンド (NestJS/TypeScript) の命名規則
※NestJSの標準的なルール（CLIが自動生成する形式）に準拠する。
- **ディレクトリ名**: 小文字のケバブケース。 (例: `assets`, `audit-logs`)
- **ファイル名**: `[ドメイン名].[役割].ts` のケバブケース。
  - ⭕️ OK: `assets.controller.ts`, `audit-logs.service.ts`
- **クラス名**: パスカルケース。ファイル名と対応させる。
  - ⭕️ OK: `AssetsController`, `AuditLogsService`
- **変数名 / 関数名**: キャメルケース。

## 4. データベース (PostgreSQL / Prisma) の命名規則
- **Prisma Model (テーブル名)**: パスカルケース（単数形）。 (例: `Asset`, `User`, `AuditLog`)
- **カラム名 (Prisma Schema内)**: キャメルケース。 (例: `departmentId`, `specificDetails`)
  ※実際のDB(PostgreSQL)上では、Prismaが自動的にスネークケース(`department_id`)にマッピングする想定。
- **列挙型 (Enum)**: パスカルケース、値はすべて大文字のスネークケース。 (例: `enum Category { PHYSICAL, PRODUCT }`)