---
## Front matter
title: "Отчёт по лабораторной работе №6"
subtitle: "Вариант 2"
author: "Ле Тиен Винь"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true # Table of contents
toc-depth: 2
lof: false # List of figures
lot: false # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
	- spelling=modern
	- babelshorthands=true
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase,Scale=0.9
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lotTitle: "Список таблиц"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage[T2B]{fontenc}
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

## Выполнение лабораторной работы

Формула для выбора варианта: `(1032215241%70)+1` = 2 вариант.

# I.Цель работы

Изучать задачу об эпидемии и построить график об скорости изменении каждой группы особи в эпидемии.

# II. Задание

На одном острове вспыхнула эпидемия. Известно, что из всех проживающих на острове $(N=25 000)$ в момент начала эпидемии $(t=0)$ число заболевших людей (являющихся распространителями инфекции) $I(0)=150$, А число здоровых людей с иммунитетом к болезни $R(0)=15$. Таким образом, число людей восприимчивых к болезни, но пока здоровых, в начальный момент времени $S(0)=N-I(0)-R(0)$.

Постройте графики изменения числа особей в каждой из трех групп. Рассмотрите, как будет протекать эпидемия в случае:

1. Если $I(0) \le I^*$

2. Если $I(0) > I^*$

# III. Выполнение задания

## 1. Теорема

В простейшей модели эпидемии мы разделим популяцию N на 3 группы:

* Восприимчивые к болезни, но пока здоровые особи, обозначим их через $S(t)$.

* Число инфицированных особей, которые также при этом являются распространителями инфекции, обозначим их $I(t)$.

* Здоровые особи с иммунитетом к болезни, обозначим их $R(t)$.

В случае число заболевших не превышает критического значения $I^*$, считаем, что все больные изолированы и не заражают здоровых, то скорость изменения числа $S(t)$ меняется по следующему:

$$\frac{dS}{dt}=0 \Rightarrow S(t) = S(0)$$

Скорость изменения числа инфекционных особей $I(t)$ представляет разность за единицу времени между заразившимися и теми, кто уже болеет и лечится, то есть:

$$\frac{dI}{dt}=-\beta I \Rightarrow \frac{dI}{I}=-\beta dt \Rightarrow lnI=-\beta t \Rightarrow I = e^{-\beta t}$$

Скорость изменения выздоравливающих особей $R(t)$ меняется по следующему:

$$\frac{dR}{dt}=\beta I \Rightarrow dR=\beta Idt \Rightarrow R=\beta It$$

Постоянные пропорциональности $\alpha$, $\beta$, - это коэффициенты заболеваемости и выздоровления соответственно.

Когда $I(t)>I^*$, тогда инфицирование способны заражать восприимчивых к болезни особей. В этом случае скорость изменения числа $S(t)$ меняется по следующему:

$$\frac{dS}{dt}=-\alpha S \Rightarrow \frac{dS}{S}=-\alpha dt \Rightarrow lnS=-\alpha t \Rightarrow S=e^{-\alpha t}$$

Скорость изменения числа $I(t)$ меняется по следующему:

$$\frac{dI}{dt}=\alpha S-\beta I \Rightarrow I'+\beta I=\alpha S \Rightarrow e^{\beta t}I'+e^{\beta t}\beta I =e^{\beta t}\alpha S$$
$$\Rightarrow (Ie^{\beta t})'=e^{\beta t}\alpha S \Rightarrow Ie^{\beta t}=\int e^{\beta t}\alpha Sdt \Rightarrow I=\beta e^{\beta t}\alpha S $$

Скорость изменения числа $R(t)$ меняется по следующему:

$$\frac{dR}{dt}=\beta I \Rightarrow dR=\beta Idt \Rightarrow R=\beta It$$

## 2. С помощью Scilab построим график случая: $I(t) \le I^*$

* В Scilab мы введём начальные условия и коэффициенты $\alpha$, $\beta$:

``` Julia
a = 0.01;	// коэффициент заболеваемости
b = 0.02;	//коэффициент выздоровления
N = 25000;	// общая численность популяции
I0 = 150;	// количество инфицированных особей в начальный момент времени
R0 = 15;	// количество здоровых особей с иммунитетом в начальный момент времени
S0 = N - I0 - R0;	// количество восприимчивых к болезни особей в начальный момент времени
```

* Задаём функии для решения:

``` Julia
function dx=syst(t, x)
dx(1) = 0;
dx(2) = - b*x(2);
dx(3) = b*x(2);
endfunction
```

* Решаем системы:

``` Julia
t0 = 0;
x0=[S0;I0;R0]; //начальные значения
t = [0: 0.01: 200];
y = ode(x0, t0, t, syst);
```

* Построим график:

``` Julia
plot(t, y);
hl=legend(['S(t)';'I(t)';'R(t)']);
```

Мы получим результат:

![График первого случая](https://drive.google.com/uc?id=1fG8XiwIjp9I8z9rOA7KetXdSKREpup4E)

## 3. С помощью Scilab построим график случая: $I(t) > I^*$

* После введения начальных условии и коэффициентов, мы введём функии для решения:

``` Julia
function dx=syst(t, x)
dx(1) = - a*x(1);
dx(2) = a*x(1) - b*x(2);
dx(3) = b*x(2);
endfunction
```

Решая и построив график, мы получим результат:

![График второго случая](https://drive.google.com/uc?id=1y8_0XrxmbGK1Ekw8vW19URNiHeK557mE)

# IV. Вывод

После лабораторной работы, я познакомился с задачой об эпидемии и приобрел привык к построению графика об скорости изменении каждой группы особи в эпидемии.
