GETCWD = 17,
EVENTFD = 19,
EPOLL_CREATE = 20,
EPOLL_CTL = 21,
EPOLL_PWAIT = 22,
DUP = 23,
DUP3 = 24,
FCNTL64 = 25,
IOCTL = 29,
MKDIRAT = 34,
SYMLINKAT = 36,
UNLINKAT = 35,
LINKAT = 37,
RENAMEAT = 38,
UNMOUNT = 39,
MOUNT = 40,
STATFS = 43,
FTRUNCATE64 = 46,
FACCESSAT = 48,
CHDIR = 49,
FCHMODAT = 53,
FCHOWN = 54,
OPENAT = 56,
CLOSE = 57,
PIPE2 = 59,
GETDENTS64 = 61,
LSEEK = 62,
READ = 63,
WRITE = 64,
READV = 65,
WRITEV = 66,
PPOLL = 73,
FSTATAT = 79,
PREAD64 = 67,
PWRITE64 = 68,
SENDFILE64 = 71,
PSELECT6 = 72,
PREADLINKAT = 78,
FSTAT = 80,
SYNC = 81,
FSYNC = 82,
UTIMENSAT = 88,
RENAMEAT2 = 276,
COPYFILERANGE = 285,
STATX = 291,
PIDFD_OPEN = 434,



// x86_64
OPEN = 2,
STAT = 4,
EVENTFD = 284,
EVENTFD2 = 290,
GETCWD = 79,
UNLINK = 87,
EPOLL_CREATE = 213,
EPOLL_CTL = 233,
EPOLL_WAIT = 232,
DUP = 32,
DUP2 = 33,
DUP3 = 292,
FCNTL64 = 72,
IOCTL = 16,
MKDIRAT = 258,
SYMLINKAT = 266,
RENAME = 82,
MKDIR = 83,
RMDIR = 84,
UNLINKAT = 263,
LINKAT = 265,
UNMOUNT = 166,
MOUNT = 165,
STATFS = 137,
FTRUNCATE64 = 77,
FACCESSAT = 269,
ACCESS = 21,
CHDIR = 80,
FCHMODAT = 268,
OPENAT = 257,
CLOSE = 3,
PIPE = 22,
PIPE2 = 293,
GETDENTS64 = 217,
LSEEK = 8,
READ = 0,
WRITE = 1,
READV = 19,
WRITEV = 20,
PPOLL = 271,
POLL = 7,
CREAT = 85,
FSTATAT = 262,
PREAD64 = 17,
PWRITE64 = 18,
SENDFILE64 = 40,
SELECT = 23,
PSELECT6 = 270,
READLINK = 89,
CHMOD = 90,
PREADLINKAT = 267,
FSTAT = 5,
LSTAT = 6,
SYNC = 162,
FSYNC = 74,
UTIMENSAT = 280,
RENAMEAT = 264,
RENAMEAT2 = 316,
COPYFILERANGE = 326,
EPOLL_CREATE1 = 291,
EPOLL_PWAIT = 281,
STATX = 332,
CHOWN = 92,
MKNOD = 259,
FCHOWN = 93,
PIDFD_OPEN = 434,




GETCWD
EVENTFD
EPOLL_CREATE
EPOLL_CTL
EPOLL_PWAIT
DUP
DUP3
FCNTL64
IOCTL
MKDIRAT
SYMLINKAT
UNLINKAT
LINKAT
RENAMEAT
UNMOUNT
MOUNT
STATFS
FTRUNCATE64
FACCESSAT
CHDIR
FCHMODAT
FCHOWN
OPENAT
CLOSE
PIPE2
GETDENTS64
LSEEK
READ
WRITE
READV
WRITEV
PPOLL
FSTATAT
PREAD64
PWRITE64
SENDFILE64
PSELECT6
PREADLINKAT
FSTAT
SYNC
FSYNC
UTIMENSAT
RENAMEAT2
COPYFILERANGE
STATX
PIDFD_OPEN
OPEN
STAT
EVENTFD2
UNLINK
EPOLL_WAIT
DUP2
RENAME
MKDIR
RMDIR
ACCESS
PIPE
POLL
CREAT
SELECT
READLINK
CHMOD
LSTAT
EPOLL_CREATE1
CHOWN
MKNOD

---

### 1. **GETCWD**
**功能**: 获取当前工作目录的绝对路径。

**描述**: `getcwd` 系统调用用于获取调用进程的当前工作目录的绝对路径。它将路径存储在提供的缓冲区中。

**原型**:
```c
char *getcwd(char *buf, size_t size);
```

**参数**:
- `buf`: 指向存储路径的缓冲区。
- `size`: 缓冲区的大小。

**返回值**:
- 成功时返回 `buf` 指针。
- 失败时返回 `NULL`，并设置 `errno`。

**错误**:
- `EINVAL`: 缓冲区大小为0。
- `ERANGE`: 缓冲区不足以存储路径。

---

### 2. **EVENTFD**
**功能**: 创建一个事件文件描述符，用于事件通知和进程间同步。

**描述**: `eventfd` 提供了一种轻量级的机制，用于在用户空间实现事件通知。常用于多线程或多进程间的信号传递。

**原型**:
```c
int eventfd(unsigned int initval, int flags);
```

**参数**:
- `initval`: 初始化事件计数器的值。
- `flags`: 控制行为的标志（如 `EFD_NONBLOCK`, `EFD_SEMAPHORE`）。

**返回值**:
- 成功时返回一个新的文件描述符。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EAGAIN`: 非阻塞模式下资源暂时不可用。
- `EINVAL`: 参数无效。

---

### 3. **EPOLL_CREATE**
**功能**: 创建一个新的 `epoll` 实例，用于监控多个文件描述符的事件。

**描述**: `epoll_create` 用于创建一个 `epoll` 对象，该对象可以高效地监视大量文件描述符的事件。通常与 `epoll_ctl` 和 `epoll_wait` 一起使用。

**原型**:
```c
int epoll_create(int size);
```

**参数**:
- `size`: 提示内核预留的文件描述符数量。自 Linux 2.6.8 以后，这个参数已被忽略，但仍需要传递一个正整数。

**返回值**:
- 成功时返回一个新的 `epoll` 文件描述符。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EINVAL`: 参数无效。
- `ENOMEM`: 内存不足。

**注意**: 推荐使用 `epoll_create1`，因为它提供了更多的选项和更好的接口。

---

### 4. **EPOLL_CTL**
**功能**: 对 `epoll` 实例进行控制操作，如添加、修改或删除文件描述符。

**描述**: `epoll_ctl` 用于管理 `epoll` 实例中的文件描述符。可以添加新的文件描述符、修改现有文件描述符的事件或从监视列表中删除文件描述符。

**原型**:
```c
int epoll_ctl(int epfd, int op, int fd, struct epoll_event *event);
```

**参数**:
- `epfd`: `epoll` 实例的文件描述符。
- `op`: 操作类型（如 `EPOLL_CTL_ADD`, `EPOLL_CTL_MOD`, `EPOLL_CTL_DEL`）。
- `fd`: 要操作的文件描述符。
- `event`: 指向 `epoll_event` 结构的指针，定义感兴趣的事件。

**返回值**:
- 成功时返回 `0`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `ENOENT`: `epfd` 无效，或 `fd` 未被监视（对于 `MOD` 和 `DEL` 操作）。
- `EEXIST`: 对于 `ADD` 操作，`fd` 已经被监视。
- `ENOMEM`: 内存不足。

---

### 5. **EPOLL_PWAIT**
**功能**: 等待 `epoll` 实例中的事件，并支持信号掩码。

**描述**: `epoll_pwait` 类似于 `epoll_wait`，但它允许调用者在等待事件时临时更改信号掩码。这对于处理信号和事件的同步非常有用。

**原型**:
```c
int epoll_pwait(int epfd, struct epoll_event *events, int maxevents, int timeout, const sigset_t *sigmask);
```

**参数**:
- `epfd`: `epoll` 实例的文件描述符。
- `events`: 指向 `epoll_event` 结构数组的指针，用于存储触发的事件。
- `maxevents`: `events` 数组的大小。
- `timeout`: 等待的最长时间（毫秒）。`-1` 表示无限等待。
- `sigmask`: 指向信号掩码的指针，用于临时设置阻塞的信号。

**返回值**:
- 成功时返回触发的事件数量。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EINVAL`: 参数无效。
- `EINTR`: 调用被信号中断。
- `ENOMEM`: 内存不足。

---

### 6. **DUP**
**功能**: 复制一个文件描述符，返回新的文件描述符。

**描述**: `dup` 创建一个与给定文件描述符相同的新文件描述符。新文件描述符指向相同的文件表项，因此共享文件偏移量和状态标志。

**原型**:
```c
int dup(int oldfd);
```

**参数**:
- `oldfd`: 要复制的现有文件描述符。

**返回值**:
- 成功时返回新文件描述符。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EBADF`: `oldfd` 无效。
- `EMFILE`: 进程已打开的文件描述符数量达到限制。
- `ENOMEM`: 内存不足。

---

### 7. **DUP3**
**功能**: 复制一个文件描述符，并可以指定新描述符的标志。

**描述**: `dup3` 类似于 `dup2`，但允许在复制时设置文件描述符的标志，如 `O_CLOEXEC`。它避免了需要在复制后使用 `fcntl` 设置标志的情况。

**原型**:
```c
int dup3(int oldfd, int newfd, int flags);
```

**参数**:
- `oldfd`: 要复制的现有文件描述符。
- `newfd`: 指定的新文件描述符。如果 `newfd` 已打开，则 `dup3` 会先关闭它。
- `flags`: 文件描述符的标志（目前仅支持 `O_CLOEXEC`）。

