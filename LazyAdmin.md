# TryHackMe - LazyAdmin

**Data:** 2025-10-02  
**Poziom:** Easy  
**Kategoria:** Web

---

## 1. Opis

Zdobycie flagi przez znalezienie luki w url strony i pobranie pliku zawierającego wrażliwe dane

---

## 2. Kroki rozwiązania
1. nmap -sS -A - oN do sprawdzenia otwartych portów. Otwarte porty 80 i 22
2. użycie ffuf do znalezienia adresu content który ujawnia użycie sweetRice cms
3. skorzystanie z searchsploit aby znaleźć błędy w oprogramowaniu.
4. znalezienie arpitrary file update i zapisanie exploitu na komputerze. exploit potrzebuje loginu oraz hasła użytkownika 
5. zastosowanie ffuf do do adresu /content co pokazuje że dalsza część url którą można wykorzystać jest inc. Inc pozwala zapisać plik z buckup'em
6. w pliku buckup jest zapisana nazwa i hasło które były potrzebne do exploitu 
7. hasło trzeba odkodować bo jest zahashowane 
8. następnie używamy exploitu który wymaga od nas url loginu hasła oraz reverseshella
9. exploit tworzy nowe url za którego pomocą przy użyciu curl i nasłuchując odpowiedni port używając nc -nvlp dzięki czemu wchodzimy na maszyne
10. umocniamy nasłuch za pomocą komendy pythin3 -c "import pty;pty.spawn('/bin/bash')" stty raw -echo oraz export TERM=xterm 
11. pierwsza flaga jest na /home/itguy
12. przy pomocy sudo -l dowiadujemy się że można skorzystać z perl scrip na root
13. perl script uaktywania kolejny plik o nazwie copy.sh
14. copy.sh może być nadpisany przez każdego co pozwala użyć własnego revershella 
15. używając nc -nvlp ponownie oraz pliku copy.sh otrzymujemy dostęp do roota gdzie znajduje się kolejna i ostania flaga
