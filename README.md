# Анализ данных в разработке игр [in GameDev]
Отчет по лабораторной работе #5 выполнил(а):
- Колчин Андрей Алексеевич
- РИ220950
  
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

Структура отчета

- Данные о работе: название работы, фио, группа, выполненные задания.
- Цель работы.
- Задание 1.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 2.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 3.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Выводы.
- ✨Magic ✨

## Цель работы
- Познакомиться с программными средствами для создания системы машинного обучения и ее интеграции в Unity.

## Задание 1
### Найдите внутри C# скрипта “коэффициент корреляции ” и сделать выводы о том, как он влияет на обучение модели.  
Проанализировав C# скрипт, я нашел коэффицент корреляции - переменная distanceToTarget   
![Image alt](https://github.com/tox3k/DA-in-GameDev-lab5/blob/main/scrinshots/step1.png)    
Изменим коэффицент корреляции и сделаем вывод:     
![Image alt](https://github.com/tox3k/DA-in-GameDev-lab5/blob/main/scrinshots/step2.png)   
Вывод: Так как при коэффиценте корреляции равным 1.42 мы имеем максимальное вознаграждение и стандартное отклонение равное 0, то при его изменения, мы видим что вознаграждение стало асбсолютно разным и появилось стандартное отклонение. Следовательно коэффицент корреляции отвечает за точность обучения, то есть чем точней мы его подберем, тем выше точность обучения.

## Задание 2  
### Изменить параметры файла yaml-агента и определить какие параметры и как влияют на обучение модели. Привести описание не менее трех параметров.  
Стартовые настройки:  
![Image alt](https://github.com/tox3k/DA-in-GameDev-lab5/tree/main/scrinshots/2-step30.png)
![Image alt](https://github.com/prepref/UrFU-GameAnalysis/raw/main/github-screenshots/workshop5/2-step31.png)
![Image alt](https://github.com/prepref/UrFU-GameAnalysis/raw/main/github-screenshots/workshop5/2-step32.png)
- network_settings:  
  - normalize: Показывает, нужно ли нормализировать входные данные.(true, false)  
  normalize = true  
  ![Image alt](https://github.com/prepref/UrFU-GameAnalysis/raw/main/github-screenshots/workshop5/2-step33.png)
  ![Image alt](https://github.com/prepref/UrFU-GameAnalysis/raw/main/github-screenshots/workshop5/2-step34.png)
  ![Image alt](https://github.com/prepref/UrFU-GameAnalysis/raw/main/github-screenshots/workshop5/2-step35.png)
  Вывод:
    - Скачет ошибка обучения, которая в процессе,конечно, уменьшается. Дополнительные вознаграждения(Extrinsic Rewards) сначала растут, достигают максимума и уменьшаются. Оценка внешней ценности (Extrinsic value estimate) стабильны, но на низком уровне в сравнение со стартовыми настройками, где ценность повышается со временем. Энтропия(Entropy) стабильно растет.
    
  - hidden_units: (по умолчанию = 128) Количество узлов в скрытых слоях нейронной сети. То есть каждый скрытый слой нейронной сети имеет такое количество узлов. Если задача простая. то необходимости в большем количестве узлов в каждом слое нейронной сети не требуется.(32 - 512)  
   hidden_units = 32  
  ![Image alt](https://github.com/prepref/UrFU-GameAnalysis/raw/main/github-screenshots/workshop5/2-step36.png)
  ![Image alt](https://github.com/prepref/UrFU-GameAnalysis/raw/main/github-screenshots/workshop5/2-step37.png)
  ![Image alt](https://github.com/prepref/UrFU-GameAnalysis/raw/main/github-screenshots/workshop5/2-step38.png)
   hidden_units = 512    
  ![Image alt](https://github.com/prepref/UrFU-GameAnalysis/raw/main/github-screenshots/workshop5/2-step48.png)
  ![Image alt](https://github.com/prepref/UrFU-GameAnalysis/raw/main/github-screenshots/workshop5/2-step49.png)
  ![Image alt](https://github.com/prepref/UrFU-GameAnalysis/raw/main/github-screenshots/workshop5/2-step50.png)  
  Вывод:
    - В связи с тем, что узлов в каждом скрытом слое 32, уменьшилось время обучения, но и точность обучения из-за этого тоже страдает. Очень сильно скачет ошибка обучения (Value Loss), очень не стабильно. В остальном графики +- одинаковы. Но при 512 узлов в скрытом слое существенно увеличивается время обучения. На 20000 мы имеем Mean Rewards = -1.  Оценка внешней ценности (Extrinsic value estimate) начинает уменьшатьсяс 20000 в отличие от hidden_units = 32. (Extrinsic Rewards) растут экспотенциально.  
            
  - num_layers: (по умолчанию = 2) Количество скрытых слоев в нейронной сети. Для простых задач нет необходимости большого количества скрытых слоев - это может быть неэффективно и долго по времени.(1-3)  
  num_layers = 1  
  ![Image alt](https://github.com/prepref/UrFU-GameAnalysis/raw/main/github-screenshots/workshop5/2-step39.png)
  ![Image alt](https://github.com/prepref/UrFU-GameAnalysis/raw/main/github-screenshots/workshop5/2-step40.png)
  ![Image alt](https://github.com/prepref/UrFU-GameAnalysis/raw/main/github-screenshots/workshop5/2-step41.png)
  num_layers = 3    
  ![Image alt](https://github.com/prepref/UrFU-GameAnalysis/raw/main/github-screenshots/workshop5/2-step51.png)
  ![Image alt](https://github.com/prepref/UrFU-GameAnalysis/raw/main/github-screenshots/workshop5/2-step52.png)
  ![Image alt](https://github.com/prepref/UrFU-GameAnalysis/raw/main/github-screenshots/workshop5/2-step53.png)  
  Вывод:
    - Так как всего один скрытый слой, то в начале ошибка обучения будет максимальной, но в процессе обучения ошибка будет стремится к 0. Время обучения тоже немного сократилось. Точность чуть пострадала,  что на 20000 шаге мы получаем mean rewards < 0. Дополнительные вознаграждения (Extrinsic Rewards) растут экспотенциально. В остальном графики +- похожи. При num_layers = 3 существенно возрастает время обучения, std в среднем выше чем при num_layers = 1. Дополнительные вознаграждения (Extrinsic Rewards) не стабильны.
        
- learning_rate: начальная скорость обучения для градиентного спуска. Как правило, этот показатель следует уменьшить, если обучение нестабильно, а вознаграждение постоянно не увеличивается.  
learning_rate = 0.0001  
![Image alt](https://github.com/prepref/UrFU-GameAnalysis/raw/main/github-screenshots/workshop5/2-step42.png)
![Image alt](https://github.com/prepref/UrFU-GameAnalysis/raw/main/github-screenshots/workshop5/2-step43.png)
![Image alt](https://github.com/prepref/UrFU-GameAnalysis/raw/main/github-screenshots/workshop5/2-step44.png)
learning_rate = 1
![Image alt](https://github.com/prepref/UrFU-GameAnalysis/raw/main/github-screenshots/workshop5/2-step45.png)
![Image alt](https://github.com/prepref/UrFU-GameAnalysis/raw/main/github-screenshots/workshop5/2-step46.png)
![Image alt](https://github.com/prepref/UrFU-GameAnalysis/raw/main/github-screenshots/workshop5/2-step47.png)  
Вывод:
  - Как мы видим, если мы скорость обучения (Learning Rate, Value Loss ) уменьшим просто в 3 раза, ничего особо не поменяется, но если мы зададим значение равное одному, то можем увидить, как существенно сократилось время обучения. Также можно заметить, что в стартовых настройках энтропия (Entropy) +- держится на одном уровне, а тут она сначала возрастает и только потом стабилизируется. Дополнительные вознаграждения(Extrinsic Rewards) тут тоже со не очень стабильно в сравнение со стартовыми настройками.
  
## Задание 3
### Приведите примеры, для каких игровых задачи и ситуаций могут использоваться примеры 1 и 2 с ML-Agent’ом. В каких случаях проще использовать ML-агент, а не писать программную реализацию решения?  
-  1 пример может использоваться для nps-врагов, которые находили бы путь до игрока,наводились на него и двигались к нему: "Need for speed" - соперники едут вплотную
-  2 пример может использоваться для nps, которые ходят только из одной точки в другую: "Clash of clans" - строить постройки, "World of Warcraft" - собирать золото
  
ML-агента проще использовать тогда, когда игрок совершает много действий и к ним требуется адаптация. Также проще использовать уже готовый алгоритм, а не писать новый, что существенно сократит время разработку игры. Но есть случаи, когда ML-агент вовсе не требуется, и использовать более простые алгоритмы будет гораздо правильнее и логичнее.
 

## Выводы
- Познакомился с программными средствами для создания системы машинного обучения и ее интеграции в Unity
- Научился создавать виртуальное пространство для ml-agenta и связывать ml-агента с Unity
- Использовал визуализацию на основне библиотеке tenseorflow

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
