## ps -ef | grep [processName]
* 查看当时的一个进程快照，静态

## top
* 动态显示当时进程的状态

## htop
* 一个查看进程的工具 Ubuntu下可以通过 apt-get install htop 安装


---
## nohup

* 可以将进程调入到后台进行，不挂起 例如

  ``` shell
  nohup wget xxxx.deb &
  #可以不挂起调入后台运行 但是会在当前目录下生成一个nohup.out文件
  ```

  ```shell
  nohup wget xxx.deb >log 2>&1 &
  #可以将输出文件重定向到log文件.
  #可以使用jobs查看任务.
  #可以使用fg %n 关闭任务.
  ```

<a href="http://man.linuxde.net/">man</a>

```html
http://man.linuxde.net/
```