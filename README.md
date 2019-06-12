# Azure IoT C SDK Compilation on VAR-SOM-MX7 : NXP/Freescale iMX7

## Microsoft Azure IoT Device SDK for C
#### [Microsoft Azure IoT Device SDK for C](https://azure.github.io/azure-iot-sdk-c/index.html) 
## WiFi Setup
``
 nano /etc/wpa_supplicant.conf
``
```ruby
 network={
         ssid="wifi_name"
         psk="wifi_key"
}
```
 kill every wpa_supplicant and dhclient task before!!!
```ruby
ip link set wlan0 down
ip link set wlan0 up
wpa_supplicant -B -iwlan0 -c /etc/wpa_supplicant.conf
```
 
In a different terminal
``
dhclient wlan0
``
Once internet acces is verified
## Azure IoT dev apt-get
```ruby
ap-get update
apt-get install -y git 
apt-get install -y cmake
apt-get install -y build-essential
apt-get install -y curl
apt-get install -y libcurl4-openssl-dev
apt-get install -y libssl-dev
apt-get install -y uuid-dev
```
### https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client 
### https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-device-sdk-c-intro



### Install rsync
```
ap-get update
apt-get install rsync
```
 
### sync usr and lib into development machine
``
rsync -rl --safe-links pi@<your Pi identifier>:/{lib,usr} /home/sergio/usr_lib.DEV/
``
 
### openssl path setup
in home/.profile add
``
export OPENSSL_ROOT_DIR=/home/sergio/usr_lib.DEV/usr/lib/arm-linux-gnueabihf
``
 
then
``
. ~/.profile
``
 
### Cmake compilation
```ruby
root@var-som-mx7:/home/user/home/sergio/azure-iot-sdk-c# mkdir cmake
root@var-som-mx7:/home/user/home/sergio/azure-iot-sdk-c# cd cmake/
root@var-som-mx7:/home/user/home/sergio/azure-iot-sdk-c/cmake# ls

root@var-som-mx7:/home/user/home/sergio/azure-iot-sdk-c/cmake# cmake ..
-- The C compiler identification is GNU 6.3.0
-- The CXX compiler identification is GNU 6.3.0
-- Check for working C compiler: /usr/bin/cc
-- Check for working C compiler: /usr/bin/cc -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /usr/bin/c++
-- Check for working CXX compiler: /usr/bin/c++ -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- IoT Client SDK Version = 1.2.13
-- Looking for include file stdint.h
-- Looking for include file stdint.h - found
-- Looking for include file stdbool.h
-- Looking for include file stdbool.h - found
-- target architecture: ARM
-- Performing Test CXX_FLAG_CXX11
-- Performing Test CXX_FLAG_CXX11 - Success
-- Found OpenSSL: /usr/lib/arm-linux-gnueabihf/libssl.so;/usr/lib/arm-linux-gnueabihf/libcrypto.so (found version "1.1.0j")
-- Could NOT find PkgConfig (missing:  PKG_CONFIG_EXECUTABLE)
-- Found CURL: /usr/lib/arm-linux-gnueabihf/libcurl.so (found version "7.52.1")
-- Found CURL: /usr/lib/arm-linux-gnueabihf/libcurl.so
-- target architecture: ARM
-- target architecture: ARM
-- target architecture: ARM
-- target architecture: ARM
-- iothub architecture: ARM
-- Configuring done
-- Generating done
-- Build files have been written to: /home/user/home/sergio/azure-iot-sdk-c/cmake
```

