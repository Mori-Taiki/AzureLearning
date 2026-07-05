共有アクセス署名 (SAS) を作成すると、パラメーターとトークンを使って URI (Uniform Resource Identifier) が作成されます。この URI は、Azure Storage のリソース URI と SAS トークンで構成されます。

> [!VIDEO https://learn-video.azurefd.net/vod/player?id=09447e1d-017d-4349-9656-9142e06998fb]

### URI の定義について知っておくべきこと

URI の定義例を見て、パラメーターを確認しましょう。この例は、BLOB への読み取りと書き込みのアクセス許可を付与するサービス レベルの SAS を作成しています。自分の Azure Storage のリソースを支えるには、パラメーターをどう構成すればよいか考えてみてください。

```URI
https://myaccount.blob.core.windows.net/?restype=service&comp=properties&sv=2015-04-05&ss=bf&st=2015-04-29T22%3A18%3A26Z&se=2015-04-30T02%3A23%3A26Z&sr=b&sp=rw&sip=168.1.5.60-168.1.5.70&spr=https&sig=F%6GRVAZ5Cdj2Pw4tgU7IlSTkWgn7bUkkAg8P6HESXwmf%4B
```

| パラメーター | 例 | 説明 |
| --- | --- | --- |
| **リソース URI** | `https://myaccount.`**`blob`**`.core.windows.net/` `?restype=`**`service`** `&amp;comp=properties` | Azure Storage のエンドポイントとその他のパラメーターを定義します。この例では、Blob Storage のエンドポイントを定義し、この SAS がサービス レベルの操作に適用されることを示しています。この URI を `GET` で使うと Storage のプロパティが取得され、`SET` で使うと Storage のプロパティが構成されます。 |
| **Storage のバージョン** | **`sv`**`=2015-04-05` | Azure Storage バージョン 2012-02-12 以降では、このパラメーターは使用するバージョンを示します。この例は、バージョン 2015-04-05 (2015 年 4 月 5 日) を使うべきことを示しています。 |
| **Storage サービス** | **`ss`**`=bf` | SAS が適用される Azure Storage を指定します。この例は、SAS が Blob Storage と Azure Files に適用されることを示しています。 |
| **開始時刻** | **`st`**`=2015-04-29T22%3A18%3A26Z` | (省略可能) SAS の開始時刻を UTC 時間で指定します。この例は、開始時刻を 2015 年 4 月 29 日 22:18:26 UTC に設定しています。SAS を即座に有効にしたい場合は、開始時刻を省略してください。 |
| **有効期限** | **`se`**`=2015-04-30T02%3A23%3A26Z` | SAS の有効期限を UTC 時間で指定します。この例は、有効期限を 2015 年 4 月 30 日 02:23:26 UTC に設定しています。 |
| **リソース** | **`sr`**`=b` | SAS でアクセスできるリソースを指定します。この例は、アクセスできるリソースが Blob Storage にあることを指定しています。 |
| **アクセス許可** | **`sp`**`=rw` | 付与するアクセス許可を列挙します。この例は、読み取りと書き込みの操作へのアクセスを付与しています。 |
| **IP 範囲** | **`sip`**`=168.1.5.60-168.1.5.70` | リクエストを受け付ける IP アドレスの範囲を指定します。この例は、IP アドレス範囲 168.1.5.60 〜 168.1.5.70 を定義しています。|
| **プロトコル** | **`spr`**`=https` | Azure Storage が SAS を受け付けるプロトコルを指定します。この例は、HTTPS を使うリクエストだけを受け付けることを示しています。 |
| **署名** | **`sig`**`=F%6GRVAZ5Cdj2Pw4tgU7Il` `STkWgn7bUkkAg8P6HESXwmf%4B` | リソースへのアクセスが、ハッシュベースのメッセージ認証コード (HMAC) 署名で認証されることを指定します。署名は、SHA256 アルゴリズムでキーを使って計算され、Base64 エンコードでエンコードされます。 |


> [!TIP]
> 「[*共有アクセス署名を実装する*](/training/modules/implement-shared-access-signatures/)」トレーニング モジュールで学習を続けましょう。
