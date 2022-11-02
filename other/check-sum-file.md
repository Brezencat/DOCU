# Проерка контрольной суммы файла (проверка целостности)
Как проверить хэш сумму файла без дополнительного ПО из консоли в разных системах.

## Windows
В Window в командрой строке (cmd) используется команда certutil -hashfile <путь к файлу> <алгоритм хэширования> (наиболее популярные MD5, SHA256).
```bash
P:\>certutil -hashfile C:\source\test_rep\.gitignore SHA256
Хэш SHA256 C:\source\test_rep\.gitignore:
b9fb8d0f90895809fe217982ddd6d5d2bf1985fc69c1cf942a94d11723a647ed
CertUtil: -hashfile — команда успешно выполнена.

P:\>certutil -hashfile C:\source\test_rep\.gitignore MD5
Хэш MD5 C:\source\test_rep\.gitignore:
fff434be72e2da7768640fa0ac3c9521
CertUtil: -hashfile — команда успешно выполнена.
```

## Linux
В Linux в терминале используется утилита sha256sum (для проверки по алгоритму SHA256) или md5sum (для проверки по алгоритму MD5).
```shell
$ sha256sum ./.gitignore
b9fb8d0f90895809fe217982ddd6d5d2bf1985fc69c1cf942a94d11723a647ed *./.gitignore

$ md5sum ./.gitignore
fff434be72e2da7768640fa0ac3c9521 *./.gitignore
```

## MacOS
В MacOS в терминале используется утилита shasum (для проверки функцией хэширования SHA, далее выбирается алгоритм хэширования) и утилита md5 (для проверки по алгоритму MD5).
```shell
~ shasum -a 256 /Users/user/source/test_rep/.gitignore
b9fb8d0f90895809fe217982ddd6d5d2bf1985fc69c1cf942a94d11723a647ed  /Users/user/source/test_rep/.gitignore

~ md5 /Users/user/source/test_rep/.gitignore
MD5 (/Users/user/source/test_rep/.gitignore) = fff434be72e2da7768640fa0ac3c9521
```
