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
$ git clone https://github.com/slidevjs/slidev --depth=1 --single-branch --branch=tonai-addons branch_1
Cloning into 'branch_1'...
remote: Enumerating objects: 680, done.
remote: Counting objects: 100% (680/680), done.
remote: Compressing objects: 100% (634/634), done.
remote: Total 680 (delta 31), reused 394 (delta 17), pack-reused 0 (from 0)
Receiving objects: 100% (680/680), 8.56 MiB | 7.81 MiB/s, done.
Resolving deltas: 100% (31/31), done.
```

# 1.3 Різниця в розмірі баз даних двох клонів
Порівняння отриманих репозиторіїв:
```
$ du -sh ./*/.git
8.8M    ./branch_1/.git
78M     ./slidev/.git
```
Різниця в розмірах баз даних клонів пов'язана з тим, що гілка branch_1 містить лише об'єкти, необхідні для відображення останнього стану однієї гілки tonai-addons.
### 2. Зробити не менше трьох локальних комітів
Створено три файли `1.txt`, `2.txt`, `3.txt`, а також змінено вміст файлу `.gitpod.yml`
```
$ git add 1.txt
$ git commit -m "add 1.txt"
[tonai-addons 483e500] add 1.txt
 1 file changed, 1 insertion(+)
 create mode 100644 1.txt
```
* 2)
```
$ git commit -am "some changes to gitpod.yml"
[tonai-addons 427637d] some changes to gitpod.yml
 1 file changed, 1 insertion(+)
```
* 3)
```
$ git add .
$ git commit -m "all"
[tonai-addons 208bbcd] all
 2 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 2.txt
 create mode 100644 3.txt
```
### 3.Внесення змін за допомогою опції --amend.
Дана опція працює наступним чином: ми робимо всі необхідні змінни, які будуть додаватись до попереднього коміту
і використовуємо `git commit --amend`. Тоді замість створення нового коміту всі зміни додадуться в попередній.
```
$ git status
On branch tonai-addons
Your branch is ahead of 'origin/tonai-addons' by 2 commits.
  (use "git push" to publish your local commits)

Untracked files:
  (use "git add <file>..." to include in what will be committed)
lab1.txt

nothing added to commit but untracked files present (use "git add" to track)

$ git add lab1.txt

$ git commit --amend -m "create all modifications and lab1.txt file"
[tonai-addons f498cdb] create all modifications and lab1.txt file
 Date: Fri Nov 1 16:56:39 2024 +0200
 3 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 2.txt
 create mode 100644 3.txt
 create mode 100644 lab1.txt

$ git status
On branch tonai-addons
Your branch is ahead of 'origin/tonai-addons' by 2 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```
Кількість нових комітів не змінилась, але змінилось наповнення та опис останнього коміту.
### 4.Об'єднання кількох останніх комітів в один за допомогою git reset.
Для об'єднання декількох останніх комітів в один, можна попросити гіт відкотитись на N комтів назад, 
але при цьому зміни залишивши в дереві.
```
$ git reset HEAD~3
Unstaged changes after reset:
M       .gitpod.yml

$ git status
On branch tonai-addons
Your branch is up to date with 'origin/tonai-addons'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   .gitpod.yml

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        1.txt
        2.txt
        3.txt
        lab1.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
Гіт скасував три останні коміти, але залишив на диску збереженні в них зміни.
HEAD~N -- адресує N-ний коміт назад від поточної голови. Тобто HEAD~1 (або скорочено для одного
коміту HEAD~) адресує попередній коміт, HEAD~3 адресує третій коміт назад від поточного.
### 5.Видалення файлів.
Скористаємось `git rm`, вона одразу видалить файл з файлової системи і додасть факт видалення файлу до індексу.
І закомітимо зміни.
```
$ git rm lab1.txt
rm 'lab1.txt'
$ git status -uno 
On branch tonai-addons
Your branch is ahead of 'origin/tonai-addons' by 1 commit.
  (use "git push" to publish your local commits)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        deleted:    lab1.txt

Untracked files not listed (use -u option to show untracked files)

$ git commit -m "delete lab1.txt"
[tonai-addons 2b942f2] delete lab1.txt
 2 files changed, 1 insertion(+)
 delete mode 100644 lab1.txt
```
### 6.Переміщення файлів.
Скористаємось `git mv`, вона одразу перемістить файл з файлової системи і додасть факт видалення 
старого файлу і додавання нового до індексу.
І закомітимо зміни.
```
$ git mv 4.txt 4new.txt

$ git status -uno
On branch tonai-addons
Your branch is ahead of 'origin/tonai-addons' by 6 commits.
  (use "git push" to publish your local commits)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        renamed:    4.txt -> 4new.txt

Untracked files not listed (use -u option to show untracked files)

$ git commit -m "rename 4.txt to 4new.txt"
[tonai-addons 0c87082] rename 4.txt to 4new.txt
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename 4.txt => 4new.txt (100%)
```
### 7.Гілкування.
# 7.1 Створення 3-ох гілок.

