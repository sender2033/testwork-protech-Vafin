Здесь будут решаться задачи с сайта aldpro [[Задачи]]

# Практическая работа 6. Работа с файлами и каталогами, FHS
## Задание 1. 
- Найдите в директории /usr/share все файлы размером более 500 Кб.
- Полученный в предыдущем пункте список сохраните в файл /tmp/search.list.
- Выясните размер файла /tmp/search.list в килобайтах и сохраните это значение в файл /tmp/search-size.txt.
- Выясните количество строк в файле /tmp/search.list и запишите результат в файл /tmp/search-size.txt, сохранив предыдущие данные.
Выполнение:
1. Для того, чтобы найти файлы, размер которых больше 500 Кб я использовал команду `find /usr/share/ -size +500k`. Объяснение: `find` - команда поиска, `/usr/share/` -  место где мы ищем, `-size +500k` - флаг для фильтрации размера файлов
2. Для сохранения списка в файл была использована команда `find /usr/share/ -size +500k > /tmp/search.list`. Объяснение: первые 3 части команды такие же как и в предыдущем этапе, потом добавляется `>` - который отвечает за отправку данных в файл `/tmp/search.list`
3. Чтобы выяснить размер списка была использована команда `ls -sh /tmp/search.list`, где `ls` - выводит список, флаг `-sh` - комбинированный флаг (-s, -h), который показывает размер файла в удобном для понимания формате. В данном случае ![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251005143127.png?raw=true) был такой вывод. Чтобы сохранить вывод в файл к команде `ls -sh /tmp/search.list` было добавлено ` > /tmp/search-size.txt` и команда стала выглядеть так `ls -sh /tmp/search.list > /tmp/search-size.txt`
4. Чтобы узнать количество строк в файле *Search-size.txt* и записать результат в файл */tmp/search-size.txt* сохранив предыдущие данные используется команда `wc -l /tmp/search.list >> /tmp/search-size.txt` , где  `wc -l` - выводит количество строк, а `>> /tmp/search-size.txt` - дополняет файл этой информацией. ![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251005145112.png?raw=true) Результат записи.

## Задание 2. 
- Создайте одной командой директорию /tmp/block6/task/1/2/3 и переместите в нее так же одной командой файлы /tmp/search.list и /tmp/search-size.txt.
- Создайте жесткую и символическую ссылки на файл /tmp/block6/task/1/2/3/search-size.txt.
- Выведите содержимое каталога /tmp/block6/task/1/2/3/ с получением айноды всех файлов.
- Удалите созданный каталог /tmp/block6/task/1/2/3/ вместе с содержимым.

Выполнение:
1. Создаем директорию командой `mkdir -p /tmp/block6/task/1/2/3 && mv /tmp/search.list /tmp/search-size.txt /tmp/block6/task/1/2/3/`, потом перемещаем файлы, созданные в предыдущем задании в эту директорию.   `mkdir -p /tmp/block6/task/1/2/3` - эта часть команды отвечает за создание директории, а эта `mv /tmp/search.list /tmp/search-size.txt /tmp/block6/task/1/2/3/` - за перенос файлов. Две команды были объединены `&&`
2. Создаем жесткую символьную ссылку командой `ln /tmp/block6/task/1/2/3/search-size.txt /tmp/block6/task/1/2/3/search-size-hard.txt`, а также мягкую символьную ссылку командой `ln -s /tmp/block6/task/1/2/3/search-size.txt /tmp/block6/task/1/2/3/search-size-soft.txt`
3. Выводим содержимое всех каталогов командой `ls -li /tmp/block6/task/1/2/3/`.  Результат вывода: ![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251005150533.png?raw=true)
4. Удаляем созданный каталог с помощью команды `rm -rf /tmp/block6/task/1/2/3/` 





# Практическая работа 9. Работа с правами доступа, ACL
## Задание 1.
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
![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251005174351.png?raw=true)

## Задание 2.
- Скопируйте исполняемый файл cat в домашнюю директорию пользователя.
- Выполните чтение из файла `file.txt` с помощью утилиты `cat` из домашней директории.
- Назначьте на исполняемый файл права доступа 600 (u=rw,g=,o=) и проверьте, что вы не можете запускать эту утилиту для чтения файлов.
-  Назначьте на исполняемый файл права 100 (u=x,g=,o=) и проверьте, что права доступа на запуск утилиты снова появились.
Выполнение:
1. Скопируем исполняемый файл `cat` в домашнюю директорию пользователя
```
which cat
cp /usr/bin/cat ~/
ls -l ~/cat
```
   ![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251005175319.png?raw=true)
   2. Пытаемся прочитать файл с помощью команды `~/cat ~/file.txt`
   ![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251005175614.png?raw=true)
   3. Назначаем на исполнительный файл права доступа 600 и пытаемся прочитать файл 
   ```
   chmod u=rw,g=,o= ~/cat
   ~/cat ~/file.txt
   ```
   ![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251005181941.png?raw=true)
   4. Назначаем на исполнительный файл права доступа 600 и пытаемся прочитать файл 
   ```
   chmod 100 ~/cat
   ~/cat ~/file.txt
   ```
   ![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251005182406.png?raw=true)

