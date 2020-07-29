# **FBox 的订阅与发布主题**

**MQTT 服务端与盒子客户端连通后，现以 MQTT 网页客户端为例，登录 MQTT 网页客户端，可以** 

**进行订阅和发布主题。在 MQTT 客户端可以查看设备的主题 Topic 列表，FLEXEM MQTT 的主题** 

**（以下简称 Topic）均以 json 格式传输。查看设备的主题列表如图：（以盒子 222218030009 为例）**



![订阅与发布主题](images\tupian25.png)

已经订阅的主题，都会在这个地方展示出来。

在 MQTT客户端“Websocket”菜单中进行订阅、发布主题。注意填写内容大小写。



![订阅与发布主题](images\tupian26.png)





## **2.1 发布主题** 

**在 MQTT客户端的订阅处填写这些主题，就会接收到盒子发布的相应的信息。（以盒子**

**222218030009为例，且主题没有自定义，默认是：Topic/flexem/fbox/）**



### **2.1.1实时数据**

  该主题是盒子主动发布的主题，根据默认的发布周期（10s）进行发布，在 MQTT客户端订阅

此主题可以接收到盒子条目的推送。

例：盒子中有监控点，在 MQTT客户端订阅该主题，会接收到盒子中推送的监控点内容：



| 主题 | Topic/flexem/fbox/{盒子序列号}/system/MonitorData  （例：Topic/flexem/fbox/222218030009/system/MonitorData） |
| ---- | ------------------------------------------------------------ |
| 类型 | 发布                                                         |
| 内容 | {"time":"2018-4-26  17:33:16",“data”:[{"name":"Temp","value","124"},{"name":"mqtt_connect","value","1"},{"name":"bit","value","0"}] } |

**"Time":条目监控点推送时间**

**"name":监控点名称**

**"value":监控点的值**



**注意：一个 MQTT报文最大的监控点数量是  50个，当需要上传的监控点数量超过 50之后，盒子**

​            **会分成多个报文推送。分开发送的这几个报文的时间戳是相同的，可以根据这个来组包。**



**在盒子客户端（FlexManager）中可以查看盒子中添加的监控点：**

![订阅与发布主题](images\tupian27.png)



**在“Subscribe-->Topic”填写主题：Topic/flexem/fbox/222218030009/system/MonitorData，点击**

**“Subscribe”，MQTT客户端订阅的主题会展示在右侧列表中，接收到的信息在右下方的“Messages**

**received”列表中，按默认的发布周期接收信息。**



![订阅与发布主题](images\tupian28.png)



**如果要取消订阅该主题，在订阅的主题列表中取消该主题就行了。**



![订阅与发布主题](images\tupian29.png)



### 2.1.2发布盒子相关状态或信息

**当盒子收到一些获取相关信息或状态主题时，则需要以该主题进行发布。 MQTT客户端订阅该主题后，就会获取盒子的相关信息。**



| 主题                | Topic/flexem/fbox/222218030009/system/Status |                  |
| ------------------- | -------------------------------------------- | ---------------- |
| 类型                | 发布                                         |                  |
| 内容                | {状态类型：状态值}                           |                  |
| 状态：Pause         | {"Pause":"Enable"} 或者{"Pause":"Disable"}   | 是否处于暂停     |
| 状态：MDataPubCycle | {"MDataPubCycle":10}                         | 监控点发布周期值 |



**注意：盒子不会主动发布该主题，当盒子收到主题为Topic/flexem/fbox/222218030009/system/GetInfo， 内容为 Pause 或者 MDataPubCycle 时，才会发布盒子相关状态或信息，MQTT 客户端订阅该主题会收到相应的信息。**



**在“Subscribe-->Topic”填写主题：Topic/flexem/fbox/222218030009/system/Status，点击“Subscribe”订阅该主题。在“Messages-->Topic”填写主题：Topic/flexem/fbox/222218030009/system/GetInfo，在“Messages-->Messages”填写点的内容“Pause”，会获取盒子是否处于暂停推送条目状态，填写内容“MDataPubCycle”，会获取盒子监控点发布周期值。**



![订阅与发布主题](images\tupian30.png)

