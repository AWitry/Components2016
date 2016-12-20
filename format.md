## Format-Spezifikation

Nachrichten weisen folgende Felder auf:
* 'request-id': string. Generierte GUID. Bezeichner f�r den urspr�nglichen Auftrag. Auftragnehmer und weiterleitende Broker geben der Wert unver�ndert zur�ck/weiter.
* 'sender': string. URI des Auftraggebers. Bleibt beim Weiterleiten durch Broker unver�ndert. Andernfalls wird die eigene URI eingetragen.
* 'sudoku': int[N*N]. N*N gro�e Integer Matrix, wobei N = K*K (etwa N=9 := K=3 Bl�cke mal K=3 Zellen). G�ltige Werte sind 0 (undefiniert/leer) und 1 bis N. Die Matrix ist Zeilenweise in das Array abgebildet.
* 'instruction': string:
  * 'register:*': registriere mich als * aus {'broker','gui','solver','generator'}
  * 'unregister': entferne mich aus der Registrierung. Kann auch vom Broker gesendet werden, nachdem 'pong'-Nachrichten ausbleiben.
  * 'ping': lebst du noch? Lokale Komponente antwortet mit 'pong'
  * 'pong': ich lebe noch
  * 'solve': l�se das R�tsel
  * 'solved:*': R�tsel wurde gel�st mit Ergebnis * aus {'one', 'many', 'impossible'}
  * 'generate:*': generiere R�tsel mit Schwierigkeit * (Zahl). Absender muss 'soduko'-Matrix mit N*N Nullen f�llen.
  
  
Idealerweise sollten Empf�nger damit umgehen k�nnen, wenn in Paketen Felder fehlen oder zu viel sind.
Felder mit ung�ltigen/unerwarteten Namen oder Werten sollten ggf. gelogt/ausgegeben aber ignoriert werden.
Broker sollten Pakete mit allen erhaltenen Feldern weiterleiten (auch mit unerwarteten/unverst�ndlichen).
