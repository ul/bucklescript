ifdef WIN32
	EXE := .exe
endif
ifndef EXE
	EXE := # empty
endif
NATIVE=ocamlopt.opt$(EXE)
BSC_FLAGS= -w -40-30 -I ../runtime -I ../stdlib -bs-files
BSC=./bsc.exe
OCAMLOPT_FLAGS= -g -w -40-30 ../stubs/ext_basic_hash_stubs.c
# -inline 1000 makes size too large
# TODO: make sure it can be bootstrapped, at least is a very good
# test case of our optimizations
bsppx.exe: bsppx.mli bsppx.ml
	$(NATIVE) $(OCAMLOPT_FLAGS) $^ -o $@

bspp.exe:   bspp.mli bspp.ml
	$(NATIVE) $(OCAMLOPT_FLAGS) $^ -o $@

bsdep.exe: bsdep.mli bsdep.ml
	$(NATIVE) $(OCAMLOPT_FLAGS) $^ -o $@

bsb.exe:  bsb.mli bsb.ml
	$(NATIVE) $(OCAMLOPT_FLAGS) unix.cmxa str.cmxa $^ -o $@

bsb_helper.exe:  bsb_helper.mli bsb_helper.ml
	$(NATIVE) $(OCAMLOPT_FLAGS) unix.cmxa str.cmxa -w -a $^ -o $@

refmt.exe: refmt_main.mli refmt_main.ml
	$(NATIVE) -I +compiler-libs ocamlcommon.cmxa $^ -o $@

reactjs_jsx_ppx.exe:reactjs_ppx.mli reactjs_ppx.ml
	$(NATIVE) -I +compiler-libs ocamlcommon.cmxa $^ -o $@

config_whole_compiler.ml:config_whole_compiler.mlp ../config.js
	node ../config.js
bsc.exe: config_whole_compiler.mli config_whole_compiler.ml  whole_compiler.mli whole_compiler.ml
	$(NATIVE) $(OCAMLOPT_FLAGS) $^  -o $@

bspack.exe: bspack.mli bspack.ml
	$(NATIVE) $(OCAMLOPT_FLAGS) unix.cmxa  $^ -o $@

bspack.js:	bspack.mli bspack.ml
	$(BSC) $(BSC_FLAGS) $^

all: bsppx.exe bspp.exe bsdep.exe bsc.exe bspack.exe bsb.exe bsb_helper.exe refmt.exe reactjs_jsx_ppx.exe
