---
aliases:
  - set
  - 设定参数
  - 参数
  - Linux 命令
  - shell 指令
date: 2024-12-15
---

# 用法

set 命令为 shell 设定参数变量。许多命令的输出是以空格分隔的值，如果要使用其中的某个数据域，使用 set 非常有效。

```
#!/bin/sh  
echo the date is $(date)  
set $(date)  
echo the month is $2  
输出：  
the date is Wed Apr 23 15:34:16 CST 2014  
the month is Apr

将 date 命令的输出设置为参数表，再通过位置参数 $2 取得月份。
```

> [!note] 参考资料
> [Shell 中的set --用法 - 滴滴滴 - 博客园](https://www.cnblogs.com/gaoyuechen/p/14336063.html)

# set -eou

在 Shell 脚本中，`set -euo pipefail` 是一组用于增强脚本健壮性和安全性的命令选项组合。它通过严格限制脚本的执行行为，帮助开发者更早发现错误。以下是逐项解释：

---

## 选项分解
```bash
set -e    # 等同于 set -o errexit
set -u    # 等同于 set -o nounset
set -o pipefail
```

---

## 1. `set -e` (错误时退出)
- **作用**：当任何命令以非零状态退出时，立即终止脚本执行
- **使用场景**：避免错误积累（例如：文件不存在时继续操作可能引发更严重问题）
- **示例**：
  ```bash
  # 未启用 -e 的情况
  rm non_existent_file.txt  # 此命令失败（返回非零状态码）
  echo "继续执行"            # 仍然会执行

  # 启用 -e 的情况
  set -e
  rm non_existent_file.txt  # 失败后脚本立即终止
  echo "这行不会执行"
  ```

---

## 2. `set -u` (禁止未定义变量)
- **作用**：当使用未定义的变量时，触发错误并终止脚本
- **使用场景**：防止变量名拼写错误导致的意外行为
- **示例**：
  ```bash
  # 未启用 -u 的情况
  echo "$undef_var"   # 输出空行，无报错
  echo "继续执行"

  # 启用 -u 的情况
  set -u
  echo "$undef_var"   # 报错：unbound variable
  echo "这行不会执行"
  ```
- **安全用法**：
  ```bash
  # 使用默认值避免报错
  echo "${undef_var:-默认值}"
  ```

---

## 3. `set -o pipefail` (管道错误检测)
- **作用**：管道命令中任意一个子命令失败，整个管道返回非零状态码
- **默认行为**：仅最后一个命令的退出码决定管道结果
- **示例**：
  ```bash
  # 默认管道行为
  ls non_existent_file.txt | sort  # ls失败（返回2），但sort成功（返回0）
  echo $?                          # 输出0（错误被掩盖）

  # 启用 pipefail
  set -o pipefail
  ls non_existent_file.txt | sort  # 整个管道返回2
  echo $?                          # 输出2
  ```

---

## 组合效果
当同时使用这三个选项时：
```bash
set -euo pipefail
```
脚本会具有以下行为：
1. **严格错误检查**：任何命令失败或使用未定义变量立即终止脚本
2. **精确错误定位**：管道中任意环节失败都会被捕获
3. **防御性编程**：强制开发者处理变量初始化和错误流

---

## 最佳实践
### 脚本模板
```bash
#!/bin/bash
set -euo pipefail
# 确保在脚本开头设置
# 后续代码必须处理所有可能的失败路径
```

### 临时禁用选项
```bash
set +e      # 临时禁用 -e
dangerous_command || true
set -e      # 重新启用
```

### 错误处理
```bash
# 捕获错误并自定义处理
if ! some_command; then
  echo "优雅处理错误"
  exit 1
fi
```

---

## 注意事项
| 场景 | 处理方案 |
|------|----------|
| 故意忽略错误 | 使用 `command || true` |
| 可选文件操作 | 先检查文件存在性 `[ -f file ] && rm file` |
| 外部命令状态码 | 提前了解命令的退出码含义 |

---

## 调试技巧
```bash
# 显示执行过程（与严格模式结合使用）
set -exuo pipefail

# 检查变量赋值
echo "变量值: ${MY_VAR}"
```

通过 `set -euo pipefail`，Shell 脚本的可靠性和可维护性将显著提升，特别适合用于生产环境中的关键任务脚本。