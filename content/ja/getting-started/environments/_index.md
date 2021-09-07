---
title: '環境構築'
linkTitle: '環境構築'
date: 2021-09-03T13:47:49+09:00
type: docs
weight: 10
description: この章ではrehearsalのインストール方法、Getting Startedで使用するツールについて解説します。
---

# rehearsalのインストール

## rehearsalのダウンロード

### 1) GitHub Releasesからのダウンロード（推奨）
　こちらからダウンロードしてください[（GitHub releases）]({{<val "latest_url">}})。その際にダウンロードしたファイルは環境変数 `$PATH` に含まれているディレクトリに含めることを推奨します。

### 2) `go` を用いたダウンロード（開発者向け）
　`go` 開発環境を用いてターミナル上でインストールを行います。

1.  [go](https://golang.org/dl/) をインストールし、任意のディレクトリでターミナル（`bash` , `powershell` , `cmd` など）を開き、 `go version` で `$PATH` が通っているかを確認してください。通っていない場合は環境変数を編集してください。

1. 次に、以下のコマンドを実行します。
   ```sh
   $ go install github.com/rehearsal-oepn/rehearsal/rehearsal-cli@latest
   ```

### インストールの確認方法
　任意のディレクトリでターミナル（`bash` , `powershell` , `cmd` など）を開き、以下のコマンドを実行します（バージョンによって表示内容は異なる場合があります）。
```sh
$ rehearsal-cli version
  
rehearsal v1.202109 Copyright (C) 2021  Kasai Koji
  
This program comes with ABSOLUTELY NO WARRANTY; for details type 'rehearsal-cli version'.   
This is free software, and you are welcome to redistribute it
under certain conditions; type 'rehearsal-cli version' for details.


 /        ____     ____    _  _     ____    __     ____     ___     __     _
 \(o)    /____\   /____\  //  \\   /____\  /__\   /____\   /___\   /__\   //
   \\_  //____\\ //_____ //____\\ //_____ //  \\ //____\\ //___   //  \\ //
   /\  // \ ___//______//______ //______///___//// \ ___//____ \ //___////
  /  \ \\_ \\__ \\_____ \\  _ ////_____ / ____ \\\_ \\__ ____/ // ____ \\\______
_/\  /\_\_\ \__\ \____/  \\ \_/ \_____//_/    \_\\_\ \__\\____//_/    \_\\_____/


rehearsal v1.202109 / process-conecting test tool
Copyright (C) 2021  Kasai Koji

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.
This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.
You should have received a copy of the GNU General Public License
along with this program.  If not, see <https://www.gnu.org/licenses/>.
```
