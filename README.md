# DB設計

## Devise
### users
|column              |Type  |Option     |
|--------------------|------|-----------|
|user_id             |string|null: false , unique: true|
|email               |string|null: false , unique: true|
|encrypted_passwoord |string|null: false|

<!-- 
  検索関係はscanを使用することになると思う

 -->

## DynamoDB

### Users
Table: Users
Partition Key: user_id (String)
Attributes:
  - nickname (String) null:false #GSI
  - user_icon (String) 
  - profile (String) null:false
  - follow (Number)
  - follower (Number)
  - created_at (String) null:false

### Follow
Table: Follow
Partition Key：followee_id
Sort Key: follower_id #GSI
Attributes:
 - follow_at

### Posts
Table: Posts
Partition Key: user_id(String) #user_id#ユーザーのポスト数にすると良いのかな？
Sort Key: created_at (String)
Attributes:
  - content (String) #GSI?を使用して検索できると良いのかな？ソートキーにしたい(scanを使用して検索機能を実装する)
  - images(List)
  - comment (Number)
  - spread (Number)
  - good (Number)
  - bookmark (Number)
  - parent_post_id (String) #リプライ時に使用

### Manga
Table: Manga
Partition Key: user_id(String)
Sort Key: created_at (String)
Attributes:
  - tag (string)
  - public_status (bool) null:false
  - title(String)

### Chapter
Table: Chapter
Partition Key: Manga_id(String)
Sort Key: create_at (String)
Attributes:
  - subtitle (String) null:false
  - images (List) null:false
  - public_status (bool) null:false
  - reservation_time (number)

