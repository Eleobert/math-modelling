---
## Front matter
lang: ru-RU
title: Structural approach to the deep learning method
author: |
	Leonid A. Sevastianov\inst{1,3}
	\and
	Anton L. Sevastianov\inst{1}
	\and
	Edik A. Ayrjan\inst{2}
	\and
	Anna V. Korolkova\inst{1}
	\and
	Dmitry S. Kulyabov\inst{1,2}
	\and
	Imrikh Pokorny\inst{4}
institute: |
	\inst{1}RUDN University, Moscow, Russian Federation
	\and
	\inst{2}LIT JINR, Dubna, Russian Federation
	\and
	\inst{3}BLTP JINR, Dubna, Russian Federation
	\and
	\inst{4}Technical University of Košice, Košice, Slovakia
date: NEC--2019, 30 September -- 4 October, 2019 Budva, Montenegro

## Formatting
toc: false
slide_level: 2
theme: metropolis
header-includes: 
 - '\metroset{progressbar=frametitle,sectionpage=progressbar,numbering=fraction}'
 - '\makeatletter'
 - '\beamer@ignorenonframefalse'
 - '\makeatother'
aspectratio: 43
section-titles: true
---

# Цель работы

Движение грузика на пружинке, маятника, заряда в электрическом контуре, а
также эволюция во времени многих систем в физике, химии, биологии и других
науках при определенных предположениях можно описать одним и тем же
дифференциальным уравнением, которое в теории колебаний выступает в качестве
основной модели. Эта модель называется линейным гармоническим осциллятором.

# Задание

Постройте фазовый портрет гармонического осциллятора и решение уравнения
гармонического осциллятора для следующих случаев
1. Колебания гармонического осциллятора без затуханий и без действий внешней
силы $\ddot{x}+1.7x=0$
2. Колебания гармонического осциллятора c затуханием и без действий внешней
силы $\ddot{x}+9.8\dot{x}+x=0$
3. Колебания гармонического осциллятора c затуханием и под действием внешней
силы  $\ddot{x}+3.9\dot{x}+2.9x=0.9sin(2t)$

На интервале t $\in [0; 29]$ (шаг 0.05) с начальными условиями $x_0=0, y_0=-1.4$

# Выполнение лабораторной работы

Построение динамики изменения числа людей из каждой группы для случая $I(0) \leqslant I^*$ . Код в среде Scilab:

```scilab
w = sqrt(1.7);
g = 0.00;

//Правая часть уравнения f(t)
function f=f(t)
    f = sin(0.0.* t);
endfunction

function dx=y(t, x)
    dx(1) = x(2);
    dx(2) = -w.* w.* x(1) - g.* x(2) - f(t);
endfunction

//Точка, в которой заданы
//начальные условия
t0 = 0;

x0 = [-1; 1];

t = [0: 0.05: 50];

x = ode(x0, t0, t, y);
//Количество столбцов в матрице
n = size(x, "c");
//Переписываем отдельно
//x в y1, x' в y2

for i = 1: n
    y1(i) = x(1, i);
    y2(i) = x(2, i);
end
//Рисуем фазовый портрет: зависимость x(x')
plot(y1, y2);
xgrid();
```

![Фазовый портрет гармонического осциллятора без затуханий, без
действия внешней силы, с собственной частотой колебания $w=1.304$ по
горизонтальной оси значения x, по вертикальной оси значения
$\dot{x}$ (скорость).](../report/image/vibration-case-1.png){ #fig:001 width=70% }


```scilab
w = sqrt(8.7);
g = 8.7;

//Правая часть уравнения f(t)
function f=f(t)
    f = sin(0.0.* t);
endfunction

function dx=y(t, x)
    dx(1) = x(2);
    dx(2) = -w.* w.* x(1) - g.* x(2) - f(t);
endfunction

//Точка, в которой заданы
//начальные условия
t0 = 0;

x0 = [-1; 1];

t = [0: 0.05: 50];

x = ode(x0, t0, t, y);
//Количество столбцов в матрице
n = size(x, "c");
//Переписываем отдельно
//x в y1, x' в y2

for i = 1: n
    y1(i) = x(1, i);
    y2(i) = x(2, i);
end
//Рисуем фазовый портрет: зависимость x(x')
plot(y1, y2);
xgrid();
```

![Фазовый портрет гармонического осциллятора без затуханий, без
действия внешней силы, с собственной частотой колебания $w=2.95$ по
горизонтальной оси значения $x$, по вертикальной оси значения
$\dot{x}$ (скорость).](../report/image/vibration-case-2.png){ #fig:001 width=70% }

```scilab
w = sqrt(2.9);
g = 3.9;

//Правая часть уравнения f(t)
function f=f(t)
    f = sin(0.0.* t);
endfunction

function dx=y(t, x)
    dx(1) = x(2);
    dx(2) = -w.* w.* x(1) - g.* x(2) - f(t);
endfunction

//Точка, в которой заданы
//начальные условия
t0 = 0;

x0 = [-1; 1];

t = [0: 0.05: 50];

x = ode(x0, t0, t, y);
//Количество столбцов в матрице
n = size(x, "c");
//Переписываем отдельно
//x в y1, x' в y2

for i = 1: n
    y1(i) = x(1, i);
    y2(i) = x(2, i);
end
//Рисуем фазовый портрет: зависимость x(x')
plot(y1, y2);
xgrid();
```

![Фазовый портрет гармонического осциллятора без затуханий, без
действия внешней силы, с собственной частотой колебания $w=1.07$ по
горизонтальной оси значения $x$, по вертикальной оси значения
$\dot{x}$ (скорость).](../report/image/vibration-case-3.png){ #fig:001 width=70% }

# Выводы

Рассмотрели простейшую модель движения грузика на пружинке. Все щаги били успещно выполнёны.

## {.standout}

