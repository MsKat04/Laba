Работа #2. Нужно больше золота

Коротаева Екатарени Андреевна
РИ-220930

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |

Работу проверили:

к.т.н., доцент Денисов Д.В.
к.э.н., доцент Панов М.А.
ст. преп., Фадеев В.О.
N|Solid

Build Status

Цель работы.
научиться передавать в Unity данные из Google Sheets с помощью Python.

Задание 1. Выберите одну из компьютерных игр, приведите скриншот её геймплея и краткое описание концепта игры. Выберите одну из игровых переменных в игре (ресурсы, внутри игровая валюта, здоровье персонажей и т.д.), опишите её роль в игре, условия изменения / появления и диапазон допустимых значений. Постройте схему экономической модели в игре и укажите место выбранного ресурса в ней.

Game: Ark: Survival Evolved

![image](https://github.com/MsKat04/Laba/assets/116561169/e1902ab8-c815-480a-9daa-14dd49d9a9a3)


Ход работы:
Кратко описать концепт игры, выбрать игровую переменную, описать её характеристики и роль в игре и построить экономическую модель игры.

Описание концепта игры.
Ark: Survival Evolved - Многопользовательская компьютерная игра в жанре симулятора выживания. Игроки должны выжить на острове, наполненном разнообразными существами, и другими потенциально враждебными игроками.

Игровой валютой являются природные ресурсы (камни, брёвна, ягоды, мясо и т.д.)
Валюта может использоваться для: строительста, выживания, изучения, покупки в форме обмена с торговцами и другими игроками.

Минимальное значение: 0 всего. при старте игры ты оказываешься ни с чем, но это можно добыть практически сразу.
Максимальное значение: с собой ты всё хранить не сможешь т.к есть ограничение мест в рюкзаке, но можно будет хранить вещи в сундуках и тут уже ограничений нет.


Схема "экономической" модели в игре.

![image](https://github.com/MsKat04/Laba/assets/116561169/1a7b205e-ed1c-4013-b472-29840adade58)

Задание 2. С помощью скрипта на языке Python заполните google-таблицу данными, описывающими выбранную игровую переменную в выбранной игре (в качестве таких переменных может выступать игровая валюта, ресурсы, здоровье и т.д.). Средствами google-sheets визуализируйте данные в google-таблице (постройте график, диаграмму и пр.) для наглядного представления выбранной игровой величины.

Ход работы:

Настроить доступ к google-таблице по api, написать код генерации данных с помощью Python, используя gspread.
Передать данные в таблицу, построить график и диаграмму, используя переданные данные.
```py
import gspread
import numpy as np
gc = gspread.service_account(filename='myprojecteb.json')
sh = gc.open("UnityWorkshop2")
price = np.random.randint(-50, 200, 11)
mon = list(range(1,11))
i = 0
while i <= len(mon):
    i += 1
    if i == 0:
        continue
    else:
        tempInf = price[i-1]
        tempInf = str(tempInf)
        tempInf = tempInf.replace('.',',')
        sh.sheet1.update(('A' + str(i)), str(i))
        sh.sheet1.update(('B' + str(i)), str(price[i-1]))
        sh.sheet1.update(('C' + str(i)), str(tempInf))
        print(tempInf)
```


![image](https://github.com/MsKat04/Laba/assets/116561169/05a2cade-ee57-49b0-9da2-8144a97f447e)



Задание 3
Настройте на сцене Unity воспроизведение звуковых файлов, описывающих динамику изменения выбранной переменной. Например, если выбрано здоровье главного персонажа вы можете выводить сообщения, связанные с его состоянием.
Ход работы:

Создать ключ API для передачи данных из google-таблицы в Unity.
Создать новый 3D проект на Unity, добавить необходимые звуковые файлы.
Написать скрипт для воспроизведения звуков, в зависимости от значения в таблице.

```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.Networking;
using SimpleJSON;



public class NewBehaviourScript : MonoBehaviour
{
    public AudioClip goodSpeak;
    public AudioClip normalSpeak;
    public AudioClip badSpeak;
    private AudioSource selectAudio;
private Dictionary<string,float> dataSet = new Dictionary<string, float>();
    private bool statusStart = false;
    private int i = 1;

    // Start is called before the first frame update
    void Start()
    {
        StartCoroutine(GoogleSheets());
    }

    // Update is called once per frame
    void Update()
    {
        if(dataSet.Count == 0) return;
        if (dataSet["Mon_" + i.ToString()] <= 10 & statusStart == false & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioGood());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
        }

        if (dataSet["Mon_" + i.ToString()] > 10 & dataSet["Mon_" + i.ToString()] < 100 & statusStart == false & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioNormal());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
        }

        if (dataSet["Mon_" + i.ToString()] >= 100 & statusStart == false & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioBad());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
        }
    }
IEnumerator GoogleSheets()
    {
        UnityWebRequest curentResp = UnityWebRequest.Get("https://sheets.googleapis.com/v4/spreadsheets/1CEjtCsGKu_fHyNkAAnhjj7Op5AObTqc0w-XotEF8bTI/values/Лист1?key=AIzaSyBKVavx-X7nPIJWv_SaABdWUtD5ewh_Omk");
        yield return curentResp.SendWebRequest();
        string rawResp = curentResp.downloadHandler.text;
        var rawJson = JSON.Parse(rawResp);
        foreach (var itemRawJson in rawJson["values"])
        {
            var parseJson = JSON.Parse(itemRawJson.ToString());
            var selectRow = parseJson[0].AsStringList;
            dataSet.Add(("Mon_" + selectRow[0]), float.Parse(selectRow[2]));
        }
    }

    IEnumerator PlaySelectAudioGood()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = goodSpeak;
        selectAudio.Play();
        yield return new WaitForSeconds(3);
        statusStart = false;
        i++;
    }
    IEnumerator PlaySelectAudioNormal()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = normalSpeak;
        selectAudio.Play();
        yield return new WaitForSeconds(3);
        statusStart = false;
        i++;
}
    IEnumerator PlaySelectAudioBad()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = badSpeak;
        selectAudio.Play();
        yield return new WaitForSeconds(4);
        statusStart = false;
        i++;
    }
}
```
![image](https://github.com/MsKat04/Laba/assets/116561169/52422cbd-bfdf-4b9b-bf28-fbc778a2a4ab)


## Выводы

Я узнала как передавать данные в гугл таблицу, используя язык Python, а также как считывать данные из таблицы и затем их использовать в Unity.
Также я вспомнила как создавать диаграммы в Google таблице и синтаксис Python.

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
