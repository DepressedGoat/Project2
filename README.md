# Project2
Second assignment for class "Αρχιτεκτονική Υ/Η"

# **Βήμα 1**

### Ερωτημα 1:

Το μέγεθος της L1 cache (icache και dcache), το cache line size καθώς και το associativity της L1 και L2 είναι ίδιο σε όλες τις προσομοιώσεις σε αυτό το βήμα. Αυτο συμβαίνει δίοτι αυτά τα στοιχεία αποτελούν μερικές από τις παραμέτρους με τις οποίες τρέχει η προσομοίωση. Αφού δεν ορίζουμε εμείς τις τιμές τους όταν καλούμε να τρέξει ο gem5 τότε χρησιμοποιούνται οι default τιμές που ορίζονται απο το script που τρέχουμε. Επομένως ελέγχοντας και τα stats.txt για επαλήθευση έχουμε πως:

- L1 icache = 32758 (32kB) , L1 dcache = 65536 (64kB)
  
- L1 associativity = 2 , L2 associativity = 8
  
- cache line size = 64kB
  

Όσον αφορά τα μεγέθη της L2 cache για τις 5 προσομοιώσεις έχουμε:

- Specbzip : L2 icache = 1796 , L2 dcache = 2133756
  
- Spechmmer : L2 icache = 10955 , L2 dcache = 199202
  
- Speclibm : L2 icache = 1325 , L2 dcache = 4462914
  
- Specmcf : L2 icache = 2006342 , L2 dcache = 165404
  
- Specsjeng : L2 icache = 1517 , L2 dcache = 15789180
  

### Ερώτημα 2:

Εξετάζοντας τα αρχεία stats.txt βρίσκουμε πως :

- **Simulation seconds :**
  
  - Specbzip : 0.083982
    
  - Spechmmer : 0.059396
    
  - Speclibm : 0.174671
    
  - Specmfc : 0.064955
    
  - Specsjeng : 0.513528
    
- **CPI :**
  
  - Specbzip : 1.679650
    
  - Spechmmer : 1.187917
    
  - Speclibm : 3.493415
    
  - Specmfc : 1.299095
    
  - Specsjeng : 10.270554
    
- **Μiss rates icache :**
  
  - Specbzip : 0.000077
    
  - Spechmmer : 0.000221
    
  - Speclibm : 0.000094
    
  - Specmfc : 0.023612
    
  - Specsjeng : 0.000020
    
- **Miss rates dcache :**
  
  - Specbzip : 0.014798
    
  - Spechmmer : 0.001637
    
  - Speclibm : 0.060972
    
  - Specmfc : 0.023612
    
  - Specsjeng : 0.121831
    

Παραθέτω τα αντίστοιχα γραφήματα.

**Sim_seconds :**