**返回值**:
- 成功时返回新文件描述符。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EBADF`: `oldfd` 无效，或 `newfd` 无效。
- `EEXIST`: `newfd` 已打开，且未指定 `O_CLOEXEC`。
- `EINVAL`: 传递了无效的标志。
- `EMFILE`: 进程已打开的文件描述符数量达到限制。
- `ENOMEM`: 内存不足。

---

### 8. **FCNTL64**
**功能**: 对文件描述符执行各种控制操作，支持 64 位偏移。

**描述**: `fcntl64` 是 `fcntl` 的 64 位版本，主要用于支持大文件和特定的文件描述符控制操作。

**原型**:
```c
int fcntl64(int fd, int cmd, ... /* arg */ );
```

**参数**:
- `fd`: 要操作的文件描述符。
- `cmd`: 控制命令，如 `F_GETFL`, `F_SETFL`, `F_DUPFD`, `F_GETFD`, `F_SETFD`, 等。
- `arg`: 取决于 `cmd`，可能是一个整数或指针。

**返回值**:
- 成功时返回相应的值（如标志、文件描述符等）。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EBADF`: `fd` 无效。
- `EINVAL`: `cmd` 无效，或 `arg` 无效。
- `ENOMEM`: 内存不足。
- 其他根据具体命令而定。

**常见用途**:
- 获取或设置文件描述符的标志（如 `O_NONBLOCK`）。
- 复制文件描述符。
- 获取文件状态。

---

### 9. **IOCTL**
**功能**: 控制设备，提供与设备驱动程序的交互接口。

**描述**: `ioctl`（输入输出控制）系统调用用于设备控制命令的发送。这允许用户空间程序与设备驱动程序进行各种操作，如配置设备、获取设备状态等。

**原型**:
```c
int ioctl(int fd, unsigned long request, ...);
```

**参数**:
- `fd`: 设备文件的文件描述符。
- `request`: 控制命令，定义具体的操作。
- `...`: 可选参数，取决于 `request`。

**返回值**:
- 成功时返回特定值，通常为 `0`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EBADF`: `fd` 无效。
- `ENOTTY`: `fd` 不是一个终端设备，或者请求不适用于此设备。
- `EINVAL`: 请求无效，或者参数无效。
- `EFAULT`: 参数指针指向的内存不可访问。

**常见用途**:
- 设置串口参数。
- 控制网络设备。
- 获取或设置设备特定的属性。

**注意**: `ioctl` 的具体行为依赖于设备驱动程序和请求命令，因此使用时需要参考相应设备的文档。

---

### 10. **MKDIRAT**
**功能**: 在指定目录下创建一个新的目录。

**描述**: `mkdirat` 允许在给定的目录文件描述符下创建目录，支持相对路径和绝对路径。它是相对于指定目录的 `mkdir`。

**原型**:
```c
int mkdirat(int dirfd, const char *pathname, mode_t mode);
```

**参数**:
- `dirfd`: 参考目录的文件描述符。如果为 `AT_FDCWD`，则使用当前工作目录。
- `pathname`: 要创建的目录的路径。
- `mode`: 新目录的权限模式。

**返回值**:
- 成功时返回 `0`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EACCES`: 权限不足。
- `EEXIST`: 目录已存在。
- `EINVAL`: 参数无效。
- `ENOSPC`: 设备空间不足。
- `ENOMEM`: 内存不足。
- `EROFS`: 文件系统只读。

**常见用途**:
- 在相对于特定目录的位置创建新目录。
- 支持原子性操作，如同时创建和移动目录。

---

### 11. **SYMLINKAT**
**功能**: 在指定目录下创建一个符号链接。

**描述**: `symlinkat` 允许在给定的目录文件描述符下创建符号链接，支持相对路径和绝对路径。它是相对于指定目录的 `symlink`。

**原型**:
```c
int symlinkat(const char *target, int dirfd, const char *linkpath);
```

**参数**:
- `target`: 符号链接指向的目标路径。
- `dirfd`: 参考目录的文件描述符。如果为 `AT_FDCWD`，则使用当前工作目录。
- `linkpath`: 要创建的符号链接的路径。

**返回值**:
- 成功时返回 `0`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EACCES`: 权限不足。
- `EEXIST`: 符号链接已存在。
- `EINVAL`: 参数无效。
- `ENOSPC`: 设备空间不足。
- `ENOMEM`: 内存不足。
- `EROFS`: 文件系统只读。

**常见用途**:
- 创建相对路径的符号链接。
- 支持在不同目录下的灵活链接创建。

---

### 12. **UNLINKAT**
**功能**: 删除指定目录中的文件。

**描述**: `unlinkat` 允许在给定的目录文件描述符下删除文件或符号链接，支持相对路径和绝对路径。它是相对于指定目录的 `unlink`。

**原型**:
```c
int unlinkat(int dirfd, const char *pathname, int flags);
```

**参数**:
- `dirfd`: 参考目录的文件描述符。如果为 `AT_FDCWD`，则使用当前工作目录。
- `pathname`: 要删除的文件或符号链接的路径。
- `flags`: 控制行为的标志，如 `AT_REMOVEDIR`（用于删除目录）。

**返回值**:
- 成功时返回 `0`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EACCES`: 权限不足。
- `ENOENT`: 文件不存在。
- `ENOTDIR`: 预期的目录部分不是目录。
- `EISDIR`: 尝试删除目录但未指定 `AT_REMOVEDIR`。
- `EINVAL`: 参数无效。
- `ENOSPC`: 设备空间不足。
- `ENOMEM`: 内存不足。

**常见用途**:
- 删除文件或符号链接。
- 通过 `AT_REMOVEDIR` 删除目录。

---

### 13. **LINKAT**
**功能**: 在指定目录下创建一个硬链接。

**描述**: `linkat` 允许在给定的目录文件描述符下创建硬链接，支持相对路径和绝对路径。它是相对于指定目录的 `link`。

**原型**:
```c
int linkat(int olddirfd, const char *oldpath, int newdirfd, const char *newpath, int flags);
```

**参数**:
- `olddirfd`: 源文件所在目录的文件描述符。如果为 `AT_FDCWD`，则使用当前工作目录。
- `oldpath`: 源文件的路径。
- `newdirfd`: 目标链接所在目录的文件描述符。如果为 `AT_FDCWD`，则使用当前工作目录。
- `newpath`: 新硬链接的路径。
- `flags`: 控制行为的标志（目前通常为 `0`）。

**返回值**:
- 成功时返回 `0`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EACCES`: 权限不足。
- `EEXIST`: 目标路径已存在。
- `EINVAL`: 参数无效。
- `ENOENT`: 源文件不存在。
- `ENOSPC`: 设备空间不足。
- `ELOOP`: 符号链接过多。
- `ENOMEM`: 内存不足。
- `EROFS`: 文件系统只读。

**常见用途**:
- 创建硬链接，以便多个路径指向同一个文件。
- 支持相对路径的灵活链接创建。

---

### 14. **RENAMEAT**
**功能**: 将指定目录中的文件或目录重命名。

**描述**: `renameat` 允许在给定的目录文件描述符下重命名文件或目录，支持相对路径和绝对路径。它是相对于指定目录的 `rename`。

**原型**:
```c
int renameat(int olddirfd, const char *oldpath, int newdirfd, const char *newpath);
```

**参数**:
- `olddirfd`: 源文件所在目录的文件描述符。如果为 `AT_FDCWD`，则使用当前工作目录。
- `oldpath`: 源文件的路径。
- `newdirfd`: 目标路径所在目录的文件描述符。如果为 `AT_FDCWD`，则使用当前工作目录。
- `newpath`: 新路径的路径。

**返回值**:
- 成功时返回 `0`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EACCES`: 权限不足。
- `ENOENT`: 源文件不存在。
- `EINVAL`: 参数无效。
- `ENOSPC`: 设备空间不足。
- `EPERM`: 尝试跨文件系统重命名。
- `EEXIST`: 目标路径已存在且不能覆盖。
- `ENOMEM`: 内存不足。
- `EROFS`: 文件系统只读。

**常见用途**:
- 移动文件或目录到新位置。
- 重命名文件或目录。

---

### 15. **UNMOUNT**
**功能**: 卸载文件系统。

**描述**: `umount` 系统调用用于卸载已经挂载的文件系统，使其从文件系统层次结构中移除。

**原型**:
```c
int umount(const char *target);
```

**参数**:
- `target`: 要卸载的挂载点路径。

**返回值**:
- 成功时返回 `0`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EBUSY`: 文件系统正在使用中，无法卸载。
- `EINVAL`: 挂载点无效。
- `EIO`: 输入/输出错误。
- `ELOOP`: 符号链接过多。
- `ENOTBLK`: 目标不是块设备。
- `EPERM`: 权限不足。
- `ENOMEM`: 内存不足。

**常见用途**:
- 从系统中移除外部存储设备（如 USB 驱动器）。
- 卸载网络文件系统。

**注意**: 为了避免数据丢失或文件系统损坏，确保没有进程在使用该文件系统或相关文件。

---

### 16. **MOUNT**
**功能**: 挂载文件系统。

**描述**: `mount` 系统调用用于将文件系统挂载到文件系统层次结构中的指定挂载点，使其内容可以通过该挂载点访问。

**原型**:
```c
int mount(const char *source, const char *target, const char *filesystemtype, unsigned long mountflags, const void *data);
```

**参数**:
- `source`: 要挂载的设备或源（如设备文件）。
- `target`: 挂载点路径。
- `filesystemtype`: 文件系统类型（如 `ext4`, `ntfs`）。
- `mountflags`: 挂载选项（如 `MS_RDONLY`, `MS_NOSUID`）。
- `data`: 文件系统特定的挂载数据。

**返回值**:
- 成功时返回 `0`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EACCES`: 权限不足。
- `EBUSY`: 挂载点已被占用。
- `EINVAL`: 参数无效。
- `EIO`: 输入/输出错误。
- `ENODEV`: 未找到设备。
- `ENOMEM`: 内存不足。
- `EROFS`: 文件系统只读。

