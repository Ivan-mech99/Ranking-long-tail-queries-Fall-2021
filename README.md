# Ranking-long-tail-queries-Fall-2021
Примечание 1: в исходном проекте все .ipynb файлы лежат в одной директории. В репозитории файлы разбиты по папкам из соображений их функций и последовательности запуска  

Примечание 2: в этой же директории должны лежать файлы:  
   *  docs.tsv.gz
   *  2017.tar
   *  queries.tsv
   *  url.data
   *  train.marks.tsv
   *  sample.csv  

## Инструкция по запуску
1. Запустить файлы из папки **parse_docs_and_titles**: Сначала запускается Парсинг заголовков.ipynb.

При этом сгенерируется 2 набора файлов. Файлы:  
* enlarged_querrys.pickle
* id_querry.pickle
* id_querry_clean.pickle
* id_querry_norm.pickle
* id_querry_spelled.pickle
* querry_id.pickle
* querry_id_spelled.pickle

необходимо поместить в папку **query_dict**. Файлы:

* clean_title_data.pickle
* norm_title_data.pickle
* spelled_title_data.pickle
* title_data.pickle

необходимо поместить в папку **title_dict**. Остальные файлы можно запускать в любом порядке (разбиваем нормализованные и ненормализованные тексты по запросам).

2. Запускаем файлы из папки **classic_text_features** - генерируем классические текстовые фичи для документов (можно запускать в любом порядке, можно запускать несколько ноутбуков параллельно - если позволяет cpu).

3. Запускаем файлы из папки **classic_title_features** - генерируем классические текстовые фичи для заголовков (можно запускать в любом порядке, можно запускать несколько ноутбуков параллельно - если позволяет cpu)

4. Запускам фвйлы из папки **neuro_features** - генерируем семантические фичи для текстов и заголовков. Запускать можно в любом порядке, файл Make preembeddings.ipynb - генерирует файл правильно упорядоченный документов для загрузки в collab и расчета на gpu. Его можно не использовать.

5. Кодируем кликовые данные в числовые кортежи (с целью экономии памяти и ускорения майнинга кликовых фичей). Сначала запускаем два файла из папки **recoding_click_data**:

* Обработка кликовых данных upd.ipynb
* Обработка хостовых данных.ipynb

Затем строим вспомогательные словари и исправляем возникающую при этом ошибку - **последовательно** запускаем файлы из той же папки:

* Скелет запрос-блок для урлов.ipynb
* Скелет запрос-блок для хостов.ipynb
* Error_correction.ipynb

6. Первый этап генерации кликовых фичей для урлов и хостов. Запускаем файлы из папки **mining_url_host_features** (в любом порядке).

7. Первый этап генерации кликовых фичей для пар запрос-урл и пар запрос-хост: Запускаем файлы из папки **mining_url-query_host-query_features** (в любом порядке).

8. Второй этап генерации всех кликовых фичей - запускаем файлы из папки **final_click_features_preprocessing** (в любом порядке).

9. Генерируем трейновый и тестовый датафрейм для загрузки в google colab и расчетов на gpu. Запускаем файл make_prediction.ipynb из папки **predict_and_submit**. Полученные при этом файлы (см. ниже) загружаем на гугл диск:

* export_train.csv
* export_test.csv
* export_y.pickle
* qifs.pickle

В google colab запускаем ноутбук **catboost_best_best.ipynb**, обучаем модель, сохраняем ее в файл "deep_yeti_trees.cbm" (можно раскомментить соотв. ячейку), делаем predict. Можем загрузить уже обученную модель по ссылке (см. ниже), поместить ее на гугл диск и сделать predict на 6000 деревьев.

# Дополнительно: 

по ссылке **https://drive.google.com/drive/folders/1SHBvYh3UH2awktM9h-thxuntkUIxE6-J?usp=sharing** можно загрузить:

* файловые системы, генерирующиеся на шагах 1 и 5 - нужно распаковать содержимое файла **FILESYS.rar** в директорию проекта
* признаки, генерирующиеся на шагах с 1 по 8 - нужно распаковать содержимое файла **GOOD FEATURES.rar** в директорию проекта
* датафреймы и вспомогательные файлы, генерирующиеся на файле 8, а также модель, обученную на шаге 9 - нужно распаковать содержимое файла **for final submit.rar**
