# rbegin
* map[meta header]
* std[meta namespace]
* map[meta class]
* function[meta id-type]

```cpp
reverse_iterator rbegin() noexcept;
const_reverse_iterator rbegin() const noexcept;
```

## 概要
`map` コンテナ内の最後の要素を指す逆イテレータを返す。 
内部的に、`map` コンテナは各要素をキーの値に従って下位から上位へと並べており、従って `rbegin()` は最上位のキーにあたる値を返す。 
`rbegin()` は [`end()`](/reference/map/map/end.md) と同じ要素を指すわけではなく、その前の要素を指すことに注意。


## 戻り値
反転したシーケンスの先頭を指す逆イテレータ。 
`reverse_iterator` と `const_reverse_iterator` はともにメンバ型である。`map` クラステンプレートにおいて、これらは逆双方向イテレータであり、それぞれ `reverse_iterator<iterator>`, `reverse_iterator<const_iterator>` と定義される。


## 計算量
定数時間。


## 例
```cpp example
#include <iostream>
#include <map>

int main()
{
  std::map<int, char> m;
  m.insert(std::make_pair(5, 'e'));
  m.insert(std::make_pair(2, 'b'));
  m.insert(std::make_pair(4, 'd'));
  m.insert(std::make_pair(1, 'a'));
  m.insert(std::make_pair(1, 'a'));

  std::map<int,char>::reverse_iterator i = m.rbegin();
  for( ; i != m.rend() ; ++i )
    std::cout << i->first << " " << i->second << std::endl;

  return 0;
}
```
* rbegin()[color ff0000]
* m.rend()[link rend.md]
* m.insert[link insert.md]

### 出力
```
5 e
4 d
2 b
1 a
```

### 処理系
- [Clang](/implementation.md#clang): ??
- [GCC](/implementation.md#gcc): ??
- [ICC](/implementation.md#icc): ??
- [Visual C++](/implementation.md#visual_cpp): 2012


## 関連項目
| 名前 | 説明 |
---------------------------------------------------------------------------------------------|--------------------------------------------------|
| [`map::begin`](/reference/map/map/begin.md) | 先頭を指すイテレータを取得する |
| [`map::end`](/reference/map/map/end.md) | 末尾を指すイテレータを取得する |
| [`map::cbegin`](/reference/map/map/cbegin.md) | 先頭を指すconstイテレータを取得する |
| [`map::cend`](/reference/map/map/cend.md) | 末尾を指すconstイテレータを取得する |
| [`map::rend`](/reference/map/map/rend.md) | 先頭を指す逆イテレータを取得する |
| [`map::crbegin`](/reference/map/map/crbegin.md) | 末尾を指す逆constイテレータを取得する |
| [`map::crend`](/reference/map/map/crend.md) | 先頭を指す逆constイテレータを取得する |

