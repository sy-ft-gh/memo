レッスン

	〇メソッド ★
		URL
			https://ufcpp.net/study/csharp/st_function.html
		概要
			クラスが持つ関数(function)をメソッドと呼ぶ。
			※lambdaをはじめ匿名メソッド等、広い意味のものを関数と呼ぶ
			メソッドの書式

			戻り値の型 関数名(引数一覧)
			{
				関数本体(具体的な処理)
			}
		ポイント
			引数
				https://ufcpp.net/study/csharp/st_function.html#arity
				
					型名・引数名（仮引数名）の組を宣言
					タプルも型として指定可能
			void型
				https://ufcpp.net/study/csharp/st_function.html#void
					結果が無いことを明示する型指定
					「rerturn;」は記述可能（以降のコードは実行されない）※デッドコード
			タプル
				https://ufcpp.net/study/csharp/st_function.html#tuple
					「(int x, int y)t」の様に型情報をその場で定義する宣言記法
					フィールドに名前を付けたものValueTuple、フィールドも無名のものTubple
					フィールドが無名の場合はitem1、item2といった宣言順で自動生成され
					るフィールド名を使用しアクセスする
			オーバーロード
				https://ufcpp.net/study/csharp/st_function.html#overload
					同名の関数を引数の型、個数の違いにより並列して宣言する記述方法
					関数の名前と型・個数が関数呼び出しには重要
						⇒これの組み合わせをシグネチャと呼ぶ
							※（ラムダなど他メソッドの定義方法を含む）
					同一の型・個数での引数の宣言を持つ同名メソッドはエラーとなる。
					呼び出す場合、一番型が近いメソッドが選択される。
					
						例えば以下の場合どうなるか？？
						
							class Program3 {
								public static void display(string value) { Console.WriteLine(value); } // 引数：string
								public static void display(object value) { Console.WriteLine(value); } // 引数：object
								public static void display(int value) { Console.WriteLine(value); } // 引数：int

								public static void Main(string[] args) {
									display(1.0);  // 引数：double
									display("AAA");  // 引数：string
									display('A');  // 引数：Char
									display(new { f1 = "a", f2 = "b" });  // 引数：匿名型
								}
							}

		実践
		（タプル）
			合計と平均を返すメソッド
			private (int sum, int avg) calc(int i, int j) {
				return (i + j, (i + j) / 2);
			}
		その他
			〇デストラクタ
				URL
					https://ufcpp.net/study/csharp/resource/rm_destructor/#abstract
				概要
					オブジェクトがガベージ コレクションに回収されるときに呼び出される特別なメソッドです。
					※役割を終え、最終的に破棄される際のタイミング
					確保したリソースの破棄はDisposeメソッドを使用して行う。
					class SampleClass
					{
					  // ↓これがデストラクター。クラス名にチルダが着いたメソッド
					  ~SampleClass()
					  {
					    // インスタンスの破棄用のコードを書く
					  }
					}
					破棄されるタイミングが.NetFrameworkに任されるため、基本的にリソースの破棄は
					デストラクタを用いずにfinallyなどで行う。
					例：
						GUIアプリでのUSBポート監視など。デストラクタに任せるのではなく
						画面を閉じるタイミングで接続中であれば破棄処理を行うなどを検討する。
	
	〇プロパティ ★
		URL
			https://ufcpp.net/study/csharp/oo_property.html
		概要
			手続き（操作・処理）と状態（データ）を持つ構造
			操作の対象となるもの。
			setter、getterのC#独自の実装。
			アクセッサーと呼ばれることもある。
			
		ポイント
			自動プロパティ
				https://ufcpp.net/study/csharp/oo_property.html#auto
			expression-bodied 
				https://ufcpp.net/study/csharp/oo_property.html#expression-bodied
					
					以下二つはメソッド？プロパティ？
						public int a() => 10; 
						public int b => 10;   
		実践
			リファクタリング
			⇒ラムダの簡単な説明

		その他
			〇インデクサー
				URL
					https://docs.microsoft.com/ja-jp/dotnet/csharp/programming-guide/indexers/using-indexers
				概要
					配列のようなインデックス付きのプロパティ。
					添え字の型が指定でき、複数も扱える。
					複数のインデクサーを同一クラスに作る場合、引数の型・個数が異なると作れる。

	〇静的メンバー ★
		URL
			https://ufcpp.net/study/csharp/oo_static.html
		概要
			クラスに持つメソッドやフィールド。
			全てのインスタンスで共通の変数やメソッドを静的メンバーにする。
		ポイント
			使い方
				静的メンバーはクラスに属する値なので、値を参照するには、変数を介してではなく、以下のようにします。
				Person p = new Person()
				p.name = "野上冴子"; // インスタンス フィールドは [インスタンス名.フィールド名] で参照する。
				p.age  = 40;

				// 静的フィールドは [クラス名.フィールド名] で参照する。
				Person.scientificName = "Homo Sapiens";

	〇継承 ★
		URL
			https://ufcpp.net/study/csharp/oo_inherit.html
		概要
			１つのクラスから性質を受け継ぎ新しいクラスを作ること。
			受け継ぐ元：基底クラス（親クラス）、受け継ぐ先：派生クラス（子クラス）
			派生クラスのインスタンスは基底クラスの変数に格納できる。
		ポイント
			書式
				class 派生クラス名 : 基底クラス名
				{
				  派生クラスの定義
				}
			基底クラスのコンストラクタ呼び出し
				派生クラスのコンストラクタが呼ばれる前に、引数無しの基底クラスのコンストラクタが自動的に呼ばれる。
				基底クラスの引数ありコンストラクタを呼ぶ場合は以下の様に派生クラスのコンストラクタに書く。
					派生クラスのコンストラクタ(引数) : base(基底クラスに渡したい引数)
					{
					}
			基底クラスのメンバーの隠蔽
				https://ufcpp.net/study/csharp/oo_inherit.html#conceal
				親・子で同じ名前のメンバーが宣言されると、インスタンスの宣言時の型により
				親・子のいずれかのメンバーが呼ばれる。
				⇒本来これは、オブジェクト指向での「多態性」のような利便性のある使用方法とは異なる
				⇒メンバーフィールドについては同じインスタンスでも、メモリは別領域になるため値が２重管理になる

					class Program1 {
						public int outerIntValue;
					}
					class Program2: Program1 {
						public new int outerIntValue;
					}

					Program1 pg2 = new Program2();
					Program2 pg22 = pg2 as Program2;
					pg2.outerIntValue = 2;
					Console.WriteLine(pg2.outerIntValue);
					Console.WriteLine(pg22.outerIntValue);

					pg22.outerIntValue = 4;
					Console.WriteLine(pg2.outerIntValue);
					Console.WriteLine(pg22.outerIntValue);
					Console.WriteLine(pg2 == pg22);
					
					⇒publicの同一メンバー変数は継承先では宣言しないか、別管理をするならば new で上書きする
	〇抽象クラス ★
		
	〇インタフェース ★
	
	〇多態性 ★
		URL
			https://ufcpp.net/study/csharp/oo_polymorphism.html
		概要
			同じ名前のメソッドを呼び出しで、異なる振る舞いをすること。
			特に重要なのは、仮想関数を使った動的多態性。インスタンスの動的な型に応じて異なる振る舞いをする。
		ポイント
			静的な型・動的な型
				https://ufcpp.net/study/csharp/oo_polymorphism.html#type
				実行時に変化する可能性がある型を動的な型という。
				typeof()で比較し確認できる。
					Program1 pg = new Program1();
					if (typeof(Program1) == pg.GetType()) { 
					}
				is / as でキャストのチェックと安全なダウンキャスト・アップキャスト可能
				※as でキャストして、キャスト不可な場合はnullになる
			仮想メソッド
				識別子virtualをつける事で、動的な型のメソッドが実行できる
				https://ufcpp.net/study/csharp/oo_polymorphism.html#usage
				
				⇒派生クラスを作成する際に初めて基底クラスにvirtualをつける事もある。
				　本来であれば設計時に考慮するべき事項。（追加改修などで発生する事も）
				
				仮想メソッドの利用例を実施
				https://ufcpp.net/study/csharp/oo_polymorphism.html#usage

	〇ジェネリクス ★
		URL
			https://ufcpp.net/study/csharp/sp2_generics.html#abst
		概要
			様々なな型に対応するために、型をパラメータとして与えて、その型に対応したクラスや関数を生成するもの機能です。
			型だけ違って処理の内容が同じようなものを作るときに使う。

宿題：
	１．今週取り扱ったURLの復習をしてください。
		⇒リンク先の部分で興味がある部分、もっと深く知りたい部分も含めます。
	２．構造化の賞を読んで、章末にある練習問題を解いてください。
	３．次回はオブジェクト指向のセクションを中心に行います。予習をお願いします。