**常见用途**:
- 挂载外部存储设备（如硬盘、USB 驱动器）。
- 挂载网络文件系统（如 NFS, SMB）。
- 挂载虚拟文件系统（如 `proc`, `sysfs`）。

**注意**: 挂载操作通常需要超级用户权限。

---

### 17. **STATFS**
**功能**: 获取文件系统的状态信息。

**描述**: `statfs` 系统调用用于获取指定路径的文件系统的统计信息，如总块数、可用块数、块大小等。

**原型**:
```c
int statfs(const char *path, struct statfs *buf);
```

**参数**:
- `path`: 要查询的文件系统的路径。
- `buf`: 指向 `statfs` 结构的指针，用于存储文件系统的统计信息。

**返回值**:
- 成功时返回 `0`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EACCES`: 权限不足。
- `ENOENT`: 路径不存在。
- `EINVAL`: 参数无效。
- `ENOMEM`: 内存不足。

**`struct statfs` 包含**:
- `f_type`: 文件系统类型。
- `f_bsize`: 文件系统块大小。
- `f_blocks`: 文件系统中的总块数。
- `f_bfree`: 可用块数。
- `f_bavail`: 非超级用户可用块数。
- `f_files`: 文件系统中的总文件节点数。
- `f_ffree`: 可用文件节点数。
- `f_fsid`: 文件系统标识符。
- `f_namelen`: 文件名的最大长度。
- `f_frsize`: 基本块大小。
- 其他文件系统特定字段。

**常见用途**:
- 获取文件系统的容量和使用情况。
- 监控磁盘空间。

---

### 18. **FTRUNCATE64**
**功能**: 修改文件的大小，支持 64 位偏移。

**描述**: `ftruncate64` 用于将文件截断为指定的长度。如果文件当前长度大于指定长度，文件末尾将被截断；如果文件当前长度小于指定长度，文件将扩展，并在新增部分填充零。

**原型**:
```c
int ftruncate64(int fd, off64_t length);
```

**参数**:
- `fd`: 要截断的文件的文件描述符。
- `length`: 新的文件长度（64 位偏移）。

**返回值**:
- 成功时返回 `0`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EBADF`: `fd` 无效。
- `EACCES`: 权限不足。
- `EINVAL`: 文件类型不支持截断（如套接字）。
- `EFBIG`: 新长度超过文件系统限制。
- `EIO`: 输入/输出错误。
- `ENOSPC`: 设备空间不足。
- `ENOMEM`: 内存不足。

**常见用途**:
- 缩短或扩展文件大小。
- 预分配文件空间以提高性能。

**注意**: 在扩展文件时，新增部分未被写入的数据通常是未定义的（可能是零或未初始化的数据）。

---

### 19. **FACCESSAT**
**功能**: 检查文件的访问权限，支持相对路径和指定目录。

**描述**: `faccessat` 类似于 `access`，但允许指定基目录的文件描述符。这使得可以检查相对路径的文件权限，而不依赖于进程的当前工作目录。

**原型**:
```c
int faccessat(int dirfd, const char *pathname, int mode, int flags);
```

**参数**:
- `dirfd`: 基目录的文件描述符。如果为 `AT_FDCWD`，则使用当前工作目录。
- `pathname`: 要检查的文件路径。
- `mode`: 要检查的权限（`R_OK`, `W_OK`, `X_OK`, `F_OK`）。
- `flags`: 控制行为的标志，如 `AT_EACCESS`（使用有效用户 ID 和组 ID）。

**返回值**:
- 成功时返回 `0`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EACCES`: 权限不足。
- `ENOENT`: 文件不存在。
- `ELOOP`: 符号链接过多。
- `EINVAL`: 参数无效。
- `ENOMEM`: 内存不足。

**常见用途**:
- 检查文件的可读、可写或可执行权限。
- 在执行文件之前验证权限。

---

### 20. **CHDIR**
**功能**: 改变当前工作目录。

**描述**: `chdir` 系统调用用于更改调用进程的当前工作目录。更改后，所有相对路径的文件操作将基于新的工作目录。

**原型**:
```c
int chdir(const char *path);
```

**参数**:
- `path`: 要切换到的目标目录路径。

**返回值**:
- 成功时返回 `0`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EACCES`: 权限不足，无法进入目录。
- `ENOENT`: 目录不存在。
- `ENOTDIR`: 指定路径不是目录。
- `ELOOP`: 符号链接过多。
- `ENOMEM`: 内存不足。

**常见用途**:
- 改变进程的工作目录，以便在新目录下执行文件操作。
- 在脚本或程序中导航文件系统结构。

**注意**: 改变工作目录对当前进程及其子进程有效，但不影响其他进程。

---

### 21. **FCHMODAT**
**功能**: 修改指定文件的权限，支持相对路径和指定目录。

**描述**: `fchmodat` 类似于 `chmod`，但允许指定基目录的文件描述符。这使得可以修改相对路径的文件权限，而不依赖于进程的当前工作目录。

**原型**:
```c
int fchmodat(int dirfd, const char *pathname, mode_t mode, int flags);
```

**参数**:
- `dirfd`: 基目录的文件描述符。如果为 `AT_FDCWD`，则使用当前工作目录。
- `pathname`: 要修改权限的文件路径。
- `mode`: 新的权限模式。
- `flags`: 控制行为的标志（通常为 `0`）。

**返回值**:
- 成功时返回 `0`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EACCES`: 权限不足。
- `ENOENT`: 文件不存在。
- `ENOTDIR`: 指定路径中的某个部分不是目录。
- `EINVAL`: 参数无效。
- `ENOMEM`: 内存不足。

**常见用途**:
- 修改文件或目录的权限。
- 支持相对路径的权限修改操作。

---

### 22. **FCHOWN**
**功能**: 改变指定文件的所有者和组，支持文件描述符。

**描述**: `fchown` 用于更改通过文件描述符引用的文件的所有者（用户 ID）和组（组 ID）。

**原型**:
```c
int fchown(int fd, uid_t owner, gid_t group);
```

**参数**:
- `fd`: 要修改的文件的文件描述符。
- `owner`: 新的所有者的用户 ID。如果不更改所有者，传递 `-1`。
- `group`: 新的组的组 ID。如果不更改组，传递 `-1`。

**返回值**:
- 成功时返回 `0`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EACCES`: 权限不足。
- `EPERM`: 调用者没有足够的权限更改所有者。
- `EINVAL`: 参数无效。
- `ENOMEM`: 内存不足。

**常见用途**:
- 修改文件或目录的所有者或组。
- 实现文件所有权的管理和控制。

**注意**: 只有超级用户（root）或文件的当前所有者可以更改文件的所有者。

---

### 23. **OPENAT**
**功能**: 在指定目录下打开文件，支持相对路径和指定目录。

**描述**: `openat` 类似于 `open`，但允许指定基目录的文件描述符。这使得可以在相对路径的基础上打开文件，而不依赖于进程的当前工作目录。

**原型**:
```c
int openat(int dirfd, const char *pathname, int flags, mode_t mode);
```

**参数**:
- `dirfd`: 基目录的文件描述符。如果为 `AT_FDCWD`，则使用当前工作目录。
- `pathname`: 要打开的文件路径。
- `flags`: 打开标志（如 `O_RDONLY`, `O_WRONLY`, `O_RDWR`, `O_CREAT`）。
- `mode`: 如果创建文件，指定文件的权限模式。

**返回值**:
- 成功时返回新打开的文件描述符。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EACCES`: 权限不足。
- `ENOENT`: 文件不存在（如果未指定 `O_CREAT`）。
- `EEXIST`: 文件已存在，且使用了 `O_CREAT | O_EXCL`。
- `EINVAL`: 参数无效。
- `EMFILE`: 进程打开的文件描述符数量达到限制。
- `ENOMEM`: 内存不足。

**常见用途**:
- 在特定目录下打开文件，支持相对路径的灵活操作。
- 实现安全的文件访问控制，避免路径遍历攻击。

---

### 24. **CLOSE**
**功能**: 关闭文件描述符。

**描述**: `close` 系统调用用于关闭一个已打开的文件描述符，释放相关的资源。如果文件描述符是文件的最后引用，相关的文件资源将被释放。

**原型**:
```c
int close(int fd);
```

**参数**:
- `fd`: 要关闭的文件描述符。

**返回值**:
- 成功时返回 `0`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EBADF`: `fd` 无效。
- `EINTR`: 调用被信号中断。

**常见用途**:
- 释放不再需要的文件描述符。
- 管理进程的文件描述符表，避免资源泄漏。

**注意**: 关闭文件描述符后，任何对其的进一步操作都会失败，通常会分配给其他打开的文件。

---

### 25. **PIPE2**
**功能**: 创建一个管道，并可以指定标志。

**描述**: `pipe2` 系统调用用于创建一个匿名管道，与 `pipe` 类似，但允许在创建时指定额外的标志，如 `O_CLOEXEC` 或 `O_NONBLOCK`。

**原型**:
```c
int pipe2(int pipefd[2], int flags);
```

**参数**:
- `pipefd`: 指向包含两个文件描述符的数组，用于返回管道的读端和写端。
- `flags`: 控制行为的标志（如 `O_CLOEXEC`, `O_NONBLOCK`）。

