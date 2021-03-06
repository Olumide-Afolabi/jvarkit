# VcfTrap

annotate vcf with trap database http://trap-score.org/


## Usage

```
Usage: vcftrap [options] Files
  Options:
    -A, --attribute
      VCF INFO attribute Format:(ALT|GENE|SCORE)
      Default: TRAP
    -h, --help
      print help and exit
    --helpFormat
      What kind of help
      Possible Values: [usage, markdown, xml]
    --ignore-filtered
      Ignore FILTERed variants (faster)
      Default: false
  * -m, --manifest
      Manifest file. A tab delimited file with two columns : 
      chromosome(tab)path-to-file-indexed-with-trapindex. 
    -o, --out
      Output file. Optional . Default: stdout
    --outputbcf
      Output bcf (for streams)
      Default: false
    --vcfcreateindex
      VCF, create tribble or tabix Index when writing a VCF/BCF to a file.
      Default: false
    --vcfmd5
      VCF, create MD5 checksum when writing a VCF/BCF to a file.
      Default: false
    --version
      print version and exit

```


## Keywords

 * vcf
 * trap
 * annotation


## Compilation

### Requirements / Dependencies

* java [compiler SDK 1.8](http://www.oracle.com/technetwork/java/index.html) (**NOT the old java 1.7 or 1.6**) and avoid OpenJdk, use the java from Oracle. Please check that this java is in the `${PATH}`. Setting JAVA_HOME is not enough : (e.g: https://github.com/lindenb/jvarkit/issues/23 )
* GNU Make >= 3.81
* curl/wget
* git
* xsltproc http://xmlsoft.org/XSLT/xsltproc2.html (tested with "libxml 20706, libxslt 10126 and libexslt 815")


### Download and Compile

```bash
$ git clone "https://github.com/lindenb/jvarkit.git"
$ cd jvarkit
$ make vcftrap
```

The *.jar libraries are not included in the main jar file, [so you shouldn't move them](https://github.com/lindenb/jvarkit/issues/15#issuecomment-140099011 ).
The required libraries will be downloaded and installed in the `dist` directory.

Experimental: you can also create a [fat jar](https://stackoverflow.com/questions/19150811/) which contains classes from all the libraries, on which your project depends (it's bigger). Those fat-jar are generated by adding `standalone=yes` to the gnu make command, for example ` make vcftrap standalone=yes`.

### edit 'local.mk' (optional)

The a file **local.mk** can be created edited to override/add some definitions.

For example it can be used to set the HTTP proxy:

```
http.proxy.host=your.host.com
http.proxy.port=124567
```
## Source code 

[https://github.com/lindenb/jvarkit/tree/master/src/main/java/com/github/lindenb/jvarkit/tools/trap/VcfTrap.java](https://github.com/lindenb/jvarkit/tree/master/src/main/java/com/github/lindenb/jvarkit/tools/trap/VcfTrap.java)


<details>
<summary>Git History</summary>

```
Fri Nov 10 19:31:29 2017 +0100 ; fix a bug in trapindexer ; https://github.com/lindenb/jvarkit/commit/83c4f8cbf9cdf85a1d310b4e661797ed6febe5bd
Fri Nov 10 18:25:15 2017 +0100 ; vcftrap min/max && fix fat in makefile ; https://github.com/lindenb/jvarkit/commit/aad41d76ccb11cc7b8d6eafb289c2a0242a18f2e
Tue Nov 7 10:25:46 2017 +0100 ; tools for trap-score.org ; https://github.com/lindenb/jvarkit/commit/54bf01ddbf3594f5a5b4aee149d67604df343af7
Tue Nov 7 10:22:52 2017 +0100 ; tools for trap-score.org ; https://github.com/lindenb/jvarkit/commit/f4229a3e73f1be84e74e1ba3aad3d11fdbdaf541
```

</details>

## Contribute

- Issue Tracker: [http://github.com/lindenb/jvarkit/issues](http://github.com/lindenb/jvarkit/issues)
- Source Code: [http://github.com/lindenb/jvarkit](http://github.com/lindenb/jvarkit)

## License

The project is licensed under the MIT license.

## Citing

Should you cite **vcftrap** ? [https://github.com/mr-c/shouldacite/blob/master/should-I-cite-this-software.md](https://github.com/mr-c/shouldacite/blob/master/should-I-cite-this-software.md)

The current reference is:

[http://dx.doi.org/10.6084/m9.figshare.1425030](http://dx.doi.org/10.6084/m9.figshare.1425030)

> Lindenbaum, Pierre (2015): JVarkit: java-based utilities for Bioinformatics. figshare.
> [http://dx.doi.org/10.6084/m9.figshare.1425030](http://dx.doi.org/10.6084/m9.figshare.1425030)


## Example:

```
java -jar dist/trapindexer.jar  -o chr22.dat chr22.TraPv2.txt.gz
echo -e "22\tchr22.dat" > out.manifest
java -jar dist/vcftrap.jar -m out.manifest input.vcf
```


## See also

* TrapIndexer


