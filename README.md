# JavaScript Best Practice Guide.
### 1. Избегайте смешивания с другими технологиями.
JavaScript хорош для вычислений, преобразования, доступа к внешним источникам и для определения поведения интерфейса (обработки событий). Все остальное следует оставить в технологиях, которые у нас есть для этой работы (например, css).

Плохо:
```
var f = document.getElementById('mainform');
var inputs = f.getElementsByTagName('input');
for(var i=0,j=inputs.length;i<j;i++){
   if(inputs[i].className === 'mandatory' && inputs.value === ''){
      inputs[i].style.borderColor = '#f00';
      inputs[i].style.borderStyle = 'solid';
      inputs[i].style.borderWidth = '1px';
   }
}
```
Хорошо:
```
var f = document.getElementById('mainform');
var inputs = f.getElementsByTagName('input');
for(var i=0,j=inputs.length;i<j;i++){
   if(inputs[i].className === 'mandatory' && inputs.value === ''){
      inputs[i].className+=' error';
   }
}
```
Важно:
не нужно изменять ваш код JavaScript, чтобы изменить внешний вид. Используя CSS, вы можете избежать перебора большого количества элементов.
### 2. Используйте сокращенные обозначения.
Обозначения сокращений делают ваш код быстрым и легким для чтения, когда вы к нему привыкнете.

Плохо:
```
var lunch = new Array();
lunch[0]='Dosa';
lunch[1]='Roti';
lunch[2]='Rice';
lunch[3]='what the heck is this?';
```
Хорошо:
```
var lunch = [
   'Dosa',
   'Roti',
   'Rice',
   'what the heck is this?'
];
```
### 3. Объявления сверху.
Хорошая практика программирования - помещать все объявления вверху каждого скрипта или функции.

Преимущества:

+ Более чистый код
+ Обеспечивается единое место для поиска локальных переменных
+ Упрощается избежание нежелательных (подразумеваемых) глобальных переменных
+ Уменьшается вероятность нежелательных повторных деклараций
Например:
```
var firstName, lastName, price, discount, fullPrice;

firstName = "John";
lastName = "Doe";

price = 19.90;
discount = 0.10;

fullPrice = price - discount;
```
Это также касается переменных цикла:
```
var i;

for (i = 0; i < 5; i++) {
//
}
```
### 4. Инициализирование переменных.
Инициализация переменных при их объявлении является хорошей практикой кодирования.

Преимущества:

+ Дайте более чистый код
+ Обеспечьте единое место для инициализации переменных
+ Избегайте неопределенных значений

Пример:
```
var firstName = "",
lastName = "",
price = 0,
discount = 0,
fullPrice = 0,
myArray = [],
myObject = {};
```
Инициализация переменных дает представление о предполагаемом использовании (и предполагаемом типе данных).
### 5. Объявление.
+ Используйте `{}` вместо `new Object()`
+ Используйте `""` вместо `new String()`
+ Используйте `0` вместо `new Number()`
+ Используйте `false` вместо `new Boolean()`
+ Используйте `[]` вместо `new Array()`
+ Используйте `/()/` вместо `new RegExp()`
+ Используйте function `(){}` вместо `new Function()`

Пример:
```
var x1 = {};           // new object
var x2 = "";           // new primitive string
var x3 = 0;            // new primitive number
var x4 = false;        // new primitive boolean
var x5 = [];           // new array object
var x6 = /()/;         // new regexp object
var x7 = function(){}; // new function object
```
### 6. Завершите switch настройками по умолчанию.
Всегда заканчивайте свои `switch` расширением `default`. Даже если вы думаете, что в этом нет необходимости.

Пример:
```
switch (new Date().getDay()) {
  case 0:
    day = "Sunday";
    break;
  case 1:
    day = "Monday";
    break;
  case 2:
    day = "Tuesday";
    break;
  case 3:
    day = "Wednesday";
    break;
  case 4:
    day = "Thursday";
    break;
  case 5:
    day = "Friday";
    break;
  case 6:
    day = "Saturday";
    break;
  default:
    day = "Unknown";
}
```
### 7. Снижение активности в циклах.
Циклы часто используются в программировании.

Каждый оператор в цикле, включая оператор `for`, выполняется для каждой итерации цикла.

Операторы или присваивания, которые могут быть размещены вне цикла, заставят цикл работать быстрее.

Плохо:
```
var i;
for (i = 0; i < arr.length; i++) {
//
}
```
Хорошо:
```
var i;
var l = arr.length;
for (i = 0; i < l; i++) {
//
}
```
Плохой код обращается к свойству `length` массива каждый раз, когда цикл повторяется.
Хороший код получает доступ к свойству длины вне цикла и ускоряет выполнение цикла.

### 8. Доступ к DOM.
Доступ к HTML DOM происходит очень медленно по сравнению с другими операторами JavaScript.

Если вы ожидаете получить доступ к элементу DOM несколько раз, получите доступ к нему один раз и используйте его как локальную переменную.
Пример:
```
var obj;
obj = document.getElementById("demo");
obj.innerHTML = "Hello";
```
### 9. Избегайте ненужных переменных.
Не создавайте новые переменные, если не планируете сохранять значения.

Плохо:
```
var fullName = firstName + " " + lastName;
document.getElementById("demo").innerHTML = fullName;
```
Хорошо:
```
document.getElementById("demo").innerHTML = firstName + " " + lastName;
```
### 10. Используйте === вместо ==
В JavaScript используются два вида операторов равенства: `=== | !==` и `== | !=` . Рекомендуется всегда использовать первый набор при сравнении, так как это предотвращает ошибки приведения типов.
> «Если двое операндов имеют один и тот же тип и значение, то в результате использования === получаем true, а в результате использования !== – false.» – «JavaScript: The Good Parts» (* JavaScript. Сильные стороны).

Однако при работе с == и != у вас могут возникнуть ошибки (* приведения типов), если значения имеют различный тип данных. В этих случаях они попробуют преобразовать тип значений, что часто приводит к ошибкам.