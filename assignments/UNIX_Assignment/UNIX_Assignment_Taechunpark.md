# Unix Assignment

* Tae-Chun Park

## Data Inspection
### Attributes of fang_el_al_genotypes

1-1. Check the file how it looks like
```
cat fang_el_al_genotypes.txt
```
```
cat snp_position.txt
```
* The files look so big.

1-2. Using head command to see the first several rows
```
head -n 3 fang_el_al_genotypes.txt
```
```
head -n 3 snp_position.txt
```
* fang_el_al_genotypes.txt looks it has genotypic information in it.
* snp_position.txt file has snp information of each SNP ID

1-3. Using wc command to cound words and lines
```
wc fang_el_al_genotypes.txt snp_position.txt
```
* fang_el_al_genotypes.txt file has 2,783 lines, 2,744,038 words, and 11,051,939 bytes
* snp_position.txt file has 984 lines, 13,198 words, and 11,134,702 bytes
* Total 3,767 lines, 2,757,236 words, and 11,134,702 bytes


### Data Processing
2-1. As the instruction of assignment, the file is needed to transpose to join
```
awk -f transpose.awk fang_et_al_genotypes.txt > transposed_genotypes.txt
```

2-2. Before joining the files, sorting the data files
```
sort -k1,1 transposed_genotypes.txt > sorted_transposed_fang.txt
```
```
sort -k1,1 snp_position.txt > sorted_snp_position.txt
```

2-3. Join
```
join -1 1 -2 1 sorted_transposed_fang.txt sorted_snp_position.txt > joined_file.txt
```

2-4. Extract data from the joining file.
The idea is that Using grep to search SNP_ID for maize and teosinte, respectively, and grep for searching chromosome01 with increasing order values and with missing data encoded by "?" symbol
```
grep -E "(SNP_ID|ZMMILZMMLR|ZMMMR)" joined_file.txt | grep -E "1" | sort -k3,3 | sed 's/\?\/\?/?/g' joined_file.txt > maize_genotypes_chr01_Q.txt
```
```
grep -E "(SNP_ID|ZMPBA|ZMPIL|ZMPJA)" joined_file.txt | grep -E "1" | sort -k3,3 | sed 's/\?\/\?/?/g' joined_file.txt > teosinte_genotypes_chr01_Q.txt
```
* The file successively created, and then change the code to extact other chromosome such as grep -E "2", grep -E "3", and so on.


2-5. Do the same way as 2-4, but need some changes for decreasing SNP order and "-" symbol
```
grep -E "(SNP_ID|ZMMILZMMLR|ZMMMR)" joined_file.txt | grep -E "1" | sort -k3,3 -r | sed 's/-?/-/g' | sed 's/?/-/g' joined_file.txt > maize_genotypes_chr01_D.txt
```
```
grep -E "(SNP_ID|ZMPBA|ZMPIL|ZMPJA)" joined_file.txt | grep -E "1" | sort -k3,3 -r | sed 's/-?/-/g' | sed 's/?/-/g' joined_file.txt > teosinte_genotypes_chr01_D.txt
``` 

2-6. It is difficult to do change chromosome numbers manually.
```
for i in {1..10}; do awk grep -E "(SNP_ID|ZMMILZMMLR|ZMMMR)" joined_file.txt | grep -E "$i" | sort -k3,3 -r | sed 's/-?/-/g' | sed 's/?/-/g' > maize_genotypes_chr0${i}_D.txt; done
```
```
for i in {1..10}; do awk grep -E "(SNP_ID|ZMPBA|ZMPIL|ZMPJA)" joined_file.txt | grep -E "$i" | sort -k3,3 -r | sed 's/-?/-/g' | sed 's/?/-/g' > maize_genotypes_chr0${i}_D.txt; done
```

2-7. 1 file with all SNPs with unknown positions in the genome for maize and teosinte
```
grep -E "(SNP_ID|ZMMILZMMLR|ZMMMR)" joined_file.txt | grep "unknown" joined_file.txt > maize_unknown_snps.txt
```
```
grep -E "(SNP_ID|ZMPBA|ZMPIL|ZMPJA)" joined_file.txt | grep "unknown" joined_file.txt > teosinte_unknown_snps.txt
```

2-8. 1 file with all SNPs with multiple positions in the genome for maize and teosinte
```
grep -E "(SNP_ID|ZMMILZMMLR|ZMMMR)" joined_file.txt | grep "unknown" joined_file.txt > maize_multiple_snps.txt
```
```
grep -E "(SNP_ID|ZMPBA|ZMPIL|ZMPJA)" joined_file.txt | grep "unknown" joined_file.txt > teosinte_multiple_snps.txt
```

2-9 Check the files and move to the new directory ("results").


