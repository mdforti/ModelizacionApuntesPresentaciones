# INCLUDES=./FRAMES/title.tex ./FRAMES/01-WHOIAM.tex 
PDFLATEX=pdflatex # -interaction=batchmode 

PREAMBLE=./PREAMBLE/*.tex
INCLUDES=./01-Problema/*.tex  ./02-Matriza/*.tex ./03-CondicionContorno/*.tex

all: notes.pdf beamer.pdf

notes.pdf: notes.aux # figures ${INCLUDES} main.tex notes.tex lists
	${PDFLATEX} notes.tex

notes.aux: handout.aux #notes.tex ${INCLUDES} main.tex lists figures
	${PDFLATEX} notes.tex

beamer.pdf: ${INCLUDES} main.tex beamer.tex figures lists
	${PDFLATEX} beamer.tex
	${PDFLATEX} beamer.tex

handout.pdf:  handout.aux # handout.tex figures ${INCLUDES} main.tex lists
	${PDFLATEX} handout.tex

handout.aux: handout.tex figures ${INCLUDES} main.tex lists
	${PDFLATEX} handout.tex

##########################################	
figures: Figura1-Chapa Figura1-Grilla Figura-Tiempos-Escaleo 07-CondicionesDeContorno2

Figura1-Chapa: 01-Problema/Figura01-01-Chapa.tikz
	cd 01-Problema; ${PDFLATEX} Figura01-01-Chapa.tikz ; cd ..

Figura1-Grilla: 01-Problema/01-Figura-Grilla.tikz
	cd 01-Problema; ${PDFLATEX} 01-Figura-Grilla.tikz ; cd ..

Figura-Tiempos-Escaleo: DATA/plot-tiempos.gpi
	cd DATA; gnuplot plot-tiempos.gpi ; ${PDFLATEX} tiempos.tex ; cd ..

07-CondicionesDeContorno2:
	make -C ./07-CondicionesDeContorno2



#########################################

clase-lo/clase-lo.pdf: ./clase-lo
	make -C ./clase-lo

.PHONY: clase-lo/clase-lo.pdf   07-CondicionesDeContorno2 


lists: 
	grep -e \\label{Eq.*}  */*.tex > ListOfEquations.md      	
	grep -e \\label{[fF]ig.*}  */*.tex > ListOfFigures.md
	grep -e \\[label=Frame.*\\] */*.tex > ListOfFrames.md

clean: 
	find -iname  \*.log \
	  -o -iname \*.out \
	  -o  -iname \*.aux \
	  -o  -iname \*.toc \
	  -o  -iname \*.vrb \
	  -o  -iname \*.snm \
	  -o  -iname \*.nav \
	  |xargs rm

cleanpdfs:
	find -iname \*.pdf -exec rm {} +


