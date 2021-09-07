---
title: 'Getting Startedで使用するツールについて'
linkTitle: 'Getting Startedで使用するツールについて'
date: 2021-09-03T14:17:37+09:00
type: docs
---

　rehearsalは **「言語・デバイス・目的の壁を越えて」** をコンセプトに開発されているので、本来は自分の普段使用している言語・環境で実践するべきだと考えています。

しかし、残念ながら何らかの言語を用いてGetting Startedを書かなければいけません。このGetting Startedでは、主に基本的なPythonの標準入出力のみを使用して進めていくので基本的な部分を確認します。

## インストール
### Python
　すでにPython環境があるかどうかを確認し、ない場合はインストールを行ってください。任意のディレクトリでターミナル（`bash` , `powershell` , `cmd` など）を開き、以下のコマンドを実行します（バージョンによって表示内容は異なる場合があります）。
```sh
$ python --version
Python 3.9.5
```
ダウンロードは[公式](https://www.python.org/downloads/)より配布されている物がよいでしょう。

### C++(gcc)
　すでにC++環境があるかどうかを確認し、ない場合はインストールを行ってください。
任意のディレクトリでターミナル（`bash` , `powershell` , `cmd` など）を開き、以下のコマンドを実行します（バージョンなど、各環境によって表示内容は異なる場合があります）。
```sh
$ g++ -v
Using built-in specs.
COLLECT_GCC=C:\tools\msys64\mingw64\bin\g++.exe
COLLECT_LTO_WRAPPER=C:/tools/msys64/mingw64/bin/../lib/gcc/x86_64-w64-mingw32/10.3.0/lto-wrapper.exe
Target: x86_64-w64-mingw32
Configured with: ../gcc-10.3.0/configure --prefix=/mingw64 --with-local-prefix=/mingw64/local --build=x86_64-w64-mingw32 --host=x86_64-w64-mingw32 --target=x86_64-w64-mingw32 --with-native-system-header-dir=/mingw64/x86_64-w64-mingw32/include --libexecdir=/mingw64/lib --enable-bootstrap --enable-checking=release --with-arch=x86-64 --with-tune=generic --enable-languages=c,lto,c++,fortran,ada,objc,obj-c++,jit --enable-shared --enable-static --enable-libatomic --enable-threads=posix --enable-graphite --enable-fully-dynamic-string --enable-libstdcxx-filesystem-ts=yes --enable-libstdcxx-time=yes --disable-libstdcxx-pch --disable-libstdcxx-debug --enable-lto --enable-libgomp --disable-multilib --disable-rpath --disable-win32-registry --disable-nls --disable-werror --disable-symvers --with-libiconv --with-system-zlib --with-gmp=/mingw64 --with-mpfr=/mingw64 --with-mpc=/mingw64 --with-isl=/mingw64 --with-pkgversion='Rev2, Built by MSYS2 project' --with-bugurl=https://github.com/msys2/MINGW-packages/issues --with-gnu-as --with-gnu-ld --with-boot-ldflags='-pipe -Wl,--dynamicbase,--high-entropy-va,--nxcompat,--default-image-base-high -Wl,--disable-dynamicbase -static-libstdc++ -static-libgcc' 'LDFLAGS_FOR_TARGET=-pipe -Wl,--dynamicbase,--high-entropy-va,--nxcompat,--default-image-base-high' --enable-linker-plugin-flags='LDFLAGS=-static-libstdc++\ -static-libgcc\ -pipe\ -Wl,--dynamicbase,--high-entropy-va,--nxcompat,--default-image-base-high\ -Wl,--stack,12582912'
Thread model: posix
Supported LTO compression algorithms: zlib zstd
gcc version 10.3.0 (Rev2, Built by MSYS2 project) 
```
ダウンロードはlinux仮想環境をインストールして同梱のものを用いるか、WindowsであればMSYS2を使用してgccをインストールするのがよいでしょう。

## 標準入出力
### Python
　Pythonの標準入出力系の関数を確認します。 rehearsalのGetting Startedで使用する関数は **2個** しかありません。これはどれだけ複雑な組み合わせをしていても変わりません。
```python
str s
input(s)                     # 標準入力
println("Hello World, " + s) # 標準出力・標準エラー出力（改行含む）
```
`input()`, `print()` はどちらも言語に組み込まれている関数で、それぞれ標準入力からのデータ取得、標準出力への書き込みを行います。
### C++
　C++の標準入出力系の関数を確認します。rehearsalのGetting Startedで使用する関数は **2個** しかありません。
```c++
#include <bits/stdc++.h>
using namespace std;

int main() {
    string s;
    cin >> s;                               // 標準入力
    cout << "Hello World, " + s << endl;    // 標準出力（改行含む）
    cerr << "OK" << endl;                   // 標準エラー出力（改行を含む、今回は使用しない）
    return 0;
}
```

これらに相当する関数は各言語ある（と思っている）ので、Python以外を使用する方はそれらを利用してください。ただし、言語に組み込まれている関数の中には、Go言語の [`(builtin).print()`](https://pkg.go.dev/builtin#print) 関数など、標準エラー出力に書き込む関数もあるためその確認もしておくとよいでしょう。

## テキストエンコーディングについて
　残念ながら、開発者の力不足により異種のエンコーディングをrehearsal内部で変換する実装が行えていません。rehearsalとしては、一般的なutf-8の使用を推奨しています。
