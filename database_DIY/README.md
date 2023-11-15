# ToDo

1.  どんなデータがいるか
2.  どのような操作をするか
3.  表に起こす

## テーブル

| テーブル名       | 説明                                                 |
| :--------------- | :--------------------------------------------------- |
| uses             | 一般利用者、法人、管理者の情報を格納する             |
| companies        | 法人の情報を格納する                                 |
| jobs             | 求人情報を格納する                                   |
| events           | イベント情報を格納する                               |
| authors          | 求人情報、イベント情報の投稿者情報を格納する         |
| reviews          | レビューを格納する                                   |
| tags             | タグを格納する                                       |
| event_tag        | イベントとタグの関係を格納する                       |
| job_tag          | 求人情報とタグの関係を格納する                       |
| event_bookmark   | イベントを気になるリストに追加したユーザーを格納する |
| job_bookmark     | 求人情報を気になるリストに追加したユーザーを格納する |
| job_application  | 求人情報に応募したユーザーを格納する                 |
| job_history      | 求人情報を閲覧したユーザーを格納する                 |
| event_history    | イベントを閲覧したユーザーを格納する                 |
| messages         | メッセージを格納する                                 |
| purchase_plan    | 購入プランを格納する                                 |
| purchase_history | 購入履歴を格納する                                   |


## テーブルの構成

- PK: primary key
- FK: foreign key
- NN: not null
- UQ: unique


### ユーザー
  | カラム名   | 制約   | データ型     | 説明                                 |
  | :--------- | :----- | :----------- | :----------------------------------- |
  | id         | PK     | Integer      | ユーザーを識別するための ID          |
  | username   | UQ, NN | VarChar(20)  | ユーザーの名前                       |
  | email      | UQ, NN | VarChar(255) | ユーザーのメールアドレス             |
  | password   | NN     | Char(255)    | ユーザーのパスワード(ハッシュ化済み) |
  | sex        |        | Char(1)      | ユーザーの性別                       |
  | birthday   | NN     | Date         | ユーザーの誕生日                     |
  | created_at | NN     | DateTime     | ユーザーの作成日時                   |
  | deleted_at |        | DateTime     | ユーザーの削除日時                   |
  | user_type  | NN     | Char(1)      | ユーザーのタイプ                     |
  | company_id | FK     | Integer      | 法人を識別するための ID              |
  | is_active  | NN     | Boolean      | アカウントが有効か否か               |

### 法人
  | カラム名       | 制約 | データ型     | 説明                    |
  | :------------- | :--- | :----------- | :---------------------- |
  | company_id     | PK   | Integer      | 法人を識別するための ID |
  | name           | NN   | VarChar(255) | 法人の名前              |
  | postal_code    | NN   | Char(7)      | 法人の郵便番号          |
  | prefecture     | NN   | Char(31)     | 法人の都道府県          |
  | city           | NN   | VarChar(255) | 法人の市区町村          |
  | adress         | NN   | VarChar(255) | 法人の番地・建物名      |
  | phone_number   | NN   | Char(13)     | 法人の電話番号          |
  | email          | NN   | VarChar(255) | 法人のメールアドレス    |
  | homepage       |      | VarChar(255) | 法人のホームページ      |
  | representative | NN   | VarChar(255) | 法人の代表者名          |
  | created_at     | NN   | DateTime     | 法人の作成日時          |

### 求人情報
  | カラム名           | 制約 | データ型      | 説明                        |
  | :----------------- | :--- | :------------ | :-------------------------- |
  | id                 | PK   | Integer       | 求人情報を識別するための ID |
  | name               | NN   | VarChar(255)  | 求人の名前                  |
  | event_id           | FK   | Integer       | イベントを識別するための ID |
  | created_at         | NN   | DateTime      | 求人の作成日時              |
  | updated_at         | NN   | DateTime      | 求人の更新日時              |
  | salary             | NN   | VarChar(255)  | 求人の給料                  |
  | working_location   | NN   | VarChar(1023) | 求人の勤務場所              |
  | job_description    | NN   | Text          | 求人の仕事内容              |
  | additional_message |      | Text          | 企業からの追加メッセージ    |
  | is_one_day         | NN   | Boolean       | 求人が単発か否か            |
  | period             | NN   | DateTime      | 求人の掲載期間              |
  | status             | NN   | Char(1)       | 求人のステータス            |
  | created_by         | FK, NN | Integer      | 作成者                    |
  | updated_by         | FK     | Integer      | 更新者                    |

