# Environment

## 作用

- 仿真时间
- 事件的调度和处理

## 仿真控制

- 结束条件
	- 没有更多事件
	- 定时结束
	- 特定事件被触发
-  运行方式
	- 逐步
	- 混合
- run 方法
	- 参数
		- 不传参数
		- 过期时间
		- 传递事件
			- timeout
			- 其他类型的事件
- peek 方法
	- 返回值
		- 下一个调度事件的时间
		- 如果没有调度事件返回 infinity
- step 方法
	- 作用
		- 下一调度事件
	- 异常
		- 如果没有可用的事件抛出 EmptySchedule 异常

## 状态获取

- 当前仿真时间
	- 默认从 0 开始
	- 数字但不带单位
	- 可以通过 Environment.now 获取
- active 状态
	- 进程函数正在被执行时处于 active 状态
	- 进程函数挂起等待时处于 inactive 状态
	- 可以通过 Environment.active_process 获取
		- 要么返回 None
		- 要么指向当前 active 的进程

## 事件创建

- 快捷方式
	- Environment.event()
	- Environment.process()
	- Environment.timeout()
	- Environment.all_of()
	- Environment.any_of()