# 基于STM32F103C8T6的模拟电路处理后的ADC采样&处理  
🏠个人的水平有限不要嘲笑我  
☀️电路图的设计 -> 电路板的设计 -> 元件器的购买 -> 焊接 -> 代码的编写 -> 测试，这些流程都走了一遍  
⚡可以把这个小项目当作一个练习
***
## 电流采样&电压采样的工作原理  
具体的工作原理可以下载压缩包后查看里面的详细的工作原理图  
主要利用ADC固件进行ADC的采集12位
（0 - 4095），采样的数据有二分之一的输入电压，小电阻采集到的电压进行处理后的电压（这个电压经过处理之后得到的就是相对于二分之一处理器芯片的工作电压）  
另外应该是再采集一个小电阻采集时的参考电压  
***
## 电路板的硬件模块  
<img width="565" alt="硬件组成" src="https://github.com/user-attachments/assets/3a0a7146-c043-414f-b359-95b208a41e95" />    

***  

## CubeMx  
1️⃣UART 115200 直接异步通信就可以了  
2️⃣IIC  直接开启就可以了
> 不过好像电路中的SCL与SDA线接错了，所以我又采用了软件模拟IIC的方式来跟显示屏通信

3️⃣ADC  
4️⃣EXIT  别忘了配置NVIC    
***

## 代码
😟代码写得很烂，不想展示。
```c
	HAL_ADCEx_Calibration_Start(&hadc1);//进入while前都要校准模数转换器
```

代码的框架如下：  
![image](https://github.com/user-attachments/assets/503992b9-2908-4373-bbf4-ef852638682f)  
***  

## 焊接
这就是一个熟能生巧的过程，希望大家都可以成为焊武帝  
个人觉得焊得还不错：  
![image](https://github.com/user-attachments/assets/6d02b238-1ff2-44dd-af27-ac60194a745f)  

## 测试
🐱对采样电路的电压测量
![image](https://github.com/user-attachments/assets/5a99a610-fb02-4b72-9f90-46f9af5613e2)  
测的时候，黑笔直接按在了USB上可能测量得有一定的误差，图三与图二的差就是电流的值  
🐶看一下显示屏的耗电  
![image](https://github.com/user-attachments/assets/ecd15b1d-ea02-42cf-b9c5-575dd3bbfa99)  
大概10mA左右，看了数据手册差不多

🐰当我去测量手机快充时，电流好像有点大把保险丝烧坏了😨





