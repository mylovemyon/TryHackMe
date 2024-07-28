# TryHackMe
## Rooms
- Hashing - Crypto 101  
  `hashid`でハッシュ識別, `JohnTheRipper`でクラック, [CrackStation](https://crackstation.net/)・[hashes.com](https://hashes.com/en/decrypt/hash)でクラック  
  Linuxのパスワードが保存される/etc/shadowの標準フォーマットは`$format$rounds$salt$hash`、$formatでHash形式が分かる。  
- John The Ripper  
  `john`によるWordlistsを使用したMD5/NTLMクラック・Wordlistsを使用しないSingleCrackMode, `/etc/john/john.conf`でCustomルールの確認・作成    
  `unshadow`による/etc/passwdと/etc/shadowのCombine, 
  [hash_identifier](https://hashes.com/en/tools/hash_identifier)というWebサイトでハッシュ識別, [SecLists](https://github.com/danielmiessler/SecLists), 
## Modules
- [Cryptography](https://tryhackme.com/module/cryptography)  
  Hashing - Crypto 101 | John The Ripper | Encription - Cripto 101
