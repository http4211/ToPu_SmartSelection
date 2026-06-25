# ToPu SmartSelection

![Blender](https://img.shields.io/badge/Blender-4.0%2B-orange)
![Version](https://img.shields.io/badge/version-1.4.9-blue)
![License](https://img.shields.io/badge/license-GPL--3.0--or--later-green)

**ToPu SmartSelection** は、Blender の選択セット管理と Local View を拡張するアドオンです。  
オブジェクト、コレクション、メッシュ要素の選択を素早く呼び出しながら、選択範囲だけを階層的に表示できます。

複雑なモデル、リグ、背景セット、複数オブジェクト編集などで、
「必要なものだけ選ぶ」「必要な範囲だけ表示する」「元の階層へ戻る」操作を軽くすることを目的にしています。

---

## 主な機能

### オブジェクト選択セット

- 選択中のオブジェクトから選択セットを作成
- セット名のリネーム、並べ替え、削除
- 選択セットへの追加／削除
- 無効なオブジェクト参照の更新／整理
- 選択セット一覧の JSON 保存／読み込み

### コレクション選択

- シーン内のコレクションを一覧表示
- コレクション内のオブジェクトをワンクリックで選択
- 選択後に Local View へ入る「Local View on Select」に対応

### メッシュ選択セット

Edit Mode の頂点・辺・面選択をセットとして保存できます。

- 頂点／辺／面の選択セット作成
- メッシュセットの適用、追加、削除
- マルチオブジェクト編集時の統合リスト表示
- 同名メッシュセットを複数メッシュへまとめて適用
- GUID ベースの保存により、単純なインデックス依存より壊れにくい選択管理
- `Ctrl + J` によるメッシュ統合時も、メッシュ選択セットをできるだけ保持

### TP Smart Local View

Blender 標準の Local View を、階層的に使いやすくする機能です。

- 選択範囲だけを Local View に表示
- さらに選択したものへ 1 階層深く入る
- 1 階層ずつ戻る
- 各階層の選択状態を記憶
- Local View 中のレベルをオーバーレイ表示
- Object Mode / Mesh Edit Mode / Curve / Surface / Armature / Metaball の Edit Mode に対応
- Mesh Local は Paint / Sculpt / Object など別モードへ移動しても状態を保持し、Edit Mode に戻った時に再適用

### ヘッダー UI

3D View のヘッダーから、選択セットと Local View を直接操作できます。

- オブジェクト／コレクション／メッシュモード切替
- 現在のセット名表示
- 追加／削除ボタン
- Local View on Select の目玉ボタン
- 詳細設定ポップオーバー

### 軽量な状態同期

`depsgraph_update_post` のような常時更新に頼りすぎず、入力イベントと RNA msgbus を中心に状態を同期します。  
Local View や Mesh Local の状態がずれた場合も、可能な範囲で実際の View 状態と再同期します。

### 日本語 / English UI

アドオンプリファレンスから UI 言語を切り替えできます。

- 自動
- 日本語
- English

---

## 動作環境

- Blender 4.0 以上
- 外部 Python パッケージ不要
- ライセンス: GPL-3.0-or-later

---

## インストール

1. GitHub の Release から zip ファイルをダウンロードします。
2. Blender を開きます。
3. `Edit > Preferences > Add-ons` を開きます。  
   Blender のバージョンによっては `Extensions > Install from Disk...` からインストールします。
4. ダウンロードした zip を選択します。
5. `ToPu: SmartSelection` を有効化します。

有効化すると、3D View のヘッダーに ToPu SmartSelection の UI が追加されます。

---

## 基本操作

### 1. オブジェクト選択セットを作る

1. Object Mode でオブジェクトを選択します。
2. ヘッダーの `+` ボタンを押します。
3. セット名を入力して作成します。
4. セットを選んで `選択` を押すと、登録したオブジェクトを再選択できます。

#### 便利操作

| 操作 | 内容 |
|---|---|
| `+` | 新規選択セットを作成 |
| `Shift + +` | 選択中のオブジェクトをアクティブセットへ追加 |
| `-` | アクティブセットを削除 |
| `Shift + -` | 選択中のオブジェクトをアクティブセットから削除 |
| `更新` | セット内の無効な参照を整理 |
| `Save` | 選択セット一覧を JSON 保存 |
| `Load` | JSON から選択セット一覧を読み込み |

---

### 2. コレクションを選択する

1. ヘッダー左側のモード切替ボタンで `コレクション` モードにします。
2. コレクション一覧から対象を選びます。
3. `選択` を押すと、コレクション内のオブジェクトを選択できます。

目玉ボタンを ON にしている場合、選択後にそのまま Local View へ入ります。

---

### 3. メッシュ選択セットを作る

1. Mesh の Edit Mode に入ります。
2. 頂点／辺／面を選択します。
3. `選択から作成` を押します。
4. 作成したメッシュセットを選び、`選択` で再適用します。

#### メッシュセットの操作

| 操作 | 内容 |
|---|---|
| `選択から作成` | 現在の頂点／辺／面選択からセットを作成 |
| `選択` | メッシュセットを適用 |
| `選択を追加` | 現在の選択をアクティブメッシュセットへ追加 |
| `選択を削除` | 現在の選択をアクティブメッシュセットから削除 |
| `削除` | アクティブメッシュセットを削除 |

複数メッシュを同時に Edit Mode で編集している場合は、同名のメッシュセットをまとめて扱えます。

---

### 4. TP Smart Local View を使う

デフォルトでは、3D View 上で `Numpad /` を押すと TP Smart Local View を実行できます。  
ツールヘッダーの目玉ボタンからも操作できます。

| 操作 | 内容 |
|---|---|
| クリック / `Numpad /` | Local View の開始／終了 |
| `Shift + クリック` | 選択中の対象へ 1 階層深く入る |
| `Alt + クリック` | 1 階層戻る |

例:

1. キャラクター全体を選択して Local View に入る
2. その中から腕だけ選択して `Shift + クリック`
3. 腕の中から指だけ選択してさらに `Shift + クリック`
4. `Alt + クリック` で腕の階層へ戻る
5. 通常クリックで Local View を終了

現在の階層は `Local View — Level 1` のように 3D View 上へ表示されます。

---

## アドオン設定

`Edit > Preferences > Add-ons > ToPu: SmartSelection` から設定できます。

| 設定 | 内容 |
|---|---|
| UI Language | UI とツールチップの表示言語を切り替え |
| Keep Selection on Apply | セット適用時に現在の選択を保持 |
| Show icon in Tool Header | 3D View ツールヘッダーの目玉ボタン表示 |
| Auto switch to Mesh mode in Edit Mode | Edit Mode 時にメッシュモードへ自動切替 |
| キーマップを修復 | 壊れた／重複したキーマップを掃除して再登録 |

---

## デフォルトキーマップ

| キー | 内容 |
|---|---|
| `Numpad /` | TP Smart Local View |
| `Ctrl + J` | Join Objects (keep Mesh Sets) |

キーマップが登録されていない、または重複している場合は、アドオンプリファレンスの `キーマップを修復` を実行してください。

---

## トラブルシューティング

### 日本語が文字化けする

Blender の Interface Font が日本語に対応していない可能性があります。  
`Edit > Preferences > Interface > Text Rendering > Interface Font` で、Noto Sans CJK などの CJK 対応フォントを指定してください。

### `Numpad /` が使えない

テンキーのないキーボードの場合は、Blender の Keymap 設定から `TP Smart Local View` に別のショートカットを割り当ててください。

### Local View の状態がずれた

通常の Local View 操作、モード切替、アドオン再読み込みなどで状態がずれた場合は、一度 Local View を終了してから再実行してください。  
キーマップが原因の場合は `キーマップを修復` も試してください。

### メッシュ統合後にメッシュセットを残したい

Object Mode で `Ctrl + J` を使うと、このアドオンの `Join Objects (keep Mesh Sets)` が実行されます。  
通常の Join よりも、各オブジェクトが持っていたメッシュ選択セットを統合後のメッシュに残しやすくなります。

---

## 現在の対応範囲

| 対象 | 対応 |
|---|---|
| Object Mode | 選択セット / Smart Local View |
| Collection | コレクション選択 / Local View on Select |
| Mesh Edit Mode | メッシュ選択セット / Mesh Local |
| Curve Edit Mode | Edit Local |
| Surface Edit Mode | Edit Local |
| Armature Edit Mode | Edit Local |
| Metaball Edit Mode | Edit Local |
| Lattice Edit Mode | 現時点では未対応 |

---

## 開発メモ

このアドオンは、複雑な Blender シーンで「選択」と「表示範囲」を扱いやすくするために作成しています。  
大規模なモデルや複数オブジェクト編集でも使いやすいよう、メッシュ要素の GUID 保存、Local View 階層、軽量な状態同期を中心に実装しています。

不具合報告や要望は GitHub Issues へお願いします。

---

## Author

- http4211

## License

GPL-3.0-or-later
