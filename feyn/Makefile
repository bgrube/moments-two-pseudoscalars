SHELL := $(shell which bash)
LATEX := TEXINPUTS=".:..:" latex --file-line-error --shell-escape
DVIPS := dvips
METAPOST := mpost
EPSTOPDF := epstopdf

STYLE_FILES = ../sty/packages.sty \
              ../sty/macros.sty

COMPILESTAMP := ./compile-stamp


feynman.ps: feynman.tex $(STYLE_FILES)
	rm --force feyn.*
	rm --force $(COMPILESTAMP)
	$(LATEX) feynman
	$(METAPOST) feyn
	$(LATEX) feynman
	NUM=1;for i in `cat feynman.lst`; \
	do \
		$(DVIPS) -E -pp $$NUM -o $$i.eps feynman; \
		$(EPSTOPDF) $$i.eps; \
		let NUM++; \
	done
	$(DVIPS) -o -R feynman
	touch $(COMPILESTAMP)
	gv feynman.ps

clean:
	rm --recursive --force --verbose ./*.{aux,,dvi,eps,log,lst,out,pdf,ps} ./feyn.* ./_minted-feynman
	rm --force --verbose $(COMPILESTAMP)
