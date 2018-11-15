```uml
@startuml
activate ユーザ
    opt 会員未登録の場合
        activate 会員登録
        ユーザ -> 会員登録:新規登録
        会員登録 -> :メール配信処理
        ユーザ <-- :メール送信
        ユーザ -> 会員登録:有効化

    end
    ユーザ -> ログイン : ログインする
    activate ログイン
    ログイン -> ユーザ情報 :ログイン処理
    ref over ユーザ情報,権限情報 :権限チェック
    ユーザ情報 --> ログイン
        alt 認証[成功]
            ログイン --> ユーザ : /dashboradにリダイレクト
            deactivate ログイン
        else 認証[失敗]
            ログイン --> ユーザ :認証失敗のメッセージを表示
        end
    deactivate ログイン
@enduml
```