# Введение

X-Box original является, возможно, самой интересной и необычной консолью в своем поколении. А самое интересное в что необычность X-Box’а заключается в его обычности! Под капотом X-Box почти обычный ПК! Добавляет сходства и наличие жесткого диска (ни PS 2, ни GameCube не имели жесткого диска), а в качестве привода служит обычный IDE DVD-ROM.   

# Технические характеристики

Если взглянуть на аппаратную составляющую консоли от  Microsoft то окажется что в качестве CPU трудиться процессор архитектуры x86 производства компании Intel очень похожий на обычный Intel Pentium III для домашних ПК, работающий на частоте 733 Мгц. В качестве видеопроцессора используется чип производства компании NVidia, что-то среднее между GeForce 2 и 3. На плате распаяно 64 Мб оперативной памяти. Звучит почти как технические характеристики домашнего ПК. И это в то время когда архитектура консолей других производителей сильно отличается от x86 (цп архитектуры MIPS и прочее). Еще одним отличием является тот факт что X-Box original поставлялся с установленным обычным IDE HDD объемом 10 Гб, увы устанавливать игры было нельзя, диск используется как хранилище сохранений, кэширования различный данных игр, а также содержит системное ПО - dasboard и музыкальный проигрыватель. В качестве DVD-привода использовался IDE DVD-привод, который в случае поломки просто меняли на другой хоть от домашнего ПК. Даже порты для подключения геймпадов на самом деле являются обычными USB 1.1.

# ОС и процесс загрузки

Сначала Microsoft хотела использовать Windows как операционную систему для X-Box но очень быстро стало понятно что Windows не подходит и для чтобы обеспечить максимально быстрый старт (оригинальный X-Box и по сегодняшним меркам стартует очень быстро) и запуск игр нужно разрабатывать отдельное решение. Таким решением стало сильно модифицированное и урезанное ядро Windows 2000. Ядро XboxOS занимает в сжатом виде ~256 Кб, в несжатом ~500 Кб. Так, например,  XboxOS не поддерживает динамическую линковку, отсутствуют различные уровни привилегий, остался только уровень ядра, наверно это было сделано для того чтобы предоставить играм доступ к оборудованию. На диске располагаются dasboard, проигрыватель, шрифты и другое прикладное ПО. Судя по всему прикладное ПО и явилось причиной добавления ЖД кв конфигурацию X-Box, дело в том что dasboard довольно крупное крупное ПО (~100 Мб ). В качестве файловой системы  используется FATX основанная на FAT32. Хотя FATX и FAT32 принадлежать к одному семейству ФС они не совместимы и компьютеры того времени, работающие под управлением различных версий Windows файловую систему X-Box’а не понимали, а энтузиасты и хакеры использовали для доступа к ФС Linux для которого необходимый драйвер вскоре появился. На диске нет библиотек DirectX и каких либо других вспомогательных библиотек, игры статически линковались со всеми необходимыми им библиотеками. Разделы на жестком диске:
С: - системный раздел, содержит dashboard
D: - DVD-ROM
E: - системный раздел, на нем хранятся сохранения игр, музыка закаченная на X-Box
F, G - не родные разделы, обычно создаются при замене ЖД на более емкий
X: Y: Z: - Это разделы кеша, там хранятся временные файлы от игры, в которая в данным момент запущена. Без них Xbox работать не будет.
Если по аппаратному обеспечению X-Box сильно похож на обычный ПК то процесс загрузки - то место где X-Box очень сильно отличается от ПК. Процесс загрузки X-Box состоит из нескольких стадий:
Загрузчик из Secret ROM, выполняет инициализацию оборудования, проверяет целостность FLASH RAM, извлекает из  FLASH RAM вторичный загрузчик и передает ему управление
Вторичный загрузчик выполняет расшифровку ядра, копирует код ядра в память и передает управление ядру
Ядро XboxOS проверяет наличие диска с игрой в приводе, если диск найден то запускает игру, если нет то запускает dasboard  с ЖД  
Таким образом на довольно раннем этапе мы получаем загруженное в память ядро XBoxOS. Ядро исполняет только подписанный код. Эта особенность работы X-Box препятствовала возможности запуска других ОС, ведь ключа для подписи исполняемых файлов у Linux-энтузиастов не было.
	
# Homebrew

