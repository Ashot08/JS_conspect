# Event Loop

## Движок JavaScript (JS engine, ранее - JS interpreter)
Например, V8 (Google Chrome, Chromium, NodeJS), Spider_Monkey (Firefox)

__Движок предоставляет:__
- кучу (heap) - область памяти для хранения объектов, массивов, переменных, функций итп,
- стек вызовов (call stack),
- компиляцию JS в машинный код

Event Loop __не является частью движка__

Event Loop - это отдельный механизм для реализации неблокирующей модели ввода/вывода. 

## Стек вызовов (call stack)

Стек вызовов хранит в себе перечень ещё не вызванных функций, в том порядке, в каком они будут вызваны (синхронно - шаг за шагом). 
Если стек не пустой, то функции из него вызываются поочередно по принципу LIFO (last in first out).
```
function first () {
    second();
    console.log('1');
}

function second() {
    third();
    console.log('2');
}

function third() {
    console.log('3');
}

first();
```
В стеке вызовов будут эти функции разместятся в следующем порядке:
```
third()
second()
first()
```
При запуске кода
```
    // в консоли мы увидим:
    3
    2
    1
```
Таким образом, функции из стека вызовов выполняются синхронно, одна за одной. 
Если какая-то из функций будет выполняться очень долго, то интерфейс браузера будет полностью заблокирован
до тех пор, пока функция не завершит выполнение.