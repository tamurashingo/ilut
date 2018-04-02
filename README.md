# 単体試験ツール

## これは

C言語用の単体試験ツールです。

## 使い方

### テストソース

実際のテスト用コードで説明します。


```c

// ILUT.h をインクルードします
#include “ILUT.h” 

// ILUT_Test型のテストを用意します
// ILUT_Testの実態はChar*型です
ILUT_Test test_add ( 
) 
{ 
    /**/ 
    /**/ 

    // ILUT_ASSERT でテストを書きます
    // テスト部分は通常のassert(3)と同じです
    ILUT_ASSERT( "正・正", add(3,4) == 7 ); 
    ILUT_ASSERT( "正・負", add(3, -4) == -1 ); 
    ・・・ 

    // すべてのテストが無事終了した場合は ILUT_SUCCESS を返します
    return ILUT_SUCCESS; 
} 

ILUT_Test test_foo(
)
{
    /**/
    /**/

    if ( 0 ) {
        // 到達したらエラーにする場合は、 ILUT_FAIL を使います
        ILUT_FAIL("ここには到達しない");
    }

    return ILUT_SUCCESS; 
{


int main( 
    int argc, 
    char** argv 
)  
{ 
    /**/ 
    // ILUT_TestCase型の配列に、上で記述した試験用関数を定義していきます
    // 最後はかならずTestCaseEndを定義します
    static ILUT_TestCase test[] = { 
        DEF_TEST(test_add), 
        DEF_TEST(test_foo, 
        TestCaseEnd 
    } 
    /**/ 


    // ILUT_RunTestで定義した試験を実施します。正常であれば0が返ります
    return ILUT_RunTest( test ); 
} 
```

### ビルド

`ILUT.o` をテスト用のオブジェクトとリンクしてください。


### その他

`sample` ディレクトリにテストのサンプルがあります。

---

## リファレンス

### `ILUT_RunTest`

定義済みのテストを実行する。

#### 引数

- `ILUT_TestCase*`
    - 定義したテストの配列

#### 出力

- テスト結果
    - 0: 全テスト合格
    - 1: テスト不合格

### `ILUT_Show`

テストログを出力する。

#### 引数

- `ILUT_MODE`
    - ログ出力モード
    - `ILUT_MODE_NONE`: 表示しない
    - `ILUT_MODE_SHOW`: テストケース名を表示
    - `ILUT_MODE_DETAIL`: テストケース + Assertionを表示
- `const char*`
    - 出力フォーマット。形式は `printf(3)` と同様
- `...`
    - 出力内容。形式は `printf(3)` と同様

#### 出力

なし

### `ILUT_SetLogOut`

ログ出力先を設定する。

#### 引数

- `FILE*`
    - 出力先

#### 出力

なし

### `ILUT_ResultOut`

テスト結果を独自形式のフォーマットで出力する。
これで出力した結果は、`ilut2xml.awk`を使用してXML形式に変換できる。 

#### 引数

- `FILE*`
    - 出力先
- `const char*`
    - テストケース名（テスト対象の関数名など）
- `const ILUT_TestCase*`
    - ILUT_RunTestで実施済みのテストケース

#### 出力

なし


### `ILUT_ASSERT`

想定した結果であることを確認する。

#### 引数

- `const char*`
    - メッセージ（テスト内容など）
- `boolean`
    - テスト。`assert(3)` と同様

#### 出力

なし

### `ILUT_FAIL`

テストを失敗させる。
`fopen` 失敗などテストの前提条件が崩れた際などに使用する。

#### 引数

- `const char*`
    - メッセージ

#### 出力

なし



License
-------
Copyright &copy; 2008 tamura shingo
Licensed under the [MIT License][MIT].

[MIT]: http://www.opensource.org/licenses/mit-license.php

