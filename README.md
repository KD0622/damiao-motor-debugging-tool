# DMTool

[日本語](./README.md) | [EN](./README.en.md)

このドキュメントは、現在のディレクトリ内に実際に存在するファイルに基づいて作成されており、直接配布される DMTool のインストールパッケージおよび実行パッケージに適用されます。
また、supporting_documentsにはGiteeから入手されるファイルを含んでいます。具体的には、DAMIAOに関するGiteeとDM2325のデータシートなどを含んでいます。

## ディレクトリの内容

現在のリポジトリのルートディレクトリには、以下の実行可能リソースが含まれています：

- `Windows/x86_64/DMTool 2.1.6.7.exe`
- `Linux/x86_64/DMTool-v2.1.6.7-x86_64.AppImage`
- `Linux/x86_64/arch_lib_install.sh`
- `Linux/arm64/DMTool-v2.1.6.7-arm64/start.sh`
- `MacOS/x86_64/DMTool-v2.1.6.7-x86_64.app`
- `MacOS/arm64/DMTool-v2.1.6.7-arm64.app`
- `DMTool上位机软件说明书.pdf`

## Windows

対象ファイル：

- `Windows/x86_64/DMTool 2.1.6.7.exe`

使用方法：

1. `Windows/x86_64/` フォルダに移動します。
2. `DMTool 2.1.6.7.exe` をダブルクリックして実行します。
3. 初回実行時にシステムによってブロックされた場合は、「詳細情報」を選択してから実行を続けてください。

説明：

- 現在のディレクトリには、`x86_64`版の Windowsインストールパッケージのみが用意されています。
- デバイスドライバ、権限、またはシリアルポートへのアクセスに関する問題が発生した場合は、まず `DMTool PC用ソフトウェア取扱説明書.pdf` を参照してください。

## Linux

対象ファイル：

- `Linux/x86_64/DMTool-v2.1.6.7-x86_64.AppImage`
- `Linux/x86_64/arch_lib_install.sh`

### 一般的な実行手順

1. `Linux/x86_64/` ディレクトリに移動します。
2. AppImage に実行権限を付与します：

```bash
chmod +x DMTool-v2.1.6.7-x86_64.AppImage
```

3. プログラムを実行する：

```bash
./DMTool-v2.1.6.7-x86_64.AppImage
```

### Arch Linux の追加依存関係

Arch Linux または互換性のあるディストリビューションでライブラリが不足している場合は、まず次のコマンドを実行してください：

```bash
chmod +x arch_lib_install.sh
./arch_lib_install.sh
```

その後、AppImageを再実行してください。

### USBデバイスの権限

プログラムがUSB/CANデバイスにアクセスできない場合は、まずデバイス情報を確認してください：

```bash
lsusb
```

現在のデバイスのアクセス権限を解除するには、ディストリビューションの設定に従って `udev` ルールを設定します。一般的な例：

Debian / Ubuntu:

```bash
echo 'SUBSYSTEM=="usb", ATTR{idVendor}=="34b7", ATTR{idProduct}=="6877", MODE="0666", GROUP="plugdev"
SUBSYSTEM=="usb_device", ATTR{idVendor}=="34b7", ATTR{idProduct}=="6877", MODE="0666", GROUP="plugdev"' | sudo tee /etc/udev/rules.d/99-dm-fdcan.rules > /dev/null
sudo udevadm control --reload-rules
sudo udevadm trigger
sudo usermod -aG plugdev $USER
```

Arch Linux:

```bash
echo 'SUBSYSTEM=="usb", ATTR{idVendor}=="34b7", ATTR{idProduct}=="6877", MODE="0666", GROUP="uucp", TAG+="uaccess"
SUBSYSTEM=="usb_device", ATTR{idVendor}=="34b7", ATTR{idProduct}=="6877", MODE="0666", GROUP="uucp", TAG+="uaccess"' | sudo tee /etc/udev/rules.d/99-dm-fdcan.rules > /dev/null
sudo udevadm control --reload-rules
sudo udevadm trigger
sudo usermod -aG uucp $USER
```

実行が完了したら、一度システムに再ログインしてから、DMToolを起動することをお勧めします。

## macOS

対象ファイル：

- Intel: `MacOS/x86_64/DMTool-v2.1.6.7-x86_64.app`
- Apple Silicon: `MacOS/arm64/DMTool-v2.1.6.7-arm64.app`

使用方法：

1. チップのアーキテクチャに応じて、対応するディレクトリに移動します
2. `.app` をダブルクリックして起動します
3. Gatekeeper によってブロックされた場合は、「システム設定」→「プライバシーとセキュリティ」で、今回のみ開くことを許可してください

- `x86_64` ディレクトリは、Intel Mac 向けです。
- `arm64` ディレクトリは、Apple Silicon Mac 向けです。
- 現在のディレクトリ内の `.app` には、実行に必要なフレームワークとリソースファイルがすでに含まれています。

## 関連ドキュメント

- 詳細な使用説明：`DMTool PC用ソフトウェア取扱説明書.pdf`
- 変更履歴：[`CHANGELOG.md`](./CHANGELOG.md)

## バージョン

- 現在のディレクトリにある DMTool のバージョン：`2.1.6.7`

#### 著作権およびサードパーティのライセンス

1. **ソフトウェアの著作権**
本ソフトウェアはクローズドソースソフトウェアであり、著作権は達妙科技有限公司に帰属します。

2. **サードパーティ製コンポーネントに関する声明**
本ソフトウェアのコアプログラムはプロプライエタリソフトウェアです。開発過程では、オープンソースライセンスに準拠したオープンソースライブラリが使用されています。具体的には以下の通りです：

Qt ライブラリ：GNU Lesser General Public License version 2.1 (LGPLv2.1) または version 3 (LGPLv3) に準拠しています。使用されているモジュールには、`QtCore`、`QtGui`、`QtSerialPort`、`QtCore5Compat`、`QtSql`、`QtOpenGL` が含まれます。

Copyright (C) 2025 The Qt Company Ltd. All rights reserved.
Qwt ライブラリ：GNU Lesser General Public License バージョン 2.1 (LGPLv2.1) に準拠しています。

libusb ライブラリ：GNU Lesser General Public License バージョン 2.1 (LGPLv2.1) に準拠しています。

ユーザーは、上記のオープンソースライセンスの要件に従い、対応するサードパーティ製コンポーネントのソースコードを取得、変更、および再配布することができます。現在のディレクトリにあるプログラムは、関連するライセンスの要件を満たすため、これらのライブラリを動的リンク方式で利用しています。
