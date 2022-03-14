```perl
use Bio::Structure::IO;
use strict;

$seq_obj = Bio::Seq->new(-seq => "aaaatgggggggggggccccgtt",
                        -alphabet => 'dna' );

print $seq_obj->seq;
print "\n";
$prot_obj = $seq_obj->translate;
print $prot_obj->seq;
```
## Zadanie 1
```perl
my $file = "1FNT.pdb"; 
my $structio = Bio::Structure::IO->new(-file => $file);
my $struc = $structio->next_structure;
 
for my $chain ($struc->get_chains) {
   my $chainid = $chain->id;
   # one-letter chaincode if present, 'default' otherwise
   for my $res ($struc->get_residues($chain)) {
      my $resid = $res->id;
      # format is 3-lettercode - dash - residue number, e.g. PHE-20
      my $atoms = $struc->get_atoms($res);
      # actually a list of atom objects, used here to get a count
      print join "\t", $chainid,$resid,$atoms,"\n";
   }
}
```

## Zadanie 2
```perl
use Bio::DB::GenBank;
use Bio:::SeqIO;
my $gb = Bio::DB::GenBank->new();
 
my $seq = $gb->get_Seq_by_id('J01673');

my $out = Bio::SeqIO->new(-file => ">output" ,
                         -format => 'FASTA');
$out->write_seq($seq);
```

## Zadanie 3
```perl
use Bio::DB::GenBank;
use Bio::SeqIO;
my $gb = Bio::DB::GenBank->new();
 
my $seq = $gb->get_Seq_by_id('j01673');

my $prot_obj = $seq_obj->translate;

my $out = Bio::SeqIO->new(-file => ">output.fasta" ,
                         -format => 'fasta');
$out->write_seq($prot_obj);
```