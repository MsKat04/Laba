# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #3 выполнил(а):
- Коротаева Катя
- РИ-220930

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |


Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

## Цель работы
Разработать оптимальный баланс для десяти уровней игры Dragon Picker.
## Задание 1. 

### Предложите вариант изменения найденных переменных для 10 уровней в игре. Визуализируйте изменение уровня сложности в таблице. 

Я проанализировала варианты возможного усложнения переменных и решила увеличивать (или уменьшать) все переменные одновременно. 
Визуализироваю данные в таблице:

![image](https://github.com/MsKat04/Laba/assets/116561169/7a817713-54c3-45c4-9ed8-e3aaa2a3716c)

## Задание 2
### Создайте 10 сцен на Unity с изменяющимся уровнем сложности.

- Создать ещё 9 аналогичных сцен. Поменять значение "Speed", "TimeBetweenEgg", "LeftRightDistance", "ChanceDirection" в уровнях.
Создание уровней: 
![image](https://github.com/MsKat04/Laba/assets/116561169/50a83666-bb6f-4f37-8ac2-ef79fc115252)

![image](https://github.com/MsKat04/Laba/assets/116561169/eee9ef16-cd6d-4dd7-9eb5-4c87cd0101b0)


## Задание 3
### Решение в 80+ баллов должно заполнять google-таблицу данными из Python. В Python данные также должны быть визуализированы.

## Ход работы:
Создала таблицу, написав код заполняющий Google таблицу данными из скрипта. Результатом является скрин с первого задания.

```py
import gspread
import numpy as np
gc = gspread.service_account(filename='work3-402301-5356a8a03963.json')
sh = gc.open("UnityWorkShop 3")
speed = 4.00
timeEgg = 2.00
lrDist = 10.00
chanceDir = 0.01
i = 0
while i < 10:   
    rand = np.random.randint(-50, 150, 3)    
    i += 1     
    sh.sheet1.update(('A' + str(i+2)), speed+2.35*i+(rand[0]/1000))
    sh.sheet1.update(('B' + str(i+2)), timeEgg-0.17*i+(rand[1]/1000))
    sh.sheet1.update(('C' + str(i+2)), lrDist+0.49*i+(rand[2]/1000))
    sh.sheet1.update(('D' + str(i+2)), chanceDir+0.0004*i)
    sh.sheet1.update(('E' + str(i+1)), i)
    print('ok')
```

## Выводы
Я создала 10 сцен в игре Dragon Picker. Попробовала разные изменения переменных и создала уровни с разными сложностями. И заполнила таблицу с помощью Python.

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| GitHub | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**






