# php

# 源码地址
https://github.com/chuan-yun/Molten

# 针对于穿云编译部署
./configure --with-php-config=php-config --enable-level-id

# 设置扩展信息(php.ini)
extension=molten.so 
molten.enable=1 
molten.sink_log_path=/var/wd/log/tracing/php/ 
molten.sampling_rate=1 //设置sampling 
