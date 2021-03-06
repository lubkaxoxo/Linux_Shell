## Cистемни примитиви на C за работа с процеси

* execl(3) `int execl(const char *path, const char *arg, ... /* (char  *) NULL */);`

* T1 - Да се напише програма на C, която изпълнява команда date.

* execlp(3) `int execlp(const char *file, const char *arg, ... /* (char  *) NULL */);`

* T2 - Да се напише програма на C, която изпълнява команда ls с точно един аргумент.
* T3 - Да се напише програма на C, която изпълнява команда sleep (за 60 секунди).

* fork(2) `pid_t fork(void);`
* T4 - Да се напише програма на C, която създава процес дете и демонстрира принцина на конкурентност при процесите.

* wait(2) `pid_t wait(int *wstatus);`
* T5 - Да се напише програма на C, която е аналогична на горния пример, но принуждава родителския процес да изчака детинския си процес да завърши изпълнение.

* getpid(2) `pid_t getpid(void);` `pid_t getppid(void);`

* Прегледайте прикачената програма на C във **fork-loop/main.c** и отговорете на следните въпроси:
1) В какъв ред ще се отпечатат символните низове на всеки от процесите? Пробвайте да изпълните програмата няколко пъти.
2) Какво ще се изпише на стандартния изход, ако само разкоментираме `exit(0);` в детинските процеси?
3) В какъв ред ще се отпечатат низовете, ако само разкоментираме `wait(NULL);`? Редът един и същ ли ще е винаги? Защо?
4) Какво ще се отпечата на стандартния изход, ако разкоментираме и `exit(0);`, и `wait(NULL);`?
5) Колко реда ще се отпечатат, ако `N = 3` при обстоятелствата от предния въпрос?
6) Колко реда ще се отпечатат, ако `N = 3`, но `exit(0);` е закоментиран? При тези обстоятелства, как нараства броят на отпечатаните редове при растене на `N`? (Съвет: НЕ пробвайте да изпълнявате програмата с "голямо" `N`)
7) Ще има ли **memory leak**, ако разменим реда на `free(indentation);` и разкоментирания `exit(0);`?
8) Ще има ли **memory leak**, ако махнем всичките 2 реда `free(indentation);` и оставим само един `free(indentation);` на последния ред във `for` цикъла? Ако да, при какви ситуации?

## Задачи за самостоятелна работа

6. Да се напише програма на С, която получава като параметър команда (без параметри) и при успешното ѝ изпълнение, извежда на стандартния изход името на командата.
7. Да се напише програма на С, която получава като параметри три команди (без параметри), изпълнява ги последователно, като изчаква края на всяка и извежда на стандартния изход номера на завършилия процес, както и неговия код на завършване.
8. Да се напише програма на С, която получава като параметър име на файл. Създава детински процес, който записва стринга `foobar` във файла (ако не съществува, го създава, в противен случай го занулява), след което процеса родител прочита записаното във файла съдържание и го извежда на стандартния изход, добавяйки по един интервал между всеки два символа.
9. Да се напише програма на C, която която създава файл в текущата директория и генерира два процесa, които записват низовете `foo` и `bar` в създадения файл.
	* Програмата не гарантира последователното записване на низове.
	* Променете програмата така, че да записва низовете последователно, като първия е `foo`.
10. Да се напише програма на C, която получава като параметри от команден ред две команди (без параметри). Изпълнява първата. Ако тя е завършила успешно изпълнява втората. Ако не, завършва с код -1.
11. Да се напише програма на C, която изпълнява последователно подадените ѝ като параметри команди, като реализира следната функционалност постъпково:
	* `main cmd1 ... cmdN` Изпълнява всяка от командите в отделен дъщерен процес.
	* ... при което се запазва броя на изпълнените команди, които са дали грешка и броя на завършилите успешно.
12. Да се напише програма на C, която получава като параметри от команден ред две команди (без параметри) и име на файл в текущата директория. Ако файлът не съществува, го създава. Програмата изпълнява командите последователно, по реда на подаването им. Ако първата команда завърши успешно, програмата добавя нейното име към съдържанието на файла, подаден като команден параметър. Ако командата завърши неуспешно, програмата уведомява потребителя чрез подходящо съобщение.
13. Да се напише програма на C, която получава като командни параметри две команди (без параметри). Изпълнява ги едновременно и извежда на стандартния изход номера на процеса на първата завършила успешно. Ако нито една не завърши успешно извежда -1.

## Системни примитиви на C за работа с pipe-ове

* `fork` -- the child inherits copies of the parent's set of open file descriptors
* T1 - Да се напише програма на C, която приема аргумент - име на файл. Програмата да:
	* записва във файла 'fo'
	* създава child процес, който записва 'bar\n'
	* parent-а, след като изчака child процеса, записва 'o\n'
* pipe(7)
* pipe(2) `int pipe(int pipefd[2]);`

* T2 - Напишете програма на C, която демонстрира комуникация през pipe между parent и child процеси. Parent-ът трябва да изпраща стринга, получен като първи аргумент на командния ред към child-а, който да го отпечатва на стандартния изход.

* mkfifo(3) `int mkfifo(const char * pathname, mode_t mode);`
* dup(2) `int dup(int oldfd);`
* dup2(2) `int dup2(int oldfd, int newfd);`

* T3 - Напишете програма на C, която демонстрира употребата на dup/dup2 между parent и child процеси. Parent-ът трябва да изпраща стринга, получен като първи аргумент на командния ред към child-а, където той да може да се чете от stdin. Child процесът да изпълнява`wc -c`.
