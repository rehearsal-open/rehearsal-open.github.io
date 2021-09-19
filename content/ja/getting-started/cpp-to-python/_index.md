---
title: 'Cpp to Python'
linkTitle: 'Cpp to Python'
date: 2021-09-03T15:30:18+09:00
type: docs
weight: 20
description: この章ではPythonで書かれた2種類のプログラムを用いて、実際にrehearsalの使い方を解説します。
---

Getting Startedでは、C++とPythonの四則演算について考えることにします。
Pythonが
```
<整数> <演算子> <整数>
```
と出力するので、その結果をC++のプログラムに
```
<計算結果>
```
という形で答えてもらいます。
このソースコードは[github.com/rehearsal-open/template-sample/getting-started](https://github.com/rehearsal-open/template-sample/tree/main/getting-started)に公開しています。

## コーディング{#code}

それでは、実際にコードを書いていきましょう。下図のようなファイル構成です。
```md
 ┣ answer.cpp
 ┣ quiz.py
 ┗ rehearsal.yml
```

ひとつずつファイル構成を見てみましょう

### ./answer.cpp{#code-answer_cpp}

C++側のコードです。単純に入力を受け取り、計算結果を出力しています。わざと間違えるように`int`型でのみ計算を行います。
```cpp
// ./answer.cpp

#include <iostream>
#include <string>
using namespace std;

int main() {

    for (auto i = 0; i < 1000; i++) {
        int a, b;
        string ope;

        // input line to get question
        cin >> a >> ope >> b;

        // output answer
        switch (ope[0]) {
        case '+': cout << a + b << flush << endl; break;
        case '-': cout << a - b << flush << endl; break;
        case '*': cout << a * b << flush << endl; break;
        case '/': cout << a / b << flush << endl; break;
        case '%': cout << a % b << flush << endl; break;
        }
    }
}
```
このコードを実行した場合、1000問出題する必要があるため、とても手動では行うことができません。

### ./quiz.py{#code-quiz_py}
Python側のコードです。問題を作成し、出力、Pythonとしての答えを計算してからC++の回答を取得し、それらを最後に一覧として表示します。確認のためにPythonのファイル出力でも最後の一覧を出力しておきます。

```python

# ./quiz.py

import random

nQuiz = 1000
data = []

f = open(file="out.txt", mode='w')

for i in range(nQuiz):
    
    # make quiz
    first = random.choice(range(1, 100000))
    second = random.choice(range(1, 100000))
    operator = random.choice(["+", "-", "*", "/", "%"])

    # please flush property true
    print(first, operator, second, sep=" ", flush=True)

    # get python's answer
    pyAns = 0
    if operator == "+":
        pyAns = first + second
    if operator == "-":
        pyAns = first - second
    if operator == "*":
        pyAns = first * second
    if operator == "/":
        pyAns = first / second
    if operator == "%":
        pyAns = first % second

    # get c++'s answer
    cppAns = input()

    # compare with table
    data.append([first, operator, second, pyAns, cppAns])

for i in range(nQuiz):
    first, operator, second, pyAns, cppAns = data[i][0], data[i][1], data[i][2], data[i][3], data[i][4]
    # please flush property true
    print(str(first)+" "+operator+" "+str(second)+" = (python: "+str(pyAns)+", cpp: "+cppAns+")", flush=True)
    print(str(first)+" "+operator+" "+str(second)+" = (python: "+str(pyAns)+", cpp: "+cppAns+")", file=f)
```

### ./rehearsal.yml{#code-rehearsal_yml}
最後にrehearsal.ymlです。それぞれのタスクのリレーションを組みます。`build`フェイズでC++のビルドを行ってから実行を行います。
```yaml
# ./rehearsal.yml, uses version 1.202109

version: 1.202109
phase:
- name: build # build and set environments
  task:
  - name: gcc_build
    kind: cui
    cmd: g++
    args: [answer.cpp, -o, answer]
    stdout:
      write-log: true
    stderr:
      write-log: true
- name: run_task  # cpp executable file
  task:
  - name: cpp
    kind: cui
    cmd: ./answer.exe
    stdout:
      write-log: true
      sendto:
        - python
  - name: python # run python script
    kind: cui
    cmd: python
    args: [quiz.py]
    stdout:
      write-log: true
      sendto:
        - cpp
```

## 実行{#run}
善は急げです。すべて書き終えたらさっそく実行してみましょう。シェルを開いて`rehearsal-cli run -p ./rehearsal.yml`を実行します。問題生成はランダムであるため問題の内容はおそらく異なります。
```sh
$ rehearsal-cli run -p ./rehearsal.yml

[INFO]:  start phase (1 / 5)
[INFO]:  __init::__frontend_logger was started.
[INFO]:  start phase (2 / 5)
[INFO]:  build::gcc_build was started.
[INFO]:  build::gcc_build has been already stopped.
[INFO]:  start phase (3 / 5)
[INFO]:  run_task::cpp was started.
[INFO]:  run_task::python was started.
run_task::python(standard output)       : 71191 * 98267
run_task::cpp(standard output)          : -1594208595
run_task::python(standard output)       : 97901 - 46723
run_task::cpp(standard output)          : 51178
...
<中略>
...
run_task::python(standard output)       : 50414 / 28825 = (python: 1.7489679098005204, cpp: 1)
run_task::python(standard output)       : 78334 * 78476 = (python: 6147338984, cpp: 1852371688)
run_task::python(standard output)       : 99560 - 33870 = (python: 65690, cpp: 65690)
run_task::python(standard output)       : 82352 / 43550 = (python: 1.89097588978186, cpp: 1)
run_task::python(standard output)       : 38297 % 12706 = (python: 179, cpp: 179)
run_task::python(standard output)       : 35321 - 34331 = (python: 990, cpp: 990)
run_task::python(standard output)       : 62255 % 37346 = (python: 24909, cpp: 24909)
run_task::python(standard output)       : 56890 / 71068 = (python: 0.8005009286880171, cpp: 0)
[INFO]:  run_task::cpp has been already stopped.
[INFO]:  run_task::python has been already stopped.
[INFO]:  start phase (4 / 5)
[INFO]:  start phase (5 / 5)
[INFO]:  __init::__frontend_logger was stopped.
```
このように表示されたら完了です。

## これが終わったら？{#ended}
[ドキュメント](/documents)であなたがしたいことを見つけましょう。rehearsalはあなたがやりたいこと、確かめたいことを必ずや実現してくれるはずです。
