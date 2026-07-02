# 応募フォーム修理 TODO（2026-07-02開始）

背景: 応募フォームが見た目だけで実際には何も送信していなかった（handleSubmitがalertのみのDEMO実装）。
設計: Cloudflare Worker（受付係）+ D1（記録帳）+ メール通知（info@frevia-agency.jpの受信箱宛）。寛樹さん承認済み。

- [x] 現状調査（フォーム欄・デプロイ方式・既存Cloudflareパターン）
- [x] 設計提案と承認（Worker + D1 + メール通知）
- [x] Cloudflareログイン状態の確認（soccer.8.regista@gmail.com でログイン済み）
- [ ] frevia-recruit-api 新規作成（Worker + D1 + send_email）
- [ ] LP index.html の送信処理を本物の送信に差し替え（POSTボディ送信・失敗時は入力を消さない・ハニーポット追加）
- [ ] 多角レビュー（セキュリティ / Cloudflare作法 / 連携・UX）→ メイン監査
- [ ] デプロイ（D1作成 → マイグレーション → Worker公開 → recruit-api.frevia-agency.jp）
- [ ] 実測テスト（テスト応募 → D1保存確認 → 通知メール到達確認）
- [ ] LP変更をGitHubへ反映 → 本番サイトで実測テスト
- [ ] 仕様書類の作成・更新（PROJECT_SPEC / CLAUDE.md / lessons）
- [ ] codexレビュー実行
- [ ] 過去応募データは復元不能である旨を寛樹さんに伝達（設計提案時に伝達済み → 完了報告でも再掲）

## レビュー（完了時に記入）
（未記入）
