# Инициализация и настройка
git init
git config --global user.name "Dias"
git config --global user.email "chokubashev.dias@gmail.com"

# Фиксация изменений
git add .
git commit -m "Initial commit"

# Работа с ветками
git branch feature
git checkout feature
# ... вносим изменения ...
git add .
git commit -m "Added new feature"

# Слияние с master
git checkout master
git merge feature

# Выгрузка на GitHub (используйте Personal Access Token вместо пароля)
git remote add origin [https://github.com/Dias30008001000/repository-name.git](https://github.com/Dias30008001000/repository-name.git)
git push -u origin master
