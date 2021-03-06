# VcfGapFrequent

![Last commit](https://img.shields.io/github/last-commit/lindenb/jvarkit.png)

Filter VCF annotated with external (AF or AC/AN) frequency information like vcfgnomad


## Usage

```
Usage: vcfgapfrequent [options] Files
  Options:
    -D, --database
      VCF database(s) used as a reference of frequent variants. One file 
      ending with '.list' is interpretted as a list of path.
      Default: []
    -f, --fields
      Where to peek the frequencies from the database.How to extract the 
      AlleleFrequencies from a variant. Multiple separated with comma or 
      semicolon. e.g: "AC/AN;exome_CEU_*;genome_NFE_AF;another_AC/another/AN". 
      Input is a set of AC/AN field pairs or/and AF field separated by 
      semicolon. 'x/y' means AC/AN fields. '*' will be replaced with AC and 
      AN, hence, 'exome_CEU_*' will be interpreted as 
      exome_CEU_AC/exome_CEU_AN. Other field will be interpreted as an AF 
      field. 
      Default: AC/AN;AF
    -h, --help
      print help and exit
    --helpFormat
      What kind of help
      Possible Values: [usage, markdown, xml]
    -M, --max-length
      Max segment length of NO_CALL
      Default: 1000000
    -m, --min-length
      Min segment length of NO_CALL
      Default: 1000
    -o, --output
      Output file. Optional . Default: stdout
    -C, -skip, --skip
      Skip missing whole chromosome
      Default: false
    -t, --max, --treshold
      Allele Frequency Treshold. Only Variant in database(s) with extracted AF 
      greater than this value are considered.
      Default: 0.4
    --version
      print version and exit

```


## Keywords

 * vcf


## Compilation

### Requirements / Dependencies

* java [compiler SDK 1.8](http://www.oracle.com/technetwork/java/index.html) (**NOT the old java 1.7 or 1.6**, not the new 1.9) and avoid OpenJdk, use the java from Oracle. Please check that this java is in the `${PATH}`. Setting JAVA_HOME is not enough : (e.g: https://github.com/lindenb/jvarkit/issues/23 )
* GNU Make >= 3.81
* curl/wget
* git


### Download and Compile

```bash
$ git clone "https://github.com/lindenb/jvarkit.git"
$ cd jvarkit
$ make vcfgapfrequent
```

The *.jar libraries are not included in the main jar file, [so you shouldn't move them](https://github.com/lindenb/jvarkit/issues/15#issuecomment-140099011 ).
The required libraries will be downloaded and installed in the `dist` directory.

Experimental: you can also create a [fat jar](https://stackoverflow.com/questions/19150811/) which contains classes from all the libraries, on which your project depends (it's bigger). Those fat-jar are generated by adding `standalone=yes` to the gnu make command, for example ` make vcfgapfrequent standalone=yes`.

### edit 'local.mk' (optional)

The a file **local.mk** can be created edited to override/add some definitions.

For example it can be used to set the HTTP proxy:

```
http.proxy.host=your.host.com
http.proxy.port=124567
```
## Source code 

[https://github.com/lindenb/jvarkit/tree/master/src/main/java/com/github/lindenb/jvarkit/tools/structvar/VcfGapFrequent.java](https://github.com/lindenb/jvarkit/tree/master/src/main/java/com/github/lindenb/jvarkit/tools/structvar/VcfGapFrequent.java)

### Unit Tests

[https://github.com/lindenb/jvarkit/tree/master/src/test/java/com/github/lindenb/jvarkit/tools/structvar/VcfGapFrequentTest.java](https://github.com/lindenb/jvarkit/tree/master/src/test/java/com/github/lindenb/jvarkit/tools/structvar/VcfGapFrequentTest.java)


## Contribute

- Issue Tracker: [http://github.com/lindenb/jvarkit/issues](http://github.com/lindenb/jvarkit/issues)
- Source Code: [http://github.com/lindenb/jvarkit](http://github.com/lindenb/jvarkit)

## License

The project is licensed under the MIT license.

## Citing

Should you cite **vcfgapfrequent** ? [https://github.com/mr-c/shouldacite/blob/master/should-I-cite-this-software.md](https://github.com/mr-c/shouldacite/blob/master/should-I-cite-this-software.md)

The current reference is:

[http://dx.doi.org/10.6084/m9.figshare.1425030](http://dx.doi.org/10.6084/m9.figshare.1425030)

> Lindenbaum, Pierre (2015): JVarkit: java-based utilities for Bioinformatics. figshare.
> [http://dx.doi.org/10.6084/m9.figshare.1425030](http://dx.doi.org/10.6084/m9.figshare.1425030)


## Example

```
$ find /commun/data/pubdb/broadinstitute.org/gnomad/release-170228/ -name "*.vcf.gz" > gnomad.list

$ java -jar dist/vcfgapfrequent.jar --fields "AF_POPMAX" -C -D gnomad.list genotyped.22.vcf.gz  > out.bed

```


