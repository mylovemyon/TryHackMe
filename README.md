# TryHackMe
## Rooms
- Attacking Kerberos  
  Kerberosの仕組み  
  `Kerbrute`によるWordlistを用いたドメイン内ユーザの列挙  
  `Rubeus`によるTGTの収集、BruteForce・PasswordSpray、Kerberoasting、ASREPRoasting  
  `impacket-GetUserSPNs`によるKerberoasting（取得したユーザのSPNに対応したアカウントのTGSを取得できる）  
  `impacket-GetNPUsers`によるASREPRoasting（事前認証を必要としないユーザのTGTを取得する攻撃）  
  `impacket-secretsdump`によるDCSync攻撃での全ドメインユーザのNTハッシュの取得  
  TGS（$krb5tgs）をHashcatでクラック（Johnではクラック不可）、TGT（$krb5asrep）をJohnやHashcatでクラック  
  `mimikatz`による「Pass the Ticket」、「Golden/Silver Ticket」、「Skeleton Key」
- Attacktive Directory  
  `enum4linux`でのDomain名取得, ADのデフォルトのTLDは`.local`  
  `Kerbrute`によるWordlistを用いたドメイン内ユーザの列挙  
  `impacket-GetNPUsers`によるASREPRoasting（事前認証を必要としないユーザのTGTチケットを取得する攻撃）  
  `impacket-secretsdump`による`DRSUAPI`を介した全ドメインユーザのNTLM・Kerberosキーの取得  
  TGT（$krb5asrep）をJohnでクラック  
  `smbclient`や`SMBMap`によるShareの列挙・接続  
  `Evil-WinRM`によるWinRM接続
- Careers in Cyber
- Encryption - Crypto 101  
  `ssh-keygen`, `ssh2john`でSSH秘密鍵のパスワードをJohnで解析するために抽出, `gpg`コマンド  
  SSH秘密鍵の権限は600か700でないとSSH鍵認証できない, [RsaCtfTool](https://github.com/Ganapati/RsaCtfTool), [rsatool](https://github.com/ius/rsatool)
- Hashing - Crypto 101  
  `hashID`でハッシュ識別, `JohntheRipper`でクラック, [CrackStation](https://crackstation.net/)・[hashes.com](https://hashes.com/en/decrypt/hash)でクラック  
  Linuxのパスワードが保存される/etc/shadowの標準フォーマットは`$format$rounds$salt$hash`、$formatでHash形式が分かる
- Intro to C2  
  [C2Matrix](https://howto.thec2matrix.com/), msfconsoleとApacheを使用したC2リダイレクト
- Intro to Defensive Security
- Intro to Digital Forensics  
  `pdfinfo`によるPDFメタデータの確認、`exiftool`によるGPS情報などのEXIFの確認
- Intro to Offensive Security  
  `GoBuster`によるWeb探索
- John the Ripper  
  `john`によるWordlistsを使用したMD5/NTLMクラック・Wordlistsを使用しないSingleCrackMode  
  `zip2john`, `rar2john`, `ssh2john` らを使用したZIPやRAR・SSH秘密鍵のパスワードをJohnで解析するために抽出  
  `/etc/john/john.conf`でCustomルールの確認・作成・Wordlistsの拡張  
  `unshadow`による/etc/passwdと/etc/shadowのCombine   
  [hash_identifier](https://hashes.com/en/tools/hash_identifier)というWebサイトでハッシュ識別, [SecLists](https://github.com/danielmiessler/SecLists)
- Network Security  
  `FTP`のAnonymousログオン
- Operating System Security  
  `history`コマンドによるPassword窃取、NCSCの[100,000 most common passwords](https://www.ncsc.gov.uk/blog-post/passwords-passwords-everywhere)
- Red Team Engagements
- Red Team Fundamentals  
  [REDTEAM.GUIDE](https://redteam.guide/)、[Unified Kill Chain](https://unifiedkillchain.com/)
- Red Team OPSEC  
  [Pentoo](https://pentoo.github.io/)というペネトレ用のLinux
- Red Team Threat Intel  
  [ATT&CK Navigator](https://mitre-attack.github.io/attack-navigator/)による脅威グループのTTPマッピング、[OST Map](https://intezer.com/ost-map/)
- Security Operations
- Web Application Security
- Windows Fundamentals 1  
  `lusrmgr.msc`(ローカルユーザとグループ)
- Windows Fundamentals 2  
  `msconfig`(システム構成) , `taskmgr`(タスクマネージャー) , `control`(コントロールパネル), `UserAccountControlSettings`(ユーザアカウント制御の設定)


## Modules
- [Cryptography](https://tryhackme.com/module/cryptography)  
  Hashing - Crypto 101 | John The Ripper | Encription - Cripto 101
- [Introduction to Cyber Security](https://tryhackme.com/module/introduction-to-cyber-security)  
  Intro to Offensive Security | Intro to Defensive Security | Careers in Cyber
- [Introduction to Defensive Security](https://tryhackme.com/module/introduction-to-defensive-security)  
  Intro to Digital Forensics | Security Operations
- [Introduction to Offensive Security](https://tryhackme.com/module/introduction-to-offensive-security)  
  Web Application Security | Operating System Security | Network Security
- [Red Team Fundamentals](https://tryhackme.com/module/red-team-fundamentals)  
  Red Team Fundamentals | Red Team Engagements | Red Team Threat Intel | Red Team OPSEC | Intro to C2
- [Threat Emulation](https://tryhackme.com/module/threat-emulation-old)  
  Attacktive Directory | Attacking Kerberos
- [Windows Fundamentals](https://tryhackme.com/module/windows-fundamentals)  
  Windows Fundamentals 1 | Windows Fundamentals 2 | Windows Fundamentals 3


## Learning Paths
- [Introdution to Cyber Security](https://tryhackme.com/path/outline/introtocyber)  
  Introduction to Cyber Security | Introduction to Offensive Security | Introduction to Defensive Security
