---
## Front matter
title: "Отчёт по лабораторной работе №6"
subtitle: "лабораторная работа №6"
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
lof: true # List of figures
lot: true # List of tables
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
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы
Изучаем модель боевых действий и построим графики изменения численности войск армии Х и армии У для каждого случая

## Выполнение лабораторной работы

Формула для выбора варианта: `(1032215241%70)+1` = 2 вариант.

# Задание

Постройте график распространения рекламы, математическая модель которой описывается следующим уравнением:

1. $\frac{dn}{dt} = (0.65 + 0.0002 (t)n(t))(N-n(t))$
2. $\frac{dn}{dt} = (0.0003 + 0.9 (t)n(t))(N-n(t))$
3. $\frac{dn}{dt} = (0.1*sin(2*t) + 0.2*cos(3*t) (t)n(t))(N-n(t))$

При этом объем аудитории $N = 1000$, в начальный момент о товаре знает $2$ человек. Для случая 2 определите в какой момент времени скорость распространения рекламы будет иметь максимальное значение.

 III. Выполнение задания

## 1. Введение теоремы

Модель рекламной кампании имеет вид:

$$
\frac{dn}{dt}=(\alpha _1 (t)+\alpha _2 (t)n(t))(N-n(t))
$$

где,

* $\frac{dn}{dt}$ - скорость изменения со временем числа потребителей,
узнавших о товаре и готовых его купить.

* $t$ -  время, прошедшее с начала рекламной кампании.

* $n(t)$ - число уже информированных клиентов.

* $N$ - общее число потенциальных платежеспособных покупателей.

* $\alpha _1(t)>0$ - характеризует интенсивность рекламной кампании (зависит от затрат на рекламу в данный момент времени).

* $\alpha _2(t)$ - функция, описывающая сарафанное радио

## 2. Построии график распространения рекламы, математическая модель которой описывается следующим уравнением:

### 2.1. $\frac{dn}{dt} = (0.65 + 0.0002 (t)n(t))(N-n(t))$

Введём в Scilab:

* Начальные условия, соответствующие заданию:

``` Julia
t0=0;  //начальный момент времени
x0=2;  // количество людей, знающих о товаре в момент t0
N=1000; // максимальное количество людей, которых может заинтересовать товар
t=0:0.1:30; // временной промежуток
```

* Функция, отвечающая за платную рекламу и функция, описывающая сарафанное радио:

``` Julia
// Функция, отвечающая за платную рекламу
function g=k(t);
g=0.65;
endfunction
// Функция, описывающая сарафанное радио:
function v=p(t);
v=0.0002;
endfunction
```

* Уравнение, описывающее распространение рекламы:

``` Julia
function dx=f(t,x);
dx=(k(t)+p(t)*x)*(N-x);
endfunction
```

* Решение и график решения:

``` Julia
x=ode(x0,t0,t,f);
plot(t,x);
```

После этого, мы получим результат:

![](https://drive.google.com/uc?id=1vwB6Bbe0xQzdIyYo4MRE3poDPrCHeRlm)

### 2.2. $\frac{dn}{dt} = (0.0003 + 0.9 (t)n(t))(N-n(t))$

В этом случае, мы введём начальные условия, соответствующие заданию, задаём временной промежуток от 0 до 3, чтобы видеть график видно. Затем введём функцию, отвечающую за платную рекламу и функцию, описывающую сарафанное радио. Введём уравнение, описывающее распространение рекламы и решение уравнения.

После этого, мы получим результат:

![](https://drive.google.com/uc?id=14msLEBWHBCokgboFdT7Iz0h_9JOC1sIR)

В результате указывается в момент $t=0.1$ скорость распространения рекламы будет иметь максимальное значение.

### 2.3.$\frac{dn}{dt} = (0.1*sin(2*t) + 0.2*cos(3*t) (t)n(t))(N-n(t))$

Мы задаём временной промежуток от 0 до 3, и остальные введём как в части 2.1 и 2.2. Мы получим результат:

![](https://drive.google.com/uc?id=1NWcXMmEKUgSvyik5kl-P0F6rKK882zlq)

# IV. Вывод

После лабораторной работе я познакомился с моделью рекламной компании и получил навыки по построению график этой модели.
