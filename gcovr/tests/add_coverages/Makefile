CFLAGS= -fprofile-arcs -ftest-coverage -fPIC

all:
	$(CXX) $(CFLAGS) -c foo.cpp -o foo.o
	$(CXX) $(CFLAGS) -c bar.cpp -o bar.o
	$(CXX) $(CFLAGS) -DFOO -c main.cpp -o main_foo.o
	$(CXX) $(CFLAGS) main_foo.o foo.o -o testcase_foo
	$(CXX) $(CFLAGS) -DBAR -c main.cpp -o main_bar.o
	$(CXX) $(CFLAGS) main_bar.o bar.o -o testcase_bar

run: txt xml html sonarqube json

# Enable JSON output via the --json-pretty mode.
# However, this option cannot take a filename directly
# so that "-o" is used.
coverage_foo.json:
	./testcase_foo
	$(GCOVR) -d --json-pretty -o $@

# Just use --json and pass the output filename directly.
coverage_bar.json:
	./testcase_bar
	$(GCOVR) -d --json $@

txt: coverage_foo.json coverage_bar.json
	$(GCOVR) -a coverage_foo.json -a coverage_bar.json -o coverage.txt

xml: coverage_foo.json coverage_bar.json
	$(GCOVR) -a coverage_foo.json -a coverage_bar.json -x -o coverage.xml

html: coverage_foo.json coverage_bar.json
	$(GCOVR) -a coverage_foo.json -a coverage_bar.json --html-details -o coverage.html

sonarqube: coverage_foo.json coverage_bar.json
	$(GCOVR) -a coverage_foo.json -a coverage_bar.json --sonarqube sonarqube.xml

# Use both --json and --json-pretty here
json: coverage_foo.json coverage_bar.json
	$(GCOVR) -a 'coverage_*.json' --json-pretty --json coverage.json

clean:
	rm -f testcase_*
	rm -f *.gc*
	rm -f *.o
	rm -f coverage*.* sonarqube*.*
