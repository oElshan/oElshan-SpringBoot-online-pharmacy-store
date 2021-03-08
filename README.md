pharmacy-market.herokuapp.com/

<h1> Online pharmacy store</h1>

<h2>Технологии</h2>

<ul class="discharged">
    <li>JDK 1.8, Spring Boot (v2.3.8), Thymeleaf</li>
    <li>авторизация пользователей: Spring Security</li>
    <li>доступ к данным: Hibernate, Spring Data JPA</li>
    <li>веб-служба в стиле REST</li>
    <li>тесты: Spring Test, JUnit, Mockito</li>
    <li>веб-интерфейс: jQuery, jQuery Validate Plugin, Twitter Bootstrap</li>
    <li>база данных: MySQL</li>
    <li>контейнер сервлетов: Apache Tomcat 9</li>
    <li>сборка и деплой проекта: Maven </li>
</ul>

<h2>Функционал магазина</h2>

<ol class="discharged">
    <li>Наглядное представление ассортимента товаров</li>
    <li>Корзина покупателя
        <ul>
            <li>выбор товаров: добавление, удаление, изменение количества</li>
            <li>просмотр содержимого корзины</li>
            <li>оформление заказа</li>
            <li>хранение корзины покупателя в сессии и куки</li>
        </ul>
    </li>
    <li>Панель управления магазином
        <ul>
            <li>просмотр информации о заказах, редактирование </li>
            <li>поиск товаров по имени</li>
            <li>товары и категории: добавление, редактирование, удаление</li>
            <li>изменение статусов заказа</li>
            <li>поиск заказов</li>
        </ul>        
    </li>
    <li>Безопасный доступ к приложению
        <ul>
            <li>регистрация и авторизация пользователей</li>
            <li>ограничение доступа к панели управления</li>
        </ul>
    </li>
    <li>Двойная проверка содержимого форм: на стороне клиента и на стороне сервера</li>
</ol>

<h2>Валидация форм</h2>

<p>Проверка данных всех форм пользовательского и административного интерфейса выполняется
    дважды: на стороне пользователя и на стороне сервера.</p>
<ul class="discharged">
    <li>Проверка на стороне пользователя осуществляется с использованием jQuery Validate Plugin,
        который проверяет данные в момент ввода средствами JavaSript. Для посимвольной проверки строки применены
        регулярные выражения (regex). Визуализация дополнена классами Bootstrap.</li>
    <li>Проверка на стороне сервера выполняется с использованием пакетов <code>javax.validation</code> и
        <code>org.springframework.validation</code>.</li>
</ul>
<p>Такой подход к валидации форм делает процесс проверки данных комфортным
    для пользователя и вместе с тем гарантирует выполнение проверки при отключённом
    JavaScript в браузере пользователя.</p>  
    
 
<h2>Безопасность</h2>

<p>За безопансотсь приложения овтечает Spring Security.</p>
 <p>Класс <code>MultiHttpSecurityConfig</code> отвечает за два вида аутентификации LoginForm и httpBasic для REST </p>




<h2>Обработка исключений</h2>

<p>В приложении реализована централизованная обработка исключений классом
    <code>ExceptionControllerAdvice</code> с аннотацией
    <code>@ControllerAdvice</code>, предоставленной Spring. А также обработка исключений для REST запросов</p>

<h2>Модель базы данных</h2>

<p>База данных приложения состоит из 11 связанных таблиц, отображаемых средствами Hibernate в 11 классов Entity.</p>

<p>Слой доступа к данным представлен классами Repository, функций разбивки на страницы и сортировки реализован
    с помощью репозитория Spring Data JPA.</p>

<h2>Пользовательские классы Spring</h2>

<p>Функционал фреймворков Spring MVC и Spring Security расширен следующими классами:</p>
<ul class="discharged">
    <li><code>UserDetailsServiceImpl</code> реализует интерфейс <code>UserDetailsService</code>
        и обеспечивает извлечение профиля пользователя из базы данных;</li>
    <li><code>ContextOnListener</code> реализует интерфейс  <code>ApplicationListener<ContextRefreshedEvent></code>
        при инициализации контектста приложения запрашивает в базе данные о категории товаров и производителей записывая 
        их в переменную ServletContext обеспечивая быструю загрузку и уменьшение количества обращений к базе</li>
    <li><code>ExceptionControllerAdvice</code> осуществляет централизованную обработку исключений;</li>
    <li><code>SessionCartInterceptor</code> реализует интерфейс <code>HandlerInterceptorAdapter</code>
        и проверяет до обработки запроса контроллерами, существует ли атрибут корзины покупателя в сессии или куки;
        при отсутствии создатся новая корзина; такое решение позволяет централизовать создание корзины,
        в том числе для случая, когда браузер пользователя не принимает cookies и поэтому
        не поддерживает хранение параметров сессии;</li>
</ul>

<h1>Веб-служба REST</h1>

<p>REST-интерфейс приложения предоставляет доступ к ресурсам магазина: позволяет запрашивать
    сведения о товарах, заказах и производить оформление заказов.</p>
<p>Обмен данными между клиентом и веб-службой магазина осуществляется в формате JSON,
    аутентификация выполняется средствами Basic Authentication за cчет второй точки входа в Spring Security.</p>
<p>В соответствии со стилем REST, взаимодействие между клиентом и сервером лишено
    сеансового состояния, поэтому веб-служба магазина не предоставляет гостевую
    корзину и не хранит ее в сессии: информация о товарах доступна всем клиентам, но заказ может быть
    собран и оформлен только зарегистрированным пользователем.</p>

<h2>Взаимодействие с веб-службой</h2>

<p>Доступ к ресурсам магазина можно получить с использованием любого HTTP-клиента,
    поддерживающего Basic-аутентификацию.Доступ к веб службе REST осуществляется черех url /rest**</p>

<h2>Операции с ресурсами</h2>

<h4>Сведения о товарах</h4>
<table class="table table-marked">
    <thead>
        <tr>
            <th width="200">ресурс</th>
            <th width="170">описание</th>
            <th>статусы ответа</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>GET /products</td>
            <td>Возвращает перечень всех товаров магазина</td>
            <td>200</td>
        </tr>
        <tr>
            <td>GET /products/:id</td>
            <td>Возвращает товар с указанным id</td>
            <td>200 — товар возвращён в теле ответа,<br>
                404 — товара с таким id не существует</td>
        </tr>
    </tbody>
</table>


<h4>Админстрирование заказов (требует авторизации)</h4>
<table class="table table-marked">
    <thead>
        <tr>
            <th width="200">ресурс</th>
            <th width="170">описание</th>
            <th>статусы ответа</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>GET /admin/orders</td>
            <td>Возвращает все заказы </td>
            <td>200 — контактные данные возвращены в теле ответа</td>
        </tr>
         <tr>
                    <td>GET /admin/orders/id</td>
                    <td>Возвращает заказ по id </td>
                    <td>200 — контактные данные возвращены в теле ответа</td>
                </tr>
        <tr>
            <td>POST /admin/orders</td>
            <td>Создает новый заказ</td>
            <td>201 — заказ создан, данные возвращены в теле ответа,<br>
                406 — некорректный формат полученных данных; пояснения в теле ответа</td>
        </tr>
        <tr>
            <td>DELETE /admin/orders</td>
            <td>Удаление заказа</td>
            <td>200 — заказ удален</td>
        </tr>
    </tbody>
</table>

