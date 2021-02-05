用于学习 protobuf

- 利用 protoc 生成代码
```
protoc --proto_path=IMPORT_PATH --cpp_out=DST_DIR --java_out=DST_DIR --python_out=DST_DIR path/to/file.proto
```
IMPORT_PATH声明了一个.proto文件所在的具体目录。如果忽略该值，则使用当前目录。如果有多个目录则可以 对--proto_path 写多次，它们将会顺序的被访问并执行导入。-I=IMPORT_PATH是它的简化形式。

```
protoc -I=protobuf --python_out=./ protobuf/addressbook.proto
```
- 运行 `write_test.py`，新建对象，并序列化到文件中
- 运行 `read_test.py`，从文件中读取反序列化读取数据


## 其他学习
在消息定义中，每个字段都有唯一的一个数字标识符。这些标识符是用来在消息的二进制格式中识别各个字段的，一旦开始使用就不能够再改变。
optional：消息格式中该字段可以有0个或1个值（不超过1个）。
repeated：在一个格式良好的消息中，这种字段可以重复任意多次（包括0次）。重复的值的顺序会被保留。表示该值可以重复，相当于java中的List。由于一些历史原因，基本数值类型的repeated的字段并没有被尽可能地高效编码。在新的代码中，用户应该使用特殊选项[packed=true]来保证更高效的编码。
Python编译器为.proto文件中的每个消息类型生成一个含有静态描述符的模块，，该模块与一个元类（metaclass）在运行时（runtime）被用来创建所需的Python数据访问类。
消息描述中的一个元素可以被标记为“可选的”（optional）。一个格式良好的消息可以包含0个或一个optional的元素。当解 析消息时，如果它不包含optional的元素值，那么解析出来的对象中的对应字段就被置为默认值。默认值可以在消息描述文件中指定。
如果没有为optional的元素指定默认值，就会使用与特定类型相关的默认值：对string来说，默认值是空字符串。对bool来说，默认值是false。对数值类型来说，默认值是0。对枚举来说，默认值是枚举类型定义中的第一个值。
对于 Python，这个包声明符是被忽略的，因为Python模块是按照其在文件系统中的位置进行组织的。




**参考**
- [https://github.com/menghaocheng/hello_protobuf](https://github.com/menghaocheng/hello_protobuf)
- [https://blog.csdn.net/menghaocheng/article/details/80176763](https://blog.csdn.net/menghaocheng/article/details/80176763)
- [https://colobu.com/2015/01/07/Protobuf-language-guide/](https://colobu.com/2015/01/07/Protobuf-language-guide/)