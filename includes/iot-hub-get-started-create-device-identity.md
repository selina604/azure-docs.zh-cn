## <a name="create-a-device-identity"></a>创建设备标识

本部分使用名为 [iothub-explorer][iot-hub-explorer] 的 Node.js 工具为本教程创建设备标识。 设备 ID 区分大小写。

1. 在命令行环境中运行以下命令：

    `npm install -g iothub-explorer@latest`

1. 然后，运行以下命令登录到中心。 将 `{iot hub connection string}` 替换为前面复制的 IoT 中心连接字符串：

    `iothub-explorer login "{iot hub connection string}"`

1. 最后，以下使用命令创建名为 `myDeviceId` 的新设备标识：

    `iothub-explorer create myDeviceId --connection-string`

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

记下结果中的设备连接字符串。 设备应用使用此设备连接字符串以设备身份连接到 IoT 中心。

![][img-identity]

若要以编程方式创建设备标识，请参阅 [IoT 中心入门][lnk-getstarted]。

<!-- images and links -->
[img-identity]: media/iot-hub-get-started-create-device-identity/devidentity.png

[iot-hub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md

[lnk-getstarted]: ../articles/iot-hub/quickstart-send-telemetry-dotnet.md
