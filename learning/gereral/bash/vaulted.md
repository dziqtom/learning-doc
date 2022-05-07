#Vaulted 
Vaulted służy do zarządzania zmiennymi środowiskowymi aws's dla narzędzia `aws-cli`.

https://github.com/miquella/vaulted

Polega to na tym że `aws-cli` posługuje się zmiennymi lokalnymi do autoryzacji.
Zmienne wykorzystywane do tego to:
```
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
```
Z reguły te zmienne albo się ustawia ręcznie albo w pliku `~/.aws/credentials` gdzie mają postać:
```
$ cat ~/.aws/credentials

aws_access_key_id = AKIADEFGT7JX34J6BW
aws_secret_access_key = Y0E6RpDFgOtqs9h9hesd1LEh68ksO0N
```

Kiedy jest wiele kont to cieżko jest przełączać się miedzy userami i dlatego warto mieć `vaulted`
`vaulted` przechowuje wszystkie wrażliwe dane lokanie zaszyfrowane i umożliwia przełączanie sie pomiędzy
kontami z linii komend.
Aby skonfigurować konto należy uruchomić `vaulted add <nazwa profilu>` jak poniżej:
```
$ vaulted add development-env
```
i podać access key i secret dla środowiska które chce się skonfigurować
Aby przełączyć się na profil należy użyć komendy:
```
$ vaulted shell development-env
```
To spowoduje otworzenie nowej sesji shell wraz z ustawionym kluczem i hasłem do AWS.

Sprawdzamy jako kto jesteśmy zalogowani:
```
$ aws sts get-caller-identity
{
    "UserId": "AIDAUKNUO6M4EA44VORDH",
    "Account": "297268081464",
    "Arn": "arn:aws:iam::297268081464:user/eksdude"
}
```