![simsecondspng](file://https://github.com/DepressedGoat/Project2/blob/main/graphs/sim_seconds.png)

**CPI :**

![CPIpng](file://C:\Users\Jay\Desktop\ERGASIA_MASTER\Ergasia%202\graphs\CPI.png?msec=1669989967037)

**Μiss rates icache :**

![miss rate icachepng](file://C:\Users\Jay\Desktop\ERGASIA_MASTER\Ergasia%202\graphs\miss%20rate%20icache.png?msec=1669989967038)

**Μiss rates dcache :**

![miss rate dcachepng](file://C:\Users\Jay\Desktop\ERGASIA_MASTER\Ergasia%202\graphs\miss%20rate%20dcache.png?msec=1669989967038)

### Eρώτημα 3:

Σε όλες τιςπροσομοιώσεις το **system.clk_domain.clock** είναι **1000** (1GHz). Γενικά το cpu clock και το system clock δεν έχουν την ίδια ταχύτητα, είναι ανεξάρτητα μεταξύ τους και προσδιορίζονται κατα την κλήση του gem5 απο τις παραμέτρους που ορίζουμε. Αφού τρέξω τις προσομοιώσεις ξανά, μια φορά με cpu clock 1Ghz και μια με 3Ghz, έχω τα εξής αποτελέσματα.

- Για default GHz : cpu_clock_domain = 500 , cpu_cluster.clk_domain.clock. = 500
  
- Για 1GHz : cpu_clock_domain = 1000 , cpu_cluster.clk_domain.clock. = 1000
  
- Για 3Ghz : cpu_clock_domain = 333 , cpu_cluster.clk_domain.clock. = 333
  

Ίδια για όλες τις προσομοιώσεις.

Παρατηρώ πως ενώ ανεβάζω το cpu clock η τιμή cpu_clock_domain μειώνεται. Το γεγονός αυτό δεν είναι τυχαίο, μπορώ εύκολα να διαπιστώσω πως το πραγματικο clock του επεξεργαστή δίνεται απο τον τύπο system.clk_domain.clock / cpu_clock_domain. Επομένως για την συχνότητα 3Ghz έχω απο τον τύπο, 1000/333 = 3GHz (ομοίως και για τα 1GHz κ.ο.κ). Δεν γνωρίζω ακριβώς γιατί ο gem5 αναγράφει το clock του cpu αναλογικά με το system clock, πάντως μια εξήγηση είναι ότι το clock (system και cpu) αναφέρεται στην περίοδο και όχι στην συχνότητα, επομένως έχοντας περίοδο cpu 333 και περίοδο 1000 system σημαίνει ότι εχω τριπλάσια συχνότητα απο το system clock, επομένως 3GHz. Το ίδιο ακριβώς συμβαίνει σε όλες τις συχνότητες (1Ghz και default που είναι 2GHz). Εάν προσθέσουμε και άλλο επεξεργαστή τότε η συχνότητα του θα είναι η ίδια με του πρώτου, δηλαδή η default 2GHz εκτός και εάν έχουμε ορίσει εμείς άλλη συχνότητα σαν παράμετρο κατα τη κλήση του gem5.

Παρατηρώ ότι όταν ανεβάζω τη ταχήτητα του του επεξαργαστή, δηλαδή όταν αυξάνω το cpu clock, τότε ο χρόνος εκτέλεσης του προγράμματος μειώνεται. Φυσικά και υπάρχει μια αναλογική σχέση μεταξύ cpu clock και χρόνου εκτέλεσης, αλλά δεν υπάρχει τέλειο scaling. Όταν διπλασιάζω τη συχνότητα του cpu δεν υποδιπλασιάζεται ο χρόνος εκτέλεσης. Συγκεκριμένα ο χρόνος εκτέλεσης του specbzip για 1GHz είναι 0.161 ενώ για 3GHz είναι 0.058, δηλαδή για τριπλασιασμό του clock έχω βελτίωση 2.77 στο χρόνο εκτέλεσης.

### Eρώτημα 4:

Τρέχοντας το **specmfc** με τύπο μνήμης DDR3 2133MHz x64 παρατηρώ ότι ο χρόνος εκτέλεσης και το CPI μειώνονται, λογικό αφόυ η ταχύτητα της μνήμης RAM επιρεάζει το χρόνο εκτέλεσης.

# **Βήμα 2**

### Ερώτημα 1:

Η απόδοση του κάθε benchmark εξαρτάται απο διαφορετικούς παράγοντες. To benchmark **bzip** παρουσιάζει καλύτερη απόδοση όσο αυξάνω το μέγεθος της **L1 dcache** size και **L2 size**. Το benchmark **spechmmer** βασίζεται σχεδόν αποκλειστικά απο το **L1 dcache** size. Το **specmcf** παρουσιάζει σημαντική βελτίωση όταν αυξάνω το **L1 icache** size, ενώ η απόδοση μειώνεται εαν μεγαλώσω το cache line size. Για το **speclibm** ισχύει ότι ο παράγοντας **cache line size** παίζει καθοριστικό ρόλο στη βελτίωση του CPI, η επίδραση των άλλων είναι μηδαμινή. Ομοίως για το benchmark **specsjeng**, ο μοναδικός παράγοντας που βελτίωσε σημαντικά το CPI είναι το **cache line size**.

### Ερώτημα 2:

Παραθέτω τα γραφήματα:

- Specbzib:
  
  ![specsbzibCPIpng](file://C:\Users\Jay\Desktop\ERGASIA_MASTER\Ergasia%202\graphs\specsbzib_CPI.png?msec=1669989967039)
  
- Speclibm:
  
  ![speclibmCPIpng](file://C:\Users\Jay\Desktop\ERGASIA_MASTER\Ergasia%202\graphs\speclibm_CPI.png?msec=1669989967040)
  
- Specmcf:
  
  ![specmcfCPIpng](file://C:\Users\Jay\Desktop\ERGASIA_MASTER\Ergasia%202\graphs\specmcf_CPI.png?msec=1669989967040)
  
- specsjeng:
  
  ![specsjengCPIpng](file://C:\Users\Jay\Desktop\ERGASIA_MASTER\Ergasia%202\graphs\specsjeng_CPI.png?msec=1669989967040)
  
- Spechmmer:
  
  ![spechmmerCPIpng](file://C:\Users\Jay\Desktop\ERGASIA_MASTER\Ergasia%202\graphs\spechmmer_CPI.png?msec=1669989967041)
  

# Βήμα 3

Παίρνοντας υπόψιν τις παραμέτρους του βήματος δύο προκειμένου να βελτιστοποιήσουμε το κόστος/απόδοση , καταλήξαμε στα εξής συμπεράσματα. Ξεκινώντας με τις L1 cache και L2 cache υπάρχει μια αναλογία 4/1 ως προς τη ταχύτητα τους (η L1 είναι 4 φορές πιο γρήγορη) γι΄αυτό θα θέσω το κόστος της L1 να είναι τετραπλάσιο της L2 . Όσον αφορά την επίδοσή τους παρατηρούμε μέσω του προηγούμενου ερωτήματος πως η L1 (d cache και i cache d) επηρεάζει το CPI μερικών από των παραπάνω bencmarks, όμως σύμφωνα με δεδομένα έχουμε πως τα σφάλματα της L1 (missfires) οφείλονται κατα 75% σε instruction references και 25% σε data references. Το μέγεθος cache line εξαρτάται από τις εντολές τις οποίες θέλουμε να τρέξουμε , ένα πολύ μεγάλο μέγεθος δεν είναι απαραίτητα χρήσιμο ενώ ταυτόχρονα είναι πολυδάπανο, αντίστοιχα ένα μικρό μέγεθος μπορεί να αυξήσει αρκετά την πολυπλοκότητα του κυκλώματος , άρα να επηρεάσει αρνητικά την ταχύτητα και απόδοση του κυκλώματος. Η αύξηση του cache line size, ανάλογα το simulation, μπορεί να εχεί μια σημαντική βελτίωση του CPI, αύτο είναι ιδιαίτερα εμφανές στο benchmark specsjeng. Όσο μεγαλύτερο το CPI του κάθε benchmark τόσο πιο εμφανής ήταν η επίδραση του cache line size. Επομένως επιζητούμε μια μεγάλη τιμή για το μέγεθος cache line σε benchmarks με υψηλό CPI και μια σχετικά χαμηλή τιμή σε αυτά με μικρό CPI (κοντά στο 1). Τέλος τα L1 associativity και L2 associativity είναι αυτά που ευθύνονται για την πολυπλοκότητα , οπότε παρόλο το μέτριο κόστος τους δεν επιθυμούμε πολύ μεγάλη τιμή. Σύμφωνα με τα παραπάνω καταλήγουμε σε μια συνάρτηση κόστους που είναι ως εξής:

**Κόστος** = 16L1( icache size + dcache size) + 4L2 cache size + 6cache line size + 6L1( icache assoc + dcache assoc) + 2L2 cache assoc

Για την βελτιστοποίηση των benchmark έχω πως:

- Specbzib: Παρατηρώ ότι έχω την ίδια βελτίωση του CPI όταν αυξάνω το L2 και το L1. Επομένως λόγο του κόστους επιλέγω να αυξήσω την L2 διότι είναι πιο φθηνή. Το κόστος είναι **16**.
  
- Speclibm: Αυξάνω το cache line size κατα 64kB, το κόστος είναι **384**. Το CPI βελτιώνεται κατα 0.912. Πολύ καλή βελτίωση!
  
- Specmcf: Αυξάνω το L1 icache κατά 32kB επομένως το κόστος είναι **512**. Πετυχαίνω βελτίωση του CPI κατα 0.183.
  
- Specsjeng: Αυξάνω το cache line size κατα 64kB, το κόστος είναι **384**, με καινούριο CPI 6.799471, εξαιρετική βελτίωση (περιπου 3.5) για χαμηλό κόστος.
  
- Spechmmer: Αυξάνω το cache line size κατα 64kB και L1 dcache κατα 64kB, με κόστος **1024 + 384**. Μεγάλο κόστος για όχι τόσο σημαντική βελτίωση, ο CPI του benchmark αυτού είναι ήση πολύ κοντά στο 1. Καλύτερα να μην αλλάξω τίποτα.
