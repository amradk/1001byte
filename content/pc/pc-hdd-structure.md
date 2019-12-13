Title: Структура жесткого диска ПК 
Date: 12-06-2019 13:06
Category: PC
Tags: PC, MBR, HDD

# Введение 

Когда я только начинал изучать устройство ПК в моем распоряжении были только различные журналы (Домашний компьютер, Мир ПР, Upgrade, ][акер, Железо прочие) и книги, обычно уже устаревшие. Работа по сбору и упорядочиванию информации из большего количества различных источников часто приводила к появлению новых вопросов одним из которых был вопрос адрессации блоков информации на жестком диске ПК. В BIOSе своего ПК и в некотых программых для разметки я видел CHS-адрессацию в других программах использовалась LBA-адресация. Из литературы следовало что CHS это устаревший способ и будущее за LBA так почему же этот старой способ все еще присутствует в каждой второй утилите для работы с ЖД и разделами? И самое главное почему CHS так сложно устроен и как это возможно чтобы на диске было 255 головок? Ответ оказался очевиден - обратная совместимость, а подробности читайте ниже.  

# Адресация CHS.  

Cylinder-Head-Sector (CHS) или Цилиндр-Головка-Сектор - наиболее ранний способ адресации пространство на жестком диске. Жесткий диски, используемые в ПК, для хранения информации представляют собой набор пластин (дисков), выполненных из специального сплава с магнитными свойствами. Внутри корпуса жесткого диска расположено несколько таких пластин (обычно от 2-х до 4-х).  Поверхность пластин поделена на небольшие ячейки - сектора. Сектор является минимальной адресуемой ячейкой на жестком диске. Сектора расположены в виде концентрических окружностей - дорожек. Группа дорожек, расположенная на равном расстояние от центра, на всех сторонах всех дисков - цилиндр. Головка -  номер считывающей головки, над каждой стороной каждого диска расположена магнитная считывающая головка.  

Данный способ адресации был придуман в стародавние времена, когда жесткие диски не имели встроенных контроллеров, а управлением диском занималась отдельная специальная плата. Для того чтобы успешно справляться со своей работой плата должна была знать информацию о геометрии жесткого диска т.е. количество цилиндров, секторов и головок.  

Первые жесткие диски были небольшого объема (объем был невелик хотя количество головок, а соответственно и пластин могло быть намного больше, чем у современных жестких дисков) и содержали одинаковое количество секторов на всех дорожках.   

# Ограничения адресации CHS. 

Первая часть загрузочного процесса происходит на уровне BIOS, и подвергается ограничениям как BIOS'а так и аппаратным ограничениям физического интерфейса посредством которого жесткий диск подключался к материнской плате компьютера. Так, например, стандарт ATA (сейчас более известный как IDE) в своей первой редакции максимально поддерживал: 
    * 255 сектора на дорожку; 
    * 16 головок; 
    * 65536 цилиндров; 
    * 139.9 Гб дискового пространства. 

В тоже время BIOS, а точнее функция чтения данных с диска - INT 13h, имел другие ограничения: 
    * 63 сектора на дорожку; 
    * 255 головок; 
    * 1024 цилиндра; 
    * 8.4 Гб дискового пространства. 

Со временем как стандарт ATA, так и BIOS получили развитие, функция INT 13h получила улучшения и максимально доступный объем дискового пространства доступного для BIOS увеличился до 32-х Гб. Подобные ограничения привели к забавным цифрам в описании геометрии диска, например, никогда не выпускалось дисков с 128 пластинами (256 головок), но подобные координаты транслировались контроллером диска в действительные. 

# Адресация LBA. 

Для преодоления ограничений CHS был придуман дрогой способ адресации секторов жесткого дика - LBA (Logical block addressing). При данном способе все сектора жесткого диска получают сквозную адресацию начиная с нуля. Текущая версия стандарта резервирует 48 бит для номера сектора что позволяет адресовать 144 Пт.

# Источники

* http://www.infocellar.com/software/ 
* https://en.wikipedia.org/wiki/Parallel_ATA 
* https://www.thomas-krenn.com/en/wiki/CHS_and_LBA_Hard_Disk_Addresses 