**返回值**:
- 成功时返回 `0`，并在 `pipefd` 中返回两个文件描述符。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EFAULT`: `pipefd` 指针无效。
- `EINVAL`: 标志无效。
- `EMFILE`: 进程打开的文件描述符数量达到限制。
- `ENOMEM`: 内存不足。

**常见用途**:
- 在进程间或线程间进行数据通信。
- 实现生产者-消费者模型。
- 管道重定向，用于子进程与父进程间的数据交换。

**注意**: 管道是单向的，数据只能从读端读取，从写端写入。

---

### 26. **GETDENTS64**
**功能**: 读取目录内容，返回目录项的信息。

**描述**: `getdents64` 系统调用用于从目录文件描述符中读取目录项，返回目录中包含的文件和子目录的信息。它支持 64 位目录项结构，适用于大目录。

**原型**:
```c
int getdents64(unsigned int fd, struct linux_dirent64 *dirp, unsigned int count);
```

**参数**:
- `fd`: 打开的目录文件描述符。
- `dirp`: 指向 `linux_dirent64` 结构的缓冲区，用于存储目录项信息。
- `count`: 缓冲区的大小，以字节为单位。

**返回值**:
- 成功时返回读取的字节数。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EBADF`: `fd` 无效。
- `EIO`: 输入/输出错误。
- `EINVAL`: 参数无效。
- `ENOMEM`: 内存不足。

**`struct linux_dirent64` 包含**:
- `ino`: 文件的 inode 号。
- `off`: 下一个目录项的偏移量。
- `d_reclen`: 当前目录项的长度。
- `d_type`: 文件类型（如 `DT_REG`, `DT_DIR`）。
- `d_name`: 文件或目录的名称。

**常见用途**:
- 实现文件浏览器或目录列表工具。
- 遍历目录内容，获取文件和子目录的信息。

**注意**: 用户空间程序通常使用更高级别的库函数（如 `readdir`）来访问目录内容，但底层实现依赖于 `getdents64`。

---

### 27. **LSEEK**
**功能**: 移动文件指针到指定位置。

**描述**: `lseek` 系统调用用于改变打开文件的读写位置（文件偏移量）。它可以用于跳转到文件的任意位置进行读写操作。

**原型**:
```c
off_t lseek(int fd, off_t offset, int whence);
```

**参数**:
- `fd`: 要操作的文件描述符。
- `offset`: 相对于 `whence` 的偏移量。
- `whence`: 参考点，值可以是 `SEEK_SET`（文件开头）、`SEEK_CUR`（当前文件指针）、`SEEK_END`（文件末尾）。

**返回值**:
- 成功时返回新的文件偏移量。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EBADF`: `fd` 无效。
- `EINVAL`: 参数无效，或文件描述符不支持定位。
- `EOVERFLOW`: 文件偏移量超出支持的范围。

**常见用途**:
- 读取文件的特定部分。
- 实现文件的随机访问。
- 重置文件指针以重新读取文件内容。

**注意**: 对于某些设备文件，`lseek` 可能不支持定位操作。

---

### 28. **READ**
**功能**: 从文件描述符中读取数据。

**描述**: `read` 系统调用用于从指定的文件描述符中读取数据到缓冲区中。它是最基本的文件读取操作。

**原型**:
```c
ssize_t read(int fd, void *buf, size_t count);
```

**参数**:
- `fd`: 要读取的文件描述符。
- `buf`: 指向存储读取数据的缓冲区。
- `count`: 要读取的字节数。

**返回值**:
- 成功时返回实际读取的字节数，可能小于 `count`。
- 到达文件末尾时返回 `0`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EAGAIN` 或 `EWOULDBLOCK`: 非阻塞模式下没有数据可读。
- `EBADF`: `fd` 无效或未打开为读取。
- `EFAULT`: `buf` 指针无效。
- `EINTR`: 调用被信号中断。
- `EINVAL`: 参数无效。
- `ENOMEM`: 内存不足。

**常见用途**:
- 从文件、套接字、管道等读取数据。
- 实现文件复制、数据处理等操作。

**注意**: `read` 可能会读取少于请求的字节数，尤其是在非阻塞模式下或数据源速度较慢时。

---

### 29. **WRITE**
**功能**: 将数据写入文件描述符。

**描述**: `write` 系统调用用于将数据从缓冲区写入指定的文件描述符。它是最基本的文件写入操作。

**原型**:
```c
ssize_t write(int fd, const void *buf, size_t count);
```

**参数**:
- `fd`: 要写入的文件描述符。
- `buf`: 指向包含要写入数据的缓冲区。
- `count`: 要写入的字节数。

**返回值**:
- 成功时返回实际写入的字节数，可能小于 `count`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EAGAIN` 或 `EWOULDBLOCK`: 非阻塞模式下无法立即写入。
- `EBADF`: `fd` 无效或未打开为写入。
- `EFAULT`: `buf` 指针无效。
- `EINTR`: 调用被信号中断。
- `EINVAL`: 参数无效。
- `ENOSPC`: 设备空间不足。
- `EIO`: 输入/输出错误。

**常见用途**:
- 向文件、套接字、管道等写入数据。
- 实现文件写入、日志记录、数据传输等操作。

**注意**: `write` 可能会写入少于请求的字节数，尤其是在非阻塞模式下或数据目的地速度较慢时。

---

### 30. **READV**
**功能**: 从文件描述符中读取数据到多个缓冲区（散布输入）。

**描述**: `readv` 系统调用允许一次性从文件描述符中读取数据，并将其分散存储到多个缓冲区中。它支持向量化的读操作，提高数据传输效率。

**原型**:
```c
ssize_t readv(int fd, const struct iovec *iov, int iovcnt);
```

**参数**:
- `fd`: 要读取的文件描述符。
- `iov`: 指向 `iovec` 结构数组的指针，每个结构定义一个缓冲区。
- `iovcnt`: `iovec` 结构的数量。

**返回值**:
- 成功时返回实际读取的字节数，可能小于请求的总字节数。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EAGAIN` 或 `EWOULDBLOCK`: 非阻塞模式下没有数据可读。
- `EBADF`: `fd` 无效或未打开为读取。
- `EFAULT`: `iov` 指针无效。
- `EINVAL`: 参数无效。
- `ENOMEM`: 内存不足。

**常见用途**:
- 高效地读取分散存储的数据，如网络协议解析。
- 实现数据的并行处理。

**注意**: `iovcnt` 的值应在合理范围内，通常不超过 `IOV_MAX`。

---

### 31. **WRITEV**
**功能**: 将多个缓冲区的数据写入文件描述符（聚集输出）。

**描述**: `writev` 系统调用允许一次性将多个缓冲区中的数据写入指定的文件描述符。它支持向量化的写操作，提高数据传输效率。

**原型**:
```c
ssize_t writev(int fd, const struct iovec *iov, int iovcnt);
```

**参数**:
- `fd`: 要写入的文件描述符。
- `iov`: 指向 `iovec` 结构数组的指针，每个结构定义一个缓冲区。
- `iovcnt`: `iovec` 结构的数量。

**返回值**:
- 成功时返回实际写入的字节数，可能小于请求的总字节数。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EAGAIN` 或 `EWOULDBLOCK`: 非阻塞模式下无法立即写入。
- `EBADF`: `fd` 无效或未打开为写入。
- `EFAULT`: `iov` 指针无效。
- `EINVAL`: 参数无效。
- `ENOSPC`: 设备空间不足。
- `EIO`: 输入/输出错误。

**常见用途**:
- 高效地写入分散存储的数据，如日志记录。
- 实现数据的并行处理。

**注意**: `iovcnt` 的值应在合理范围内，通常不超过 `IOV_MAX`。

---

### 32. **PPOLL**
**功能**: 等待多个文件描述符的事件，支持信号掩码。

**描述**: `ppoll` 系统调用类似于 `poll`，但允许在等待事件时临时更改信号掩码。这使得可以在等待期间阻塞特定的信号，提供更好的信号处理控制。

**原型**:
```c
int ppoll(struct pollfd *fds, nfds_t nfds, const struct timespec *timeout, const sigset_t *sigmask);
```

**参数**:
- `fds`: 指向 `pollfd` 结构数组的指针，每个结构定义一个要监视的文件描述符和事件。
- `nfds`: `pollfd` 结构的数量。
- `timeout`: 等待的最长时间，指定为 `struct timespec`。`NULL` 表示无限等待。
- `sigmask`: 指向信号掩码的指针，用于临时设置阻塞的信号。

**返回值**:
- 成功时返回就绪的文件描述符数量。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EFAULT`: `fds` 或 `timeout` 指针无效。
- `EINVAL`: 参数无效。
- `ENOMEM`: 内存不足。
- `EINTR`: 调用被信号中断。

**常见用途**:
- 等待多个文件描述符的输入/输出事件。
- 实现高效的事件驱动程序，如网络服务器。

**注意**: `ppoll` 提供了比 `poll` 更灵活的信号处理机制，适用于需要精细控制信号的应用。

---

### 33. **FSTATAT**
**功能**: 获取指定文件的状态信息，支持指定目录。

**描述**: `fstatat` 类似于 `fstat`, 但允许指定基目录的文件描述符。这使得可以获取相对路径文件的状态信息，而不依赖于进程的当前工作目录。

**原型**:
```c
int fstatat(int dirfd, const char *pathname, struct stat *statbuf, int flags);
```

**参数**:
- `dirfd`: 基目录的文件描述符。如果为 `AT_FDCWD`，则使用当前工作目录。
- `pathname`: 要查询的文件路径。
- `statbuf`: 指向 `stat` 结构的指针，用于存储文件的状态信息。
- `flags`: 控制行为的标志，如 `AT_SYMLINK_NOFOLLOW`（不跟随符号链接）。

