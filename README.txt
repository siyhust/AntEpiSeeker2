Modified AntEpiSeeker2.0
-----------------

Modify it for handling multi class input. You can use it on data out of 0-1.

Only test on Ubuntu 14.04.

For ubuntu/debian users, you can only install this program with command below:

sudo apt-get install libgsl0ldbl 
sudo apt-get install libgsl0-dev
g++ AntEpiSeeker2.cpp -o AntEpiSeeker2 -lgsl -lgslcblas

It will be better if you edit the parameter.txt with vi/vim, it was prepared from Windows, edit it with other editor may destory the format of text in it.


-----------------
1.Installation and execution
For linux system version, users may simply unzip the package into one folder and run the program by typing "./AntEpiSeeker2"(gcc version 3.4.6 or above is needed). 
For windows system version, unzip all files into one folder. The GNU Scientific Library (GSL) files "libgsl.dll", "libslcblas.dll" and "WinGsl.dll" in this package should be put in the same folder with AntEpiSeeker2 as well as your system folder (e.g., "c:\\windows\\system32"). Start MS-DOS by Start>Run>cmd and change your working directory to AntEpiSeeker2. Run the program by typing "AntEpiSeeker2.exe". 
For Mac OS X lion version, users may start xterm, unzip the package into one folder and run the program by typing "./AntEpiSeeker2" .

2.Compile from source
For linux systems, make sure the GNU Scientific Library (GSL) is installed properly. GSL can be downloaded from http://www.gnu.org/s/gsl/. After the package is uncompressed, GSL can be installed using the following commands:
1) "./configure"
2) "make"
3) "make install"
If GSL is installed by defaut, type "g++ AntEpiSeeker2.cpp -o AntEpiSeeker2 -lgsl -lgslcblas" to compile. If GSL is installed in a specific path, type "g++ AntEpiSeeker2.cpp -o AntEpiSeeker2 -P /home/username/gsl/lib/libgsl.a /home/username/gsl/lib/libgslcblas.a" to complile. Note that the paths for the two library files "libgsl.a" and"libgslcblas.a" in the above command should be changed to where GSL is installed and the include path in the file "AntEpiSeeker2.cpp" should be directed to "/home/username/gsl/include/gsl/gsl_cdf.h".

For windows systems, make sure that GNU Scientific Library (GSL) works properly before compiling. If users use Visual C++ 6.0 to compile, here are some tips: 
1) Download WinGsl-Lib-1.4.02.zip from http://www6.in.tum.de/~kiss/WinGsl.htm. 
2) Unzip WinGsl-Lib-1.4.02.zip. Copy the  files in \WinGsl-Lib-1.4.02\WinGsl\bin to \Microsoft Visual Studio\VC98\Bin and to C:\WINDOWS\system32, the directory \WinGsl-Lib-1.4.02\WinGsl\Gsl to \Microsoft Visual Studio\VC98\Include, the files in \WinGsl-Lib-1.4.02\WinGsl\Lib to \Microsoft Visual Studio\VC98\Lib, the file \WinGsl-Lib-1.4.02\WinGsl\WinGslDLL.inl to  \Microsoft Visual Studio\VC98\Include. 
3) Open the file antepiseeker.cpp using VC++ 6.0, click project>settings>link and append WinGsl.lib to object/library modules (Note that modules should be space delimited). 

For Mac OS X version, Xcode and GSL need to be installed on the user's computer. Xcode is available at http://developer.apple.com/xcode/. GSL can be downloaded from http://www.gnu.org/s/gsl/. Users may start Xterm. After the package is uncompressed, gsl can be installed through using the following commands:
1) "./configure"
2) "make"
3) "sudo make install" 
If GSL is installed by defaut, type "g++ AntEpiSeeker2.cpp -o AntEpiSeeker2 -lgsl -lgslcblas" to compile. 

2.Input Format
Users should create a tab-delimited file which contains the case-control genotype data as an input for the program. The first row of this input file contains the sample status (0 or 1). The following rows are the genotype data which should be coded by 0, 1 and 2 with each row corresponding to one SNP. For example,

class 1 1 1 0 0
rs1 0 1 1 2 2
rs2 1 2 0 1 2
rs3 2 2 1 2 1
rs4 2 2 1 1 2

Users should also make a tab-delimited file which contains information of pathway-SNP associations. Each pathway should be placed in one row, with the first column specifying the pathway ID and the following columns containing its associated SNPs. For example,

pw1 rs1 rs2 rs3
pw2 rs4 rs5
pw3 rs6 rs7 rs8 rs9

"testing_genotypes.txt" and "testing_pwy2snp.txt" are a complete testing dataset.

3.Parameter file
The parameters for running AntEpiSeeker are specified in the "parameters.txt" file. These parameters include iAntCount, iItCountHsize, alpha, iTopModel, iTopLoci, rou, phe, largesetsize, smallsetsize, iEpiModel, pvalue, pwprop, weighted PWSNPFL, INPFILE, OUTFILE and PWYFILE.

The parameter "iEpiModel" specifies the number of SNPs in an epistatic interaction. The parameters "largesetsize", "smallsetsize" must be greater than "iEpiModel". For two-locus interaction model, we suggest largesetsize=6, smallsetsize=3, iEpiMode=2; For three-locus interaction model, we suggest largesetsize=6, smallsetsize=4, iEpiModel=3.

The parameter "iItCountHsize" should be chosen according to the number of SNPs genotyped in the data. Typically, we suggest iItCountHsize=200 for <=100000 SNPs and iItCountHsize=1000 for >100000 SNPs.

4.Output
Four output files will be generated by AntEpiSeeker2. "AntEpiSeeker2.log" under the AntEpiSeeker2 directory records the intermediate results including the detected top ranked SNP sets and the loci with top pheromone levels. "results_maximized.txt" records all detected epistatic interactions meeting the pre-defined P-value threshold. The OUTFILE and PWYFILE specified by the user in the parameter file report the detected epistatic interactions with minimized false positives and sorted pathways according to pheromones respectively.

5.Support
Questions and comments should be directed to Yupeng Wang (wyp1125@gmail.com).

