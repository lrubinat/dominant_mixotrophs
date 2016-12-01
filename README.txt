----------------------
SAGs' GLOBAL ABUNDANCE
----------------------

3) Print a table with two columns: swarm ID + swarm taxogroup.

	$awk -F "\t" '{print $3, "\t", $(NF-2)}' data_info_table.txt | sort -V > swarms_taxogroups.txt

		--> Input: "data_info_table.txt" (contains swarms data excluding occurrence data in TAA, TV and BM stations)
				(R command: >write.table(data[,.SD,.SDcols=colnames(data)[!grepl("TV|TA|BV",colnames(data))]],"data_info_table.txt",sep="\t",row.names=T))
		--> Output: swarms_taxogroups.txt

	#taxogroups occurrence
	$awk -F "\t" '{print $(NF-2)}' data_info_table.txt | sort -V | uniq -c > swarms_taxogroups_uniq.txt



----------------------

4)	Table of swarms classified as red or green algae: swarm ID + taxogroup.

	$grep "Chlorophyta" data_info_table.txt | awk -F "\t" '{print $3, "\t", $(NF-2)}' > swarms_taxogroups_green-red.txt
	$grep "Streptophyta" data_info_table.txt | awk -F "\t" '{print $3, "\t", $(NF-2)}' >> swarms_taxogroups_green-red.txt
	$grep "Rhodophyta" data_info_table.txt | awk -F "\t" '{print $3, "\t", $(NF-2)}' >> swarms_taxogroups_green-red.txt
		
		--> Input: "data_info_table.txt" #474304 rows
		--> Output: "swarms_taxogroups_green-red.txt" #9250 rows
	

	#taxogroups occurrence in Chlorophyta
	$grep "Chlorophyta" data_info_table.txt | awk -F "\t" '{print $(NF-2)}' | sort -V | uniq -c > swarms_taxogroups_chlorophyta_uniq.txt



-----------------------

5) Identification of red and green algae.

	$python3 identify_red_green_algae.py

		--> input



###############
#### UTILS ####
###############

#all rows have same no. of rows? 
awk -F "\t" '{print NF}' data_info_table.txt | sort -V | uniq -c | less

#print the rows that have 19 columns
awk -F "\t" 'NF==19{print}{}' data_info_table.txt
