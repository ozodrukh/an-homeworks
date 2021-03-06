# Домашнее задание к лекции 1.3 Типы данных в Java: примитивы

Пришла новая неделя и нам снова нужно запланировать задачи для нашей команды.
Для расчета времени работы каждого участника команды разработки нужна программа, которая сможет точно рассчитать нагрузку для каждого.

## Задача № 1

Наша программа должна принимать на вход название задачи и время, требуемое на ее выполнение (например, 1 день или 1 час), после ввода запросить название ещё одной задачи, до тех пор пока мы не введем `end`. 
После этого у пользователя программы запрашивается единица измерения: ч (часы), м (минуты), с (секунды) и результат возвращается в запрошенных единицах измерения.

### Процесс реализации

1. При запуске программы создать цикл, который будет запрашивать ввод данных пользователем (название задачи и количество времени необходимое для ее разрешения).
2. Добавить условие выхода из цикла:
   - Если пользователь ввел вместо названия задачи `end`, то завершаем цикл.
   ```
   //Создаем scanner - объектор, который будет считывать из стандартного потока ввода/вывода (console)
   Scanner scanner = new Scanner(System.in);
   String input = "";
   
   //Цикл будет работать пока пользователь не введет `end`
   while (!"end".equals(input)) {
       
       input = scanner.next();
       //TODO
   }
   ```
3. При запусуке программы запросите у пользователя ввод названия задачи. Пример: `Добавить в приложение валидацию дат`.
   Для вывода сообщения в console достаточно использовать:
   ```
   System.out.println("Введите название задачи (для завершения введите end)");
   ```
4. Сохраните введенное значение в переменную task типа String (`String task = scanner.next();`)
5. Запросите у пользователя ввод времени на выполнение задачи. Пример: `4 ч`
   ```
   System.out.println("Сколько времени потребуется на выполнение задачи?");
   ```
6. Сохраните введенные зачения в переменные `time` (тип int или long) и `unit` (тип Char или String).
   ```
   int time = scanner.nextInt();
   String unit = scanner.next();
   ```
7. Если значение `time > 0` нужно перевести время в секунды и сохранить:
   - Создать переменную `totalTime = 0` (тип long или int).
   - Создать условие: если `unit = ч`, умножить `time` на 3600 и прибавить к `totalTime`.
   - Если `unit = м`, умножить time на 60 и прибавить к `totalTime`.
   - Если `unit = с`, прибавить time к `totalTime`.
8. Не выходя из цикла запросите ввод у пользователя новый ввод названия задачи, время на выполнение и единицы измерения (вернуться на шаг 3).
9. Перезапишите в переменные `time` и `unit` только что введенные значения.
10. Проверте работу с вводом разных единиц измерения.
11. Если пользователь ввел `end` выходим цикла, проверяем значение переменной `totalTime` если значение больше нуля, запрашиваем единицу измерения для вывода на экран.
   ```
   System.out.println("В какой единице измерения вернуть значение (ч - часы, м - минуты, c - секунды)");
   ```
12. Если пользователь ввел `end` и `totalTime` меньше или равно нулю, выйти из цикла и завершить работу программы.
    Структура программы будет примерно такая:
    ```
    //Создаем scanner - объектор, который будет считывать из стандартного потока ввода/вывода (console)
    Scanner scanner = new Scanner(System.in);
    String input = "";
    int totalTime = 0;
    
    //Цикл будет работать пока пользователь не введет `end`
    while (!"end".equals(input)) {
        
        input = scanner.next();
        //TODO
        String task = input;
        int time = scanner.nextInt();
        String unit = scanner.next();
        ...
        //Переведем время в секунды
        switch (unit) {
          case "ч" : time = time * 3600;
            break;
          case "м" : time = time * 60;
            break;     
        }
        totalTime += time
    }
    
    //После ввода "end" проверяем если totalTime
    if (totalTime > 0) {
      
      System.out.println("В какой единице измерения вернуть значение (ч - часы, м - минуты, c - секунды)");
      String unit = scanner.next()
      
      //Переводим в необходимую единицу измерения
      switch (unit) {
        case "ч" : totalTime = totalTime / 3600;
          break;
        case "м" : totalTime = totalTime / 60;
          break;     
      }
      
      //Выводим результат
      System.out.println(totalTime + " " + unit);
    }
    ```

## Задача № 2

Программами пользуются не только опытные пользователи, но и новички, хотя это не важно, когда существует понятие "человеческий фактор" - любой человек может допустить ошибку, поэтому к нашему приложению **нужно добавить проверку пользовательского ввода.** 

Вы создаете план работы на неделю вперед и на каком-то этапе ввели неверные данные (например, дату не в том формате). Ваш менеджер задач должен корректно обработать эту ситуацию, не упасть, позволить исправить ошибку и продолжить работу.
Нужно написать функцию, принимающую от пользователя дату-время в принятом в России формате yyyy-MM-dd-hh-mm-ss (например, 2018-02-12-16-30-00). 

Если пользователь введет дату/время не в нужном формате, менеджер задач (наше приложение) должен бросить исключение (т.е. принудительно создать ошибку, например, throw new Exception(“error text”)) и (самое важное!) позволить пользователю исправить эту ошибку.

