# UnityBindingDemo

NData - плагин для NGUI, реализующий возможность биндинга между данными в коде и элементами пользовательского интерфейса.
Целью являлось написание аналога, который будет работать на Unity UI.

В репозитории представлено как само решение (Assets/BndSystem), так и сцена демонстрирующая возможности биндингов.

Полученное решение должно было быть достаточно производительным.
Данная цель была достигнута за счет кеширование get/set-методов свойств в делегаты.
Подробно об этом способе можно почитать здесь - http://stackoverflow.com/questions/7999652/best-way-to-cache-a-reflection-property-getter-setter

Также Ndata обладала недостатком, в виде необходимости писать громоздкий набор свойств. Пример:

	private readonly IntProperty m_fuelProperty = new IntProperty();
	public IntProperty fuelProperty { get { return m_fuelProperty; } }
	public int fuel { get { return fuelProperty.GetValue(); } set { fuelProperty.SetValue(value); } }

Такие меры имеют ряд недостатков в виде нечитабельного кода, большой вероятности допустить ошибку, и необходимости помечать свойство как public, что противоречит идеологии ООП

Мое решение избавлено от большинства данных недостатков, в коде достаточно объявить всего одно привычное свойство:

public int Fuel {get; set;}

Если нужен биндинг для компонента которому требуется только get (например label должен выводить значение переменной из контекста), то set можно установить в private:

public int Fuel {get; private set;}
