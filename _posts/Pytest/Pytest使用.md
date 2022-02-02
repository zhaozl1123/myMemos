# Pytest

#### 通过对configService服务进行接口测试的过程说明pytest的使用方法

````bash
# configService接口服务及测试用例的文件结构
F:.   
├─app_configService
│  │  Publish_configService.py
│  │  __init__.py
│  │  
│  └─apps
│      │  __init__.py
│      │  
│      └─v1
│              Method_configDefine.py
│              Service_configDefine.py
│              __init__.py
└─test_configService
        params4ConfigService.py
        pytest.ini
        report.html
        test_configService.py
`````

### pytest.ini

```bash
[pytest]
log_cli = 1  # 是否使用cli输出log
log_cli_level = INFO  # with options: CRITICAL WARNING DEBUG INFO NOTSET
log_cli_format = %(asctime)s %(filename)s:%(lineno)s [%(levelname)8s] : %(message)s  # log的内容格式
log_cli_date_format = %Y-%m-%d %H:%M:%S  # log的时间格式

markers =
    marker1  # marker
    marker2

python_files = Test_* test_* *_Test *_test
python_classes = Test_* test_* *_Test *_test
python_functions = Test_* test_* *_Test *_test
```

#### 对pytest.ini文件中日志参数的说明

```ini
# disable printing caught logs on failed tests.
--no-print-logs
# logging level used by the logging module
--log-level=LOG_LEVEL
# log format as used by the logging module.
--log-format=LOG_FORMAT
# log date format as used by the logging module.
--log-date-format=LOG_DATE_FORMAT  
# cli logging level.
--log-cli-level=LOG_CLI_LEVEL  
# log format as used by the logging module.
--log-cli-format=LOG_CLI_FORMAT  
# log date format as used by the logging module.
--log-cli-date-format=LOG_CLI_DATE_FORMAT  
# path to a file when logging will be written to.
--log-file=LOG_FILE  
# log file logging level.
--log-file-level=LOG_FILE_LEVEL  
# log format as used by the logging module.
--log-file-format=LOG_FILE_FORMAT  
# log date format as used by the logging module.
--log-file-date-format=LOG_FILE_DATE_FORMAT  
```

对test_XXX.py文件中，log的说明

```python
import logging

log = logging.getLogger(__name__)

def func():
	log.error(f"{_testTargetName}不在可选项中,参考:[mysql, mqtt, minio, storage, uhf]")
    log.info(f"向configService[PUT]发出{_testTargetName}参数设置请求")
```

#### 输出html测试报告

```shell
# 需要安装pytest-html
# 在bash中，使用以下命令开启测试，并输出测试结果到html文件
pytest /
--html=report.html /  # 开启测试结果向html文件的存储
--self-contained-html /  # 将CSS写入html中
--capture sys  # 存入html的测试结果不仅包含测试内容，还包含sys输出，包括log、print（stdout）
```