​                                    ![订阅与发布主题](images\tupian31.png)





### 2.1.3发布条目信息列表

**在 MQTT客户端订阅该主题后，就会获取盒子中的监控点信息。**

| 主题 | Topic/flexem/fbox/222218030009/system/Taglist                |
| ---- | ------------------------------------------------------------ |
| 类型 | 发布                                                         |
| 内容 | {"Version":1,"list":[{"name":"Temp"},{"name":"mqtt_connect"},{"name":"bit"},{"name":"single"} ] } |

**注意：盒子不会主动发布该主题，当盒子收到获取盒子信息主题为Topic/flexem/fbox/222218030009/system/GetInfo  并且内容为 Taglist时，表示要获取盒子的条目信息列表，这时盒子才会以  Topic/flexem/fbox/222218030009/system/Taglist  进行发布。**



**在“Subscribe-->Topic”填写主题：Topic/flexem/fbox/222218030009/system/Taglist，点击“Subscribe”订阅该主题。在“Messages-->Topic”填写发布主题：Topic/flexem/fbox/222218030009/system/GetInfo，在“Messages-->Messages”填写点的内容“Taglist”，会获取盒子中所有的监控点条目。**

![订阅与发布主题](images\tupian32.png)





### 2.1.4发布主题列表

**主题列表为系统默认主题，在 MQTT客户端订阅该主题后，可以获取该设备支持的主题列表。其**

**中 sub表示该主题是盒子订阅的主题，pub表示盒子可发布的主题。**





| 主题 | Topic/flexem/fbox/222218030009/system/Topiclist              |
| ---- | ------------------------------------------------------------ |
| 类型 | 发布                                                         |
| 内容 | {"topicVer":  1,"topicList":[{"topicname":  "WriteData","type":  "sub"},{"topicname":  "GetInfo","type":  "sub"},{"topicname":  "Reboot","type":  "sub"},{"topicname":  "Pause","type":  "sub"},{"topicname":  "MDataPubCycle","type":  "sub"},{"topicname":  "MonitorData","type":  "pub"},{“topicname":  "Status","type":  "pub"}{"topicname":  "Taglist","type":  "pub"}{topicname":"Topiclist","type":  "pub"} ]} |

**"topicVer"：**主题版本号.

**"topicList"：**设备支持的主题列表，sub表示该主题是盒子订阅的主题，pub表示盒子可发布的主题,所有主题的前缀都是默认的 

​                       Topic/flexem/fbox/222218030009/system/。因此只需要回复最后一级即可。



**注意：**盒子不会主动发布该主题，同理，当盒子收到获取盒子信息主题 Topic/flexem/fbox/222218030009/system/GetInfo

​            并且内容为 Topiclist时，表示要获取盒子的条目信息列表，这时盒子才会以Topic/flexem/fbox/222218030009/system/Topiclist进行发布。



**在“Subscribe-->Topic”填写主题：Topic/flexem/fbox/222218030009/system/Topiclist，点击“Subscribe”订阅该主题。在“Messages-->Topic”填写发布主题：Topic/flexem/fbox/222218030009/system/GetInfo，在“Messages-->Messages”填写点的内容“Topiclist”，会获取设备持支的主题列表。**



![订阅与发布主题](images\tupian33.png)







## 2.2订阅主题



**以下几个主题为盒子订阅主题，在 MQTT客户端的发布主题处填写这些主题，盒子才可以订阅接收到这些信息。（以盒子 222218030009为例，且主题没有自定义，默认是：Topic/flexem/fbox/）**



### 2.2.1设置监控点

**设置监控点会控制盒子进行监控点的写入操作，目前 FLEXEM  MQTT的写入操作只支持一次写入**

**一条变量值。例：盒子中有名称为“Temp”的监控点，在 MQTT客户端修改其值为  30。**

| 主题 | Topic/flexem/fbox/222218030009/system/WriteData      |
| ---- | ---------------------------------------------------- |
| 类型 | 订阅                                                 |
| 内容 | {"Version":10,"Data":[{"name":"Temp","value":"30"}]} |

**"Version":10：**主题的版本号.

**"name":** 需要修改的监控点名称.

