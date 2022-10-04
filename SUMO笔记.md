# 结果输出

* vehicle-based informantion, disaggregated(以车辆为基础的信息，非集计数据)
* simulated detectors(模拟检测器)
  * Inductive loop detectors(E1)：电磁感应圈
  * Instantaneous induction loops detectors
  * Lane area detectors(E2)：detectors that capture a lane segment：瞬时电磁感应圈
  * Multi-Entry-Exit detectors(E3)：simulators that track traffic in an area by detecting entry and exit events at defined locations

## 模拟检测器

### 1. Inductive loops detetors (E1)

设置在**断面**的检测器，具体到特定车道(lane)的具体位置(pos)

可以输出的主要指标：
| 变量名 | 描述 |
|--|--|
|flow|完全穿越检测器的车辆流量，单位vehicles/hour|
|speed|时间平均车速，单位m/s|
|harmonicMeanSpeed|空间平均车速，单位m/s|
|length|完全穿越检测器的车辆平均长度|
|occupancy|占有率，检测器被车辆占用的时间与观测时段长的比值，0-100%|
|nVehEntered|接触过检测器的车辆数|

车辆检测器一般只对**完全穿越检测器**的车辆进行数据采集和计算，因此换道车辆可能不会被计入。

traci提供调用支持。

### 2. Instantaneous induction loops detectors

同样是**断面**检测器。

该检测器根据state分为三种：

* "enter"：车辆进入检测器的仿真步
* "stay"：车辆进入检测器后还处于检测器中的仿真步
* "leave"：车辆离开检测器的仿真步

可以输出的主要指标：
| 变量名 | 描述 |
|--|--|
|time|事件发生的仿真步|
|speed|车辆瞬时车速，单位m/s|
|length|车辆长度，单位m|
|type|车辆类型|
|gap|车头时距，当state为"enter"时输出，单位s|
|occupancy|车辆穿越检测器的时间，当state为"leave"时输出，单位s|

traci不支持Instantaneous induct loops。当使用traci时，可以每秒使用Induction loops作为代替。

### 3. Lanearea detectors (E2)

**车道**级别的检测器,可以采集车道特定长度上的数据。

主要用来评估拥堵、排队长度等。

可以输出的主要指标：
| 变量名 | 描述 |
|--|--|
|sampledSeconds|采集时间内对每秒在车道上的车辆加和，即采集样本数|
|nVehEntered|进入检测器的车辆数|
|nVehLeft|离开检测器的车辆数|
|nVehSeen|检测器观察到的车辆数|
|meanSpeed|平均速度(实际为空间平均车速)，单位m/s|
|meanOccupancy|平均空间占有率，0-100%|
|maxJamLengthInVehicles|最大拥堵长度，以车辆数为单位|
|meanHaltingDuration|平均等待时间|
|meanVehicleNumber|检测器观察到的平均车辆数|

traci提供调用支持。

### 4. Multi-Entry-Exit Detectors (E3)

利用一系列Entry和Exit描述的检测器。

可以输出的主要指标：
| 变量名 | 描述 |
|--|--|
|meanTravelTime|车辆穿越区域所需时间(车辆前身进入区域)|
|meanSpeed|平均车速(实际为空间平均车速)，单位m/s|
|meanHaltsPerVehicle|已穿越检测区域车辆的平均等待时间|
|meanTimeLoss|已穿越检测区域车辆的平均时间损失|
|vehicleSum|已离开检测区域的车辆总数|

路径完全包含在检测区域中的车辆不会被计入检测样本中。

traci提供调用支持。

### 5. RouteProbe

定义在edge上的检测器，用来检测路径分布。
