## Zadanie 1
```perl
use warnings;
use strict;
my @words=();
while(<>){
    push(@words,$_);
}

sub compare{
    if ($c < $d){           #dla lancucha zankow: if ($c lt $d)
        return -1;
    }
    elsif($c == $d){        #dla lancucha znakow: elsif ($c eq $d)
        return 0;
    }
    else{
        return 1;
    }
}

my @sortedNumbers =  sort compare @words;

my @sorted = sort {lc $a cmp lc $b} @words;     # w przypadku porownania do liczb: {$a <=> $b}
#print "@words\n";
#print "============\n";
print "@sorted\n";
```

## Zadanie 2
```perl
use warnings;
use strict;
my @words=();
while(<>){
    chomp;
    push(@words,$_);
}
#my @wordslc = map {lc $_} @words;      #lc - lower case, uc - upper case, ucfirst - pierwsza duza litera, lcfirst - pierwsza mala litera
my @wordslc = map {[lc $_,$_]} @words;  #tablica dwuwymiarowa: map produkuje pierwszy element podlegajacy transformacji, drugi element bedacy elementem wejsciowym
#print "@wordslc\n";
#print "${$_}[0],${$_}[1]\n" foreach @wordslc;

#print "===========\n";
my @sorted = sort {${$a}[0] cmp ${$b}[0]} @wordslc;
#print "${$_}[0],${$_}[1]\n" foreach @sorted;

#print "-----------\n";
my @final = map {${$_}[1]} @sorted;
print "$_\n" foreach @final;
```