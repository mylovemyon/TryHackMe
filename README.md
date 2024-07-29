# TryHackMe
## Rooms
- Encryption - Crypto 101  
  `ssh-keygen`, SSH秘密鍵の権限は所有者のみだけの読みまたは書きこみ権限でないとSSH実行できない, `[RsaCtfTool](https://github.com/Ganapati/RsaCtfTool), [rsatool](https://github.com/ius/rsatool)
- Hashing - Crypto 101  
  `hashid`でハッシュ識別, `JohnTheRipper`でクラック, [CrackStation](https://crackstation.net/)・[hashes.com](https://hashes.com/en/decrypt/hash)でクラック  
  Linuxのパスワードが保存される/etc/shadowの標準フォーマットは`$format$rounds$salt$hash`、$formatでHash形式が分かる。  
- John The Ripper  
  `john`によるWordlistsを使用したMD5/NTLMクラック・Wordlistsを使用しないSingleCrackMode  
  `zip2john`, `rar2john`, `ssh2john` らを使用したZIPやRAR・SSH秘密鍵のパスワードをJohn用に抽出  
  `/etc/john/john.conf`でCustomルールの確認・作成・Wordlistsの拡張  
  `unshadow`による/etc/passwdと/etc/shadowのCombine   
  [hash_identifier](https://hashes.com/en/tools/hash_identifier)というWebサイトでハッシュ識別, [SecLists](https://github.com/danielmiessler/SecLists), 
## Modules
- [Cryptography](https://tryhackme.com/module/cryptography)  
  Hashing - Crypto 101 | John The Ripper | Encription - Cripto 101