```ruby
root@var-som-mx7:/home/user/home/sergio/azure-iot-sdk-c/cmake# cmake --build .
Scanning dependencies of target parson
[  1%] Building C object CMakeFiles/parson.dir/deps/parson/parson.c.o
[  1%] Linking C static library libparson.a
[  1%] Built target parson
Scanning dependencies of target aziotsharedutil
[  1%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/base32.c.o
[  1%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/base64.c.o
[  2%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/buffer.c.o
[  2%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/constbuffer_array.c.o
[  3%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/connection_string_parser.c.o
[  3%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/constbuffer.c.o
[  4%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/consolelogger.c.o
[  4%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/crt_abstractions.c.o
[  5%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/constmap.c.o
[  5%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/doublylinkedlist.c.o
[  5%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/gballoc.c.o
[  6%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/gbnetwork.c.o
[  6%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/gb_stdio.c.o
[  7%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/gb_time.c.o
[  7%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/gb_rand.c.o
[  8%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/hmac.c.o
[  8%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/hmacsha256.c.o
[  9%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/xio.c.o
[  9%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/singlylinkedlist.c.o
[ 10%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/map.c.o
[ 10%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/sastoken.c.o
[ 10%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/sha1.c.o
[ 11%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/sha224.c.o
[ 11%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/sha384-512.c.o
[ 12%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/strings.c.o
[ 12%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/string_token.c.o
[ 13%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/string_tokenizer.c.o
[ 13%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/uuid.c.o
[ 14%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/urlencode.c.o
[ 14%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/usha.c.o
[ 14%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/vector.c.o
[ 15%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/xlogging.c.o
[ 15%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/optionhandler.c.o
[ 16%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/memory_data.c.o
[ 16%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/adapters/agenttime.c.o
[ 17%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/adapters/condition_pthreads.c.o
[ 17%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/adapters/lock_pthreads.c.o
[ 18%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/adapters/platform_linux.c.o
[ 18%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/adapters/socketio_berkeley.c.o
[ 19%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/adapters/tickcounter_linux.c.o
[ 19%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/adapters/threadapi_pthreads.c.o
[ 19%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/adapters/uniqueid_linux.c.o
[ 20%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/adapters/envvariable.c.o
[ 20%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/adapters/linux_time.c.o
[ 21%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/httpapiex.c.o
[ 21%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/httpapiexsas.c.o
[ 22%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/httpheaders.c.o
[ 22%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/adapters/httpapi_curl.c.o
[ 23%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/http_proxy_io.c.o
[ 23%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/adapters/tlsio_openssl.c.o
[ 23%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/adapters/x509_openssl.c.o
[ 24%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/wsio.c.o
[ 24%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/uws_client.c.o
[ 25%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/uws_frame_encoder.c.o
[ 25%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/utf8_checker.c.o
[ 26%] Building C object c-utility/CMakeFiles/aziotsharedutil.dir/src/ws_url.c.o
[ 26%] Linking C static library libaziotsharedutil.a
[ 26%] Built target aziotsharedutil
Scanning dependencies of target uamqp
[ 26%] Building C object uamqp/CMakeFiles/uamqp.dir/src/amqp_definitions.c.o
[ 26%] Building C object uamqp/CMakeFiles/uamqp.dir/src/amqp_frame_codec.c.o
[ 27%] Building C object uamqp/CMakeFiles/uamqp.dir/src/amqp_management.c.o
[ 27%] Building C object uamqp/CMakeFiles/uamqp.dir/src/amqpvalue.c.o
[ 28%] Building C object uamqp/CMakeFiles/uamqp.dir/src/amqpvalue_to_string.c.o
[ 28%] Building C object uamqp/CMakeFiles/uamqp.dir/src/async_operation.c.o
[ 29%] Building C object uamqp/CMakeFiles/uamqp.dir/src/cbs.c.o
[ 29%] Building C object uamqp/CMakeFiles/uamqp.dir/src/connection.c.o
[ 30%] Building C object uamqp/CMakeFiles/uamqp.dir/src/frame_codec.c.o
[ 30%] Building C object uamqp/CMakeFiles/uamqp.dir/src/header_detect_io.c.o
[ 30%] Building C object uamqp/CMakeFiles/uamqp.dir/src/link.c.o
[ 31%] Building C object uamqp/CMakeFiles/uamqp.dir/src/message.c.o
brcmfmac: brcmf_cfg80211_reg_notifier: not a ISO3166 code (0x30 0x30)
[ 31%] Building C object uamqp/CMakeFiles/uamqp.dir/src/message_receiver.c.o
[ 32%] Building C object uamqp/CMakeFiles/uamqp.dir/src/message_sender.c.o
[ 32%] Building C object uamqp/CMakeFiles/uamqp.dir/src/messaging.c.o
[ 33%] Building C object uamqp/CMakeFiles/uamqp.dir/src/sasl_anonymous.c.o
[ 33%] Building C object uamqp/CMakeFiles/uamqp.dir/src/sasl_frame_codec.c.o
[ 34%] Building C object uamqp/CMakeFiles/uamqp.dir/src/sasl_mechanism.c.o
[ 34%] Building C object uamqp/CMakeFiles/uamqp.dir/src/sasl_server_mechanism.c.o
[ 35%] Building C object uamqp/CMakeFiles/uamqp.dir/src/sasl_mssbcbs.c.o
[ 35%] Building C object uamqp/CMakeFiles/uamqp.dir/src/sasl_plain.c.o
[ 35%] Building C object uamqp/CMakeFiles/uamqp.dir/src/saslclientio.c.o
[ 36%] Building C object uamqp/CMakeFiles/uamqp.dir/src/session.c.o
[ 36%] Building C object uamqp/CMakeFiles/uamqp.dir/src/socket_listener_berkeley.c.o
[ 37%] Linking C static library libuamqp.a
[ 37%] Built target uamqp
Scanning dependencies of target umqtt
[ 37%] Building C object umqtt/CMakeFiles/umqtt.dir/src/mqtt_client.c.o
[ 38%] Building C object umqtt/CMakeFiles/umqtt.dir/src/mqtt_codec.c.o
[ 38%] Building C object umqtt/CMakeFiles/umqtt.dir/src/mqtt_message.c.o
[ 39%] Linking C static library libumqtt.a
[ 39%] Built target umqtt
Scanning dependencies of target uhttp
[ 39%] Building C object deps/uhttp/CMakeFiles/uhttp.dir/src/uhttp.c.o
[ 40%] Linking C static library libuhttp.a
[ 40%] Built target uhttp
Scanning dependencies of target iothub_service_client
[ 40%] Building C object iothub_service_client/CMakeFiles/iothub_service_client.dir/src/iothub_deviceconfiguration.c.o
[ 41%] Building C object iothub_service_client/CMakeFiles/iothub_service_client.dir/src/iothub_devicemethod.c.o
[ 41%] Building C object iothub_service_client/CMakeFiles/iothub_service_client.dir/src/iothub_devicetwin.c.o
[ 41%] Building C object iothub_service_client/CMakeFiles/iothub_service_client.dir/src/iothub_messaging.c.o
[ 42%] Building C object iothub_service_client/CMakeFiles/iothub_service_client.dir/src/iothub_messaging_ll.c.o
[ 42%] Building C object iothub_service_client/CMakeFiles/iothub_service_client.dir/src/iothub_registrymanager.c.o
[ 43%] Building C object iothub_service_client/CMakeFiles/iothub_service_client.dir/src/iothub_sc_version.c.o
[ 43%] Building C object iothub_service_client/CMakeFiles/iothub_service_client.dir/src/iothub_service_client_auth.c.o
[ 44%] Building C object iothub_service_client/CMakeFiles/iothub_service_client.dir/__/iothub_client/src/iothub_message.c.o
[ 44%] Linking C static library libiothub_service_client.a
[ 44%] Built target iothub_service_client
Scanning dependencies of target iothub_client_mqtt_transport
[ 45%] Building C object iothub_client/CMakeFiles/iothub_client_mqtt_transport.dir/src/iothub_client_authorization.c.o
[ 45%] Building C object iothub_client/CMakeFiles/iothub_client_mqtt_transport.dir/src/iothub_client_retry_control.c.o
[ 46%] Building C object iothub_client/CMakeFiles/iothub_client_mqtt_transport.dir/src/iothub_transport_ll_private.c.o
[ 46%] Building C object iothub_client/CMakeFiles/iothub_client_mqtt_transport.dir/src/iothubtransport_mqtt_common.c.o
[ 46%] Building C object iothub_client/CMakeFiles/iothub_client_mqtt_transport.dir/src/iothubtransportmqtt.c.o
[ 47%] Linking C static library libiothub_client_mqtt_transport.a
[ 47%] Built target iothub_client_mqtt_transport
Scanning dependencies of target iothub_client_amqp_ws_transport
[ 48%] Building C object iothub_client/CMakeFiles/iothub_client_amqp_ws_transport.dir/src/iothub_client_authorization.c.o
[ 48%] Building C object iothub_client/CMakeFiles/iothub_client_amqp_ws_transport.dir/src/iothub_client_retry_control.c.o
[ 49%] Building C object iothub_client/CMakeFiles/iothub_client_amqp_ws_transport.dir/src/iothub_transport_ll_private.c.o
[ 49%] Building C object iothub_client/CMakeFiles/iothub_client_amqp_ws_transport.dir/src/iothubtransport_amqp_common.c.o
[ 50%] Building C object iothub_client/CMakeFiles/iothub_client_amqp_ws_transport.dir/src/iothubtransport_amqp_device.c.o
[ 50%] Building C object iothub_client/CMakeFiles/iothub_client_amqp_ws_transport.dir/src/iothubtransport_amqp_cbs_auth.c.o
[ 50%] Building C object iothub_client/CMakeFiles/iothub_client_amqp_ws_transport.dir/src/iothubtransport_amqp_connection.c.o
[ 51%] Building C object iothub_client/CMakeFiles/iothub_client_amqp_ws_transport.dir/src/iothubtransport_amqp_telemetry_messenger.c.o
[ 51%] Building C object iothub_client/CMakeFiles/iothub_client_amqp_ws_transport.dir/src/iothubtransport_amqp_twin_messenger.c.o
[ 52%] Building C object iothub_client/CMakeFiles/iothub_client_amqp_ws_transport.dir/src/iothubtransport_amqp_messenger.c.o
[ 52%] Building C object iothub_client/CMakeFiles/iothub_client_amqp_ws_transport.dir/src/iothubtransportamqp_methods.c.o
[ 53%] Building C object iothub_client/CMakeFiles/iothub_client_amqp_ws_transport.dir/src/message_queue.c.o
[ 53%] Building C object iothub_client/CMakeFiles/iothub_client_amqp_ws_transport.dir/src/uamqp_messaging.c.o
[ 54%] Building C object iothub_client/CMakeFiles/iothub_client_amqp_ws_transport.dir/src/iothubtransportamqp_websockets.c.o
[ 54%] Linking C static library libiothub_client_amqp_ws_transport.a
[ 54%] Built target iothub_client_amqp_ws_transport
Scanning dependencies of target iothub_client_amqp_transport
[ 54%] Building C object iothub_client/CMakeFiles/iothub_client_amqp_transport.dir/src/iothub_client_authorization.c.o
[ 54%] Building C object iothub_client/CMakeFiles/iothub_client_amqp_transport.dir/src/iothub_client_retry_control.c.o
[ 55%] Building C object iothub_client/CMakeFiles/iothub_client_amqp_transport.dir/src/iothub_transport_ll_private.c.o
[ 55%] Building C object iothub_client/CMakeFiles/iothub_client_amqp_transport.dir/src/iothubtransport_amqp_common.c.o
[ 56%] Building C object iothub_client/CMakeFiles/iothub_client_amqp_transport.dir/src/iothubtransport_amqp_device.c.o
[ 56%] Building C object iothub_client/CMakeFiles/iothub_client_amqp_transport.dir/src/iothubtransport_amqp_cbs_auth.c.o
[ 57%] Building C object iothub_client/CMakeFiles/iothub_client_amqp_transport.dir/src/iothubtransport_amqp_connection.c.o
[ 57%] Building C object iothub_client/CMakeFiles/iothub_client_amqp_transport.dir/src/iothubtransport_amqp_telemetry_messenger.c.o
[ 58%] Building C object iothub_client/CMakeFiles/iothub_client_amqp_transport.dir/src/iothubtransport_amqp_twin_messenger.c.o
[ 58%] Building C object iothub_client/CMakeFiles/iothub_client_amqp_transport.dir/src/iothubtransport_amqp_messenger.c.o
[ 58%] Building C object iothub_client/CMakeFiles/iothub_client_amqp_transport.dir/src/iothubtransportamqp_methods.c.o
[ 59%] Building C object iothub_client/CMakeFiles/iothub_client_amqp_transport.dir/src/message_queue.c.o
[ 59%] Building C object iothub_client/CMakeFiles/iothub_client_amqp_transport.dir/src/uamqp_messaging.c.o
[ 60%] Building C object iothub_client/CMakeFiles/iothub_client_amqp_transport.dir/src/iothubtransportamqp.c.o
[ 60%] Linking C static library libiothub_client_amqp_transport.a
[ 60%] Built target iothub_client_amqp_transport
Scanning dependencies of target iothub_client_http_transport
[ 60%] Building C object iothub_client/CMakeFiles/iothub_client_http_transport.dir/src/iothub_client_authorization.c.o
[ 61%] Building C object iothub_client/CMakeFiles/iothub_client_http_transport.dir/src/iothub_client_retry_control.c.o
[ 61%] Building C object iothub_client/CMakeFiles/iothub_client_http_transport.dir/src/iothub_transport_ll_private.c.o
[ 62%] Building C object iothub_client/CMakeFiles/iothub_client_http_transport.dir/src/iothubtransporthttp.c.o
[ 62%] Linking C static library libiothub_client_http_transport.a
[ 62%] Built target iothub_client_http_transport
Scanning dependencies of target iothub_client_mqtt_ws_transport
[ 62%] Building C object iothub_client/CMakeFiles/iothub_client_mqtt_ws_transport.dir/src/iothub_client_authorization.c.o
[ 63%] Building C object iothub_client/CMakeFiles/iothub_client_mqtt_ws_transport.dir/src/iothub_client_retry_control.c.o
[ 63%] Building C object iothub_client/CMakeFiles/iothub_client_mqtt_ws_transport.dir/src/iothub_transport_ll_private.c.o
[ 64%] Building C object iothub_client/CMakeFiles/iothub_client_mqtt_ws_transport.dir/src/iothubtransport_mqtt_common.c.o
[ 64%] Building C object iothub_client/CMakeFiles/iothub_client_mqtt_ws_transport.dir/src/iothubtransportmqtt_websockets.c.o
[ 65%] Linking C static library libiothub_client_mqtt_ws_transport.a
[ 65%] Built target iothub_client_mqtt_ws_transport
Scanning dependencies of target iothub_client
[ 66%] Building C object iothub_client/CMakeFiles/iothub_client.dir/src/iothub.c.o
[ 66%] Building C object iothub_client/CMakeFiles/iothub_client.dir/src/iothub_client.c.o
[ 67%] Building C object iothub_client/CMakeFiles/iothub_client.dir/src/iothub_client_core.c.o
[ 67%] Building C object iothub_client/CMakeFiles/iothub_client.dir/src/iothub_client_core_ll.c.o
[ 68%] Building C object iothub_client/CMakeFiles/iothub_client.dir/src/iothub_client_diagnostic.c.o
[ 68%] Building C object iothub_client/CMakeFiles/iothub_client.dir/src/iothub_client_ll.c.o
[ 68%] Building C object iothub_client/CMakeFiles/iothub_client.dir/src/iothub_device_client.c.o
[ 69%] Building C object iothub_client/CMakeFiles/iothub_client.dir/src/iothub_device_client_ll.c.o
[ 69%] Building C object iothub_client/CMakeFiles/iothub_client.dir/src/iothub_message.c.o
[ 70%] Building C object iothub_client/CMakeFiles/iothub_client.dir/src/iothub_module_client.c.o
[ 70%] Building C object iothub_client/CMakeFiles/iothub_client.dir/src/iothub_module_client_ll.c.o
[ 71%] Building C object iothub_client/CMakeFiles/iothub_client.dir/src/iothubtransport.c.o
[ 71%] Building C object iothub_client/CMakeFiles/iothub_client.dir/src/version.c.o
[ 72%] Building C object iothub_client/CMakeFiles/iothub_client.dir/src/iothub_client_ll_uploadtoblob.c.o
[ 72%] Building C object iothub_client/CMakeFiles/iothub_client.dir/src/blob.c.o
[ 73%] Linking C static library libiothub_client.a
[ 73%] Built target iothub_client
Scanning dependencies of target iothub_convenience_sample
[ 73%] Building C object iothub_client/samples/iothub_convenience_sample/CMakeFiles/iothub_convenience_sample.dir/iothub_convenience_sample.c.o
[ 74%] Linking C executable iothub_convenience_sample
/usr/bin/ld: warning: libssl.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libssl.so.1.1
/usr/bin/ld: warning: libcrypto.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libcrypto.so.1.1
[ 74%] Built target iothub_convenience_sample
Scanning dependencies of target iothub_ll_c2d_sample
[ 74%] Building C object iothub_client/samples/iothub_ll_c2d_sample/CMakeFiles/iothub_ll_c2d_sample.dir/iothub_ll_c2d_sample.c.o
[ 74%] Building C object iothub_client/samples/iothub_ll_c2d_sample/CMakeFiles/iothub_ll_c2d_sample.dir/__/__/__/certs/certs.c.o
[ 75%] Linking C executable iothub_ll_c2d_sample
/usr/bin/ld: warning: libssl.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libssl.so.1.1
/usr/bin/ld: warning: libcrypto.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libcrypto.so.1.1
[ 75%] Built target iothub_ll_c2d_sample
Scanning dependencies of target iothub_ll_client_x509_sample
[ 75%] Building C object iothub_client/samples/iothub_ll_client_x509_sample/CMakeFiles/iothub_ll_client_x509_sample.dir/iothub_ll_client_x509_sample.c.o
[ 76%] Linking C executable iothub_ll_client_x509_sample
/usr/bin/ld: warning: libssl.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libssl.so.1.1
/usr/bin/ld: warning: libcrypto.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libcrypto.so.1.1
[ 76%] Built target iothub_ll_client_x509_sample
Scanning dependencies of target iothub_ll_telemetry_sample
[ 76%] Building C object iothub_client/samples/iothub_ll_telemetry_sample/CMakeFiles/iothub_ll_telemetry_sample.dir/iothub_ll_telemetry_sample.c.o
[ 77%] Linking C executable iothub_ll_telemetry_sample
/usr/bin/ld: warning: libssl.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libssl.so.1.1
/usr/bin/ld: warning: libcrypto.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libcrypto.so.1.1
[ 77%] Built target iothub_ll_telemetry_sample
Scanning dependencies of target iotedge_downstream_device_sample
[ 78%] Building C object iothub_client/samples/iotedge_downstream_device_sample/CMakeFiles/iotedge_downstream_device_sample.dir/iotedge_downstream_device_sample.c.o
[ 78%] Linking C executable iotedge_downstream_device_sample
/usr/bin/ld: warning: libssl.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libssl.so.1.1
/usr/bin/ld: warning: libcrypto.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libcrypto.so.1.1
[ 78%] Built target iotedge_downstream_device_sample
Scanning dependencies of target iothub_client_sample_upload_to_blob
[ 78%] Building C object iothub_client/samples/iothub_client_sample_upload_to_blob/CMakeFiles/iothub_client_sample_upload_to_blob.dir/iothub_client_sample_upload_to_blob.c.o
[ 79%] Linking C executable iothub_client_sample_upload_to_blob
/usr/bin/ld: warning: libssl.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libssl.so.1.1
/usr/bin/ld: warning: libcrypto.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libcrypto.so.1.1
[ 79%] Built target iothub_client_sample_upload_to_blob
Scanning dependencies of target iothub_client_sample_upload_to_blob_mb
[ 79%] Building C object iothub_client/samples/iothub_client_sample_upload_to_blob_mb/CMakeFiles/iothub_client_sample_upload_to_blob_mb.dir/iothub_client_sample_upload_to_blob_mb.c.o
[ 80%] Linking C executable iothub_client_sample_upload_to_blob_mb
/usr/bin/ld: warning: libssl.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libssl.so.1.1
/usr/bin/ld: warning: libcrypto.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libcrypto.so.1.1
[ 80%] Built target iothub_client_sample_upload_to_blob_mb
Scanning dependencies of target serializer
[ 80%] Building C object serializer/CMakeFiles/serializer.dir/src/agenttypesystem.c.o
[ 81%] Building C object serializer/CMakeFiles/serializer.dir/src/codefirst.c.o
[ 81%] Building C object serializer/CMakeFiles/serializer.dir/src/commanddecoder.c.o
[ 82%] Building C object serializer/CMakeFiles/serializer.dir/src/datamarshaller.c.o
[ 82%] Building C object serializer/CMakeFiles/serializer.dir/src/datapublisher.c.o
[ 83%] Building C object serializer/CMakeFiles/serializer.dir/src/dataserializer.c.o
[ 83%] Building C object serializer/CMakeFiles/serializer.dir/src/iotdevice.c.o
[ 83%] Building C object serializer/CMakeFiles/serializer.dir/src/jsondecoder.c.o
[ 84%] Building C object serializer/CMakeFiles/serializer.dir/src/jsonencoder.c.o
[ 84%] Building C object serializer/CMakeFiles/serializer.dir/src/multitree.c.o
[ 85%] Building C object serializer/CMakeFiles/serializer.dir/src/schema.c.o
[ 85%] Building C object serializer/CMakeFiles/serializer.dir/src/schemalib.c.o
[ 86%] Building C object serializer/CMakeFiles/serializer.dir/src/schemaserializer.c.o
[ 86%] Building C object serializer/CMakeFiles/serializer.dir/src/methodreturn.c.o
[ 87%] Linking C static library libserializer.a
[ 87%] Built target serializer
Scanning dependencies of target iothub_client_sample_mqtt_dm
[ 87%] Building C object iothub_client/samples/iothub_client_sample_mqtt_dm/CMakeFiles/iothub_client_sample_mqtt_dm.dir/iothub_client_sample_mqtt_dm.c.o
[ 87%] Building C object iothub_client/samples/iothub_client_sample_mqtt_dm/CMakeFiles/iothub_client_sample_mqtt_dm.dir/pi_device/pi.c.o
[ 88%] Linking C executable iothub_client_sample_mqtt_dm
/usr/bin/ld: warning: libssl.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libssl.so.1.1
/usr/bin/ld: warning: libcrypto.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libcrypto.so.1.1
[ 88%] Built target iothub_client_sample_mqtt_dm
Scanning dependencies of target iothub_client_sample_amqp_shared_methods
[ 88%] Building C object iothub_client/samples/iothub_client_sample_amqp_shared_methods/CMakeFiles/iothub_client_sample_amqp_shared_methods.dir/iothub_client_sample_amqp_shared_methods.c.o
[ 89%] Linking C executable iothub_client_sample_amqp_shared_methods
/usr/bin/ld: warning: libssl.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libssl.so.1.1
/usr/bin/ld: warning: libcrypto.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libcrypto.so.1.1
[ 89%] Built target iothub_client_sample_amqp_shared_methods
Scanning dependencies of target iothub_ll_client_shared_sample
[ 89%] Building C object iothub_client/samples/iothub_ll_client_shared_sample/CMakeFiles/iothub_ll_client_shared_sample.dir/iothub_ll_client_shared_sample.c.o
[ 90%] Linking C executable iothub_ll_client_shared_sample
/usr/bin/ld: warning: libssl.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libssl.so.1.1
/usr/bin/ld: warning: libcrypto.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libcrypto.so.1.1
[ 90%] Built target iothub_ll_client_shared_sample
Scanning dependencies of target iothub_client_device_twin_and_methods_sample
[ 91%] Building C object iothub_client/samples/iothub_client_device_twin_and_methods_sample/CMakeFiles/iothub_client_device_twin_and_methods_sample.dir/iothub_client_device_twin_and_methods_sample.c.o
[ 91%] Linking C executable iothub_client_device_twin_and_methods_sample
/usr/bin/ld: warning: libssl.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libssl.so.1.1
/usr/bin/ld: warning: libcrypto.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libcrypto.so.1.1
[ 91%] Built target iothub_client_device_twin_and_methods_sample
Scanning dependencies of target remote_monitoring
[ 91%] Building C object serializer/samples/remote_monitoring/CMakeFiles/remote_monitoring.dir/remote_monitoring.c.o
[ 92%] Linking C executable remote_monitoring
/usr/bin/ld: warning: libssl.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libssl.so.1.1
/usr/bin/ld: warning: libcrypto.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libcrypto.so.1.1
[ 92%] Built target remote_monitoring
Scanning dependencies of target simplesample_amqp
[ 92%] Building C object serializer/samples/simplesample_amqp/CMakeFiles/simplesample_amqp.dir/simplesample_amqp.c.o
[ 92%] Building C object serializer/samples/simplesample_amqp/CMakeFiles/simplesample_amqp.dir/linux/main.c.o
[ 93%] Linking C executable simplesample_amqp
/usr/bin/ld: warning: libssl.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libssl.so.1.1
/usr/bin/ld: warning: libcrypto.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libcrypto.so.1.1
[ 93%] Built target simplesample_amqp
Scanning dependencies of target simplesample_http
[ 93%] Building C object serializer/samples/simplesample_http/CMakeFiles/simplesample_http.dir/simplesample_http.c.o
[ 94%] Building C object serializer/samples/simplesample_http/CMakeFiles/simplesample_http.dir/linux/main.c.o
[ 94%] Linking C executable simplesample_http
/usr/bin/ld: warning: libssl.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libssl.so.1.1
/usr/bin/ld: warning: libcrypto.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libcrypto.so.1.1
[ 94%] Built target simplesample_http
Scanning dependencies of target temp_sensor_anomaly
[ 94%] Building C object serializer/samples/temp_sensor_anomaly/CMakeFiles/temp_sensor_anomaly.dir/windows/main.c.o
[ 95%] Linking C executable temp_sensor_anomaly
/usr/bin/ld: warning: libssl.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libssl.so.1.1
/usr/bin/ld: warning: libcrypto.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libcrypto.so.1.1
[ 95%] Built target temp_sensor_anomaly
Scanning dependencies of target simplesample_mqtt
[ 96%] Building C object serializer/samples/simplesample_mqtt/CMakeFiles/simplesample_mqtt.dir/simplesample_mqtt.c.o
[ 96%] Building C object serializer/samples/simplesample_mqtt/CMakeFiles/simplesample_mqtt.dir/linux/main.c.o
[ 97%] Linking C executable simplesample_mqtt
/usr/bin/ld: warning: libssl.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libssl.so.1.1
/usr/bin/ld: warning: libcrypto.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libcrypto.so.1.1
[ 97%] Built target simplesample_mqtt
Scanning dependencies of target devicemethod_simplesample
[ 98%] Building C object serializer/samples/devicemethod_simplesample/CMakeFiles/devicemethod_simplesample.dir/devicemethod_simplesample.c.o
[ 98%] Building C object serializer/samples/devicemethod_simplesample/CMakeFiles/devicemethod_simplesample.dir/linux/main.c.o
[ 99%] Linking C executable devicemethod_simplesample
/usr/bin/ld: warning: libssl.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libssl.so.1.1
/usr/bin/ld: warning: libcrypto.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libcrypto.so.1.1
[ 99%] Built target devicemethod_simplesample
Scanning dependencies of target devicetwin_simplesample
[ 99%] Building C object serializer/samples/devicetwin_simplesample/CMakeFiles/devicetwin_simplesample.dir/devicetwin_simplesample.c.o
[ 99%] Linking C executable devicetwin_simplesample
/usr/bin/ld: warning: libssl.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libssl.so.1.1
/usr/bin/ld: warning: libcrypto.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libcrypto.so.1.1
[ 99%] Built target devicetwin_simplesample
Scanning dependencies of target remote_monitoring_client
[ 99%] Building C object samples/solutions/remote_monitoring_client/CMakeFiles/remote_monitoring_client.dir/remote_monitoring.c.o
[100%] Linking C executable remote_monitoring_client
/usr/bin/ld: warning: libssl.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libssl.so.1.1
/usr/bin/ld: warning: libcrypto.so.1.0.2, needed by /usr/lib/gcc/arm-linux-gnueabihf/6/../../../arm-linux-gnueabihf/libcurl.so, may conflict with libcrypto.so.1.1
[100%] Built target remote_monitoring_client
root@var-som-mx7:/home/user/home/sergio/azure-iot-sdk-c/cmake#
```
### Compilation commands
```
sergio@ubuntu:~/azure-iot-sdk-c/build_all/linux$ ./build.sh --toolchain-file toolchain-prtn.cmake  --no-amqp --no-http -cl -DMBED_BUILD_TIMESTAMP  -cl --sysroot=/home/sergio/usr_lib.DEV
```
```
./build.sh --toolchain-file toolchain-prtn.cmake  --no-amqp --no-http -cl -DMBED_BUILD_TIMESTAMP -cl --sysroot=/home/sergio/usr_lib.DEVX
```
```
./build.sh --toolchain-file toolchain-prtn.cmake  --no-amqp --no-http --skip-unittests  -cl -DMBED_BUILD_TIMESTAMP -cl -shared -cl --sysroot=/home/sergio/SPX_G25SDK/buildroot-at91/output/host/usr/arm-buildroot-linux-gnueabi/sysroot
```
### .profile
```ruby
# ~/.profile: executed by the command interpreter for login shells.
# This file is not read by bash(1), if ~/.bash_profile or ~/.bash_login
# exists.
# see /usr/share/doc/bash/examples/startup-files for examples.
# the files are located in the bash-doc package.

# the default umask is set in /etc/profile; for setting the umask
# for ssh logins, install and configure the libpam-umask package.
#umask 022

# if running bash
if [ -n "$BASH_VERSION" ]; then
    # include .bashrc if it exists
    if [ -f "$HOME/.bashrc" ]; then
	. "$HOME/.bashrc"
    fi
fi

# set PATH so it includes user's private bin directories
PATH="$HOME/bin:$HOME/.local/bin:$PATH"

export PATH=$PATH:/home/sergio/var_som_mx7_debian/toolchain/gcc-linaro-6.3.1-2017.05-x86_64_arm-linux-gnueabihf/bin
# for clab
export ARCH=arm
export CROSS_COMPILE=arm-linux-gnueabihf-
export VARiMX7_ROOT=/home/sergio/usr_lib.DEVX
export OPENSSL_ROOT_DIR=/home/sergio/usr_lib.DEVX/usr/lib/arm-linux-gnueabihf
# for clab
export DTB="imx7d-*imx7*.dtb"
```


