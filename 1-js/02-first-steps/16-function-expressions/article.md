# Function expression

In JavaScript, una funzione non è una "struttura magica del linguaggio", ma un valore speciale.

La sintassi che abbiamo utilizzato finora viene chiamata *Dichiarazione di Funzione*:

```js
function sayHi() {
  alert( "Hello" );
}
```

E' disponibile un'altra sintassi per creare una funzione, chiamata *function expression*.

<<<<<<< HEAD
La sintassi:
=======
It allows to create a new function in the middle of any expression.

For example:
>>>>>>> 8d04d0d2db97276dbb2b451c30a7bd3e05d65831

```js
let sayHi = function() {
  alert( "Hello" );
};
```

<<<<<<< HEAD
Qui la funzione viene esplicitamente creata ed assegnata ad una variabile, proprio come un qualsiasi altro valore. Non ha importanza come la funzione viene definita, è solo un valore salvato nella variabile `sayHi`.

Il significato di questo esempio è lo stesso di: "crea una funzione e mettila dentro la variabile `sayHi`".
=======
Here we can see a variable `sayHi` getting a value, the new function, created as `function() { alert("Hello"); }`.

As the function creation happens in the context of the assignment expression (to the right side of `=`), this is a *Function Expression*.

Please note, there's no name after the `function` keyword. Omitting a name is allowed for Function Expressions.

Here we immediately assign it to the variable, so the meaning of these code samples is the same: "create a function and put it into the variable `sayHi`".

In more advanced situations, that we'll come across later, a function may be created and immediately called or scheduled for a later execution, not stored anywhere, thus remaining anonymous.

## Function is a value

<<<<<<< HEAD
Let's reiterate: no matter how the function is created, a function is a value. Both examples above store a function is `sayHi` variable.
>>>>>>> 8d04d0d2db97276dbb2b451c30a7bd3e05d65831
=======
Let's reiterate: no matter how the function is created, a function is a value. Both examples above store a function in the `sayHi` variable.
>>>>>>> 3c934b5a46a76861255e3a4f29da6fd54ab05c8c

Possiamo anche mostrarne il valore usando `alert`:

```js run
function sayHi() {
  alert( "Hello" );
}

*!*
alert( sayHi ); // mostra il codice della funzione
*/!*
```

Da notare che l'ultima riga di codice non esegue la funzione, perché non ci sono parentesi dopo `sayHi`. Ci sono linguaggi di programmazione in cui la semplice menzione del nome di una funzione ne causa l'esecuzione; JavaScript non funziona così.

In JavaScript, una funzione è un valore, quindi possiamo lavorarci come con un qualsiasi altro valore. Il codice sopra ne mostra la sua rappresentazione in stringa, cioè il codice contenuto dentro la funzione.

E' chiaramente un valore speciale, poiché possiamo richiamarla con `sayHi()`.

Ma rimane comunque un valore, e come tale possiamo trattarlo.

Possiamo copiare la funzione in un'altra variabile:

```js run no-beautify
function sayHi() {   // (1) creazione
  alert( "Hello" );
}

let func = sayHi;    // (2) copia

func(); // Hello     // (3) esegue la copia (funziona)!
sayHi(); // Hello    //     anche questa continua a funzionare (perché non dovrebbe?)
```

Quello che succede, nel dettaglio, è:

1. La dichiarazione di funzione `(1)` crea la funzione e la inserisce nella variabile denominata `sayHi`.
2. La linea `(2)` la copia nella variabile `func`.

<<<<<<< HEAD
    Ancora una volta: non ci sono parentesi dopo `sayHi`. Se ci fossero state, allora `func = sayHi()` avrebbe inserito *il risultato della chiamata* `sayHi()`, non *la funzione* `sayHi`.
3. Adesso la funzione può essere richiamata sia con `sayHi()` che con `func()`.

Avremmo anche potuto utilizzare, nella prima riga, una function expression per dichiarare `sayHi`:
=======
We could also have used a Function Expression to declare `sayHi`, in the first line:
>>>>>>> 8d04d0d2db97276dbb2b451c30a7bd3e05d65831

```js
let sayHi = function() { // (1) create
  alert( "Hello" );
};

let func = sayHi;
// ...
```

Tutto funzionerebbe ugualmente. Risulta anche più chiaro cosa sta succedendo, giusto?


````smart header="Perché c'è un punto e virgola alla fine?"
Vi starete chiedendo perché con la function expression bisogna mettere `;` alla fine, mentre con la dichiarazione di funzione non serve:

```js
function sayHi() {
  // ...
}

let sayHi = function() {
  // ...
}*!*;*/!*
```

<<<<<<< HEAD
La risposta è semplice:
- Non c'è bisogno di `;` alla fine dei blocchi di codice che utilizzano una sintassi del tipo `if { ... }`, `for {  }`, `function f { }` etc.
- Una function expression viene utilizzata all'interno di un'istruzione: `let sayHi = ...;`, come valore. Non è un blocco di codice. Quindi il `;` è consigliato al termine dell'istruzione, indipendentemente dal valore.  Il punto e virgola non è collegato alla function expression; più semplicemente, termina un'istruzione.
=======
The answer is simple: a Function Expression is created here as `function(…) {…}` inside the assignment statement: `let sayHi = …;`. The semicolon `;` is recommended at the end of the statement, it's not a part of the function syntax.

