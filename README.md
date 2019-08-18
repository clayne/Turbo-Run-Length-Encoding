TurboRLE: Turbo Run Length Encoding [![Build Status](https://travis-ci.org/powturbo/TurboRLE.svg?branch=master)](https://travis-ci.org/powturbo/TurboRLE)
===================================

##### Efficient and fastest **Run Length Encoding** library
  - :new: The fastest now up to 50% more faster incl. SSE/AVX2
  - 100% C (C++ compatible headers), without inline assembly
  - Most efficient compression 
  - No other RLE compress or decompress faster with better compression
  - :sparkles: faster compression and 2x faster decompression with :+1: SIMD
  - :+1: **Java** Critical Natives Interface. Access TurboRLE **incl. SIMD!** from Java
  - Compress better and up to 12 times faster and decompress up to 6 times faster than other fast RLEs
  - Can be faster than memcpy!
  - :+1: **ZERO!** byte overhead

  - No modification of the raw data, preserving compressibility for further postprocessing (ex. entropy coding)
  - Order preserving 

##### TurboRLE
  - **TRLE**: TurboRLE - Efficient and fast Run Length Encoding
  - **SRLE**: TurboRLE Escape - Fast Run Length Encoding with automatic escape determination 

## Benchmark:
- with [TurboBench](https://github.com/powturbo/TurboBench)
- Single thread
- Realistic and practical benchmark with large files and different distributions

------------------------------------------------------------------------
#### CPU: Skylake i7-6700 3.4GHz, gcc 8.3 
- BMP File: [girl.bmp in RLE64Samples](http://sourceforge.net/projects/nikkhokkho/files/RLE64/3.00/)

(bold = pareto)  MB=1.000.000

|C Size|ratio%|C MB/s|D MB/s|Name / 2019-08|
|--------:|-----:|--------:|--------:|----------------|
|2623680|  0.6|**2074.35**|**11112.89**|**trle**|
|4744806|  1.2|**10765.75**|**12342.86**|**srle 8**|
|4744807|  1.2|2067.30|**12374.24**|**srle 0** (auto escape)|
|8431844|  2.1|7368.11|**12692.71**|**srle 16**|
|13722311|  3.4|**11089.70**|**13188.36**|**srle 32**|
|19839711|  4.9|**16268.73**|**13732.71**|**srle 64**|
|403920054|100.0|13977.92|**14000.70**|**memcpy**|

- Checkers program "End Game Table Base": [1034.db](http://encode.su/threads/2077-EGTB-compression?p=41392&viewfull=1#post41392)

|C Size|ratio%|C MB/s|D MB/s|Name / 2019-08|
|--------:|-----:|--------:|--------:|----------------|
|73108990| 17.4|**754.08**|**2983.03**|**trle**|
|92369164| 22.0|**1018.80**|**5860.34**|**srle 8**|
|92369165| 22.0|739.48|5860.10|srle 0|
|113561548| 27.1|**2027.71**|**7113.72**|**srle 16**|
|136918311| 32.7|**3587.63**|**9026.28**|**srle 32**|
|165547365| 39.5|**5972.39**|**10120.11**|**srle 64**|
|419225625|100.0|**13937.49**|**14017.17**|**memcpy**|

- Text File: [enwik9bwt](http://mattmahoney.net/dc/textdata.html) enwik9 bwt generated w. [libdivsufsort](https://code.google.com/p/libdivsufsort/)

|C Size|ratio%|C MB/s|D MB/s|Name / 2019-08|
|--------:|-----:|--------:|--------:|----------------|
|375094084| 37.5|**470.28**|**1742.31**|**trle**|enwik9bwt|
|419263924| 41.9|**538.40**|**4256.44**|**srle 8**|enwik9bwt|
|419263925| 41.9|450.03|4254.72|srle 0|enwik9bwt|
|487430623| 48.7|**1347.36**|**6286.70**|**srle 16**|enwik9bwt|
|549202860| 54.9|**2780.33**|**8238.25**|**srle 32**|enwik9bwt|
|605759578| 60.6|**5356.30**|**9471.04**|**srle 64**|enwik9bwt|
|1000000008|100.0|**13931.07**|**13925.83**|**memcpy**|enwik9bwt|

------------------------------------------------------------------------
#### CPU: Sandy bridge i7-2600k at 4.2GHz, gcc 6.2

###### External functions benchmarked
  - **MRLE**: Mespotine RLE [MRLE](http://encode.su/threads/2121-No-more-encoding-overhead-in-Run-Length-Encoding-Read-about-Mespotine-RLE-here-)
  - **RLE64**: Run Length Encoding - [RLE64](http://sourceforge.net/projects/nikkhokkho/files/RLE64/)
<p>


|C Size|ratio%|C MB/s|D MB/s|Name / 2018-06|
|--------:|-----:|--------:|--------:|----------------|
|3289669|  0.8|**2122**|**10499**|**trle**|
|4482388|  1.1|346|3467|mrle|
|4732081|  1.2|**7971**|10156|**srle 8**|
|4732082|  1.2|2110|10494|srle 0 |
|8431853|  2.1|4848|10272|srle 16|
|8832647|  2.2|1274|2921|rle64 8|
|9265516|  2.3|2241|5722|rle64 16|
|13727062|  3.4|**8515**|10421|**srle 32**|
|15175482|  3.8|4609|9360|rle64 32|
|19844801|  4.9|**14114**|**10611**|**srle 64**|
|21910714|  5.4|8301|10232|rle64 64|
|403920058|100.0|9391|9161|memcpy|

- Checkers program "End Game Table Base": [1034.db](http://encode.ru/threads/2077-EGTB-compression?p=41392&viewfull=1#post41392)

|C Size|ratio%|C MB/s|D MB/s|Name  /       2018-06|
|--------:|-----:|--------:|--------:|------------------------|
|82421332| 19.7|**801**|**4145**|**trle**|
|88055364| 21.0|273|1255|mrle|
|92422320| 22.0|**814**|**5936**|**srle 0**|
|92423009| 22.0|**1178**|**6697**|**srle 8**|
|93905327| 22.4|780|1660|rle64 8|
|113620895| 27.1|**1906**|5550|**srle 16**|
|117590491| 28.0|1341|2826|rle64 16|
|136948765| 32.7|**3581**|**8360**|**srle 32**|
|143953177| 34.3|2971|5506|rle64 32|
|165561604| 39.5|**5924**|**8953**|**srle 64**|
|176442237| 42.1|5090|7872|rle64 64|
|419225629|100.0|**9323**|**9179**|**memcpy**|

- Text File: [enwik9bwt](http://mattmahoney.net/dc/textdata.html) enwik9 bwt

|C Size|ratio%|C MB/s|D MB/s|Name /     2018-06 |
|--------:|-----:|--------:|--------:|----------------------|
|378377069| 37.8|**500**|**2090**|**trle**|
|419339698| 41.9|**506**|**5937**|**srle 0**|
|419340318| 41.9|**626**|4408|**srle 8**|
|422296235| 42.2|558|1364|rle64 8|
|487461871| 48.7|**1396**|4373|**srle 16**|
|498420792| 49.8|1113|2511|rle64 16|
|549214826| 54.9|**2778**|**7540**|**srle 32**|
|563503744| 56.4|2730|5074|rle64 32|
|576619945| 57.7|217|793|mrle|
|605764304| 60.6|**4998**|**7784**|**srle 64**|
|620676412| 62.1|**5247**|7376|**rle64 64**|
|1000000012|100.0|**9364**|**9184**|**memcpy**|

- Post-processing with entropy coding<br> 
  direct entropy encoding after "trle" (no additional "move to front" or other transformation)

|C Size|ratio%|C MB/s|D MB/s|Name /             CPU Skylake 3.4 GHz (2019-06)|
|--------:|-----:|--------:|--------:|-----------------------------------------------|
|180510948| 18.1|**154**| **132**|**trle + TurboRC o0** (order 0 bitwise Range Coder)|
|187099490| 18.7|23|**2560**|**trle + TurboHF 0** (Huffman Coding)|
|192420471| 19.2|**1527**|**3834**|**trle + TurboANX 12** (Asymmetric Numeral Systems)|
|193455670| 19.3|**2192**|2986|**trle + TurboHF 12**|
|197974078| 19.8|1078|1406|trle + fse (Finite State Entropy)|
|254312056| 25.4|119|105|mrle + TurboRC o0|

for more info, see also: [Entropy Coder Benchmark](https://sites.google.com/site/powturbo/entropy-coder)

### Compile:

  		git clone git://github.com/powturbo/TurboRLE.git
        cd TurboRLE

##### Linux + Windows MingW 
 
  		make
        or
  		make AVX2=1

##### Windows Visual C++

  		nmake /f makefile.vs
        or
  		nmake AVX2=1 /f makefile.vs

## Usage:

        ./trle file
        ./trle -e# file

		# = function id (see file trle.c)

### Environment:

###### OS/Compiler (32 + 64 bits):
- Linux: GNU GCC (>=4.6)
- clang (>=3.2) 
- Intel ICC 19.0
- Windows: MinGW
- Windows: Visual c++

#### References
  - [Real-Time Compression of IEC 61869-9 Sampled Value Data](https://pure.strath.ac.uk/portal/files/55444712/Blair_etal_AMPS2016_Real_time_compression_of_IEC_61869_9_sampled_value_data.pdf)
  - [Understanding Compression: Data Compression for Modern Developers](https://books.google.de/books?id=2C2rDAAAQBAJ&pg=PA216&lpg=PA216&dq=%22turborle%22&source=bl&ots=TiLU4Qf47s&sig=tkk0Dnk9NnU0JMR3Z6iW4TRquxg&hl=de&sa=X&ved=0ahUKEwjZq-Li5uXSAhXFCJoKHe77B6cQ6AEIyAEwHQ#v=onepage&q=%22turborle%22&f=false)
  - [Understanding Compression](http://file.allitebooks.com/20160805/Understanding%20Compression.pdf)
  - [Entropy Coder Benchmark](https://sites.google.com/site/powturbo/entropy-coder)

Last update: 18 Aug 2019


