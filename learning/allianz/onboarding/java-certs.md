##Java certs 
There is a need to put Allianz certifiactes to java security of any used jdk otherwise it will rise error:
```

Caused by: sun.security.validator.ValidatorException: PKIX path building failed: sun.security.provider.certpath.SunCertPathBuilderException: unable to find valid certification path to requested target
	at java.base/sun.security.validator.PKIXValidator.doBuild(PKIXValidator.java:439)

``` 
To solve it, the original cacerts file from %JAVA_HOME%\lib\security folder should be copied to new installed jdks

To check if the cert is already stored in cacerts file:

```
C:\>"C:\Program Files\Java\jdk-11.0.3_7\bin\keytool.exe" -list -keystore "C:\Program Files\Java\jre8\lib\security\cacerts"
``` 