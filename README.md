# ENGG3110 Assignment 4 Submission

**Student:** Timothy Khan (1239165)  
**Instructor:** Andrew Hamilton-Wright  
**Date:** March 31, 2025

## Assignment Completion
- [x] Name is in a comment at the beginning of the program  
- [x] Completed thread-based implementation  
- [x] Included a functional makefile - with debug statements  
- [x] Compiles and runs on linux.socs.uoguelph.ca  
- [x] Submission contains a brief discussion describing program design  
- [x] Implemented and tested the following missing functions in `fat12fs.c`:  
	- `fat12fsDumpFat()`  
	- `fat12fsDumpRootdir()`  
	- `fat12fsSearchRootdir()`  
	- `fat12fsLoadDataBlock()`  
	- `fat12fsVerifyEOF()`  
	- `fat12fsReadData()`  

### Implemented Functions

1. **`fat12fsDumpFat()`**  
   This function prints the FAT table in hexadecimal format with 16 entries per row. Although the comments in the code suggested hexadecimal output, the implementation was aligned with the provided sample output, which uses decimal row indices. The function ensures proper formatting and handles cases where the FAT size is not a multiple of 16.

2. **`fat12fsDumpRootdir()`**  
   This function iterates through the root directory and prints non-empty entries. It categorizes entries as `VOL` (volume label), `DEL` (deleted), or `FILE` (regular file). The output includes the file name, extension, size, and starting block, formatted to match the sample output.

3. **`fat12fsSearchRootdir()`**  
	This function searches the root directory for a file or directory entry matching a given name. It iterates through the directory entries, comparing each name with the target. If a match is found, the function returns the entry's details, such as its starting block and size. If no match is found, an error is reported. The implementation of this function used reference code mentioned in the comments of `fat12fs.c`, specifically for handling the file name processing.  

4. **`fat12fsLoadDataBlock()`**  
   This function reads a logical data block into a buffer. It calculates the physical block number based on the FAT-12 filesystem structure and ensures the block index is valid. Errors are reported if the block cannot be read.

5. **`fat12fsVerifyEOF()`**  
   This function verifies the integrity of a file by traversing its FAT chain. It ensures the last block is marked as EOF and that the file size matches the number of blocks traversed. If any inconsistency is found, the function returns an error.

6. **`fat12fsReadData()`**  
   This function reads data from a file starting at a specified position and for a given number of bytes. It uses the FAT chain to locate the required blocks and handles cases where the requested range exceeds the file size. The function outputs the read data and reports errors if encountered.

### Expected Output

The program's output matches the provided sample output in `smallfiles.sampleoutput`. Key highlights include:

- **FAT Table Dump (`f` command):** The FAT table is printed with decimal row indices and hexadecimal values for entries.
- **Root Directory Dump (`r` command):** The root directory entries are categorized and displayed with their attributes.
- **File Data Read (`d` command):** Data from files like `letters.txt` and `small.txt` is read and displayed, including special characters and padding.

### Notes

- The comments in the code occasionally differed on whether to use hexadecimal or decimal values for certain outputs. To ensure consistency, the implementation was adjusted to match the sample output provided in `smallfiles.sampleoutput`.
### Additional Testing Notes

- The additional information from the tested files using the `d` command aligns with the expected outputs based on the provided codebase, even though it differs slightly from the `smallfiles.sampleoutput`. 


	**My Output:**
	```
	d letters.txt 2000 58
	Read :: Data Bytes - file 'letters.txt', 58 bytes, start 2000
	Buffer using return status
	File 'letters.txt' 58 bytes beginning at 2000
	aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000QQQQQQQQQQQQQQQQ
	Buffer using request size
	File 'letters.txt' 58 bytes beginning at 2000
	aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000QQQQQQQQQQQQQQQQ
	```

	**Sample Output (`smallfiles.sampleoutput`):**
	```
	d letters.txt 2000 58
	Read :: Data Bytes - file 'letters.txt', 58 bytes, start 2000
	File 'letters.txt' 58 bytes beginning at 2000
	aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa\000\000\000\000\000\000\000\000\000\000\000\000\000\
	000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\000\
	000\000QQQQQQQQQQQQQQQQ
	```

	The discrepancy in the output arises from the additional "Buffer using return status" and "Buffer using request size" sections in **My Output**, which are not present in the **Sample Output**. These sections appear to provide extra debugging information that was not part of the expected output format. To resolve this, the program would simply be adjusted to suppress these additional sections.

- The program was thoroughly tested to ensure correctness and alignment with the expected behavior, with adjustments made to match the sample output wherever feasible.

