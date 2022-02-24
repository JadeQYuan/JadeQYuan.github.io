title: Spring 源码
categories:
  - Java
  - 源码
description: Spring 源码
author: Jade
date: 2022-02-04 16:00:00
---

## 相关组件
- BeanDefinition，保存表示Bean的配置元信息。
- BeanDefinitionReader，从各个配置收集BeanDefinition，如XML、注解等。
- BeanDefinitionRegistry，保存BeanDefinition的地方。
- BeanFactoryPostProcessor，对BeanDefinition进行一定程序上的修改和替换（如占位符）。
- BeanWrapper，
- BeanFactory
- ApplicationContext
- Aware
- BeanPostProcessor

## Bean实例化过程
### 容器启动阶段
开始 -> BeanDefinitionReader（读取配置元信息） -> BeanDefinition -> BeanDefinitionRegistry（BeanFactoryPostProcessor） -> 结束

### Bean实例化阶段
开始 -> 原生Bean实例 -> BeanWrapper -> 检查Aware相关接口 -> BeanPostProcessor前置处理 -> InitializingBean/init-method -> BeanPostProcessor后置处理 -> DisposeBean/destroy-method -> 使用 -> 调用回调销毁接口 -> 结束