**返回值**:
- 成功时返回 `0`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EACCES`: 权限不足。
- `ENOENT`: 文件不存在。
- `EINVAL`: 参数无效。
- `ENOMEM`: 内存不足。

**`struct stat` 包含**:
- `st_mode`: 文件类型和权限。
- `st_ino`: 文件的 inode 号。
- `st_dev`: 文件所在设备。
- `st_nlink`: 链接数。
- `st_uid`: 所有者用户 ID。
- `st_gid`: 所有者组 ID。
- `st_size`: 文件大小。
- `st_atime`: 最后访问时间。
- `st_mtime`: 最后修改时间。
- `st_ctime`: 最后状态改变时间。
- 其他文件属性。

**常见用途**:
- 获取文件的详细信息，如类型、权限、大小等。
- 实现文件属性检查和验证。

---

### 34. **PREAD64**
**功能**: 从指定位置读取文件的内容，支持 64 位偏移。

**描述**: `pread64` 系统调用用于在不改变文件描述符的当前偏移量的情况下，从指定的文件位置读取数据。这对于多线程程序中的并行读取非常有用。

**原型**:
```c
ssize_t pread64(int fd, void *buf, size_t count, off64_t offset);
```

**参数**:
- `fd`: 要读取的文件描述符。
- `buf`: 指向存储读取数据的缓冲区。
- `count`: 要读取的字节数。
- `offset`: 从文件开头的偏移量。

**返回值**:
- 成功时返回实际读取的字节数，可能小于 `count`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EAGAIN` 或 `EWOULDBLOCK`: 非阻塞模式下没有数据可读。
- `EBADF`: `fd` 无效或未打开为读取。
- `EFAULT`: `buf` 指针无效。
- `EINVAL`: 参数无效。
- `EIO`: 输入/输出错误。
- `ENOMEM`: 内存不足。

**常见用途**:
- 从文件的特定位置读取数据，支持随机访问。
- 实现高效的文件读取操作，避免改变文件描述符的全局偏移量。

**注意**: `pread64` 是线程安全的，因为它不依赖于文件描述符的共享偏移量。

---

### 35. **PWRITE64**
**功能**: 从指定位置写入内容到文件，支持 64 位偏移。

**描述**: `pwrite64` 系统调用用于在不改变文件描述符的当前偏移量的情况下，将数据写入指定的文件位置。这对于多线程程序中的并行写入非常有用。

**原型**:
```c
ssize_t pwrite64(int fd, const void *buf, size_t count, off64_t offset);
```

**参数**:
- `fd`: 要写入的文件描述符。
- `buf`: 指向包含要写入数据的缓冲区。
- `count`: 要写入的字节数。
- `offset`: 从文件开头的偏移量。

**返回值**:
- 成功时返回实际写入的字节数，可能小于 `count`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EAGAIN` 或 `EWOULDBLOCK`: 非阻塞模式下无法立即写入。
- `EBADF`: `fd` 无效或未打开为写入。
- `EFAULT`: `buf` 指针无效。
- `EINVAL`: 参数无效。
- `ENOSPC`: 设备空间不足。
- `EIO`: 输入/输出错误。
- `ENOMEM`: 内存不足。

**常见用途**:
- 在文件的特定位置写入数据，支持随机访问。
- 实现高效的文件写入操作，避免改变文件描述符的全局偏移量。

**注意**: `pwrite64` 是线程安全的，因为它不依赖于文件描述符的共享偏移量。

---

### 36. **SENDFILE64**
**功能**: 将一个文件的内容发送到另一个文件描述符中，支持 64 位文件偏移。

**描述**: `sendfile64` 系统调用用于在文件描述符之间高效地传输数据，通常用于将文件内容发送到套接字，以减少用户空间与内核空间之间的数据拷贝，提高性能。

**原型**:
```c
ssize_t sendfile64(int out_fd, int in_fd, off64_t *offset, size_t count);
```

**参数**:
- `out_fd`: 输出文件描述符，通常是套接字。
- `in_fd`: 输入文件描述符，通常是文件。
- `offset`: 指向文件偏移量的指针。如果为 `NULL`，则使用并更新文件描述符的当前偏移量。
- `count`: 要传输的字节数。

**返回值**:
- 成功时返回传输的字节数。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EAGAIN` 或 `EWOULDBLOCK`: 非阻塞模式下无法立即传输。
- `EBADF`: `in_fd` 或 `out_fd` 无效。
- `EFAULT`: `offset` 指针无效。
- `EINVAL`: 参数无效。
- `ENOSPC`: 设备空间不足。
- `EPIPE`: `out_fd` 已关闭。
- `ENOMEM`: 内存不足。

**常见用途**:
- 实现高效的文件传输到网络套接字，如 HTTP 服务器发送文件。
- 减少用户空间与内核空间的数据拷贝，提高性能。

**注意**: `sendfile64` 在某些文件系统或设备上可能不支持，需要根据具体情况使用。

---

### 37. **PSELECT6**
**功能**: 选择待处理的文件描述符，支持信号掩码（类似于 `select`，但支持更多选项）。

**描述**: `pselect6` 系统调用用于监视多个文件描述符的状态变化（如可读、可写、异常），并允许在等待事件时临时更改信号掩码。这提供了比 `select` 更灵活的信号处理机制。

**原型**:
```c
int pselect6(int nfds, fd_set *readfds, fd_set *writefds, fd_set *exceptfds, const struct timespec *timeout, const sigset_t *sigmask);
```

**参数**:
- `nfds`: 要监视的文件描述符数量。
- `readfds`: 要监视可读事件的文件描述符集合。
- `writefds`: 要监视可写事件的文件描述符集合。
- `exceptfds`: 要监视异常事件的文件描述符集合。
- `timeout`: 等待的最长时间，指定为 `struct timespec`。`NULL` 表示无限等待。
- `sigmask`: 指向信号掩码的指针，用于临时设置阻塞的信号。

**返回值**:
- 成功时返回就绪的文件描述符数量。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EINTR`: 调用被信号中断。
- `EINVAL`: 参数无效。
- `ENOMEM`: 内存不足。

**常见用途**:
- 实现多路复用的 I/O 操作，监视多个文件描述符的状态。
- 实现高效的事件驱动程序，如网络服务器。

**注意**: `pselect6` 提供了比 `select` 更好的信号处理控制，适用于需要精细管理信号的应用。

---

### 38. **PREADLINKAT**
**功能**: 读取符号链接的目标路径，支持指定目录。

**描述**: `preadlinkat` 允许在给定目录文件描述符下读取符号链接的目标路径，支持相对路径和绝对路径。它是相对于指定目录的 `readlink`.

**原型**:
```c
ssize_t preadlinkat(int dirfd, const char *pathname, char *buf, size_t bufsiz, off_t offset);
```

**参数**:
- `dirfd`: 基目录的文件描述符。如果为 `AT_FDCWD`，则使用当前工作目录。
- `pathname`: 要读取的符号链接路径。
- `buf`: 存储符号链接目标路径的缓冲区。
- `bufsiz`: 缓冲区的大小。
- `offset`: 从符号链接目标路径的哪个位置开始读取。

**返回值**:
- 成功时返回读取的字节数。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EACCES`: 权限不足。
- `ENOENT`: 符号链接不存在。
- `EINVAL`: 参数无效。
- `EIO`: 输入/输出错误。
- `ENOMEM`: 内存不足。

**常见用途**:
- 获取符号链接指向的目标路径。
- 实现符号链接解析和验证。

**注意**: `preadlinkat` 允许从符号链接的特定偏移量读取，但通常 `readlink` 更为常用。

---

### 39. **FSTAT**
**功能**: 获取文件的状态信息，支持文件描述符。

**描述**: `fstat` 系统调用用于获取通过文件描述符引用的文件的状态信息，如文件类型、权限、大小等。

**原型**:
```c
int fstat(int fd, struct stat *statbuf);
```

**参数**:
- `fd`: 要查询的文件描述符。
- `statbuf`: 指向 `stat` 结构的指针，用于存储文件的状态信息。

**返回值**:
- 成功时返回 `0`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EBADF`: `fd` 无效。
- `EINVAL`: 参数无效。
- `ENOMEM`: 内存不足。

**`struct stat` 包含**:
- `st_mode`: 文件类型和权限。
- `st_ino`: 文件的 inode 号。
- `st_dev`: 文件所在设备。
- `st_nlink`: 链接数。
- `st_uid`: 所有者用户 ID。
- `st_gid`: 所有者组 ID。
- `st_size`: 文件大小。
- `st_atime`: 最后访问时间。
- `st_mtime`: 最后修改时间。
- `st_ctime`: 最后状态改变时间。
- 其他文件属性。

**常见用途**:
- 获取文件的详细信息，如类型、权限、大小等。
- 实现文件属性检查和验证。

---

### 40. **SYNC**
**功能**: 同步所有的文件系统缓存到磁盘。

**描述**: `sync` 系统调用用于将所有未写入的数据和元数据从内核的文件系统缓存同步到磁盘。这有助于确保数据在系统崩溃或断电时不会丢失。

**原型**:
```c
int sync(void);
```

**参数**:
- 无。

**返回值**:
- 永远返回 `0`。

**错误**:
- 无。

**常见用途**:
- 在系统关机或重启之前确保数据完整性。
- 强制写入数据到磁盘，以防止数据丢失。

**注意**: `sync` 是异步操作，调用后并不保证数据立即写入磁盘，但会尽快完成。

---

### 41. **FSYNC**
**功能**: 同步指定文件的内容到磁盘。

**描述**: `fsync` 系统调用用于将指定文件描述符关联的文件的所有未写入的数据和元数据同步到磁盘。这确保文件内容和元数据的持久性。

**原型**:
```c
int fsync(int fd);
```

**参数**:
- `fd`: 要同步的文件描述符。

**返回值**:
- 成功时返回 `0`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EBADF`: `fd` 无效。
- `EIO`: 输入/输出错误。
- `EINVAL`: 参数无效。
- `ENOMEM`: 内存不足。

**常见用途**:
- 在写入重要数据后确保数据持久性。
- 实现事务性操作，如数据库的提交。

**注意**: `fsync` 可能会阻塞，直到数据写入完成。

---

### 42. **UTIMENSAT**
**功能**: 修改文件的访问和修改时间，支持指定目录。

**描述**: `utimensat` 系统调用用于更新文件的访问时间和修改时间。它允许指定基目录的文件描述符，支持相对路径和绝对路径，并可以选择是否跟随符号链接。

**原型**:
```c
int utimensat(int dirfd, const char *pathname, const struct timespec times[2], int flags);
```

