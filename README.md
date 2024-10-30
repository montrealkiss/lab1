## Національний технічний університет України<br>“Київський політехнічний інститут ім. Ігоря Сікорського”

## Факультет прикладної математики<br>Кафедра системного програмування і спеціалізованих комп’ютерних систем


# Лабораторна робота №1<br>"Базова робота з git"

## КВ-21 Юдін Дмитро

## Хід виконання роботи

### 1. Зклонувати будь-який невеликий проєкт open-source з github

# 1.1 Клонування повного репозиторію
Обираємо невеликий проєкт на GitHub для клонування. Для прикладу візьмемо інструмент створення презентацій для розробників https://github.com/slidevjs/slidev.

```
$ git clone https://github.com/slidevjs/slidev
Cloning into 'slidev'...
remote: Enumerating objects: 30532, done.
remote: Counting objects: 100% (1265/1265), done.
remote: Compressing objects: 100% (610/610), done.
remote: Total 30532 (delta 748), reused 1081 (delta 652), pack-reused 29267 (from 1)
Receiving objects: 100% (30532/30532), 76.32 MiB | 9.32 MiB/s, done.
Resolving deltas: 100% (22351/22351), done.
```
# 1.2 Клонування часткового репозиторію
Для клонування часткового репозиторію оберемо гілку, в данному випадку це буде tonai-addons.
```
$ git clone https://github.com/slidevjs/slidev --depth=1 --single-branch --branch=tonai-addons bran
ch_1
Cloning into 'branch_1'...
remote: Enumerating objects: 680, done.
remote: Counting objects: 100% (680/680), done.
remote: Compressing objects: 100% (634/634), done.
remote: Total 680 (delta 31), reused 394 (delta 17), pack-reused 0 (from 0)
Receiving objects: 100% (680/680), 8.56 MiB | 7.81 MiB/s, done.
Resolving deltas: 100% (31/31), done.
```

# 1.3 Різниця в розмірі баз даних двох клонів
