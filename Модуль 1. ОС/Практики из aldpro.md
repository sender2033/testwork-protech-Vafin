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
1. Следующим шагом после создания архива и `file2.txt` в предыдущем задании будет их сжатие. Следуя заданию, первой для сжатия будет использоваться утилита `gzip`. Команда будет выглядеть так:
```
gzip -k file2.txt
gzip -k archive.tar
```
Далее будем сжимать с помощью таких утилит как: `bzip2`,`xz`и `cpio`. Список команд:
```
#bzip2
bzip2 -k file2.txt
bzip2 -k archive.tar

#xz
xz -k file2.txt
xz -k archive.tar

#cpio
ls file2.txt | cpio -o > file2.txt.cpio
ls archive.tar | cpio -o > archive.cpio
```

   ![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251006110255.png?raw=true)

## Задание 3. 
Не разжимая полученные сжатые файлы, поищите (zgrep) слово Lorem.
Выполнение: 
1. Для выполнения этого задания воспользуемся все теми же утилитами `gzip`, `bzip2`, `xz`, `cpio`. Сначала будем искать в `file2.txt`, а потом уже в архивах. Это будет выглядеть так: 
```
#Поиск в файлах
zgrep "Lorem" file2.txt.gz
bzgrep "Lorem" file2.txt.bz2
xzgrep "Lorem" file2.txt.xz
cpio -i --to-stdout < file2.txt.cpio | grep "Lorem"

#Поиск в архивах
zgrep "Lorem" -a archive.tar.gz
bzgrep "Lorem" -a archive.tar.bz2
xzgrep "Lorem" -a archive.tar.xz
cpio -i --to-stdout < archive.cpio | grep -a "Lorem"
```
![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251006111231.png?raw=true) Результат поиска в файлах. 
![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251006111542.png?raw=true) Результат поиска в архивах. Во всех попытках вывод одинаковый

## Задание 4.
Разархивируйте только файл `file2.txt`.
Выполнение:
1. Разархивирование выполним с помощью команды `tar -xvf archive.tar file2.txt`

# Практическая работа 18. Управление устройствами и модулями ядра ОС.
## Задание 1. 
1. По умолчанию группой файла /dev/tty8 является группа tty. Поменяйте группу на группу root для /dev/tty8.
2. После того как группа будет изменена, отмените свои изменения.

Выполнение: 
1.  С помощью команды  `echo 'SUBSYSTEM=="tty", KERNEL=="tty8", GROUP="root"' | sudo tee /etc/rules.d/10-tty8.rules` создадим файл в директории `/etc/udev/rules.d/10-tty8.rules`, в котором будет находится правило `SUBSYSTEM=="tty", KERNEL=="tty8", GROUP="root"`, которое устанавливает, что после каждого создания устройства `/dev/tty8`, его группа будет меняться на root.  Однако, после выполнения этой команды система выдала ошибку о том, что файл не найден. Причина этого в том, что в Debian директория `/etc/rules.d` не существует, решением было заменить эту директорию на `/etc/udev/rules.d/`.

Проверяем результат с помощью команд `udevadm trigger /sys/devices/virtual/tty/tty8` и `ls -l /dev/tty8`, в результате чего наблюдаем успешное выполнение правила 
![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251006115327.png?raw=true)
 После этого удаляем правило командой `rm /etc/udev/rules.d/10-tty8.rules` и возвращаем tty8 в группу tty `chown :tty /dev/tty8` 

## Задание 2.
1. Определите путь к сетевому устройству eth0 в каталоге /sys.
2. Выведите все атрибуты устройства eth0.

Выполнение:
1. Чтобы определить путь к eth0 посмотрим какие ссылки есть в `/sys/net/`, воспользовавшись командой `ls -l /sys/class/net/`, но как выяснилось, на моем устройстве нет eth0, вместо него используется ens33.
![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251006120034.png?raw=true) 
2. Для вывода всех атрибутов использовалась команда  `udevadm info -a -p /sys/devices/pci0000:00/0000:00:11.0/0000:02:01.0/net/ens33`. 
### Список атрибутов

