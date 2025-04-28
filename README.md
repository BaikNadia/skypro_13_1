# Библиотека csv
Формат CSV (Comma-Separated Values — значения, разделенные запятыми) — это текстовый формат, широко используемый
для хранения табличных данных, где каждая строка файла соответствует строке таблицы, а ячейки в строке разделены 
специальным символом-разделителем, чаще всего запятой.

Функция csv.reader — используется для чтения содержимого файла. В качестве аргумента функции чтения передается файл.

import csv

with open('file.csv') as file:
    reader = csv.reader(file)   #reader = csv.reader(file, delimiter=';')
    for row in reader:
        print(row)

Функция csv.writer — используется, чтобы записать данные в CSV-файл.

import csv

rows = [['Name', 'Age', 'Gender'],
        ['Alice', '25', 'Female'],
        ['Bob', '30', 'Male'],
        ['Charlie', '35', 'Male']]

with open('file.csv', 'w', newline='') as file:
    writer = csv.writer(file)
    writer.writerows(rows)

Функция DictReader— позволяет читать CSV-файл и создавать словари из строк файла. Ключами в словаре будут названия столбцов, 
а значениями — значения в соответствующих ячейках.

import csv

with open('file.csv') as file:
    reader = csv.DictReader(file)
    for row in reader:
        print(row['Name'], row['Age'], row['Gender'])

Функция DictWriter — позволяет записывать словари в CSV-файл.  

import csv

rows = [{'Name': 'Alice', 'Age': '25', 'Gender': 'Female'},
        {'Name': 'Bob', 'Age': '30', 'Gender': 'Male'},
        {'Name': 'Charlie', 'Age': '35', 'Gender': 'Male'}]

with open('file.csv', 'w', newline='') as file:
    fieldnames = ['Name', 'Age', 'Gender']
    writer = csv.DictWriter(file, fieldnames=fieldnames)
    writer.writeheader()
    for row in rows:
        writer.writerow(row)

# Создание и чтение данных в pandas

Функция pd.read_csv() — используется для чтения данных из CSV-файла

wine_reviews = pd.read_csv("winemag-data-130k-v2.csv")

Метод head() — по умолчанию выводит первые пять строк таблицы. Вы можете указать другое количество строк в аргументе.

Функция pd.read_excel() — используется для чтения данных из файла Excel. Этот метод обладает дополнительными параметрами, 
такими как имя листа или указание столбца, который следует использовать в качестве индекса.

Установка библиотеки openpyxlдля корректной работы с Excel-файлами в pandas:

poetry add openpyxl

excel_data = pd.read_excel("example_data.xlsx")

## Обращение к данным по строкам через индексацию

Индексация — это процесс доступа к данным в датафрейме с использованием их позиции (номеров строк и столбцов) или меток (имен строк и столбцов). 
Индексация позволяет эффективно выбирать, модифицировать и анализировать данные, содержащиеся в датафрейме.
iloc(Integer Location) — позволяет осуществлять доступ к данным по их числовым индексам или позициям.
loc(Label Location) — позволяет осуществлять доступ к данным по их меткам или именам.

dataframe.iloc[индексы строк, индексы столбцов] #reviews.iloc[0]    # Первая строка датафрейма
dataframe.loc[метки строк, метки столбцов] #reviews.loc[0, 'country']     # Значение первой строки в столбце 'country'

## Управление индексом

Метод set_index()в pandas — позволяет управлять индексом датафрейма и используется для назначения одного или нескольких столбцов в качестве индекса датафрейма.

import pandas as pd

data = {
    'student_id': ['001', '002', '003'],
    'name': ['Alice', 'Bob', 'Charlie'],
    'grade': [87, 92, 78]
}

df = pd.DataFrame(data)

 Установить 'student_id' в качестве индекса
df.set_index('student_id', inplace=True)

 Легкий доступ к данным конкретного студента
print(df.loc['001'])