**参数**:
- `dirfd`: 基目录的文件描述符。如果为 `AT_FDCWD`，则使用当前工作目录。
- `pathname`: 要修改时间的文件路径。
- `times`: 指向 `timespec` 结构数组的指针，包含访问时间和修改时间。可以使用 `NULL` 表示将时间设置为当前时间。
- `flags`: 控制行为的标志，如 `AT_SYMLINK_NOFOLLOW`（不跟随符号链接）。

**返回值**:
- 成功时返回 `0`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EACCES`: 权限不足。
- `ENOENT`: 文件不存在。
- `EINVAL`: 参数无效。
- `ENOMEM`: 内存不足。

**`struct timespec` 包含**:
- `tv_sec`: 秒部分。
- `tv_nsec`: 纳秒部分。

**常见用途**:
- 更新文件的访问和修改时间。
- 实现文件时间戳管理。

**注意**: 修改时间不会影响文件内容，只更新元数据。

---

### 43. **RENAMEAT2**
**功能**: 改进版的 `renameat`，允许指定更多选项。

**描述**: `renameat2` 系统调用扩展了 `renameat` 的功能，允许在重命名或移动文件时指定额外的标志，如 `RENAME_EXCHANGE`（交换两个文件的位置）或 `RENAME_NOREPLACE`（不替换现有文件）。

**原型**:
```c
int renameat2(int olddirfd, const char *oldpath, int newdirfd, const char *newpath, unsigned int flags);
```

**参数**:
- `olddirfd`: 源文件所在目录的文件描述符。如果为 `AT_FDCWD`，则使用当前工作目录。
- `oldpath`: 源文件的路径。
- `newdirfd`: 目标路径所在目录的文件描述符。如果为 `AT_FDCWD`，则使用当前工作目录。
- `newpath`: 新路径的路径。
- `flags`: 控制行为的标志，如 `RENAME_EXCHANGE`, `RENAME_NOREPLACE`。

**返回值**:
- 成功时返回 `0`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EACCES`: 权限不足。
- `ENOENT`: 源文件不存在。
- `EINVAL`: 参数无效，或不支持的标志。
- `ENOSPC`: 设备空间不足。
- `EEXIST`: 目标路径已存在，且不允许替换。
- `EINVAL`: 尝试跨文件系统重命名（如果不支持）。
- `EFAULT`: 参数指针无效。
- `ENOMEM`: 内存不足。

**常见用途**:
- 实现更灵活和安全的文件重命名和移动操作。
- 支持原子交换两个文件的位置。

**注意**: `renameat2` 需要内核支持相应的标志，可能在较旧的内核版本中不可用。

---

### 44. **COPYFILERANGE**
**功能**: 将一个文件的某一部分复制到另一个文件的指定位置。

**描述**: `copy_filerange` 系统调用用于在两个文件描述符之间高效地复制数据，支持指定源和目标的偏移量和字节数。这避免了用户空间与内核空间之间的数据拷贝，提高性能。

**原型**:
```c
ssize_t copy_filerange(int out_fd, loff_t *out_offset, int in_fd, loff_t *in_offset, size_t len, unsigned int flags);
```

**参数**:
- `out_fd`: 目标文件描述符。
- `out_offset`: 指向目标文件偏移量的指针。如果为 `NULL`，则使用并更新目标文件描述符的当前偏移量。
- `in_fd`: 源文件描述符。
- `in_offset`: 指向源文件偏移量的指针。如果为 `NULL`，则使用并更新源文件描述符的当前偏移量。
- `len`: 要复制的字节数。
- `flags`: 控制行为的标志（目前通常为 `0`）。

**返回值**:
- 成功时返回复制的字节数。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EAGAIN` 或 `EWOULDBLOCK`: 非阻塞模式下无法立即复制。
- `EBADF`: `in_fd` 或 `out_fd` 无效。
- `EINVAL`: 参数无效。
- `EIO`: 输入/输出错误。
- `ENOSPC`: 设备空间不足。
- `ENOMEM`: 内存不足。
- `EPIPE`: 目标文件描述符已关闭（如套接字）。

**常见用途**:
- 高效地复制文件内容，如文件备份或镜像。
- 实现文件传输功能，减少数据拷贝开销。

**注意**: `copy_filerange` 是内核级别的复制操作，适用于需要高性能数据传输的场景。

---

### 45. **STATX**
**功能**: 获取文件的扩展状态信息，比 `stat` 更加全面。

**描述**: `statx` 系统调用用于获取文件的详细状态信息，包括更多的属性和元数据。它支持通过指定掩码选择所需的信息，提高效率。

**原型**:
```c
int statx(int dirfd, const char *pathname, int flags, unsigned int mask, struct statx *statxbuf);
```

**参数**:
- `dirfd`: 基目录的文件描述符。如果为 `AT_FDCWD`，则使用当前工作目录。
- `pathname`: 要查询的文件路径。
- `flags`: 控制行为的标志，如 `AT_SYMLINK_NOFOLLOW`。
- `mask`: 指定要获取的字段的掩码，如 `STATX_TYPE`, `STATX_MODE`, `STATX_SIZE` 等。
- `statxbuf`: 指向 `statx` 结构的指针，用于存储文件的状态信息。

**返回值**:
- 成功时返回 `0`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EACCES`: 权限不足。
- `ENOENT`: 文件不存在。
- `EINVAL`: 参数无效。
- `ENOMEM`: 内存不足。

**`struct statx` 包含**:
- `stx_mask`: 实际返回的字段掩码。
- `stx_blksize`: 文件系统块大小。
- `stx_attributes`: 文件属性。
- `stx_nlink`: 链接数。
- `stx_uid`: 所有者用户 ID。
- `stx_gid`: 所有者组 ID。
- `stx_mode`: 文件模式（类型和权限）。
- `stx_ino`: inode 号。
- `stx_size`: 文件大小。
- `stx_blocks`: 分配的块数。
- `stx_attributes_mask`: 可用的属性掩码。
- `stx_atime`, `stx_mtime`, `stx_ctime`: 访问时间、修改时间、状态改变时间。
- 其他扩展属性，如文件 ID、设备 ID、扩展时间等。

**常见用途**:
- 获取文件的详细属性信息。
- 实现高效的文件属性查询，按需选择所需的信息。

**注意**: `statx` 提供了比 `stat` 更灵活和高效的接口，适用于需要详细文件信息的应用。

---

### 46. **PIDFD_OPEN**
**功能**: 打开一个进程的 PID 文件描述符，用于管理进程的信息。

**描述**: `pidfd_open` 系统调用用于获取一个指向指定 PID 的进程文件描述符。通过这个文件描述符，可以执行与进程相关的操作，如等待进程退出或获取进程状态。

**原型**:
```c
int pidfd_open(pid_t pid, unsigned int flags);
```

**参数**:
- `pid`: 要打开的进程的 PID。
- `flags`: 控制行为的标志（目前通常为 `0`）。

**返回值**:
- 成功时返回新的进程文件描述符。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `ESRCH`: 指定的 PID 不存在。
- `EINVAL`: 参数无效。
- `EPERM`: 权限不足，无法打开指定进程的文件描述符。
- `ENOMEM`: 内存不足。

**常见用途**:
- 实现进程监控和管理功能。
- 在多线程或多进程应用中跟踪子进程的状态。

**注意**: 进程文件描述符在进程退出后会自动关闭，确保不会泄漏。

---

### 47. **OPEN**
**功能**: 打开一个文件。

**描述**: `open` 系统调用用于打开或创建文件，返回一个文件描述符以供后续的读写操作。

**原型**:
```c
int open(const char *pathname, int flags, ... /* mode_t mode */ );
```

**参数**:
- `pathname`: 要打开或创建的文件路径。
- `flags`: 打开标志（如 `O_RDONLY`, `O_WRONLY`, `O_RDWR`, `O_CREAT`）。
- `mode`: 如果创建文件，指定文件的权限模式（可选）。

**返回值**:
- 成功时返回新打开的文件描述符。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EACCES`: 权限不足。
- `ENOENT`: 文件不存在，且未指定 `O_CREAT`。
- `EEXIST`: 文件已存在，且使用了 `O_CREAT | O_EXCL`。
- `EINVAL`: 参数无效。
- `EMFILE`: 进程打开的文件描述符数量达到限制。
- `ENOMEM`: 内存不足。
- `EROFS`: 文件系统只读。

**常见用途**:
- 打开文件进行读写操作。
- 创建新文件或截断现有文件。

**注意**: 文件描述符是进程的资源，确保在不再需要时关闭，以避免资源泄漏。

---

### 48. **STAT**
**功能**: 获取文件的状态信息，支持文件路径。

**描述**: `stat` 系统调用用于获取指定路径的文件的状态信息，如文件类型、权限、大小等。

**原型**:
```c
int stat(const char *pathname, struct stat *statbuf);
```

**参数**:
- `pathname`: 要查询的文件路径。
- `statbuf`: 指向 `stat` 结构的指针，用于存储文件的状态信息。

**返回值**:
- 成功时返回 `0`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EACCES`: 权限不足。
- `ENOENT`: 文件不存在。
- `EINVAL`: 参数无效。
- `ENOMEM`: 内存不足。

**`struct stat` 包含**:
- `st_mode`: 文件类型和权限。
- `st_ino`: 文件的 inode 号。
- `st_dev`: 文件所在设备。
- `st_nlink`: 链接数。
- `st_uid`: 所有者用户 ID。
- `st_gid`: 所有者组 ID。
- `st_size`: 文件大小。
- `st_atime`: 最后访问时间。
- `st_mtime`: 最后修改时间。
- `st_ctime`: 最后状态改变时间。
- 其他文件属性。

**常见用途**:
- 获取文件的详细信息，如类型、权限、大小等。
- 实现文件属性检查和验证。

**注意**: `stat` 会跟随符号链接，获取符号链接指向的文件的状态信息。若要获取符号链接自身的信息，应使用 `lstat`。

