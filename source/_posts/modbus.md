title: modbus
categories: []
tags:
  - How/Why
description: modbus
author: Jade
date: 2021-06-03 15:14:00
---
# modbus
> How/Why

## modbus
1. 串行通信协议

### 变种
- modbus ASCII
- modbus RTU
	使用RS232/RS485接口
- modbus TCP
	使用RJ45接口

### 架构
master/slave


代码	中文名称	英文名	位操作/字操作	操作数量
01	读线圈状态	READ COIL STATUS	位操作	单个或多个
02	读离散输入状态	READ INPUT STATUS	位操作	单个或多个
03	读保持寄存器	READ HOLDING REGISTER	字操作	单个或多个
04	读输入寄存器	READ INPUT REGISTER	字操作	单个或多个
05	写线圈状态	WRITE SINGLE COIL	位操作	单个
06	写单个保持寄存器	WRITE SINGLE REGISTER	字操作	单个
15	写多个线圈	WRITE MULTIPLE COIL	位操作	多个
16	写多个保持寄存器	WRITE MULTIPLE REGISTER	字操作	多个


<p style="text-align: center"><strong>END</strong></p>