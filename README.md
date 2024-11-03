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
Щоб виконати клонування часткового репозиторію оберемо гілку, обираємо tonai-addons.
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
Даний набір опцій відповідає за наступне:
* --depth=1 -- задає кількість комітів історії, що нам потрібна для скачування
* --single-branch -- задає гіту отримувати лише одну гілку
* --branch=tonai-addons -- задає гіту ім'я гілки, робоче дерево якої буде створене після
клонування. В поєднанні із --single-branch задає ім'я єдиної гілки, яку треба отримати
* branch_1 -- останній опційний параметр вказує бажане ім'я локальної папки, замість
оригінального імені репозиторію, в яку буде зклоновано проєкт.

# 1.3 Вираховуємо різницю в розмірі баз даних двох клонів
Порівняння отриманих репозиторіїв:
```
$ du -sh ./*/.git
8.8M    ./branch_1/.git
78M     ./slidev/.git
```
Різниця в розмірах баз даних клонів пов'язана з тим, що гілка branch_1 містить лише об'єкти, необхідні для відображення останнього стану однієї гілки tonai-addons.

### 2. Зробити не менше трьох локальних комітів

Створено три файли `1.txt`, `2.txt`, `3.txt`, а також змінено вміст файлу `.gitpod.yml`
Демонструємо різні способи додавання файлів до індексу та різні способи вказання повідомлення коміту.
1)
```
$ git add 1.txt
$ git commit -m "add 1.txt"
[tonai-addons 483e500] add 1.txt
 1 file changed, 1 insertion(+)
 create mode 100644 1.txt
```
2)
```
$ git commit -am "some changes to gitpod.yml"
[tonai-addons 427637d] some changes to gitpod.yml
 1 file changed, 1 insertion(+)
```
3)
```
$ git add .
$ git commit -m "all"
[tonai-addons 208bbcd] all
 2 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 2.txt
 create mode 100644 3.txt
```
### 3. Внесення змін за допомогою опції --amend.

Опція `--amend` працює наступним чином: ми вносимо всі необхідні змінни, які потрібно додати до попереднього коміту,
і виконуємо команду `git commit --amend`. У результаті, замість створення нового коміту, всі зміни будуть додані до попереднього коміту.
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
Кількість нових комітів не змінилась, проте змінилось наповнення та опис останнього коміту.

### 4. Об'єднання кількох останніх комітів в один за допомогою git reset.

Щоб об'єднанати декілька останніх комітів в один, можна скористатися командою `git reset` та відкотитись на N комтів назад, 
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
Було скасувано три останні коміти, проте зміни залишились на диску.
HEAD~N адресує N-ний коміт назад від поточної голови. Тобто HEAD~1 (або скорочено для одного
коміту HEAD~) адресує попередній коміт, HEAD~3 адресує третій коміт назад від поточного.

### 5. Видалення файлів.

Для видалення файлів можна скористатись `git rm`, це призведе до видалення файлу з файлової системи і додасть факт видалення файлу до індексу. Зміни лишається лише закомітити.
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
### 6. Переміщення файлів.

Для переміщення файлів можна скористатись командою `git mv`, як результат файл перемістить з файлової системи і додасть факт видалення старого файлу і додавання нового до індексу. Зміни лишається лише закомітити.
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
### 7. Гілкування.
# 7.1 Створення 3-ох гілок.
Команда `git branch` використовується для перегляду списку локальних гілок. Якщо `git branch` надати аргумент, то буде створена нова гілка. Аргумент буде використовуватись як ім'я новостворенної гілки. 
```
$ git branch branch_1
$ git branch branch_2
$ git branch branch_3

$ git branch
  branch_1
  branch_2
  branch_3
* tonai-addons
```
Активна гілка буде позначена зірочкою.
Команда `git checkout` змінює активну гілку на новостворену. Стан робочого дерева при цьому не зміниться, оскільки обидві гілки - стара та новостворена вказуватимуть на один і той же коміт.
```
$ git checkout branch_1
Switched to branch 'branch_1'

$ git branch
* branch_1
  branch_2
  branch_3
  tonai-addons
```
Біля гілки, стан коміту якої наразі відображений в робочому дереві, тобто активної гілки, буде
стояти зірочка. Так як зірочка змінила своє положення на новостворену 1-у гілку переключення між 
гілками відбулось.

### 8. Знаходження в історії комітів тих, в яких була зміна по конкретному шаблону в конкретному файлі

Беремо файл README.md, обираємо рядок за яким потрібно дізнатись історію його зміни, нехай це буде `Documentation:`. Для виконання цієї задачі використовується комбінація `git log` та `git diff`. Альтернативою до `git diff` є `git show`. 

Спочатку за допомогою `git log` виведемо лише ті коміти, в яких змінювався текс заданий шаблоном через опцію -G та обмежимо виведення лише файлом, що нас цікавить, а саме README.md:
```
$ git log -G 'Documentation:' README.md
commit ba1ff998bd0f3edcb05a6f14d657e3864dfbaf9d (grafted, origin/tonai-addons)
Author: _Kerman <kermanx@qq.com>
Date:   Mon Oct 28 14:18:10 2024 +0800

    Merge branch 'main' into tonai-addons
```
Перегляд зміни коміту за допомогою `git show`:
```
$ git show ba1ff998bd0f3edcb05a6f14d657e3864dfbaf9d README.md
commit ba1ff998bd0f3edcb05a6f14d657e3864dfbaf9d (grafted, origin/tonai-addons)
Author: _Kerman <kermanx@qq.com>
Date:   Mon Oct 28 14:18:10 2024 +0800

    Merge branch 'main' into tonai-addons

diff --git a/README.md b/README.md
new file mode 100644
index 0000000..c8ea9b9
--- /dev/null
+++ b/README.md
@@ -0,0 +1,103 @@
+<br>
+<p align="center">
+<a href="https://sli.dev" target="_blank">
+<img src="https://sli.dev/logo-title.png" alt="Slidev" height="250" width="250"/>
+</a>
+</p>
+
+<p align="center">
+Presentation <b>slide</b>s for <b>dev</b>elopers 🧑‍💻👩‍💻👨‍💻
+</p>
+
:
```