### 勤務時間
  | カラム名   | 制約 | データ型 | 説明                    |
  | :--------- | :--- | :------- | :---------------------- |
  | job_id     | FK   | Integer  | 求人を識別するための ID |
  | start_time | NN   | DateTime | 開始時間                |
  | end_time   | NN   | DateTime | 終了時間                |


### イベント
  | カラム名           | 制約   | データ型     | 説明                        |
  | :----------------- | :----- | :----------- | :-------------------------- |
  | id                 | PK     | Integer      | イベントを識別するための ID |
  | name               | NN     | VarChar(255) | イベントの名前              |
  | postal_code        | NN     | Char(7)      | イベントの郵便番号          |
  | prefecture         | NN     | Char(31)     | イベントの都道府県          |
  | city               | NN     | VarChar(255) | イベントの市区町村          |
  | address            | NN     | VarChar(255) | イベントの番地・建物名      |
  | phone_number       |        | Char(13)     | イベントの電話番号          |
  | email              |        | VarChar(255) | イベントのメールアドレス    |
  | homepage           |        | VarChar(255) | イベントのホームページ      |
  | event_description  | NN     | Text         | イベントの内容              |
  | participation_fee  |        | Integer      | イベントの参加費            |
  | capacity           |        | Integer      | イベントの定員              |
  | caution            |        | VarChar(255) | イベントの注意事項          |
  | additional_message |        | VarChar(255) | イベントの追加メッセージ    |
  | created_at         | NN     | DateTime     | イベントの作成日時          |
  | updated_at         | NN     | DateTime     | イベントの更新日時          |
  | period             | NN     | DateTime     | イベントの掲載期間          |
  | status             | NN     | Char(1)      | イベントのステータス        |
  | created_by         | FK, NN | Integer      | 作成者                    |
  | updated_by         | FK     | Integer      | 更新者                    |


### イベント日程
  | カラム名   | 制約 | データ型 | 説明                        |
  | :--------- | :--- | :------- | :-------------------------- |
  | event_id   | FK   | Integer  | イベントを識別するための ID |
  | start_time | NN   | DateTime | 開始時間                    |
  | end_time   | NN   | DateTime | 終了時間                    |
  
### レビュー
  
  | カラム名           | 制約   | データ型     | 説明                        |
  | :----------------- | :----- | :----------- | :-------------------------- |
  | id                 | PK     | Integer      | レビューを識別するための ID |
  | title              | NN     | VarChar(255) | レビューのタイトル          |
  | review_description | NN     | Text         | レビューの内容              |
  | review_score       | NN     | Integer      | レビューの評価(1~5)         |
  | created_at         | NN     | DateTime     | レビューの作成日時          |
  | updated_at         | NN     | DateTime     | レビューの更新日時          |
  | user_id            | FK, NN | Integer      | ユーザーを識別するための ID |
  | job_id             | FK     | Integer      | 求人を識別するための ID     |
  | event_id           | FK     | Integer      | イベントを識別するための ID |
  
### タグ
  | カラム名 | 制約 | データ型     | 説明                    |
  | :------- | :--- | :----------- | :---------------------- |
  | id       | PK   | Integer      | タグを識別するための ID |
  | name     | NN   | VarChar(255) | タグの名前              |

### イベントタグ
  
  | カラム名 | 制約   | データ型 | 説明                        |
  | :------- | :----- | :------- | :-------------------------- |
  | event_id | FK, PK | Integer  | イベントを識別するための ID |
  | tag_id   | FK, PK | Integer  | タグを識別するための ID     |

