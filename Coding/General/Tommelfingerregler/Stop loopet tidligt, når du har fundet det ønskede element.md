Hvis du kun er interesseret i at finde én værdi i et array, kan du bruge `break` for at afslutte loopet, så snart du har fundet det ønskede element. Dette optimerer din kode ved at forhindre unødvendige iterationer.

**Eksempel:**
```java
for (Song s : Playlist) {
    if (s.equals(søgtSong)) {
        // Sangen blev fundet, gør noget med s
        System.out.println("Sangen blev fundet!");
        break;  // Stopper løkken, når sangen er fundet
    }
}
```