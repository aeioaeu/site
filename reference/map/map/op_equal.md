# operator==
* map[meta header]
* std[meta namespace]
* function template[meta id-type]

```cpp
namespace std {
  template <class Key, class T, class Compare, class Allocator>
  bool
    operator==(const map<Key,T,Compare,Allocator>& x,
               const map<Key,T,Compare,Allocator>& y); // (1) C++03
}
```

## 概要
`x` が `y` と等しいかどうかの判定を行う。


## 戻り値
- C++03 : `x.`[`size`](size.md)`() == y.`[`size`](size.md)`() &&` [`equal`](/reference/algorithm/equal.md)`(x.`[`begin`](begin.md)`(), x.`[`end`](end.md)`(), y.`[`begin`](begin.md)`());`
- C++14 : [`equal`](/reference/algorithm/equal.md)`(x.`[`begin`](begin.md)`(), x.`[`end`](end.md)`(), y.`[`begin`](begin.md)`(), y.`[`end`](end.md)`());`


## 計算量
[`size()`](/reference/map/map/size.md) に対して線形時間。ただし、`x`と`y`のサイズが異なる場合は定数時間。


## 備考
- この演算子により、以下の演算子が使用可能になる (C++20)：
    - `operator!=`


## 例
```cpp example
#include <iostream>
#include <map>

int main()
{
  std::map<int,char> m1;
  m1[0] = 'a';

  auto m2 = m1;

  std::cout << (m1 == m2) << std::endl;

  m2[0] = 'b';

  std::cout << (m1 == m2) << std::endl;

  return 0;
}
```

### 出力
```
1
0
```

### 処理系
- [Clang](/implementation.md#clang): ??
- [GCC](/implementation.md#gcc): ??
- [ICC](/implementation.md#icc): ??
- [Visual C++](/implementation.md#visual_cpp): 2012


## 参照
- [LWG Issue 2257. Simplify container requirements with the new algorithms](http://www.open-std.org/jtc1/sc22/wg21/docs/lwg-defects.html#2257)
    - C++14から、2つ目の範囲のendイテレータをとる`equal()`アルゴリズムを使用するようになった。
- [P1614R2 The Mothership has Landed](https://www.open-std.org/jtc1/sc22/wg21/docs/papers/2019/p1614r2.html)
    - C++20での三方比較演算子の追加と、関連する演算子の自動導出
