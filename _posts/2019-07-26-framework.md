## cucumberとは

CucumberとはRuby製のテストツール．

アプリケーションの振る舞いをテストできる．

Gherkinという言語で記述したテストケースを実行するツール．

日本語でテストケースを記述可能

コードを書けなくてもみるだけで仕様が理解可能

** ↓The RSpec[1,pp7] **
<font color = "DarkKhaki">
BDD はフルスタックのアジャイル開発技法です.BDD は ATDP(Acceptance Test-Driven Planning) と呼ばれる Acceptance TDD の一種を含め，エクストリームプログラミングからヒントを得ています.ATDP では，顧客受け入れテストを 導入し，それを主体にコードの開発を進めて行きます.それらは顧客と開発チーム による共同作業の結果であることが理想的です.開発チームによってテストが書か れた後，顧客がレビューと承認を行うこともあります.いずれにしても，それらのテストは顧客と向き合うものなので，顧客が理解できる言語とフォーマットで表現されていなければなりません.Cucumber を利用すれば，そのための言語とフォーマットを手に入れることができます.Cucumber は，アプリケーションの機能とサ ンプルシナリオを説明するテキストを読み取り，そのシナリオの手順に従って開発中のコードとのやり取りを自動化します
</font>

- cucumberの構造

  1.Featureファイル

　  テストのシナリオを記述するファイル

　  Given(前提)/When(処理内容)/Then(その結果)として記述する
<br>
  2.Stepファイル

　  シナリオの動作を記述するファイル

　  .featureファイルのGiven/When/Thenをプログラム的にどう解釈すると良いのかを記述するファイル

- [Gherkinを使ったほうが良い理由](https://sakanasoft.net/gherkin-is-valuable-test-practice/)
<br>
<br>
## RSpecとは

  プログラムの振舞 (behaviour)」を記述するためのドメイン特化言語 (DomainSpecific Language:DSL) を提供するフレームワーク

- プログラミングの振舞とは
「プログラムの振舞」とはプログラム全体あるいは様々なレベルでの部分 (モ ジュールやクラス、メソッド) に対して期待する振舞 (behaviour:ビヘイビア) のこと
<br>
<br>
例えば配列が空の場合に期待する振舞

    > ``` {.example}
    >arr = []
    >arr.empty? #=> 振舞として true を返すことを期待する
    >arr.size   #=> 振舞として 0 を返すことを期待する
    > ```
<br>
<br>
- ドメイン特化言語(DSL)とは
　ドメイン特化言語 (Domain Specific Language:DSL) とは、特定の問題領域(ドメイン) を記述するために設計された「言語」です。RSpec が特化しているドメインは「開発対象のプログラムの振舞を記述する」という領域です。RSpecはプログラムの振舞を記述する言語として、Ruby を拡張することを選びました

    **RSpecを使って書いた空の配列のテストケース**
    > ``` {.example}
    >describe Array, "when empty" do
    >  before do
    >    @empty_array = []
    >  end
    >
    >  it "should be empty" do
    >    @empty_array.should be_empty
    >  end
    >
    >  it "should size 0" do
    >     @empty_array.size.should == 0
    >  end
    >
    >  after do
    >     @empty_array = nil
    >  end
    >end
    > ```
    
    **Test::Unitを使って書いたテストケース**
    > ``` {.example}
    >require 'test/unit'
    > 
    >class ArrayTest < Test::Unit::TestCase
    >  def setup
    >	@empty_array = []
    >  end
    >	
    >  def test_empty?
    >    assert(@empty_array.empty?)
    >  end
    >
    >  def test_size
    >    assert_equal(0, @empty_array.size)
    >  end
    >
    >  def teardown
    >    @empty_array = nil
    >  end
    >end
    > ```

    上記を比べるとTest::UnitとRSpecとで最も大きく異なる点は、Test::Unitではクラスやメソッドを定義するのに対し、RSpecではブロック付きメソッド呼び出しや、カッコの省略を活用して記述したRubyスクリプトになっている点

[ブロック付きメソッドとは](https://qiita.com/shuhei_sfc/items/5c582f89d5d8d7ab956c)

- なぜRSpecか

  RSpecのプログラミングに対する考え方と，フレームワークとして支援するプログラミングの進め方はTDDと似ているから。

  describeやitを使うことによりテストが何をしているかがわかりやすい

[RSpecの基本的な構文を理解する](https://qiita.com/jnchito/items/42193d066bd61c740612)


## arubaとは

  コマンドラインツールをCucumber/RSpec/Minitestでテストするgem

  ArubaはCucumber、RSpec、Minitestのような人気のあるTDD/BDDフレームワ\\
ークでコマンドラインアプリケーションのテストを簡単で楽しいものにする拡\
張です。

- 特徴

  1.どんな言語で実装されたコマンドラインツールでもテスト可能

  2.テスト自体はRubyで書くが、テスト対象はPythonのCLI ツールでもGolang\
のCLI ツールでもよい

  3.ファイルシステムやプロセス環境をヘルパーによって操作できる例えばre\
adでファイルを読み込みできる

  4.例えば run で外部コマンドを実行し、その結果を have_output matcher \
などで検証できる

  5.ファイルシステムやプロセス環境はテストのたびにリセットされるのでle\
akingstateがない

  6.コミュ二ティーサポートが手厚い

  7.[ドキュメント](https://github.com/cucumber/aruba/tree/master/featu\
res)にあるとおりに動作することが期待できる

- なぜarubaだとcliのテストが簡単になるのか

 runコマンドを用いて外部コマンドを実行できるためreturnなどを付け加えなくて良いため

- [last_comman_startedとは](https://relishapp.com/cucumber/aruba/v/0-11-0/docs/command/return-last-command-started)