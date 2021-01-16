背景
	后端： spring boot + websocket
	前端： vue + websocket + stomp
	
心跳配置
	后端： [n1, n2]
		n1表示 后端给前端发送ping的间隔
		n2表示 前端应该给后端发送ping的间隔
	前端： [m1, m2]
		m1表示 前端发送给后端ping的间隔
		m2表示 前端检查后端消息发送的间隔
		
心跳frame
	心跳帧的数据为 0x0A(\n)
	
解释
	心跳要客户端和服务端都要接收和发送数据，否则心跳不能维持，必须保证四个数字都不能为0。
	前端发送ping，间隔取 n2,m1 最大值，打印为ping
	后端定时器间隔取 n1,n2 最小值，读间隔取 m1,n2 最大值 乘3, 写间隔取 m2, n1 最大值，定时器执行，lastWriteTime为上次发送消息的时间（只有发送Message才会更新），lastReadTime为接收消息的时间
	前端检验间隔取 n1,m2 最大值
	前端接收后端发送心跳，打印为pong