UNAME_S := $(shell uname -s)
HEADERS := $(wildcard *.h)
VPATH := src:include:tests

ifeq ($(UNAME_S),Darwin)
GCOV := xcrun llvm-cov gcov
else
GCOV := llvm-cov gcov
endif

CC   := clang

CFLAGS += $(if $(COVERAGE), -fprofile-arcs -ftest-coverage )
CFLAGS += $(if $(DEBUG), -DDEBUG=1 )
CFLAGS += -Werror -Iinclude -g

LDLIBS += $(if $(or $(COVERAGE),$(DEBUG)), -g )
LDLIBS += $(if $(COVERAGE), --coverage )

test_{{cookiecutter.project_name|lower}}: LDLIBS += -lcmocka
test_{{cookiecutter.project_name|lower}}: {{cookiecutter.project_name|lower}}.o test_{{cookiecutter.project_name|lower}}.o

.PHONY: test
test: test_{{cookiecutter.project_name|lower}}
	./test_{{cookiecutter.project_name|lower}} 

{{cookiecutter.project_name|lower}}.o: {{cookiecutter.project_name|lower}}.h

valgrind_%: %
	valgrind --leak-check=full --error-exitcode=1 ./$* 

coverage: COVERAGE=1
coverage: test
	$(GCOV) $(SRCS)

TAGS: $(SRCS) {{cookiecutter.project_name|lower}}.h test_*.[ch]
	etags $^

docs: $(HEADERS)
	doxygen

.PHONY: clean
clean:
	rm -rf *.o *.gcda *.gcno test_{{cookiecutter.project_name|lower}} *.dSYM html/ latex/
