# corenlp
corenlp is the wrapper of stanfordcorenlp tools which need jdk-1.8
and you need download model from https://stanfordnlp.github.io/CoreNLP/index.html

## Usage
Examples 1:

```python
# encoding: utf-8
# author: Geoff Liang
# time: 2021/3/9

# import class
from stanfordcorenlp import StanfordCoreNLP

sentence = 'Guangdong University of Foreign Studies is located in Guangzhou.'

# load jar from stanford corenlp path
# memory default is '4g', we set it as '8g'
nlp = StanfordCoreNLP(r'stanford-corenlp-4.2.0', 
                    memory='8g',
                    lang='en',
                    quiet=True)

print("Sentence:", sentence)
# word tokenizer
print("Tokenize:", nlp.word_tokenize(sentence))

print("Part of Speech:", nlp.pos_tag(sentence))

print("Name Entities:", nlp.ner(sentence))

print("Constituency Parsing:", nlp.parse(sentence))

print('Dependency Parsing:', nlp.dependency_parse(sentence))
# server should be closed 
nlp.close()
```

Example 2:

```python
# encoding: utf-8
# author: Geoff Liang
# time: 2021/3/9

# import class
from stanfordcorenlp import StanfordCoreNLP


text = 'Guangdong University of Foreign Studies is located in Guangzhou. ' \
       'GDUFS is active in a full range of international cooperation and exchanges in education. '



# load jar from stanford corenlp path
# memory default is '4g', we set it as '8g'
nlp = StanfordCoreNLP(r'stanford-corenlp-4.2.0', 
                    memory='8g',
                    lang='en',
                    quiet=True) # if you want to debug, you need to set quiet=False
# Details of annotators: https://stanfordnlp.github.io/CoreNLP/annotators.html
props={
    'annotators': 'tokenize,ssplit,pos', # tokenize, split sentence, part of speech
    'pipelineLanguage': 'en', # english
    'outputFormat': 'json' # xml
    }
print(nlp.annotate(text, properties=props))

nlp.close()
```

Example 3:
```python
from corenlp import StanfordCoreNLP


text = 'Guangdong University of Foreign Studies is located in Guangzhou. ' \
       'GDUFS is active in a full range of international cooperation and exchanges in education. '

# load jar from stanford corenlp path
# memory default is '4g', we set it as '8g'

nlp = StanfordCoreNLP(r'/root/stanford-corenlp-4.3.2', 
                    memory='8g',
                    lang='en',
                    quiet=True) # if you want to debug, you need to set quiet=False

print(nlp.sent_tokenize(text))
# ['Guangdong University of Foreign Studies is located in Guangzhou .',
# 'GDUFS is active in a full range of international cooperation and exchanges in education .']
print(nlp.sent_word_tokenize(text))
# [['Guangdong',
#   'University',
#   'of',
#   'Foreign',
#   'Studies',
#   'is',
#   'located',
#   'in',
#   'Guangzhou',
#   '.'],
#  ['GDUFS',
#   'is',
#   'active',
#   'in',
#   'a',
#   'full',
#   'range',
#   'of',
#   'international',
#   'cooperation',
#   'and',
#   'exchanges',
#   'in',
#   'education',
#   '.']]
print(nlp.word_tokenize(text))
# ['Guangdong',
#   'University',
#   'of',
#   'Foreign',
#   'Studies',
#   'is',
#   'located',
#   'in',
#   'Guangzhou',
#   '.',
#   'GDUFS',
#   'is',
#   'active',
#   'in',
#   'a',
#   'full',
#   'range',
#   'of',
#   'international',
#   'cooperation',
#   'and',
#   'exchanges',
#   'in',
#   'education',
#   '.']

nlp.close()
```