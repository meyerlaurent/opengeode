all: test

parse:
	../../../opengeode.py basic.pr system_structure.pr --check

generate-ada:
	@../../../opengeode.py basic.pr system_structure.pr --check --toAda

compile-ada: generate-ada
	@asn1.exe -Ada dataview-uniq.asn -typePrefix asn1Scc -equal
	@gnatmake -c *.adb

run-ada: compile-ada
	@gcc -c test_ada.c
	@gnatbind -n basic.ali
	@gnatlink test_ada.o basic.ali -lgnat -lm -o testcase
	@./testcase | diff expected -

test: run-ada
	echo "ALL OK!"

clean:
	@rm -rf *.adb *.ads *.pyc runSpark.sh spark.idx *.o *.ali gnat.cfg examiner bin *.wrn *.gpr testcase
