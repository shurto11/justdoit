# justdoit

ターミナル上で画像をASCIIアート化し、**「Just」→ 「Do It」** を同じ位置で差し替え表示する、ちょっとした気合い注入ツールです。ループ再生にも対応しています。

やる気が足りないときは `justdoit`。

## 仕組み

1. `justdoit11.png`（Just）と `justdoit12.png`（Do It）を [jp2a](https://github.com/cslarsen/jp2a) でターミナル幅に合わせてASCIIアート化します。
2. [figlet](http://www.figlet.org/) で「Just」「Do It」のバナーを中央寄せで描画します。
3. 1枚目を表示すると同時に音声（`justdoit.mp3`）を [mpg123](https://www.mpg123.de/) で再生し、1秒後に同じ位置で2枚目へ差し替えます。
4. ターミナルの幅・高さに合わせて自動でサイズをフィットさせるため、画面からはみ出しません。

## 必要なもの

以下のコマンドが必要です。

| コマンド | 用途 | 備考 |
| --- | --- | --- |
| `bash` | 実行シェル | bash 4以上（`mapfile` / `local -n` を使用） |
| [`jp2a`](https://github.com/cslarsen/jp2a) | 画像のASCIIアート化 | 必須 |
| [`figlet`](http://www.figlet.org/) | テキストバナー描画 | 必須 |
| [`mpg123`](https://www.mpg123.de/) | 効果音の再生 | 任意（無ければ無音で動作） |
| `tput` | 端末サイズ取得・カーソル制御 | 通常はncursesに同梱 |

### インストール例

**Debian / Ubuntu**

```bash
sudo apt install jp2a figlet mpg123 ncurses-bin
```

**macOS (Homebrew)**

```bash
brew install jp2a figlet mpg123
```

**Arch Linux**

```bash
sudo pacman -S jp2a figlet mpg123
```

## インストール

リポジトリを取得して実行権限を付与します。

```bash
git clone https://github.com/shurto11/justdoit.git
cd justdoit
chmod +x justdoit
```

`PATH` の通ったディレクトリにシンボリックリンクを張っておくと、どこからでも呼び出せます（スクリプトは実体のディレクトリを解決して画像・音声を読み込むため、リンク経由でも正しく動作します）。

```bash
ln -s "$PWD/justdoit" ~/.local/bin/justdoit
```

## 使い方

一度だけ表示（Just → 1秒後に Do It で停止）：

```bash
justdoit
```

ループ再生（Just を1秒 → Do It を2秒、を繰り返し。各サイクルの先頭で効果音を再生）：

```bash
justdoit --loop
```

ループ中はカーソルが非表示になります。`Ctrl-C` で停止すると、効果音を止めてカーソルを復帰させて終了します。

## ファイル構成

| ファイル | 説明 |
| --- | --- |
| `justdoit` | 本体スクリプト |
| `justdoit11.png` | 1枚目の画像（Just） |
| `justdoit12.png` | 2枚目の画像（Do It） |
| `justdoit.mp3` | 効果音 |

> **Note**: 画像・音声はスクリプトと同じディレクトリに置く必要があります。差し替えれば、好きな画像・効果音でカスタマイズできます。

## ライセンス

スクリプト本体は自由に利用・改変いただけます。同梱の画像・音声素材を再配布する場合は、各素材の権利にご注意ください。
