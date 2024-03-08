---
## Front matter
title: "Отчёт по лабораторной работе №5"
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

Изучаем модель хищник-жертва и построим график модели с помощью Scilab.

# II.Задание

Для модели «хищник-жертва»:

$$
\begin{cases} \frac{dx}{dt}=-0.13x(t)+0.042x(t)y(t)\\ \frac{dy}{dt}=0.33y(t)-0.03x(t)y(t) \end{cases}
$$

Постройте график зависимости численности хищников от численности жертв,
а также графики изменения численности хищников и численности жертв при
следующих начальных условиях: $x_0=7, y_0=12$. Найдите стационарное
состояние системы.

# III. Выполнение задания

## 1. С помощью Scilab построим график зависимости численности хищников от численности жертв, а также графики изменения численности хищников и численности жертв

В Scilab мы задаём коеффициенты, соответстующие с заданием:

``` Juila
a= 0.13; // коэффициент естественной смертности хищников
b= 0.33; // коэффициент естественного прироста жертв
c= 0.042; // коэффициент увеличения числа хищников
d= 0.03; // коэффициент смертности жертв
```
Затем задаём функция модели:
``` Julia
function dx=syst2(t, x)
dx(1) = -a*x(1) + c*x(1)*x(2);
dx(2) = b*x(2) - d*x(1)*x(2);
endfunction
```

После этого задаём начальные условия модели, и интервал с шагом:

``` Julia
t0 = 0; // Начальный момент
x0=[7;12]; //начальное значение x и у (популяция хищников и популяция жертв)
t = [0: 0.1: 300];
```

Решаем дифференциальные уравнения:

``` Julia
y = ode(x0, t0, t, syst2);
n = size(y, "c");
for i = 1: n
y2(i) = y(2, i);
y1(i) = y(1, i);
end
```
И построим график модели с помощью кодами:

* Построение графика колебаний изменения числа популяции хищников:
``` Julia
plot(t, y1);
```

Результат:

![График колебаний изменения числа популяции хищников](https://drive.google.com/uc?id=1TJ8fd3-mNnshdh3DQrpsVl1yyyEZLzhA)

* Построение графика колебаний изменения числа популяции хищников:
``` Julia
plot(t, y2);
```

![График колебаний изменения числа популяции жертв](https://drive.google.com/uc?id=1I_pUkiYXkiqRn8HS9-KtLyiD5GeiqiXF)

* Построение графика зависимости изменения численности хищников от изменения численности жертв:
``` Julia
plot(y1, y2);
```

![График зависимости изменения численности хищников от изменения численности жертв](https://drive.google.com/uc?id=1fcA9gEmDNZYtJXdi9kAKcvaA_oELcBmb)

## 2. Наидём стационарное состояние системы

$$
\begin{cases} \frac{dx}{dt}=-0.13x(t)+0.042x(t)y(t)\\ \frac{dy}{dt}=0.33y(t)-0.03x(t)y(t) \end{cases}
$$

От этой системы мы получим коеффициенты: $a=0.13;$ $b=0.042;$ $c=0.33;$ $d=0.03$

Стационарное состояние системы (положение равновесия, не зависящее
от времени решение) будет в точке:

$$
\begin{cases} x_0=\frac{a}{b}=0.13/0.042 \approx 3.905 \\ y_0=\frac{c}{d}=0.33/0.033 \approx 11 \end{cases}
$$

# IV. Вывод

После лабораторной работы я познакомилься с моделей хищник-жертва и получил графики модели.
