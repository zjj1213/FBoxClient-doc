# **MQTT参数规范**

**说明：下文中的参数都是内部变量属性参数，用于MQTT功能上进行交互的参数，是由繁易定义的参数信息；参数名称不可修改，默认情况下使用默认参数名，一旦修改内部变量参数名称将不执行对应功能；**


**标准参数属性格式定义和说明：**

| **参数默认名**               | **类型**                    | **说明**                                                     |
| ---------------------------- | --------------------------- | ------------------------------------------------------------ |
| **flexem_timestamp**         | **Long(默认)/String**       | **时间戳**                                                   |
| **flexem_pause**             | **boolean**                 | **暂停MQTT数据推送**                                         |
| **flexem_reboot**            | **boolean**                 | **该数据段表示是否重启FBOX**                                 |
| **flexem_push_interval**     | **unsigned integer**        | **该数据段表示需要设置监控点数据的发布周期（单位：ms）**     |
| **flexem_push_mode**         | **string**                  | **数据推送方式（“interval”:周期推送，”change”:变化推送）**   |
| **flexem_push_alarm**        | **boolean**                 | **该数据段表示是否启用报警点信息上报功能**                   |
| **flexem_get_info**          | **string**                  | **该数据段表示需要获取盒子的一些状态信息（“location” 获取位置信息，“status” 获取状态信息）** |
| **flexem_info_type**         | **string**                  | **该数据段表示需要发布盒子的一些信息的类型（“location” 发布位置信息，“status” 发布状态信息）** |
| **flexem_sim_lac**           | **unsigned integer/string** | **基站-位置区域码（也叫，小区号）**                          |
| **flexem_sim_ccid**          | **unsigned integer/string** | **基站-基站编号**                                            |
| **flexem_sim_mcc**           | **unsigned integer/string** | **基站-移动国家号码**                                        |
| **flexem_sim_mnc**           | **unsigned integer/string** | **基站-移动网络号码**                                        |
| **flexem_longitude**         | **float/string**            | **GPS信息-经度信息**                                         |
| **flexem_latitude**          | **float/string**            | **GPS信息-纬度信息**                                         |
| **flexem_fcs_ver**           | **unsigned integer/string** | **该数据段表示FBox内Fcs的代码版本**                          |
| **flexem_floader_ver**       | **unsigned integer/string** | **该数据段表示FBox内Floader的代码版本**                      |
| **flexem_fds_ver**           | **unsigned integer/string** | **该数据段表示FBox内Fds的代码版本**                          |
| **flexem_alarm**             | **string**                  | **报警触发类型（“alarm”-触发报警，“restore”-报警恢复）**     |
| **flexem_get_picture**       | **boolean**                 | **获取图片信息（true-获取，false-停止获取）**                |
| **flexem_picture_base64**    | **string**                  | **图片的信息，以base64格式发送**                             |
| **flexem_message_id**        | **Long（默认）/String**     | **客户自定义数值字段，返回时会原样返回改数值。可用于识别数据包。** |
| **flexem_mqtt_ver**          | **unsigned integer/string** | **该数据段表示fbox内MQTT的代码版本**                         |
| **flexem_message**           | **String**                  | **操作后返回状态的文字描述**                                 |
| **flexem_error_code**        | **Integer/string**          | **操作后返回的状态码**                                       |
| **flexem_mac**               | **string**                  | **MAC地址**                                                  |
| **flexem_sn**                | **string**                  | **盒子/屏的序列号**                                          |
| **flexem_password**          | **string**                  | **盒子/屏的密码**                                            |
| **flexem_online_sta**        | **integer**                 | **盒子在线状态**                                             |
| **flexem_net_type**          | **integer**                 | **盒子联网类型**                                             |
| **flexem_wireless**          | **integer**                 | **盒子无线信号强度**                                         |
| **flexem_vnc_op_password**   | **string**                  | **VNC操控密码**                                              |
| **flexem_vnc_mo_password**   | **string**                  | **VNC监控密码**                                              |
| **flexem_connect_sta**       | **boolean**                 | **网络连接状态**                                             |
| **flexem_sd_card_sta**       | **boolean**                 | **SD卡插入状态**                                             |
| **flexem_usb_sta**           | **boolean**                 | **U盘插入状态**                                              |
| **flexem_usb_down_line_sta** | **boolean**                 | **USB下载线连接状态**                                        |

​                                                            





##  附录1：状态码说明

| flexem_error_code | flexem_message                                      | 说明                             |
| ----------------- | --------------------------------------------------- | -------------------------------- |
| 200               | success                                             | 请求成功                         |
| 400               | Request error                                       | 内部服务错误，处理时发生内部错误 |
| 460               | Request parameter error                             | 内部服务错误，处理时发生内部错误 |
| 429               | Too many requests                                   | 请求过于频繁                     |
| 401               | Serial port did not get the image data(not picture) | 串口错误，无法获取图片信息       |