## Задание 3. 

- Создайте каталог `~/folder` и файл `~/folder/file.txt` с контентом «hello».
 - Назначьте на каталог права 000 (u=,g=,o=) и проверьте, что вы не можете более просматривать содержимое папки.
- Назначьте на каталог права 400 (u=r,g=,o=) и проверьте, что теперь вы можете просмотреть список файлов, но без прав доступа к ним. Создание новых файлов все так же недоступно.
- Назначьте на каталог права 600 (u=rw,g=,o=) и проверьте, что ничего не изменилось. Запись все так же недоступна.
- Назначьте на каталог права 700 (u=rwx,g=,o=) и проверьте, что x дает возможность читать права на дочерние файлы, а в сочетании wx появилась возможность создания файлов.
Выполнение: 
1. Создаем каталог *~/folder* и файл *~/folder/file.txt*
```
mkdir ~/folder
echo "hello" > ~/folder/file.txt
ls -l ~/folder/
```
![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251005182859.png?raw=true)
2. Назначаем на каталог права 000 и смотрим результат
```
chmod 000 ~/folder/
ls -l ~/folder/
cd ~/folder/
```
![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251005183040.png?raw=true)
3. Назначаем на каталог права 400 и смотрим результат
```
chmod 400 ~/folder/
ls -l ~/folder/
echo "hello2" > ~/folder/file2.txt
```
![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251005183321.png?raw=true)
4. Назначаем на каталог права 600 и смотрим результат
```
chmod 600 ~/folder/
echo "hello2" > ~/folder/file2.txt
```
![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251005183607.png?raw=true)
Как мы видим, ничего не поменялось
5. Назначаем на каталог права 700 (полный доступ владельцу) и смотрим результат
```
chmod 700 ~/folder/
ls -l ~/folder/
echo "hello2" > ~/folder/file2.txt
```
![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251005183830.png?raw=true)


## Задание 4.
- Откройте еще одно окно терминала с правами root и создайте файл `~/file2.txt` с контентом «hello». Владельцем файла должен быть root:root, права доступа по умолчанию 644 (u=rw,g=r,o=r).
- Назначьте на файл права доступа 007 (u=,g=,o=rwx).
- Добавьте пользователя user1 в ACL файла c правами 4 (u:user1:r).
    Убедитесь, что пользователь потерял права на запись, которые ему ранее предоставляла категория others, и теперь у него права только на чтение через ACL.
-  Установите на файл через ACL маску c правами 0 (m::).
Убедитесь, что права на чтение, которые ему ранее предоставляла запись в ACL, перекрываются маской, поэтому он «выпадает» из ACL, и ему снова выдаются права в соответствии с правами категории others.

Выполнение:
1. Открываем новый терминал из под root и создаем файл `~/file2.txt` с текстом "hello"
```
cd /home/user1/ 
echo "hello2" > file2.txt 
ls -l file2.txt
```
![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251005184630.png?raw=true)
По умолчанию права доступа у этого файла 644.
2. Назначаем права доступа на файл 007 `chmod u=,g=,o=rwx file2.txt` , таким образом user1 полные права к этому файлу, т.к. он попадает под категорию "Другие". Для проверки переключаемся на user1 и проверяем доступ к файлу.
![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251005184854.png?raw=true)
```
echo "world2" >> ~/file2.txt
cat ~/file2.txt
```
![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251005185255.png?raw=true)
3. Добавляем пользователя user1 в ACL с правами на чтение
```
setfacl -m u:user1:r file2.txt
getfacl file2.txt
```
![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251005185747.png?raw=true)
После этого проверяем, остались ли у пользователя права. 
```
echo "wide2" >> ~/file2.txt
cat ~/file2.txt
```
![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251005190005.png?raw=true)
Как мы видим, у user1 остались права только на чтение
4. Устанавливаем на файл через ACL маску с правами 0
```
setfacl -m m::- file2.txt
getfacl file2.txt
```
![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251005190301.png?raw=true)
Проверяем пользователя и теперь у него снова полный доступ
```
echo "wide2" >> ~/file2.txt
cat ~/file2.txt
```
![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251005190505.png?raw=true)



