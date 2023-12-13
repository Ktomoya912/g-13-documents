
# テーブル

| テーブル名      | 説明                                                 |
| :-------------- | :--------------------------------------------------- |
| users           | 一般利用者、法人の情報を格納する                     |
| companies       | 法人の情報を格納する                                 |
| tags            | タグを格納する                                       |
| events          | イベント情報を格納する                               |
| event_times     | イベント開催時間を格納する                           |
| event_reviews   | イベントレビューを格納する                           |
| event_tag       | イベントとタグの関係を格納する                       |
| event_bookmarks | イベントを気になるリストに追加したユーザーを格納する |
| event_watched   | イベントを閲覧したユーザーを格納する                 |
| jobs            | 求人情報を格納する                                   |
| job_times       | 求人募集時間を格納する                               |
| job_reviews     | 求人レビューを格納する                               |
| job_tag         | 求人情報とタグの関係を格納する                       |
| job_bookmarks   | 求人情報を気になるリストに追加したユーザーを格納する |
| job_watched     | 求人情報を閲覧したユーザーを格納する                 |
| application     | 求人情報に応募したユーザーを格納する                 |
| messages        | メッセージ内容を格納                                 |
| message_box     | メッセージを格納する                                 |
| plans           | 購入プランを格納する                                 |
| purchases       | 購入履歴を格納する                                   |


# テーブルの構成
## キー制約の略称
- PK: primary key
- FK: foreign key
- NN: not null
- UQ: unique

## users
  | カラム名   | 制約   | データ型     | 説明                                 |
  | :--------- | :----- | :----------- | :----------------------------------- |
  | id         | PK     | Integer      | ユーザーを識別するための ID          |
  | username   | UQ, NN | VarChar(20)  | ユーザーの名前                       |
  | email      | UQ, NN | VarChar(255) | ユーザーのメールアドレス             |
  | password   | NN     | Char(255)    | ユーザーのパスワード(ハッシュ化済み) |
  | sex        |        | Char(1)      | ユーザーの性別                       |
  | birthday   | NN     | Date         | ユーザーの誕生日                     |
  | user_type  | NN     | Char(1)      | ユーザーのタイプ                     |
  | is_active  | NN     | Boolean      | アカウントが有効か否か               |
  | created_at | NN     | DateTime     | データ作成日時                       |
  | updated_at |        | DateTime     | データ更新日時                       |

## companies
  | カラム名       | 制約 | データ型     | 説明                        |
  | :------------- | :--- | :----------- | :-------------------------- |
  | company_id     | PK   | Integer      | 法人を識別するための ID     |
  | name           | NN   | VarChar(255) | 法人の名前                  |
  | postal_code    | NN   | Char(7)      | 法人の郵便番号              |
  | prefecture     | NN   | Char(31)     | 法人の都道府県              |
  | city           | NN   | VarChar(255) | 法人の市区町村              |
  | adress         | NN   | VarChar(255) | 法人の番地・建物名          |
  | phone_number   | NN   | Char(13)     | 法人の電話番号              |
  | email          | NN   | VarChar(255) | 法人のメールアドレス        |
  | homepage       |      | VarChar(255) | 法人のホームページ          |
  | representative | NN   | VarChar(255) | 法人の代表者名              |
  | created_at     | NN   | DateTime     | データ作成日時              |
  | updated_at     | NN   | DateTime     | データ更新日時              |
  | user_id        | FK   | Integer      | ユーザーを識別するための ID |

## tags
  | カラム名   | 制約 | データ型     | 説明                    |
  | :--------- | :--- | :----------- | :---------------------- |
  | id         | PK   | Integer      | タグを識別するための ID |
  | name       | NN   | VarChar(255) | タグの名前              |
  | created_at | NN   | DateTime     | データ作成日時          |
  | updated_at | NN   | DateTime     | データ更新日時          |

## jobs
  | カラム名           | 制約 | データ型      | 説明                        |
  | :----------------- | :--- | :------------ | :-------------------------- |
  | id                 | PK   | Integer       | 求人情報を識別するための ID |
  | name               | NN   | VarChar(255)  | 求人の名前                  |
  | salary             | NN   | VarChar(255)  | 求人の給料                  |
  | working_location   | NN   | VarChar(1023) | 求人の勤務場所              |
  | job_description    | NN   | Text          | 求人の仕事内容              |
  | additional_message |      | Text          | 企業からの追加メッセージ    |
  | is_one_day         | NN   | Boolean       | 求人が単発か否か            |
  | period             | NN   | DateTime      | 求人の掲載期間              |
  | status             | NN   | Char(1)       | 求人のステータス            |
  | user_id            | FK   | Integer       | 作成者                      |
  | created_at         | NN   | DateTime      | データ作成日時              |
  | updated_at         | NN   | DateTime      | データ更新日時              |

