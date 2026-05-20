# Markdown Experience Guidelines (MDXG)

**Language:** [English](README.md) | 日本語

**インターフェースが Markdown ドキュメントをどう提示し、どう操作させるべきかを定義する仕様です。**

Markdown はもっとも広く使われているドキュメント形式です。あらゆる AI モデルが扱え、あらゆる開発者が読み、あらゆるプラットフォームで描画できます。  
しかし、Markdown の「読む体験」は長年ほとんど進化していません。

50 行の README も、3,000 行の仕様書も、同じように「ただ長くスクロールするだけ」の表示になりがちです。  
ナビゲーションがなく、構造が見えず、いまどこを読んでいるのか分かりにくい。  
MDXG はこの課題を解決します。

![MDXG Preview](assets/screenshot.png)

*MDXG の仕様を実装した一例である VS Code 拡張。単一の markdown ファイルを、ナビゲーション可能な複数ページ体験に変換します。*

**[仕様のライブ版を読む (mdxg.org) →](https://mdxg.org)**

## MDXG とは

MDXG は、Markdown の**構文**ではなく、Markdown をどう**提示・操作**するかの仕様です。  
CommonMark / GFM / MDX と競合するものではなく、その一段上の「体験レイヤー」を定義します。

| レイヤー | |
|---|---|
| **MDXG** | 表示 + 操作の仕様 |
| **GFM / MDX** | 構文拡張 |
| **CommonMark** | 基本構文仕様 |

MDXG は既存の `.md` ファイルをそのまま扱えます。  
ファイル内容を変えるのではなく、「見せ方」を変える仕様です。

Markdown を表示するあらゆるインターフェース（エディタ、ドキュメント基盤、ノートアプリ、AI UI、CMS など）が実装対象になります。

### 何が違うのか

**ドキュメントサイトジェネレーター（VitePress / MkDocs / Docusaurus など）との違い**  
MDXG は構築パイプラインではなく、読書体験に焦点を当てます。コンテンツ配置に依存せず、任意の `.md` に適用できます。

**Markdown ビューア系ツールとの違い**  
優れた機能は既に存在しますが、実装ごとに仕様がばらつきます。MDXG はその共通ルールを標準化します。

## 主要機能

詳細は [SPEC.md](SPEC.md)（日本語版: [SPEC.ja.md](SPEC.ja.md)）を参照してください。要点は次のとおりです。

- **仮想ページ化**: H1/H2 で文書をページ分割し、1 ファイルを複数ページ体験にする  
- **ページナビゲーション**: 全ページ表示・任意移動・現在ページの明示  
- **テーマ適応**: ホストのライト/ダークテーマに追従  
- **コードブロック描画**: 言語付きフェンスをシンタックスハイライト、全コードにコピー操作  
- **タスクリスト表示**: `- [ ]` / `- [x]` をチェックボックス化  
- **ページ内アウトライン**: H3–H6 をナビゲート可能にする  
- **前後ページ移動**: previous/next の順次遷移  
- **検索**: 全ページ横断の一致ハイライトと前後移動  
- **プレビュー/ソース切替**: 同一画面内で描画表示とソース表示を切替  
- **文書リンク**: 他の `.md` へのリンクも同じ MDXG 体験で開く  

## なぜ今か

Markdown は、AI と人間の協業における標準インターフェースです。  
AI は Markdown を生成し、人はそれを読む・直す・承認します。

AI にとって Markdown は低コストで扱いやすい一方、人間側の閲覧体験は十分とは言えません。  
MDXG はこのギャップを埋め、1 つの形式で AI と人の双方に最適な体験を目指します。

## 参考実装

| Package | 説明 | 状態 |
|---|---|---|
| [@mdxg/parser](packages/parser) | 共有 Markdown パーサー | コアライブラリ |
| [@mdxg/vscode](packages/vscode) | VS Code 拡張 | 参考実装 |
| [@mdxg/web](apps/web) | ドキュメントサイト ([mdxg.org](https://mdxg.org)) | 参考実装 |

## 実装者向け

MDXG は Markdown を描画する任意の環境で実装できます。適合レベルは 2 種類です。

- **MDXG Viewer**: 読み取り専用（表示・ナビゲーション中心）
- **MDXG Editor**: Viewer の全機能 + ソース編集と文書リンク統合

まずは [SPEC.md](SPEC.md) / [SPEC.ja.md](SPEC.ja.md) を確認してください。  
実装例として [VS Code 版](packages/vscode) を参照できます。  
共有パーサー [`@mdxg/parser`](packages/parser) は、文書分割・見出し抽出・slug 生成を提供します。

## コントリビュート

仕様フィードバック、バグ報告、新規実装、コード改善を歓迎します。  
詳細は [CONTRIBUTING.md](CONTRIBUTING.md)（日本語版: [CONTRIBUTING.ja.md](CONTRIBUTING.ja.md)）を参照してください。

Issue / Discussion / Pull Request は [GitHub リポジトリ](https://github.com/vercel-labs/mdxg) から利用できます。
