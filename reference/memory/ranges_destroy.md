# destroy
* memory[meta header]
* std::ranges[meta namespace]
* function template[meta id-type]
* cpp20[meta cpp]

```cpp
namespace std::ranges {
  template <no-throw-input-iterator I, no-throw-sentinel<I> S>
    requires destructible<iter_value_t<I>>
  constexpr I destroy(I first, S last) noexcept;            // (1) C++20

  template <no-throw-input-range R>
    requires destructible<range_value_t<R>>
  constexpr borrowed_iterator_t<R> destroy(R&& r) noexcept; // (2) C++20
}
```
* no-throw-forward-iterator[link no-throw-forward-iterator.md]
* no-throw-sentinel[link no-throw-sentinel.md]
* destructible[link /reference/concepts/destructible.md]
* no-throw-forward-range[link no-throw-forward-range.md]
* range_value_t[link /reference/ranges/range_value_t.md]
* borrowed_iterator_t[link /reference/ranges/borrowed_iterator_t.md]

## 概要
デストラクタを呼び出す。

この関数は、配置`new`で構築したオブジェクトを破棄するために使用する。

- (1): イテレータペアで範囲を指定する
- (2): 範囲を直接指定する


## テンプレートパラメータ制約
- (1):
    - `I`が[`no-throw-forward-iterator`](no-throw-forward-iterator.md)である
    - `S`が[`I`に対する例外を投げない番兵](no-throw-sentinel.md)である
    - `I`の要素型が、[破棄可能](/reference/concepts/destructible.md)である
- (2):
    - `R`が[`no-throw-forward-range`](no-throw-forward-range.md)である
    - `R`の要素型が、[破棄可能](/reference/concepts/destructible.md)である


## 効果
以下と等価：

```cpp
for (; first != last; ++first)
  destroy_at(addressof(*first));
return first;
```
* destroy_at[link ranges_destroy_at.md]
* addressof[link addressof.md]


## 例
```cpp example
#include <iostream>
#include <memory>

#include <algorithm>

int main()
{
  std::allocator<int> alloc;

  // メモリ確保。
  // この段階では、[p, p + size)の領域は未初期化
  const std::size_t size = 3;
  int* p = alloc.allocate(size);

  // 未初期化領域[p, p + size)の各要素をデフォルト構築
  std::ranges::uninitialized_default_construct(std::ranges::subrange{p, p + size});

  // pの領域が初期化され、かつvからpに要素がコピーされているか確認
  std::for_each(p, p + size, [](int x) {
    std::cout << x << std::endl;
  });

  // 要素を破棄
  std::ranges::destroy(std::ranges::subrange{p, p + size});

  // メモリ解放
  alloc.deallocate(p, size);
}
```
* std::ranges::destroy[color ff0000]
* std::ranges::uninitialized_default_construct[link ranges_uninitialized_default_construct.md]
* std::allocator[link allocator.md]
* alloc.allocate[link allocator/allocate.md]
* alloc.deallocate[link allocator/deallocate.md]

### 出力例
```
578175192
0
0
```

## バージョン
### 言語
- C++20

### 処理系
- [Clang](/implementation.md#clang): 16.0
- [GCC](/implementation.md#gcc): 10.2.0
- [Visual C++](/implementation.md#visual_cpp): 2019 Update 10


## 関連項目
- [`destroy`](destroy.md)

## 参照
- [P9896R4 The One Ranges Proposal](https://www.open-std.org/jtc1/sc22/wg21/docs/papers/2018/p0896r4.pdf)
