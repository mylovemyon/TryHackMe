# TryHackMe
## Rooms
- Attacktive Directory  
  `enum4linux`でのDomain名取得, ADのデフォルトのTLDは`.local`  
  `Kerbrute`によるWordlistを用いたドメイン内ユーザの列挙  
  `impacket-GetNPUsers`によるASREPRoasting（事前認証を必要としないユーザのTGTチケットを取得する攻撃）  
  `impacket-secretsdump`による`DRSUAPI`を介したドメイン内ユーザのNTLM・Kerberosキーの取得  
  TGT（$krb5asrep）をJohnでクラック  
  `smbclient`や`smbmap`によるShareの列挙・接続  
  `Evil-WinRM`によるWinRM接続
- Atacking Kerberos  
  Kerberosの仕組み  
  `Kerbrute`によるWordlistを用いたドメイン内ユーザの列挙  
  `Rubeus`によるTGTの収集、BruteForce・PasswordSpray、Kerberoasting、ASREPRoasting  
  `impacket-GetUseSPNs`によるKerberoasting（取得したユーザのSPNに対応したアカウントのTGSを取得できる）  
  `impacket-GetNPUsers`によるASREPRoasting（事前認証を必要としないユーザのTGTを取得する攻撃）  
  TGS（$krb5tgs）をHashcatでクラック（Johnではクラック不可）、TGT（$krb5asrep）をJohnやHashcatでクラック  
  `mimikatz`による「Pass the Ticket」、「Golden/Silver Ticket」、「Skeleton Key」
- Encryption - Crypto 101  
  `ssh-keygen`, `ssh2john`でSSH秘密鍵のパスワードをJohnで解析するために抽出, `gpg`コマンド  
  SSH秘密鍵の権限は600か700でないとSSH鍵認証できない, [RsaCtfTool](https://github.com/Ganapati/RsaCtfTool), [rsatool](https://github.com/ius/rsatool)
- Hashing - Crypto 101  
  `hashid`でハッシュ識別, `JohnTheRipper`でクラック, [CrackStation](https://crackstation.net/)・[hashes.com](https://hashes.com/en/decrypt/hash)でクラック  
  Linuxのパスワードが保存される/etc/shadowの標準フォーマットは`$format$rounds$salt$hash`、$formatでHash形式が分かる。  
- John The Ripper  
  `john`によるWordlistsを使用したMD5/NTLMクラック・Wordlistsを使用しないSingleCrackMode  
  `zip2john`, `rar2john`, `ssh2john` らを使用したZIPやRAR・SSH秘密鍵のパスワードをJohnで解析するために抽出  
  `/etc/john/john.conf`でCustomルールの確認・作成・Wordlistsの拡張  
  `unshadow`による/etc/passwdと/etc/shadowのCombine   
  [hash_identifier](https://hashes.com/en/tools/hash_identifier)というWebサイトでハッシュ識別, [SecLists](https://github.com/danielmiessler/SecLists), 
## Modules
- [Cryptography](https://tryhackme.com/module/cryptography)  
  Hashing - Crypto 101 | John The Ripper | Encription - Cripto 101
- [Threat Emulation](https://tryhackme.com/module/threat-emulation-old)  
  Attacktive Directory | Attacking Kerberos
