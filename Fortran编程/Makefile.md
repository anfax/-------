# Fortran项目通用Makefile

## 定义变量

```Makfile
SRC_DIR = ./
OBJS_DIR = ./obj/
EXE_DIR = ./bin/
EXE = DynamicStarkControl.exe
CFLAGS = -O3
LFLAGS =
LIBS =
```

## 使用通配符获取源文件和目标文件列表

```Makefile
SRCS_ford1 = $(notdir $(filter %.for %.f90 %.f %.f77,$(wildcard $(SRC_DIR)*)))
OBJS_ford1 = $(addprefix $(OBJ_DIR),$(SRCS_ford1:.for=.o) $(SRCS_ford1:.f90=.o) $(SRCS_ford1:.f=.o) $(SRCS_ford1:.f77=.o))
DEPS_ford1 = $(addprefix $(OBJ_DIR),$(SRCS_ford1:.for=.d) $(SRCS_ford1:.f90=.d) $(SRCS_ford1:.f=.d) $(SRCS_ford1:.f77=.d))
```

## 声明伪目标

```Makefile
.PHONY: all clean
```

## 默认目标

```Makefile
all : $(EXE)
```

## 链接可执行文件

```Makefile
$(EXE) : $(OBJS_ford1)
    @mkdir -p $(EXE_DIR)
    $(LD) -o $(EXE_DIR)$(EXE) $(OBJS_ford1) $(LFLAGS) $(LIBS)
```

## 编译源文件

```Makfile
$(OBJS_DIR)%.o: $(SRC_DIR)%.for
    @mkdir -p $(OBJS_DIR)
    $(FC) $(CFLAGS) -gen-dep -c $< -o $@
```

## 包含依赖文件

```makefile
-include $(DEPS_ford1)
```

## 清理目标文件和可执行文件

```Makefile
clean :
    rm -f $(OBJS_DIR)*.*
    rm -f $(EXE_DIR)$(EXE)
```

## 根据编译器选择不同的选项

```makefile
ifeq ($(FC),ifort)
  LD = ifort
else ifeq ($(FC),gfortran)
  LD = gfortran
  CFLAGS += -MMD
endif
```
