# SuiteCrm
**проект in4security**

## 🏰 Структура CRM системы.

```
📁 crm
├─📁 .git                    Данные репозитория
├─📁 Api                     ? Какое-то Api ( назначение не понятно )
├─📁 build                   ? что-то ( назначение не понятно )
├─📁 cache                   Кеш всего в CRM системе 
├─📁 custom                  Переопределение/Дополнение системы 
│ ├─📁modulebuilder              папки с файлами конфигураций модулей созданных в "Конструкторе модулей"
│ └─📄custom                     Определение меню профиля(Правый верхний угол)
├─📁 data                    ? содержет что то вроде моделей ( назначение не понятно )
├─📁 dbdata                  ! в DEV окружении не используемая директория ( назначение не понятно )
├─📁 dist                    ? Дистрибутив som.hrar ( назначение не понятно )
├─📁 include                 Содержет системные компоненты 
├─📁 install                 Директория с установочными файлами  
├─📁 jssource                Библиотека структурированных JS файлов
├─📁 lib                     Подключеные к проекту библиотеки
├─📁 metadata                Метадата модулей (описание модулей для системы)
├─📁 ModuleInstall           Системная папка расширения функционала модулей
├─📁 modules                 Модули системы
├─📁 packages                Пакеты системы (судя по всему установленные)
├─📁 public                  ! в DEV окружении не используемая директория ( назначение не понятно )
├─📁 service                 "Компоненты" системы
├─📁 soap                    SOAP
├─📁 tests                   Тесты 
├─📁 themes                  Темы (шаблоны)
├─📁 upload                  Дирекория загружаемых файлов
├─📁 upload_1                Дирекория для загружаемых файлов ( зачем две - это Вопрос... )
├─📁 vendor                  Директория в которой живёт Composer 
├─📁 XTemplate               XTemplate
├─📁 Zend                    Zend folder 
│ ...
├─📄 config.php              Конфиг системы (генерируется) 
└─📄 config_override.php     Обновление значений конфига (генерируется)
```

### 🧱 Структура "модуля" CRM системы.
```
📁 Dashlets                  Файлы описывают визуал для главной страницы
📁 language                  Локализация
📁 metadata                  описывают блок модуля при разных 'action'
📁 tpl                       Используемые шаблоны модуля, шаблонизатора Smarty
📁 views                     Стандартные шаблоны модуля для 'actions' index, view, edit
📄 vardefs.php               Определение модуля (его структура/схема/ поля)
📄 JustFile.php              Просто файл = "action"
```

__________

<p align="center">_ _ _ _ _ _ _ _ _ _</p>

# 🔌 Установка.


## Требования
* **PHP** 7.2.31
* **MariaDB** 10.4.11
* **Zend Engine** v3.2.0
* **Zend OPcache** v7.2.31


### 1. Скачивание
1.1 Получить доступ к репозиторию.  
1.2 В консоле  
1.2.1 Переходим в директорию куда надо скачать проект  
1.2.2 выполнить команду клонирования:  
⌨ `git clone git@sec-abathur.iss.corp:iss-crm/suitecrm.git .`  
⌨ `git clone https://sec-abathur.iss.corp/iss-crm/suitecrm.git .`  
либо без точки для создания директории проекта.



### 2. Установка зависимотей
Если **composer** <u>не установлен локально</u>, то скачать **composer.phar** с
<a href="https://getcomposer.org/download/">официального сайта</a>
в корневую дирекорию проекта(туда клонировался проект).

Выполнить в консоле команду, если **composer** локально:

| установлен     | не установлен               |
|--------------------|-----------------------------|
| `composer install` | `php composer.phar install` |


#### ERRORS
Возможные ошибки:

* ***Ошибка:*** Composer #.#.# dropped support for PHP <{A.B.C} and you are running #.#.#  
    * ***Решение:*** Необходимо сменить используемую версию PHP на версию. {A.B.C}  
_____
  
