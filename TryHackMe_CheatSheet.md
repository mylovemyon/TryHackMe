# Tools
- hashid  
  `hashid --john "Hashファイル名"`（--johnで、JohnTheRipperのFormat形式も確認できる）
- John The Ripper  
  - `john --wordlist=/usr/share/wordlists/rockyou.txt "Hashファイル名" --format=暗号方式`  
  - `john "Hashファイル名" --show` クラック済み結果を表示（もしくは`/home/kali/.john/.john.pot`に解析結果がある）
  - `john --list=formats` 全フォーマット形式を表示
  - `--format=Raw-MD5` MD５ハッシュ, `--format=nt` NTハッシュ
  - `unshadow /etc/passwd /etc/shadow` Johnで /etc/passwd をクラックする際のフォーマット作成
# Linux
  - `$format$rounds$salt$hash` /etc/shadowのフォーマット、`$format`でハッシュ種別が分かる。
# BookMark
- [CrackStation](https://crackstation.net/)
- [hashes.com](https://hashes.com/en/decrypt/hash)
- [hash_identifier](https://hashes.com/en/tools/hash_identifier)
