title: Mockito
categories:
  - Java
  - UT
description: Mockito
author: Jade
date: 2022-07-01 22:00:00
---

## Mockito
- when
- doReturn
- doNothing
- thenThrowing
- any
- anyString

## Mock Spy
- Mock 返回数据类型的默认值。
- Spy 除打桩方法外，执行原对象的方法。

## @Mock Mock
- Mock需每次创建。
- @Mock可直接使用。

## @Mock @MockBean
- @Mock生成的对象不由spring管理。
- @MockBean生成的对象由spring管理，相当于自动替换相应类型的bean。

## doReturn().when() when().thenReturn
- when().thenReturn() 会执行方法并产生结果，并返回指定的结果。
- doReturn().when() 不执行方法，直接返回结果。

## junit4 junit5
- org.junit.*  org.junit.jupiter.api.*

## @SpringBootTest @RunWith
- @SpringBootTest 使用Spring上下文。
- @RunWith

## Q&A
- Test中注入ServiceA，可以使用@SpyBean注解依赖的ServiceB，但无法使用@SpyBean注解对应的MapperA。（使用@MockBean并指定name属性为MapperA的beanName）
