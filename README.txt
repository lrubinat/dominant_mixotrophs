----------------------
SAGs' GLOBAL ABUNDANCE
----------------------

3) Print a table with two columns: swarm ID + swarm taxogroup.

	$awk -F "\t" '{print $3, "\t", $(NF-2)}' data_info_table.txt | sort -V > swarms_taxogroups.txt

		Input: "data_info_table.txt" (contains swarms data excluding occurrence data in TAA, TV and BM stations)
				(R command: >write.table(data[,.SD,.SDcols=colnames(data)[!grepl("TV|TA|BV",colnames(data))]],"data_info_table.txt",sep="\t",row.names=T))
		Output: swarms_taxogroups.txt

	$awk -F "\t" '{print $(NF-2)}' data_info_table.txt | sort -V | uniq -c > swarms_taxogroups_uniq.txt
	#taxogroups occurrence







	$grep "Chlorophyta" data_info_table.txt | awk -F "\t" '{print $(NF-2)}' | sort -V | uniq -c > swarms_taxogroups_chlorophyta_uniq.txt
	#taxogroups occurrence in Chlorophyta






