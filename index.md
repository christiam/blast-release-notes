---
layout: page
title: "NCBI BLAST Cloud Documentation"
---
# BLAST+ 2.7.1: October 23, 2017

## Improvements
* Provided an upper limit on the number of threads for BLAST+ search applications.
* Improved performance of taxonomic name lookups.
* Fixed Mac installers so they are interoperable with other NCBI applications.
* Reduced the amount of locking in BLASTDB reading library (CSeqDB).

## Bug fixes
* Fixed race condition when using gilist parameter.
* Fixed culling_limit bug with HSPs from different strands
* Fixed dustmasker bug with long region of Ns
* Fixed bl2seq problem with HTML output

# BLAST+ 2.6.0: January 09, 2017

## New features
* Handle bare accessions on blastdb_aliastool.
* Change defaults for output formats 6, 7, and 10 to incorporate version in accessions.

## Improvements
* Add support for NCBI_DONT_USE_LOCAL_CONFIG and NCBI_DONT_USE_NCBIRC environment variables.
* Better runtime performance in blastdbcmd when the entry_batch parameter is used.
* SAM output improvements.
* Changed gapped alignment starting point to minimize the chance to produce sub-optimal alignments.
* For custom matrices absent from the util/tables source file, use BLOSUM62 for reporting number of positives.
* Added long_seqids flag to blastdbcmd to use long (legacy) NCBI Seq-id format.

## Bug fixes
* Fixed issue with missing alignments in blastx.
* Fixed problem processing accession.version in makeblastdb.
* Fixed blastdbcmd problem with local IDs.
* Removed memory leak for multi-threaded runs.
* Fixed blastdbcmd crash when listing all entries and a sequence has no title.
 
# BLAST+ 2.5.0: September 12, 2016

## New features
* Composition based statistics for rpstblastn.
* Added output format for taxonomic organism report.
* Support for bare accessions in FASTA and BLAST reports.

