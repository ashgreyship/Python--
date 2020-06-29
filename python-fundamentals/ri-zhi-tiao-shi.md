# 日志调试

## 日志调试:

```python
#日志调试
import logging
logging.debug('this is debug')
logging.info('this is info')
logging.warning('this is warning')
logging.error('this is error')
logging.critical('this is critical')

#将日志打印到文件中
import logging

logging.basicConfig(level=logging.DEBUG,filename='log.log',filemode='a')
logging.debug('this is debug')
logging.info('this is info')
logging.warning('this is warning')
logging.warning(time.strftime('%y-%m-%d'))
logging.error('this is error')
logging.critical('this is critical')

```

