# Unix_Assignment_GN
## Data Inspection

### Attributes of fang_et_al_genotypes

here is my snippet of code used for data inspection:
1. $ wc fang_et_al_genotypes.txt
2. $ du -h fang_et_al_genotypes.txt
3. $ awk -F "\t" '{print NF; exit}' fang_et_al_genotypes.txt

By inspecting this file I learned that:
1. 2783 lines 
2. 2744038 words 
3. 11051939 bytes
4. 6.1M
5. 986 columns

### Attributes of snp_position.txt

here is my snippet of code used for data inspection
1. $ wc snp_position.txt
2. $ du -h snp_position.txt
3. $ awk -F "\t" '{print NF; exit}' snp_position.txt

By inspecting this file I learned that:
1. 984 lines
2. 13198 words
3. 82763 bytes
4. 38K 
5. 15 columns

## Prep_Data Processing

### Maize Data

$ grep -E "ZMMLR|ZMMIL|ZMMMR|Sample_ID" fang_et_al_genotypes.txt > maize_genotypes.txt
This command searches for ZMMLR, ZMMIL, ZMMMR and Sample_ID and then save into a new file called maize_genotypes

$ awk -f transpose.awk maize_genotypes.txt > maize_transposed_genotypes.txt
This command transposes genotype data so the columns become rows

$ sed -i '1,3d' maize_transposed_genotypes.txt 
This comand removes header of this file

$ sed '1d' snp_position.txt > snp_position_nohead.txt
This command removes header of this file

$ sort -k1,1V snp_position_nohead.txt > snp_position_nohead_sorted.txt
This command sorts data in column 1 that are alpha-numeric and V opption can recognize number inside strings. 

$  sort -k1,1V maize_transposed_genotypes.txt > maize_transposed_genotypes_sorted.txt 
This command sort data in column 1 that are alpha-numeric and V opption can recognize number inside strings. 

$join -1 1 -2 1 -t $'\t' snp_position_nohead_sorted.txt maize_transposed_genotypes_sorted.txt > maize_transposed_genotypes_joined.bed 
merge snp position with genotypes

$sort -k2,2 maize_transposed_genotypes_joined.bed > maize_transposed_genotypes_joined_chr.bed
sort in chromosome orders, column 2.

### Teosinte Data

$ grep -E "ZMPBA|ZMPIL|ZMPJA|Sample_ID" fang_et_al_genotypes.txt > teosinte_genotypes.txt 
#grep ZMPBA, ZMPIL, and ZMPJA

$ awk -f transpose.awk teosinte_genotypes.txt > teosinte_transposed_genotypes.txt

$ sed -i '1,3d' teosinte_transposed_genotypes.txt

$ sort -k1,1V teosinte_transposed_genotypes.txt > teosinte_transposed_genotypes_sorted.txt 
#sort teosinte

$ join -1 1 -2 1 -t $'\t' snp_position_nohead_sorted.txt teosinte_transposed_genotypes_sorted.txt > teosinte_transposed_genotypes_joined.bed 
#join snp with teosinte

$ sort -k3,3 teosinte_transposed_genotypes_joined.bed > teosinte_transposed_genotypes_joined_chr.bed 
#sort chrom colum

$ grep -v "^#" teosinte_transposed_genotypes_joined_chr.bed | cut -f3 | uniq -c
#count chro
output
     153 1
     53 10
    118 2
    103 3
     88 4
    119 5
     76 6
     97 7
     62 8
     60 9
      6 multiple
     27 unknown
     
### Data Processing

### Maize Data

$ sed -n '1,155p' maize_transposed_genotypes_joined_chr.bed > maize_transposed_genotypes_joined_chr1.bed
$ sed -n '156,208p' maize_transposed_genotypes_joined_chr.bed > maize_transposed_genotypes_joined_chr10.bed
$ sed -n '209,335p' maize_transposed_genotypes_joined_chr.bed > maize_transposed_genotypes_joined_chr2.bed
$ sed -n '336,442p' maize_transposed_genotypes_joined_chr.bed > maize_transposed_genotypes_joined_chr3.bed
$ sed -n '443,533p' maize_transposed_genotypes_joined_chr.bed > maize_transposed_genotypes_joined_chr4.bed
$ sed -n '534,655p' maize_transposed_genotypes_joined_chr.bed > maize_transposed_genotypes_joined_chr5.bed
$ sed -n '656,731p' maize_transposed_genotypes_joined_chr.bed > maize_transposed_genotypes_joined_chr6.bed
$ sed -n '732,828p' maize_transposed_genotypes_joined_chr.bed > maize_transposed_genotypes_joined_chr7.bed
$ sed -n '829,890p' maize_transposed_genotypes_joined_chr.bed > maize_transposed_genotypes_joined_chr8.bed
$ sed -n '891,950p' maize_transposed_genotypes_joined_chr.bed > maize_transposed_genotypes_joined_chr9.bed
$ sed -n '951,956p' maize_transposed_genotypes_joined_chr.bed > maize_transposed_genotypes_joined_mutiple.bed
$ sed -n '957,983p' maize_transposed_genotypes_joined_chr.bed > maize_transposed_genotypes_joined_unknown.bed  

