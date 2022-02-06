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
1. Запустить файлы из папки parse_docs_and_titles: Сначала запускается Парсинг заголовков.ipynb.

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

2. Запускаем файлы из папки classic_text_features - генерируем классические текстовые фичи (можно запускать в любом порядке, можно запускать несколько ноутбуков параллельно - если позволяет cpu).

3. a
4. ф
5. ф
6. ф
7. ф
8. ф
9. ф
10. ф
11. ф
