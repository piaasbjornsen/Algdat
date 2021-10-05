markdown
# Rotfaste trestrukturer 
## Binære heap 
Den binære heap datastrukturen er en liste som vi kan se på som et nesten komplett binærtre. Hver node i treet korresponderer til et element i listen. Treet er helt fylt i alle nivåer, med (mulig) unntak av det laveste nivået, som er fylt fra venstre mot høyre. 

En binær heap er et komplett binnært tre, med noen ekstre egenskaper, kjent som heap egenskaper. Det finnes to forskjellige varianter av heaps; *max-heap* og *min-heap*. Egenskapene til heapen kommer an på hvilken type det er, og er videre forklart under. 

Roten til treet er A[0]. Gitt en index til en node, kan vi lett finne indeksen til dets forgjenger (parent), venstre og høyre barn.

![binary heap](images/binary-heap.png)
*MAX-HEAP*

### Finne parent, left og rigth child til en node i 

```java
parent(i){                          //Finner index til parent av i
    int parentIndex = ⌊i/2⌋;
}

leftChild(i){                       //Finner index til venstre barn av i
    int leftChildindex = 2*i;
}

rigthChild(i){                      //Finner index til høyre barn av i 
    int rigthChildIndex = 2*i+1;
}
```

### To typer heaps
Det finnes to typer binære heaps. I begge typene tilfredstiller verdiene i nodene en heap-egenskap, som avhenger av typen heap:

* **Max-heap egenskapen**:
    * For hver node *i* &ne; 0 er `A[parent(i)] ≥  A[i]`
      * Altså er veriden til  parent alltid høyere enn til barnet 
    * En nodes verdi er på det meste sin forgjengers verdi - dvs største element ligger i roten.
* **Min-heaps egenskapen**:
  * For hver node *i* &ne; 0 `A[parent(i)] ≤ A[i]` 
    * Altså er verdien til parent alltid lavere enn til barnet 
  * En nodes verdi er på det misnte sin forgjenger verdi - dvs. minste element ligger i roten 

![min and max heap](images/max%20and%20min%20heap%20.png)

Dersom vi ser på en heap som et tre, definerer vi høyden til en node i treet til den lengste enkle veien fra noden til en løvnode, og vi definerer *høyden* til treet til å være høyden til roten.

> Siden en heap av n elementer er basert på et komplett binært tre, er dens høyde θ(log n), som vi ser igjen på tradisjonelle heap-prosedyrer 

## Heap operasjoner 
### MAX_HEAPIFY(A, i)
Er en veldig vanlig operasjon på en allerede eksisterende heap. Den omorganiserer en heap slik at den opprettholder sine egenskaper. 

```java
MAX-HEAPIFY(A,i)
1   l = left(i)                  //Left child
2   r = right(i)                //Right child
3   if l ≤ A.heap-size and A[l] > A[i]
4       largest = 1 
5   else largest = i
6   if r ≤ A.heap-size and A[r] > A[largest]
7       largest = r
8   if largest ≠ i
9       exchange A[i] with A[largest]
10      MAX-HEAPIFY(A, largest)
```

*A: input array  
i: index of the node*

>#### *Kjøring av MAX-HEAPIFY*
>* På hvert steg velges det største elementet av `A[i]`, `A[left(i)]`og `A[right(i)]`, og dets indeks blir lagret som largest. Dersom `A[i]` er størst vil subtreet på node i allerede være en MAX-HEAP og prosedyren terminerer. 
>* Hvis ikke er en av de to barna det største elementet, og bytter plass på `A[i]` og `A[largest]`, som gjør at node i og dets barn tilfredsstiller MAX-HEAP egenskapen. 
>* Noden med indeks largest har nå den originale verdien til `A[i]`, og derfor kan det hende at subtreet med rot *largest* muligens bryter med max-heap egenskapen. Derfor kaller vi MAX-HEAPIFY rekursivt på subtreet

For å bygge en heap med max-heap egenskapen, kaller vi på prosedyren MAX-HEAPIFY. Når den kalles antar algoritmen at binærtreet med røtter i `left(i)` og `rigth(i)`, er max_heaps, men at A[i] kanskje er mindre enn sine barn, som bryter med heap-egenskapen. Max-heapify lar verdien til A[i] *"flyte ned"* i max-heapen slik at subtreet med rot p åindex i holder heap-egenskapen.

**Kjøretid**:
* `T(n) ≤ T(2n/3) + θ(1)`, som med master teoremet gir `T(n) = O(log n)`
* Alternativt kan vi karakterisere kjøretiden på en node med høyde h som O(h)

## Bygging av heaps
Vi kan bruke *MAX_HEAPIFY* på en bottomup måte for å konvertere en liste 
*Flere kilder*: https://www.baeldung.com/cs/binary-tree-max-heapify