#10 files were built, and each one was in the same chromosome. Chromosomes of mutiple and unknown also were built.

$ cp maize_transposed_genotypes_joined_mutiple.bed / Data-Processing/
$ cp maize_transposed_genotypes_joined_unknown.bed / Data-Processing/
copy Chromosomes of mutiple and unknown to Data processing folder

$ sort -k3,3V maize_transposed_genotypes_joined_chr9.bed > maize_chr9_ordered_increased.bed                     
$ sort -k3,3V maize_transposed_genotypes_joined_chr8.bed > maize_chr8_ordered_increased.bed                     
$ sort -k3,3V maize_transposed_genotypes_joined_chr7.bed > maize_chr7_ordered_increased.bed
$ sort -k3,3V maize_transposed_genotypes_joined_chr6.bed > maize_chr6_ordered_increased.bed
$ sort -k3,3V maize_transposed_genotypes_joined_chr5.bed > maize_chr5_ordered_increased.bed
$ sort -k3,3V maize_transposed_genotypes_joined_chr4.bed > maize_chr4_ordered_increased.bed
$ sort -k3,3V maize_transposed_genotypes_joined_chr3.bed > maize_chr3_ordered_increased.bed
$ sort -k3,3V maize_transposed_genotypes_joined_chr2.bed > maize_chr2_ordered_increased.bed
$ sort -k3,3V maize_transposed_genotypes_joined_chr1.bed > maize_chr1_ordered_increased.bed
$ sort -k3,3V maize_transposed_genotypes_joined_chr10.bed > maize_chr10_ordered_increased.bed
#Sort in increased order of 10 files

$ cp maize_chr9_ordered_increased.bed / Data-Processing/
$ cp maize_chr8_ordered_increased.bed / Data-Processing/
$ cp maize_chr7_ordered_increased.bed / Data-Processing/
$ cp maize_chr6_ordered_increased.bed / Data-Processing/
$ cp maize_chr5_ordered_increased.bed / Data-Processing/
$ cp maize_chr4_ordered_increased.bed / Data-Processing/
$ cp maize_chr3_ordered_increased.bed / Data-Processing/
$ cp maize_chr2_ordered_increased.bed / Data-Processing/
$ cp maize_chr1_ordered_increased.bed / Data-Processing/
$ cp maize_chr10_ordered_increased.bed / Data-Processing/
#copy files to Data processing folder

$ sed 's/?/-/g' maize_transposed_genotypes_joined_chr8.bed | sort -k3,3nr > maize_chr8_ordered_decreased.bed    
$ sed 's/?/-/g' maize_transposed_genotypes_joined_chr9.bed | sort -k3,3nr > maize_chr9_ordered_decreased.bed
$ sed 's/?/-/g' maize_transposed_genotypes_joined_chr10.bed | sort -k3,3nr > maize_chr10_ordered_decreased.bed
$ sed 's/?/-/g' maize_transposed_genotypes_joined_chr7.bed | sort -k3,3nr > maize_chr7_ordered_decreased.bed
$ sed 's/?/-/g' maize_transposed_genotypes_joined_chr5.bed | sort -k3,3nr > maize_chr5_ordered_decreased.bed
$ sed 's/?/-/g' maize_transposed_genotypes_joined_chr4.bed | sort -k3,3nr > maize_chr4_ordered_decreased.bed
$ sed 's/?/-/g' maize_transposed_genotypes_joined_chr3.bed | sort -k3,3nr > maize_chr3_ordered_decreased.bed
$ sed 's/?/-/g' maize_transposed_genotypes_joined_chr2.bed | sort -k3,3nr > maize_chr2_ordered_decreased.bed
$ sed 's/?/-/g' maize_transposed_genotypes_joined_chr1.bed | sort -k3,3nr > maize_chr1_ordered_decreased.bed
#decreasing position values and with missing data encoded by this symbol: -
1. All files were sorted in desearsed order and all '?' were changed into '-'
2. g was used to change all '?', otherwise, only '?' before '/' would be changed

Repeat same things for Teosinte Data
### Teosinte Data

