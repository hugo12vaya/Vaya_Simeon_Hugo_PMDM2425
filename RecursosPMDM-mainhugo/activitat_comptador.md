
# Activitat: Comptador i Arxius Relacionats

## Introducció

En aquesta tasca anem a fer un repàs pràctic i reflexiu sobre els aspectes més rellevants de la unitat, tals com:

- Estructura d'un projecte i fitxers principals
- Activitats: Què són i com s'organitzen
- Anàlisi del cicle de vida d'una activitat
- Manteniment de l'estat mitjançant Bundles
- Components d'arquitectura d'Android: MVVM
- Conceptes i forma de treball de Jetpack Compose

## Lliurament

Fruit de la investigació i treball, hem creat un repositori a GitHub que inclou una memòria en format Markdown amb els passos seguits, resultats obtinguts i conclusions extretes. Hem documentat i explicat de manera justificada les diferents solucions aplicades. També hem inclòs els tres projectes de comptador amb les modificacions proposades, documentant-los en un fitxer `README.md`.

---

## Bloc 1: Activitats sobre el comptador

### Anàlisi de l'estructura del projecte

Aquest projecte és un **Comptador** basat en una estructura típica d'Android. A continuació, es mostra la seva estructura bàsica:

```
/src/main
    /java
        /com/example/comptador
            - MainActivity.kt
    /res
        /layout
            - activity_main.xml
        /values
            - strings.xml
```

- **MainActivity.kt**: Conté la lògica principal de l'aplicació.
- **activity_main.xml**: Definició de la interfície d'usuari, incloent botons i text.
- **strings.xml**: Definicions de cadenes de text utilitzades en l'app.

### Modificacions inicials

- **Reemplaçar el layout**: Hem substituït el layout original pel subministrat.
- **Afegir funcionalitat als botons**: Hem implementat el codi necessari per dotar de funcionalitat els botons de "decrementar" i "resetejar".

### Activitats sobre el cicle de vida i pèrdua d'estat

Hem investigat què passa amb l'aplicació durant els canvis d'orientació del dispositiu. Hem utilitzat els següents mètodes de la classe `Activity`:

- `onStart()`
- `onResume()`
- `onPause()`
- `onStop()`
- `onRestart()`
- `onDestroy()`
- `onSaveInstanceState(Bundle)` i `onRestoreInstanceState(Bundle)`

Aquestes són algunes de les implementacions afegides als mètodes per tal de depurar el cicle de vida de l'aplicació:

```kotlin
override fun onStart() {
    super.onStart()
    Log.d(TAG, "Al mètode onStart")
}
```

Per a solucionar el mal funcionament davant els canvis d'orientació, hem gestionat l'estat mitjançant `Bundle` en els mètodes `onSaveInstanceState` i `onRestoreInstanceState`.

### Intents entre activitats

Hem afegit una segona activitat, que mostra el valor actual del comptador. Aquesta activitat inclou un botó per tancar-la i tornar a l'activitat principal.

Per crear aquesta nova activitat, hem creat:

1. **Un fitxer XML** per definir el layout.
2. **Un fitxer Kotlin** per gestionar la lògica d'aquesta activitat.

---

## Bloc 2: Comptador amb MVVM

En aquesta part, hem fet les modificacions necessàries per tal que l'aplicació del comptador pugui decrementar i resetejar el valor, utilitzant l'arquitectura **MVVM** (Model-View-ViewModel).

### Modificacions realitzades

- **ViewModel**: S'han afegit les funcions corresponents per gestionar les accions de "decrementar" i "resetejar" el comptador.
- **View**: La interfície ha estat ajustada per interactuar amb les noves funcions del `ViewModel`.

### Reflexió sobre la Intent en MVVM

Hem investigat si, en el cas de MVVM, és necessari passar el valor del comptador mitjançant una `Intent` per a la segona activitat. Després d'explorar la possibilitat, hem conclòs que, utilitzant el mateix `ViewModel` en ambdues activitats, no cal passar el valor explícitament, ja que es pot accedir directament al valor del `ViewModel`.

---

## Bloc 3: Comptador amb Jetpack Compose

Hem començat amb el projecte **ComptadorComposable** proporcionat. Les modificacions realitzades inclouen l'afegit dels botons per:

- **Decrementar el comptador**
- **Resetejar el comptador**

### Implementació

Per organitzar els botons en la interfície, hem utilitzat la funció `Row`, que permet col·locar diversos components en una fila, de manera similar a com `Column` organitza components en una columna.

Exemple de codi utilitzat:

```kotlin
Row{
// - Un boto per incrementar el comptador
    Button(onClick = { comptador++ }) {
        Text(text = "+", fontSize = 34.sp)
    }
    Button(onClick = { comptador-- }) {
        Text(text = "-", fontSize = 34.sp)
    }
    Button(onClick = { comptador==0 }) {
        Text(text = "0", fontSize = 34.sp)
    }
}
```

---

## Conclusions

- Hem après a gestionar el cicle de vida de les activitats i a implementar una solució robusta per evitar la pèrdua d'estat en els canvis d'orientació.
- L'ús del patró **MVVM** ha simplificat la gestió de la lògica de negoci en l'aplicació, facilitant la separació de responsabilitats.
- Hem explorat les capacitats de **Jetpack Compose** per crear interfícies modernes i reactives, simplificant el disseny d'interfícies d'usuari.

