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

Рассмотрим простейшую модель эпидемии. Предположим, что некая
популяция, состоящая из $N$ особей, (считаем, что популяция изолирована)
подразделяется на три группы. Первая группа - это восприимчивые к болезни, но
пока здоровые особи, обозначим их через $S(t)$. Вторая группа – это число
инфицированных особей, которые также при этом являются распространителями
инфекции, обозначим их $I(t)$. А третья группа, обозначающаяся через $R(t)$ – это
здоровые особи с иммунитетом к болезни. 

# Задание

На одном острове вспыхнула эпидемия. Известно, что из всех проживающих на острове ($N=12 100$) в момент начала эпидемии ($t=0$) число заболевших людей
(являющихся распространителями инфекции) $I(0)=120$, А число здоровых людей с
иммунитетом к болезни $R(0)=52$. Таким образом, число людей восприимчивых к
болезни, но пока здоровых, в начальный момент времени $S(0)=N-I(0)- R(0)$.
Постройте графики изменения числа особей в каждой из трех групп.
Рассмотрите, как будет протекать эпидемия в случае:

1) если $I(0) \leqslant I^*$
2) если $I(0) > I^*$


# Выполнение лабораторной работы

Построение динамики изменения числа людей из каждой группы для случая $I(0) \leqslant I^*$ . Код в среде Scilab:

```scilab
a = 0.01;// коэффициент заболеваемости
b = 0.02;//коэффициент выздоровления
N = 12100;// общая численность популяции

I0 = 120; // количество инфицированных особей в начальный момент времени
R0 = 52; // количество здоровых особей с иммунитетом в начальный момент времени
S0 = N - I0 - R0; // количество восприимчивых к болезни особей в начальный момент времени

// случай, когда I(0)<=I*

function dx=syst(t, x)
    dx(1) = 0;
    dx(2) = - b*x(2);
    dx(3) = b*x(2);
endfunction

t0 = 0;
x0=[S0;I0;R0]; //начальные значения
t = [0: 0.01: 200];
y = ode(x0, t0, t, syst);
plot(t, y); //построение динамики изменения числа особей в каждой из трех групп
hl=legend(['S(t)';'I(t)';'R(t)']);
```

![Динамика изменения числа людей в каждой из трех групп в случае, когда $I(0) \leqslant I^*$, с начальными условиями $I(0)=120$, $R(0)=52$, $S(0)=11928$.
Коэффициенты $\alpha=0.01$, $\beta=0.02$.](image/infection-graph-below-critical.png){ #fig:001 width=70% }

Для случая $I(0)> I^*$ изменяем систему дифференциальных уравнений:
```
function dx=syst(t, x)
    dx(1) = -a*x(1);
    dx(2) =  a*x(1) - b*x(2);
    dx(3) =  b*x(2);
endfunction

```
![Динамика изменения числа людей в каждой из трех групп в случае, когда $I(0) > I^*$, с начальными условиями $I(0)=120$, $R(0)=52$, $S(0)=11928$.
Коэффициенты $\alpha=0.01$, $\beta=0.02$.](image/infection-graph-above-critical.png){ #fig:001 width=70% }
# Выводы

Рассмотрели простейшую модель эпидемии. Все щаги били успещно выполнёны.
