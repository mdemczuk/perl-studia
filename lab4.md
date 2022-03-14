## Zadanie 1
```perl
my $autor = "Bursa";
my $zm = << "END";
Dzieci są milsze od dorosłych
Zwierzęta są milsze od dzieci...
Andrzej $autor, 1957
END

print $zm;
```

## Zadanie 2
```perl
while(<>){ #$_, operator diamentowy
    print;
}
print "\n";
```

## Zadanie 3
```perl
my $sqr= 0;
if ($ARGV[0]) { $sqr = $ARGV[0]*$ARGV[0]; };
print "$sqr\n";
```

## Zadanie 4

Wyświetla się wynik równy -4. Dzieje się tak ponieważ wartość -2 nie jest określona w nawiasie i przez to program odnosi "-" do wyniku a nie do konkretnej wartości.


## Zadanie 5
```perl
my $sqr = 0;
$sqr = <STDIN>;
chomp($sqr);
if ($sqr=~ /^[0-9]+/) { $sqr = $sqr=$sqr**2; };
else {die("Nie podano liczby\n");}
print "$sqr\n";
```

## Zadanie 6
```perl
sub log10{
    my $n = shift;
    return log($n)/log(10);
}
```

Zadanie 7
```perl
print "@a\n";   #elementy zostają odddzielone spacjami
print @a;       #elementy są wypisywane bez spacji
```

## Zadanie 8
```perl
print "@a";	#elementy zostają oddzielone spacjami
print @a;	#elementy zostają wypisane zaraz po elementach z poprzedniej tablicy i nie są oddzielone spacjami

print "@b";	#elementy zostają oddzielone spacjami, zostaje też zinterpretowany znak \n jako znak nowej linii, ponieważ był on w podwójnym cudzysłowie
print @b;	#elementy nie zostają oddzielone spacjami, ale nadal zostaje zinterpretowany znak nowej linii

print "@c";print "\n"; 	#elementy zostaja oddzielone spacjami, jednak znak nowej linii nie został zinterpretowany, ponieważ w tablicy był ujęty w pojedynczym cudzysłowie, więc został wypisany jako ciąg znaków
```

## Zadanie 9

q - pojedynczy cudzysłów
qw - wypisanie słów z łańcucha bez żadnych separatorów
qq - podwójny cudzysłów


## Zadanie 10
```perl
a) perl -le '$a=0; print ++$a + $a++'; => 3
b) perl -le '$a=0; print $a++ + ++$a'; => 2
c) perl -le '$a=0; print $a++ + $a++'; => 1
d) perl -le '$a=0; print ++$a + ++$a'; => 4
```

## Zadanie 11
```perl
my $i = 0;
my @t = 0;
$t[$i++] = $t[$i++] + 1;
print "i = $i  t = @t\n";
$i = 0;
@t = 0;
$t[$i++] += 1;
print "i = $i  t = @t\n";
```
Wyniki działań na zmiennej $a dają taki sam wynik. W przypadku zmiennych $i oraz $t[i++] wyniki są już inne. Przy dłuższej wersji zmienna $i zwiększana jest łącznie dwa razy poprzez dwukrotne wywołanie $i++. W przypadku, gdy t jest tablicą, to wynik dłuższej wersji to:
i = 2, t = 0 1

W wersji skróconej inkrementacja zmiennej $i następuje tylko raz, przez co werjsa skrócona nie rozwija się do wersji dłuższej, a otrzymany wynik to:
i = 1, t = 1


## Zadanie 12
```perl
$a = $b || 'default'; 	# || ma priorytet wyższy niż znak =, czyli najpierw robi się $b || default, a potem $a = $b

$a = $b or 'default'; 	# or ma priorytet niższy niż znak =
```

Można powiedzieć, że 
" $a = $b || 'default' "
działa jak 
" $a = ($b || 'default') "
natomiast 
" $a = $b or 'default' "
działa jak 
" ($a = $b) or 'default' "

## Zadanie 13
```perl
my $string = q(ALA,A
ARG,R
ASN,N
ASP,D
CYS,C
GLN,Q
GLU,E
GLY,G
HIS,H
HSD,H
ILE,I
LEU,L
LYS,K
MET,M
PHE,F
PRO,P
SER,S
THR,T
TRP,W
TYR,Y
VAL,V);


$string=~ s/\n/,/g;     #zamienianie wystąpień znaku nowej linii "\n" na znak przecinka ","; g oznacza, że robimy to globalnie
#print "$string\n";
my %amino = split(/,/,$string); #zmieniamy łańcuch znaków na tablice (czesc ze splitem), a te tablice wykorzystujemy do zainicjalizowania hasha
#print "$amino{'ARG'}\n";
while (<>){
    if ((/^ATOM/) && (/CA/)){       #jak nie ma żadnej literki na początku, to wykonywane jest match
        $aminokwas = substr($_,17,3);
        $chain = substr($_,21,1);
        print "$amino{$aminokwas}";
    }
    #if (/^TER/) {last;}            #jezeli dla jednego modelu, to sprawdzamy, czy sie zakonczyla sekcja za tym modelem, czyli sekcja TER
}
print "\n";

```

## Zadanie 14
```perl
$string=~ s/\n/,/g;
my %amino = split(/,/,$string);
while (<>){
    if ((/^ATOM/) && (/CA/)){
        $aminokwas = substr($_,17,3);
        $chain = substr($_,21,1);
        print "$amino{$aminokwas}";
    }
    #if (/^TER/) {last;}          
}
print "\n";
```