# Практическая работа 10. Система аутентификации PAM и управление правами SUDO
## Задание 1. 
- Используя команду sudo, измените пароль суперпользователя (root). Напоминаем, что это плохая практика и задание носит учебный характер.
- Убедитесь, что новый пароль работает при входе в систему.
Выполнение: 
1. Изменяем пароль суперпользователя, для этого используется команда `sudo passwd root`
![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251005191156.png?raw=true)

## Задание 2. 
- Создайте пользователей john, user1, user2.
- Задайте пароли для пользователей user1, user2.
- Создайте файл правил 01_usermanagement (с использованием `visudo`).
- Добавьте пользователю john права использования `sudo` без ввода пароля для команд `groupadd` и `usermod`.
Выполнение: 
1. Создаем пользователей  john, user1, user2 и задаем им пароли.
```
sudo useradd -m -s /bin/bash john
sudo useradd -m -s /bin/bash user1
sudo useradd -m -s /bin/bash user2
sudo passwd user1
sudo passwd user2
```
![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251005191628.png?raw=true)
Пользователь user1 не создался, т.к. он уже существует 
2. Создаем файл правил `01_usermanagement` и даем доступ к sudo без использования пароля. 
`sudo visudo -f /etc/sudoers.d/01_usermanagement`
и добавляем в этот файл следующий текст: 
`john ALL=(ALL) NOPASSWD:`
`/usr/sbin/groupadd, /usr/sbin/usermod`
![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251005192256.png?raw=true)

## Задание 3
- Переключитесь в пользователя john.
- Создайте группу g_admin и добавьте в нее пользователей user1 и user2.
- Отредактируйте файл `/etc/pam.d/su` и добавьте ограничение, чтобы только пользователи из группы «g_admin» могли использовать команду `su`.
- Проверьте, что user1 и user2 могут использовать `su`, а пользователь john – не может.
Выполнение: 
1. Создаем группу `g_admin`  `sudo groupadd g_admin` и добавляем в нее user1 и user2
```
sudo groupadd g_admin
sudo usermod -aG g_admin user1
sudo usermod -aG g_admin user2
```
![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251005192848.png?raw=true)
2. Редактируем файл `/etc/pam.d/su` и добавляем ограничения на то, что только пользователи из группы `g_admin` могли использовать команду `su`
Переходим в файл `/etc/pam.d/su` с помощью команды `sudo nano /etc/pam.d/su` и вставляем в него следующую строку `auth required pam_wheel.so group=g_admin`
![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251005193209.png?raw=true)
3. Поверяем результативность наших действий 
![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251005193839.png?raw=true)

## Задание 4
- Настройте модуль pam_tally для отслеживания неудачных попыток входа в систему.
- Установите правило блокировки учетной записи на 5 минут после 3 неудачных попыток входа.
- Проверьте функциональность. Для этого введите неправильные учетные данные и убедитесь, что учетная запись блокируется.

Выполнение: 
1. `/etc/pam.d/common-auth` открываем этот файл и добавляем в него строку `auth [success=ignore default=die] pam_tally2.so per_user deny=3 unlock_time=300` 
результат:
![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251005195919.png?raw=true)


# Практическая работа 14. Архивирование и сжатие информации
## Задание 1. 
1. Создайте 3 текстовых файла:
    - `file1.txt` - Используя случайные символы `/dev/random`
    - `file2.txt` - Копируя один и тот же текст 10 раз:
        «Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.»
    - `file3.txt` - Используя бинарный файл в качестве текстового
2. Заархивируйте файлы, используя команду `tar`.

Выполнение: 
1. Создадим `file1.txt` со случайным набором символов с помощью команды `dd if=/dev/random of=file1.txt bs=1024 count=1`. 
   Создадим `file2.txt` с текстом «Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.» и повторим его 10 раз с помощью команды `for i in {1..10}; do echo "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."; done > file2.txt`. Чтобы не вызывать команду echo 10 раз воспользуемся циклом for. 
   Для создания `file3.txt` с бинарным содержимым, скопируем это содержимое из директории */usr/bin/zip*, и, таким образом у нас получится следующая команда `cp /usr/bin/zip file3.txt`. На моей машине утилита *zip* была не установлена, поэтому я установил ее командой `sudo apt install zip`
   Для архивирования воспользуюсь командой `tar -cvf archive.tar file1.txt file2.txt file3.txt`![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251006104858.png?raw=true)
## Задание 2.
Сожмите полученный архив и файл `file2.txt`, используя следующие методы сжатия/архивации – `gzip`, `bzip2`, `xz`, `cpio`.
Выполнение:
1. Следующим шагом после создания архива и `file2.txt` в предыдущем задании будет их сжатие. Следуя заданию, первой для сжатия будет использоваться утилита `gzip`. Команда будет выглядеть так
```
gzip -k file2.txt
gzip -k archive.tar
```
