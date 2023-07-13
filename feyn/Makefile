SHELL:=$(shell which bash)
LATEX:=TEXINPUTS=".:..:" latex
DVIPS:=dvips
METAPOST:=mpost
EPSTOPDF:=epstopdf

feynman.ps: feynman.tex
	rm -f feyn.*
	rm -f compile-stamp
	$(LATEX) -shell-escape feynman
	$(METAPOST) feyn
	$(LATEX) -shell-escape feynman
	num=1;for i in `cat feynman.lst`;do \
		$(DVIPS) -E -pp $$num -o $$i.eps feynman; \
		$(EPSTOPDF) $$i.eps;let num++; \
	done
	$(DVIPS) -o -R feynman
	touch compile-stamp
	gv feynman.ps

clean:
	rm -fv ./*.{aux,,dvi,eps,log,lst,out,pdf,ps}
	rm -fv ./feyn.*
	rm -fv ./compile-stamp
	rm -fv ./*~
	rm -rfv ./_minted-feynman
