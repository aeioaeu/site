# basic_fstream
* fstream[meta header]
* std[meta namespace]
* class template[meta id-type]

```cpp
namespace std {
  template <class CharT, class Traits = char_traits<CharT>>
  class basic_fstream : public basic_iostream<CharT, Traits>;

  using fstream  = basic_fstream<char>;
  using wfstream = basic_fstream<wchar_t>;
}
```
* char_traits[link /reference/string/char_traits.md]
* basic_istream[link /reference/istream/basic_istream.md]

## 概要


## メンバ関数

| 名前                                             | 説明                                 | 対応バージョン |
|--------------------------------------------------|--------------------------------------|----------------|
| [(constructor)](basic_fstream/op_constructor.md) | コンストラクタ                       | |
| (destructor)                                     | デストラクタ                         | |
| `operator=`                                      | ムーブ代入                           | C++11 |
| `swap`                                           | 値の交換                             | C++11 |
| [`rdbuf`](basic_fstream/rdbuf.md)                | ストリームバッファオブジェクトの取得 | |
| [`is_open`](basic_fstream/is_open.md)            | ファイルを開いているかの判定         | |
| [`open`](basic_fstream/open.md)                  | ファイルを開く                       | |
| [`close`](basic_fstream/close.md)                | ファイルを閉じる                     | |


## 非メンバ関数

| 名前   | 説明                          | 対応バージョン |
|--------|-------------------------------|----------------|
| `swap` | 2つのオブジェクトを入れ替える | C++11 |


## メンバ型

| 名前             | 説明                          | 対応バージョン |
|------------------|-------------------------------|----------------|
| `char_type`      | テンプレート仮引数`CharT`     | |
| `int_type`       | `Traits::int_type`            | |
| `pos_type`       | `Traits::pos_type`            | |
| `off_type`       | `Traits::off_type`            | |
| `traits_type`    | テンプレート仮引数`Traits`    | |

