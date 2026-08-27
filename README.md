# List-of-out-of-focus-photos-Excel-output-

# 🔍 ピンボケ写真検索（n8nワークフロー）

Google Gemini AIを使用して写真フォルダ内の不要写真（ピンぼけ・誤撮影等）を自動判別し、
Excel一覧に出力するn8nワークフローです。

## 📋 機能

- 指定フォルダ内の写真を一括読み込み
- Gemini AIが各写真を分析し「KEEP / MOVE」を判定
- 判定結果をExcelファイルに蓄積出力（ファイル名・パス・判定理由）
- 処理済みファイルのログ管理により、再実行時にスキップ
- 1日あたり最大500枚の処理制限付き

## ⚙️ 事前準備

### 1. n8n環境
- n8n v1.0以上（セルフホストまたはn8n Cloud）

### 2. Google Gemini APIキー
- [Google AI Studio](https://aistudio.google.com/) でAPIキーを取得
- n8nの認証情報に「Google Gemini (PaLM) API」を追加

### 3. 写真フォルダの配置

以下のディレクトリ構成で写真を配置してください：

/home/node/.n8n-files/picture/2026/2026-06/IMG_xxxxx.jpg

### 4. 処理済みログの初期化

初回実行時に自動生成されますが、手動でリセットしたい場合は：

/home/node/.n8n-files/progress/processed.txt

の中身を空にしてください。

## 🔧 インポートとセットアップ

1. n8nダッシュボードで **「Workflows」→「Import from File」** を選択
2. `workflow.json` ファイルを選択
3. 以下のパスを**ご自身の環境に合わせて修正**：

   | ノード名 | 修正対象 | 修正内容 |
   |----------|----------|----------|
   | 写真フォルダ内の一覧取得 | `fileSelector` | 写真パスを変更 |
   | 処理済みログ読み込み | `fileSelector` | ログファイルパスを変更 |
   | 処理済み写真ログの追記保存 | `fileName` | ログファイルパスを変更 |
   | ピンぼけ写真一覧エクセル出力 | `fileName` | Excel出力パスを変更 |
   | 既存エクセル読み込み | `fileSelector` | Excelファイルパスを変更 |
   | エクセル用出力データの生成 | コード内 `D:\Pictures` | Windows側の写真パスに変更 |

4. **Geminiによる不要写真判定** ノードの認証情報を設定
5. ワークフローを保存し、手動実行で動作確認

## ⚠️ 注意事項

- **API費用**: Gemini APIの使用量に応じた料金が発生します
- **処理速度**: 写真1枚あたり数秒〜十数秒程度かかります
- **待機ノード**: 各写真処理後に30秒の待機が設定されています（APIレート制限対策）
- **判定精度**: AI判定は完全ではありません。重要写真は手動で確認してください

---

## 📖 開発経緯・詳細解説

開発の背景や試行錯誤のプロセスについてはブログにて詳しく解説しています。

👉 **[n8n×Geminiでピンボケ写真を自動検出！8万枚の写真整理を爆速自動化した話（貧乏暇なしB型ブログ）](https://b-blog.gogogogogogogogogogo5555555555.uk/?p=333)**

---

## 👤 作者

- **ごーどん**
- **Blog**: [貧乏暇なしB型ブログ](https://b-blog.gogogogogogogogogogo5555555555.uk/)
- **X (Twitter)**: [@hfduohsfu342542](https://x.com/hfduohsfu342542)

---

## 📄 ライセンス

本プロジェクトは [MIT License](LICENSE) のもとで公開されています。