### Other fixes
``
sergio@ubuntu:~/usr_lib.DEVX/usr/lib/arm-linux-gnueabihf$ ln -s libdl-2.24.so libdl.so.2
``
``
copy /home/sergio/azure-iot-sdk-c/certs/certs.h to /home/sergio/usr_lib.DEVX/usr/include``

```
copy /home/sergio/azure-iot-sdk-c/certs/certs.c content  into  /home/sergio/azure-iot-sdk-c/iothub_client/samples/iothub_ll_client_x509_sample/iothub_ll_client_x509_sample.c
... devicemethod_simplesample.c
... simplesample_mqtt.c
```
```
sergio@ubuntu:~/usr_lib.DEVX$ cp ./lib/arm-linux-gnueabihf/libcom_err.so.2 ./usr/lib/arm-linux-gnueabihf/
```
```
sergio@ubuntu:~/usr_lib.DEVX$ cp ./lib/arm-linux-gnueabihf/libz.so.1 ./usr/lib/arm-linux-gnueabihf/
```
```
sergio@ubuntu:~/usr_lib.DEVX$ cp ./lib/arm-linux-gnueabihf/libgcrypt.so.20 ./usr/lib/arm-linux-gnueabihf/
```
```
sergio@ubuntu:~/usr_lib.DEVX$ cp ./lib/arm-linux-gnueabihf/libkeyutils.so.1 ./usr/lib/arm-linux-gnueabihf/
```
```
sergio@ubuntu:~/usr_lib.DEVX$ cp ./lib/arm-linux-gnueabihf/libresolv.so.2 ./usr/lib/arm-linux-gnueabihf/
```
```
sergio@ubuntu:~/usr_lib.DEVX$ cp ./lib/arm-linux-gnueabihf/libgpg-error.so.0 ./usr/lib/arm-linux-gnueabihf/
```
### libm issue
base line root file systema version of libm.a was not compiled for dynamic allocation, but toolchain version was.So use these
```
sergio@ubuntu:~/var_som_mx7_debian/toolchain/gcc-linaro-6.3.1-2017.05-x86_64_arm-linux-gnueabihf$ cp arm-linux-gnueabihf/libc/usr/lib/libm.so /home/sergio/usr_lib.DEVX/usr/lib/arm-linux-gnueabihf/
```
```
sergio@ubuntu:~/var_som_mx7_debian/toolchain/gcc-linaro-6.3.1-2017.05-x86_64_arm-linux-gnueabihf$ cp arm-linux-gnueabihf/libc/usr/lib/libm.a /home/sergio/usr_lib.DEVX/usr/lib/arm-linux-gnueabihf/
```
So this comman now works
```
sergio@ubuntu:~/azure-iot-sdk-c/build_all/linux$ ./build.sh --toolchain-file toolchain-prtn.cmake  --no-amqp --no-http  -cl -DMBED_BUILD_TIMESTAMP -cl -shared -cl --sysroot=/home/sergio/usr_lib.DEVX
```
### lua headers into usr_lib.DEVX
```
sergio@ubuntu:~/var_som_mx7_debian/apps/lua-5.1.5/src$ cp lua.h ../../../../usr_lib.DEVX/usr/include/
sergio@ubuntu:~/var_som_mx7_debian/apps/lua-5.1.5/src$ cp luaconf.h ../../../../usr_lib.DEVX/usr/include/
sergio@ubuntu:~/var_som_mx7_debian/apps/lua-5.1.5/src$ cp lauxlib.h ../../../../usr_lib.DEVX/usr/include/
```

