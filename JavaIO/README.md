
În Java, biblioteca NIO (New Input/Output) introduce conceptele de canale (channels) și bufere (buffers), care oferă o modalitate mai eficientă și mai flexibilă de a lucra cu operațiuni de intrare/ieșire (I/O), comparativ cu fluxurile de intrare/ieșire standard (streams) din pachetul java.io.

Canale (Channels)
Un canal reprezintă o conexiune deschisă către o entitate capabilă de I/O, cum ar fi un fișier sau un socket. Canalele pot fi de mai multe tipuri, inclusiv:

FileChannel: Pentru citirea, scrierea și manipularea fișierelor.
SocketChannel: Pentru conexiuni de rețea TCP.
ServerSocketChannel: Pentru ascultarea și acceptarea conexiunilor de rețea TCP.
DatagramChannel: Pentru comunicații de rețea UDP.
Principalele avantaje ale canalelor:

Acces Bidirecțional: Spre deosebire de fluxurile tradiționale care sunt fie pentru citire, fie pentru scriere, canalele pot fi, în general, folosite pentru ambele operațiuni.
Non-blocking I/O: Canalele pot fi configurate în moduri neblocaj, permițând unui thread să continue executarea în timp ce așteaptă ca operațiunea de I/O să fie completată.
Performanță Îmbunătățită: Pot oferi performanțe mai bune pentru operațiunile de I/O, în special pentru citirea și scrierea în fișiere mari sau în comunicațiile de rețea.
Bufere (Buffers)
Un buffer în Java NIO este un container de date. Este folosit pentru stocarea temporară a datelor în timp ce sunt transportate între canale. Buferele sunt de obicei folosite împreună cu canalele pentru a eficientiza procesul de I/O.

Există diferite tipuri de bufere în funcție de tipul de date pe care îl conțin, cum ar fi ByteBuffer, CharBuffer, IntBuffer, etc.

Caracteristicile cheie ale unui buffer includ:

Capacitate: Numărul maxim de elemente pe care bufferul îl poate conține.
Limită: Prima poziție care nu trebuie citită sau scrisă.
Poziție: Poziția curentă a următorului element care va fi citit sau scris.
Flip/Clear/Compact/...: Buferele au metode pentru manipularea și resetarea datelor, cum ar fi flip() pentru pregătirea pentru citire, clear() pentru resetarea întregului buffer, sau compact() pentru comprimarea datelor neconsumate.
Utilizarea combinată a canalelor și a buferelor în Java NIO permite un control mai precis și mai eficient al datelor în timpul operațiunilor de I/O, făcându-le potrivite pentru aplicații cu cerințe de performanță ridicate, cum ar fi servere web, baze de date și aplicații de procesare a fișierelor mari.
