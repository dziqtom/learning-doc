#Zakładanie użytkownika przez Terraform

##IAM resource w Terraform
Zakładanie użytkownika przez terraforma, gdzie hasło jest generowane przez program [GPG](https://gnupg.org/), 
czyli w programie do szyfrowania i podpisywania certyfikatem danych.
Zasobem terraformowym do zakładania usera jest
```
resource "aws_iam_user" "example" {
name          = "example"
path          = "/"
force_destroy = true
}

resource "aws_iam_user_login_profile" "example" {
user    = aws_iam_user.example.name
pgp_key = "keybase:some_person_that_exists"
}

output "password" {
value = aws_iam_user_login_profile.example.encrypted_password
}
```
##GPG
Jako `pgp_key` należy podać klucz wygenerowany prze `gpg`. Jak nie ma gpg to standard `brew install gpg` \
Do sprawdzenia istniejących kluczy służy komenda 
```
$ gpg -k                                                                                                                                                                                       <aws:admin-sso>

/Users/tomek/.gnupg/pubring.kbx
-------------------------------
pub   ed25519 2022-04-27 [SC] [expires: 2024-04-26]
      10F9362224A6C17FAA18A9EA01F7C6D77DC29E7C
uid           [ultimate] dziq
sub   cv25519 2022-04-27 [E] [expires: 2024-04-26]

pub   ed25519 2022-04-27 [SC] [expires: 2024-04-26]
      FC6918572CBD726543BB6935836D6E22C6A4FE61
uid           [ultimate] eksdude
sub   cv25519 2022-04-27 [E] [expires: 2024-04-26]
```
Klucz tworzy się w oparciu o komendę:
```
gpg --gen-key
```
podając potem wszystkie dane typu user, email etc.\
Można też zrobić plik template'u np. `key-gen-template` zawierającego: 
```
%echo Generating a default key
Key-Type: default
Subkey-Type: default
Name-Real: dziq
Name-Comment: somecomment
Name-Email: dziqtom@gmail.com
Expire-Date: 2
# Passphrase: ABC
%commit
%echo done
```
i potem generowanie z użyciem tego pliku 
```
gpg --batch --gen-key key-gen-template 
```
Efekt ten sam, tyle że nie trzeba podawać user'a i maila. \
Wzięte z [How to Use PGP to Encrypt Your Terraform Secrets](https://menendezjaume.com/post/gpg-encrypt-terraform-secrets/)

Należy teraz wziąć klucz publiczny i wstawić bezpośrednio w pole `pgp_key`. Klucz ten zostanie użyty do
zaszyfrowania wygenerowanego przez terraform hasła użytkownika. 

##Odczytanie hasła użytkownika założonego przez Terraform
Po założeniu user'a przez terraform'a w outpucie pojawi się zaszyfrowane hasło:
```
$ tf output

key = "AKIAUKNUO6M4F6NDTZTB"
password = "wVg....WRhn"
secret = "wV4....m5J"
```
Żeby teraz odczytać hasło to musi być dostęp do klucza prywatnego i można odszyfrować hasło za pomocą 
komendy:
```
$ tf output -raw password | base64 --decode | gpg --decrypt

gpg: encrypted with cv25519 key, ID 6ABED925E2D62563, created 2022-04-27
      "eksdude"
D.Ns.6C]mm%  
```
i dla secretu to samo
```
$ tf output -raw secret | base64 --decode | gpg --decrypt

gpg: encrypted with cv25519 key, ID 6ABED925E2D62563, created 2022-04-27
      "some_user"
IhV2L4joziPTYeJ9.......yTH0LXQkF224ibuF%    

```
albo od razu do schowka 
```
tf output -raw secret | base64 --decode | gpg --decrypt | pbcopy
```