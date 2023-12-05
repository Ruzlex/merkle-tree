# Merkle Tree

В проекте представлены основные классы данных, которые используются в блокчейне. 
Необходимо написать реализацию методов и проверить правильность с помощью тестов.  
Для запуска тестов необходимо установить [nodejs](https://nodejs.org/) и необходимые библиотеки.  

## Установка 

Клонируйте репозиторий, перейдите в каталог проекта и установите зависимости.  
```bash 
git clone https://github.com/labintsev/merkle-tree
cd merkle-tree
npm install
```

Запуск всех тестов 
```bash
npx mocha test
```

## 1. Blockhain primitive

Блокчейн - это структура данных, состоящая из нескольких блоков. 
В этом упражнении класс `Block` представляет собой простую обертку над некоторыми данными. 
Для упрощения мы считаем что `data` - это просто некоторая строка.  

Кроме данных, блок содержит поле `previousHash`, которое хранит в себе хэш предыдущего блока в блокчейне.
Хэш блока вычисляется от конкатенации двух полей `data + previousHash`. 
Итерактивное демо https://blockchaindemo.io/   

Каждый новый блок добавляется в блокчейн через вызов метода `addBlock(block)`. 
Перед добавлением в цепочку в поле `block.previousHash` необходимо записать хэш предыдущего блока. 
Реализуйте эту логику.  


Когда к сети подключается новый участник, он должен проверить правильность построения всей цепочки. 
Метод `isValid()` возвращает `true`, если для каждого блока в цепочке в поле `previousHash` содержится хэш предыдущего блока. 
При любом несовпадении возвращается `false`. 
Реализуйте эту логику.    

Запуск теста:  

```sh
npx mocha test/Blockchain.js
``` 

## 2. Transaction output

Объект `TXO` - transaction output, содержит информацию об адресе владельца и количестве монет. 
Реализуйте конструктор транзакции с полями `owner, amount, spent, hash`. 

Метод `spend()` означает проведение транзакции и может быть вызван только один раз. 
Реализуйте метод `spend()`, который будет устанавливать поле `spent` в значение `true`. 
При попытке провести транзакцию дважды должна бросаться ошибка `Error('Already spended!')`.  

Запуск теста:  

```sh
npx mocha test/TXO.js
``` 

## 3. Binary search tree 

Транзакции хранятся в блоке в специальной структуре данных - модифицированном дереве Меркла. 
В отличии от линейных структур данных типа массива или связного списка, деревья позволяют осуществлять эффективный поиск за логарифмическое время.  

Мы пойдем от простого к сложному и для начала вспомним, как реализуются основные методы классического бинарного дерева поиска. 
Класс `Node` является узлом бинарного дерева, помимо полезных данных от содержит ссылки на левого и правого потомка. 
Здесь важно не запутаться в синонимах, под словом `Node` мы также можем иметь ввиду узел вычислительной сети. 
Практически всегда можно понять о какой ноде идет речь из контекста повествования.  

Класс `Tree` - классическое бинарное дерево поиска.  

В файле `Tree.js` реализуйте метод `addNode(node)` для добавления узла. 

Реализуйте метод `hasNode(data)` для проверки, есть ли в дереве узел с таким содержимым.  

Запуск теста:  

```sh
npx mocha test/Tree.js
``` 
