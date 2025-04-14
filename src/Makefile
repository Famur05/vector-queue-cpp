#===========================================================================
CC = g++
FLAGS = -std=c++17 -pedantic -Wall -Werror -Wextra -lm
#===========================================================================
TARGET = s21_vector_queue.a
#===========================================================================
TEST_FLAGS = -lgtest -lgmock -pthread -lgtest_main
#===========================================================================
FILE = stl/queue/s21_queue.cc stl/vector/s21_vector.cc
FILE_H = stl/queue/s21_queue.h stl/vector/s21_vector.h
#===========================================================================
all: $(TARGET)

$(TARGET):
	$(CC) $(FLAGS) -c $(FILE)
	ar rcs $(TARGET) *.o
	ranlib $(TARGET)
	rm -rf *.o

test: $(TARGET)
	$(CC) tests/*.cc $(TARGET) $(FLAGS) $(TEST_FLAGS) -o test.out
	./test.out

gcov_report: clean
	$(CC) $(FILE) tests/*.cc $(FLAGS) $(TEST_FLAGS) --coverage -o coverage.out
	./coverage.out
	lcov -c -d ./ -o coverage.info
	genhtml -o coverage_html coverage.info 
	open coverage_html/index.html

valgrind: clean test
	valgrind --tool=memcheck --leak-check=yes  ./test.out

clang_i:
	clang-format -i -style=Google $(FILE) $(FILE_H)

clang_n:
	clang-format -n -style=Google $(FILE) $(FILE_H)

clean:
	rm -rf coverage_html *.gcno *.gcda *.out *.info *.a *.o

rebuild: clean all
#===========================================================================
