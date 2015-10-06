#Copyright (c) Microsoft. All rights reserved.
#Licensed under the MIT license. See LICENSE file in the project root for full license information.

#this is CMakeLists.txt for iothub_client_sample_amqp
set(iothub_client_sample_amqp_c_files
iothub_client_sample_amqp.c
./windows/main.c
)

set(iothub_client_sample_amqp_h_files
iothub_client_sample_amqp.h
)

IF(WIN32)
	#windows needs this define
	add_definitions(-D_CRT_SECURE_NO_WARNINGS)
ENDIF(WIN32)

include_directories(.)

add_executable(iothub_client_sample_amqp ${iothub_client_sample_amqp_c_files} ${iothub_client_sample_amqp_h_files})
#TODO: debug folder is hard coded and horrible. Should be something like configuration
target_link_libraries(iothub_client_sample_amqp common iothub_client_amqp_transport iothub_client $ENV{proton_path}/qpid-proton/build/proton-c/Debug/qpid-protond.lib)
file(COPY $ENV{proton_path}/qpid-proton/build/proton-c/Debug/qpid-protond.dll DESTINATION ${CMAKE_CURRENT_BINARY_DIR}/Debug)