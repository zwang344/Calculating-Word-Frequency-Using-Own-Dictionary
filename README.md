# Calculating-Word-Frequency-Using-Own-Dictionary
import os
import glob
import pandas as pd

path = ''

#automatically read all same file type in the folder
reviewlist = []
for eachfile in glob.glob(os.path.join(path, '*.csv')):
    f = pd.read_csv(eachfile)
    f = f['reviews']
    
    content =''
    for line in f:
        content = content+line
    reviewlist.append(content)

#Create A List For Our Own Dictionary
dict_path = 'D:\\Fashion AI\\SHFW\\Fashion_Dictionary_new.csv'

dictionary = pd.read_csv(dict_path, header=None, encoding='utf-8-sig')
dict_list = []
for word in dictionary[0]:
    dict_list.append(word)

#Count Word Frequency for Each File
wordcount_list=[]
for review in reviewlist:
    word_count={}
    for word in dict_list:
        word_count[word] = review.count(word)
    wordcount_list.append(word_count)

rowname = ['a', 'b','c','d','e','f','g']

wordcount_matrix = pd.DataFrame(wordcount_list, index=rowname)
wordcount_matrix

#save file
wordcount_matrix.to_csv('D:\\Fashion AI\\SHFW\\wordcount_matrix.csv',  encoding='utf-8')
