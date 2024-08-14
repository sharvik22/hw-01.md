# Домашнее задание к занятию «Введение в Terraform» Шарапат Виктор

### Цели задания

1. Установить и настроить Terrafrom.
2. Научиться использовать готовый код.

------

### Чек-лист готовности к домашнему заданию

1. Скачайте и установите **Terraform** версии ~>1.8.4 . Приложите скриншот вывода команды ```terraform --version```.
2. Скачайте на свой ПК этот git-репозиторий. Исходный код для выполнения задания расположен в директории **01/src**.
3. Убедитесь, что в вашей ОС установлен docker.

1)
![Screenshot_1](https://github.com/user-attachments/assets/6ebae687-4170-4697-b28b-c4b0e2a7c1c5)

2)
![image](https://github.com/user-attachments/assets/6099bb52-433d-4501-b8a6-b207738d96fb)

3)
![image](https://github.com/user-attachments/assets/4cac0770-1d1e-48fd-892a-6346f9ff91ad)

------

### Инструменты и дополнительные материалы, которые пригодятся для выполнения задания

1. Репозиторий с ссылкой на зеркало для установки и настройки Terraform: [ссылка](https://github.com/netology-code/devops-materials).
2. Установка docker: [ссылка](https://docs.docker.com/engine/install/ubuntu/). 
------
### Внимание!! Обязательно предоставляем на проверку получившийся код в виде ссылки на ваш github-репозиторий!
------

### Задание 1

1. Перейдите в каталог [**src**](https://github.com/netology-code/ter-homeworks/tree/main/01/src). Скачайте все необходимые зависимости, использованные в проекте. 
2. Изучите файл **.gitignore**. В каком terraform-файле, согласно этому .gitignore, допустимо сохранить личную, секретную информацию?(логины,пароли,ключи,токены итд)
3. Выполните код проекта. Найдите  в state-файле секретное содержимое созданного ресурса **random_password**, пришлите в качестве ответа конкретный ключ и его значение.
4. Раскомментируйте блок кода, примерно расположенный на строчках 29–42 файла **main.tf**.
Выполните команду ```terraform validate```. Объясните, в чём заключаются намеренно допущенные ошибки. Исправьте их.
5. Выполните код. В качестве ответа приложите: исправленный фрагмент кода и вывод команды ```docker ps```.
6. Замените имя docker-контейнера в блоке кода на ```hello_world```. Не перепутайте имя контейнера и имя образа. Мы всё ещё продолжаем использовать name = "nginx:latest". Выполните команду ```terraform apply -auto-approve```.
Объясните своими словами, в чём может быть опасность применения ключа  ```-auto-approve```. Догадайтесь или нагуглите зачем может пригодиться данный ключ? В качестве ответа дополнительно приложите вывод команды ```docker ps```.
8. Уничтожьте созданные ресурсы с помощью **terraform**. Убедитесь, что все ресурсы удалены. Приложите содержимое файла **terraform.tfstate**. 
9. Объясните, почему при этом не был удалён docker-образ **nginx:latest**. Ответ **ОБЯЗАТЕЛЬНО НАЙДИТЕ В ПРЕДОСТАВЛЕННОМ КОДЕ**, а затем **ОБЯЗАТЕЛЬНО ПОДКРЕПИТЕ** строчкой из документации [**terraform провайдера docker**](https://docs.comcloud.xyz/providers/kreuzwerker/docker/latest/docs).  (ищите в классификаторе resource docker_image )


------

### Решение 1

2. Изучите файл **.gitignore**. В каком terraform-файле, согласно этому .gitignore, допустимо сохранить личную, секретную информацию?(логины,пароли,ключи,токены итд)
   
Сохранить личную, секретную информацию (логины, пароли, ключи, токены и т.д.) допустимо в файле personal.auto.tfvars. 


3. Выполните код проекта. Найдите  в state-файле секретное содержимое созданного ресурса **random_password**, пришлите в качестве ответа конкретный ключ и его значение.

terraform init

![image](https://github.com/user-attachments/assets/06bb9eac-ec82-4fd9-a7e1-8559dbe2ad1a)

terraform plan

![image](https://github.com/user-attachments/assets/d2f65390-bee0-41e8-a359-4644d8c417cf)

terraform apply

![image](https://github.com/user-attachments/assets/07cfbf73-51e5-472c-82c0-df6154ac7efd)

![image](https://github.com/user-attachments/assets/b7a1d1e7-aac4-4466-a7c3-d8a087feddac)


nano terraform.tfstate

![image](https://github.com/user-attachments/assets/3a5d6070-8c20-47f8-9dde-65db89014759)


4. Раскомментируйте блок кода, примерно расположенный на строчках 29–42 файла **main.tf**.
Выполните команду ```terraform validate```. Объясните, в чём заключаются намеренно допущенные ошибки. Исправьте их.

terraform validate

![image](https://github.com/user-attachments/assets/d3a593f3-650e-40c5-9c62-9a4d09826fb9)

Неверный синтаксис:

Отсуствует имя ресурса resource "docker_image

Не верное имя ресурса 1nginx

![image](https://github.com/user-attachments/assets/46f3de56-e103-46d0-9b74-1c1d19981bf4)

5. Выполните код. В качестве ответа приложите: исправленный фрагмент кода и вывод команды ```docker ps```.

terraform apply

![image](https://github.com/user-attachments/assets/dfc96386-1b00-48f5-b06a-e9ac43beec12)

![image](https://github.com/user-attachments/assets/abe61190-29ad-434e-a94d-715b1b39105b)

![image](https://github.com/user-attachments/assets/dce7bed6-a716-4850-8d0c-f112ccebcf73)

исправленный фрагмент кода:

resource "docker_image" "nginx" {
  name         = "nginx:latest"
  keep_locally = true
}

resource "docker_container" "nginx" {
  image = docker_image.nginx.image_id
  name  = "example_${random_password.random_string.result}"
  

6. Замените имя docker-контейнера в блоке кода на ```hello_world```. Не перепутайте имя контейнера и имя образа. Мы всё ещё продолжаем использовать name = "nginx:latest". Выполните команду ```terraform apply -auto-approve```.
Объясните своими словами, в чём может быть опасность применения ключа  ```-auto-approve```. Догадайтесь или нагуглите зачем может пригодиться данный ключ? В качестве ответа дополнительно приложите вывод команды ```docker ps```.

![image](https://github.com/user-attachments/assets/8bbcfbab-6858-4bfe-b730-527b7d11d9a3)

terraform apply -auto-approve

![image](https://github.com/user-attachments/assets/1ee8db1a-7861-43d8-91a7-42b913f5301b)

docker ps

![image](https://github.com/user-attachments/assets/6fdae254-a5af-48d5-ad61-3acde52af08b)


Опасность применения ключа -auto-approve заключается в том, что Terraform не запрашивает подтверждения перед применением изменений, а это в свою очередь может привести к риску потери данных, отсутсвию проверки и немедленному применению изменений.

Ключа -auto-approve может пригодиться в скриптах, где требуется последовательное выполнение команд, ну или в проверенных сценариях (CI/CD).


7. Уничтожьте созданные ресурсы с помощью **terraform**. Убедитесь, что все ресурсы удалены. Приложите содержимое файла **terraform.tfstate**. 

terraform destroy

![image](https://github.com/user-attachments/assets/df9a2668-dae6-4d7f-b381-8388d78c6638)

nano terraform.tfstate

![image](https://github.com/user-attachments/assets/6da6d4ff-48eb-44e6-a48b-42ce3fbee13d)


8. Объясните, почему при этом не был удалён docker-образ **nginx:latest**. Ответ **ОБЯЗАТЕЛЬНО НАЙДИТЕ В ПРЕДОСТАВЛЕННОМ КОДЕ**, а затем **ОБЯЗАТЕЛЬНО ПОДКРЕПИТЕ** строчкой из документации [**terraform провайдера docker**](https://docs.comcloud.xyz/providers/kreuzwerker/docker/latest/docs).  (ищите в классификаторе resource docker_image )

Образ не был удален, т.к. в конфигурации есть параметр keep_locally = true, который предотвращает удаление образа при уничтожении ресурсов Terraform.

resource "docker_image" "nginx" {
  name         = "nginx:latest"
  keep_locally = true
}

![image](https://github.com/user-attachments/assets/97ee41c2-cef6-4e20-83d0-a127fd25c4ae)

-------
