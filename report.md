# Отчёт о тестировании Credit Card Number Validator

## Краткое описание
02/04/2021 было проведено тестирование функциональности приложения Credit Card Number Validator.

На тестирование затрачено: 2 часа

В результате тестирования выявлены следующие дефекты:

**Карты с длинной номера меньше и больше чем 16 символов не работают** 
## Пример:
* Ошибка при валидации карт с номерами короче и длиннее 16 символов - [Ошибка при валидации карт с номерами короче и длиннее 16 символов](https://github.com/yannikkel/java-one/issues/1)



## Описание процесса тестирования

В процессе тестирования использовались следующие артефакты:

* Тестовый сценарий:

1. Взять код из [задачи](https://github.com/netology-code/javaqa-homeworks/tree/master/intro)
```java
public class Main {
  public static void main(String[] args) {
    // TODO: подставлять номер карты нужно сюда между двойными кавычками, без пробелов
    String number = "5351719427810741";
    System.out.println(String.format("Result is %s", isValidCardNumber(number) ? "OK" : "FAIL"));
  }

  public static boolean isValidCardNumber(String number) {
    if (number == null) {
      return false;
    }

    if (number.length() != 16) {
      return false;
    }

    long result = 0;
    for (int i = 0; i < number.length(); i++) {
      int digit;
      try {
        digit = Integer.parseInt(number.charAt(i) + "");
      } catch (NumberFormatException e) {
        return false;
      }

      if (i % 2 == 0) {
        digit *= 2;
        if (digit > 9) {
          digit -= 9;
        }
      }
      result += digit;
    }

    return (result != 0) && (result % 10 == 0);
  }
}
```
2. Произвести ввод данных карт с сайта [freeformatter](https://www.freeformatter.com/credit-card-number-generator-validator.html)
3. В четвертой строке "String number" в ковычках вставлять номера карт и запускать код сочетанием клавиш Shift+F10
4. Зафиксировать результат теста в репорте

В качестве тестовых данных использовались данные с сайта [freeformatter](https://www.freeformatter.com/credit-card-number-generator-validator.html#validate)

VISA
4716190824973750 - OK
4485162215983142982 - FAIL 

Discover 
6011571995278441 - OK
6011839645693134181 - FAIL 

Diners Club - Carte Blanche
30236366931644 - FAIL

Visa Electron
4844864378324041 - OK

Master Card
5484644555559698 - OK

JCB
3543692823284254 - OK

Diners Club - International
36551090799644 - FAIL

InstaPayment
6393194188834330 - OK

American Express AMEX
379100866248686 - FAIL

Diners Club - North America
5492223920327337 - OK

Maestro
6763170186299611 - OK

Тестирование производилось в следующем окружении:
* Windows 10 Pro x64
* Java "11.0.10" 2021-01-19
* IntelliJ IDEA Community Edition "2020.3.3"