Силами энтузиастов методом обратной разработки был создан OpenXDK - свободный SDK для разработки программ для X-Box. Не зная с помощью ли OpenXDK или с помощью оригинального XboxSDK для X-Box было разработано несколько альтернативных dashboard’ов. Альтернативные оболочки предоставляли намного более обширный функционал чем оригинальная оболочка от Microsoft, так, например, используя альтернативную оболочку можно было устанавливать игры с дисков на HDD, устанавливать дополнительное ПО, такое как эмуляторы консолей, получать доступ к содержимому диска по протоколу FTP и многое другое. Также альтернативные оболочки предоставляли больше информации о системе, позволяли менять регион консоли и др. Силами энтузиастов для X-Box был разработан весьма неплохой медиацентр - XBMC, портированы некоторые игры, например, DOOM.  

# Запуск Linux

Из-за особенностей процесса загрузки X-Box у Linux энтузиастов было два способа запустить Linux:
Перезаписать или обойти FLASH-память так чтобы первичный загрузчик никогда не загружал 2bl и ядро XboxOS
Использовать специальный modchip, который содержит несколько версий BIOS и позволяет переключаться между ними
Заставить ядро XboxOS выполнять неподписанный код, написать спицеальную программы которая пудет производить запуск Linux уже из-под запущенной XboxOS
Недостатком первого способа является невозможность дальнейшего использования X-Box original в качестве игровой приставки, что на мой взгляд делает этот менее полезным с практической точки зрения, для реализации этого метода была разработана специальная версия прошивки для X-Box, которая позволяла выполнить загрузку Linux с HDD, называется прошивка Cromwell. Второй способ используя softmod, позволяет выполнить установку дистрибутива Linux в существующий раздел HDD (обычно F:). Для реализации используется специальная версия Cromwell в виде исполняемого файла  XBE и называется xromwell. Такой способ оставляет возможность запуска оригинальной XboxOS и для меня это наиболее интересный с технической точки зрения метод.
Существует несколько способов обойти эту проблему. Первый способ - переписать содержимое FLASH памяти, убрать оттуда ядро XboxOS, а вместо него записать какой-нибудь загрузчик способный прочитать с диска ядро Linux и выполнить загрузку. Недостатком данного способа является невозможность дальнейшего использования X-Box original в качестве игровой приставки, поэтому мне этот метод не интересен. Еще один метод заключался в установке дополнительного чипа, который позволял осуществлять загрузку как оригинальной XboxOS так и других OS. Этот способ мне не доступен, остался последний. Последний способ требует чтобы X-Box был разблокирован методом softmod (впрочем первый способ тоже требует modchip или softmod) и позволяет выполнить установку дистрибутива Linux в существующий раздел HDD (обычно F:). Такой способ оставляет возможность запуска оригинальной XboxOS и для меня это наиболее интересный с технической точки зрения метод.
Зачем нужен softmod? Изначально X-Box запрещает выполнение кода не подписанного ключом от Microsoft. Адаптированные для консоли дистрибутивы Linux не имеют в своем составе подписанного кода, поэтому для запуска Linux и других сторонних приложений необходимо обойти проверку подписи кода что и делает softmod. Так же softmod позволяет устанавливать на X-Box сторонние DashBoard’s, и другое ПО, например, эмуляторы других приставок. Принцип работы Softmod’а опирается на ошибки в стандартном MS Dashboard и других компонентов системы и тот факт что весь исполняемый XboxOS код работает в привилегированном режиме т.е. Используя уязвимости в ПО XboxOS можно получить неограниченный доступ к системе и выполнить перепрошивку FLASH памяти, заменить MS Dashboard и сделать все что душе угодно. 
С момента выхода Xbox многие энтузиасты стали искать способ использовать консоль в качестве обычного ПК, ведь приобретая Xbox владелец по сути получал, за сравнительно небольшие деньги. довольно неплохой ПК. который он может использовать только как игровую консоль, потому что компания Microsoft не хотела чтобы кто-нибудь устанавливал другие ОС на их детище. Напомню что PlayStation 2 наблюдалась другая ситуация - Sony не запрещала запускать Linux на свой консоли. После продолжительной и упорной работы был X-Box был взломан и Linux-энтузиасты получили возможность запуска неподписанного кода. Вскоре был разработан драйвер для FATX, и создано несколько Linux -дистрибутивов которые могли запускаться и работать на железе X-Box. Был даже разработан специальный вариант прошивки FLASH памяти предназначенный для того чтобы избавиться от ядра XboxOS  и другого кода Microsoft. Называется эта прошивка - Cromwell и она позволяет превратить X-Box из игровой консоли в Linux- машину. Еще один вариант позволяет установить Linux в папку на разделе диска X-Box (обычно E:) и далее с помощью специально написанной программы, которая используя вызовы ядра XboxOS загружает в память ядро Linux, образ initrd и передает управление ядру. 