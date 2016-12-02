################################
#### SAGs' GLOBAL ABUNDANCE ####
################################

3) Print a table with two columns: swarm ID + swarm taxogroup.

	$ awk -F "\t" '{print $3, "\t", $(NF-2)}' data_info_table.txt | sort -V > swarms_taxogroups.txt

		--> Input: "data_info_table.txt" (contains swarms data excluding occurrence data in TAA, TV and BM stations)
				(R command: >write.table(data[,.SD,.SDcols=colnames(data)[!grepl("TV|TA|BV",colnames(data))]],"data_info_table.txt",sep="\t",row.names=T))
		--> Output: swarms_taxogroups.txt

	#taxogroups occurrence
	$ awk -F "\t" '{print $(NF-2)}' data_info_table.txt | sort -V | uniq -c > swarms_taxogroups_uniq.txt



-------------------------------

4)	Table of swarms classified as red or green algae: swarm ID + taxogroup.

	$ grep "Chlorophyta" data_info_table.txt | awk -F "\t" '{print $3, "\t", $(NF-2)}' > swarms_taxogroups_green-red.txt
	$ grep "Streptophyta" data_info_table.txt | awk -F "\t" '{print $3, "\t", $(NF-2)}' >> swarms_taxogroups_green-red.txt
	$ grep "Rhodophyta" data_info_table.txt | awk -F "\t" '{print $3, "\t", $(NF-2)}' >> swarms_taxogroups_green-red.txt
		
		--> Input: "data_info_table.txt" #474304 rows
		--> Output: "swarms_taxogroups_green-red.txt" #9250 rows
	

	#taxogroups occurrence in Chlorophyta
	$ grep "Chlorophyta" data_info_table.txt | awk -F "\t" '{print $(NF-2)}' | sort -V | uniq -c > swarms_taxogroups_chlorophyta_uniq.txt



-------------------------------

5) Identification of red and green algae.

	$python3 identify_red_green_algae.py

		--> Input: "data_info_table.txt" (for identifying Chlorophyta classified as "undetermined archaeplastida" and "a blaster").
		--> Output: "identify_red_green_allgae_all_swarms_output.txt". Composition:

			   - Taxogroups:
			   	$ grep -v "other$" identify_red_green_algae_all_swarms_output.txt | awk -F "\t" '{print $2}' | sort -V | uniq -c | less

			   [7901 GREEN ALGAE (Chlorophyta & Streptophyta)]
				   3041  "Chlorophyceae"
				   1113  "Mamiellophyceae"
				    391  "Prasinophyceae Clade 7"
				    321  "Pyramimonadales"
				    602  "Trebouxiophyceae"
				    463  "Ulvophyceae"
				    448  "other core chlorophytes"
				    155  "other prasinophytes"
				     16  "? a blaster"
				   1296  "? undetermined archaeplastida *"
				    166  "? undetermined green algae"
   				    492  "Streptophyta"

		   	   	[764 RED ALGAE]
		   	  	  746  "Rhodophyta"


		   	  - No. of red and green algae:
		   	   	$ grep -v "other" identify_red_green_algae_all_swarms_output.txt | awk -F "\t" '{print $3}' | sort -V | uniq -c | less

				   7901 green
				   746 red



###############
#### UTILS ####
###############

#all rows have same no. of rows? 
awk -F "\t" '{print NF}' data_info_table.txt | sort -V | uniq -c | less

#print the rows that have 19 columns
awk -F "\t" 'NF==19{print}{}' data_info_table.txt
