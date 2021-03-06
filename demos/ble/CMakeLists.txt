# BLE Gatt Server demo
# Only build on boards that support BLE.
afr_demo_module(ble)

afr_set_demo_metadata(ID "BLE_GATT_SERVER_DEMO")
afr_set_demo_metadata(DESCRIPTION "An example that demonstrates creating and running a BLE GATT Server")
afr_set_demo_metadata(DISPLAY_NAME "BLE GATT Server Demo")

afr_module_sources(
    ${AFR_CURRENT_MODULE}
    INTERFACE
        "${AFR_DEMOS_DIR}/include/aws_ble_gatt_server_demo.h"
        "${CMAKE_CURRENT_LIST_DIR}/aws_ble_gatt_server_demo.c"
        # Todo: Needed for Console. Fix this. BLE requires this header, but it doesn't take data from numericComparision demo.
        "${AFR_DEMOS_DIR}/include/iot_ble_numericComparison.h"
)
afr_module_dependencies(
    ${AFR_CURRENT_MODULE}
    INTERFACE
        AFR::ble
)


# MQTT over BLE demo
afr_demo_module(mqtt_ble)

afr_set_demo_metadata(ID "MQTT_BLE_DEMO")
afr_set_demo_metadata(DESCRIPTION "An example that demonstrates MQTT over BLE assisted by a companion device")
afr_set_demo_metadata(DISPLAY_NAME "MQTT over BLE Hello World")

afr_module_sources(
    ${AFR_CURRENT_MODULE}
    INTERFACE
        "${CMAKE_CURRENT_LIST_DIR}/mqtt_demo_ble_transport.c"
)

afr_module_include_dirs(
    ${AFR_CURRENT_MODULE}
    INTERFACE
        ${AFR_MODULES_DIR}/logging/include
)

afr_module_dependencies(
    ${AFR_CURRENT_MODULE}
    INTERFACE
        AFR::core_mqtt
        AFR::ble
        AFR::mqtt_ble
        # Add dependency on the core_mqtt_demo_dependencies metadata module 
        # so that FreeRTOS console shows this demo when BOTH the core MQTT
        # (or another library depending on coreMQTT) AND BLE libraries are
        # selected on the console.
        AFR::core_mqtt_demo_dependencies
)

# BLE Number Comparison Demo
# Only build on boards that support BLE.
# We don't display the demo below in AFR console
if(AFR_METADATA_MODE)
    return()
endif()
afr_demo_module(ble_numeric_comparison)

afr_module_sources(
    ${AFR_CURRENT_MODULE}
    INTERFACE
        "${AFR_DEMOS_DIR}/include/iot_ble_numericComparison.h"
        "${CMAKE_CURRENT_LIST_DIR}/iot_ble_numericComparison.c"
)
afr_module_dependencies(
    ${AFR_CURRENT_MODULE}
    INTERFACE
        AFR::ble
)
