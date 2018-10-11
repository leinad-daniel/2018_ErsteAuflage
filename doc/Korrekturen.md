## Ein paar Korrekturen...
Ich kann euch gar nicht sagen, wie oft alleine **ich** das Manuskript durchgegangen bin – wieder und wieder und wieder, und dann kamen die Korrektoren, die Lektoren, sie alle... und doch hat sich der ein oder andere Fehlerteufel eingeschlichen.

Das sei unvermeidbar, habe ich mir sagen lassen; genervt bin ich trotzdem :unamused: Um es für euch, meine lieben Leser, möglichst transparent zu halten gibt es nun diese Datei als Referenz. Meldet, wenn euch etwas auffällt: gerne im [Issue Tracker](https://github.com/smarthome-mit-openhab2/2018_ErsteAuflage/issues) oder erstellt, wenn ihr möchtet, [Pull Requests](https://github.com/smarthome-mit-openhab2/2018_ErsteAuflage/pulls) – schlussendlich hilft das allen.

Im Code werde ich die Korrekturen natürlich ebenfalls vornehmen; die Seitenzahlen beziehen sich jeweils auf die gedruckte Ausgabe des Buches.

### Kapitel 6
#### Listing 6.19 (S. 129)
```diff
rule "Status Summary Aktuell"
when
  Item Aussentemperatur changed or
  Item Wetterlage changed
then
  var Number temp = ((Aussentemperatur.state as DecimalType).floatValue)
- var lage = transform("MAP", "Wetterlage.map", Vorhersage_Wetterlage.state.toString)
+ var lage = transform("MAP", "Wetterlage.map", Wetterlage.state.toString)
  var String Ausgabe = String::format("%s bei %.1f°C", lage, temp)
  SummaryStateAktuell.postUpdate(Ausgabe)
end
```
<small>*(Dank an Frank S.)*</small>

### Kapitel 8
#### Listing 8.9 (S. 156)
```diff
Text item=fbDslStatus label="FRITZ!Box [%s]" {
  // FRAME Anwesenheit
  // FRAME Anrufbeantworter

  Frame label="Leitungswerte" {
-   Text item=fbExterneIp
+   Text item=fbExternalIp
     label="Externe IP-Adresse [%s]"
     icon="line"
     visibility=[fbDslStatus == "Up"]

-   Text item=fbDslExterneIp
+   Text item=fbExternalIp
     label="Keine DSL-Verbindung [⛔️]"
     icon="error"
     visibility=[fbDslStatus != "Up"]

   Text item=fbDslUpstream
     label="Upstream [%s mbit/s]
     icon="line"
     visibility=[fbDslStatus == "Up"]

   Text item=fbDslUpstream
     label="Upstream N/A []"
     icon="error"
     visibility=[fbDslStatus != "Up"]

   Text item=fbDslDownstream
     label="Downstream [%s mbit/s]"
     icon="line"
     visibility=[fbDslStatus == "Up"]

   Text item=fbDslDownstream
     label="Downstream N/A []"
     icon="error"
     visibility=[fbDslStatus != "Up"]
  } // END Frame Leitungswerte
} // END FRITZ!Box
```
<small>*Dank an Michael G.*</small>
