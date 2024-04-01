SHELL := $(shell which bash)
LATEX := TEXINPUTS=".:..:" latexmk -pdf

STYLE_FILES = ../sty/packages.sty \
              ../sty/macros.sty
WRAPPER := ./documentWrapper.tex
SOURCES = ./pipiomega_analyzer.tex

PDFS = $(SOURCES:.tex=.pdf)
COMPILESTAMP := ./compile-stamp


.PHONY: all

default: all

all: $(PDFS)

%.pdf: %.tex $(WRAPPER) $(STYLE_FILES)
	rm --force $(COMPILESTAMP)
	$(LATEX) -pdflatex="pdflatex --file-line-error --shell-escape --synctex=1 %O '\def\tikzFigureFile{'$*'}\input{%S}'" $(WRAPPER)
	mv --verbose $(basename $(WRAPPER)).pdf $(basename $*).pdf
	touch $(COMPILESTAMP)

clean: WRAPPER_NAME = $(basename $(WRAPPER))
clean:
	rm --recursive --force --verbose $(WRAPPER_NAME).{aux,pdf,fls,fdb_latexmk,log,out,soc,synctex.gz} ./_minted-$(notdir $(WRAPPER_NAME))
	for i in $(SOURCES); do \
		rm --force --verbose $${i%.tex}.pdf; \
	done
	rm --force $(COMPILESTAMP)
