TARGETS = ro-core-inst-inst
TARGETS_P9 = $(patsubst %,fol-derived/%.prover9,$(TARGETS))
TARGETS_CLIF = $(patsubst %,fol-derived/%.clif,$(TARGETS))
TARGETS_OWL = $(patsubst %,owl-derived/%.owl,$(TARGETS))

all: all_p9 all_clif all_owl
all_p9: $(TARGETS_P9)
all_clif: $(TARGETS_CLIF)
all_owl: $(TARGETS_OWL)

clean: 
	rm $(TARGETS_CLIF) $(TARGETS_P9) $(TARGETS_OWL)

%.prover9: %.clif
	clif-to-prover9 -rm example/3 -rm example/2 -rm label/2 -rm comment/2 -rm text_definition/2 -rm text_definition_xref/2 $< > $@

owl-derived/%.owl: fol-src/%-src.clif
	cl-expand-macros -m meta/bfo-meta-owl-mapping.clif  -m meta/text-metadata-owl-mapping.clif $< -to owl > $@

fol-derived/ro-core-inst-inst.%: fol-src/ro-core-inst-inst-src.clif
	cl-expand-macros -m meta/bfo-meta.clif -to $* $< > $@

fol-derived/ro-core-type-type.%: fol-src/ro-core-type-type-src.clif
	cl-expand-macros -m meta/bfo-meta.clif $< > $@.tmp && cl-expand-macros -m meta/bfo-meta-type-level.clif $@.tmp -to $* > $@