**"value":** 需要修改监控点的值.



**在“  Messages-->Topic”填写主题：     Topic/flexem/fbox/222218030009/system/WriteData ，在“Messages-->Messages”填写修改监控点的内容，点击发送“send”，盒子收到该主题后，并进行写值操作。**

![订阅与发布主题](images\tupian34.png)

***注意：***在登记条目的时候，切勿使用相同 name的条目MQTT不支持字符串条目



### 2.2.2暂停数据推送

**服务器可以暂停 MQTT的实时数据的发布。也可以通过此主题打开取消暂停实时数据的发布。**

| 主题 | Topic/flexem/fbox/222218030009/system/Pause |
| ---- | ------------------------------------------- |
| 类型 | 订阅                                        |
| 内容 | "Enable"或者  "Disable"                     |

**"Enable"：**表示暂停当前所有实时数据的发布。

**"Disable"：**表示取消暂停，实时数据继续发布。

**在“Messages-->Topic”填写主题：Topic/flexem/fbox/222218030009/system/Pause，在“Messages-->Messages”中填写"Enable"或者  "Disable"，盒子接收到主题，根据内容会“暂停”或者“取消暂停”监控条目的推送。**



**以暂停推送条目为例：**

![订阅与发布主题](images\tupian35.png)

**注意：不支持对单个条目的暂停推送**



### 2.2.3重启盒子

盒子收到该主题后，会立即进行重启，此时 MQTT服务器应主动断开现有链接，释放已经订阅的主题。盒子重启登录后，会重新注册设备，获取列表等。

| 主题 | Topic/flexem/fbox/222218030009/system/Reboot |
| ---- | -------------------------------------------- |
| 类型 | 订阅                                         |
| 内容 | "True"（内容可以为空）                       |

**在“Messages-->Topic”填写主题：Topic/flexem/fbox/222218030009/system/Reboot，在“Messages-->Messages”中填写“True”（可以为空），盒子收到该命令后，会立即进行重启。**

![订阅与发布主题](images\tupian36.png)

**注意：如果 MQTT客户端多次发布该主题，则在盒子再次登录的时候，MQTT服务器仍会再继续发送没有传输完成的报文。**

比如：MQTT客户端连续发送了  10次重启命令。盒子收到一次重启命令后，立即重启，此时  MQTT服务器仍记录还有  9次重启命令未传达，在下次盒子启动后，MQTT将继续发送。



### 2.2.4立即让盒子发布监控点

盒子收到该主题后，则立即发布 Topic/flexem/fbox/222218030009/system/MonitorData主题，内容为当前要采集的条目的值.

| 主题 | Topic/flexem/fbox/222218030009/system/MDataPubNow |
| ---- | ------------------------------------------------- |
| 类型 | 订阅                                              |
| 内容 | 任意内容，可以为空                                |

**如果设置的监控条目周期比较长，但又想立即获取监控条目，客户端可发布该主题，当  FBox收到该主题后，会以** 

**Topic/flexem/fbox/222218030009/system/MonitorData主题进行发布监控条目。先在“Subscribe-->Topic”填写主题：**

**Topic/flexem/fbox/222218030009/system/MonitorData，获取盒子的监控点，便于观察修改发布周期后监控点的发送。**

**在“Messages-->Topic”填写主题：Topic/flexem/fbox/222218030009/system/MDataPubNow，点击发送，就可以立即得到盒子监控点数据。**

![订阅与发布主题](images\tupian37.png)



### 2.2.5设置监控点条目发布周期 

​                 **允许通过主题交互形式设置监控点的发布周期。**

| 主题 | Topic/flexem/fbox/222218030009/system/MDataPubCycle |
| ---- | --------------------------------------------------- |
| 类型 | 订阅                                                |
| 内容 | 5                                                   |

**先在“Subscribe-->Topic”填写主题：Topic/flexem/fbox/222218030009/system/MonitorData，获取盒子的监控点，便于观察修改发布周期后监控点的发送。**

**在“Messages-->Topic”填写主题：Topic/flexem/fbox/222218030009/system/MDataPubCycle，在“Messages-->Messages”中填写“5”（修改的发布周期，单位：S），盒子收到该命令后，就会立即修改监控点的发布周期。**

