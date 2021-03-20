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
Коэффициенты $\alpha=0.01$, $\beta=0.02$.](../report/image/infection-graph-below-critical.png){ #fig:001 width=70% }

Для случая $I(0)> I^*$ изменяем систему дифференциальных уравнений:
```
function dx=syst(t, x)
    dx(1) = -a*x(1);
    dx(2) =  a*x(1) - b*x(2);
    dx(3) =  b*x(2);
endfunction

```
![Динамика изменения числа людей в каждой из трех групп в случае, когда $I(0) > I^*$, с начальными условиями $I(0)=120$, $R(0)=52$, $S(0)=11928$.
Коэффициенты $\alpha=0.01$, $\beta=0.02$.](../report/image/infection-graph-above-critical.png){ #fig:001 width=70% }
# Выводы

Рассмотрели простейшую модель эпидемии. Все щаги били успещно выполнёны.

## {.standout}

