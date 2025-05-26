# Laravel Lesson レビュー①

## Todo一覧機能

### Todoモデルのallメソッドで実行しているSQLは何か
* SELECT * FROM todos;

### Todoモデルのallメソッドの返り値は何か
* Illuminate\Database\Eloquent\Collectionクラスのインスタンス

### 配列の代わりにCollectionクラスを使用するメリットは
* Collectionクラスのメソッドを使用するだけで配列操作をすることができる。

### view関数の第1・第2引数の指定と何をしているか
* 第1引数はユーザーの画面に表示したいbladeファイルの指定。views以下の相対パスを.区切りで記述し、拡張子は記述しない。
* 第2引数はbladeファイルに渡したい情報の指定。['bladeファイル内の変数名'=>bladeファイルに渡す値]のように記述する。
* bladeファイルの変数に値を渡し、HTMLを返している。

### index.blade.phpの$todos・$todoに代入されているものは何か
* $todosにはIlluminate\Database\Eloquent\Collectionクラスのインスタンス、$todoにはTodoモデルが代入されている。

## Todo作成機能

### Requestクラスのallメソッドは何をしているか
* フォームから送信された内容を全て、連想配列で取得している。

### fillメソッドは何をしているか
* 連想配列で取得された、フォームから送信された内容を、連想配列のキーと対応するTodoモデルのプロパティにそれぞれ代入している。

### $fillableは何のために設定しているか
* フォームの項目を不正に増やしてname属性を変更して送信され、本来テーブルに挿入されるはずだった情報に不正な情報が上書きされないよう、フォームから送信された内容からTodoモデルのプロパティに代入する要素を選択するため。

### saveメソッドで実行しているSQLは何か
* INSERT INTO todos ('content') VALUES (テキスト欄に入力された文字列);

### redirect()->route()は何をしているか
* route関数の引数に渡されたルート名のルートにリダイレクトしている。

## その他

### テーブル構成をマイグレーションファイルで管理するメリット
* SQLを知らない人でもPHPを使うだけでテーブル構成を設定できる。
* テーブル構成を複数の開発者間で共有できる。

### マイグレーションファイルのup()、down()は何のコマンドを実行した時に呼び出されるのか
* up(): php artisan migrate
* down(): php artisan migrate:rollback

### Seederクラスの役割は何か
* テストデータを作成する役割。

### route関数の引数・返り値・使用するメリット
* 引数はweb.phpのRoute::name()で指定したルートの名前。
* 返り値はルート名に対応するルートのURL。
* ルートの名前を引数に渡すため、コードの可読性が上がる。

### @extends・@section・@yieldの関係性とbladeを分割するメリット
* @yieldは親bladeの、子bladeを挿入する場所に記述。 @sectionは子bladeの親bladeに挿入したい部分に@endsectionと挟んで記述。@yieldと@sectionに渡された引数が一致することで、親bladeと子bladeが紐づけられる。
* @extendsは@sectionの前に記述し、継承する親bladeのviews以下からの相対パスを.区切り、拡張子なしで記述して引数に渡し、どの親bladeを継承しているのか示す。
* bladeを分割するメリットとしては同じ記述をまとめることで、変更があった場合一つのファイルの内容を修正するだけで済むため、保守性が上がる。また、それぞれのbladeファイルのコードが短縮されるため可読性も上がる。

### @csrfは何のための記述か
*CSRFの攻撃を防ぐため、formにtokenを付属させるための記述。

### {{ }}とは何の省略系か
* <?php echo ?>の省略形。
