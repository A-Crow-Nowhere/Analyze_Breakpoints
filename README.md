cd~
cd envs/yaml
wget https://raw.githubusercontent.com/A-Crow-Nowhere/MalariAPI/main/yaml/breakpoints.yml
conda env create -f breakpoints.yml
conda activate breakpointenv

cd~
mkdir -p tools/breakpoints/
cd tools/breakpoints/
wget https://raw.githubusercontent.com/A-Crow-Nowhere/MalariAPI/main/scripts/analyze_breakpoints/breakpoints.sh
wget https://raw.githubusercontent.com/A-Crow-Nowhere/MalariAPI/main/scripts/analyze_breakpoints/intergenic.sh
chmod +x breakpoints.sh

#Call DG minima in 2000bp range around teh 5'&3' region of a bed region in sliding 50bp windows.
#The peak closest to the input breakpoints are retained. Also calculates GC content in a 100bp around that breakpoint.
./breakpoints.sh <regionstoanalyze.bed> <reference.fasta> => final_summary.tsv

#Determine if peak position called in final_summary.tsv is in an intergenic region based on CDS regions in a .gff file. 
./intergenic.sh <final_summary.clean.tsv> <reference.gff> => finall_summary.annotated.tsv