Udevadm info starts with the device specified by the devpath and then
walks up the chain of parent devices. It prints for every device
found, all possible attributes in the udev rules key format.
A rule to match, can be composed by the attributes of the device
and the attributes from one single parent device.

  looking at device '/devices/pci0000:00/0000:00:11.0/0000:02:01.0/net/ens33':
    KERNEL=="ens33"
    SUBSYSTEM=="net"
    DRIVER==""
    ATTR{addr_assign_type}=="0"
    ATTR{addr_len}=="6"
    ATTR{address}=="00:0c:29:d4:48:07"
    ATTR{broadcast}=="ff:ff:ff:ff:ff:ff"
    ATTR{carrier}=="1"
    ATTR{carrier_changes}=="2"
    ATTR{carrier_down_count}=="1"
    ATTR{carrier_up_count}=="1"
    ATTR{dev_id}=="0x0"
    ATTR{dev_port}=="0"
    ATTR{dormant}=="0"
    ATTR{duplex}=="full"
    ATTR{flags}=="0x1003"
    ATTR{gro_flush_timeout}=="0"
    ATTR{ifalias}==""
    ATTR{ifindex}=="2"
    ATTR{iflink}=="2"
    ATTR{link_mode}=="0"
    ATTR{mtu}=="1500"
    ATTR{name_assign_type}=="4"
    ATTR{napi_defer_hard_irqs}=="0"
    ATTR{netdev_group}=="0"
    ATTR{operstate}=="up"
    ATTR{power/async}=="disabled"
    ATTR{power/control}=="auto"
    ATTR{power/runtime_active_kids}=="0"
    ATTR{power/runtime_active_time}=="0"
    ATTR{power/runtime_enabled}=="disabled"
    ATTR{power/runtime_status}=="unsupported"
    ATTR{power/runtime_suspended_time}=="0"
    ATTR{power/runtime_usage}=="0"
    ATTR{proto_down}=="0"
    ATTR{queues/rx-0/rps_cpus}=="00000000,00000000,00000000,00000000"
    ATTR{queues/rx-0/rps_flow_cnt}=="0"
    ATTR{queues/tx-0/byte_queue_limits/hold_time}=="1000"
    ATTR{queues/tx-0/byte_queue_limits/inflight}=="0"
    ATTR{queues/tx-0/byte_queue_limits/limit}=="7626"
    ATTR{queues/tx-0/byte_queue_limits/limit_max}=="1879048192"
    ATTR{queues/tx-0/byte_queue_limits/limit_min}=="0"
    ATTR{queues/tx-0/tx_maxrate}=="0"
    ATTR{queues/tx-0/tx_timeout}=="0"
    ATTR{queues/tx-0/xps_rxqs}=="0"
    ATTR{speed}=="1000"
    ATTR{statistics/collisions}=="0"
    ATTR{statistics/multicast}=="0"
    ATTR{statistics/rx_bytes}=="808920"
    ATTR{statistics/rx_compressed}=="0"
    ATTR{statistics/rx_crc_errors}=="0"
    ATTR{statistics/rx_dropped}=="0"
    ATTR{statistics/rx_errors}=="0"
    ATTR{statistics/rx_fifo_errors}=="0"
    ATTR{statistics/rx_frame_errors}=="0"
    ATTR{statistics/rx_length_errors}=="0"
    ATTR{statistics/rx_missed_errors}=="0"
    ATTR{statistics/rx_nohandler}=="0"
    ATTR{statistics/rx_over_errors}=="0"
    ATTR{statistics/rx_packets}=="2046"
    ATTR{statistics/tx_aborted_errors}=="0"
    ATTR{statistics/tx_bytes}=="157410"
    ATTR{statistics/tx_carrier_errors}=="0"
    ATTR{statistics/tx_compressed}=="0"
    ATTR{statistics/tx_dropped}=="0"
    ATTR{statistics/tx_errors}=="0"
    ATTR{statistics/tx_fifo_errors}=="0"
    ATTR{statistics/tx_heartbeat_errors}=="0"
    ATTR{statistics/tx_packets}=="1084"
    ATTR{statistics/tx_window_errors}=="0"
    ATTR{testing}=="0"
    ATTR{threaded}=="0"
    ATTR{tx_queue_len}=="1000"
    ATTR{type}=="1"

  looking at parent device '/devices/pci0000:00/0000:00:11.0/0000:02:01.0':
    KERNELS=="0000:02:01.0"
    SUBSYSTEMS=="pci"
    DRIVERS=="e1000"
    ATTRS{acpi_index}=="16777736"
    ATTRS{ari_enabled}=="0"
    ATTRS{broken_parity_status}=="0"
    ATTRS{class}=="0x020000"
    ATTRS{consistent_dma_mask_bits}=="32"
    ATTRS{d3cold_allowed}=="1"
    ATTRS{device}=="0x100f"
    ATTRS{dma_mask_bits}=="32"
    ATTRS{driver_override}=="(null)"
    ATTRS{enable}=="1"
    ATTRS{irq}=="19"
    ATTRS{label}=="Ethernet0"
    ATTRS{local_cpulist}=="0-1"
    ATTRS{local_cpus}=="00000000,00000000,00000000,00000003"
    ATTRS{msi_bus}=="1"
    ATTRS{numa_node}=="-1"
    ATTRS{power/async}=="enabled"
    ATTRS{power/control}=="on"
    ATTRS{power/runtime_active_kids}=="0"
    ATTRS{power/runtime_active_time}=="5645368"
    ATTRS{power/runtime_enabled}=="forbidden"
    ATTRS{power/runtime_status}=="active"
    ATTRS{power/runtime_suspended_time}=="0"
    ATTRS{power/runtime_usage}=="2"
    ATTRS{power/wakeup}=="disabled"
    ATTRS{power/wakeup_abort_count}==""
    ATTRS{power/wakeup_active}==""
    ATTRS{power/wakeup_active_count}==""
    ATTRS{power/wakeup_count}==""
    ATTRS{power/wakeup_expire_count}==""
    ATTRS{power/wakeup_last_time_ms}==""
    ATTRS{power/wakeup_max_time_ms}==""
    ATTRS{power/wakeup_total_time_ms}==""
    ATTRS{power_state}=="D0"
    ATTRS{remove}=="(not readable)"
    ATTRS{rescan}=="(not readable)"
    ATTRS{reset}=="(not readable)"
    ATTRS{reset_method}=="pm"
    ATTRS{revision}=="0x01"
    ATTRS{subsystem_device}=="0x0750"
    ATTRS{subsystem_vendor}=="0x15ad"
    ATTRS{vendor}=="0x8086"

  looking at parent device '/devices/pci0000:00/0000:00:11.0':
    KERNELS=="0000:00:11.0"
    SUBSYSTEMS=="pci"
    DRIVERS==""
    ATTRS{ari_enabled}=="0"
    ATTRS{broken_parity_status}=="0"
    ATTRS{class}=="0x060401"
    ATTRS{consistent_dma_mask_bits}=="32"
    ATTRS{d3cold_allowed}=="0"
    ATTRS{device}=="0x0790"
    ATTRS{dma_mask_bits}=="32"
    ATTRS{driver_override}=="(null)"
    ATTRS{enable}=="1"
    ATTRS{irq}=="0"
    ATTRS{local_cpulist}=="0-1"
    ATTRS{local_cpus}=="00000000,00000000,00000000,00000003"
    ATTRS{msi_bus}=="1"
    ATTRS{numa_node}=="-1"
    ATTRS{power/async}=="enabled"
    ATTRS{power/control}=="on"
    ATTRS{power/runtime_active_kids}=="4"
    ATTRS{power/runtime_active_time}=="5645405"
    ATTRS{power/runtime_enabled}=="forbidden"
    ATTRS{power/runtime_status}=="active"
    ATTRS{power/runtime_suspended_time}=="0"
    ATTRS{power/runtime_usage}=="1"
    ATTRS{power/wakeup}=="disabled"
    ATTRS{power/wakeup_abort_count}==""
    ATTRS{power/wakeup_active}==""
    ATTRS{power/wakeup_active_count}==""
    ATTRS{power/wakeup_count}==""
    ATTRS{power/wakeup_expire_count}==""
    ATTRS{power/wakeup_last_time_ms}==""
    ATTRS{power/wakeup_max_time_ms}==""
    ATTRS{power/wakeup_total_time_ms}==""
    ATTRS{power_state}=="D0"
    ATTRS{remove}=="(not readable)"
    ATTRS{rescan}=="(not readable)"
    ATTRS{revision}=="0x02"
    ATTRS{secondary_bus_number}=="2"
    ATTRS{subordinate_bus_number}=="2"
    ATTRS{subsystem_device}=="0x0790"
    ATTRS{subsystem_vendor}=="0x15ad"
    ATTRS{vendor}=="0x15ad"
    ATTRS{waiting_for_supplier}=="0"

  looking at parent device '/devices/pci0000:00':
    KERNELS=="pci0000:00"
    SUBSYSTEMS==""
    DRIVERS==""
    ATTRS{power/async}=="enabled"
    ATTRS{power/control}=="auto"
    ATTRS{power/runtime_active_kids}=="41"
    ATTRS{power/runtime_active_time}=="0"
    ATTRS{power/runtime_enabled}=="disabled"
    ATTRS{power/runtime_status}=="unsupported"
    ATTRS{power/runtime_suspended_time}=="0"
    ATTRS{power/runtime_usage}=="0"
    ATTRS{power/wakeup}=="disabled"
    ATTRS{power/wakeup_abort_count}==""
    ATTRS{power/wakeup_active}==""
    ATTRS{power/wakeup_active_count}==""
    ATTRS{power/wakeup_count}==""
    ATTRS{power/wakeup_expire_count}==""
    ATTRS{power/wakeup_last_time_ms}==""
    ATTRS{power/wakeup_max_time_ms}==""
    ATTRS{power/wakeup_total_time_ms}==""
    ATTRS{waiting_for_supplier}=="0"

