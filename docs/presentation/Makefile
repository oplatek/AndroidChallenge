NAME = main
all: ${NAME}.pdf

${NAME}.pdf: ${NAME}.tex $(wildcard *.tex)
	pdflatex $<

pdf:
	xpdf -remote 127.0.0.1 -raise ${NAME}.pdf &
clean:
	rm -f *.vrb *.nav *.snm *.log  *.dvi *.aux *.toc *.lof *.out ${NAME}.ps ${NAME}.pdf