The semicolon would be there for a simpler assignment, such as `let sayHi = 5;`, and it's also there for a function assignment.
>>>>>>> 8d04d0d2db97276dbb2b451c30a7bd3e05d65831
````

## Callback functions (funzioni richiamate)

Diamo un'occhiata ad ulteriori esempi di passaggio di funzione come valore e utilizzo della sintassi function expression.

Scriveremo una funzione `ask(question, yes, no)` con tre parametri:

`question`
: Il testo della domanda

`yes`
: Funzione da eseguire se la risposta è "Yes"

`no`
: Funzione da eseguire se la risposta è "No"

La funzione dovrebbe richiedere la `question` e, in base alla risposta dell'utente, chiamare `yes()` o `no()`:

```js run
*!*
function ask(question, yes, no) {
  if (confirm(question)) yes()
  else no();
}
*/!*

function showOk() {
  alert( "You agreed." );
}

function showCancel() {
  alert( "You canceled the execution." );
}

// utilizzo: funzioni showOk, showCancel vengono passate come argomenti ad ask
ask("Do you agree?", showOk, showCancel);
```

Queste funzioni possono essere molto utili. La principale differenza tra un'implementazione realistica e gli esempi sopra è che le funzioni "reali" utilizzano modalità più complesse per interagire con l'utente, non un semplice `confirm`. In ambiente browser, queste funzioni mostrano spesso delle finestre molto carine per gli input dell'utente. Ma questo è un altro discorso.

**Gli argomenti `showOk` e `showCancel` della `ask` sono chiamati *funzioni di richiamo* o semplicemente *callbacks*.**

L'idea è di passare una funzione e di "richiamarla" più tardi se necessario. Nel nostro caso `showOk` diventa la callback per la risposta "yes", e `showCancel` per la risposta "no".

Possiamo utilizzare una function expression per scrivere la stessa funzione più concisamente:

```js run no-beautify
function ask(question, yes, no) {
  if (confirm(question)) yes()
  else no();
}

*!*
ask(
  "Do you agree?",
  function() { alert("You agreed."); },
  function() { alert("You canceled the execution."); }
);
*/!*
```


Qui la funzione viene dichiarata dentro alla chiamata di `ask(...)`. Queste non hanno nome, e perciò sono denominate *anonime*. Queste funzioni non sono accessibili dall'esterno di `ask` (perché non sono assegnate a nessuna variabile), ma è proprio quel che vogliamo in questo caso.

Questo tipo di codice comparirà nei nostri script molto naturalmente: è nello spirito di JavaScript.


```smart header="Una funzione è un valore che rappresenta un \"azione\""
I valori regolari come le stringhe o i numeri rappresentano *dati*.

Una funzione può anche essere vista come un'*azione*.

Possiamo passarla tra le variabili ed eseguirla quando vogliamo.
```


## Function expression vs Dichiarazione di Funzioni

Cerchiamo di elencare le differenze chiave tra Dichiarazioni ed Espressioni di Funzione.

Primo, la sintassi: come  distinguerle nel codice.

- *Dichiarazione di funzione:* una funzione, dichiarata come un'istruzione separata, nel flusso principale del programma.

    ```js
    // Dichiarazione di funzione
    function sum(a, b) {
      return a + b;
    }
    ```
- *Function expression:* una funzione, creata all'interno di un'espressione o all'interno di un altro costrutto. Qui, la funzione è creata alla destra dell' "espressione di assegnazione" `=`:
    
    ```js
    // function expression
    let sum = function(a, b) {
      return a + b;
    };
    ```

La differenza più subdola è *quando* una funzione viene creata dal motore JavaScript.

**Una function expression viene creata quando l'esecuzione la raggiunge ed è utilizzabile solo da quel momento in poi.**

Quando il flusso di esecuzione passa alla destra dell'operatore di assegnamento `let sum = function…` , la funzione viene creata e, a partire da questo momento, può essere utilizzata (assegnata, chiamata, etc...).

Una dichiarazione di funzione funziona diversamente.

**Una dichiarazione di funzione è utilizzabile nell'intero script/blocco di codice.**

In altre parole, quando JavaScript si *prepara* ad eseguire lo script o un blocco di codice, come prima cosa cerca le dichiarazioni di funzione e le crea. Possiamo pensare a questo processo come a uno "stage di inizializzazione".

E' solo dopo che tutte le dichiarazioni di funzione sono state processate che l'esecuzione potrà procedere.

Come risultato, una funzione creata tramite una dichiarazione di funzione può essere richiamata anche prima della sua definizione.

Ad esempio, il seguente codice funziona:

```js run refresh untrusted
*!*
sayHi("John"); // Hello, John
*/!*

function sayHi(name) {
  alert( `Hello, ${name}` );
}
```

