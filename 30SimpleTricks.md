# Python のコーディングを上達させるための30のヒント

* (原文: [30 Simple Tricks to Level Up Your Python Coding](https://medium.com/better-programming/30-simple-tricks-to-level-up-your-python-coding-5b625c15b79a))

現在、汎用的なプログラミング言語としての Python はほとんど全ての産業と学術分野に浸透しています。生体医科学といった分野の場合、私自身を含めてかなりの数の Python プログラマは、例えば Matlab、C/C++、Java、JavaScript、そして Swift などを使った様々なプログラミングの経験を持ってはいるものの、コーディングをしたことがない人が居ることも事実です。

彼らにとって Python は「外国語」でもあるため、そのコーディングについてしっかりとしたトレーニングを受けておらず、またその言語特有の特徴を利用した開発手法を知らない人も居るかもしれません。


だからといって誤解しないで下さい。プログラムが意図した目的を満足しているのであれば、依然としていろいろな方法で素晴らしいコードを書くことができます。したがって、私の場合だと Python らしくないコードを書くことだって許容できるのです。

しかし外国人である私がアメリカへ来て英語の発音を改善しようと日々努力しているのと同じように、できるだけ Python らしいコードを書きたいと考えています。この記事では、私が過去数年間にわたって蓄積してきた Python 特有の使い方をいくつか紹介します。これらがあなたの Python プログラミングのレベルアップに役に立つことを願っています。

---

## 1. シーケンスをスライスする

いくつか共通なシーケンス型にリスト、タプル、そして文字列があります。ここで別のシーケンスをスライスすると新しいシーケンスを生成できます。次に示す処理では例としてリストを使っていますが、もちろんタプルや文字列、そしてその他のシーケンス型（例えばバイト）にも適用できます。

```python
 In [3]: a = [0, 2, 4, 6, 8, 10, 12, 14, 16, 18, 20]

# 範囲 [開始, 終了) を指定する
 In [4]: a[1:3]
 Out[4]: [2, 4]

# ステップ付きの範囲を指定する
 In [5]: a[1:9:2]
 Out[5]: [2, 6, 10, 14]

# 「開始」を省略する - 強制的に「開始」は0
 In [6]: a[:5]
 Out[6]: [0, 2, 4, 6, 8]

# 「終了」を省略する - 強制的に「終了」は一番最後の要素
 In [7]: a[9:]
 Out[7]: [18, 20]

# リスト全体
 In [8]: a[:]
 Out[8]: [0, 2, 4, 6, 8, 10, 12, 14, 16, 18, 20]

```

## 2. シーケンスを反転する

まれにシーケンスを反転させたい時があります。``for`` ループを使うという手もありますが、もっと明快な方法があります。これは上のヒントと同様に、処理がシーケンスに適用できるのであれば通常は文字列、タプル、そしてリストが全てこの機能をサポートしています。

 ```python
 In [9]: a = (1, 2, 3, 4, 5)

 In [10]: a[::-1]
 Out[10]: (5, 4, 3, 2, 1)

 In [11]: b = 'start'

 In [12]: b[::-1]
 Out[12]: 'trats'

 ```

## 3. 逆向きのインデックスを利用してシーケンスにある要素にアクセスする

シーケンスの終端に向かって要素にアクセスしたいのであれば、逆順でアクセスした方が楽です。Python のシーケンスの場合、終端の要素は ``-1`` と云うインデックスを持ち、その一つ前の要素は ``-2`` と云うインデックス持ち、以下、同じようなインデックスを持っています。

 ```python
 In [17]: a = 'Hello World!'

# a[len(a)-1] を使う代わりに
 In [18]: a[-1]
 Out[18]: '!'

# スライスと連携して
 In [19]: a[-6:-1]
 Out[19]: 'World'

 ```

## 4. 複数回の代入

幾つかの変数に特定の値をそれぞれ代入したい時は、代入を複数回おこなうことができます。同じ書き方を利用して二つの変数を入れ替えたり、あるいはリストの中の二つの要素を入れ替えることもできます。この機能は、その処理の裏で、あとで紹介するタプルのアンパックに密接に関係しています。

 ```python
# a = 8; b = 5 をする代わりに
 In [24]: a, b = 8, 5

 In [25]: print(f'a is {a}; b is {b}')
 a is 8; b is 5

# 二つの変数を入れ替える
 In [26]: a, b = b, a

 In [27]: print(f'a is {a}; b is {b}')
 a is 5; b is 8

# リストの中にある先頭と最後の要素を入れ替える
 In [28]: numbers = [1, 2, 3, 4, 5]

 In [29]: numbers[0], numbers[-1] = numbers[-1], numbers[0]

 In [30]: numbers
 Out[30]: [5, 2, 3, 4, 1]

 ```

## 5. シーケンスが空かどうかチェックする

いくつかの操作は、リストやタプルなどシーケンスが空ではない時にだけ意味があり、操作を適切なものにするために事前にチェックしておく必要があります。そのため ``not`` キーワードを使って、例えば ``not []`` のようなシーケンスの否定ができます。これはシーケンスが空の場合は ``True`` と評価します。さらに他の二つの一般的なデータ型である ``dict`` と ``set`` を使っても同じようなことができます。

 ```python
 In [31]: empty_list = [{}, '', [], set()]

 In [32]: for item in empty_list:
 ...:     if not item:
 ...:         print(f'Do something with the {type(item)}')
 ...:
 Do something with the <class 'dict'>
 Do something with the <class 'str'>
 Do something with the <class 'list'>
 Do something with the <class 'set'>

 ```

## 6. リスト内包表記

Python の便利な機能の一つにリスト内包表記（ _List Comprehensions_ ）があります。これを使うと、とても簡単にリストを生成できます。リスト内包表記には ``[式 for 要素 in イテラブル if 条件]`` という一般的な書き方があります。

 ```python
 In [33]: a = {1, 2, 3, 4, 5}

 In [34]: [x*2 for x in a]
 Out[34]: [2, 4, 6, 8, 10]

 In [35]: [x*3 for x in a if x%2 == 1]
 Out[35]: [3, 9, 15]

 ```

## 7. セット内包表記

セット内包表記 ( _Set Comprehensions_ ) の使い方は、上で紹介したリスト内包表記に似ています。違いは、大括弧 ``[]`` の代わりに中括弧 ``{}`` を使用する点です。さらに ``set`` 型の定義で重複した要素は削除される点が違います。

 ```python
 In [36]: a = [1, -2, 2, -3, 3, 4, 5, 5, 5]

 In [37]: {x*x for x in a}
 Out[37]: {1, 4, 9, 16, 25}

 ```

## 8. ディクショナリ内包表記

リスト内包表記やセット内包表記の他に、内包表記の機能にはディクショナリ型の生成にも利用できるものがあります。``dict`` 型の中にはキーと値のペアがいくつか含まれているので、ディクショナリ内包表記 ( _Dictionary Comprehensions_ ) にはコロンによって区切られたキーと値の機能が含まれます。

 ```python
 In [38]: a = {1, 2, 3, 4, 5}

 In [39]: {x: x*x for x in a}
 Out[39]: {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

 ```

## 9. ジェネレータ式

Python の「ジェネレータ」はイテレータを生成する便利な方法の一つです。ジェネレータは「なまけ者」（つまり、要求された時に初めて必要なアイテムを生成する）なので、ジェネレータはとてもメモリ効率がよいです。ジェネレータを生成する特別な方法は「ジェネレータ式」を呼び出すことです。ジェネレータ式は構文的にリスト内包表記に似ていますが、大括弧 ``[]`` の代わりに括弧 ``()`` を使います。

次の例で、イテレータを受け取ることが可能な関数の中で直接ジェネレータを使用する場合は括弧 ``()`` を省略できます。

 ```python
 In [13]: sum(x**2 for x in range(100))
 Out[13]: 328350

 In [14]: max(x*x for x in range(100))
 Out[14]: 9801

# 冗長になるので、関数の中で括弧は必要ない
 In [18]: min((x*-2 for x in range(100)))
 Out[18]: -198

 ```

## 10. タプルのアンパック

タプルは Python の中でよく使われるデータ構造の一つです。タプルはまさに関連しあう値をまとめたグループであり、一般的な使用法には、それらの要素へのアクセスが含まれます。インデックスを使っても要素にアクセスできますが、アンパックを使う方がもっと便利です。その際はアンダースコア ``_`` を使って不要な要素を指定し、アスタリスク ``*`` を使って名前付きの要素以外の残りの要素を指定できます。


 ```python
 In [19]: items = (0, 'b', 'one', 10, 11, 'zero')

 In [20]: a, b, c, d, e, f = items

 In [21]: print(f)

 In [22]: a, *b, c = items

 In [23]: print(b)
 ['b', 'one', 10, 11]

 In [24]: *_, a, b = items
 In [25]: print(a)
 11

 ```

## 11. ループで Enumerate() を使う

``enumerate()`` 関数はイテラブルを一つ受け取り、イテレータを生成します。さらに反復する回数を追跡することができます。オプションでカウントを始める数値を指定できます（デフォルトは ``0`` からカウント）。


 ```python
 In [26]: students = ('John', 'Mary', 'Mike')

 In [27]: for i, student in enumerate(students):
    ...:     print(f'Iteration: {i}, Student: {student}')
    ...:
 Iteration: 0, Student: John
 Iteration: 1, Student: Mary
 Iteration: 2, Student: Mike

 In [28]: for i, student in enumerate(students, 35001):
    ...:     print(f'Student Name: {student}, Student ID #: {i}')
    ...:
 Student Name: John, Student ID #: 35001
 Student Name: Mary, Student ID #: 35002
 Student Name: Mike, Student ID #: 35003

 ```


## 12. ループで Reversed() を使う

``reversed()`` 関数は、イテラブルを逆順に並べたものでイテレータを生成する際にループと一緒に使うことがよくあります。

 ```python
 In [29]: tasks = ['laundary', 'picking up kids', 'gardening', 'cooking']

 In [30]: for task in reversed(tasks):
    ...:     print(task)
    ...:
 cooking
 gardening
 picking up kids
 laundary

 ```

## 13. Zip() 関数

``zip()`` は複数のイテラブルを1対1で対応させ、その結果を連結するのに便利な関数です。特定のイテラブルが最短を超えると捨てられます。さらに ``zip()`` 関数でアスタリスク記号 ``*`` を使うとイテレータの要素を展開し、それぞれ変数に格納することも可能です。

 ```python
 In [36]: students = ('John', 'Mary', 'Mike')

 In [37]: ages = (15, 17, 16)

 In [38]: scores = (90, 88, 82, 17 ,14)

 In [39]: for student, age, score in zip(students, ages, scores):
    ...:     print(f'{student}, age: {age}, score: {score}')
    ...:
 John, age: 15, score: 90
 Mary, age: 17, score: 88
 Mike, age: 16, score: 82

 In [41]: zipped = zip(students, ages, scores)

 In [42]: a, b, c = zip(*zipped)

 In [43]: print(b)
 (15, 17, 16)

 ```


## 14. Lambda 式を使った並び替え

Lambda 式は、単一の式で複数の引数を受け取る無名関数（ _Anonymous Function_）です。この関数の一般的な使い方が ``sorted()`` 関数の中でその ``key`` 引数を指定するというものです。この他に、Lambda 式はいくつかの関数 (例えば ``max()``、``map()`` など) の中でもよく使用されます。この場合、``def`` キーワードを使って定義した通常の関数を単一の式で置き換えるということが可能です。

```python
In [44]: students = [{'name':'John', 'score':98},
    ...:             {'name':'Mike', 'score':94},
    ...:             {'name':'Jenifer', 'score':99}]

In [45]: students
Out[45]:
[{'name': 'John', 'score': 98},
 {'name': 'Mike', 'score': 94},
 {'name': 'Jenifer', 'score': 99}]

# Lambda 式を sort() の key にする
In [46]: sorted(students, key=lambda x : x['score'])
Out[46]:
[{'name': 'Mike', 'score': 94},
 {'name': 'John', 'score': 98},
 {'name': 'Jenifer', 'score': 99}]

```


## 15. 条件付き略式代入

これは、いわゆる「シンタックス・シュガー」と呼ばれる機能です。ある値を特定の条件に基づいて変数に代入したい場合、次の一般的な形式を使用して略式代入ができます： ``y = x if 条件 else another_x``

```python
In [47]: some_condition = True

In [48]: if some_condition:
    ...:     x = 5
    ...: else:
    ...:     x = 3
    ...: print(f'x is {x}')
x is 5

In [49]: x = 5 if some_condition else 3
    ...: print(f'x is {x}')
x is 5

```


## 16. コレクションでの存在確認 (Membership Testing)

たまに、コレクションやその中にある特定の要素に対して何か操作する前に対象となる要素の存在を確認したいときがあります。この場合は ``in`` キーワードを使います。

```python
In [55]: a = ('one', 'two', 'three', 'four', 'five')

In [56]: if 'one' in a:
    ...:     print('The tuple contains one.')
    ...:
The tuple contains one.

In [57]: b = {0:'zero', 1:'one', 2:'two', 3:'three'}

In [58]: if 2 in b.keys():
    ...:     print('The dict has the key of 2.')
    ...:
The dict has the key of 2.

```


## 17. ディクショナリから値を取得するときは Get() を使う

ディクショナリからキーに対応した値を取得する際、普通は角括弧 ``[]`` の中にキーを入れて指定します。しかしキーがディクショナリの中に存在ない場合はエラーが発生します。もちろん try/except 文を使ってエラーには対処できます。代わりに ``get()`` メソッドがあります。このメソッドは、もしディクショナリにキーが存在していない場合はデフォルト値を返します。

```python
In [59]: number_dict = {0:'zero', 1:'one', 2:'two', 3:'three'}

In [60]: number_dict[5]
---------------------------------------------------------------------------
KeyError                                  Traceback (most recent call last)
<ipython-input-60-a0eb05bc230d> in <module>
----> 1 number_dict[5]

KeyError: 5

In [61]: number_dict.get(5, 'None')
Out[61]: 'None'

```


## 18. ディクショナリの中で最大値のキーを取得する方法

ディクショナリを使っていると、たまに値が最大となるキーを見つけたいときがあります。まず最初に全ての値を要素としたリストの中から最大値のインデックスを見つけ出し、次に全てのキーを要素とするリストからインデックスに対応するものを見つけます。あるいは、もっと簡単な方法として ``max()`` 関数の引数 ``key`` を指定するというものがあります。

説明を簡単にするために、ディクショナリの中で最大値が重複することはないとします。さらには ``min()`` 関数を使用して最小値を見つけるために同じ方法が使えます。


```python
In [62]: model_scores = {'model_a': 100, 'model_b':198, 'model_c': 150}

# 典型的な方法
In [63]: keys, values = list(model_scores.keys()), list(model_scores.values())

In [64]: keys
Out[64]: ['model_a', 'model_b', 'model_c']

In [65]: values
Out[65]: [100, 198, 150]

In [66]: keys[values.index(max(values))]
Out[66]: 'model_b'

# 「ワンライナー」で書くと
In [67]: max(model_scores, key=model_scores.get)
Out[67]: 'model_b'

```


## 19. Print() 関数を使ってデバッグする

小規模なプロジェクトだと ``print()`` 関数がデバッグ時に役に立つことが多いです。さらに人に教えるような場面でも ``print()`` 関数をよく使います。我々がよく使う ``print()`` 関数のトリックがいくつかあります。一つ目は改行文字以外で文字の終端を指定するというもの。そして二つ目は ``f`` キーワードを使うことです。これにより評価可能な「式」を含む文字列を作成できます。

```python
In [68]: for i in range(5):
    ...:     print(i, end=', ' if i < 4 else '\n')
    ...:
0, 1, 2, 3, 4

In [69]: for i in range(5):
    ...:     print(f'{i} & {i+1}', end=', ' if i < 4 else '\n') 
    ...:
0 & 1, 1 & 2, 2 & 3, 3 & 4, 4 & 5

```

## 20. セイウチ演算子

「セイウチ演算子」（ _Walrus Operator_ ）と呼ばれる ``:=`` は Python 3.8 以上で利用できる新しい機能です。これは「代入式」（式の中にある変数へ代入する演算子）の別名です。通常、式の中で変数を使用する場合は先に宣言しておく必要があります。このセイウチ演算子を使うと、変数への代入を式の内部に含めることが可能になり、そして変数を直ぐに使用できるようになります。


```python
In [71]: a = ['j', 'a', 'k', 'd', 'c']

In [72]: if (n := len(a)) % 2 == 1: 
    ...:     print(f'The number of letters is {n}, which is odd.')
    ...:
The number of letters is 5, which is odd.

```


## 21. 文字列の分割

文字列を扱う時によく行うのが文字列を区切って単語のリストを生成するというものです。この場合は ``split()`` 関数を使用します。これは区切り文字を受け取る他に、オプションとして最大分割数を受け取ります。これと関連する関数が ``rsplit()`` です。これは、指定した最大分割数を満たすよう文字列の右から区切っていくことを除けば ``split()`` と同じです。

```python
In [73]: sentence = 'This is, a python, tutorial, about, idioms.'

In [74]: sentence.split(', ')
Out[74]: ['This is', 'a python', 'tutorial', 'about', 'idioms.']

In [75]: sentence.split(', ', 2)
Out[75]: ['This is', 'a python', 'tutorial, about, idioms.']

In [76]: sentence.rsplit(', ')
Out[76]: ['This is', 'a python', 'tutorial', 'about', 'idioms.']

In [77]: sentence.rsplit(', ', 2)
Out[77]: ['This is, a python, tutorial', 'about', 'idioms.']


```

## 22. 文字列を連結してイテラブルにする

文字列を操作する時、まれにリストやタプルといったイテラブルの中に含まれている複数の文字列を連結して単一の文字列にしたいときがあります。このような場合は区切り記号を引数にして ``join()`` 関数を呼び出します。


```python
In [78]: words = ('Hello', 'Python', 'Programmers')

In [79]: '!'.join(words)
Out[79]: 'Hello!Python!Programmers'

In [80]: words_dict = {0:'zero', 1:'one', 2:'two', 3:'three'}

In [81]: '&'.join(words_dict.values())
Out[82]: 'zero&one&two&three'


```

## 23. Map() 関数

``map()`` 関数は別の関数を引数にとるか、または返り値として関数を返す、いわゆる「高階関数（ _High-Order Function_）」の一つです。``map(関数, イテラブル)`` という書式で呼び出すと、イテラブルに対して「関数」を呼び出して、イテレータ型の ``map`` オブジェクトを返します。イテラブルの数は「関数」が受け取る必要がある引数の数と同じにして下さい。

次の例では、二つの引数を受け取る Python 標準の ``pow()`` 関数を使用しています。もちろん独自に作成した関数でも構いません。一点補足すると、``map()`` 関数を使ってリストを生成するような時、たいていの場合はリスト内包表記を使用しても同じ結果が得られます。


```python
In [84]: numbers = (1, 2, 4, 6)

In [85]: indices = (2, 1, 0.5, 2)

# map() を使った場合
In [86]: list(map(pow, numbers, indices))
Out[86]: [1, 2, 2.0, 36]

# リスト内包表記を使った場合
In [87]: [pow(x, y) for x, y in zip(numbers, indices)]
Out[87]: [1, 2, 2.0, 36]

```

## 24. Filter() 関数

``filter()`` は任意の関数またはラムダ式を使ってシーケンスをフィルタリングする関数です。これはイテレータ型のフィルタ・オブジェクトを返します。一般に、この使い方は ``map()`` 関数と非常に似ています。

```python
In [97]: def good_word(x: str):
    ...:     has_vowels = not set('aeiou').isdisjoint(x.lower())
    ...:     long_enough = len(x) > 7
    ...:     good_start = x.lower().startswith('pre')
    ...:     return has_vowels & long_enough & good_start
    ...:

In [98]: words = ['Good', 'Presentation', 'preschool', 'prefix']

In [99]: list(filter(good_word, words))
Out[99]: ['Presentation', 'preschool']

```


## 25. リストの中から一番頻繁に使用される要素を見つける

例えば一連のゲームの勝者を追跡してランキングを作成するといった、一般的に重複する可能性のある要素を記録するためにリストを使用するのであれば、誰が一番多く勝利したかを見つけ出すことが意味のある処理といえます。これは ``max()`` 関数で ``key`` オプションを使うことで実現できます。このオプションは集合の中にある要素の数をカウントしていくことで最大値を見つけ出します。


```python
In [100]: winnings = ['John', 'Billy', 'Billy', 'Sam', 'Billy', 'John']

In [101]: max(set(winnings), key = winnings.count)
Out[101]: 'Billy'

```

## 26. リストの中の要素の出現頻度を追跡する

ヒント25の例に続いて、コンテストでチャンピン以外のプレイヤーの成績も知りたいので二位と三位のプレイヤーを見つけ出すことにします。そのためには各プレイヤーが勝利した数を把握する必要があります。ディクショナリ内包表記とラムダ式を引数にした ``sorted()`` 関数を使って実現できます。

```python
In [102]: winnings = ['John', 'Billy', 'Billy', 'Sam', 'Billy', 'John']

# ディクショナリ内包表記で各人の勝利数を出す
In [103]: tracked = {item: winnings.count(item) for item in set(winnings)}
In [104]: tracked
Out[104]: {'Billy': 3, 'Sam': 1, 'John': 2}

# sort() で並び替える
In [105]: sorted(tracked.items(), key=lambda x: x[1], reverse=True)
Out[105]: [('Billy', 3), ('John', 2), ('Sam', 1)]

```

## 27. オブジェクトの型チェック

オブジェクトの型チェックは Python におけるイントロスペクションの話題の範疇になります。ときどきオブジェクトが特定の型であるかどうかを、それを扱う関数を呼び出す前に知りたい時があります。その際は ``type()`` または ``isinstance()`` 関数を使います。後者の ``isinstance()`` は一対多のチェックを可能にするという点で他よりも自由度の高い関数です。

```python
In [109]: def check_type(number):
     ...:     if type(number) == int:
     ...:         print('do something with an int')
     ...:     if isinstance(number, (int, float)):
     ...:         print('do something with an int or float')
     ...:

In [110]: check_type(5)
do something with an int
do something with an int or float

In [111]: check_type(4.2)
do something with an int or float

```


## 28. Any() 関数

例として、John が会社に出社した時刻を記録しつづけたリストがあるとします。まず最初のユースケースは「今週 John は遅刻したかどうかを知りたい」です。このような場合は ``any()`` 関数がピッタリです。この関数は論理型の値を要素とするリストの中に True の要素があるかどうかを返します。

```python
In [112]: arraival_hours = {'Mon': 8.5, 'Tue':8.75, 'Wed': 9, 'Thu':8.5, 'Fri':8.5}

In [113]: arraival_checks = [x>8.75 for x in arraival_hours.values()]

In [114]: any(arraival_checks)
Out[114]: True

```


## 29. All() 関数

ヒント28の例に続いて、二つ目のユースケースは「今週をとおして John は 9:30 よりも前に出社していたかどうか知りたい」です。このケースをテストする場合は ``all()`` 関数が使えます。この関数は論理型の値を要素とするリストで全ての要素が True であるかどうかを返します。


```python
In [115]: arrival_checks_all = [x<9.5 for x in arraival_hours.values()]

In [116]: all(arrival_checks_all)
Out[116]: True

```


## 30. ファイルに対しては With キーワードを使う

ファイルを処理する時は、まずファイルをオープンし中身を処理してからクローズする必要があります。もしファイルを使用した後にクローズしないと、しばらくの間はそのファイルを使用できない場合があります。このような場面で ``with`` キーワードは非常に便利です。次に示すように、ファイルを使用したあとに自動的にクローズしてくれます。

```python
In [2]: with open('a_file.txt') as file:
...:     pass
...:

In [3]: file.closed
Out[3]: True

```

---

## 最後に

この記事では、Python プログラミング特有の使い方を完全に網羅した一覧を提供することは意図していません。その代わり、その特有の使い方から一般的なものを紹介しようとする試みです。そして、そのほとんどは毎日の Python コーディングで利用できるものです。

この記事には Python コーディング特有の使い方のうち幾つかが抜けているはずです。したがって、もし他の Python プログラマらと共有するのに役立つようなことを思いついたら、それは大歓迎です。
