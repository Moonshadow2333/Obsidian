# Event

## 是什么？

- 拓展
- 资源

## 事件层级

- 所有的事件都继承自 simpy.events.Event
- 层级
	- events.Event
		- events.Timeout
		- events.Initialize
		- events.Process
		- events.Condition
			- events.AllOf
			- events.AnyOf

## 事件基础

- 事件状态
	- 可能发生（未触发）
	- 打算发生（已触发）
	- 已经发生（已处理）
- 过程
	- 一开始，事件未触发并且仅仅是内存中的对象
	- 事件被触发
		- 在给定的时间被调度
		- 被添加到事件队列
		- Event.triggered 属性变为 true
		- 事件的状态未变为已处理前，可以给事件添加 callbacks
			- callbacks 是接收事件作为参数的 callables
			- callbacks 被存储在 Event.callbacks 列表中
	- 事件已处理
		- 从事件队列中出队
		- 调用所有的 callbacks
		- 不能再添加 callbacks
		- Event.processed 属性变为 true
- 事件的值
	- 设置时机
		- 事件触发前
		- 事件触发时
	- 获取方法
		- 通过 Event.value 属性
		- 在进程内，通过生成事件（value = yield event)
- 向事件中添加 callbacks
	- 最常见的方式
		- 在进程内生成事件（yield event）
	- envent.callbacks.append 方法
		- 可以添加任何 callable 对象（方法）到 callbacks 列表中
		- callable 对象（方法）接收事件实例作为它的单一参数
	- Event.callbacks
		- 事件已处理时会执行所有的 callbacks
		- Event.callbacks 会被设置为 None
- 触发事件
	- 事件结果
		- 成功
		- 失败
	- 触发方法
		- Event.succeed 方法
			- 触发事件并标记为成功
			- 参数非必传
		- Event.fail 方法
			- 触发事件并标记为失败
			- 参数
				- 异常实例
		- Event.trigger 方法
			- 更加通用的方式
		- 以上三种方式的返回值
			- 绑定的事件实例
## Timeout

- 参数
	- dealy
	- 可选值
- 触发时机
	- now + delay

##  Processes 也是事件

-  进程可以生成另外一个进程
- 其他进程结束时恢复
- 事件的值将会是进程的返回值
- simpy.until.start_delayed 方法
	- 作用 
		- 在一个特定的 delay 后启动进程
	- 返回值
		-  a helper process
	- 注意
		- 使用两次 yield

## 等待多个事件

- AnyOf
	- 场景
		- 在有限的事件内等一个资源
	- 参数
		- 事件列表
	- 触发
		- 事件列表中的任意一个事件被触发
- AllOf
	- 场景
		- 等一系列的事件发生
	- 参数
		- 事件列表
	- 触发
		- 事件列表中的所有事件被触发
- 返回值
	- 有序字典
	- 长度
		- AllOf
			- 和事件列表等长
		- AnyOf
			- 至少有一个条目