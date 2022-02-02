# Pytest

````bash
# 安装主程序包
pip install pytest

# 安装多线程包
pip install pytest-xdist

# 安装HTML报告包
pip install pytest-html
`````

### pytest.ini

```bash
[pytest]
markers =
    slow
    fast
    normal

# 需要自动检查的文件前缀后缀名
python_files = Test_* test_* *_Test *_test
python_classes = Test_* test_* *_Test *_test
python_functions = Test_* test_* *_Test *_test
```
