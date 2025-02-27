进一步配置环境，可以成功使用 vscode 连接到 docker 容器内部，使用相关插件进行开发。

复现了对 starry-next 新支持的 riscv64 和 loongarch64 的 basic 测例支持，可以在线评测和在本地使用 docker 构建环境评测。

其中， testsuits-for-oskernel 中的makefile有问题，需要把 sdcard 中的一处 riscv64 改成 loongarch ，才能成功构建测例。