![订阅与发布主题](images\tupian38.png)



### 2.2.6设置单个或多个监控点条目发布周期

在 MQTT客户端发布该主题，设置的单个或多个监控点就会按照设置的发布周期进行发布，如果没有使用该主题设置过的监控条目周期，会使用默认周期或者使用  MDataPubCycle设置的周期。当设置为 0时，监控条目使用全局的发布周期。

| 主题 | Topic/flexem/fbox/222218030009/system/MDPCS                  |
| ---- | ------------------------------------------------------------ |
| 类型 | 订阅                                                         |
| 内容 | {"cycle":10,"num":3,"item":["ItemName1","ItemName2","ItemName3"]  } |

**"cycle":**  修改的发布周期时间，单位：s   。

**"num":** 设置修改的监控点的数量。

**"item":** 监控点条目的名称。

**先在“Subscribe-->Topic”填写主题：Topic/flexem/fbox/222218030009/system/MonitorData，获取盒子的监控点，便于观察修改发布周期后监控点的发送。**

**在“Messages-->Topic”填写主题：Topic/flexem/fbox/222218030009/system/MDPCS，在“Messages-->Messages”中填写对应的内容，盒子接收到该主题后，会改变设置的监控点的推送周期。**

![订阅与发布主题](images\tupian39.png)



### 2.2.7获取盒子相关状态或信息

当盒子收到不同的获取信息后，以指定的主题发布。这个主题在前文中均有用到。

| 主题          | Topic/flexem/fbox/222218030009/system/GetInfo |
| ------------- | --------------------------------------------- |
| 类型          | 订阅                                          |
| Taglist       | 获取当前条目列表                              |
| Topiclist     | 获取当前盒子的主题（订阅和可发布）            |
| Pause         | 获取当前盒子的暂停状态（是否处于暂停）        |
| MDataPubCycle | 获取当前盒子监控条目的推送周期                |

**1.**   **Taglist ：** 

Topic/flexem/fbox/300216080083/system/GetInfo    Taglis

当盒子收到该主题和内容后，则发布 Topic/flexem/fbox/222218030009/system/Taglist主题，内容为：

{

"Version":1,

"list":[{"name":"Temp"},

{"name":"mqtt_connect"},

{"name":"bit"},

{"name":"single"}

​      ]

}

![订阅与发布主题](images\tupian40.png)



**2.**   **Topiclist获取当前盒子的主题：**

Topic/flexem/fbox/300216080083/system/GetInfo   Topiclist

当盒子收到该主题和内容后，则发布  Topic/flexem/fbox/222218030009/system/Topiclist主题，内容为

{"topicVer":  1,

"topicList":  [

{"topicname":  "WriteData","type": "sub"},

{"topicname":  "GetInfo","type": "sub"},

{"topicname":  "Reboot","type": "sub"},

{"topicname":  "Pause","type": "sub"},

{"topicname":  "MDataPubCycle","type": "sub"},

{"topicname":  "MonitorData","type": "pub"},

{"topicname":  "Status","type": "pub"},

{"topicname":  "Taglist","type": "pub"},

{"topicname":  "Topiclist","type": "pub"},

]}

所有主题的前缀都是默认的 Topic/flexem/fbox/222218030009/system/，因此只需要回复最后一级即

可。

![订阅与发布主题](images\tupian41.png)



**3.**   **Pause获取当前盒子的暂停状态（是否处于暂停）**

Topic/flexem/fbox/222218030009/system/GetInfo    Pause

当盒子收到该主题及内容时，则发布 Topic/flexem/fbox/222218030009/system/Status主题，内容为{"Pause":"Enable"}或者{"Pause":"Disable"}

![订阅与发布主题](images\tupian42.png)



**4.**   **MDataPubCycle获取当前盒子监控条目的推送周期**

Topic/flexem/fbox/222218030009/system/GetInfo     MDataPubCycle

当盒子收到该主题及内容时，则发布 Topic/flexem/fbox/222218030009/system/Status主题，内容为：{"MDataPubCycle ":10}

![订阅与发布主题](images\tupian43.png)

