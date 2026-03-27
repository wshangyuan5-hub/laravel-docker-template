# Laravel Lesson レビュー①

## Todo一覧機能

### Todoモデルのallメソッドで実行しているSQLは何か
* SELECT * FROM todos;
### Todoモデルのallメソッドの返り値は何か
* Illuminate\Database\Eloquent\Collection {#261 ▼
  #items: array:2 [▼
    0 => App\Todo {#262 ▶}
    1 => App\Todo {#263 ▶}
  ]
}
・Illuminate\Database\Eloquent\Collectionクラスのインスタンス
### 配列の代わりにCollectionクラスを使用するメリットは
* 可読性向上
* SQL文を意識することなくテーブル操作が可能.  
<br>
* 配列の場合、keyを取得したが該当のkeyがない時、エラーが返ってくる。それに対して、Collectionクラスを使うと、nullで返ってくる。
### view関数の第1・第2引数の指定と何をしているか
* 第1引数は画面に表示したいbladeファイル
* 第2引数は代入したい値
* 取得したデータを画面に渡す.   
<br>
* 第1引数は、viewフォルダー以下のパスを表しています
* 第2引数は、配列のキーにbladeファイルで表示させたい変数名を指定し、バリューにキーに代入したい値を指定する
* 取得したデータを返しています
### index.blade.phpの$todos・$todoに代入されているものは何か
* $todos：コントローラで取得した Todoテーブルの全レコード
* $todo：$todos から1件取得したもの  
<br>
* 一件ずつレコードを取り出しています
## Todo作成機能

### Requestクラスのallメソッドは何をしているか
* 送信されたデータをすべて配列として取得
### fillメソッドは何をしているか
* 連想配列で取得した値をTodoインスタンスの各プロパティに一括で代入
### $fillableは何のために設定しているか
* 意図しないカラムを更新されないように
### saveメソッドで実行しているSQLは何か
* INSERT文（新規追加）
### redirect()->route()は何をしているか
* リダイレクトさせることができる  
<br>
* ->route()はweb.phpへ遷移する為に必要です
## その他

### テーブル構成をマイグレーションファイルで管理するメリット
* 現在のデータベースの状態を他の開発者に共有することができる
* いつ、どのテーブルを、どう変更したか、変更履歴として残る
### マイグレーションファイルのup()、down()は何のコマンドを実行した時に呼び出されるのか
* #up appコンテナ内で、php artisan migrate コマンドを実行します
* #down appコンテナ内で、php artisan migrate:rollback コマンドを実行します
### Seederクラスの役割は何か
* テストデータを開発者間で共有できる. 

* レコードを作成する
### route関数の引数・返り値・使用するメリット
* ルート名（name）を指定する
* URLを生成して返す
* 変更に強い、直接URLを記述しなくてよい
### @extends・@section・@yieldの関係性とbladeを分割するメリット
* @extendsで継承する親Bladeを引数で指定
* @section('content') ~ @endsectionで囲われた部分を、親Bladeの@yield('content')の部分に挿入。引数に同じ文字列'content'を指定することで、@section()と@yield()を紐づけています
* 重複するコードを共通化して再利用できるようになるため、保守性が向上
### @csrfは何のための記述か
* CSRF攻撃を防ぐための記述（フォームに CSRFトークン（認証用の文字列） が自動で追加）
### {{ }}とは何の省略系か
PHPコードの省略形
* `<?php echo e ; ?>`