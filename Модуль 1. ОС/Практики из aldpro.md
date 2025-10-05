Здесь будут решаться задачи с сайта aldpro [[Задачи]]

# Практическая работа 6. Работа с файлами и каталогами, FHS
Задание 1. 
- Найдите в директории /usr/share все файлы размером более 500 Кб.
- Полученный в предыдущем пункте список сохраните в файл /tmp/search.list.
- Выясните размер файла /tmp/search.list в килобайтах и сохраните это значение в файл /tmp/search-size.txt.
- Выясните количество строк в файле /tmp/search.list и запишите результат в файл /tmp/search-size.txt, сохранив предыдущие данные.
Выполнение:
1. Для того, чтобы найти файлы, размер которых больше 500 Кб я использовал команду `find /usr/share/ -size +500k`. Объяснение: `find` - команда поиска, `/usr/share/` -  место где мы ищем, `-size +500k` - флаг для фильтрации размера файлов
2. Для сохранения списка в файл была использована команда `find /usr/share/ -size +500k > /tmp/search.list`. Объяснение: первые 3 части команды такие же как и в предыдущем этапе, потом добавляется `>` - который отвечает за отправку данных в файл `/tmp/search.list`
3. Чтобы выяснить размер списка была использована команда `ls -sh /tmp/search.list`, где `ls` - выводит список, флаг `-sh` - комбинированный флаг (-s, -h), который показывает размер файла в удобном для понимания формате. В данном случае ![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251005143127.png?raw=true) был такой вывод. Чтобы сохранить вывод в файл к команде `ls -sh /tmp/search.list` было добавлено ` > /tmp/search-size.txt` и команда стала выглядеть так `ls -sh /tmp/search.list > /tmp/search-size.txt`
4. Чтобы узнать количество строк в файле *Search-size.txt* и записать результат в файл */tmp/search-size.txt* сохранив предыдущие данные используется команда `wc -l /tmp/search.list >> /tmp/search-size.txt` , где  `wc -l` - выводит количество строк, а `>> /tmp/search-size.txt` - дополняет файл этой информацией. ![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251005145112.png?raw=true) Результат записи.

Задание 2. 
- Создайте одной командой директорию /tmp/block6/task/1/2/3 и переместите в нее так же одной командой файлы /tmp/search.list и /tmp/search-size.txt.
- Создайте жесткую и символическую ссылки на файл /tmp/block6/task/1/2/3/search-size.txt.
- Выведите содержимое каталога /tmp/block6/task/1/2/3/ с получением айноды всех файлов.
- Удалите созданный каталог /tmp/block6/task/1/2/3/ вместе с содержимым.

Выполнение:
1. Создаем директорию командой `mkdir -p /tmp/block6/task/1/2/3 && mv /tmp/search.list /tmp/search-size.txt /tmp/block6/task/1/2/3/`, потом перемещаем файлы, созданные в предыдущем задании в эту директорию.   `mkdir -p /tmp/block6/task/1/2/3` - эта часть команды отвечает за создание директории, а эта `mv /tmp/search.list /tmp/search-size.txt /tmp/block6/task/1/2/3/` - за перенос файлов. Две команды были объединены `&&`
2. Создаем жесткую символьную ссылку командой `ln /tmp/block6/task/1/2/3/search-size.txt /tmp/block6/task/1/2/3/search-size-hard.txt`, а также мягкую символьную ссылку командой `ln -s /tmp/block6/task/1/2/3/search-size.txt /tmp/block6/task/1/2/3/search-size-soft.txt`
3. Выводим содержимое всех каталогов командой `ls -li /tmp/block6/task/1/2/3/`.  Результат вывода: ![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251005150533.png?raw=true)
4. Удаляем созданный каталог с помощью команды `rm -rf /tmp/block6/task/1/2/3/` 





# Практическая работа 9. # Работа с правами доступа, ACL
Задание 1.
- Создайте пользователя user1, назначьте для него пароль и выполните вход (команды `useradd`, `passwd`, `login`).
- Создайте файл в домашней директории пользователя `~/file.txt` с контентом «hello». Владельцем файла должен быть user1:user1, права доступа по умолчанию 644 (u=rw,g=r,o=r).
- Назначьте на файл права доступа 000 (u=,g=,o=) и проверьте, что вы
    1. не можете прочитать файл
    2. не можете записать в файл новую строку «world»
- Назначьте на файл права доступа 400 (u=r,g=,o=) и проверьте, что запись все еще недоступна, но чтение появилось.
-  Назначьте на файл права доступа 600 (u=rw,g=,o=) и проверьте, что вы можете теперь и читать, и писать в файл.
-  Назначьте на файл права доступа 006 (u=,g=,o=rw) и проверьте, что вы снова не можете ни читать, ни писать в файл.
Выполнение:

1. Создаем пользователя user1 с домашней директорией с помощью флага `-m` и задаем пароль  
```
sudo useradd -m user1
sudo passwd user1
```
Входим в систему из под учетки user1 `su - user1`
2. Создаем файл *file.txt* с текстом 'hello' с помощью команды `echo "hello" > file.txt` и проверяем владельца и права доступа `ls -l file.txt` ![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251005165910.png?raw=true)
3. Изменяем права доступа на файл с помощью команды `chmod 000 file.txt` и проверяем права доступа ![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251005171047.png?raw=true)
   Попытаемся прочитать файл с помощью команды `cat file.txt` , а также записать слово "World" в этот же файл с помощью команды `echo "world" >> file.txt`
    ![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251005171539.png?raw=true)

4. Теперь установим права 400 и проверим их работу ```
```
chmod 400 file.txt
ls -l file.txt
cat file.txt
echo "world" >> file.txt
```
 ![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251005172707.png?raw=true)
5. Сделаем тоже самое, только с правами 600
    ```
   chmod 600 file.txt
   ls -l file.txt
   cat file.txt
   echo "world" >> file.txt
   cat file.txt
   ```
  ![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251005173353.png?raw=true)
  
  6. Установка прав 006 и проверка 
```
chmod 006 file.txt
ls -l file.txt
cat file.txt
echo "test" >> file.txt
```
 
  7



   