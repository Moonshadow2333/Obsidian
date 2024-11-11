# SimPy 

## 基本概念

- Environment
	- 存储事件
	- 跟踪当前仿真时间
- event
	- 存储
		- 优先级
		- 仿真时间
		- 自增事件 id
	-  callbacks
		- 执行时机
			- 事件被触发
			- event is processed by event loop
	- 返回值
- process
	- 作用
		- 实现仿真模型
	- 是什么	
		- 生成事件实例的普通生成器函数
	- 事件生成
		- 生成事件，process 生成事件
		- 挂起等待，process 被添加到事件回调中并被挂起
		- 进程恢复，process 恢复时，将会收到事件的返回值
	- 进程启动
		- 调用进程函数
		- 创建进程实例