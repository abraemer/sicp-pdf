# Contributed by holomorph, 2013.
# Added to by Andres Raba, 2013-2015.

FIG := $(patsubst %.svg,%.pdf,$(wildcard fig/*/*.svg))
DIR := $(shell pwd)

all: sicp.pdf sicp-print.pdf

print: sicp-print.pdf

sicp.pdf: sicp.tex exercises.tex figures.tex coverpage.pdf ${FIG}
	latexmk -pdflatex="lualatex %O %S" -pdf -dvi- -ps- $<; \
	mv sicp.pdf ..

sicp.tex: sicp.texi preamble.tex postamble.tex texi-to-latex.pl
	./texi-to-latex.pl $<

sicp-print.pdf: sicp-print.tex exercises.tex figures.tex coverpage-print.pdf ${FIG}
	latexmk -pdflatex="lualatex %O %S" -pdf -dvi- -ps- $<; \
	mv sicp-print.pdf ..

sicp-print.tex: sicp.texi preamble-print.tex postamble.tex texi-to-latex-print.pl
	./texi-to-latex-print.pl -o sicp-print.tex $<

exercises.tex figures.tex: ex-fig-ref.pl
	./ex-fig-ref.pl -e > exercises.tex; \
	./ex-fig-ref.pl -f > figures.tex

%.pdf: %.svg
	inkscape ${DIR}/$< --export-filename ${DIR}/$@

clean:
	latexmk -CA

clean-all: clean
	${RM} ${FIG} sicp.tex sicp-print.tex exercises.tex figures.tex coverpage.pdf coverpage-print.pdf

.PHONY: all print clean clean-all
