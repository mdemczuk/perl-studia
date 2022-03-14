## Zadanie 1
```perl
use warnings;
use strict;

open(my $fh, "<", $ARGV[0])
    or die "Can't open < $ARGV[0]: $!";

open(my $fout, ">", $ARGV[1])
    or die "Can't open > $ARGV[1]: $!";

while (my $line = <$fh>) {      #ewentualnie: while (<$fh>)
    print $fout $line;          #print $fout $_;
} 
 

close($fh);
close($fout);
```

## Zadanie 2
```perl
use warnings;
use strict;
open(my $fm1, "<", $ARGV[0])
    or die "Can't open < $ARGV[0]: $!";

open(my $fm2, "<", $ARGV[1])
    or die "Can't open > $ARGV[1]: $!";

print "Martrix: $ARGV[0]\n";
my @m1 = ();
while (<$fm1>) {      
    print; 
    push(@m1,[split]);
} 
#print "\n@m1\n";
my @m2 = ();
print "\nMartrix: $ARGV[1]\n";
while (<$fm2>){
    print;
    push(@m2,[split]);
}

print "\nPetla for:\n";
my @m3 = ();

for (my $i = 0; $i < @m1; $i++) {
    for (my $j = 0; $j < @{$m1[$i]}; $j++) {
        #print "$m1[$i][$j] ";
        $m3[$i][$j] = $m1[$i][$j] + $m2[$i][$j];
    }
    print "\n";
}
print "\nSuma:\n";
print "@{$_}\n" foreach @m3;    #instrukcja print ma być wykonywana na każdym elemencie przekazywanym przez foreach; $_ to referencja do wiersza

#print "\n";
close($fm1);
close($fm2);
```


## Zadanie 3
```perl
use warnings;
use strict;
#my @tab = (0) x 101;
#my $size = @tab;      #rozmiar tablicy tab
#print "@tab\n $size $#tab\n";   # "$#tab" pokazuje indeks ostatniego elementu

my $size = 1000;
my @tab = (0..$size);
$tab[0] = '';
$tab[1] = '';
for my $i (2..sqrt($size)){
    if ($tab[$i]){
        my $j = $i * $i;
        while ($j <= $size){
            $tab[$j] = '';
            $j += $i;
        } 
    }
}

print (($_)?"$_ ":"") foreach @tab;
print "\n";
```

## Zadanie 4
```perl
use warnings;
use strict;
my $p = <STDIN>;   #przy podawaniu wzorca na wejsciu
chomp $p;
while(<>){
    if(/$p/){        # \b(\d{5}\b), \b to granica słów # 
        print "\n$_";
        my @tab = $_=~ /$p/g;
        my $count = () = $_=~ /$p/g;
        print "\nZnaleziono: |@tab|";
        print "\nCount: $count \n$_";
    }
}

print "\n";
```

## Zadanie 5
```perl
while(<>){
    s/1/jeden/g;
    s/2/dwa/g;
    s/3/trzy/g;
    s/4/cztery/g;
    s/5/piec/g;
    s/6/szesc/g;
    s/7/siedem/g;
    s/8/osiem/g;
    s/9/dziewiec/g;
    s/0/zero/g;
    print;
    print "\n";
}
```

## Zadanie 6 
```perl
my $text ="To jest tekst tekst tekst bardzo wazny i i istotny wrecz wrecz niezastapiony tekst";
#Wyjście: To jest [tekst tekst tekst] bardzo wazny [i i] istotny [wrecz wrecz] niezastapiony tekst"

#$text =~ s/(\b(\w+)\b(\s+\2\b)+)/[$1]/g;
print $text;
print "\n";
```

## Zadanie 7
```perl
my $text ="To jest tekst tekst tekst bardzo wazny i i istotny wrecz wrecz niezastapiony tekst";
$text =~ s/(?'caly'\b(?'nazwa'\w+)\b(\s+\g{nazwa}\b)+)/$+{nazwa}/g;
print "$text\n";
```
