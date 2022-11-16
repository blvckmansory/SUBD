### E-Commerce Project

### Функциональные требования

**а)Авторизация пользователей**  
В авторизацию пользователей будет входить введение логина и пароля, после чего будет переход на страницу в зависимости от роли пользователя  

**б)Управление пользователями**  
Управление пользователями будет осуществляться через админ панель

**с)Система ролей**  
Система ролей будет состоять из:  
* Клиента  
    * Аутентификация
    * Взаимодействие с корзиной (добавление и удаление продукта)
    * Возможность оставить отзыв о продукте
    * Возможность оценить продукт
    * Сможет покупать товары, взаимодействовать с корзиной, оформлять заказ, заполнять платежные данные, просматривать информацию о заказе  
* Администратора  
    * Редактирование корзины (удаление, добавление, изменение кол-ва продуктов)
    * Удаление отзывов и оценок
    * Редактирование информации о пользователе
    * Проверка логов 
 

## Сущности
  
* User - все пользователи 
    * **UserId(int)** - UUID - Many to One к Роли
    * **RoleId(string)** - ключ
    * **Name(varchar(20))** - имя пользователя
    * **LastName(varchar(20))** - фамилия пользователя
    * **PhoneNumber(varchar(20))** - номер пользователя
    * **UserEmail(varchar(50))** - эл. почта пользователя
    * **UserPassword(varchar(250))** - пароль
* **Категория:**  
    *  **id(int)** One to Many к Продукту  
    *  **CategoryName(string 255)**   
* **Продукт**
    * **id(int)** Many to One к Категории, One to Many к Накладная-Продукт, One to Many к Деталям Заказа, One to Many к Корзине
    * **Name(string 255)**
    * **Price(double >0)**
    *  **Description(string 255)**
    * **Count(int >0)**
    * **Availibility(bool Default: true)**
* Платежные данные 
    * **id(int)** One to One к Клиенту
    * **NumberCard(int <=19)**
    * **PaymentDate(Date)**
    * **TimeTransaction(decimal)**
* Клиент
    * **id(int)** One to One к Платежным данным,  Many to One к Роли, Many to One к Заказа
    * **FirstName(string 255)**
    * **SecondName(string 255)**
    * **PhoneNumber(decimal)** 
* Менеджер
    * **id(int)** One to One к Платежным данным,  Many to One к Роли, Many to One к Заказа
    * **ManagerName(string)**
    * **ManagerSecondName(string 255)**
    * **PhoneNumber(decimal)** 
* Корзина 
    * **id(int)** One to One к Заказу, Many to One к Продукту, One to One к Клиенту
    * **EmptyCart(bool)**
* Заказ
    * **id(int)** One to One к Корзине, One to Many к Клиенту
    * **OrderNumber(decimal)**
    * **OrderDate(Date)**
    * **Status(bool)** 
* Роль 
    **id(int)** One to Many к Менеджеру, One to Many к Клиенту  
