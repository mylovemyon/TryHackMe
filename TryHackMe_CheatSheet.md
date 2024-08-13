## Tools
- CyberChef  
  「Magic」可読可能な文字列に変換してくれる
- [enum4linux](https://github.com/CiscoCXSecurity/enum4linux)  (kali〇, Perl)  
  「`enum4linux` IPアドレス」
- [Evil-WinRM](https://github.com/Hackplayers/evil-winrm) (kali〇, Ruby)  
  「`evil-winrm` -i IPアドレス -u ユーザ名 -H NTハッシュ」でWinRM経由でログインできる。
- gpg (kali〇, ELF)    
  「`gpg` --import "GPG鍵(拡張子.key)"」→「`gpg` -d "メッセージファイル(拡張子.gpg)"」でGPGファイルを復号
- [hashid](https://github.com/psypanda/hashID) (kali〇, python)  
  「`hashid` --john "Hashファイル名"」（--johnで、JohnTheRipperでのフォーマットも確認できる）
- [John The Ripper](https://github.com/openwall/john)  (kali〇, C)  
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
  - 「sudo `unshadow` /etc/passwd /etc/shadow」  
    Johnで /etc/shadow をクラックするためのフォーマット作成
- [impacket](https://github.com/fortra/impacket) (Kali〇, python)  
  `impacket-〇〇`以外に、`python3 /usr/share/doc/python3-impacket/examples/〇〇.py`でも実行できる
  - GetNPUsers  
    - 「`impacket-GetNPUsers` -no-pass -dc-ip ドメコンIP ドメイン名/ユーザ名 -outputfile 出力ファイル名」  
      で`ASREPRoast`（Kerberos事前認証を必要としていないユーザのTGTを取得できる）を実行  
      取得したTGTを「john --wordlist=Wordlist名 TGT名」または「hashcat -a 0 -m 18200 wordlist名 TGT名 」でクラックできる  
    - 「`impacket-GetNPUsers` -no-pass -dc-ip ドメコンIP -userfile ユーザリスト ドメイン名/ -outputfile 出力ファイル名」　　
      では「-userfile」内の各ユーザがASREPRoastできるかどうか確認できる
  - secretsdump  
    「`impacket-secretsdump` -just-dc ドメイン名/ユーザ名:パスワード@IPアドレス」  
    でドメインユーザのパスワードハッシュをダンプできる。
- [kerbrute](https://github.com/ropnop/kerbrute) (kali×, Go)
  - install  
    GitHub上のReleaseからLinuxバイナリをインストール
  - 「`./kerbrute` userenum -d ドメイン名 --dc ドメコンIP Wordlists名 -o 出力ファイル名」Domainユーザの列挙
- smbclient (kali〇, ELF)  
  「`smbcleint` -L IPアドレス or FQDN -U ユーザ名%パスワード」共有フォルダの列挙  
  「`smbclient` //IPアドレス/共有名 -U ユーザ名%パスワード」共有フォルダにアクセス
- [smbmap](https://github.com/ShawnDEvans/smbmap) (kali〇, python)  
  「`smbmap` -H IPアドレス -u ユーザ名 -p パスワード」共有フォルダの列挙（smbclientと比べフォルダ権限まで確認できる）
- SSH  
  SSH秘密鍵の権限は600か700でないとSSH鍵認証できない
  - sshkeygen
## Linux
### Command
- 「`sed` -i '1s/^/文字列' ファイル名」 ファイルの１行目（`1s`）先頭に文字列を追加（改行なし）
### Preference
- 「`sudo sed -i '$a10.10.253.185 spookysec.local' /etc/hosts`」を実行しHOSTSファイルを編集
- `$format$rounds$salt$hash` /etc/shadowのフォーマット、`$format`でハッシュ種別が分かる
## BookMark
- [CrackStation](https://crackstation.net/)
- [hashes.com](https://hashes.com/en/decrypt/hash)
- [hash_identifier](https://hashes.com/en/tools/hash_identifier)
- [SecLists](https://github.com/danielmiessler/SecLists)
- [RsaCtfTool](https://github.com/Ganapati/RsaCtfTool)
- [rsatool](https://github.com/ius/rsatool)