---

### 49. **EVENTFD2**
**功能**: 创建一个事件文件描述符，支持更多选项。

**描述**: `eventfd2` 是 `eventfd` 的改进版，允许在创建事件文件描述符时指定更多的标志，如 `EFD_CLOEXEC` 和 `EFD_NONBLOCK`，以控制文件描述符的行为。

**原型**:
```c
int eventfd2(unsigned int initval, int flags);
```

**参数**:
- `initval`: 初始化事件计数器的值。
- `flags`: 控制行为的标志（如 `EFD_CLOEXEC`, `EFD_NONBLOCK`）。

**返回值**:
- 成功时返回一个新的事件文件描述符。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EINVAL`: 参数无效。
- `EEXIST`: 文件描述符已存在。
- `ENOMEM`: 内存不足。

**常见用途**:
- 进程间或线程间的事件通知和同步。
- 实现信号通知机制，支持非阻塞操作和文件描述符自动关闭。

**注意**: `eventfd2` 提供了比 `eventfd` 更灵活的文件描述符控制选项，适用于需要精细控制文件描述符行为的应用。

---

### 50. **UNLINK**
**功能**: 删除文件。

**描述**: `unlink` 系统调用用于删除指定路径的文件。它会减少文件的链接数，如果链接数降为零且没有打开的文件描述符，文件的数据和元数据将被释放。

**原型**:
```c
int unlink(const char *pathname);
```

**参数**:
- `pathname`: 要删除的文件路径。

**返回值**:
- 成功时返回 `0`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EACCES`: 权限不足。
- `ENOENT`: 文件不存在。
- `EISDIR`: 尝试删除目录而未使用 `unlinkat`。
- `EINVAL`: 参数无效。
- `EIO`: 输入/输出错误。
- `ENOMEM`: 内存不足。
- `EROFS`: 文件系统只读。

**常见用途**:
- 删除不再需要的文件。
- 清理临时文件或缓存文件。

**注意**: `unlink` 不会删除目录。要删除目录，请使用 `rmdir` 或 `unlinkat` 带有 `AT_REMOVEDIR` 标志。

---

### 51. **EPOLL_WAIT**
**功能**: 等待 `epoll` 实例中注册的事件。

**描述**: `epoll_wait` 系统调用用于等待 `epoll` 实例中注册的文件描述符的事件发生。它会阻塞调用线程，直到至少一个事件被触发或超时。

**原型**:
```c
int epoll_wait(int epfd, struct epoll_event *events, int maxevents, int timeout);
```

**参数**:
- `epfd`: `epoll` 实例的文件描述符。
- `events`: 指向 `epoll_event` 结构数组的指针，用于存储触发的事件。
- `maxevents`: `events` 数组的大小。
- `timeout`: 等待的最长时间（毫秒）。`-1` 表示无限等待。

**返回值**:
- 成功时返回触发的事件数量。
- 超时时返回 `0`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EINVAL`: 参数无效。
- `EINTR`: 调用被信号中断。
- `ENOMEM`: 内存不足。

**常见用途**:
- 实现高效的事件驱动程序，如网络服务器。
- 监视多个文件描述符的状态变化，处理 I/O 事件。

**注意**: `epoll_wait` 可以在阻塞模式下使用，也可以在非阻塞模式下使用，具体取决于 `epoll` 实例的标志。

---

### 52. **DUP2**
**功能**: 类似于 `dup`，但可以指定新文件描述符。

**描述**: `dup2` 用于复制一个文件描述符到另一个指定的文件描述符。如果目标文件描述符已经打开，则先关闭它。`dup2` 允许指定新文件描述符的编号。

**原型**:
```c
int dup2(int oldfd, int newfd);
```

**参数**:
- `oldfd`: 要复制的现有文件描述符。
- `newfd`: 指定的新文件描述符编号。

**返回值**:
- 成功时返回新文件描述符。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EBADF`: `oldfd` 无效。
- `EINVAL`: `newfd` 无效，或 `oldfd` 和 `newfd` 相同。
- `EMFILE`: 进程打开的文件描述符数量达到限制。
- `ENOMEM`: 内存不足。
- `EINTR`: 调用被信号中断。

**常见用途**:
- 重定向标准输入、输出或错误（如 `stdin`, `stdout`, `stderr`）。
- 将文件描述符复制到预定义的编号，以便与其他函数接口兼容。

**注意**: 如果 `oldfd` 和 `newfd` 相同，`dup2` 不会关闭 `newfd`，但会返回 `newfd`。

---

### 53. **RENAME**
**功能**: 重命名文件或目录。

**描述**: `rename` 系统调用用于重命名或移动文件或目录。它是 `renameat` 的简化版本，使用当前工作目录作为参考点。

**原型**:
```c
int rename(const char *oldpath, const char *newpath);
```

**参数**:
- `oldpath`: 源文件或目录的路径。
- `newpath`: 目标文件或目录的路径。

**返回值**:
- 成功时返回 `0`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EACCES`: 权限不足。
- `ENOENT`: 源文件不存在。
- `EEXIST`: 目标路径已存在，且不允许覆盖。
- `EINVAL`: 参数无效。
- `ENOSPC`: 设备空间不足。
- `EPERM`: 尝试跨文件系统重命名。
- `EIO`: 输入/输出错误。
- `ENOMEM`: 内存不足。
- `EROFS`: 文件系统只读。

**常见用途**:
- 移动文件或目录到新位置。
- 重命名文件或目录。
- 实现原子性文件更新，如通过先写入临时文件再重命名覆盖原文件。

---

### 54. **MKDIR**
**功能**: 创建目录。

**描述**: `mkdir` 系统调用用于在指定路径创建一个新的目录，并设置其权限模式。

**原型**:
```c
int mkdir(const char *pathname, mode_t mode);
```

**参数**:
- `pathname`: 要创建的目录路径。
- `mode`: 新目录的权限模式。

**返回值**:
- 成功时返回 `0`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EACCES`: 权限不足。
- `EEXIST`: 目录已存在。
- `EINVAL`: 参数无效。
- `ENOSPC`: 设备空间不足。
- `ENOMEM`: 内存不足。
- `EROFS`: 文件系统只读。

**常见用途**:
- 创建新目录以存储文件或子目录。
- 实现目录结构的动态创建。

**注意**: 创建目录时，`mode` 可能会受到进程的 umask 影响，实际权限可能低于指定值。

---

### 55. **RMDIR**
**功能**: 删除空目录。

**描述**: `rmdir` 系统调用用于删除指定路径的空目录。如果目录中包含文件或子目录，则删除失败。

**原型**:
```c
int rmdir(const char *pathname);
```

**参数**:
- `pathname`: 要删除的目录路径。

**返回值**:
- 成功时返回 `0`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `ENOTDIR`: 指定路径不是目录。
- `EACCES`: 权限不足。
- `ENOTEMPTY`: 目录不为空。
- `EINVAL`: 参数无效。
- `EIO`: 输入/输出错误。
- `ENOMEM`: 内存不足。
- `EROFS`: 文件系统只读。

**常见用途**:
- 删除不再需要的空目录。
- 清理临时目录。

**注意**: `rmdir` 仅删除空目录。如果需要递归删除目录及其内容，需要先删除子文件和子目录。

---

### 56. **ACCESS**
**功能**: 检查文件的访问权限。

**描述**: `access` 系统调用用于检查调用进程对指定文件的访问权限，如可读、可写、可执行等。它基于进程的有效用户 ID 和组 ID 进行权限检查。

**原型**:
```c
int access(const char *pathname, int mode);
```

**参数**:
- `pathname`: 要检查的文件路径。
- `mode`: 要检查的权限（`R_OK`, `W_OK`, `X_OK`, `F_OK`）。

**返回值**:
- 成功时返回 `0`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EACCES`: 权限不足。
- `ENOENT`: 文件不存在。
- `ELOOP`: 符号链接过多。
- `EINVAL`: 参数无效。
- `ENOMEM`: 内存不足。

**常见用途**:
- 在执行文件前验证访问权限。
- 实现权限检查机制，确保用户有权访问文件。

**注意**: `access` 基于有效用户 ID 和组 ID 进行检查，而不是实际的文件描述符的权限。

---

### 57. **PIPE**
**功能**: 创建一个匿名管道。

**描述**: `pipe` 系统调用用于创建一个匿名管道，返回一对文件描述符，用于进程间的单向数据传输。一个描述符用于读，另一个用于写。

**原型**:
```c
int pipe(int pipefd[2]);
```

**参数**:
- `pipefd`: 指向包含两个文件描述符的数组，用于返回管道的读端和写端。

**返回值**:
- 成功时返回 `0`，并在 `pipefd` 中返回两个文件描述符。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EFAULT`: `pipefd` 指针无效。
- `EMFILE`: 进程打开的文件描述符数量达到限制。
- `ENOMEM`: 内存不足。

**常见用途**:
- 在父子进程之间传输数据。
- 实现生产者-消费者模型。
- 管道重定向，用于子进程与父进程间的数据交换。

**注意**: 管道是单向的，数据只能从写端写入，从读端读取。若需要双向通信，需要创建两个管道。

---

### 58. **POLL**
**功能**: 等待多个文件描述符的事件，类似于 `select`。

**描述**: `poll` 系统调用用于监视多个文件描述符的状态变化（如可读、可写、异常），并等待事件的发生。与 `select` 相比，`poll` 支持更大的文件描述符集合和更灵活的事件处理。

**原型**:
```c
int poll(struct pollfd *fds, nfds_t nfds, int timeout);
```

**参数**:
- `fds`: 指向 `pollfd` 结构数组的指针，每个结构定义一个要监视的文件描述符和事件。
- `nfds`: `pollfd` 结构的数量。
- `timeout`: 等待的最长时间（毫秒）。`-1` 表示无限等待。