$ sed -n '1,155p' teosinte_transposed_genotypes_joined_chr.bed > teosinte_transposed_genotypes_joined_chr1.bed
$ sed -n '156,208p' teosinte_transposed_genotypes_joined_chr.bed > teosinte_transposed_genotypes_joined_chr10.bed
$ sed -n '209,335p' teosinte_transposed_genotypes_joined_chr.bed > teosinte_transposed_genotypes_joined_chr2.bed
$ sed -n '336,442p' teosinte_transposed_genotypes_joined_chr.bed > teosinte_transposed_genotypes_joined_chr3.bed
$ sed -n '443,533p' teosinte_transposed_genotypes_joined_chr.bed > teosinte_transposed_genotypes_joined_chr4.bed
$ sed -n '534,655p' teosinte_transposed_genotypes_joined_chr.bed > teosinte_transposed_genotypes_joined_chr5.bed
$ sed -n '656,731p' teosinte_transposed_genotypes_joined_chr.bed > teosinte_transposed_genotypes_joined_chr6.bed
$ sed -n '732,828p' teosinte_transposed_genotypes_joined_chr.bed > teosinte_transposed_genotypes_joined_chr7.bed
$ sed -n '829,890p' teosinte_transposed_genotypes_joined_chr.bed > teosinte_transposed_genotypes_joined_chr8.bed
$ sed -n '891,950p' teosinte_transposed_genotypes_joined_chr.bed > teosinte_transposed_genotypes_joined_chr9.bed
$ sed -n '951,956p' teosinte_transposed_genotypes_joined_chr.bed > teosinte_transposed_genotypes_joined_mutiple.bed
$ sed -n '957,983p' teosinte_transposed_genotypes_joined_chr.bed > teosinte_transposed_genotypes_joined_unknown.bed

$ sort -k3,3V teosinte_transposed_genotypes_joined_chr9.bed > teosinte_chr9_ordered_increased.bed
$ sort -k3,3V teosinte_transposed_genotypes_joined_chr8.bed > teosinte_chr8_ordered_increased.bed
$ sort -k3,3V teosinte_transposed_genotypes_joined_chr7.bed > teosinte_chr7_ordered_increased.bed
$ sort -k3,3V teosinte_transposed_genotypes_joined_chr6.bed > teosinte_chr6_ordered_increased.bed
$ sort -k3,3V teosinte_transposed_genotypes_joined_chr5.bed > teosinte_chr5_ordered_increased.bed
$ sort -k3,3V teosinte_transposed_genotypes_joined_chr4.bed > teosinte_chr4_ordered_increased.bed
$ sort -k3,3V teosinte_transposed_genotypes_joined_chr3.bed > teosinte_chr3_ordered_increased.bed
$ sort -k3,3V teosinte_transposed_genotypes_joined_chr2.bed > teosinte_chr2_ordered_increased.bed
$ sort -k3,3V teosinte_transposed_genotypes_joined_chr1.bed > teosinte_chr1_ordered_increased.bed
$ sort -k3,3V teosinte_transposed_genotypes_joined_chr10.bed > teosinte_chr10_ordered_increased.bed

$ sed 's/?/-/g' teosinte_transposed_genotypes_joined_chr8.bed | sort -k3,3nr > teosinte_chr8_ordered_decreased.bed
$ sed 's/?/-/g' teosinte_transposed_genotypes_joined_chr1.bed | sort -k3,3nr > teosinte_chr1_ordered_decreased.bed
$ sed 's/?/-/g' teosinte_transposed_genotypes_joined_chr2.bed | sort -k3,3nr > teosinte_chr2_ordered_decreased.bed
$ sed 's/?/-/g' teosinte_transposed_genotypes_joined_chr3.bed | sort -k3,3nr > teosinte_chr3_ordered_decreased.bed
$ sed 's/?/-/g' teosinte_transposed_genotypes_joined_chr4.bed | sort -k3,3nr > teosinte_chr4_ordered_decreased.bed
$ sed 's/?/-/g' teosinte_transposed_genotypes_joined_chr5.bed | sort -k3,3nr > teosinte_chr5_ordered_decreased.bed
$ sed 's/?/-/g' teosinte_transposed_genotypes_joined_chr6.bed | sort -k3,3nr > teosinte_chr6_ordered_decreased.bed
$ sed 's/?/-/g' teosinte_transposed_genotypes_joined_chr7.bed | sort -k3,3nr > teosinte_chr7_ordered_decreased.bed
$ sed 's/?/-/g' teosinte_transposed_genotypes_joined_chr9.bed | sort -k3,3nr > teosinte_chr9_ordered_decreased.bed
$ sed 's/?/-/g' teosinte_transposed_genotypes_joined_chr10.bed | sort -k3,3nr > teosinte_chr10

#then copy all desired file to Data processing folder.

