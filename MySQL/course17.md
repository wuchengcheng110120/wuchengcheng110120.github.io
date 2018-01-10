## [上一页](course16)
## MySQL调优策略

1 、 硬件层相关优化

修改服务器BIOS设置：

- 选择Performance Per Watt Optimized（DAPC）模式，发挥CPU 最大性能

- Memory Frequency（内存频率）选择 Maximum Performance（最佳性能）

- 内存设置菜单中，启用Node interleaving ，避免NUMA问题

2、 磁盘I/O相关

- 使用SSD硬盘

- 如果是磁盘阵列储存，建议阵列卡同时配置CACHE及BBU模块，可明显提升IOPS

- raid级别尽量选择raid10，而不是raid5

3、 文件系统层优化

- 使用deadline/noop 这两种I/O调度器，千万别用cfq

- 使用xfs文件系统，千万别用ext3，ext4勉强可用，但业务量很大的话，则一定要用xfs；

- 文件系统momunt参数中增加：noatime、nodiratime，nobarrier几个选项（nobarrier是xfs文件系统特有的）

4、 内核参数优化

- 修改 vm、swappiness参数（5-10），降低swap使用率，RHEL7/contos7以上慎用设置为0，可能发生OOM

- 调整 vm.dirty 、background ratio（%10）、 vm.dirty ratio（5%） 内核参数，以确保能持续将脏数据刷新到磁盘，避免瞬间I/O写，产生等待

- 调整 net.ipv4.tcp_tw-recycle、net.ipv4.tcp_tw_reuse 都设置为1，减少TIME_WAIT，提高TCP效率

5、 MySQL参数优化建议

- 建议设置default-storage-engine=innoDB，强烈建议不要再使用MyISAM引擎。

- 调整innodb_buffer_pool_size的大小，如果是但实力且绝大多数是InnoDB引擎表的话，可以考虑设置为物理内存的50%-70&左右。

- 设置Innodb_file_per_table = 1 ,使用独立表空间

- 调整Innodb_data_file_path = ibdata1:1G:autoextend,不要用默认的10M，在高并发场景下，性能会有很大提升

- 设置innodb_log_file_size = 256M,设置innodb_log_files_in_group=2,基本可以满足大多数应用场景

- 调整max_connection(最大连接数)、max_connnection_error(最大错误数)设置，根据业务量大小进行设置

- 另外，open_files_limit、innodb_open_files、table_open_cache、table_definition_cache可以设置大约为max_connection的10倍大小左右

- key_buffer_size建议调小，32M即可，另外建议关闭query cache

- mp_table_size和max_heap_table_size设置不要过大，另外sort_buffer_size、join_buffer_size、read_buffer_size、read_rnd_buffer_size等设置也不要过大






## [返回目录](https://wuchengcheng110120.github.io/MySQL/learnMySQL)
## [下一页](course18)
