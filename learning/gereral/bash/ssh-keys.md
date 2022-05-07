#SSH Keys Management

###Dodawanie kluczy SSH do MacOs:
Aby dodać klucz należy wpisać:\
`$ ssh-keygen`\
System zapyta o podanie hasła, hasło jest użyte do zabezpieczenia dostępu do klucza i będzie go 
wymagało za każdym razem kiedy będzie trzeba go użyć, zatem z lenistwa nie podajemy hasła :)\
```Generating public/private rsa key pair.
Enter file in which to save the key (/Users/tomek/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /Users/tomek/.ssh/id_rsa.
Your public key has been saved in /Users/tomek/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:Qc***********************KWw tomek@MacBook-Pro-Tomasz.local
The key's randomart image is:
+---[RSA 3072]----+
| . o.....+o.+o   |
|  + . o  .o      |
| . . . o..+.O * *|
|. . .   .. o   = |
| . .        .   o|
|               o |
|                 |
|                 |
|                 |
+----[SHA256]-----+
```
Potem należy dodać hasło do system agenta:\
`$ eval $(ssh-agent) `\
`Agent pid 43108`\
`$ ssh-add ~/.ssh/id_rsa.pub`\

