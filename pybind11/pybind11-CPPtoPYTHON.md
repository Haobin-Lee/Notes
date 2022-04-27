# pybind11 使用文档

## First Test Program

```C++
#include <pybind11/pybind11.h>

int add(int i, int j) {
    return i + j;
}

//expose C++ code to python
//import example
PYBIND11_MODULE(example, m) {//`m` 是 `py::module_`类型，用来创建绑定关系
    m.doc() = "pybind11 example plugin"; // optional module docstring

    //`module_::def()`将C++代码中`add()`函数暴露给python
    m.def("add1", &add, "A function that adds two numbers");

    //也可以指定参数名称
    m.def("add2", &add, "A function which adds two numbers",
      py::arg("i"), py::arg("j"));

    //指定文字参数,_a和arg功能一样
    using namespace pybind11::literals;
    m.def("add3", &add, "i"_a, "j"_a);

    //`module::attr()`将C++ value暴露给python
    m.attr("the_answer") = 42;
    //通过`py::cast`可以转换value类型
    py::object world = py::cast("World");
    m.attr("what") = world;
}
```

build之后，会产生一个二进制module文件，这个module可以通过 python 命令行 import
（可能要将当前项目路径添加到PYTHONPATH中，因为exe文件可能和py文件不在同一级目录下 `export PYTHONPATH="项目根目录路径"`）

```shell
$ python
Python 3.9.10 (main, Jan 15 2022, 11:48:04)
[Clang 13.0.0 (clang-1300.0.29.3)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> import example
>>> example.add1(1, 2)
3
>>>example.add2(i=1, j=2)
3L
>>>
```
