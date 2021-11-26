描述文件状态的对象。<br />

# 属性

### String mode
文件的类型和存取的权限，对应 POSIX stat.st_mode。

### Number size
文件大小，单位：B，对应 POSIX stat.st_size。

### Number lastAccessedTime
文件最近一次被存取或被执行的时间，UNIX 时间戳，对应 POSIX stat.st_atime。

### Number lastModifiedTime
文件最后一次被修改的时间，UNIX 时间戳，对应 POSIX stat.st_mtime。

## 方法
[Stats.isDirectory](https://opendocs.alipay.com/mini/api/022b6t) 判断当前文件是否一个目录。

[Stats.isFile](https://opendocs.alipay.com/mini/api/022b6u) 判断当前文件是否一个普通文件。
