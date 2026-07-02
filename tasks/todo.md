# 応募フォーム修理 TODO（2026-07-02開始 / 2026-07-03完了）

背景: 応募フォームが見た目だけで実際には何も送信していなかった（handleSubmitがalertのみのDEMO実装）。
設計: Cloudflare Worker（受付係）+ D1（記録帳）+ メール通知。寛樹さん承認済み。

- [x] 現状調査（フォーム欄・デプロイ方式・既存Cloudflareパターン）
- [x] 設計提案と承認（Worker + D1 + メール通知）
- [x] Cloudflareログイン状態の確認（ログイン済み）
- [x] frevia-recruit-api 新規作成（Worker + D1 + send_email）
- [x] LP index.html の送信処理を本物の送信に差し替え（POSTボディ送信・失敗時は入力を消さない・ハニーポット追加）
- [x] 多角レビュー（セキュリティ / Cloudflare作法 / 連携・UX）→ メイン監査 → 重大1件・中1件を修正
- [x] デプロイ（D1作成 → マイグレーション → Worker公開 → recruit-api.frevia-agency.jp）
- [x] 実測テスト（テスト応募3件 → D1保存を実測確認 → メール送信ログにエラーなし）
- [x] LP変更をGitHubへ反映 → 本番ページが手元の修正版と完全一致することを照合済み
- [x] 仕様書類の作成・更新（両アプリのPROJECT_SPEC / CLAUDE.md / lessons）
- [x] codexレビュー実行
- [ ] 通知メールが受信箱に届いたことの寛樹さん確認（唯一の残項目）
- [x] 過去応募データは復元不能である旨を寛樹さんに伝達

## レビュー（2026-07-03記入）
- 修理内容: LPのhandleSubmitをfetch POST実送信に差し替え、新設のfrevia-recruit-api（Cloudflare Worker）で受信→D1保存→通知メール送信。
- 実装中に多角レビューで発見・修正したバグ: (1)【重大】mimetextのReply-Toは文字列不可・Mailboxインスタンス必須（放置すると通知メールが無音全滅）(2)【中】本文サイズ制限がContent-Length申告頼みで回避可能→実バイト数ストリーム判定に変更。
- 実測結果: テスト応募3件がD1に保存済み・Workerログにメール送信エラーなし・本番ページ反映確認済み。
- 教訓: レビュー担当の修正提案も実測してから採用する（提案2案中1案は実測で失敗）。詳細は frevia-recruit-api/tasks/lessons.md。
