# Unix Assignment
## Data Inspection
### Attributes of fang_el_al_genotypes

1-1. Check the file how it looks like
```
cat fang_el_al_genotypes.txt
cat snp_position.txt
```
* The files look so big.

1-2. Using head command to see the first several rows
```
head -n 3 fang_el_al_genotypes.txt
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
sort -k1,1 snp_position.txt > sorted_snp_position.txt

2-3. Join
```
join -1 1 -2 1 sorted_transposed_fang.txt sorted_snp_position.txt > joined_file.txt
```

2-4. Extract maize and teosinte data from the joining file, respectively. After that, using grep to find chromosome1 data with increasing order values and with missing data encoded by "?" symbol
```
grep -E "(SNP_ID|ZMMILZMMLR|ZMMMR)" joined_file.txt | grep -E "1" | sort -k3,3 | sed 's/\?\/\?/?/g' joined_file.txt > maize_genotypes_chr01_Q.txt
```
* the file successively created and change the code to extact other chromosome such as grep -E "2", grep -E "3", and so on.

