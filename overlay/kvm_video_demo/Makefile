# T527 Video Demo - 独立编译 Makefile
# 不依赖 SDK 环境变量

# 交叉编译器
CC = /home/ubuntu/T527_Tina5.0_SDK/out/toolchain/gcc-arm-10.3-2021.07-x86_64-aarch64-none-linux-gnu/bin/aarch64-none-linux-gnu-gcc
CXX = /home/ubuntu/T527_Tina5.0_SDK/out/toolchain/gcc-arm-10.3-2021.07-x86_64-aarch64-none-linux-gnu/bin/aarch64-none-linux-gnu-g++

# SDK 路径
SDK_PATH = /home/ubuntu/T527_Tina5.0_SDK/buildroot/package/auto/sdk_lib
KERN_PATH = /home/ubuntu/T527_Tina5.0_SDK/kernel/linux-5.15
OUT_PATH = /home/ubuntu/T527_Tina5.0_SDK/out/t527/demo_linux_aiot

# 库路径
SDK_LIBS = $(SDK_PATH)/libs
CEDAR_LIBS = $(OUT_PATH)/buildroot/buildroot/target/usr/lib

TARGET = kvm_video
CAP_TEST = capture_test

CFLAGS = -g -O0 -pipe -Wall -W -fPIC
CXXFLAGS = -g -O0 -pipe -Wall -W -fPIC

DEFINES += -DUSE_LOGCAT -DLOG_LEVEL=6

# 头文件
INCS = -I./ \
       -I$(KERN_PATH)/arch/arm64/include \
       -I$(SDK_PATH)/cedarx/include/libcedarc/include \
       -I$(SDK_PATH)/include \
       -I$(SDK_PATH)/include/storage \
       -I$(SDK_PATH)/include/disp2 \
       -I$(SDK_PATH)/include/cutils \
       -I$(SDK_PATH)/include/utils \
       -I$(SDK_PATH)/include/camera

# 采集测试 - 使用和 video_demo 相同的完整库
CAP_LIBS = -lsdk_memory -lMemAdapter -lVE -lcdc_base -lsdk_log \
           -lvencoder -lvenc_jpeg -lvenc_common -lvenc_h264 -lvenc_h265 -lvenc_base \
           -lsdk_encoder -lpthread -lsdk_awnn -lVIPlite -lVIPuser

# 完整版需要所有库
LIBS = -lsdk_memory -lMemAdapter -lVE -lcdc_base -lsdk_log \
       -lvencoder -lvenc_jpeg -lvenc_common -lvenc_h264 -lvenc_h265 -lvenc_base \
       -lsdk_encoder -lpthread -lsdk_awnn -lVIPlite -lVIPuser

LDFLAGS = -L$(SDK_LIBS) -L$(CEDAR_LIBS)

all: $(TARGET)

$(TARGET): main.cpp
	$(CXX) $(CXXFLAGS) $(DEFINES) $(INCS) -o $(TARGET) main.cpp $(LIBS) $(LDFLAGS)
	@echo "生成 $(TARGET) 成功!!!"

$(CAP_TEST): main_capture_test.cpp
	$(CXX) $(CXXFLAGS) $(DEFINES) $(INCS) -o $(CAP_TEST) main_capture_test.cpp $(CAP_LIBS) $(LDFLAGS)
	@echo "生成 $(CAP_TEST) 成功!!!"

capture_simple: main_simple.cpp
	$(CXX) $(CXXFLAGS) $(DEFINES) $(INCS) -o $@ $< $(CAP_LIBS) $(LDFLAGS)
	@echo "生成 $@ 成功!!!"

clean:
	rm -f $(TARGET) $(CAP_TEST) test_encoder *.o

test_encoder: test_encoder.cpp
	$(CXX) $(CXXFLAGS) $(DEFINES) $(INCS) -o $@ $< $(LIBS) $(LDFLAGS)
	@echo "生成 $@ 成功!!!"

.PHONY: all clean test_encoder
