#!/bin/bash
# Generates statistical analysis and plots and then create the pdf

# Note: Packages needed are inkscape, libcanberra-gtk-module,
# libcanberra-gtk3-module, texlive, python and its modules.

read -r -p "Do you want to regenerate the plots ? [Y/N] " response
response=${response,,}    # tolower
if [[ "$response" =~ ^(yes|y)$ ]]
then
    for d in data/*/ ; do
        echo -e "\nGenerating numa-plots for $d"
        ./scripts/plotScheduleQ.py $d
        ./scripts/plotBags.py $d
        ./scripts/plotChains.py $d
        ./scripts/plotBlocks.py $d
        ./scripts/plotTopPerformers.py $d
        ./scripts/plotWorstPerformers.py $d
    done

    for d in data_smp/*/ ; do
        echo -e "\nGenerating smp-plots for $d"
        ./scripts/plotScheduleQ.py $d
        ./scripts/plotBags.py $d
        ./scripts/plotChains.py $d
        ./scripts/plotBlocks.py $d
        ./scripts/plotTopPerformersSMP.py $d
    done
fi

# Generate the thesis PDF
pdflatex thesis.tex
bibtex   thesis.aux
pdflatex thesis.tex
pdflatex thesis.tex

# Generate the view all PDF for numa
pdflatex presentation/overview_numa.tex
mv overview_numa.pdf presentation/

# Generate the view all PDF for smp
pdflatex presentation/overview_smp.tex
mv overview_smp.pdf presentation/

# Delete unwanted auto-generated files
rm -rf *.aux *.loa *.lof *.log *.lot *.toc *.bbl *.blg *.brf *.out
