# 公式参考資料（確認日：2026年11月13日）

研修の中の製品の説明は、次の公式資料に基づく。URL は講座の制作時点のもの。改訂されることがあるため、利用前に必ず確認する。

| No. | 区分 | 資料 | 公式 URL | 使う講義 | 確認の状態 |
|---|---|---|---|---|---|
| R1 | Claude Code | メモリ（CLAUDE.md の読み込み規則、/memory、# のショートカット） | https://code.claude.com/docs/en/memory | L08 | 確認済み（検索で本文を確認） |
| R2 | Claude Code | 日本語版のメモリ管理（CLAUDE.md のインポート、サブツリーの読み込み） | https://docs.anthropic.com/ja/docs/claude-code/memory | L08 | 確認済み（検索で本文を確認） |
| R3 | Docker | ストレージ（ボリューム・バインドマウント・tmpfs の違い） | https://docs.docker.com/engine/storage/ | L04 | 確認済み |
| R4 | Docker | バインドマウント（ホストとコンテナでソースを共有する。既定は読み書き） | https://docs.docker.com/engine/storage/bind-mounts/ | L04 | 確認済み |
| R5 | Docker Desktop | WSL 2 のベストプラクティス（Linux のファイルシステムに置く） | https://docs.docker.com/desktop/features/wsl/best-practices/ | L04 | 確認済み |
| R6 | Microsoft | WSL のファイルシステム（Linux 側のファイルを使うと速い） | https://learn.microsoft.com/en-us/windows/wsl/filesystems | L04 | 確認済み |
| R7 | OpenAI | Chat Completions API のリファレンス（作成・メッセージ・応答） | https://platform.openai.com/docs/api-reference/chat/create | L05 | 確認済み（検索結果で参照先を確認。本文の項目は要確認） |
| R8 | Playwright | Python 版の導入（pip install playwright、python -m playwright install） | https://playwright.dev/python/docs/intro | L07 | 確認済み |
| R9 | Python | unittest（標準ライブラリの試験） | https://docs.python.org/3/library/unittest.html | L07 | 未確認（講座制作時に確認が必要） |
| R10 | Node.js | テストランナー（node:test） | https://nodejs.org/api/test.html | L07 | 未確認（講座制作時に確認が必要） |
| R11 | VS Code | Python のテスト（テスト画面の使い方） | https://code.visualstudio.com/docs/python/testing | L04 | 未確認（講座制作時に確認が必要） |
| R12 | Microsoft | WSL の導入 | https://learn.microsoft.com/en-us/windows/wsl/install | L04 | 未確認（講座制作時に確認が必要） |

## 使い方の注意
- 「確認済み」は、講座の制作時に公式の本文（または公式の参照先）を確かめたもの。
- 「未確認」は、URL を公式の既知の場所として示しているが、本文は確かめていない。収録前に必ず開いて確認する。
- OpenAI の項目名（モデル名、料金、usage の数え方）は変わりやすい。公式の最新の版を見て、講座の説明を直す。
