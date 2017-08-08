# docker-silicos-it

Docker image for [silicos-it software](http://silicos-it.be.s3-website-eu-west-1.amazonaws.com/index.html).

## Build

docker build -t 3dechem/silicosit .

## Run

Apply filter it on smiles strings
```
echo 'C[C@H](NCc1ccc(OCc2cccc(F)c2)cc1)C(=O)N' > input.smiles
echo 'NC(=O)c1cccc2cn(nc12)c3ccc(cc3)[C@@H]4CCCNC4' >> input.smiles
echo 'ONLY_ELEMENTS C H O N Br Cl' > filter.txt
docker run -ti --user $UID -v $PWD:/data 3dechem/silicosit filter-it --input=/data/input.smiles --filter=/data/filter.txt
```

The programs: align-it, filter-it, shape-it, strip-it are available in /usr/local/bin inside image.
