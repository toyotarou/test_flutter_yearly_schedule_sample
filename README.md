# test_flutter_yearly_schedule_sample

最終更新日：2026-03-30

## 概要

**複数年にまたがるイベントを年単位タイムラインで表示する Flutter サンプルアプリ**です。

年ごとに 12 分割した月グリッドをダイアログ内にリスト表示し、開始日〜終了日を持つ `YearRangeSpan` を各年の行にカラーバンドとして描画します。`scroll_to_index` による自動スクロールで、ボタンタップ時に指定した年の行を先頭に揃えてジャンプします。

---

## 主な機能

- **年タイムライン一覧**：複数年（例：2020〜2029）を縦スクロールリストで表示
- **12 分割月グリッド**：1 年を 1〜12 月の等幅列で表示
- **スパンイベントバンド**：開始日〜終了日を持つイベントを月グリッド上にカラーバンドで描画
- **年またぎ自動クリッピング**：イベントが複数年にまたがる場合、各年分の月範囲に自動トリミング
- **年指定オートスクロール**：ホーム画面のボタンでダイアログを開くと同時に、指定年の行へ自動スクロール（上揃え）
- **ダークテーマ**：ダークカラースキームでの表示

---

## 画面構成

```
HomePage（起動画面）
├── ElevatedButton × 5（「2021へ」「2024へ」など年指定ボタン）
└── Dialog（年タイムラインダイアログ）
    └── YearTimelineDialogBody（AutoScrollController で年ジャンプ）
        ├── ヘッダー（年範囲タイトル・閉じるボタン）
        └── ListView.builder（各年ごと）
            └── AutoScrollTag
                └── YearRow
                    ├── 年タイトルラベル
                    └── YearTimeline（12 分割月グリッド + バンド）
                        └── _Band × N（カラーバンド）
```

---

## ファイル構成

```
lib/
└── main.dart                   # エントリーポイント＋全クラス定義（単一ファイル構成）

    MyApp                       # アプリエントリー Widget
    HomePage                    # 起動画面（年指定ボタン群）
    YearTimelineDialogBody      # ダイアログ本体（StatefulWidget・AutoScroll 制御）
    YearRow                     # 1 年分の行 Widget（年ラベル + YearTimeline）
    YearTimeline                # 12 分割月グリッド＋バンド描画 Widget
    YearRangeSpan               # 年またぎイベントデータクラス（DateTime 範囲・色・ラベル）
    YearSpan                    # 1 年内にクリッピングされた月範囲データクラス
    _Band                       # カラーバンド Widget
    _demoRanges()               # サンプルイベントデータ
    _spansForYear()             # YearRangeSpan → 指定年の YearSpan リストへ変換
```

---

## 主要データクラス

### `YearRangeSpan`（年またぎイベント）

| フィールド | 型         | 説明                         |
|----------|------------|------------------------------|
| `start`  | `DateTime` | イベント開始日               |
| `end`    | `DateTime` | イベント終了日               |
| `color`  | `Color`    | バンドの色                   |
| `label`  | `String`   | イベントラベル               |

### `YearSpan`（1 年内クリッピング済み月範囲）

| フィールド     | 型       | 説明                          |
|--------------|----------|-------------------------------|
| `startMonth` | `int`    | 開始月（1〜12）               |
| `endMonth`   | `int`    | 終了月（1〜12）               |
| `color`      | `Color`  | バンドの色                    |
| `label`      | `String` | イベントラベル                |

---

## 依存パッケージ

### dependencies

| パッケージ         | バージョン   | 用途                            |
|-------------------|-------------|--------------------------------|
| `flutter`         | SDK         | Flutter フレームワーク           |
| `cupertino_icons` | `^1.0.8`   | iOS スタイルアイコン             |
| `scroll_to_index` | `^3.0.1`   | 指定インデックスへの自動スクロール |

### dev_dependencies

| パッケージ       | バージョン  | 用途              |
|----------------|------------|------------------|
| `flutter_lints` | `^5.0.0`  | 推奨 Lint ルール  |

---

## 環境

| 項目       | バージョン  |
|-----------|-----------|
| Dart SDK  | `^3.8.1`  |

---

## セットアップ

```bash
# リポジトリのクローン
git clone https://github.com/toyotarou/test_flutter_yearly_schedule_sample.git
cd test_flutter_yearly_schedule_sample

# パッケージの取得
flutter pub get

# アプリの実行
flutter run
```

---

## 対応プラットフォーム

- Android
- iOS
- Web
- macOS
- Linux
- Windows