### openssl opensslconf.h
```
sergio@ubuntu:~/usr_lib.DEVX/usr/include/arm-linux-gnueabihf/openssl$ cp  opensslconf.h ../../openssl
```

# VAR GPIO
```
GPIO3_IO[5] = (3-1)*32+5 = 69


J1[7]

echo 69 > /sys/class/gpio/export
echo out > /sys/class/gpio/gpio69/direction
echo 1 > /sys/class/gpio/gpio69/value
echo 0 > /sys/class/gpio/gpio69/value
echo 69 > /sys/class/gpio/unexport



echo 103 > /sys/class/gpio/export
echo out > /sys/class/gpio/gpio103/direction
echo 1 > /sys/class/gpio/gpio103/value
echo 0 > /sys/class/gpio/gpio103/value
echo 103 > /sys/class/gpio/unexport


1  MX7D_PAD_LCD_DATA00__GPIO3_IO5		0x79	J1 7	-> 69
2  MX7D_PAD_LCD_DATA02__GPIO3_IO7 		0x79	J1 9 	-> 71
3  MX7D_PAD_LCD_DATA03__GPIO3_IO8		0x79	J1 10	-> 72
4  MX7D_PAD_EPDC_DATA04__GPIO2_IO4		0x79	J2 1	-> 36
5  MX7D_PAD_EPDC_DATA05__GPIO2_IO5		0x79	J2 2    -> 37
6  MX7D_PAD_EPDC_DATA06__GPIO2_IO6 		0x79	J2 3    -> 38
7  MX7D_PAD_EPDC_DATA07__GPIO2_IO7		0x79	J2 4    -> 39
8  MX7D_PAD_EPDC_DATA10__GPIO2_IO10		0x79	J2 7    -> 42
9  MX7D_PAD_EPDC_DATA11__GPIO2_IO11		0x79	J2 8    -> 43
10 MX7D_PAD_EPDC_DATA12__GPIO2_IO12		0x79	J2 9    -> 44
11 MX7D_PAD_EPDC_DATA13__GPIO2_IO13		0x79	J2 10   -> 45
12 MX7D_PAD_EPDC_DATA14__GPIO2_IO14		0x79	J3 1    -> 46
13 MX7D_PAD_EPDC_DATA15__GPIO2_IO15		0x79	J3 2    -> 47
14 MX7D_PAD_LCD_DATA18__GPIO3_IO23		0x79	J3 5    -> 87
15 MX7D_PAD_LCD_DATA19__GPIO3_IO24		0x79	J3 6    -> 88
16 MX7D_PAD_LCD_DATA20__GPIO3_IO25		0x79	J3 7    -> 89
17 MX7D_PAD_LCD_DATA21__GPIO3_IO26		0x79	J3 8    -> 90
18 MX7D_PAD_LCD_DATA22__GPIO3_IO27		0x79	J3 9    -> 91
19 MX7D_PAD_LCD_DATA23__GPIO3_IO28		0x79	J3 10   -> 92

```


