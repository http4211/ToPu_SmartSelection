# ToPu SmartSelection

![Blender](https://img.shields.io/badge/Blender-4.0%2B-orange)
![Version](https://img.shields.io/badge/version-1.4.9-blue)
![License](https://img.shields.io/badge/license-GPL--3.0--or--later-green)

**ToPu SmartSelection** は、Blender の選択セット管理と Local View を拡張するアドオンです。  
オブジェクト、コレクション、メッシュ要素の選択を保存・呼び出ししながら、選択範囲だけをすばやく表示できます。

複雑なモデル、リグ、背景セット、複数オブジェクト編集などで、  
「必要なものだけ選ぶ」「必要な範囲だけ表示する」「階層的に戻る」操作を軽くすることを目的にしています。


https://github.com/user-attachments/assets/294b9ae9-ac4e-494b-abb1-5968cd1ac58b



---

## Screenshots

UI 説明用の画像は `docs/images/` に配置する想定です。  
ファイル名を変更する場合は、下記のパスも合わせて変更してください。

<p align="center">
<img width="200" height="26" alt="image" src="https://github.com/user-attachments/assets/f629482f-910a-4181-a9e7-fc95752a054f" />
</p>
<p align="center">
<img width="375" height="359" alt="image" src="https://github.com/user-attachments/assets/2668cafd-6bb6-4002-82b9-992a369561f0" />
</p>
<p align="center">
<img width="193" height="24" alt="image" src="https://github.com/user-attachments/assets/5ade42ac-3687-492f-9d7f-e274bef4bc11" />
</p>
<p align="center">
<img width="598" height="453" alt="image" src="https://github.com/user-attachments/assets/bb090854-df2d-45ec-bda6-635417ad4ca4" />
</p>

---

## Features

- オブジェクト選択セットの保存・呼び出し
- コレクション単位の選択補助
- メッシュの頂点・辺・面選択セットの保存・呼び出し
- 階層的に表示範囲を切り替える **TP Smart Local View**
- Mesh / Curve / Surface / Armature / Metaball の Edit Mode 対応
- メッシュ統合時に選択セットを保持しやすい `Ctrl + J` 拡張
- 日本語 / English UI 切り替え

---

## Requirements

- Blender 4.0 or later
- 外部 Python パッケージ不要

---

## Installation

1. Release から zip ファイルをダウンロードします。
2. Blender を開きます。
3. `Edit > Preferences > Add-ons` を開きます。
4. `Install from Disk...` から zip ファイルを選択します。
5. **ToPu: SmartSelection** を有効化します。

有効化すると、3D View のヘッダーに ToPu SmartSelection の UI が追加されます。

---

## UI Overview

![UI Overview](docs/images/ui-overview.png)

### Object / Collection / Mesh Mode

ヘッダー左側のモード切り替えから、扱う対象を変更できます。

| Mode | 内容 |
|---|---|
| Object | オブジェクト選択セットを管理 |
| Collection | コレクション内のオブジェクトを選択 |
| Mesh | Edit Mode の頂点・辺・面選択セットを管理 |

### Header Buttons

| 操作 | 内容 |
|---|---|
| `+` | 新規選択セットを作成 |
| `Shift + +` | 現在の選択をアクティブセットへ追加 |
| `-` | アクティブセットを削除 |
| `Shift + -` | 現在の選択をアクティブセットから削除 |
| 目玉ボタン | 選択後に Local View へ入る設定を切り替え |
| `Shift + 目玉ボタン` | セット適用時に現在の選択を保持する設定を切り替え |
| `Details` | 詳細設定ポップオーバーを開く |

---

## TP Smart Local View

![TP Smart Local View UI](docs/images/smart-local-view-ui.png)

**TP Smart Local View** は、Blender 標準の Local View を階層的に扱いやすくする機能です。  
選択範囲だけを表示し、さらに選択した一部へ深く入り、必要に応じて 1 階層ずつ戻れます。

### Shortcut

| Shortcut / 操作 | 内容 |
|---|---|
| `Numpad /` | TP Smart Local View を実行 |
| Local View ボタンをクリック | Local View の開始 / 終了 |
| `Shift + クリック` | 選択範囲へ 1 階層深く入る |
| `Alt + クリック` | 1 階層戻る |

### Supported Local View Targets

| 対象 | 対応 |
|---|---|
| Object Mode | 対応 |
| Mesh Edit Mode | 対応 |
| Curve Edit Mode | 対応 |
| Surface Edit Mode | 対応 |
| Armature Edit Mode | 対応 |
| Metaball Edit Mode | 対応 |

---

## Selection Sets

![Selection Set UI](docs/images/selection-set-ui.png)

Object Mode では、選択中のオブジェクトを選択セットとして保存できます。  
よく使うパーツ、リグ、背景グループなどを登録しておくと、ワンクリックで再選択できます。

主な操作:

- 選択セットの作成
- セット名の変更
- セットの削除
- 選択中オブジェクトの追加 / 削除
- 選択セット一覧の Save / Load

---

## Mesh Selection Sets

![Mesh Selection Set UI](docs/images/mesh-selection-set-ui.png)

Mesh Edit Mode では、頂点・辺・面の選択状態をメッシュ選択セットとして保存できます。  
複数メッシュの同時編集時も、同名セットをまとめて扱えます。

| 操作 | 内容 |
|---|---|
| Create from selection | 現在のメッシュ選択からセットを作成 |
| Select | メッシュ選択セットを適用 |
| Add Sel | 現在の選択をアクティブセットへ追加 |
| Remove Sel | 現在の選択をアクティブセットから削除 |
| Delete | アクティブセットを削除 |

---

## Default Shortcuts

| Shortcut | 内容 |
|---|---|
| `Numpad /` | TP Smart Local View |
| `Ctrl + J` | Join Objects (keep Mesh Sets) |

`Ctrl + J` は通常の Join の代わりに、各オブジェクトのメッシュ選択セットをできるだけ保持する統合処理を実行します。

---

## Preferences

![Preferences](docs/images/preferences.png)

`Edit > Preferences > Add-ons > ToPu: SmartSelection` から設定できます。

| 設定 | 内容 |
|---|---|
| UI Language | UI とツールチップの言語を切り替え |
| Keep Selection on Apply | セット適用時に現在の選択を保持 |
| Show icon in Tool Header | ツールヘッダーの Local View ボタン表示を切り替え |
| Auto switch to Mesh mode in Edit Mode | Edit Mode 時に Mesh モードへ自動切り替え |
| キーマップを修復 | 壊れた / 重複したキーマップを再登録 |

---

## Troubleshooting

### `Numpad /` が使えない

テンキーがないキーボードの場合は、Blender の Keymap 設定から `TP Smart Local View` に別のショートカットを割り当ててください。

### キーマップが登録されない / 重複する

アドオンプリファレンスの **キーマップを修復** を実行してください。

### 日本語が文字化けする

Blender の Interface Font が日本語に対応していない可能性があります。  
`Edit > Preferences > Interface > Text Rendering > Interface Font` で、Noto Sans CJK などの CJK 対応フォントを指定してください。

---

## License

GPL-3.0-or-later

## Author

http4211
