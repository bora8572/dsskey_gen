# dsskey_gen
Создание конфигов DSS клавиш для телефона Fanvil X210 и АТС SI3000.

Если телефонов много, то создание и загрузка конфигов не отнимает много времени, так как настройки у большинства пользователей одинаковые. Но клавиши быстрого набора обычно у всех разные. К тому же номера могут быть как внутри, так и вне данной АТС - это нужно учитывать для настройки функции BLF (отслеживание состояния номера). Для того, чтобы не кликать в веб-интерфейсе фамилии с номерами, предлагаю макросы на VBA для генерации конфигов телефона и АТС.
Пользователю достаточно заполнить файл `template.xlsx` в таком виде:

<img width="507" alt="dsskeys" src="https://github.com/bora8572/dsskey_gen/assets/127035342/47b11a36-598f-42ad-acb6-a643670e7984">

Далее этот файл загружается в файл с макросами `dsskey_gen.xlsm`, где происходит вся магия.

<img width="734" alt="dsskeys_gen" src="https://github.com/bora8572/dsskey_gen/assets/127035342/531b164c-9703-4b73-b336-b2cde4b00851">

С помощью кнопки `Загрузить конфиг` загружаем заполненный пользователем файл.

Кнопка `Исправить номера` нужна для исправления формата номера. Дело в том, что у меня используется 4-х и 8-значный формат номера, поэтому по определённым условиям я привожу 8 знаков к 4 знакам. Также по нажатию этой кнопки удаляются разделители в виде пробелов, дефисов, точек и скобок.

Кнопка `Сформировать файлы` создаёт два файла `xxxx_blf.txt` и `xxxx_config.txt`, где xxxx - номер телефона пользователя. При формировании конфигов используется файл `subs_dn_sn_conv.dat` из экспорта конфигурации SI3000. В нём содержатся локальные номера АТС, то есть те, состояние которых мы можем отслеживать с телефона. Если у вас нет этого файла, то создайте в рабочей папке файл `subs_dn_sn_conv.dat` с содержимым:
'0','0','0','0'

Кнопка `Очистить поля` очищает поля.

Далее загружаете `xxxx_config.txt` в веб-интерфейс телефона, а `xxxx_blf.txt` в менеджмент SI3000: Supplementary Service > Subscriber Line Status Display.