~

## Задание 3.
1. Выгрузите модуль intel_rapl_msr.
2. Добавьте модуль intel_rapl_msr в черный список. Перезагрузите систему и убедитесь, что он не загружен.
3. Отмените свои изменения.

Выполнение:
1. Для выгрузки модуля используем команду `modprobe -r intel_rapl_msr`
2. Создаем файл для черного списка командой `sudo touch /etc/modprobe.d/blacklist-rapl.conf` и добавляем в него правило, запрещающее загрузку модуля при старте системы `echo "blacklist intel_rapl_msr" | sudo tee /etc/modprobe.d/blacklist-rapl.conf`
3. Проверяем командой `lsmod | grep intel_rapl_msr`, что отсутствует вывод, это говорит об успешности действий.  ![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251006121524.png?raw=true)
4. Возвращаем все как было: удаляем файл `rm /etc/modprobe.d/blacklist-rapl.conf` и загружаем модуль `modprobe intel_rapl_msr`. Проверяем изменения командой `lsmod | grep intel_rapl_msr` ![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251006121834.png?raw=true)


# Практическая работа 20. Сеть и стек TCP/IP, управление сетевыми интерфейсами
## Задание 1. 
Просмотр сетевых интерфейсов в терминале:
- Выведите список всех сетевых интерфейсов на компьютере и их текущее состояние (активный/неактивный).
- Выведите только IPv4 адрес каждого интерфейса.
- Выведите таблицу ARP (Address Resolution Protocol) для конкретного сетевого интерфейса eth0.
- Выполните трассировку маршрута к ya.ru, используя ICMP-пакеты, с ограничением количества запросов до 1.
- Выведите с использованием команды netstat список всех открытых прослушивающих (listening) портов (т.е. портов, на которых приложения ожидают входящие соединения).
Выполнение:
1. Чтобы посмотреть сетевые устройства и их состояние на машине воспользуемся командой `ip link show`
![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251007192942.png?raw=true)
    Результат вывода команды
