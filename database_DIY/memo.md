# ToDo

1.  どんなデータがいるか
2.  どのような操作をするか
3.  表に起こす

## テーブル

- ユーザー

  - ユーザー ID(primary)
  - ユーザー名(unique)
  - メールアドレス(unique)
  - パスワード (ハッシュ化)
  - 性別(optional)
  - 誕生日
  - 作成日時
  - 削除日時
  - ユーザータイプ(一般or企業or管理者)
  - 法人ID (Foreign, optional)

- 法人
  - 法人 ID(primary)
  - 法人名
  - 郵便番号
  - 都道府県
  - 市区町村
  - 番地・建物名
  - 法人の電話番号
  - 法人のメールアドレス
  - 法人のホームページ (optional)
  - 代表者名
  - 作成日時
  - ユーザー ID(foreign)
 
- 求人情報

  - 求人 ID(primary)
  - 法人 ID(foreign)
  - イベント ID(foreign,optinal)
  - 作成日時
  - 更新日時
  - 給料
  - 勤務時間
  - 勤務場所
  - 仕事内容
  - 単発か否か
  - 掲載期間
  - 企業からの追加メッセージ(optional)


- イベント

  - イベント ID(primary)
  - イベント名
  - 郵便番号
  - 都道府県
  - 市区町村
  - 番地・建物名
  - イベントの電話番号(optional)
  - イベントのメールアドレス(optional)
  - イベントのホームページ(optional)
  - 作成日時
  - 更新日時
  - 掲載期間
  - 法人 ID(foreign)
  - 求人 ID(foreign,optinal)
  - イベントの内容
  - イベントの日時
  - イベントの参加費(optional)
  - イベントの定員(optional)
  - イベントの注意事項(optional)
  - イベントの追加メッセージ(optional)
  
- レビュー
  
  - レビュー ID(primary)
  - レビュー内容
  - レビューの評価(1~5)
  - 作成日時
  - 更新日時
  - ユーザー ID(foreign)
  - 求人 ID(foreign,optinal)
  - イベント ID(foreign,optinal)

- タグ
  
  - タグ ID(primary)
  - タグ名

- イベントタグ
  
  - イベント ID(foreign)
  - タグ ID(foreign)

- 求人タグ
  
  - 求人 ID(foreign)
  - タグ ID(foreign)

- 気になるリスト(イベント)

  - ユーザー ID(foreign)
  - イベント ID(foreign)

- 気になるリスト(求人)

  - ユーザー ID(foreign)
  - 求人 ID(foreign)

- 応募リスト

  - ユーザー ID(foreign)
  - 求人 ID(foreign)
  - 応募日時
  - 受領済みか否か

- 閲覧履歴(求人)

  - ユーザー ID(foreign)
  - 求人 ID(foreign)
  - 閲覧回数
  - 閲覧日時
  
- 閲覧履歴(イベント)
  - ユーザー ID(foreign)
  - イベント ID(foreign)
  - 閲覧回数
  - 閲覧日時

- メッセージ(通知)

  - メッセージ ID(primary)
  - 受信者 ID(foreign)
  - 送信日時
  - 本文

# メモ
一般利用者が求人情報に応募すると、応募リストに追加される。
また、その時に、応募した求人情報の法人に対して、メッセージが送信される。
法人はそのメッセージを受領、もしくは拒否することができる。
受領した場合、一般利用者が求人に参加したとみなし、レビューを行うことができるようにする。