### Процесс реализации

1. Создаем функцию `isValidDateFormat`, принимающую на вход строку `inputDate` и возвращающую тип true или false (boolean).
   ```
   boolean isValidDateFormat(String inputDate) {
      //TODO
   }
   ```
2. В этой функции создаем: 
   - Создаем перменную типа строка, в которую запишем наш формат для валидации дат, например: `String dateFormat = "yyyy-MM-dd-hh-mm-ss"`.
   - Создаем новую переменную `dateFormatter` типа `DateTimeFormatter` (можно использовать устаревший вариант SimpleDateFormat), с форматом который создали выше.
   ```
   boolean isValidDateFormat(String inputDate) {
      String dateFormat = "yyyy-MM-dd-hh-mm-ss";
      DateTimeFormatter dateFormatter = DateTimeFormatter.ofPattern(dateFormat);
      //TODO
   }
   ```
3. Вызываем у `dateFormatter` метод `parse`, которому передаем данные полученные на входе `inputDate` и сохраняем в переменную `parsedDate` типа `TemporalAccessor`.
   ```
   TemporalAccessor parsedDate = dateTimeFormatter.parse(inputDate);
   ```
4. Проверяем, что результат выполнения метода выше вернул объект и возвращаем `true`, в противном случае этот метод выбросит Exception, который нам необходимо обработать в нашей программе.
   ```
   if (parsedDate != null) {
      return true;
   }
   ```
   
Теперь наша программа умеет проверять корретно ли пользователь ввел данные, теперь наша задача попросить ввести корректную дату, для этого:

1. В методе `main` запрашиваем пользователя ввести дату.
2. Считываем ее в переменную `String inputDate`.
   ```
   Scanner scanner = new Scanner(System.in);
   System.out.println("Введите дату")
   String inputDate = scanner.next();
   ```
3. Передаем эту переменную в метод (функцию) `isValidDateFormat`.
4. Оборачиваем ее в блок `try/catch`.
5. В блоке `catch` мы должны поймать (обработать) иcключение (exception) ошибки разбора введенных данных `DateTimeParseException`:
   - вызываем запрос пользовательского ввода.
   ```
   try {
       
       boolean result = isValidDateFormat(inputDate);
       System.out.println("Result =" + result);
       
   } catch (DateTimeParseException e) {
       //TODO
   }
   ```
6. Если разбор введенных данных прошел корректно и метод `isValidDateFormat` вернул `true`, вернуть на экран введенную дату и завершить работу программы.
       

## Задача № 3

Написать программу, которая будет складывать, вычитать, умножать или делить два числа. Числа и знак операции вводятся пользователем. После выполнения вычисления программа не должна завершаться, а должна запрашивать новые данные для вычислений. Завершение программы должно выполняться при вводе символа '0' в качестве знака операции.

### Процесс реализации

Для решения этой задачи нам нужно создать цикл, в котором мы будем запрашивать числа на вход и тип операции, для выхода из цикла нужно добавить проверку типа операции == 0, а после завершить программу.
1. Начнем с того, что запросим у пользователя числа, над которыми нужно провести операции и саму операцию:
   - считаем первую переменную и запишем ее в `value1`;
   - считаем вторую переменную и запишем ее в `value2`.
2. Попросим пользователя ввести тип операции и записываем значение в переменную `operation`:
   - проверяем если значение переменной = 0, выходим из цикла и завершаем работу программы;
   - добавляем блок `switch`, в котором в зависимости от значения переменной `operation` выполняем нужную арифметическую операцию и выводим результат вычисления на экран.
   
   ```
   Scanner scanner = new Scanner(System.in);
   String operation = "";
   double result = 0;
   
   while (true) {
       
       //Попросим пользователя ввести данные
       System.out.println("Введите два числа и тип операции (+,-,*,/)");
       
       //Считаем введеные значения и сохраним в переменные
       int value1 = scanner.nextInt();
       int value2 = scanner.nextInt();
       String operation = scanner.next();
       
       //Выходим из цикла если операция равно нулю
       if ("0".equals(operation)) {
          break;
       }
       
       //Расчет результата
       switch (operation) {
         case "+" : result = value1 + value2;
           break;
         case "-" : result = value1 - value2;
           break;
         //TODO  
       }
       System.out.println("Результат операции = " + result);
   }

   ```
3. Запрашиваем ввод новых чисел для вычисления.    

---

## Инструкция по выполнению домашнего задания:

1. Зарегистрируйтесь на сайте [Repl.IT](https://repl.it/).
2. Перейдите в раздел **my repls**.
3. Нажмите кнопку **Start coding now!**, если приступаете впервые, или **New Repl**, если у вас уже есть работы.
4. В списке языков выберите `Java`.
5. Код пишите в левой части окна.
6. Посмотреть результат выполнения файла можно, нажав на кнопку **Run**. Результат появится в правой части окна.
7. После окончания работы нажмите кнопку **Share** и скопируйте ссылку из поля _Share link_.
8. В личном кабинете на сайте [netology.ru](http://netology.ru/) в поле комментария к домашней работе вставьте скопированную ссылку и отправьте работу на проверку.

_Никаких файлов прикреплять не нужно._
