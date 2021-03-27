---
# Front matter
lang: ru-RU
title: "Шаблон отчёта по лабораторной работе"
subtitle: "Простейший вариант"
author: "Дмитрий Сергеевич Кулябов"

# Formatting
toc-title: "Содержание"
toc: true # Table of contents
toc_depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4paper
documentclass: scrreprt
polyglossia-lang: russian
polyglossia-otherlangs: english
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase
indent: true
pdf-engine: lualatex
header-includes:
  - \linepenalty=10 # the penalty added to the badness of each line within a paragraph (no associated penalty node) Increasing the value makes tex try to have fewer lines in the paragraph.
  - \interlinepenalty=0 # value of the penalty (node) added after each line of a paragraph.
  - \hyphenpenalty=50 # the penalty for line breaking at an automatically inserted hyphen
  - \exhyphenpenalty=50 # the penalty for line breaking at an explicit hyphen
  - \binoppenalty=700 # the penalty for breaking a line at a binary operator
  - \relpenalty=500 # the penalty for breaking a line at a relation
  - \clubpenalty=150 # extra penalty for breaking after first line of a paragraph
  - \widowpenalty=150 # extra penalty for breaking before last line of a paragraph
  - \displaywidowpenalty=50 # extra penalty for breaking before last line before a display math
  - \brokenpenalty=100 # extra penalty for page breaking after a hyphenated line
  - \predisplaypenalty=10000 # penalty for breaking before a display
  - \postdisplaypenalty=0 # penalty for breaking after a display
  - \floatingpenalty = 20000 # penalty for splitting an insertion (can only be split footnote in standard LaTeX)
  - \raggedbottom # or \flushbottom
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Организуется рекламная кампания нового товара или услуги. Необходимо,
чтобы прибыль будущих продаж с избытком покрывала издержки на рекламу.
Вначале расходы могут превышать прибыль, поскольку лишь малая часть
потенциальных покупателей будет информирована о новинке. Затем, при
увеличении числа продаж, возрастает и прибыль, и, наконец, наступит момент,
когда рынок насытиться, и рекламировать товар станет бесполезным.

# Задание

Постройте график распространения рекламы, математическая модель которой описывается
следующим уравнением:

1) $$\frac{dn}{dt}=(0.61+0.000061n(t))(N(t) - n(t))$$
1) $$\frac{dn}{dt}=(0.000061+0.61n(t))(N(t) - n(t))$$
1) $$\frac{dn}{dt}=(0.61sin(t)+0.61cos(t)n(t))(N(t) - n(t))$$

При этом объем аудитории $N=537$, в начальный момент о товаре знает 6 человек. Для
случая 2 определите в какой момент времени скорость распространения рекламы будет
иметь максимальное значение.


# Выполнение лабораторной работы

Построение графика для $\frac{dn}{dt}=(0.61+0.000061n(t))(N(t) - n(t))$

```scilab
t0 = 0; //начальный момент времени
x0 = 1; // количество людей, знающих о товаре в начальный момент времени
N = 537; // максимальное количество людей, которых может заинтересовать товар
t = 0: 0.1: 30; // временной промежуток (длительность рекламной компании)

//функция, отвечающая за платную рекламу
function g=k(t);
  g = 0.61;
endfunction

//функция, описывающая сарафанное радио
function v=p(t);
  v = 0.000061;
endfunction

//уравнение, описывающее распространение рекламы
function xd=f(t, x);
  xd = ( k(t) + p(t)*x )*( N - x );
endfunction
x = ode(x0, t0, t, f); //решение ОДУ
plot(t, x); //построение графика решения
```

![График распространения информации о товаре с учетом платной
рекламы и с учетом сарафанного радио. Коэффициент $\alpha 1 = 0.61$, коэффициент
$\alpha 2 = 0.000061$.](image/publicity-case-1.png){ #fig:001 width=70% }


Построение графика для $\frac{dn}{dt}=(0.000061+0.61n(t))(N(t) - n(t))$

```scilab
t0 = 0; //начальный момент времени
x0 = 1; // количество людей, знающих о товаре в начальный момент времени
N = 537; // максимальное количество людей, которых может заинтересовать товар
t = 0: 0.1: 30; // временной промежуток (длительность рекламной компании)

//функция, отвечающая за платную рекламу
function g=k(t);
    g = 0.000061;
endfunction

//функция, описывающая сарафанное радио
function v=p(t);
    v = 0.61;
endfunction

//уравнение, описывающее распространение рекламы
function xd=f(t, x);
    xd = ( k(t) + p(t)*x )*( N - x );
endfunction

x = ode(x0, t0, t, f); //решение ОДУ
plot(t, x); //построение графика решения
```
![График распространения информации о товаре с учетом платной
рекламы и с учетом сарафанного радио. Коэффициент $\alpha 1 = 0.000061$, коэффициент
$\alpha 2 = 0.61$.](image/publicity-case-2.png){ #fig:001 width=70% }

После получения значений x и t печатаем значение момента времени t первого максимума:

```scilab
indices = find(x==max(x));
disp(t(indices(1)));
```
Максимальное значение появляется в момент $0.1$

Построение графика для $\frac{dn}{dt}=(0.61sin(t)+0.61cos(t)n(t))(N(t) - n(t))$

```scilab
t0 = 0; //начальный момент времени
x0 = 1; // количество людей, знающих о товаре в начальный момент времени
N = 537; // максимальное количество людей, которых может заинтересовать товар
t = 0: 0.001: 0.5; // временной промежуток (длительность рекламной компании)

//функция, отвечающая за платную рекламу
function g=k(t);
    g = 0.000061*sin(t);
endfunction

//функция, описывающая сарафанное радио
function v=p(t);
    v = 0.61*cos(t);
endfunction

//уравнение, описывающее распространение рекламы
function xd=f(t, x);
    xd = (k(t) + p(t)*x)*(N - x);
endfunction

x = ode(x0, t0, t, f); //решение ОДУ

plot(t, x); //построение графика решения
```
![График распространения информации о товаре с учетом платной
рекламы и с учетом сарафанного радио. Коэффициент $\alpha 1 = 0.000061*sin(t)$, коэффициент
$\alpha 2 = 0.61*cos(t)$.](image/publicity-case-3.png){ #fig:001 width=70% }

# Выводы

Рассмотрели простейшую модель эпидемии. Все щаги били успещно выполнёны.
