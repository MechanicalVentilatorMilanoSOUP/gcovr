CFLAGS= -fprofile-arcs -ftest-coverage -fPIC

all:
	- mkdir objs
	cd subdir; $(CXX) $(CFLAGS) -c A/file1.cpp -o ../objs/file1.o
	cd subdir; $(CXX) $(CFLAGS) -c A/file1.cpp -o ../objs/file1.o
	cd subdir; $(CXX) $(CFLAGS) -c A/file2.cpp -o ../objs/file2.o
	cd subdir; $(CXX) $(CFLAGS) -c A/file3.cpp -o ../objs/file3.o
	cd subdir; $(CXX) $(CFLAGS) -c A/file4.cpp -o ../objs/file4.o
	cd subdir; $(CXX) $(CFLAGS) -c A/file7.cpp -o ../objs/file7.o
	cd subdir; $(CXX) $(CFLAGS) -c A/C/file5.cpp -o ../objs/file5.o
	cd subdir; $(CXX) $(CFLAGS) -c A/C/D/file6.cpp -o ../objs/file6.o
	cd subdir; $(CXX) $(CFLAGS) -c B/main.cpp -o ../objs/main.o
	cd subdir; $(CXX) $(CFLAGS) ../objs/file1.o ../objs/file2.o ../objs/file3.o ../objs/file4.o ../objs/file5.o ../objs/file6.o ../objs/file7.o ../objs/main.o -o ./testcase

run: txt xml html sonarqube

coverage.json:
	./subdir/testcase
	$(GCOVR) -r subdir --object-directory objs --json coverage.json

txt: coverage.json
	$(GCOVR) -r subdir -a $< -o coverage.txt

xml: coverage.json
	$(GCOVR) -r subdir -a $< -x -o coverage.xml

html: coverage.json
	$(GCOVR) -r subdir -a $< --html-details -o coverage.html

sonarqube: coverage.json
	$(GCOVR) -r subdir -a $< --sonarqube sonarqube.xml

clean:
	rm -f ./subdir/testcase
	rm -f *.gc* */*.gc* */*/*.gc* */*/*/*.gc* */*/*/*/*.gc*
	rm -f *.o */*.o */*/*.o */*/*/*.o */*/*/*/*.o
	rm -f coverage*.* sonarqube*.*
