---
description: Works only for not .NET binary
---

# VMProtect + Res spoof

Открываем бинарь под который будем маскироваться в [resources hacker](https://angusj.com/resourcehacker/) и сохраняем все ресурсы в .res

<figure><img src="../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

Открываем таргетный бинарь, который хотим спаковать - и добавляем ресурсы полученные ранее

<figure><img src="../../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

Теперь  открываем vmp. **Add func - Entry Point,** ставим **Mutation** в Compilation Type. В **options** делаем так<br>

<figure><img src="../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

Пакуем
