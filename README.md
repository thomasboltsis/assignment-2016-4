# Ένα Κιλό Δεδομένων

Η ποσότητα των δεδομένων που παράγεται στον κόσμο αυξάνεται ραγδαία, και μαζί μ' αυτή και οι ανάγκες αποθήκευσης. Ήδη, τα μεγάλα υπολογιστικά κέντρα είναι μεγαλύτερα από γήπεδα ποδοσφαίρου και χρειάζονται όσο ηλεκτρικό ρεύμα όσο και μια πόλη για να λειτουργήσουν.

Οι επιστήμονες αναζητούν νέους τρόπους αποτελεσματικής αποθήκευσης δεδομένων και μία μέθοδος που έχει ενδιαφέρον είναι η χρήση του DNA ως αποθηκευτικού μέσου. Με τη σωστή κωδικοποίηση, ένα κυβικό εκατοστό DNA μπορεί να αποθηκεύσει 10<sup>16</sup> bits δεδομένων, το οποίο σημαίνει ότι μπορούμε να αποθηκεύσουμε όλα τα δεδομένα του κόσμου σε ένα κιλό DNA.

Αλλά ποια κωδικοποίηση μπορούμε να χρησιμοποιήσουμε; Μία προσέγγιση είναι η εξής. Έστω ότι θέλουμε να κωδικοποιήσουμε ένα αρχείο:

* Παίρνουμε τα περιεχόμενα του αρχείου και τα κωδικοποιούμε με κωδικοποίηση Huffman *με βάση το τρία*. Στη συνήθη κωδικοποίηση Huffman, o κώδικας Huffman που προκύπτει κωδικοποιεί τα δεδομένα μας χρησιμοποιώντας bits, δηλάδη 0 και 1. Στην κωδικοποίηση Huffman με βάση το τρία, κωδικοποιούμε τα δεδομένα μας χρησιμοποιώντας trits, δηλαδή, 0, 1, και 2. 
* Η κωδικοποίηση Huffman με βάση το τρία λειτουργεί ακριβώς με τον ίδιο τρόπο όπως και η κωδικοποίηση Huffman με βάση το δύο, όμως όταν επεξεργαζόμαστε την ουρά προτεραιτότητας, αντί να βγάζουμε κάθε φορά δύο στοιχεία και να εισάγουμε ένα, βγάζουμε τρία στοιχεία και εισάγουμε ένα. 
* Με τον τρόπο αυτό παράγεται και πάλι ένα δένδρο, το οποίο είναι τριαδικό. Στα κλαδιά του αντί για 0 και 1 αντιστοιχούμε 0, 1, και 2. Η κωδικοποίηση Huffman προκύπτει τότε και πάλι από τα μονοπάτια από το ρίζα μέχρι κάθε φύλλο του δένδρου.
* Χρειάζεται προσοχή αν το αρχείο μας δεν έχει μονό αριθμό χαρακτήρων. Αφού κατά τη διάρκεια της επεξεργασίας της ουράς προτεραιότητας κάθε φορά βγάζουμε τρία στοιχεία και προσθέτουμε ένα, κάθε φορά το μέγεθός της μειώνεται κατά δύο. Συνεπώς για να δουλέψει ο αλγόριθμος αν το αρχείο μας δεν έχει μονό αριθμό χαρακτήρων πρέπει να προσθέσουμε ένα νοητό χαρακτήρα με συχνότητα εμφάνισης μηδέν.

Έχοντας κωδικοποιήσει το αρχείο μας με τον τριαδικό κώδικα Huffman, στη συνέχεια το κωδικοποιούμε με τις βάσεις του DNA, A (adenine), C (cytocine), G (guanine), T (thymine). Για να το κάνουμε αυτό διαβάζουμε χαρακτήρα χαρακτήρα τα trits του κωδικοποιημένου με τον τριαδικό κώδικα Huffman αρχείο και κωδικοποιούμε χρησιμοποιώντας τον παρακάτω πίνακα:

<table>
  <tr>
    <th>προηγούμενη βάση</th>
    <th colspan="3">τρέχον trit</th>
  </tr>
  <tr>
    <td></td>
    <td>0</td>
    <td>1</td>
    <td>2</td>
  </tr>
  <tr>
    <td>A</td>
    <td>C</td>
    <td>G</td>
    <td>T</td>
  </tr>
  <tr>
    <td>C</td>
    <td>G</td>
    <td>T</td>
    <td>A</td>
  </tr>
  <tr>
    <td>G</td>
    <td>T</td>
    <td>A</td>
    <td>C</td>
  </tr>
  <tr>
    <td>T</td>
    <td>A</td>
    <td>C</td>
    <td>G</td>
  </tr>
