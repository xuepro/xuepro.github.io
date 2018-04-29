---
layout:       post
title:        "数据结构-哈希表Hash Table"
subtitle:     "Hash Table"
date:         2017-11-10 10:12:00
author:       "xuepro"
header-img:   "img/home_bg.jpg"
header-mask:  0.3
catalog:      true
multilingual: true
tags:
    - DS
---

原理请观看数据结构视频课程的[“网易云课堂”](http://study.163.com/course/introduction.htm?courseId=1004703004)和[“腾讯课堂”]()

哈希表Hash Table

C版本
```c
// copyright by hwdong 
#include <stdio.h> 
#include <stdlib.h> 
#define SIZE 119 
#define OK 0
#define ERROR 1

typedef int KeyType;

typedef struct{
  KeyType key;
  double score;
}ElemType;

typedef struct h_lnode{
  ElemType data;
  struct h_lnode *next;
}HLNode;

typedef struct{
   /* int *array = (int *) malloc(100 * sizeof(int)) */   
   HLNode* *table;  /* HLNode* table[100] */   
   int size;
}HashTable;

int InitHashTable( HashTable *hashT){
  hashT->table = (HLNode* *) 
      malloc(SIZE*sizeof(HLNode*));
  if (!hashT->table) return ERROR;

  hashT->size = SIZE;
  for (int i = 0; i < hashT->size; i++)
      hashT->table[i] = 0;
  return OK;
}

int  Hash(KeyType key){ return key%SIZE;}

int InsertHashTable( HashTable *hashT, 
    KeyType key, ElemType e)
{
  HLNode* s = (HLNode* )malloc(sizeof(HLNode));
  if(!s) return ERROR;
  s->data = e;

  int hash_address = Hash(key);

 /*新结点插入在hashT.table[hash_address]所指示的链表的最前面*/   
  s->next = hashT->table[hash_address]; 
  hashT->table[hash_address] = s;

  return OK;
}


int FindHashTable( HashTable hashT,
  KeyType key, ElemType *e)
{
  int hash_address = Hash(key);

  HLNode* p = hashT.table[hash_address];
  while (p){
    if (p->data.key == key) {
       *e = p->data;
       return OK;
    }
    p = p->next;
  }
  return ERROR;
}

void HashTable_test(){
    HashTable hT;  
    ElemType e; 
    KeyType key;
    InitHashTable(&hT);

    e.key = 2134;  e.score = 10.5;   
    InsertHashTable(&hT,e.key, e);

    e.key = 34;   e.score = 20.5;  
    InsertHashTable(&hT, e.key, e);

    e.key = 25;   e.score = 30.5;  
    InsertHashTable(&hT, e.key, e);

    key = 20;
    if (FindHashTable(hT, key, &e)==OK) 
      printf("%f\n", e.score);
    else 
      printf("can't find the key:%d\n", key);

    key = 25;
    if (FindHashTable(hT, key, &e)==OK) 
       printf("the value of key%d is:%f\n",key, e.score);
    else 
      printf("can't find the key%d\n", key);
}


int main(){
  HashTable_test();
  return 0;
}
```

C++引用版本
```cpp
// copyright by hwdong
#include <stdio.h>
#include <stdlib.h>
#define SIZE 119
typedef int KeyType;
typedef struct{
  KeyType key;
  double score;
}ElemType;

typedef struct h_lnode{
  ElemType data;
  struct h_lnode *next;
}HLNode;

typedef struct{
// int *array = (int *) malloc(100 * sizeof(int))
  HLNode* *table; // HLNode*  table[100]
  int size;
}HashTable;

bool InitHashTable( HashTable &hashT){
  hashT.table = (HLNode* *)                malloc(SIZE*sizeof(HLNode*));
  if (!hashT.table) return false;

  hashT.size = SIZE;
  for (int i = 0; i < hashT.size; i++)
      hashT.table[i] = 0;
  return true;
}

int  Hash(KeyType key){ return key%SIZE;}

bool InsertHashTable( HashTable &hashT,                       KeyType key, ElemType e){
  HLNode* s = (HLNode* )malloc(sizeof(HLNode));
  s->data = e;

  int hash_address = Hash(key);

//新结点插入在hashT.table[hash_address]所指示的链表的最前面
  s->next = hashT.table[hash_address]; 
  hashT.table[hash_address] = s;
  return true;
}


bool FindHashTable( HashTable &hashT,                    KeyType key, ElemType &e){
  int hash_address = Hash(key);

  HLNode* p = hashT.table[hash_address];
  while (p){
    if (p->data.key == key) {
       e = p->data;return true;
    }
    p = p->next;
  }
  return false;
}

void HashTable_test(){
    HashTable hT;  ElemType e; KeyType key;
    InitHashTable(hT);
    e.key = 2134;  e.score = 10.5;   InsertHashTable(hT,e.key, e);
    e.key = 34;   e.score = 20.5;  InsertHashTable(hT, e.key, e);
    e.key = 25;   e.score = 30.5;  InsertHashTable(hT, e.key, e);

    key = 20;
    if (FindHashTable(hT, key, e)) printf("%f\n", e.score);
    else printf("can't find the key:%d\n", key);
    key = 25;
   if (FindHashTable(hT, key, e)) printf("the value of key%d is:%f\n",key, e.score);
   else printf("can't find the key%d\n", key);
}


int main(){
  HashTable_test();
  return 0;
}
```
