# Unix_Assignment_GN
##Data Inspection

###Attributes of fang_et_al_genotypes

here is my snippet of code used for data inspection: 
$ wc fang_et_al_genotypes.txt
$ du -h fang_et_al_genotypes.txt
$ awk -F "\t" '{print NF; exit}' fang_et_al_genotypes.txt

By inspecting this file I learned that:
1. 2783 lines 
2. 2744038 words 
3. 11051939 bytes
4. 6.1M
5. 986 columns

###Attributes of snp_position.txt

here is my snippet of code used for data inspection
$ wc snp_position.txt
$ du -h snp_position.txt
$ awk -F "\t" '{print NF; exit}' snp_position.txt
By inspecting this file I learned that:
1. 984 lines
2. 13198 words
3. 82763 bytes
4. 38K 
5. 15 columns
