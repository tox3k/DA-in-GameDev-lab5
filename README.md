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
Вывод: Так как при коэффиценте корреляции равным 1.42 мы имеем максимальное вознаграждение и стандартное отклонение равное 0, то при его изменения, мы видим что вознаграждение стало асбсолютно разным и появилось стандартное отклонение. Следовательно коэффицент корреляции отвечает за точность обучения, то есть чем точней мы его подберем, тем выше точность обучения. Также он влияет на скорость обучения, чем меньше коэффицент, тем больше времени может уйти на обучение.

## Задание 2  
### Изменить параметры файла yaml-агента и определить какие параметры и как влияют на обучение модели. Привести описание не менее трех параметров.  
- network_settings:  
  - normalize: Этот параметр отвечает нормализацию входных данных, то есть если нужна их нормализации, устанавливаем значение true, если нет - false. По умолчанию у нас стоит false.    
  true:        
  ![Image alt](https://github.com/tox3k/DA-in-GameDev-lab5/blob/main/scrinshots/step3.png)  
  ![Image alt](https://github.com/tox3k/DA-in-GameDev-lab5/blob/main/scrinshots/step4.png)  
  ![Image alt](https://github.com/tox3k/DA-in-GameDev-lab5/blob/main/scrinshots/step5.png)  
  Вывод:  
    - Во первых увеличось время обучения, так как пришлось нормализовывать данные
    - Ошибка обучения планомерно уменьшается и стремится к нулю
    - Дополнительные вознаграждения(Extrinsic Rewards) и накопительные награды (Cumulative Rewards) очень неоднозначно и имеют резкое падания вознаграждения, но обратно возрастают. Оценка внешней ценности (Extrinsic value estimate) стабильны, но на низком уровне в сравнение со стартовыми настройками, где ценность повышается со временем. Энтропия(Entropy) стабильно растет.  
  
- time_horizon: Количество шагов опыта,которое должно быть собрано для каждого агента, прежде чем его можно будет добавить в буфер опыта.Если этот предел достигнут до окончания эпизода, оценка стоимости используется для прогнозирования общего ожидаемого вознаграждения на основе текущего состояния агента. Также если эпизоды обучения достаточно большие, то следует брать меньшее число. По умолчанию 64.
  32:    
  ![Image alt](https://github.com/tox3k/DA-in-GameDev-lab5/blob/main/scrinshots/step6.png)    
  ![Image alt](https://github.com/tox3k/DA-in-GameDev-lab5/blob/main/scrinshots/step7.png)    
  ![Image alt](https://github.com/tox3k/DA-in-GameDev-lab5/blob/main/scrinshots/step8.png)
  Вывод:
    -fdsfds
  64:    
  ![Image alt](https://github.com/tox3k/DA-in-GameDev-lab5/blob/main/scrinshots/step9.png)    
  ![Image alt](https://github.com/tox3k/DA-in-GameDev-lab5/blob/main/scrinshots/step10.png)    
  ![Image alt](https://github.com/tox3k/DA-in-GameDev-lab5/blob/main/scrinshots/step11.png)
  Вывод:
    -fdsfds
  128:    
  ![Image alt](https://github.com/tox3k/DA-in-GameDev-lab5/blob/main/scrinshots/step12.png)    
  ![Image alt](https://github.com/tox3k/DA-in-GameDev-lab5/blob/main/scrinshots/step13.png)    
  ![Image alt](https://github.com/tox3k/DA-in-GameDev-lab5/blob/main/scrinshots/step14.png)
  Вывод:
    -fdsfds

- hyperparameters:
    - buffer_size: Объем данных, который необходимо собрать перед обновлением модели политики. Это соответствует тому, какой объем опыта вам необходимо собрать, прежде чем вы начнете изучать или обновлять свою модель. По умолчанию 10240.
    4240:    
    ![Image alt](https://github.com/tox3k/DA-in-GameDev-lab5/blob/main/scrinshots/step9.png)    
    ![Image alt](https://github.com/tox3k/DA-in-GameDev-lab5/blob/main/scrinshots/step10.png)    
    ![Image alt](https://github.com/tox3k/DA-in-GameDev-lab5/blob/main/scrinshots/step11.png)
    Вывод:
      -fdsfds
  
    10240:    
    ![Image alt](https://github.com/tox3k/DA-in-GameDev-lab5/blob/main/scrinshots/step9.png)    
    ![Image alt](https://github.com/tox3k/DA-in-GameDev-lab5/blob/main/scrinshots/step10.png)    
    ![Image alt](https://github.com/tox3k/DA-in-GameDev-lab5/blob/main/scrinshots/step11.png)
    Вывод:
      -fdsfds

    20240:    
    ![Image alt](https://github.com/tox3k/DA-in-GameDev-lab5/blob/main/scrinshots/step9.png)    
    ![Image alt](https://github.com/tox3k/DA-in-GameDev-lab5/blob/main/scrinshots/step10.png)    
    ![Image alt](https://github.com/tox3k/DA-in-GameDev-lab5/blob/main/scrinshots/step11.png)
    Вывод:
      -fdsfds
    
  
## Задание 3
### Приведите примеры, для каких игровых задачи и ситуаций могут использоваться примеры 1 и 2 с ML-Agent’ом. В каких случаях проще использовать ML-агент, а не писать программную реализацию решения?  
-  Пример из первой практической работы можно использовать для nps-врагов, которые определяют где находится игрок и двигаются по направлению к нему. Пример: любая гонка, где враги стараются догнать тебя(любая часть Need For Speed)
-  Пример из второй практической работы можно использовать для nps-ботов,которые следуют одной и той же инструкции и передвигаются только из одной точки в другую. Пример: любая ММО, где nps, запрограмированы выполнять и одни и те же действия, передвигаясь только по заданному маршруту, даже если на пути игрок, встают перед ним, не обходя его.
  
Если игрок выполняет много действий и ему нужно к ним приспособиться, чтобы выполнять правильно, проще использовать готового ml-агента. Кроме того, проще использовать готовые алгоритмы вместо написания новых,что значительно сокращает время на разработку чего-либо. Однако ml-агенты могут вообще не потребоваться, потому что в нем нет необходимости,и использование более простого алгоритма будет гораздо более правильным решением.
 

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
