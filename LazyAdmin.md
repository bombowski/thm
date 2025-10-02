# TryHackMe - LazyAdmin

**Data:** 2025-10-02  
**Poziom:** Easy  
**Kategoria:** Web

---

## 1. Opis
Przykład: „Pokój uczy podstaw enumeracji serwera WWW i prostych ataków SQLi.”
Zdobycie flagi przez wejśćia za pośrednictwem reverse shell wgranego na strone oraz użycie pyps by dostać się do roota

---

## 2. Kroki rozwiązania
1. nmap do sprawdzenia otwartych portów. port 85 otwarty
2. sprawdzenie na stronie wersji oprogramowania
3. skorzystanie z podstawowego logina oraz hasła dla concrete cms 8.5.2
4. dodanie do akceptowalnych plików rozszerzenia .php
5. wgranien na strone reverseshell i nasłuchiwanie przez nc -nvlp co powoduje wejście na komputer zakażony ale wejśćie na konto www-data
6. trzeba dostać się do użytkownika pozwala na to przeszukanie pilków w confugu database.php znajduje się hasło użytkownika toad
7. w ten sposób można dostać pierwszą flagę
8. gdy użyjemy komendy env pojawi się token którego deszyfracja pozwoli na zalogowanie się do użytkownika mario
9. pobieramy na własny komputer pspy oraz stawiamy serwer python3 -m http.server 80 co pozwala na pobranie zawartośći w tym przypadku pspy
10. gdy pspy jest zainstalowane musimy zmienić jego wartość w systemie za pomocą chmod -x pspy
11. pozwoli to na znalezienie lokalizacji pliku który pobiera wartości z /app/castle/application/counter.sh
12. pozwala to na zmodyfikowanie własnej ścieżki
13. stawiamy serwer tym razem na porcie 85 oraz tworzymy taką samą lokalizacje pliku counter.sh
14. pobieramy do niego rever shell na basha
15. nadpisujeemy hosta echo '10.8.34.229 mkingdom.thm' > /etc/hosts
16. dzięki temu pobiera to z naszego serwera
17. dzięki wcześniejszemu zrobienia odpowiedniej ścieżki automatycznie pobiera nam zakażony plik co pozawla na wejście do roota
18. nnastępną flagę musimy przenieść do folderu tmp i ją odczytać