### 求人タグ
  
  | カラム名 | 制約   | データ型 | 説明                    |
  | :------- | :----- | :------- | :---------------------- |
  | job_id   | FK, PK | Integer  | 求人を識別するための ID |
  | tag_id   | FK, PK | Integer  | タグを識別するための ID |

### 気になるリスト(イベント)

  | カラム名 | 制約   | データ型 | 説明                        |
  | :------- | :----- | :------- | :-------------------------- |
  | user_id  | FK, PK | Integer  | ユーザーを識別するための ID |
  | event_id | FK, PK | Integer  | イベントを識別するための ID |

### 気になるリスト(求人)

  | カラム名 | 制約   | データ型 | 説明                        |
  | :------- | :----- | :------- | :-------------------------- |
  | user_id  | FK, PK | Integer  | ユーザーを識別するための ID |
  | job_id   | FK, PK | Integer  | 求人を識別するための ID     |

### 応募リスト

  | カラム名   | 制約   | データ型 | 説明                        |
  | :--------- | :----- | :------- | :-------------------------- |
  | user_id    | FK, PK | Integer  | ユーザーを識別するための ID |
  | job_id     | FK, PK | Integer  | 求人を識別するための ID     |
  | created_at | NN     | DateTime | 応募日時                    |
  | is_approve | NN     | Boolean  | 受領済みか否か              |

### 閲覧履歴(求人)

  | カラム名   | 制約   | データ型 | 説明                        |
  | :--------- | :----- | :------- | :-------------------------- |
  | user_id    | FK, PK | Integer  | ユーザーを識別するための ID |
  | job_id     | FK, PK | Integer  | 求人を識別するための ID     |
  | count      | NN     | Integer  | 閲覧回数                    |
  | watched_at | NN     | DateTime | 閲覧日時                    |
  
### 閲覧履歴(イベント)

  | カラム名   | 制約   | データ型 | 説明                        |
  | :--------- | :----- | :------- | :-------------------------- |
  | user_id    | FK, PK | Integer  | ユーザーを識別するための ID |
  | event_id   | FK, PK | Integer  | イベントを識別するための ID |
  | count      | NN     | Integer  | 閲覧回数                    |
  | watched_at | NN     | DateTime | 閲覧日時                    |

### メッセージ(通知)

  | カラム名 | 制約   | データ型     | 説明                          |
  | :------- | :----- | :----------- | :---------------------------- |
  | id       | PK     | Integer      | メッセージを識別するための ID |
  | title    | NN     | VarChar(255) | メッセージのタイトル          |
  | user_id  | FK, NN | Integer      | 受信者を識別するための ID     |
  | sent_at  | NN     | DateTime     | 送信日時                      |
  | text     | NN     | Text         | メッセージの内容              |

### 購入プラン

  | カラム名   | 制約 | データ型     | 説明                      |
  | :--------- | :--- | :----------- | :------------------------ |
  | id         | PK   | Integer      | プランを識別するための ID |
  | name       | NN   | VarChar(255) | プランの名前              |
  | price      | NN   | Char(31)     | プランの価格              |
  | created_at | NN   | DateTime     | プランの作成日時          |
  | updated_at | NN   | DateTime     | プランの更新日時          |
  | period     | NN   | Integer      | プランの期間              |

### 購入履歴

  | カラム名     | 制約   | データ型 | 説明                        |
  | :----------- | :----- | :------- | :-------------------------- |
  | user_id      | FK, PK | Integer  | ユーザーを識別するための ID |
  | plan_id      | FK, PK | Integer  | プランを識別するための ID   |
  | purchased_at | NN     | DateTime | 購入日時                    |

# メモ
一般利用者が求人情報に応募すると、応募リストに追加される。
また、その時に、応募した求人情報の法人に対して、メッセージが送信される。
法人はそのメッセージを受領、もしくは拒否することができる。
受領した場合、一般利用者が求人に参加したとみなし、レビューを行うことができるようにする。
