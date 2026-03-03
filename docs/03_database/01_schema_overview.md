# データベース設計 (Schema Overview)

## 1. 設計方針（シングルテーブル + JSONB）
6つの情報資産カテゴリを別々のテーブルに分けると、全社一覧検索やJOINが極めて複雑になる。
これを避けるため、**全資産を `Asset` テーブルに統合**する。
Excel台帳で共通する項目（CIA、重要度、部署等）は標準カラムとし、カテゴリごとに異なる項目（識別ID、バージョン等）は `specific_details` (JSONBカラム) に格納する。

## 2. Prisma ベースモデル案

```prisma
// This is your Prisma schema file

model User {
  id           String      @id @default(uuid())
  name         String
  departmentId String
  department   Department  @relation(fields: [departmentId], references: [id])
  role         Role        @default(USER) // ADMIN or USER
  assetsAsManager Asset[]  @relation("AssetManager")
  assetsAsAssignee Asset[] @relation("AssetAssignee")
}

model Department {
  id     String  @id @default(uuid())
  name   String
  users  User[]
  assets Asset[]
}

model Asset {
  id              String     @id @default(uuid())
  category        Category   // 列挙型: PHYSICAL, PRODUCT, DATA, EQUIPMENT, PERSONAL_INFO, HUMAN
  name            String     // 情報資産名
  
  // --- ほぼ共通の管理項目 ---
  purpose         String?    // 用途・利用目的
  owner           String?    // 所有者・提供元
  departmentId    String     // 管理部署FK
  department      Department @relation(fields: [departmentId], references: [id])
  managerId       String?    // 管理責任者FK
  manager         User?      @relation("AssetManager", fields: [managerId], references: [id])
  assigneeId      String?    // 管理担当者FK
  assignee        User?      @relation("AssetAssignee", fields: [assigneeId], references: [id])
  location        String?    // 所在・保管・運用場所
  userScope       String?    // 利用者の範囲
  
  // --- セキュリティ評価項目 ---
  ciaC            Int        // 機密性 (1~4)
  ciaI            Int        // 完全性 (1~4)
  ciaA            Int        // 可用性 (1~4)
  importance      Int        // 重要度 (0~4) 自動計算推奨
  
  // --- その他共通 ---
  isEmergencyExport Boolean  @default(false) // 非常持出対象か
  riskAnalysisNo  String?    // リスク分析票管理NO
  remarks         String?    // 備考
  
  // --- 個別項目 (JSONB) ---
  specificDetails Json       // カテゴリごとの個別項目を格納

  // --- メタデータ ---
  createdAt       DateTime   @default(now())
  updatedAt       DateTime   @updatedAt
}

enum Category {
  PHYSICAL
  PRODUCT
  DATA
  EQUIPMENT
  PERSONAL_INFO
  HUMAN
}
enum Role {
  ADMIN
  USER
}