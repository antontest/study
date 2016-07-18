### PCI层和网络接口卡


### 目录


#### 本章涉及的数据结构
PCI使用的关键数据结构定义哎`include/linux/mod_devicetable.h`中，另外两个定义在`include/linux/pci.h`中。   

- `pci_device_id`
  > 设备标识符；

- `pci_dev`
  > 每个PCI设备都会被分配一个`pci_dev`实例；

- `pci_driver`
  > 定义PCI层和设备驱动层之间的接口；这个结构主要由函数指针组成；

- `char *name`
  > 驱动程序名称；

- `const struct pci_device_id *id_table`
  > 这是一个ID向量，内核用于把一些设备关联到此驱动程序；

- `int (*probe) (struct pci_dev *dev, const struct pci_device_id *id)`
  > 当PCI层发现它正在搜寻驱动程序的ID和id_table中的相匹配时，就会调用此函数；该函数会开启硬件、分配`net_device`结构、初始化并注册新设备；

- `void (*remove) (struct pci_dev *dev)`
  > 当驱动程序从内核中被除名时，或者当可热拔插设备被删除时，PCI层就会调用该函数；用于清理释放已分配的I/O端口和I/O内存、释放`net_device`数据结构等；

- `int (*suspend) (struct pci_dev *dev, pm_message_t state)`
- `int (*resume) (struct pci_dev *dev)`
  > 当系统进入挂起模式或者重新继续时，PCI层就会调用该函数；

- `int (*enable_work) (struct pci_dev *dev, u32 state, int enable)`
  > 使用该函数，驱动程序可以通过产生特定的电源管理事件信号；

#### PCI NIC设备驱动程序的注册
PCI设备独一无二的识别方式是通过一些参数的组合，包括开发商以及模型等来完成的。这些参数由内核存储在`pci_device_id`类型的数据结构中，定义如下：  

```c
    struct pci_device_id {
        unsigned int vendor, device;
        unsigned int subvendor, subdevice;
        unsigned int class, class_mask;
        unsigned long driver_data;
    }
```

*字段说明*：  

- `vendor`和`device`识别设备；
- `subvendor`和`subdevice`一般很少用，通常为通配符(`PCI_ANY_ID`)；
- `class`和`class_mask`代表该设备所属的类；
- `driver_data`是驱动程序所使用的一个私有参数；

每个设备驱动程序都会把一个pci_device_id实例注册到内核，这个实例列出了其所能处理的设备ID。  
PCI设备驱动的注册与除名由`pci_register_driver`和`pci_unregister_driver`完成。这些函数在`drivers/pci/pci.c`中定义。  
PCI的优点之一就是其支持寻找IRQ和每个设备所需的其他资源的探测方式相当优雅。  

PCI探测方式有两种：  

- 静态
  > 给定一个设备PCI ID，内核就能根据id_table向量查询出正确的PCI驱动程序；

- 动态
  > 这种查询是根据用户手动配置的ID，该情况在实际情况中很少见。

#### 电源管理和网络唤醒
PCI电源管理事件由`pci_driver`数据结构的`suspend`和`resume`函数处理：  

- `suspend`主要停止设备出口队列，使得该设备无法再传输；
- `resume`重启出口队列，使得该设备得以再次传输；

网络唤醒(Wake-on-Lan, WOL)是一种功能，允许NIC在接收到一种特殊类型的帧时唤醒处于待命模式的系统。  
WOL通常是关闭的，可以通过用pci_enable_wake打开或关闭。  
WOL可以唤醒系统的数据帧叫“魔术封包”，该类型帧有两个特点：  

- 目的MAC地址属于正在接收的NIC，无论是单薄、多播还是广播；
- 帧中的某处会设置一段48位序列（也就是FF:FF:FF:FF:FF:FF）,后面再接NIC MAC地址，在一行中至少连续重复16次；

#### 大蓝图
PCI设备驱动的工作流程：  

- 当系统引导时，会建立一种数据库，把每个总线都关联一份已侦测到而使用该总线的设备列表, 每个设备由`pci_device_id`结构唯一标识。  
- 当设备驱动程序被加载时，调用`pci_register_driver`并提供其`pci_driver`实例与PCI层注册。`pci_driver`中内含一个设备ID的向量;  
- 接着PCI层使用该表去查看自己在已侦测到的PCI设备列表中与哪些设备匹配。于是就会建立该驱动程序的设备列表。  
- 对每个设备而言，PCI层会调用相匹配的驱动程序中的`pci_driver`结构中所提供的`probe`函数。`probe`函数会建立并注册相关联的网络设备。  