## job_times
  | カラム名   | 制約 | データ型 | 説明                    |
  | :--------- | :--- | :------- | :---------------------- |
  | job_id     | FK   | Integer  | 求人を識別するための ID |
  | start_time | NN   | DateTime | 開始時間                |
  | end_time   | NN   | DateTime | 終了時間                |
  | created_at | NN   | DateTime | データ作成日時          |
  | updated_at | NN   | DateTime | データ更新日時          |

## job_reviews
  | カラム名     | 制約   | データ型     | 説明                        |
  | :----------- | :----- | :----------- | :-------------------------- |
  | id           | PK     | Integer      | レビューを識別するための ID |
  | title        | NN     | VarChar(255) | レビューのタイトル          |
  | review       | NN     | Text         | レビューの内容              |
  | review_point | NN     | Integer      | レビューの評価(1~5)         |
  | created_at   | NN     | DateTime     | データ作成日時              |
  | updated_at   | NN     | DateTime     | データ更新日時              |
  | user_id      | FK, NN | Integer      | ユーザーを識別するための ID |
  | job_id       | FK     | Integer      | 求人を識別するための ID     |

## job_tag
  | カラム名   | 制約   | データ型 | 説明                    |
  | :--------- | :----- | :------- | :---------------------- |
  | job_id     | FK, PK | Integer  | 求人を識別するための ID |
  | tag_id     | FK, PK | Integer  | タグを識別するための ID |
  | created_at | NN     | DateTime | データ作成日時          |
  | updated_at | NN     | DateTime | データ更新日時          |

## job_bookmarks
  | カラム名   | 制約   | データ型 | 説明                        |
  | :--------- | :----- | :------- | :-------------------------- |
  | user_id    | FK, PK | Integer  | ユーザーを識別するための ID |
  | job_id     | FK, PK | Integer  | 求人を識別するための ID     |
  | created_at | NN     | DateTime | データ作成日時              |
  | updated_at | NN     | DateTime | データ更新日時              |

## job_watched
  | カラム名   | 制約 | データ型 | 説明                            |
  | :--------- | :--- | :------- | :------------------------------ |
  | id         | PK   | Integer  | 求人閲覧履歴を識別するための ID |
  | created_at | NN   | DateTime | データ作成日時                  |
  | updated_at | NN   | DateTime | データ更新日時                  |
  | user_id    | FK   | Integer  | ユーザーを識別するための ID     |
  | job_id     | FK   | Integer  | 求人を識別するための ID         |

## applications
  | カラム名   | 制約 | データ型 | 説明                        |
  | :--------- | :--- | :------- | :-------------------------- |
  | id         | PK   | Integer  | 応募を識別するための ID     |
  | status     | NN   | Boolean  | 受領済みか否か              |
  | created_at | NN   | DateTime | データ作成日時              |
  | updated_at | NN   | DateTime | データ更新日時              |
  | user_id    | FK   | Integer  | ユーザーを識別するための ID |
  | job_id     | FK   | Integer  | 求人を識別するための ID     |

## events
  | カラム名           | 制約 | データ型     | 説明                        |
  | :----------------- | :--- | :----------- | :-------------------------- |
  | id                 | PK   | Integer      | イベントを識別するための ID |
  | name               | NN   | VarChar(255) | イベントの名前              |
  | postal_code        | NN   | Char(7)      | イベントの郵便番号          |
  | prefecture         | NN   | Char(31)     | イベントの都道府県          |
  | city               | NN   | VarChar(255) | イベントの市区町村          |
  | address            | NN   | VarChar(255) | イベントの番地・建物名      |
  | phone_number       |      | Char(13)     | イベントの電話番号          |
  | email              |      | VarChar(255) | イベントのメールアドレス    |
  | homepage           |      | VarChar(255) | イベントのホームページ      |
  | event_description  | NN   | Text         | イベントの内容              |
  | participation_fee  |      | Integer      | イベントの参加費            |
  | capacity           |      | Integer      | イベントの定員              |
  | caution            |      | VarChar(255) | イベントの注意事項          |
  | additional_message |      | VarChar(255) | イベントの追加メッセージ    |
  | period             | NN   | DateTime     | イベントの掲載期間          |
  | status             | NN   | Char(1)      | イベントのステータス        |
  | created_id         | FK   | Integer      | 作成者                      |
  | created_at         | NN   | DateTime     | データ作成日時              |
  | updated_at         | NN   | DateTime     | データ更新日時              |


