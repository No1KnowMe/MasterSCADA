# MasterSCADA
<p>Мини-проект по MasterSCADA 4D – задействовано создание узлов, объектов (окон, параметров, функций и ФБ, а также создание графиков с возможностью архивации сообщений), библиотек (локальных и внешних) и ограничение действий пользователей в зависимости от ролей.</p>
<p>Соединение происходит по протоколу OPC UA.</p>
<p>Архивация сообщений происходит в базе данных на основе sqlite.</p>
<p>Чтобы посмотреть проект в действии, Вам необходимо скачать архив репозитория и открыть папку проекта через программу "MasterSCADA 4D".</p>

<h2>Постановка задачи</h2>

<p>Есть две одинаковые емкости, в которых подогревается жидкость. Сначала идет наполнение емкости, потом нагрев, потом слив. В каждой емкости есть два датчика: датчик температуры, датчик уровня. На верхний уровень значения приходят по протоколу OPC UA.</p>
<p>Список параметров:</p>

<table cellspacing="0" cellpadding="0" border="1">
	<tbody>
		<tr>
			<td>
			<p>Название</p>
			</td>
			<td>
			<p>Описание</p>
			</td>
			<td>
			<p>Ед. изм.</p>
			</td>
			<td>
			<p>Диапазон</p>
			</td>
		</tr>
		<tr>
			<td>
			<p>L1</p>
			</td>
			<td>
			<p>Уровень емкости 1</p>
			</td>
			<td>
			<p>м</p>
			</td>
			<td>
			<p>0-12</p>
			</td>
		</tr>
		<tr>
			<td>
			<p>L2</p>
			</td>
			<td>
			<p>Уровень емкости 2</p>
			</td>
			<td>
			<p>м</p>
			</td>
			<td>
			<p>0-12</p>
			</td>
		</tr>
		<tr>
			<td>
			<p>Т1</p>
			</td>
			<td>
			<p>Температура емкости 1</p>
			</td>
			<td>
			<p>С</p>
			</td>
			<td>
			<p>0-100</p>
			</td>
		</tr>
		<tr>
			<td>
			<p>Т2</p>
			</td>
			<td>
			<p>Температура емкости 2</p>
			</td>
			<td>
			<p>С</p>
			</td>
			<td>
			<p>0-100</p>
			</td>
		</tr>
	</tbody>
</table>

<p>Параметры в OPC UA сервере меняются не чаще, чем раз в секунду.</p>
<p>Оператор в клиенте визуализации должен видеть текущие значение, а также отследить изменение параметров во времени.</p>
<p>Для каждой емкости нужно отслеживать ВАГ, НАГ, ВПГ, НПГ значений уровня – должны формироваться сообщения в журнале.</p>
<p>Значения границ уровня:</p>

<table cellspacing="0" cellpadding="0" border="1">
	<tbody>
		<tr>
			<td>
			<p><strong>Граница</strong></p>
			</td>
			<td>
			<p><strong>Значение</strong></p>
			</td>
		</tr>
		<tr>
			<td>
			<p>Верхняя аварийная границы (ВАГ)</p>
			</td>
			<td>
			<p>11,5</p>
			</td>
		</tr>
		<tr>
			<td>
			<p>Верхняя предупредительная граница (ВПГ)</p>
			</td>
			<td>
			<p>10</p>
			</td>
		</tr>
		<tr>
			<td>
			<p>Нижняя предупредительная граница</p>
			</td>
			<td>
			<p>2</p>
			</td>
		</tr>
		<tr>
			<td>
			<p>Нижняя аварийная граница</p>
			</td>
			<td>
			<p>0.5</p>
			</td>
		</tr>
	</tbody>
</table>

<p>Кроме того, если значение температуры превысит "Уставку Т" и значение уровня будет ниже "Уставки У", то нужно выдавать сообщение: «Критичные показатели». Значения уставок задает оператор в режиме исполнения для каждой из емкостей.</p>
<p>Значения аналоговых параметров архивируются.</p>
<p>Клиент визуализации запускается на том же компьютере, что и исполнительная система. Действия пользователей (операторов) в клиенте визуализации должны фиксироваться.</p>
<p>Данные будем получать с онлайн-стенда.&nbsp;</p>
<p>Данные для доступа к стенду:</p>
<p>&nbsp;IP-адрес -&nbsp;91.221.70.79</p>
<p>&nbsp;TCP-порт - 17001</p>

<h2>Конечный вид программы</h2>
<figure>
	<img src="https://github.com/No1KnowMe/MasterSCADA/assets/99428156/4dbf3b6e-6caa-42bf-9f01-8f9c6f888929">
	<figcapture>Стартовое окно (Авторизация).</figcapture>
</figure>
<p>&nbsp;</p>

<p>При запуске проекта стартовым окном является страница авторизации – далее, в зависимости от роли (Администратор, Оператор и Стажер) открывается следующее окно.</p>
<p>Например, у пользователей с ролью "Администратор" после окна авторизации открывается окно управления аккаунтами – они могут добавлять новых и удалять старых пользователей.</p>
<figure>
	<img src="https://github.com/No1KnowMe/MasterSCADA/assets/99428156/69d6fcdf-1b9b-4d3b-b626-23eea2f7b0b1">
	<figcapture>Окно управления аккаунтами пользователей.</figcapture>
</figure>
<p>&nbsp;</p>

<p>При нажатии на кнопку "Контроль уровня" откроется следующее окно:</p>
<figure>
	<img src="https://github.com/No1KnowMe/MasterSCADA/assets/99428156/098a3504-c1c0-43a9-a898-1dfb3cb5f970">
	<figcapture>Окно контроля температуры и уровня жидоксти в резервуарах.</figcapture>
</figure>
<p>&nbsp;</p>

<p>При двойном нажатии на изображение емкости откроется поля ввода уставок по температуре (T) и уровню (L), а также тренд с архивацией сообщений.</p>
<figure>
	<img src="https://github.com/No1KnowMe/MasterSCADA/assets/99428156/5a1d9590-def9-45f1-9dd5-f7f70b14c976">
	<figcapture>Всплывающее окно по конфигурации емкости.</figcapture>
</figure>
<p>&nbsp;</p>

<p>Также указаны данные пользователя, который в данный момент следит за этим окном – логин, группа и адрес пользователя. Так как исполнительная система запускается на локальном компьютере, то и адрес соотвествует локальному серверу.</p>
<p>При нажатии кнопки "Завершить сессию" пользователь выйдет из учетной записи и будет перенаправлен на страницу авторизации.</p>

<h2>Общий вид проекта в среде разработки</h2>
<img src="https://github.com/No1KnowMe/MasterSCADA/assets/99428156/22010f4f-8d19-468f-9de1-005bc6b8520e">
