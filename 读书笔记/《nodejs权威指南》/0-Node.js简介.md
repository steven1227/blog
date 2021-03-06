## Node.js简介

### Node.js架构简介

Node.js用异步I/O和事件驱动代替多线程，带来了客观的性能提升。Node.js除了使用V8作为JavaScript引擎以外，还使用了高效的libev和libeio库支持事件驱动和异步I/O。

Node.js的开发者在libev和libeio的基础上抽象出了层libuv。对于POSIX操作系统，libuv通过封装libev和libeio来利用epoll或kqueue。而在Windows下，libuv使用了Windows的IOCP机制，以在不同的平台下实现同样的性能。

![Node.js的结构](https://raw.githubusercontent.com/blackcater/blog/master/%E8%AF%BB%E4%B9%A6%E7%AC%94%E8%AE%B0/%E3%80%8Anodejs%E6%9D%83%E5%A8%81%E6%8C%87%E5%8D%97%E3%80%8B/images/Node.js%E7%9A%84%E7%BB%93%E6%9E%84.PNG)



### CommonJS规范

CommonJS规范包括了模块（modules），包（packages），系统（system），二进制（binary），控制台（console），编码（encoding），文件系统（filesystems），套接字（sockets），单元测试（unit testing）等部分。