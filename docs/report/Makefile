#Makefile for (cs)latex
NAME = main
all: ${NAME}.dvi
WIKI_DIR = "../opengl-android.wiki"
WIKI_NAME = "report"

# Vyroba PDF primo z DVI by byla prijemnejsi, ale vetsina verzi dvipdfm nici obrazky
# ${NAME}.pdf: ${NAME}.dvi
#	dvipdfm -o $@ -p a4 -r 600 $<
pdf: ${NAME}.pdf

${NAME}.pdf: ${NAME}.ps
	ps2pdf $< $@

${NAME}.ps: ${NAME}.dvi
	dvips -o $@ -D600 -t a4 $<

# LaTeX je potreba spustit dvakrat, aby spravne spocital odkazy
${NAME}.dvi: ${NAME}.tex $(wildcard *.tex) pictures
	latex $<
	latex -src $<
#latex prijima pouze eps, je tedy potrebovat zkonvertovat obrazky
pictures: $(wildcard *.png *.jpg)
	convert $< `echo $<|sed 's:\(.*\)jpg:\1:'|sed 's:\(.*\)png:\1:'`eps

pdf: ${NAME}.pdf

read: ${NAME}.dvi
      ifeq (${USER}, ondra)
	xdvi ${NAME}.dvi &
      else
	okular ${NAME}.dvi &
      endif

readpdf: ${NAME}.pdf
	acroread ${NAME}.pdf &

clean:
	rm -f *.log  *.dvi *.aux *.toc *.lof *.out ${NAME}.ps ${NAME}.pdf ${NAME}\ *conflicted*.ps ${NAME}\ *conflicted*.pdf

wiki: ${NAME}.pdf
	pandoc -t mediawiki -o text.wiki text.tex
	#insert line(s) at the beginning 1i -insert first line
	sed -i 1i"#summary Report exported by pandoc(latex2wiki converter)\n#sidebar navigation" text.wiki 
	mv text.wiki ${WIKI_DIR}/${WIKI_NAME}.wiki
	cp *.eps ${WIKI_DIR}/img
	cp ${NAME}.pdf ${WIKI_DIR}/${WIKI_NAME}.pdf
