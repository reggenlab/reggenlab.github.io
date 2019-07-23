"# FITS Python version" 

One needs to have python 3.0+ installed in their machine. You have to download python code in your local machine/server. For execution you have to pass filename of read-counts csv as a input file. Read-count csv file does not contain header and genomic location i.e. it consist of only data on which imputation is going to perform. Row represents sites and column reprent samples/cells in csv file.

```bash
python3 main_FITS1.py -i <csv file name>
e.g.
python3 main_FITS1.py -i sce5_raw.csv
```
'sce5_raw.csv' consist of epignome data corresponding to five cell type.

Other optional input parameter you can pass in phase1 

```bash
python3 main_FITS1.py -i <csv file name> -o <name to save imputed file> -l <Depth upto which tree will grow>
```
Usage help can be availed by following command

```bash
python3 main_FITS1.py -h
```

By default -l (maxLevel) set to 4 and -o (output) set to 'FITS_OUTPUT'.
You can run FITSPhase1 parallely in background using : 

```bash
nohup python3 main_FITS1.py -i <csv file name> > <name>.txt &
```
You can create n number of imputed matrix generated through phase1. Each run will generate imputed matrix.

Once Phase1 is over then run Phase2 to generate final imputed matrix based on matrix received as output from Phase1.

```bash
python3 main_FITS2.py -i <csv file name>
e.g.
python3 main_FITS2.py -i sce5_raw.csv
```
You have to pass same input file as you passed in Phase1. Don't worry Phase2 takes only one minute to generate final output :)

Other optional input parameter you can pass in phase2 

```python3
main_FITS2.py -i <csv file name> -o <name to save imputed file same as Phase1> -t <topk correlated matrix feature/sample value use for final imputation> -c <1/0 takes values either 1 or 0> 
```
Default value for feature is zero. At value 0 phase2 will compute correlation among samples/cell (preffered) while value 1 will compute correlation features/sites wise.

Usage help can be availed by following command

```bash
python3 main_FITS2.py -h
```
