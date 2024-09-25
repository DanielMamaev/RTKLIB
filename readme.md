#
#  RTKLIB 2.4.3 b34
#

Это версия RTKLib для python библиотеки MonCenterLib [https://github.com/DanielMamaev/MonCenterLib](https://github.com/DanielMamaev/MonCenterLib)

#### Change list:
1. Модифицирован str2str. Добавлен флаг `-outstat` для вывода stderr в файл. Это нужно для отслеживания статуса подключения через python.
2. Добавлен в makefile str2str команды для сборки бинарника под Windows
3. 



#### How to build str2str on Windows

1. I downloaded and installed gcc-11.3.0-64.exe . From this site http://www.equation.com/servlet/equation.cmd?fa=fortran After installation, I checked that it works. `gcc --version`

2. After that, I made the following changes to the makefile. Path to makefile `RTKLIB_2.4.3_b34\app\consapp\str2str\gcc\makefile`.

```
CC = gcc

OPTION = -DENAGLO -DENAGAL -DENAQZS -DENACMP -DENAIRN -DTRACE -DNFREQ=5 -DNEXOBS=3 -DSVR_REUSEADDR -DWIN32

LDLIBS  = -lm -lpthread -lwinmm -lws2_32
```

3. Fix code in `str2str.c`
```
signal(SIGTERM,sigfunc);
signal(SIGINT ,sigfunc);
#ifdef __unix__
signal(SIGHUP ,SIG_IGN);
signal(SIGPIPE,SIG_IGN);
#endif
```
3. Make sure that there are no files in the gcc folder except the makefile.
4. Run `make`
