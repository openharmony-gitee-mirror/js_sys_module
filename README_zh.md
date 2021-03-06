# js_sys_module子系统/组件

-   [简介](#简介)
-   [目录](#目录)
-   [说明](#说明)
    -   [接口说明](#接口说明)
    -   [使用说明](#使用说明)

-   [相关仓](#相关仓)

## 简介
process主要是获取进程的相关id以及获取和修改进程的工作目录，及进程的退出关闭。通过childprocess对象可以用来创建一个新的进程，主进程可以获取子进程的标准输入输出，以及发送信号和关闭子进程。 
## 目录

```
base/compileruntime/js_sys_module/
├── Class:PROCESS                   # PROCESS类
├── uid                             # uid属性
├── gid                             # gid属性
├── euid                            # euid属性
├── egid                            # egid属性
├── groups                          # groups属性
├── pid                             # pid属性
├── ppid                            # ppid属性
├── chdir()                         # chdir方法
├── uptime()                        # uptime方法
├── kill()                          # kill方法
├── abort()                         # abort方法
├── on()                            # on方法
├── exit()                          # exit方法
├── cwd()                           # cwd方法
├── off()                           # off方法
├── tid                             # tid方法
├── getStartRealtime()              # getStartRealtime方法
├── getAvailableCores()             # getAvailableCores方法
├── getPastCputime()                # getPastCputime方法
├── isIsolatedProcess()             # isIsolatedProcess方法
├── is64Bit()                       # is64Bit方法
├── isAppUid()                      # isAppUid方法
├── getUidForName()                 # getUidForName方法
├── getThreadPriority()             # getThreadPriority方法
├── getSystemConfig()               # getSystemConfig方法
├── getEnvironmentVar()             # getEnvironmentVar方法
├── runCmd()                        # runCmd方法
└─── Class:CHILDPROCESS             # CHILDPROCESS类
    ├── close()                     # close方法
    ├── kill()                      # kill方法
    ├── getOutput()                 # getOutput方法
    ├── getErrorOutput()            # getErrorOutput方法
    ├── wait()                      # wait方法
    ├── killed                      # killed属性
    ├── pid                         # pid属性
    ├── ppid                        # ppid属性
    └── exitCode                    # exitCode属性
```

## 说明

### 接口说明
| 接口名 | 说明 |
| -------- | -------- |
| const uid :number | 返回进程的数字用户标识。 |
| const gid :number | 返回进程的数字组标识。 |
| const euid :number | 返回进程的数字有效用户身份。 |
| const egid :number | 返回 Node.js 进程的数字有效组标识。 |
| const groups :number[] | 返回一个带有补充组 ID 的数组。 |
| const pid :number | 返回进程的 PID。 |
| const ppid :number | 返回当前进程的父进程的 PID。                                 |
| chdir(dir:string) :void | 更改 Node.js 进程的当前工作目录。 |
| uptime() :number | 返回当前系统已运行的秒数。 |
| Kill(pid:number, signal:number) :boolean | 将signal信号发送到标识的进程 PID，true代表发送成功。 |
| abort() :void | 会导致 Node.js 进程立即退出并生成一个核心文件。 |
| on(type:string ,listener:EventListener) :void | 用来存储用户所触发的事件。 |
| exit(code:number):void | 会导致 Node.js 进程立即退出。 |
| cwd():string | 返回 Node.js 进程的当前工作目录。 |
| const tid :number | 返回进程的TID。 |
| getStartRealtime() :number | 获取从系统启动到进程启动所经过的实时时间（以毫秒为单位）。 |
| getAvailableCores() :number[] | 获取多核设备上当前进程可用的 CPU 内核。 |
| getPastCputime() :number | 获取进程启动到当前时间的CPU时间（以毫秒为单位）。 |
| isIsolatedProcess(): boolean | 检查进程是否被隔离。 |
| is64Bit(): boolean | 检查进程是否在 64 位环境中运行。 |
| isAppUid(v:number): boolean | 检查指定的 UID 是否属于特定应用程序。 |
| getUidForName(v:string): number | 根据用户名获取用户所属的用户组ID。 |
| getThreadPriority(v:number): number | 根据指定的 TID 获取线程优先级。 |
| getSystemConfig(name:number): number | 根据指定的系统配置名称获取系统的配置。 |
| getEnvironmentVar(name:string): string | 根据环境变量的名称获取对应的值。 |
| runCmd(command: string, options?: { timeout : number, killSignal : number \| string, maxBuffer : number }): ChildProcess | 通过runcmd可以fork一个新的进程来运行一段shell，并返回ChildProcess对象。第一个参数command指需要运行的shell，第二个参数options指子进程的一些运行参数。这些参数主要指timeout、killSignal、maxBuffer 。如果设置了timeout则子进程会在超出timeout后发送信号killSignal，maxBuffer用来限制可接收的最大stdout和stderr大小。 |
| wait():Promise\<number> | 用来等待子进程运行结束，返回promise对象，其值为子进程的退出码。 |
| getOutput(): Promise\<Uint8Array> | 用来获取子进程的标准输出。 |
| getErrorOutput(): Promise\<Uint8Array> | 用来获取子进程的标准错误输出。 |
| close(): void | 用来关闭正在运行的子进程。 |
| kill(signal: number \| string): void | 用来发送信号给子进程。 |
| readonly killed: boolean | 表示信号是否发送成功，true代表发送成功。 |
| readonly exitCode: number | 表示子进程的退出码。 |
| readonly pid: number | 代表子进程ID。 |
| readonly ppid: number | 代表主进程ID。 |

### 使用说明

各接口使用方法如下：
1.uid() 
```
uid(){
    var res =  Process.uid;
}
```
2.gid()
```
gid(){
    var result = Process.gid;
}
```
3.euid()
```
euid(){
    var ans = Process.euid;
}
```
4.egid()
```
egid(){
    var resb = Process.egid;
}
```
5.groups()
```
groups(){
    var answer = Process.groups;
}
```
6.pid() 
```
pid(){
    var result = Process.pid;
}
```
7.ppid()
```
ppid(){
    var result = Process.ppid;
}
```
8.chdir()
```
chdir(){
    Process.chdir("123456");
}
```
9.uptime()
```
uptime(){
    var num = Process.uptime();
}
```
10.kill()
```
kill(){
    var ansu = Process.kill(5,23);
}
```
11.abort()
```
abort(){
    Process.abort();
}
```
12.on()
```
on(){
    function add(num){
        var value = num + 5;
        return value;
    }
    Process.on("add",add);
}
```
13.exit()
```
exit(){
    Process.exit(15);
}
```
14.Cwd()
```
Cwd(){
    var result = Process.cwd();
}
```
15.off()

```
off(){
    var result =  Process.off("add");
}
```
16.runCmd()
```
runCmd(){
    var child = process.runCmd('echo abc')
    //killSignal可以是数字或字符串
    var child = process.runCmd('echo abc;', {killSignal : 'SIGKILL'});
    var child = process.runCmd('sleep 5; echo abc;', {timeout : 1, killSignal : 9, maxBuffer : 2})
}
```
17.wait()
```
wait()
{
    var child = process.runCmd('ls')
    var status = child.wait();
    status.then(val => {
        console.log(val);
    })
}
```
18.getOutput()
```
getOutput(){
    var child = process.runCmd('echo bcd;');
    var res = child.getOutput();
    child.wait();
    res.then(val => {
        console.log(val);
    })
}
```
19.getErrorOutput()
```
getErrorOutput(){
    var child = process.runCmd('makdir 1.txt'); //执行一个错误命令
    var res = child.getErrorOutput();
    child.wait();
    res.then(val => {
        console.log(val);
    })
}
```
20.close()
```
close(){
    var child =  process.runCmd('ls; sleep 5s;')
    var result = child.close()
}
```
21.kill()
```
kill(){
    var child =  process.runCmd('ls; sleep 5s;')
    var result = child.kill('SIGHUP');
    child.wait();
    var temp = child.killed;
}
```
22.killed
```
{
    var child = process.runCmd('ls; sleep 5;')
    child.kill(3);
    var killed_ = child.killed;
    child.wait();
}
```
23.exitCode
```
{
    var child = process.runCmd('ls; sleep 5;')
    child.kill(9);
    child.wait();
    var exitCode_ = child.exitCode;
}
```
24.pid
```
pid
{
    var child = process.runCmd('ls; sleep 5;')
    var pid_ = child.pid;
    child.wait();
}
```
25.ppid
```
ppid
{
    var child = process.runCmd('ls; sleep 5;')
    var ppid_ = child.ppid;
    child.wait();
}
```
26.tid()
```
tid(){
    var ansu = Process.tid;
}
```
27.isIsolatedProcess()
```
isIsolatedProcess(){
    var ansu = Process.isIsolatedProcess()();
}
```
28.isAppUid()
```
isAppUid(){
    var ansu = Process.isAppUid(10000);
}
```
29.is64Bit()
```
is64Bit(){
    var ansu = Process.is64Bit();
}
```
30.getUidForName()
```
getUidForName(){
    var buf = "root";
    var ansu = Process.getUidForName(buf);
}
```
31.getEnvironmentVar()
```
getEnvironmentVar(){
    var ansu = Process.getEnvironmentVar('USER');
}
```
32.getAvailableCores()
```
getAvailableCores(){
    var ansu = Process.getAvailableCores();
}
```
33.getThreadPriority()
```
getThreadPriority(){
    var result = Process.getTid();
    var ansu = getThreadPriority(result);
}
```
34.getStartRealtime()
```
getStartRealtime(){
    var ansu = Process.getStartRealtime();
}
```
35.getPastCputime()
```
getPastCputime(){
    var ansu = Process.getPastCputime();
}
```
36.getSystemConfig()
```
getSystemConfig(){
    var _SC_ARG_MAX = 0;
    var ansu = Process.getSystemConfig(_SC_ARG_MAX)
}
```

## 相关仓

[js_sys_module子系统](https://gitee.com/OHOS_STD/js_sys_module)

[base/compileruntime/js_sys_module/](base/compileruntime/js_sys_module-readme.md)
