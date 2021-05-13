OUT=websocket pubsub
CFLAGS=-Wall -Wextra -I../src/http-parser/
LDFLAGS=-levent -lpthread

DEBUG_FLAGS=

# if `make` is run with DEBUG=1, include debug symbols
ifeq ($(DEBUG),1)
DEBUG_FLAGS += -O0
ifeq ($(shell cc -v 2>&1 | grep -cw 'gcc version'),1) # GCC used: add GDB debugging symbols
DEBUG_FLAGS += -ggdb3
else ifeq ($(shell gcc -v 2>&1 | grep -cw 'clang version'),1) # Clang used: add LLDB debugging symbols
DEBUG_FLAGS += -g3 -glldb
endif
else
DEBUG_FLAGS += -O3
endif

CFLAGS += $(DEBUG_FLAGS)
LDFLAGS += $(DEBUG_FLAGS)

all: $(OUT) Makefile

websocket: websocket.o ../src/http-parser/http_parser.o
	$(CC) -o $@ $^ $(LDFLAGS)

pubsub: pubsub.o
	$(CC) -o $@ $< $(LDFLAGS)

%.o: %.c Makefile
	$(CC) -c $(CFLAGS) -o $@ $<

clean:
	rm -f *.o $(OUT)