## Improvements
* -remote option connects to NCBI via HTTPS. This adds a dependency on GNUTLS (see https://www.ncbi.nlm.nih.gov/books/NBK279690/)
* Pre-fetch sequences for formatting.

## Bug fixes
* Fixed improper functioning of output format 6 tokens ssciname, staxid, sscinames and staxids.
* tblastn core-dumps in multi-threaded mode.
* Ensure stable sorting of results in multi-threaded mode.
* Fixed incorrect percent identity in tabular format for sequences containing selenocysteine.

# BLAST+ 2.4.0: June 02, 2016

## New features
* Introduced multi-threaded traceback for blastp, blastx, tblastn and tblastx.
* Added new tabular format specifiers for taxonomic information (staxid, ssciname, scomname, sblastname, skingdom) that correspond to the first subject ID.

## Improvements
* Speed up makeblastdb runtime performance with input consisting of many ambiguities.
* Better support for 'bare' IDs in taxid_map option to makeblastdb.
* Score U (selenocysteine) as C (not X) in protein-protein and translated searches.

## Bug fixes
* Corrected E-value computation in finite-size correction.
* Removed memory leak from rpsblast.
* Made handling of ambiguities in subjects identical when using FASTA and BLAST database inputs.
* makeblastdb no longer replaces tabs in definition line by '#'.
* Corrected problem with spaces in database names on windows.
* Corrected handling of subject_loc.

# BLAST+ 2.3.0: December 21, 2015

## New features
* Added new PSIBLAST command line options to support saving PSSM and checkpoint files for each iteration and calculate checkpoint and PSSM for the last iteration.
* Added unique subject sequence query coverage to tabular output.
* Added support single file JSON and XML2 Blast output format.
* Beta release of SAM output format.
* Treat N subject sequences, entered with the -subject argument (bl2seq mode), as one search set rather than N sets.

## Improvements
* makeblastdb ignores and warns users about empty sequences in input.
* BLAST+ only accepts "obinary" windowmasker files for performance reasons.

## Bug fixes
* Best hits processing multi-threaded context.
* Fixed memory leak when invoking composition based statistics with an argument of 2.
* Return non-zero exit code when failing to write output file.
* Use relative paths in XInclude file for multi-file XML2 output format.
* Fixed memory leak in blastx.
* Fixed inconsistent XML2 output to standard output vs. file.
* Fixed psiblast incorrectly processing large input MSA.
* Fixed bug when running BLAST+ on windows with multiple threads.

# BLAST+ 2.2.31: May 18, 2015

## New features
* Added support for BLAST-XML2 specification.
* Added support for JSON Blast output format.

## Improvements
* Improved adaptive batch size algorithm to better handle small databases.
* Preface error/warning message(s) with name of the application.
* Allow multiple deflines even without GIs.
* Download more concise database information for -remote searches.

## Bug fixes
* Fixed problem with makeblastdb's -max_file_sz.
* Reenabled support for word size 5 in tblastn.
* Fixed memory initialization problems.
* Use score for sorting search results if evalue less than 1.0e-180.

# BLAST+ 2.2.30: October 6, 2014

## New features
* Added tblastn-fast, blastp-fast, and blastx-fast tasks. These tasks make use of longer words as described by Shiryev et al. in http://www.ncbi.nlm.nih.gov/pubmed/17921491.
* Added new output option (outfmt 12) with Seq-Align in JSON.

## Improvements
* Added new command line option qcov_hsp_perc that removes alignments below the specified query coverage.
* Added option line_length for the printing of alignment lengths (outfmt 0-4).
* Added larger gap penalties for PAM30 and PAM70 matrices.
* psiblast now accepts 0 for num_iterations to indicate iterating until convergence.
* rpsblast uses composition-based-statistics by default. Recover old behavior with "-comp_based_stats F -seg yes".
* Improved blastn multithreading performance for many queries with small databases.
* Changed cmdline option -sum_stats (formerly -sum_statistics) from flag to boolean.

## Bug fixes
* Fixed spurious messages when parsing FASTA input.
* Fixed makeprofiledb handling of PSSMs created from multiple sequence alignment.
* Fixed makeblastdb handling of '-' at the end of FASTA input.
* Fixed windowmasker segmentation fault when the incorrect window size is provided.
* Fixed problem with lower-case masking and large sequences.
* Fixed makeblastdb segmentation fault on duplicate seqids.
* Allow specification of scoring matrices in lower case letters.
* Fixed exit code when disk space is not available for the output file.
* Fixed problem with using seqids list from -outfmt "6 sseqid" as input with –seqidlist.
* Fixed bug with culling_limit that excludes top hit.
* Fixed bug with max_target_seqs not working with psiblast.

# BLAST+ 2.2.29: January 3, 2014

## Improvements
* Improved the criteria for segging subject sequences used in composition based statistics with protein and translated searches.
* Improved blastn batch query performance.
* Improved blastdbcmd performance when retrieving taxonomic data from the BLAST databases.
* blastdb_aliastool supports reading a list of BLASTDBs from a file.
* Source releases build optimized multi-threaded binaries by default.
* Multi-threaded traceback: provides performance improvement for nucleotide-nucleotide BLAST with large (>25k) queries.
* Made makeprofiledb error messages more user friendly.
* Ungapped BLAST no longer uses sum statistics by default. Recover old behavior with -sum_statistics flag.
* Improved multithreading by better dividing the BLAST database among threads.

## Bug fixes
* Allow update_blastdb.pl to work with databases containing more than 100 volumes.
* makeblastdb provides error message when -parse_seqids is used and invalid FASTA is provided.
* ASCII PSSM output for psiblast and deltablast displays two-digit scores in a more readable manner.
* Fixed negative percent identity in tabular output format
* Removed -num_threads option for binaries built without multi-threading.
* Fixed deltablast failures when searching multiple queries against multiple subject sequences.
* Fixed segmasker exception on example from BLAST cookbook.
* Fixed bogus warning about indexed megablast when using import search strategies.
* Fixed missing hits when running blastn with multiple queries, word size 7, large evalue, and no low complexity filtering.
* Fixed handling of gaps in ASN.1 input.
* Fixed Statistics_hsp-len value of 0 in XML output from blast_formatter.
* Fixed incorrect query coverage computation when sequence range was specified.
* Tabular output no longer ignores the -db_gencode argument.
* Fixed missing query sequence data in BLAST archive when -parse_deflines and FASTA with gnl ID was provided.
* Produce one XML document from BLAST archive.
* Removed 100 volume restriction in blastdb_aliastool -num_volumes.
* Fixed caption for 'query coverage' in tabular output format.
* Approximate gapped alignment in blastp is turned on/off for each query individually.
* Fixed query genetic code option.

# BLAST+ 2.2.28: March 19, 2013

## New features
* Composition based statistics support in rpsblast
* Support for query coverage, subject sequence title, and taxonomy data in custom tabular output format
* blastdbcmd support for batch subsequence retrieval

## Improvements
* Adaptive BATCH_SIZE
* Perform incremental XML output

## Bug fixes
* Formatting of asterix character in XML output
* Segmentation fault on out-of-memory
* Prevented extension of alignment into Ns
* Segmentation fault in DeltaBLAST when used with -remote and -out_ascii_pssm
* Replace tabs with spaces in FASTA deflines
* blastdbcmd displaying internal sequence ID for databases built without -parse_seqid
* blastdbcmd not fetching sequence data for complete sequence ID and -target_only
* blastn missing a hit for small word sizes
* Crash in blastn when it fetches sequence data from Genbank
* DeltaBLAST returning no hits when used with -remote option and searching more than one query
* Initialization problems for indexed megablast
* psiblast problem using -import_search_strategy
* blast_formatter displaying empty query for DeltaBLAST RID
* makeblastdb problem with ASN.1 input
* dustmasker errors with acclist and maskinfo_xml output formats
* blastx reporting of HSPs dependent on -max_target_seqs
* psiblast's display of number of queries in tabular output format
* blastx error when -ungapped and -comp_based_stats F are used

# BLAST+ 2.2.27: September 10, 2012

## New features
* Composition-based statistics for blastx.
* Added seedtop - a tool for searching for patterns in an input sequence or BLAST database.
* Enable remote DELTA-BLAST searches.

## Improvements
* Revamped controls for the number of alignments/descriptions so that they are specific to applicable output formats (see user manual for details).
* Reduce memory usage for BLAST searches that involve (large) multiple queries.
* Speed up start-up times for BLAST databases.
* Display of new statistical parameters have been added to the BLAST results.
* Speed up runtime performance of tabular output formatting.
* Improve the placement of gaps in MegaBLAST

## Bug fixes
* Fixed formatting bug when GI input format is provided to blastn.
* Fixed incorrect composition-statistics default for DELTA-BLAST.
* Bug fixes in blast_formatter, blastdbcmd.
* An asterix (stop-codon) in sequence was not rendered properly.
* The Smith-Waterman option in blastp would cause seg filtering on the subject sequence even if the composition-based statistics were not being used.
* The makeblastdb taxid_map option is broken.

# BLAST+ 2.2.26: January 31, 2012

## New features
* Mac executables are now Universal Binaries for 32- and 64-bit architectures; we no longer produce PPC and Intel Universal binaries. The executable archive names remain unchanged.
* Added DELTA-BLAST - a new tool for sensitive protein searches
* Added makeprofiledb - a tool for creating a database for RPS-BLAST

## Improvements
* The blast_formatter application can now format bl2seq RIDs.
* PSI-BLAST can produce archive format, blast_formatter can format that output.
* PSI-BLAST has two new options that work with multiple-sequence alignments: ignore_msa_master and msa_master_idx (see BLAST+ manual).
* mkmbindex can now create masked indices from a BLAST database and ASN.1 masking data.
* An improved finite size correction is now used for blastp/blastx/tblastn/rpsblast.
* The FSC is subtracted from the query and database sequence length for the calculation of the expect value. The new FSC results in more accurate expect values, especially for alignments with a short query or target sequence. Re-enable the old size correction by setting the environment variable OLD_FSC to a non-NULL value.

* The blastdbcmd -range parameter now accepts a blank value for the second parameter to signify the end of a sequence (e.g., -range "100-")
* There was a performance improvement for long database sequences in results with many matches.

## Bug fixes
* There was a blastn problem if subject_loc and lcase_masking were used together.
* There was a problem with multi-threaded blastx if the query included a long (10,000+) sequence of N's.
* The percent identity calculation was wrong if the best-hit algorithm was used.
* There was a problem with the multiple BLAST database statistics report in XML format.
* Makeblastdb failed to return an error when input was not available.
* The formatting option -outfmt "7 nident" always printed zero.
* The search strategy was not properly saving the -db_soft_mask option.
* An error message was emitted if there was a "<" in the query title.
* A problem reading lower-case masking from the query could cause a search to fail.

# BLAST+ 2.2.26: March 15, 2011

## New features
* Enhanced documentation, includes simplified setup instructions, available at
http://www.ncbi.nlm.nih.gov/books/NBK1762

## Improvements
* Added support for hard-masking of BLAST databases.
* Improve performance of makeblastdb for FASTA input with large numbers of sequences, improve error checking.
* Allow Best Hit options and XML formatting for Blast2Sequences mode
* Allow multiple query sequences for psiblast.
* Allow specification of any multiple sequence alignment sequence as the master with the -in_msa psiblast argument.
* Add an optional -input_type argument to makeblastdb.
* Added support for query and subject length to tabular output.
* Performance of -seqidlist argument improved.
* The minimum of the number of descriptions and alignments is now used for tabular and
* XML output (consistent with the behavior of the older blastall applications).

## Bug fixes
* Makeblastdb and blastdbcmd problems with parsing, storing, and retrieving sequence identifiers.
* Missing subject identifiers in tabular output.
* Blast_formatter ignoring -num_alignments and -num_descriptions
* Blast archive format could be saved incorrectly with multiple queries.
* Blast_formatter established an unneeded network connection.
* Blast_formatter did not save masking information correctly.
* Rpstblastn might crash if searching many sequences.
* Indexed megablast would not run in multi-threaded mode.
* Query title in the PSSM saved by psiblast was not being stored.
* Possible failure to run in multi-threaded mode with multiple queries or large database sequences.
* Tblastn runs with database masking might miss matches.

# BLAST+ 2.2.24 bug fix release: October 30, 2010

## Bug fixes
* Improved makeblastdb performance and taxid_map option
* Fixed segmentation faults on blastn and megablast
* Fixed truncated output for sequence input with extra spaces in the defline
* Fixed problem with MacOSX binaries on MacOSX 10.5

# BLAST+ 2.2.24: August 2, 2010
* Added support for BLAST Archive format (see BLAST+ user manual)
* Added the blast_formatter application (see BLAST+ user manual)
* Added support for translated subject soft masking in the BLAST databases
* Added support for the BLAST Trace-back operations (btop) output format
* Added command line options to blastdbcmd for listing available BLAST databases
* Improved performance of formatting of remote BLAST searches
* Use a consistent exit code for out of memory conditions
* Fixed bug in indexed megablast with multiple space-separated BLAST databases
* Fixed bugs in legacy_blast.pl, blastdbcmd, rpsblast, and makeblastdb
* Fixed Windows installer for 64-bit installations

# BLAST+ 2.2.23: Feb 03, 2010
* Bug fix for tabular output formatting involving BLAST databases that do not have parseable deflines.
* Fixed problem displaying accessions in XML output format.
* Prevent collisions between queries and subject sequences with local identifiers.
* Fixed megablast performance regression when used with query masking.
* Fixed seg filtering failure for blastx and genomic sequences.
* Implemented saving search strategies in bl2seq mode.
* Fixed bug in tabular output format with qseq, sseq, pident and ppos keywords.
* Fixed bug with blastp-short task.
* Fixed blastdbcmd retrieval of taxids for BLAST databases without GIs.
* Added makeblastdb support for adding masking information to existing BLAST databases.

# BLAST+ 2.2.22 Internal bug fix release: November 02, 2009
* Fix issue dealing with opening BLAST databases which contain references to a
* BLAST database specified with a relative path.

* Prevent collisions between queries and subject sequences with local identifiers

# BLAST+ 2.2.22: Sep 27, 2009
* Added entrez_query command line option for restricting BLAST databases.
* Added support for psi-tblastn to the tblastn command line application via the -in_pssm option.
* Improved documentation for subject masking feature in user manual.
* User interface improvements to windowmasker.
* Made the specification of BLAST databases to resolve GIs/accessions configurable.
* update_blastdb.pl downloads and checks BLAST database MD5 checksum files.
* Allowing long words with blastp.
* Added support for overriding megablast index when importing search strategy files.
* Added support for best-hit algorithm parameters in strategy files.
* Bug fixes in blastx and tblastn with genomic sequences, subject masking,
blastdbcheck, and the SEG filtering algorithm.

# BLAST+ 2.2.21: May 27, 2009

* Added support for Best-Hit algorithm.
* Added support for -in_msa psiblast option.
* Performance improvements and bug fixes to subject soft masking feature (note: the file format for the files containing the masking information has changed in a non-backwards compatible way).
* Changed command line option to specify single soft masking algorithm to mask
* BLAST databases from -mask_subjects to -db_soft_mask.
* Masked FASTA and subject masks can be obtained via blastdbcmd.
* Improved error messages when makeblastdb processes masking information.
* Bug fixes in tabular output for translated searches.
* Bug fixes to makeblastdb.
* Bug fixes to search strategies and megablast.
* Bug fixes to XML output.
* Bug fixes and performance improvements to multi-threaded execution.
* Bug fixes to lower case masking in blastx.
* Bug fixes to ungapped searches.
* Added support for smaller lookup tables for small queries.
* Added support for partial sequence fetching during traceback.
* Fixed the 2-hit algorithm so that no overlap between two hits is allowed.
* Implemented a new method to compute effective observations and new entropy-based method to compute column-specific pseudocounts in PSI-BLAST.
* Remote BLAST database data loader is used as a fallback if local BLAST databases cannot be found.
* Bug fixes, improved error messages, and support for ASN.1 input in makeblastdb.
* Bug fixes and performance improvements to subject masking feature.
* Added the update_blastdb.pl script
* Updated BLAST+ user manual with documentation about configuring BLAST, automatic resolution of sequence identifiers, and a description of how the BLAST databases are searched.

# BLAST+ 2.2.19: November 03, 2008
* Made sequence ID/title display uniform in sequence filtering applications.
* Fixed incorrect display of filtering options in XML output.
* Fixed handling of empty sequences in BLAST input.
* Fixed negative strand handling for tblastn/tblastx.

# BLAST+ 2.2.18: October 14, 2008
* Added update_blastdb.pl script to distribution of BLAST+ command line applications.
* Changed a few PSI-BLAST constants for pseudo-counts.
* Bug fix in blastdbcmd to distinguish non-redundant sequence titles.
* Bug fix to display BLAST database information remotely from outside NCBI for XML output.

# BLAST+ 2.2.17 internal release: September 24, 2008
* Fix to prevent initial seed extension from going beyond context boundary.
* Improvements to reduce memory usage when query splitting is applied.
* Print the accession and version for blastdbcmd's %a output format.
gilists/negative gilists are not saved in search strategies or supported in remote blast searches.
legacy_blast.pl fixed for MacOSX, as well as extended support for megablast formatting options (-D, -f).
Enhancements to Mac installer to add installation path to user's PATH.
ASN.1 output is now of type Seq-annot.
* -lcase_masking option now applies to subject sequences as well as queries.
* Bug fix for creation of masked databases with non-redundant sequences that use a BLAST database as its data source.
* Bug fix for merging masking locations.

# BLAST+ 2.2.16 internal release: August 21, 2008
* First internal release
