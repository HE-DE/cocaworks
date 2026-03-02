# C++ 代码质量规范

## 1. 代码风格

### 1.1 缩进与格式

- 使用空格进行缩进，缩进宽度为 4 个空格
- 大括号采用 `Allman` 风格（左大括号单独一行）
- 运算符前后保留空格
- 逗号后保留一个空格

```cpp
// 正确示例
void Function(int param1, int param2)
{
    if (condition)
    {
        DoSomething();
    }
    else
    {
        DoOtherThing();
    }
}

// 错误示例
void Function(int param1,int param2){
    if(condition){
        DoSomething();
    }else{
        DoOtherThing();
    }
}
```

### 1.2 行长度

- 单行代码不超过 100 个字符
- 超过限制时合理换行

### 1.3 头文件

- 头文件使用 `#pragma once` 或 `#define` 防止重复包含
- 包含头文件时按以下顺序：相关头文件 → C 标准库 → C++ 标准库 → 第三方库 → 项目头文件
- 使用路径按从短到长排序

---

## 2. 命名规范

### 2.1 通用规则

- 使用有意义的英文单词或词组
- 避免使用缩写，除非是广泛认可的缩写（如 `num`、`info`、`usr`）
- 不使用下划线开头或结尾的命名

### 2.2 具体命名

| 类型 | 命名规则 | 示例 |
|------|----------|------|
| 变量 | 驼峰命名法 | `int userCount;` |
| 常量 | 全部大写，下划线分隔 | `const int MAX_BUFFER_SIZE = 1024;` |
| 函数 | 驼峰命名法，首字母大写 | `void ProcessData();` |
| 类 | 帕斯卡命名法 | `class UserManager {}` |
| 枚举 | 帕斯卡命名法 | `enum class ErrorCode { Success, Failed };` |
| 命名空间 | 全部小写 | `namespace network {}` |
| 成员变量 | 驼峰命名法，可加后缀 `_` | `int userCount_;` 或 `int userCount;` |

---

## 3. 注释规范

### 3.1 文件头注释

```cpp
/**
 * @file filename.h
 * @brief 简要描述文件功能
 * @author 作者名
 * @date 2024-01-01
 */
```

### 3.2 函数注释

```cpp
/**
 * @brief 函数功能简述
 * @param param1 参数1说明
 * @param param2 参数2说明
 * @return 返回值说明
 */
```

### 3.3 代码注释

- 复杂逻辑必须添加注释说明
- 注释应解释「为什么」，而不是「是什么」
- 保持注释与代码同步更新
- TODO 注释格式：`// TODO(用户名): 待办事项`

---

## 4. 函数设计

### 4.1 函数原则

- 单一职责：每个函数只完成一件事
- 参数不宜过多，建议不超过 5 个
- 优先使用返回值而非输出参数
- 避免函数副作用过大

### 4.2 函数长度

- 函数体代码行数建议不超过 50 行
- 超过时应考虑拆分为多个子函数

### 4.3 参数传递

- 简单类型按值传递
- 类类型优先按引用传递
- 不修改的参数使用 `const` 引用

```cpp
void Process(const std::string& name, int value);  // 推荐
void Process(std::string name, int value);          // 不推荐
```

---

## 5. 类设计

### 5.1 类成员顺序

```cpp
class ClassName
{
public:        // 公共成员
    ClassName();
    ~ClassName();

    void PublicMethod();

protected:     // 保护成员
    void ProtectedMethod();

private:       // 私有成员
    void PrivateMethod();
    int member_;
};
```

### 5.2 构造函数

- 使用初始化列表代替赋值
- 禁止在构造函数中抛出异常

### 5.3 析构函数

- 基类析构函数应声明为 `virtual`
- RAII 原则：资源在构造函数中获得，析构函数中释放

### 5.4 拷贝与移动

- 遵循三/五法则
- 禁止不需要拷贝的类生成拷贝构造和拷贝赋值

```cpp
class NonCopyable
{
public:
    NonCopyable() = default;
    NonCopyable(const NonCopyable&) = delete;
    NonCopyable& operator=(const NonCopyable&) = delete;
};
```

---

## 6. 内存管理

### 6.1 智能指针

- 优先使用智能指针，避免裸指针
- 使用 `std::unique_ptr` 管理独占所有权
- 使用 `std::shared_ptr` 共享所有权
- 避免循环引用

```cpp
auto ptr = std::make_unique<Resource>();
auto shared = std::make_shared<Resource>();
```

### 6.2 资源管理

- 使用 RAII 模式管理资源
- 避免使用 `malloc`/`free`，使用 `new`/`delete` 或智能指针
- 禁止使用 `realloc`

---

## 7. 错误处理

### 7.1 异常处理

- 使用异常处理错误情况
- 异常应有明确的类型和消息
- 捕获异常时使用引用而非值

```cpp
try
{
    Process();
}
catch (const std::exception& e)
{
    LogError(e.what());
}
```

### 7.2 返回值

- 对于可恢复错误，可使用错误码
- 使用 `std::optional` 表示可能不存在的值
- 使用 `std::pair` 或结构体返回多个值

---

## 8. 性能考虑

### 8.1 优化原则

- 先保证正确性，再进行优化
- 避免不必要的拷贝
- 使用 `const` 和 `constexpr` 适当标记

### 8.2 容器使用

- 使用 `reserve()` 预分配容器容量
- 遍历容器时使用引用避免拷贝
- 优先使用范围 `for` 循环

```cpp
std::vector<int> vec;
vec.reserve(100);

for (const auto& item : vec)
{
    Process(item);
}
```

### 8.3 字符串操作

- 使用 `std::string_view` 避免字符串拷贝
- 频繁字符串拼接使用 `std::stringstream` 或 `fmt`

---

## 9. 测试要求

### 9.1 单元测试

- 每个类至少有一个对应的测试类
- 测试函数命名：`TEST(ClassName, MethodName)`
- 测试应覆盖正常情况和边界情况

### 9.2 测试原则

- 保持测试独立性和可重复性
- 测试代码同样遵循代码规范
- 自动化运行测试

---

## 10. 代码审查

### 10.1 审查要点

- 代码逻辑正确性
- 命名是否清晰
- 是否有内存泄漏风险
- 错误处理是否完善
- 性能是否有明显问题

### 10.2 审查标准

- 禁止提交编译警告的代码
- 禁止提交未通过测试的代码
- 代码风格必须统一
- 注释完整且准确

---

## 11. 其他建议

### 11.1 编码安全

- 禁止使用 `strcpy`、`sprintf` 等不安全函数
- 使用 `std::string`、`std::string_view` 替代 C 风格字符串
- 防止整数溢出

### 11.2 日志规范

- 合理使用日志级别
- 日志信息简洁明了
- 避免在日志中输出敏感信息

### 11.3 常量定义

- 使用 `constexpr` 定义编译时常量
- 避免使用宏定义常量
- 使用枚举类代替整型常量
