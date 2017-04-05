TARGET := demo.out
STATICLIB := libfma.a
SHAREDLIB := libfma.so
LIBSRC := fma.c
LIBOBJ := $(LIBSRC:.c=.o)
LIBDEP := $(LIBOBJ:.o=.d)
MAINSRC := main.c
MAINOBJ := $(MAINSRC:.c=.o)
MAINDEP := $(MAINOBJ:.o=.d)
DEPS := $(LIBDEP) $(MAINDEP)
OBJS := $(MAINOBJ) $(LIBOBJ)

CPPFLAGS :=
CPPFLAGS += -MMD
CPPFLAGS += -MP

CFLAGS :=
CFLAGS += -mfma


all : $(TARGET) $(STATICLIB) $(SHAREDLIB)

$(TARGET): $(OBJS) fma.go
	gcc -o $@ $(filter %.o,$^)
	strip $@
	go build fma.go

%.o : %.c
	gcc -c -o $@ $(CPPFLAGS) $(CFLAGS) $<

libfma.a: $(LIBOBJ)
	ar rcs $@ $^

libfma.so: $(LIBOBJ)
	echo "some command to make an $@ from $^" > $@

clean:
	rm -f *.o *.a $(TARGET)

-include $(DEPS)