* ***Ошибка:*** Root composer.json requires php >=7.2.3 but your php version ({#.#}; overridden via config.platform, actual: {A.B.C}) does not satisfy that requirement.  
    * **Решение:** файл `📄 composer.json` внести изменение в элемент : `config.platform.php` указав предлогаемую версию: {A.B.C}.  
      ( ВНИМАНИЕ! эти изменения не коммитится )
_____
  
* ***Ошибка:*** Root composer.json requires PHP extension ( ext-curl || ext-gd || ext-json || ext-openssl || ext-zip || ext-imap )  *  
    * **Решение:** Как правило достатовно раскоментировать строку в файле настроек `📄 php.ini`
```ini
;extension  = imagick
; Раскоментировать `extension = imap` и другие необходимые расширения php
extension = imap
;extension = interbase
```  
_____
  
* ***Ошибка:*** package/module is locked to version {A.B.C}-alpha and an update of this package was not requested.  
    * **Решение:** Как правило достатовно удалить файл `📄 composer.look`  
_____
  
* ***Ошибка:*** requires ext-{name} * -> it is missing from your system. Install or enable PHP's {name} extension.  
    * **Решение:** Необходимо установить php расширение( Закинуть `.dll` файл в папку с модулями в дириктории с php )  
_____
  
  
### 3. Конфигурация
В корневую папкупроекта скачать с "DEMO станда" файлы конфигурации:
* `📄 config.php`
* `📄 config_override.php`



### 4. База данных
Создать базу данных:
`in4sec_crm`

Кодировка бы данных `utf8_general_ci`  
Задаётся в файле: `config.php`


#### Dump.
Миграции отсутствуют. Поэтому в настоящее время заливается `Dump` базы данных.  
После получения доступа к серверу `BD` сделать `export`:  
⌨ `mysqldump -u <username> -p <databasename> > <filename.sql>`  
Далее импортировать в свою `BD`:  
⌨ `mysql -u <username> -p <databasename> < <filename.sql>`



### 5. Обращение к сервису
Настроить домен <b>https://in4sec.crm</b> на работу сервиса, домен должен "смотреть" в корневую директорию проекта.

#### OpenServer
Настройки > вкладка "Домены":  
заполняются поля:
* <b>Имя домена:</b> <i> https://in4sec.crm </i>
* <b>Папка домена:</b> <i> some\path\suiteCrm\ </i>



### 6. Восстановление
1. [Авторизоваться](https://in4sec.crm) в системе
2. перейти в раздел [Администрирование](https://in4sec.crm/index.php?module=Administration&action=index) > [Восстановление](https://in4sec.crm/index.php?module=Administration&action=Upgrade)  
   Выполнить
>  [Быстрое восстановление](https://in4sec.crm/index.php?module=Administration&action=repair)


__________

<p align="center">_ _ _ _ _ _ _ _ _ _</p>

## Детальная информация версий ПО на DEMO сервере.
* **MariaDB** 10.4.11-MariaDB-1:10.4.11+maria~stretch-log mariadb.org binary distribution
* **PHP** 7.2.31-1+0~20200514.41+debian9~1.gbpe2a56b (cli) (built: May 14 2020 08:33:26) ( NTS )
* **Zend Engine** v3.2.0
* **Zend OPcache** v7.2.31-1+0~20200514.41+debian9~1.gbpe2a56b

__________

<p align="center">_ _ _ _ _ _ _ _ _ _</p>

Легенда:
* `(a+)` — если файла нет его необходимо создать
* `{ pack }`  — название директории существующего или нового (созданного "Пакета")
* `{ module }`  — название директории существующего или нового (созданного "Модуля")
* `'{{custom_field_id}}'`  — идентификатор существующего или нового(созданного) поля
* `'{{custom_field_label}}'`  — идентификатор названия(заголовка/лэйбла) существующего или нового(созданного) поля

<p align="center">_ _ _ _ _ _ _ _ _ _</p>

# WorkFlow

### 🎨 Добавление "модуля" в CRM систему.
1. [Администрирование](https://in4sec.crm/index.php?module=Administration&action=index)
   \> [Конструктор модулей](https://in4sec.crm/index.php?module=ModuleBuilder&action=index&type=mb)
> [Новый Пакет](https://in4sec.crm/index.php?module=ModuleBuilder&action=index&type=mb#ajaxUILoc=&mbContent=module%3DModuleBuilder%26action%3Dpackage%26new%3D1)
- Заполнить 2 обязательных поля (другие по желанию):
    - Название пакета: ____
    - Ключ: ____
- **[сохранить]**
    - **[Новый модуль]**


2. Конструктор модулей >  "Созданный Пакет" > Новый модуль.
    - Заполнить обязательные поля:
        - "Название модуля:" ____
        - "Надпись:" _____
        - выбрать необходимый тип ( достаточно "Базовый")
    - **[сохранить]**


3. Конструктор модулей > "Созданный Пакет"
    - **[Установить]**
      7
__________

<p align="center">_ _ _ _ _ _ _ _ _ _</p>

### 📎 Добавление "поля" для модуля CRM системы.
Если нет тестового модуля и пакета, создать (см. выше)  
Далее, **создание полей**:
1. Конструктор модулей > "Тестовый пакет" > "Тестовый модуль" > Поля
2. **[добавить поле]**
    - Заполнить минимальный пул данных:
        - "Название поля:" _____
            * название поля для идентификации в системе
            * ссылка в документе на значение поля -> [`'{{custom_field_id}}'`]
        - "Отображаемая надпись:" _____
            * текст поля для LABEL. (обычно русский язык)
        - "Системная надпись:" _____
            * идентификатор генерируемый системой на основе "Название поля"
            * ссылка в документе на значение поля -> [`'{{custom_field_label}}'`]
    - Далее заполняется по необходимости...
    - "Значение по умолчанию:" _____
    - "Максимальный размер:" _____
    - и т.д. ...
    - **[сохранить]**

3. В директории `📁 \custom\modulebuilder\packages\`  
   находим дирикторию созданного пакета и созданного модуля `📁 { pack }\{ module }`  
   внутри файл `📄 vardefs.php` из которого забирем конфигурацию созданных полей.  
   Полный путь к файлу `📄 \custom\modulebuilder\packages\{ pack }\{ module }\vardefs.php`


4. Перенос конфигурации созданных полей, в расширяемый модуль.  
   Добавляется новый элемент массива в файл `📄 \custom\extansions\modules\{ module }\Ext\vardefs\custom_fields.php`(a+)
```php
// Add {date} {author}
$dictionary['{ module }']['fields'][ '{{custom_field_id}}' ]=array(
   // конфигурация поля из файла: 📄 custom\modulebuilder\packages\{ pack }\{ module }\vardefs.php
);
```


5. Описание полей (локализация).  
   Из сгенерированого системой файла  
   `📄 \custom\modulebuilder\packages\{ pack }\modules\{ module }\language\ru_ru.lang.php`  
   строки с названием сгенерированых полей и перенести в файл  
   `📄 \custom\extansions\modules\{ module }\Ext\Language\ru_ru.custom_fields.php`(a+)
```php
// Add {date} {author}
$mod_string[ '{{custom_field_label}}' ] = "Русскоязычное название поля";
```


6. Добавление свойств в класс модуля.  
   Модуль описывается в файле `📄 \modules\{ module }\{ camelCaseModuleFileName }.php`
```php
class СamelCaseModuleFileName extends SugarBean /* Или другой класс */ {
    // ... какой то код "до" ...
    
    // Add {date} {author}
    public $new_field_id //Имя свойства соответствует [{{custom_field_id}}] 
    
    // ... какой то код "после"
}
```

7. Применение изменений в CRM.  
   [Администрирование](https://in4sec.crm/index.php?module=Administration&action=index) > [Восстановление](https://in4sec.crm/index.php?module=Administration&action=Upgrade)
> [Быстрое восстановление](https://in4sec.crm/index.php?module=Administration&action=repair)

( не закрывая окно, переходим к следующему шагу)

8. Обновление структуры базы данных.  
   На странице результата "Быстрого восстановления"
   необходимо выполнить SQL запрос сгенерированный системой  
   кнопка **[выполнить]**

__________

<p align="center">_ _ _ _ _ _ _ _ _ _</p>

## Добавление элемента навигации модулю в первый блок меню.

В файл `📄 \custom\Extension\modules\{ module }\Ext\Menus\Menu.php` (a+)  добавить
код:
```php
$module_menu[]= array("index.php?module={ module }&action={ action }", $mod_strings['{ label }'], "{Icon slug }");
```

Именование происходит в файле: `📄 \modules\{ module }\language\ru_ru.lang.php`
```php
$mod_strings['{ label }'] = ' Рускоязычное название ссылки';
```

Далее необходимо применить "Быстрое восстановление".  
[Администрирование](https://in4sec.crm/index.php?module=Administration&action=index) > [Восстановление](https://in4sec.crm/index.php?module=Administration&action=Upgrade)
> [Быстрое восстановление](https://in4sec.crm/index.php?module=Administration&action=repair)


### На премере моудля News
`📄 \custom\Extension\modules\News\Ext\Menus\Menu.php`

```php
$module_menu[]= array("index.php?module=News&action=import", $mod_strings['LBL_IMPORT_ITEMS'], "Import");
```
`📄 \modules\News\language\ru_ru.lang.php`
```php
$mod_strings['LBL_IMPORT_ITEMS'] = 'Импорт';
```

__________

<p align="center">_ _ _ _ _ _ _ _ _ _</p>

## Редактирование данных модуля в блоке/панель

Происходит через конфигурационные файлы необходимой вьюхи в директории:  
`📁 \custom\modules\{ module }\metadata\`

Иснтрумент "Студия" при редактирование макетов и форм(просмотр/редактирование/...) во время сохранения вносит изменения в вышеупомянутые файлы вышеуказанной директории:  
`📄 \custom\modules\{ module }\metadata\{ file }.php`


#### на примере "Opportunities" (Сделки).
форма "просмотра", изменения вносятся в файл:  
`📄 \custom\modules\Opportunities\metadata\detailviewdefs.php`

* **!** Для применения изменений в CRM системе надо выполненить действие
> [Быстрое восстановление](https://in4sec.crm/index.php?module=Administration&action=repair)

Пример кода для блока `detailviewdefs`:
```php
$viewdefs ['module_id'] ['DetailView'] ['panels'] ['PANEL_ID'] = [
	[ //первая строка 
		array('name' => 'field_id_1', 'label' => 'LBL_FIELD_1'),
		array('name' => 'field_id_2', 'label' => 'LBL_FIELD_2'),
		array('name' => 'field_id_3', 'label' => 'LBL_FIELD_3'),
		// name - id поля таблицы из базы данных взаимодействующей с данным модулем
		// label - локализация. Названия полей. обращается к файлу ("\cache\modules\{ module }\language\ru_ru.lang.php") который формируется при "Быстрое восстановление" из файла
		"\custom\Extension\modules\{ module }\Ext\Language\ru_ru.fields_panel_{ PANEL_ID }.php" 
		//и очевидно из других файлов этого каталога
	],
	[ //вторая строка 
		array(
			'name' => 'field_id_4',
			'label' => 'LBL_FIELD_4',
			'customCode' => '{include file="custom/modules/{ module }/tpls/{ file_name }.tpl"
				var1="value2" var2="value2"
				amount_field="amount_field_id"}', 
				// пример переменная `amount_field` значение которой будет браться из amount_field_id 
		),
		array(
			'name' => 'field_id_5',
			'hideIf' => 'empty($fields.any_object.value)', // условие для скрытия ячейки
		),
		'', // пустая ячейка
	],
	[ //третья строка 
		array(
			'name' => 'field_id_6',
			'customCode' => '{$fields.some_object.value} {$APP.LBL_BY} {$fields.other_object.value}',
		),
	],	
]
```

__________

<p align="center">_ _ _ _ _ _ _ _ _ _</p>

## Валидация полей дял FrontEnd

Валидация задаётся в файле  
`📄 \custom\modules\{ module }\js\validates.js`

пример файла:
```javascript
var formname_opportunity = $('form[id^="form_SubpanelQuickCreate_"]').attr('name') || 'EditView';

SUGAR.util.doWhen('(typeof validate != "undefined") && (typeof validate["'+formname_opportunity+'"] != "undefined")', function(){

    // собственная валидация
    addToValidateCallback(formname_opportunity, 'field_id_1', 'alpha', false, 'Текст ошибки которы будет показан под полем ввода', validateCustomFunction);

    addToValidateCallback(formname_opportunity, 'field_id_3', 'required', false, 'Текст ошибки которы будет показан под полем ввода', validateRequreFunction);

    addToValidateDateBefore('EditView', 'field_id_3', 'date', '', 'Назваине поля ', 'field_id_1');
});

function validateRequreFunction(){}

function validateCustomFunction()
{
    var value_A = 1,
        value_B = 0;

    if ( value_A != value_B )
    {
        return false; // валидация не пройдена
    }

    return true; // валидация пройдена
}
```

Список всех функций для валидации находится в файле  
`📄 \jssource\src_files\include\javascript\sugar_3.js`  
имена функций начинаются на `addToValidate...`

__________

<p align="center">_ _ _ _ _ _ _ _ _ _</p>

## Редактирование CSS

Применяется тема '**Day**', стили которой находятся в файле  
`📄 \custom\themes\SuiteP\css\Day\style.css`

После внесения изменений в `css` файл необходимо удалить файл кэша:  
`📄 \cache\themes\SuiteP\css\Day\style.css`      
он сгенерируется самостоятельно при загрузке старницы.

__________

<p align="center">_ _ _ _ _ _ _ _ _ _</p>

### 📖 Материалы:
* 🎥 [Структура папок и файлов SuiteCRM](https://www.youtube.com/watch?v=u9dwMutp6Rg) (YouTube)
* 🎥 [ручное добавление новых полей в модуль](https://www.youtube.com/watch?v=pH-vl1rHQGY) (YouTube)
* 🎥 [Структура базы данных SuiteCRM](https://www.youtube.com/watch?v=vn0e1yrrvAU) (YouTube)
* 🎥 [Работа с базой данных (SQL-запросы) в SuiteCRM](https://www.youtube.com/watch?v=0IHHwb3O7DQ) (YouTube)
* 🎥 [Рабочее место программиста SuiteCRM](https://www.youtube.com/watch?v=lfRDaLFVnF0) (YouTube)
* 🎥 [Дашлеты в SugarCRM/SuiteCRM: снимаем ограничение на 6 колонок](https://www.youtube.com/watch?v=BXF5yfFFve8) (YouTube)
* 📝 ...

_________