## event_times
  | カラム名   | 制約 | データ型 | 説明                        |
  | :--------- | :--- | :------- | :-------------------------- |
  | event_id   | FK   | Integer  | イベントを識別するための ID |
  | start_time | NN   | DateTime | 開始時間                    |
  | end_time   | NN   | DateTime | 終了時間                    |
  | created_at | NN   | DateTime | データ作成日時              |
  | updated_at | NN   | DateTime | データ更新日時              |
  

## event_reviews
  | カラム名     | 制約   | データ型     | 説明                        |
  | :----------- | :----- | :----------- | :-------------------------- |
  | id           | PK     | Integer      | レビューを識別するための ID |
  | title        | NN     | VarChar(255) | レビューのタイトル          |
  | review       | NN     | Text         | レビューの内容              |
  | review_point | NN     | Integer      | レビューの評価(1~5)         |
  | created_at   | NN     | DateTime     | データ作成日時              |
  | updated_at   | NN     | DateTime     | データ更新日時              |
  | user_id      | FK, NN | Integer      | ユーザーを識別するための ID |
  | event_id     | FK     | Integer      | 求人を識別するための ID     |
  
## event_tag
  | カラム名   | 制約   | データ型 | 説明                        |
  | :--------- | :----- | :------- | :-------------------------- |
  | event_id   | FK, PK | Integer  | イベントを識別するための ID |
  | tag_id     | FK, PK | Integer  | タグを識別するための ID     |
  | created_at | NN     | DateTime | データ作成日時              |
  | updated_at | NN     | DateTime | データ更新日時              |


## event_bookmarks
  | カラム名   | 制約   | データ型 | 説明                        |
  | :--------- | :----- | :------- | :-------------------------- |
  | user_id    | FK, PK | Integer  | ユーザーを識別するための ID |
  | event_id   | FK, PK | Integer  | イベントを識別するための ID |
  | created_at | NN     | DateTime | データ作成日時              |
  | updated_at | NN     | DateTime | データ更新日時              |

## event_watched
  | カラム名   | 制約 | データ型 | 説明                                |
  | :--------- | :--- | :------- | :---------------------------------- |
  | id         | PK   | Integer  | イベント閲覧履歴を識別するための ID |
  | created_at | NN   | DateTime | データ作成日時                      |
  | updated_at | NN   | DateTime | データ更新日時                      |
  | user_id    | FK   | Integer  | ユーザーを識別するための ID         |
  | event_id   | FK   | Integer  | イベントを識別するための ID         |

## messages
  | カラム名   | 制約 | データ型     | 説明                          |
  | :--------- | :--- | :----------- | :---------------------------- |
  | id         | PK   | Integer      | メッセージを識別するための ID |
  | title      | NN   | VarChar(255) | メッセージのタイトル          |
  | message    | NN   | Text         | メッセージの内容              |
  | created_at | NN   | DateTime     | データ作成日時                |
  | updated_at | NN   | DateTime     | データ更新日時                |

## message_box
  | カラム名   | 制約 | データ型 | 説明                          |
  | :--------- | :--- | :------- | :---------------------------- |
  | id         | PK   | Integer  | メッセージを識別するための ID |
  | is_read    | NN   | Boolean  | メッセージを既読か否か        |
  | created_at | NN   | DateTime | データ作成日時                |
  | updated_at | NN   | DateTime | データ更新日時                |
  | user_id    | FK   | Integer  | 送信者を識別するための ID     |
  | message_id | FK   | Integer  | メッセージを識別するための ID |

## plans
  | カラム名   | 制約 | データ型     | 説明                      |
  | :--------- | :--- | :----------- | :------------------------ |
  | id         | PK   | Integer      | プランを識別するための ID |
  | name       | NN   | VarChar(255) | プランの名前              |
  | price      | NN   | Char(31)     | プランの価格              |
  | period     | NN   | Integer      | プランの期間              |
  | created_at | NN   | DateTime     | データ作成日時            |
  | updated_at | NN   | DateTime     | データ更新日時            |

## purchases
  | カラム名   | 制約 | データ型 | 説明                        |
  | :--------- | :--- | :------- | :-------------------------- |
  | id         | PK   | Integer  | 購入履歴を識別するための ID |
  | is_paid    | NN   | Boolean  | 支払い済みか否か            |
  | created_at | NN   | DateTime | データ作成日時              |
  | updated_at | NN   | DateTime | データ更新日時              |
  | user_id    | FK   | Integer  | ユーザーを識別するための ID |
  | plan_id    | FK   | Integer  | プランを識別するための ID   |