</table>

Ο πίνακας αυτός χρησιμοποιείται ως εξής: αν θέλουμε να κωδικοποιήσουμε το trit 2 και το προηγούμενο trit που κωδικοποιήσαμε κωδικοποιήθηκε με τη βάση G, τότε το 2 θα κωδικοποιηθεί με τη βάση C, κ.ο.κ. Για το πρώτο trit, όπου δεν έχουμε κάποιο προηγούμενο, θεωρούμε ότι υπήρχε ένα νοητό προηγούμενο trit που κωδικοποιήθηκε με τη βάση A.

Για παράδειγμα, αν θέλουμε να κωδικοποιήσουμε ένα αρχείο το οποίο περιέχει τη φράση "hello, world" με τριαδικό κώδικα Huffman, θα προκύψει η παρακάτω κωδικοποίηση:

<img src="hello_world.png">

Προσέξτε ότι το αρχείο τελειώνει σε χαρακτήρα νέας γραμμής (`\n`), ο οποίος επίσης κωδικοποιείται. Επίσης, το αρχείο έχει μονό αριθμό χαρακτήρων, οπότε στην είσοδο του αλγορίθμου για την κωδικοποίηση Huffman προσθέσαμε έναν νοητό χαρακτήρα, τον οποίο συμβολίζουμε στον παραπάνω πίνακα με &Oslash;. Στην πράξη, ο χαρακτήρας αυτός μπορεί να είναι απλώς ο κενός χαρακτήρας `''`, ο οποίος είναι το τίποτε, όχι ο χαρακτήρας του διαστήματος `' '`. Τον ίδιο το χαρακτήρα του διαστήματος τον συμβολίζουμε με &#9251;. Το δένδρο αυτό είναι στην ουσία ο παρακάτω πίνακας αντιστοίχισης:

| Γράμμα | Κωδικοποίηση |
|--------|--------------|
|   l    |      1       |
|   h    |     00       |
|   r    |     01       |
|   w    |     02       |
|   o    |     21       |
|&Oslash;|    200       |
|  \n    |    201       |
|&#9251; |    202       |
|   ,    |    220       |
|   d    |    221       |
|   e    |    222       |

Έτσι, η κωδικοποίηση σε τριαδικό κώδικα Huffman του αρχείου είναι η:

```
0022211212202020221011221201
```

Τώρα, εργαζόμενοι με τον πίνακα αντιστοίχισης trits και βάσεων, το `0` θα γίνει `C`, στη συνέχεια το δεύτερο `0` θα γίνει `G`, το `2` θα γίνει `C`, κ.λπ., ώστε στο τέλος θα έχουμε την παρακάτω αλυσίδα DNA:

```
CGCATCTGATGTGTGTGCTAGATGATAG
```
Η αποκωδικοποίηση αυτής της αλυσίδας DNA προχωράει με τον ακριβώς αντίστροφο τρόπο. Παίρνουμε έναν-ένα τις βάσεις της και τις μετατρέπουμε σε trits με βάση τον ακόλουθο πίνακα:

<table>
  <tr>
    <th>πρoηγούμενη βάση</th>
    <th colspan="4">τρέχουσα βάση</th>
  </tr>
  <tr>
    <td></td>
    <td>A</td>
    <td>C</td>
    <td>G</td>
    <td>T</td>
  </tr>
  <tr>
    <td>A</td>
    <td></td>
    <td>0</td>
    <td>1</td>
    <td>2</td>
  </tr>
  <tr>
    <td>C</td>
    <td>2</td>
    <td></td>
    <td>0</td>
    <td>1</td>
  </tr>
  <tr>
    <td>G</td>
    <td>1</td>
    <td>2</td>
    <td></td>
    <td>0</td>
  </tr>
  <tr>
    <td>T</td>
    <td>0</td>
    <td>1</td>
    <td>2</td>
    <td></td>
  </tr>
</table>

Ο πίνακας χρησιμοποιείται όπως και στην κωδικοποίηση. Αρχικά θεωρούμε ότι η προηγούμενη βάση που έχουμε δει είναι η `A`. Στο παράδειγμά μας, παίρνουμε τη βάση `C`, η οποία αποκωδικοποιείται σε `0`. Στη συνέχεια παίρνουμε τη βάση `G`, η προηγούμενη βάση είναι η `C`, οπότε αποκωδικοποιείται σε `0`, κ.ο.κ.
