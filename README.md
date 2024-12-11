# Лабораторная работа 5
## Задание 1 - Автоматизация проверки формата файлов при коммите

### 1. Создаю bash-скрипт
Создайте файл с именем pre-commit в папке .git/hooks репозитория laba5
```bash
mkdir laba5
   cd laba5
   git init
touch .git/hooks/pre-commit
```
где команда git init создаст папку .git, внутри которой будет подкаталог hooks.
![e029bbfc-153d-4392-82c5-064f3704bd11](https://github.com/user-attachments/assets/ba6762b6-eb4b-4ff7-8977-fbf2908992ec)

### 2. Пишу скрипт
![6f617223-9378-47ff-a3c3-c7a577e12578](https://github.com/user-attachments/assets/15fcbe4f-c7cd-4063-a694-91bef18ba733)

### 3. Делаю скрипт исполняемым
```bash
chmod +x .git/hooks/pre-commit
```
Где 
- **+x** 'это араметр, который указывает, что вы хотите добавить (плюс +) право на выполнение (исполнение) файла (символ x). После выполнения этой команды файл станет исполняемым
- **.** Это путь к файлу, для которого вы хотите изменить права доступа.
- **.git**: Это скрытая директория, создаваемая Git в корне вашего репозитория, которая содержит все данные о версии и конфигурации вашего проекта.
- **hooks**: Это подкаталог внутри .git, который содержит скрипты хуков. Хуки — это специальные скрипты, которые Git выполняет в ответ на определенные события (например, перед коммитом, после коммита и т.д.).
- **pre-commit**: Это конкретный хук, который выполняется перед выполнением операции коммита. Вы можете использовать этот хук для проверки кода, запуска тестов или выполнения других автоматизированных задач перед тем, как изменения будут зафиксированы в репозитории.

### 4. Протестирую скрипт
1. Создаю новый файл **test_file.txt**
```bash
echo "Это пример файла." > test_file.txt
```

2. Далее добавляю этот файл в индекс Git и пробую выполнить коммит
```bash
git add test_file.txt
git commit -m "Тест коммита"
```
3. Проверяю разные состояния файла:
   - если файл с подписью:
     ![35253307-6e10-4a1d-9e08-e635764fddf2](https://github.com/user-attachments/assets/886981b3-8b04-40b8-83f5-7c5d81bf343c)
    ![2b82d4e2-e988-4a9e-a3f1-550384703226](https://github.com/user-attachments/assets/00ed7ae9-c9da-4e68-8882-146b242ad6b8)

   - если без подписи:
   
   ![73335e8d-7377-47c3-a7b1-275e90ebfdba](https://github.com/user-attachments/assets/6c83c9c0-7e11-4116-8cce-4f2dd139ecbb)
   ![534dd8df-19cd-4625-b63b-6e9761c3e78c](https://github.com/user-attachments/assets/453a3db6-f7dc-4287-9055-964247fcb584)
### 5. Итог
Формат файла автоматически проверяется с использованием Git Hooks

## Задание 2 - Автоматизация проверки формата файлов при коммите

1. Убедитесь, что Git Flow установлен на локальной машине:

```
sudo apt-get install git-flow
```
![photo_5391312343629161772_x (1)](https://github.com/user-attachments/assets/8c1f4972-157d-4622-be86-a5e6cec2686c)

2. В корне репозитория выполните инициализацию Git Flow.

```
git flow init
```

3. Создайте ветку для новой функциональности, допустим она называется "task-management":

```
git flow feature start task-management
```
![photo_5391312343629161773_x](https://github.com/user-attachments/assets/4dac49e8-82f8-474b-a79e-4534b8baa6c7)


4. Внесите изменения в код для добавления функционала управления задачами (например, в файл task_manager.py):
![photo_5391312343629161775_x](https://github.com/user-attachments/assets/fc90c64a-4139-4c47-83b1-77beb404d91d)
![2024-12-11_15-08-21 (2)](https://github.com/user-attachments/assets/b08e5bee-5bad-48cb-bb09-7e8c760476aa)

```
def create_task(title, description):
    # Логика создания задачи
    print(f"Создана новая задача: {title}")
```

Выполните коммит изменения по мере разработки:

```
git add task_manager.py
git commit -m "Добавлен функционал управления задачами"


```

5. После завершения разработки функции завершите фичу и объедините ее с основной веткой:
![photo_5391312343629161778_x](https://github.com/user-attachments/assets/bf141bc1-f682-49ad-ac57-7fb6b3d1452d)

```
git flow feature finish task-management

```

Git Flow автоматически переключится на ветку develop и выполнит слияние. Если есть конфликты, их нужно разрешить.

6. Переключитесь на ветку "develop" и начните создание релиза:
![photo_5391312343629161792_x](https://github.com/user-attachments/assets/763a5b16-9f6c-4e4e-87ce-6305aa4326f0)


```
git checkout develop
git flow release start v1.0.0
```

7. Внесите изменения, связанные с релизом (например, обновите версию в файле version.txt):

```
echo "v1.0.0" > version.txt
git add version.txt
git commit -m "Обновлена версия для релиза v1.0.0"

```
![photo_5391312343629161780_x](https://github.com/user-attachments/assets/e6251d38-c72a-4778-aec8-f00d9ba2c0f8)

8. Завершите релиз и объедините его с ветками "develop" и "main":
![photo_5391312343629161793_x](https://github.com/user-attachments/assets/cc765a74-cdb2-449a-a21f-bad477bb21b9)

```
git flow release finish v1.0.0
```

9. Если в процессе использования выявлена критическая ошибка, создайте hotfix (у нас конечно же ошибки никакой не возникнет, но hotfix все равно создаем):
![photo_5391312343629161783_x](https://github.com/user-attachments/assets/bb833eb8-4efa-4f77-bddb-dc3cb7e84265)

```
git flow hotfix start hotfix-1.0.1
```

10. Внесите изменения для исправления ошибки и коммитите:
![photo_5391312343629161784_x](https://github.com/user-attachments/assets/ba9aa064-488d-48e9-9ece-2c92ed42e9e7)
![2024-12-11_15-07-33 (1)](https://github.com/user-attachments/assets/5d176d20-f4ec-42c7-b133-a540e982b962)

```
# Исправление ошибки
git add file_with_error.py
git commit -m "Исправлена критическая ошибка"
```

11. Завершите hotfix и объедините его с ветками "develop" и "main":
![photo_5391312343629161785_x](https://github.com/user-attachments/assets/3868a522-27f4-48b1-b024-ebe944bcb3dd)
![photo_5391312343629161786_x](https://github.com/user-attachments/assets/7acc6844-eb5a-4615-8793-25ecc3ef1af4)

```
git flow hotfix finish hotfix-1.0.1
```

12. Завершение работы и отправка изменений на удаленный репозиторий. Отправьте изменения на удаленный репозиторий:
![photo_5391312343629161787_x](https://github.com/user-attachments/assets/4f34dba5-a5c7-4232-ba25-f2e3c93b665c)

```
git push origin develop
git push origin main

```
