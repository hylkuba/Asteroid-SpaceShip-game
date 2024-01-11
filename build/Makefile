#   /**
#    * @author Jakub Hýl <hylkuba@gmail.com>
#    * @date 11.01.2024
#   */

default:
	g++ ../src/*.cpp -o Game.exe -O2 -Wall -Wno-missing-braces -I ../include/ -L ../lib/ -lraylib -lopengl32 -lgdi32 -lwinmm

NAME = Asteroid-SpaceShip-game

ifeq ($(shell uname),Linux)
    CXX = g++
    LD = g++
    CXXFLAGS = -Wall -pedantic -std=c++17 -g -O2 -fsanitize=address -I ../include
    LDFLAGS = -fsanitize=address -L ../lib -lm -lpthread -ldl -lrt -lX11 -lraylib
    TARGET = $(NAME)
else
    CXX = g++
    LD = g++ -mconsole
    CXXFLAGS = -Wall -pedantic -Wextra -std=c++17 -g -O2 -Wno-missing-braces -mconsole -I ../include
    LDFLAGS = -m64 -L ../lib -lraylib -lopengl32 -lgdi32 -lwinmm -lm
    TARGET = $(NAME).exe
endif

HEADERS = $(wildcard src/*.h)

DIR_NAME = bin

OBJS = $(DIR_NAME)/main.o

$(TARGET): $(OBJS)
	$(LD) $(LDFLAGS) $(OBJS) -o $(TARGET)

#-----------------------------------------------------------------------
# All .o objects stored in folder
run: | $(DIR_NAME) compile
	./$(TARGET)

$(DIR_NAME):
	mkdir -p $(DIR_NAME)

compile: $(DIR_NAME) $(OBJS)
	$(LD) $(LDFLAGS) $(OBJS) -o $(NAME)

doc: Doxyfile $(HEADERS)
	doxygen Doxyfile

.PHONY: clean
clean:
	rm -rf $(DIR_NAME) $(TARGET) doc/ 2>/dev/null

$(DIR_NAME)/%.o: ../src/%.cpp $(HEADERS)
	$(CXX) $(CXXFLAGS) -c $< -o $@

.PHONY: all
all: doc run clean

#-----------------------------------------------------------------------
l:
	cat Makefile src/*.h src/*.cpp | wc -l

la:
	cat Makefile src/* | wc -l
#-----------------------------------------------------------------------
# Object files dependencies
$(DIR_NAME)/main.o: ../src/main.cpp
	$(CXX) $(CXXFLAGS) -c $< -o $@