# VAR UARTs

The VAR-SOM-MX7/VAR-SOM-MX7-5G exposes up to 7 UART interfaces some of which are
muxed with other peripherals. Refer to 
[https://www.variscite.com/wp-content/uploads/2017/12/VAR-SOM-MX7_VAR-SOM-MX7-5G_datasheet.pdf](https://www.variscite.com/wp-content/uploads/2017/12/VAR-SOM-MX7_VAR-SOM-MX7-5G_datasheet.pdf)
 UART3 is used on SOM for Bluetooth interface and can be
accessible only in when Bluetooth interface is not in use.

So if you have SOM with WiFi/BT then you need to disable 
Variscite Bluetooth setup service via below command. 
```
# systemctl disable variscite-bluetooth
```
UART mapping for IMX7 is as per below

UART1 - /dev/ttymxc0 - Used as serial console
UART2 - /dev/ttymxc1 - Available and configured
[https://github.com/varigit/linux-imx/blob/imx_4.9.88_2.0.0_ga-var01/arch/arm/boot/dts/imx7d-var-som.dtsi#L933](https://github.com/varigit/linux-imx/blob/imx_4.9.88_2.0.0_ga-var01/arch/arm/boot/dts/imx7d-var-som.dtsi#L933)

UART3 - /dev/ttymxc2 - Reserved for Bluetooth purpose 
[https://github.com/varigit/debian-var/blob/debian_stretch_mx7_var02/variscite/variscite-bluetooth#L9](https://github.com/varigit/debian-var/blob/debian_stretch_mx7_var02/variscite/variscite-bluetooth#L9)

Can be available on J13 if you disable Bluetooth service 
Variscite Bluetooth setup service via below command. 
```
# systemctl disable variscite-bluetooth
```
Regarding Userspace access, sample code 
[https://github.com/varigit/linux-imx/blob/imx_4.9.88_2.0.0_ga-var01/Documentation/serial/serial-rs485.txt#L41](https://github.com/varigit/linux-imx/blob/imx_4.9.88_2.0.0_ga-var01/Documentation/serial/serial-rs485.txt#L41)

Here in sample code instead of "/dev/mydevice" use /dev/ttymxc1 or /dev/ttymxc2 device. 

 
# How to delete files only, but keep the directory structure?
```
sergio@ubuntu:~/var_som_mx7_debian/rootfs_test$ sudo find . ! -type d -delete
```

# How to copy in bash all directory and files recursive?
```
sergio@ubuntu:~/var_som_mx7_debian/rootfs$ sudo cp -avr . ../rootfsCopy/
```
Where . is new firmware directory and ../rootfsCopy/ is unit /

# Copying base line filesys
```
sergio@ubuntu:~/var_som_mx7_debian$ sudo cp -avr rootfs_ORG rootfs
```
# Updating Embedded Linux Devices
#### [Background](https://mkrak.org/2017/11/18/updating-embedded-linux-devices-part-0/)
#### [Update strategies](https://mkrak.org/2018/01/10/updating-embedded-linux-devices-part1/)
#### [SWUpdate](https://mkrak.org/2018/01/26/updating-embedded-linux-devices-part2/)
We support SWUpdate with double copy and the partition creation. 
See [variwiki](http://variwiki.com/index.php?title=SWUpdate_Guide&release=RELEASE_SUMO_V1.1_VAR-SOM-MX7) the [script](https://github.com/varigit/meta-variscite-fslc/blob/sumo/scripts/var_mk_yocto_sdcard/variscite_scripts/mx6ul_mx7_install_yocto.sh#L174)
I would advise to use SWUpdate from Yocto sumo, and see if it works for you.
##  update the whole filesystem via network
#### .[VAR-SOM-MX7 - Yocto Setup TFTP/NFS](http://variwiki.com/index.php?title=Yocto_Setup_TFTP/NFS&release=RELEASE_SUMO_V1.1_VAR-SOM-MX7)
```
With one change as below, 


Use below commands for debian rootfs,

Running Yocto rootfs on Variscite board using TFTP & NFS
1.1 Host
Make sure you installed NFS server:

$ sudo apt-get install nfs-kernel-server
$ cd ~/var_som_mx7_debian
$ sudo mkdir rootfs_nfs
$ cd rootfs_nfs
$ sudo tar xvf  ../output/rootfs.tar.gz
$ sudo gedit /etc/exports
Add the following line (change <uname> to the name of user):

/home/<uname>/var_som_mx7_debian/rootfs_nfs    *(rw,sync,no_root_squash,no_all_squash,no_subtree_check) 
exit & save

$ sudo /etc/init.d/nfs-kernel-server restart
Make sure you installed TFTP server:

$ sudo apt-get install xinetd tftpd tftp
Verify:
$ ls /usr/sbin/in.tftpd
$ sudo gedit /etc/xinetd.d/tftp
service tftp
{
protocol = udp
port = 69
socket_type = dgram
wait = yes
user = nobody
server = /usr/sbin/in.tftpd
server_args = /tftpboot
disable = no
}
$ sudo mkdir /tftpboot
$ sudo chmod -R 777 /tftpboot
$ sudo /etc/init.d/xinetd restart
$ cd ~/var-fslc-yocto/build_x11/
$ cp tmp/deploy/images/imx7-var-som/zImage /tftpboot
$ cp tmp/deploy/images/imx7-var-som/zImage-imx*.dtb /tftpboot
$ sudo rename 's/zImage-//' /tftpboot/zImage-*.dtb


1.2 Target
Make sure you have a serial connection to the target.

Reset and hold the space bar. This will bring you to U-Boot command line.

$ setenv serverip 192.168.1.188
$ setenv nfsroot /home/<uname>/rootfs_nfs (change <uname> to the name of user)
$ setenv bootcmd run netboot
$ saveenv 
```
# proftpd
## /etc/hosts
```
127.0.0.1       localhost
127.0.0.1       var-som-mx7
::1             localhost var-som-mx7 ip6-localhost ip6-loopback
ff02::1         ip6-allnodes
ff02::2         ip6-allrouters
```
## /etc/proftpd/proftpd.conf
```

# This is a basic ProFTPD configuration file
# It establishes a single server and a single anonymous login.

ServerName                      "ProFTPD Default Installation"
ServerType                      standalone
DefaultServer                   on

# Port 21 is the standard FTP port.
Port                            21
# Umask 022 is a good standard umask to prevent new dirs and files
# from being group and world writable.
Umask                           022

# To prevent DoS attacks, set the maximum number of child processes
# to 30.  If you need to allow more than 30 concurrent connections
# at once, simply increase this value.  Note that this ONLY works
# in standalone mode, in inetd mode you should use an inetd server
# that allows you to limit maximum number of processes per service

MaxInstances                    30

# Set the user and group that the server normally runs at.
User                            proftpd
Group                           proftpd

# To cause every FTP user to be "jailed" (chrooted) into their home
# directory, uncomment this line.
# DefaultRoot ~
DefaultRoot /mnt/prtnuSD/logdisk
#  If user was created with shell /bin/false, this must be declared in proftpd.conf 
RequireValidShell              off

# Normally, files should be overwritable.
<Directory /*>
  AllowOverwrite                on
</Directory>

# A basic anonymous configuration, no upload directories.
<Anonymous ~proftpd>
  User                          proftpd
  Group                         proftpd
  # Clients should be able to login with "anonymous" as well as "proftpd"
  UserAlias                     anonymous proftpd

  # Limit the maximum number of anonymous logins
  MaxClients                    10

  # 'welcome.msg' should be displayed at login, and '.message' displayed
  # in each newly chdired directory.
  DisplayLogin                  welcome.msg
  DisplayChdir                  .message

  # Limit WRITE everywhere in the anonymous chroot
  <Limit WRITE>
    DenyAll
  </Limit>
</Anonymous>

```


### Create FTP Group
```
# addgroup proftpd
```
### Create FTP user

```
# # adduser proftpd -shell /bin/false -ingroup proftpd -home /ftpshare
```
[TOC]