La dichiarazione di funzione `sayHi` viene creata quando JavaScript si sta preparando ad eseguire lo script ed è visibile in ogni suo punto.

...Se fosse stata una function expression, non avrebbe funzionato:

```js run refresh untrusted
*!*
sayHi("John"); // errore!
*/!*

let sayHi = function(name) {  // (*) nessuna magia
  alert( `Hello, ${name}` );
};
```

Le espressioni di funzione sono create quando l'esecuzione le incontra. In questo esempio avverrà solo alla riga `(*)`. Troppo tardi.

**In *strict mode*, quando una dichiarazione di funzione viene fatta all'interno di un blocco di codice sarà visibile ovunque all'interno del blocco, ma non al suo esterno.**

Qualche volta è comodo dichiarare funzioni locali, utili in un singolo blocco. Ma questa caratteristica potrebbe causare problemi.

Ad esempio, immaginiamo di aver bisogno di dichiarare una funzione `welcome()` (la utilizzeremo più avanti) in base ad un parametro `age` che valuteremo durante il *runtime*.

Il codice sotto non funziona:

```js run
let age = prompt("What is your age?", 18);

// dichiarazione di funzione condizionale
if (age < 18) {

  function welcome() {
    alert("Hello!");
  }

} else {

  function welcome() {
    alert("Greetings!");
  }

}

// ...utilizzo successivo
*!*
welcome(); // Errore: welcome non è definita
*/!*
```

Questo accade perché una dichiarazione di funzione è visibile solamente all'interno del blocco di codice in cui è stata definita.

Un altro esempio:

```js run
let age = 16; // prendiamo 16 come esempio

if (age < 18) {
*!*
  welcome();               // \   (esegue)
*/!*
                           //  |
  function welcome() {     //  |  
    alert("Hello!");       //  |  Dichiarazione di funzione disponibile
  }                        //  |  ovunque nel blocco in cui è stata dichiarata
                           //  |
*!*
  welcome();               // /   (esegue)
*/!*

} else {

  function welcome() {     
    alert("Greetings!");
  }
}

// Qui siamo all'esterno delle parentesi graffe, 
// quindi non possiamo vedere le dichiarazioni di funzione fatte al suo interno.

*!*
welcome(); // Errore: welcome non è definita
*/!*
```

Cosa possiamo fare per rendere visibile `welcome` all'esterno del blocco `if`?

Il giusto approccio è quello di utilizzare una function expression ed assegnarla ad una variabile `welcome`, che viene dichiarata all'esterno di `if` ed ha quindi la corretta visibilità.

Ora funziona:

```js run
let age = prompt("What is your age?", 18);

let welcome;

if (age < 18) {

  welcome = function() {
    alert("Hello!");
  };

} else {

  welcome = function() {
    alert("Greetings!");
  };

}

*!*
welcome(); // ora funziona
*/!*
```

Oppure possiamo semplificarla con l'utilizzo dell'operatore `?`:

```js run
let age = prompt("What is your age?", 18);

let welcome = (age < 18) ?
  function() { alert("Hello!"); } :
  function() { alert("Greetings!"); };

*!*
welcome(); // ora funziona
*/!*
```


```smart header="Quando conviene scegliere una dichiarazione di funzione piuttosto di una function expression?"
Come regola fondamentale, quando abbiamo la necessità di dichiarare una funzione, la prima opzione da considerare è la dichiarazione di funzione. Fornisce maggiore libertà per quanto riguarda l'organizzazione del codice, poiché possiamo utilizzare la funzione anche prima della sua dichiarazione.

Risulta anche più facile vedere `function f(…) {…}`, nel codice, piuttosto di `let f = function(…) {…}`. La dichiarazione di funzione è più facile da individuare.

...Ma se per qualche ragione la dichiarazione di funzione non si applica bene al caso in questione (abbiamo visto degli esempi, sopra), allora la function expression può essere un'alternativa.
```

## Riepilogo

- Le funzioni sono valori. Possono essere assegnate, copiate o dichiarate in qualsiasi punto del codice.
- Se la funzione viene dichiarata come un blocco "separato" dal flusso d'esecuzione principale del codice, tale definizione viene chiamata "dichiarazione di funzione".
- Se la funzione viene definita tramite un'espressione, viene chiamata "function expression".
- Le dichiarazioni di funzione vengono processate prima che il blocco di codice dove sono state definite sia raggiunto.
- Le function expression vengono processate quando il flusso d'esecuzione del codice principale le raggiunge.

Nella maggior parte dei casi, quando abbiamo bisogno di dichiarare una funzione una dichiarazione di funzione è preferibile poiché è visibile anche prima della sua dichiarazione. Questo ci fornisce più flessibilità nell'organizzazione del codice, e solitamente risulta più leggibile.

Dovremmo, quindi, utilizzare una function expression solo quando una dichiarazione di funzione non è adatta a un caso specifico. Abbiamo visto un paio di esempi in questo capitolo, e ne vederemo altri in futuro.