**返回值**:
- 成功时返回就绪的文件描述符数量。
- 超时时返回 `0`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EFAULT`: `fds` 指针无效。
- `EINVAL`: 参数无效。
- `ENOMEM`: 内存不足。

**常见用途**:
- 实现多路复用的 I/O 操作，监视多个文件描述符的状态。
- 实现高效的事件驱动程序，如网络服务器。

**注意**: `poll` 可以监视更大的文件描述符集合，但在性能和可扩展性上不如 `epoll`，尤其在监视大量文件描述符时。

---

### 59. **CREAT**
**功能**: 创建一个新文件或截断现有文件。

**描述**: `creat` 系统调用用于创建一个新文件，如果文件已存在，则将其截断为零长度。它是 `open` 的简化版本，等同于 `open(path, O_CREAT | O_WRONLY | O_TRUNC, mode)`。

**原型**:
```c
int creat(const char *pathname, mode_t mode);
```

**参数**:
- `pathname`: 要创建的文件路径。
- `mode`: 新文件的权限模式。

**返回值**:
- 成功时返回新打开的文件描述符。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EACCES`: 权限不足。
- `EEXIST`: 文件已存在（如果使用 `O_EXCL`）。
- `EINVAL`: 参数无效。
- `EMFILE`: 进程打开的文件描述符数量达到限制。
- `ENOMEM`: 内存不足。
- `EROFS`: 文件系统只读。

**常见用途**:
- 创建新文件进行写入操作。
- 截断现有文件以重新写入数据。

**注意**: `creat` 不支持指定打开标志，建议使用 `open`，因为它更灵活。

---

### 60. **SELECT**
**功能**: 等待多个文件描述符的事件，类似于 `poll` 和 `pselect6`。

**描述**: `select` 系统调用用于监视多个文件描述符的状态变化（如可读、可写、异常），并等待事件的发生。它是最早的多路复用机制之一，但在文件描述符数量较大时效率较低。

**原型**:
```c
int select(int nfds, fd_set *readfds, fd_set *writefds, fd_set *exceptfds, struct timeval *timeout);
```

**参数**:
- `nfds`: 要监视的最大文件描述符加一。
- `readfds`: 要监视可读事件的文件描述符集合。
- `writefds`: 要监视可写事件的文件描述符集合。
- `exceptfds`: 要监视异常事件的文件描述符集合。
- `timeout`: 等待的最长时间，指定为 `struct timeval`。`NULL` 表示无限等待。

**返回值**:
- 成功时返回就绪的文件描述符数量。
- 超时时返回 `0`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EINTR`: 调用被信号中断。
- `EINVAL`: 参数无效。
- `ENOMEM`: 内存不足。

**常见用途**:
- 实现多路复用的 I/O 操作，监视多个文件描述符的状态。
- 实现事件驱动程序，如网络客户端和服务器。

**注意**: `select` 有文件描述符数量的限制（通常为 1024），并且在监视大量文件描述符时效率较低。对于高性能应用，推荐使用 `epoll` 或 `poll`。

---

### 61. **READLINK**
**功能**: 读取符号链接的目标路径。

**描述**: `readlink` 系统调用用于读取符号链接文件的目标路径，即符号链接指向的路径。

**原型**:
```c
ssize_t readlink(const char *pathname, char *buf, size_t bufsiz);
```

**参数**:
- `pathname`: 要读取的符号链接路径。
- `buf`: 存储符号链接目标路径的缓冲区。
- `bufsiz`: 缓冲区的大小。

**返回值**:
- 成功时返回实际读取的字节数。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EACCES`: 权限不足。
- `ENOENT`: 符号链接不存在。
- `EINVAL`: 参数无效。
- `EIO`: 输入/输出错误。
- `ENOMEM`: 内存不足。
- `EINVAL`: 不是符号链接。

**常见用途**:
- 获取符号链接指向的目标路径。
- 实现符号链接解析和验证。

**注意**: `readlink` 不会在目标路径后添加空字符，因此需要确保缓冲区有足够的空间，并在需要时手动添加终止符。

---

### 62. **CHMOD**
**功能**: 修改文件权限。

**描述**: `chmod` 系统调用用于更改指定文件或目录的权限模式。它允许设置文件的读、写、执行权限。

**原型**:
```c
int chmod(const char *pathname, mode_t mode);
```

**参数**:
- `pathname`: 要修改权限的文件或目录路径。
- `mode`: 新的权限模式。

**返回值**:
- 成功时返回 `0`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EACCES`: 权限不足。
- `ENOENT`: 文件不存在。
- `EINVAL`: 参数无效。
- `ENOMEM`: 内存不足。

**常见用途**:
- 修改文件或目录的访问权限。
- 实现安全的文件权限管理。

**注意**: 权限模式通常受到进程的 umask 影响，实际权限可能低于指定值。

---

### 63. **LSTAT**
**功能**: 获取符号链接的信息，不会跟随符号链接。

**描述**: `lstat` 系统调用用于获取指定路径的文件状态信息，但不会跟随符号链接。如果路径是符号链接，则返回链接本身的状态信息，而不是链接指向的目标。

**原型**:
```c
int lstat(const char *pathname, struct stat *statbuf);
```

**参数**:
- `pathname`: 要查询的文件或符号链接路径。
- `statbuf`: 指向 `stat` 结构的指针，用于存储文件的状态信息。

**返回值**:
- 成功时返回 `0`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EACCES`: 权限不足。
- `ENOENT`: 文件不存在。
- `EINVAL`: 参数无效。
- `ENOMEM`: 内存不足。

**`struct stat` 包含**:
- `st_mode`: 文件类型和权限。
- `st_ino`: 文件的 inode 号。
- `st_dev`: 文件所在设备。
- `st_nlink`: 链接数。
- `st_uid`: 所有者用户 ID。
- `st_gid`: 所有者组 ID。
- `st_size`: 文件大小。
- `st_atime`: 最后访问时间。
- `st_mtime`: 最后修改时间。
- `st_ctime`: 最后状态改变时间。
- 其他文件属性。

**常见用途**:
- 获取符号链接自身的属性信息。
- 实现符号链接的验证和管理。

**注意**: 如果需要跟随符号链接并获取目标的状态信息，应使用 `stat`。

---

### 64. **EPOLL_CREATE1**
**功能**: 创建 `epoll` 实例，支持指定标志。

**描述**: `epoll_create1` 是 `epoll_create` 的改进版，允许在创建 `epoll` 实例时指定标志，如 `EPOLL_CLOEXEC`，以控制文件描述符的行为。

**原型**:
```c
int epoll_create1(int flags);
```

**参数**:
- `flags`: 控制行为的标志，如 `EPOLL_CLOEXEC`（在执行 `exec` 系统调用时关闭文件描述符）。

**返回值**:
- 成功时返回一个新的 `epoll` 文件描述符。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EINVAL`: 参数无效。
- `ENOMEM`: 内存不足。

**常见用途**:
- 创建带有特定标志的 `epoll` 实例，提高资源管理的灵活性。
- 避免在执行 `exec` 调用后保留不必要的文件描述符。

**注意**: `epoll_create1` 提供了更好的接口和更多的选项，推荐在支持的系统上使用。

---

### 65. **CHOWN**
**功能**: 修改文件或目录的所有者和组。

**描述**: `chown` 系统调用用于更改指定文件或目录的所有者（用户 ID）和组（组 ID）。它允许修改文件的所有权属性。

**原型**:
```c
int chown(const char *pathname, uid_t owner, gid_t group);
```

**参数**:
- `pathname`: 要修改所有者和组的文件或目录路径。
- `owner`: 新的所有者的用户 ID。如果不更改所有者，传递 `-1`。
- `group`: 新的组的组 ID。如果不更改组，传递 `-1`。

**返回值**:
- 成功时返回 `0`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EACCES`: 权限不足。
- `EPERM`: 调用者没有足够的权限更改所有者。
- `ENOENT`: 文件不存在。
- `EINVAL`: 参数无效。
- `ENOMEM`: 内存不足。

**常见用途**:
- 修改文件或目录的所有者或组。
- 实现文件所有权的管理和控制。

**注意**: 只有超级用户（root）或文件的当前所有者可以更改文件的所有者。

---

### 66. **MKNOD**
**功能**: 创建设备文件或普通文件。

**描述**: `mknod` 系统调用用于创建设备文件（字符设备或块设备）、命名管道（FIFO）或普通文件。它根据指定的类型和设备号创建相应的文件节点。

**原型**:
```c
int mknod(const char *pathname, mode_t mode, dev_t dev);
```

**参数**:
- `pathname`: 要创建的设备文件或特殊文件的路径。
- `mode`: 文件类型和权限（如 `S_IFCHR` 表示字符设备，`S_IFBLK` 表示块设备，`S_IFIFO` 表示命名管道）。
- `dev`: 设备号，对于设备文件，指定主设备号和次设备号；对于普通文件，此参数通常为 `0`。

**返回值**:
- 成功时返回 `0`。
- 失败时返回 `-1`，并设置 `errno`。

**错误**:
- `EACCES`: 权限不足。
- `EEXIST`: 文件已存在。
- `EINVAL`: 参数无效。
- `ENODEV`: 指定的设备不存在。
- `ENOSYS`: 文件系统不支持 `mknod`。
- `ENOMEM`: 内存不足。
- `EROFS`: 文件系统只读。

**常见用途**:
- 创建设备文件，以便用户空间程序与设备驱动程序交互。
- 实现命名管道，用于进程间通信。

**注意**: 创建设备文件通常需要超级用户权限。对于普通用户，建议使用 `mkfifo` 创建命名管道。

---

以上是你列出的每个系统调用的详细功能解释。每个系统调用在 Linux 系统编程中扮演着关键角色，理解它们的功能、参数和用法对于开发高效、可靠的应用程序至关重要。如果需要更深入的信息，请参考 [Linux 手册页（man pages）](https://man7.org/linux/man-pages/) 或相关的系统编程资料。