
# LuatOS@Win32

* 底层rtos FreeRTOSv202012.00
* 编译环境msys, 工具cmake/make/gcc
* 文件系统,win32原生文件系统,以工作目录为基点
* 默认luavm和rtos内存分配均为 1MByte

## 简易编译说明

* 下载msys环境, 并安装好gcc和make
* 到Cmake官网下载独立的cmake最新版
* 进入msys环境, cd到本bsp目录,执行 `./build_cmake.sh`

编译完成后, 会在build目录生成 `luatos.exe`

提示: 使用`mingw32.exe`/`mingw64.exe`启动编译环境, 可以编译出不依赖`msys-2.0.dll`的exe文件

https://www.thinbug.com/q/37524839

## 简单用法

* 新建一个目录, 将 `luatos.exe` 拷贝进去(可选,执行时使用全路径也可以)
* 拷贝sys.lua到目录内
* 在目录内新建main.lua, 写入以下内容

```lua
local sys = require "sys"

log.info("sys", "from win32")

sys.taskInit(function ()
    while true do
        log.info("hi", os.date())
        log.info("sys", rtos.meminfo("sys"))
        log.info("lua", rtos.meminfo("lua"))
        sys.wait(1000)
    end
end)

sys.run()

```


