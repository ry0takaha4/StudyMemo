# Kotlinについて

# Kotlinとは？

- JetBrain社が2010年開発開始、2011年に提唱,2012年にOSS化
- オブジェクト指向の静的型付け言語
- Javaに代わり、より完結に書くことを目的として開発された
- JVM上で動作する
- JavaScriptへのトランスパイルも可能
- LLVM Toolchainを使ってネイティブコードにコンパイルできる
 - iOS等でのクロスプラットフォームを目指している
- KotlinはJavaと100%互換有り
- 既存のJavaプロジェクトの一部をKotlinにすることも可能

# Kotlinの思想

- 歴史が浅く、(2011年)、多数の言語の影響を受けている
 - Java,Scala,C#,Groovy に大きな影響
 - Objective-C,Gosu,Spec#,Python,Eiffelも参考

- Kotlinの目標
 - Javaと同等のコンパイル速度を目指す
  - 今はまだJavaと同等のコンパイル速度ではない
   - しかし、意識するほど遅くはないので十分実用可能

# Kotlinの歴史
- 2012/2/14にApache Lisence 2.0でOSS化
- 2012/4/12　マイルストーンVersion1として、KotlinM1をリリース
- 2013/8にリリースされたM6からAndroidStudioをサポート
- 2016/2/15 1.0がリリース
 - SpringBootの正式サポート
- GoogleI/O 2017でGoogleがAndroidにKotlinを正式採用・サポートするのを発表

# Kotlinのメリットとは？何が嬉しいの？

- Android開発との親和性の高さ
 - Kotlinは何も設定せずJavaのコードを呼び出せる　逆も可能
  - RetrofitのようなJavaライブラリもそのまま使うことができる
  - Kotlinで全てを書き直す必要はない
   - 一部だけ取り替えることもできる
 - Androidの64Kメソッド問題を解決するため、ランタイムのメソッド数が少ない
 - JetBrain社の強力なIDEサポートがある
 - ライブラリのサイズが小さい（８５９KB）
- 生産性の高さ
 - 少ない記述量
 - コレクション操作の便利な関数　（map,filterなど
 - Javaにはない有用な機能
 - シングルトンの実装
  - classをobjectと書くだけでシングルトンにできる
 - ラムダ式にデフォルトで対応
 - 拡張関数,遅延初期化、演算子、オーバーロード、エルビス演算子
- メンテナビリティの高さ
 - Nullセーフ、var,letによる再代入可不可が明示的

- 例 Personクラスを作る
 - Java
  - getId(),getName(),setName(),toString(),hashCode(),equals(Objects)。。。を書く
 - Kotlin
  - dataクラスを使うと１行書くだけでその実装をKotlinが自動でやってくれる

# Kotlinの特徴
- 静的型付けのオブジェクト指向言語
- フルスタックな言語を目指して開発されている
 - JVM上で実行されている
  - Androidでもサーバーでも実行可能
- JVM以外でも動作できるように開発されている
 - JavaScriptへのトランスパイル
  - npm,webpack,React等も使用できる
- Kotlin/Navive
 - LLVMコンパイラに通して機械語にコンパイルできる
  - プログラミング言語とプラットフォームの両方から独立する中間コードを生成する
   - これにより、MacOSやUbuntu,iOS,Raspberry piなどで動作するようになる

# 高階関数

- とは？
 - 関数オブジェクトを引数にしたり戻り値にしたいできる

```kotlin
// 例
fun <T> lock(lock: Lock, body: () -> T):T {
  lock.lock()
  try{
      // 引数で渡された関数オブジェクトを実行している
      return body()
  }finnaly{
      lock.unlock()
  }
}
```

# ラムダ式

- 関数を宣言せずに関数オブジェクトを生成できる

```kotlin
// 第２引数に注目
// ラムダ式でa,bの引数をとり、比較結果を返す関数オブジェクトが記載されている
max(string, {a,b -> a.length < b.length >})
```

# Kotlinの将来の展望

- Jetbrainsとしての展望
 - モダンな言語を提供する
 - マルチプラットフォーム開発を実現させることを目的としている
  - Android,iOS,サーバサイド,Webフロント,ネイティブ等
- Androidとの連携
 - Google I/O2017でAndroid&Kotlinの正式サポートが発表
 - Google&JetBrains社が協力してKotlinの開発をサポートする非営利団体の設立
 - GoogleがAndroidでKotlinを使うことを公式でサポートした理由
  - Javaとの相互運用が可能
  - IDE開発チームと同じチームが開発、IDEサポートを受けられる
  - 言語が成熟し製品版としてリリース可能、多くの導入事例がある

# 日本国内における導入事例
- FRESH!　サイバーエージェント
- famchatty　サイバーエージェント
- AWA　AWA
- Eight　Sansan
- トクバイ　トクバイ
- Retty Retty
- Pairs エウレカ
- FOLIO（予定)

# HelloWorld

まずは、`Hello World!`と出力する簡単なプログラムのサンプルをJavaとKotlinで見比べてみる

```java
// java
public class HelloWorld {
    public static void main(String[] args){
        System.out.println("Hello World!");
    }
}
```

```kotlin
// kotlin
fun main(args: Array<String>){
  println("Hello World!")
}
```
ポイント
- 戻り値がない場合は省略可能
- 引数の型は後ろに
- トップレベルに関数をかける
- 関数定義 fun

戻り値を設定したい場合
```kotlin
fun main(args: Array<String>):Unit{
  return Unit
}
```

- 関数宣言の後ろに :クラス名 と書く
- Unit型はのシングルトンオブジェクトを返している

##  文字列の中で変数を使う

```kotlin
var str = "hoge"
println("Hello ${str}!")
println("Hello $str!")
```

## クラス定義

```kotlin
class MainActivity: AppCompatActivity(){
  override fun onCreate(savedInstanceState: Bundle?){
    super.onCreate(savedInstanceState)
    setContentView(R.layout.activity_main)
  }
}
```

- 継承は クラス名: 継承したいクラス名
- classの前に何も書かなければpublicクラスになる
- Java `@Override` -> Kotlin `override func`

## 基本文法

- var 再代入可能
- val 再代入不可能

- if文は if"式"としても使える
 - Scalaのような書き方もできる
 - 関数型プログラミング手法を使える
  - 注意：関数型言語ではない、あくまで関数型プログラミングの一部ができるだけ
- 条件判定
 - when
  - Javaでいう、switch

- 配列オブジェクトを生成する関数
 - arrayOf
  - arrayOf(1,2,3,4,5) // Array<Int>
 - mapOf
 - listOf
 - setOf
 - Rangeを使った書き方もできる

- for文
 - `for(i in 0..4)`

- for文　逆順
 - `for(i in 4 downTo 0)`

- 変数
 - NonNull
  - 変数名:変数
   - hoge:Int
 - Nullable
  - 変数名:変数?
   - hoge:Int?

- nullチェック
 - Nullable変数?
 - Nullable変数!!

- エルビス演算子
 - `?:` 演算子を用いたnullチェック方法

```kotlin
val b: String? = null
// val l:Int = b?.lengthだとコンパイルエラー（lはnonnullなのにbがnullの場合、nullが入ることになってしまうため
val l: Int = b?.length ?: -1
print(l) //-1
```

file:///Users/AdminAir/Downloads/kotlin-prior-learning-book.pdf
// 35Pで一旦中断
