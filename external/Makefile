SHELL = /bin/bash

DIR = $(EXTERNAL_DIR)
SUB_NAME = "External"

define print
printf "%b%s%b\n" "$(2)" "$(1)" "$(NO_COLOR)"
endef

all: gtest libpng libjpeg

.PHONY : clean
clean: gtest_clean libpng_clean libjpeg_clean


GTEST_ALL = $(BASE_PATH)/$(BUILD_DIR)/gtest/gtest-all.o
GTEST_MAIN = $(BASE_PATH)/$(BUILD_DIR)/gtest/gtests_main.o
GTEST_DIR = $(BASE_PATH)/$(EXTERNAL_DIR)/googletest/googletest

.PHONY : gtest
gtest: gtest_start $(GTEST_ALL) $(GTEST_MAIN)
	$(call print,Linking libgtest.a,$(LINK_COLOR))
	ar -rc $(BASE_PATH)/$(BUILD_DIR)/libgtest.a $(GTEST_ALL)
	$(call print,Linking libgtest_main.a,$(LINK_COLOR))
	ar -rc $(BASE_PATH)/$(BUILD_DIR)/libgtest_main.a $(GTEST_MAIN)

.PHONY : gtest_start
gtest_start:
	$(call print,GoogleTest Library,$(TARGET_COLOR))

.PHONY : gtest_clean
gtest_clean: gtest_start
	$(call print,Removing gtest,$(CLEAN_COLOR))
	if [ -d "$(BASE_PATH)/$(BUILD_DIR)/gtest" ]; then\
	  rm $(BASE_PATH)/$(BUILD_DIR)/gtest -r; fi
	$(call print,Removing libgtest.a,$(CLEAN_COLOR))
	if [ -e "$(BASE_PATH)/$(BUILD_DIR)/libgtest.a" ]; then\
	  rm $(BASE_PATH)/$(BUILD_DIR)/libgtest.a; fi
	$(call print,Removing libgtest_main.a,$(CLEAN_COLOR))
	if [ -e "$(BASE_PATH)/$(BUILD_DIR)/libgtest_main.a" ]; then\
	  rm $(BASE_PATH)/$(BUILD_DIR)/libgtest_main.a; fi

$(GTEST_ALL):
	mkdir -p $(@D)
	$(call print,Building $@,$(COMPILE_COLOR))
	$(COMPILER) -isystem $(GTEST_DIR)/include -I$(GTEST_DIR) -pthread -c $(GTEST_DIR)/src/gtest-all.cc -o $@

$(GTEST_MAIN):
	mkdir -p $(@D)
	$(call print,Building $@,$(COMPILE_COLOR))
	$(COMPILER) -isystem $(GTEST_DIR)/include -I$(GTEST_DIR) -pthread -c $(GTEST_DIR)/src/gtest_main.cc -o $@

.PHONY : libpng
libpng:
	$(call print,LibPNG,$(TARGET_COLOR))
	if [ ! -f "./libpng/configure" ]; then cd libpng && ./autogen.sh; fi
	if [ ! -f "./libpng/Makefile" ]; then cd libpng&& ./configure --prefix=$(BASE_PATH)/$(BUILD_DIR)/libpng; fi
	if [ ! -d "$(BASE_PATH)/$(BUILD_DIR)/libpng" ]; then cd libpng && $(MAKE) install; fi

.PHONY : libpng_clean
libpng_clean:
	$(call print,LibPNG,$(CLEAN_COLOR))
	cd libpng && $(MAKE) clean
	if [ -d "$(BASE_PATH)/$(BUILD_DIR)/libpng" ]; then rm -r $(BASE_PATH)/$(BUILD_DIR)/libpng; fi
	if [ -e "./libpng/Makefile" ]; then rm libpng/Makefile; fi

.PHONY : libjpeg
libjpeg:
	$(call print,LibJPEG,$(TARGET_COLOR))
	printf "$(BASE_PATH)/$(BUILD_DIR)/libjpeg";
	if [ ! -f "./jpeg-8d/Makefile" ]; then cd jpeg-8d && ./configure --prefix=$(BASE_PATH)/$(BUILD_DIR)/libjpeg; fi
	if [ ! -d "$(BASE_PATH)/$(BUILD_DIR)/libjpeg" ]; then cd jpeg-8d && $(MAKE) install; fi

.PHONY : libjpeg_clean
libjpeg_clean:
	$(call print,LibJPEG,$(CLEAN_COLOR))
	cd jpeg-8d && $(MAKE) clean
	if [ -d "$(BASE_PATH)/$(BUILD_DI)/libjpeg" ]; then rm -r $(BASE_PATH)/$(BUILD_DIR)/libjpeg; fi
	if [ -e "./jpeg-8d/Makefile" ]; then rm jpeg-8d/Makefile; fi

