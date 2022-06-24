## Lombok `@UtilityClass`
It is important to remember that when `@UtilityClass` is used then there is a problem with using static imports for methods.\
The problem is still unresolved in Lombok and work around is to use static imports with star `*` instead of separate static \
imports per function. 

_Due to limitations in javac, currently non-star static imports cannot be used to import stuff from @UtilityClasses; \
don't static import, or use star imports._

https://projectlombok.org/features/experimental/UtilityClass