## Tools
- gpg
  「`gpg` --import "GPG鍵"」→「`gpg` -d "メッセージファイル"」
- hashid  
  「`hashid` --john "Hashファイル名"」（--johnで、JohnTheRipperのフォーマットも確認できる）
- John The Ripper  
  - 「`john` --wordlist=/usr/share/wordlists/rockyou.txt "Hashファイル" --format=Hash方式」  
    「`john` "Hashファイル名" --show」クラック済み結果を表示（もしくは`/home/kali/.john/.john.pot`に解析結果がある）
  - 「`john` --list=formats」全フォーマットを表示  
    「--format=Raw-MD5」MD5ハッシュ, 「--format=nt」NTハッシュ
  - johnで解析するためのパスワード抽出
    - 「`zip2john` "zipファイル" > "出力ファイル"」johnで解析できるようにZIPパスワードを出力  
    - 「`rar2john` "rarファイル" > "出力ファイル"」johnで解析できるようにRARパスワードを出力  
    - 「`ssh2john` "SSH秘密鍵ファイル" > "出力ファイル"」johnで解析できるようにSSH秘密鍵を出力
    - 上記３つを実行後、「`john` --wordlist=/usr/share/wordlists/rockyou.txt "出力ファイル"」でクラック可能
  - 「john --single "Hashファイル" --format=Hash方式」SingleCrackモード（あんま使わん）  
    Hashファイルは`文字列:ハッシュ`形式。文字列を変換しながらHashクラックを行う。
  - 「sudo `unshadow` /etc/passwd /etc/shadow」Johnで /etc/shadow をクラックする際のフォーマット作成
- SSH  
  SSH秘密鍵の権限は600か700でないとSSH鍵認証できない
  - sshkeygen
## Linux
### Command
- 「`sed` -i '1s/^/文字列' ファイル名」 ファイルの１行目（`1s`）先頭に文字列を追加（改行なし）
### Preference
- `$format$rounds$salt$hash` /etc/shadowのフォーマット、`$format`でハッシュ種別が分かる。
## BookMark
- [CrackStation](https://crackstation.net/)
- [hashes.com](https://hashes.com/en/decrypt/hash)
- [hash_identifier](https://hashes.com/en/tools/hash_identifier)
- [SecLists](https://github.com/danielmiessler/SecLists)
- [RsaCtfTool](https://github.com/Ganapati/RsaCtfTool)
- [rsatool](https://github.com/ius/rsatool)