2. Чтобы вывести только ipv4 адрес каждого устройства воспользуемся командой `ip -br -4 addr show`. Я воспользовался флагом `-br` чтобы вывод был более читабелен.
![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251007192933.png?raw=true)
	Результат вывода команды
3. Для выполнения 3 пункта воспользуюсь командой `sudo arp -i ens33`. В виду отсутствия интерфейса *eth0* буду выводить интерфейс *ens33*. В моём случае, перед тем как выполнить эту команду был установлен пакет *net-tools*, в котором находится утилита `arp`
![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251007192917.png?raw=true)
	Результат вывода команды
4. Трассировка маршрута будет выполнятся с помощью команды `sudo traceroute ya.ru -q 1 -I`
![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251007193557.png?raw=true)
5. Вывод портов, которые в данный момент будут прослушиваться будет осуществлен с помощью команды `netstat -tuln`
![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D1%8C%201.%20%D0%9E%D0%A1/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/Pasted%20image%2020251007193819.png?raw=true)

## Задание 2. 
Проверка DNS:
- Просмотрите текущие DNS-настройки, используя утилиту nmtui.
- Добавьте дополнительный DNS-сервер 1.1.1.1 и сделайте его первым в списке.
- Проверьте корректность работы новых DNS-настроек путем разрешения имен хостов в IP-адреса.
Выполнение:
1. Так как у меня нет графической оболочки, я пойду немного другим путем. Чтобы посмотреть текущие DNS-настройки я воспользуюсь командой `cat /etc/resolv.conf`. В результате получил следующий вывод: 
domain localdomain;
search localdomain;
nameserver 192.168.209.2;
2. Добавлю в этот список DNS 1.1.1.1 `echo "nameserver 1.1.1.1" | sudo tee /etc/resolv.conf`

