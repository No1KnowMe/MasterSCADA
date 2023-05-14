# MasterSCADA
Мини проект по MasterSCADA 4D
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
